# Helm Repository
This is a repository of all Constellation's Helm Charts, including a library Chart, [`common`])(common/README.md), for keeping things consistent.

## Hosting
This repository is hosted via GitHub Pages. The index and packaged charts are all stored on the `dist` branch.

## Third-party Usage
Please note, this repository is very opinionated. It was designed for Constellation and as such, it makes a lot of assumptions on the conditions that the cluster is going to be running in. Thus, it may set default values that might not be appropriate or might seem strange to third-parties with different cluster conditions.

Luckily, Helm makes it very easy to change options in the output manifests by overriding the default values, even if they are not configurable directly from a `values.yml` file. You are more than welcome to use this repository, but I will not be providing support or taking requests for charts (you are welcome to submit a PR though).