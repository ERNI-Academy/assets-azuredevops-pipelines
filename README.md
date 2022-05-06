# About assets-azuredevops-pipelines

Continuous Integration / Deployment repository for Azure Pipelines 
This repository contains the needed jobs, config and templates for building and deploying pipelines as code.

Find below the repository structure:

```
.
├── build
│   ├── jobs
│   ├── config
│   └── templates
├── deploy
│   ├── templates
│   └── jobs
└── README.md
```

> `Variables Important Note`  
> Some of the jobs and templates assume that there are global variables that the pipeline can access. In the header of every job file, it is explained the variables needed. We recommend for these global variables the use of Azure DevOps libraries groups https://docs.microsoft.com/en-us/azure/devops/pipelines/library/variable-groups?view=azure-devops&tabs=yaml and create several groups with high cohesion like for example a group named Sonarcloud with all the Sonarcloud variables

<!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->
<!-- ALL-CONTRIBUTORS-BADGE:END -->

## Built With

This section should list any major frameworks that you built your project using. Leave any add-ons/plugins for the acknowledgements section. Here are a few examples.

- [Azure DevOps yaml](https://docs.microsoft.com/en-us/azure/devops/pipelines/yaml-schema/?view=azure-pipelines)

## Features

We have 2 main sections:
- Build: contains everything needed for the builds and release of the packages (CI)
- Deploy: contains everything needed for the deployment (CD)

## Getting Started

### Build phase

We have the following sections:
- Jobs: contain any kind of job needed for the CI step. It includes jobs for:
  - Azure Container Registry (containers and HELM Charts)
  - Copy files from one place to another
  - Publish csproj projects (standard)
  - Run dotnet build, tests and versions
  - Install nuget, nuget push, restore, publish
  - Install npm, npm auth, build, cache, lint, publish, test
  - Sonarqube tasks
  - Git version tasks
  - Mirroring tasks
- Templates: contain templates for libs (nuget and npm), for standard dotnet projects and for docker containers (dotnet based)

### Deploy phase

We have the following sections:
- Jobs: contain any kind of job needed for the CD step. It includes jobs for:
  - Deploy an App Service
  - Pull Helm artifacts from a Registry
  - Deploy Helm chart into AKS


## Prerequisites

Azure DevOps organization (<strong>MyOrg</strong> *for the samples) a project (<strong>MyProject</strong> *for the samples) and a repository (<strong>MyPipelines</strong> *for the samples)

## Installation

- Cloning the repo and use it directly on you solution. On this way, you will have access too entire code.

1. Clone the repo
```sh
git clone https://github.com/ERNI-Academy/assets-azuredevops-pipelines.git
```

2. Push the code to your MyPipelines repository

3. Create a pipeline in Azure DevOps from a yaml and then use the templates provided from your pipelines repository "MyPipelines", more in examples.

## Examples

### npm lib CI pipeline

``` yml
resources:

  repositories:
  - repository: templates
    type: git
    name: MyProject/MyPipelines

variables:
- group: YourGroupVar1 # read Variables Important Note
- group: YourGroupVar2

trigger:
  batch: true
  branches:
    include:
    - main

pool:
  vmImage: ubuntu-lastest # or windows-latest or a hosted agent

workspace:
  clean: all

steps:
- template: /build/templates/build-npm-lib-ci.yml@templates

```

### nuget lib CI pipeline

``` yml
resources:

  repositories:
  - repository: templates
    type: git
    name: MyProject/MyPipelines

variables:
- group: YourGroupVar1 # read Variables Important Note
- group: YourGroupVar2

trigger:
  batch: true
  branches:
    include:
    - main

pool:
  vmImage: ubuntu-lastest # or windows-latest or a hosted agent

workspace:
  clean: all

steps:
- template: /build/templates/build-lib-ci.yml@templates
  parameters:
    nugetProjects: 
    - '<relativePathTo.csproj>' # if you dont have any nuget to generate remove param nugetProjects
```

## Contributing

Please see our [Contribution Guide](CONTRIBUTING.md) to learn how to contribute.

## License

![MIT](https://img.shields.io/badge/License-MIT-blue.svg)

(LICENSE) © 2022 [ERNI - Swiss Software Engineering](https://www.betterask.erni)

## Code of conduct

Please see our [Code of Conduct](CODE_OF_CONDUCT.md)

## Stats

![Alt](https://repobeats.axiom.co/api/embed/057d5659b4939ddb574b7f444e3b719a07e917c7.svg "Repobeats analytics image")

## Follow us

[![Twitter Follow](https://img.shields.io/twitter/follow/ERNI?style=social)](https://www.twitter.com/ERNI)
[![Twitch Status](https://img.shields.io/twitch/status/erni_academy?label=Twitch%20Erni%20Academy&style=social)](https://www.twitch.tv/erni_academy)
[![YouTube Channel Views](https://img.shields.io/youtube/channel/views/UCkdDcxjml85-Ydn7Dc577WQ?label=Youtube%20Erni%20Academy&style=social)](https://www.youtube.com/channel/UCkdDcxjml85-Ydn7Dc577WQ)
[![Linkedin](https://img.shields.io/badge/linkedin-31k-green?style=social&logo=Linkedin)](https://www.linkedin.com/company/erni)

## Contact

📧 [esp-services@betterask.erni](mailto:esp-services@betterask.erni)

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- ALL-CONTRIBUTORS-LIST:END -->
This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!
