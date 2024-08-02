# Common Chart
This is a library chart used by the rest of the repository to quickly generate different types of resources with a common scaffolding without repetition or a need to correct base changes in multiple places.

It also provides a few common helper functions that might be used by other charts.

## Naming
Calling things a template can get very confusing, very quickly, thanks to Helm demanding the [`templates/`](templates) folder be named so. As a compromise, we'll use the following definitions throughout the rest of the library:
- **Template:** a file located within [`templates/`](templates)
- **Function:** a [Go Templates](https://pkg.go.dev/text/template) `define` declaration that makes a section of templating code useable
- **Helper:** a _Function_ from one of the _Template_ files that can be used by other charts to avoid repetition
- **Resource:** a _Template_ file that combines a _Base_ and _Extension_ to generate a complete manifest
- **Base:** basic structure of a _Resource_, typically only including metadata
- **Extension:** the main content from the dependent chart that will be merged with a _Base_ to form a complete manifest

## Usage
The table below demonstrates the _Functions_ available to the repository and how to use them. Helm uses [Go Template](https://pkg.go.dev/text/template) as the templating engine, so see the docs for help on syntax.

### Resources
These are _Functions_ that are intended to be used directly by other charts. For each _Resource_, there exists a `common.resource` of the same name which serves as an entrypoint for generating that _Resource's_ manifest.

| File name | Resource | Function name |
| --- | --- | --- |
| [`_configmap.yml`](templates/_configmap.yml) | [ConfigMap](https://kubernetes.io/docs/reference/kubernetes-api/config-and-storage-resources/config-map-v1/) | `common.resource.configmap`

### Helpers
A _Helper_ is simply any _Function_ that does NOT output a Kubernetes manifest. These are reusable pieces of code that do very generic but common things, such as merging the output yaml of two _Functions_.

| File name | Arguments | Function name | Purpose |
| --- | --- | --- | --- |
| [`_merge.yml`](templates/_merge.yml) | `list[Function]` | `common.helper.merge` | Merges the given _Functions'_ outputs  |

### Bases
Bases are not supposed to be exposed to the dependent chart. This is because a Base provides the foundational structure of a Resource, and any changes a chart wishes to make should be done using a Resource instead.

Pretty much all Resources intelligently merge the Base and the dependent chart's extension, with the dependent chart taking priority. This means that 
