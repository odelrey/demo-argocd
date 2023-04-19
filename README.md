# SERVICE


## Getting started

.- Install [Kustomize](https://kustomize.io/)
   (Or you can go directly [here](https://github.com/kubernetes-sigs/kustomize/releases) and to download the Windows version)

e.g: 
```
   tar xvfz kustomize_v4.5.7_windows_amd64.tar.gz -C /usr/bin
```

## Using kustomize

As simple as executing the following command:

```
   kustomize build kustomize/overlays/<app>/environment/<env>
```

 or if we want to check the base affecting all the environments of an app given

```
   kustomize build kustomize/overlays/<app>/base
```

The build comand will generate all the manifest for an application
## base

Base folders are where we define the different common pieces for all the application

```
`-- kustomize
    |-- base-java
    |   |-- deployment.yaml
    |   |-- hpa.yaml
    |   |-- kustomization.yaml
    |   |-- poddisruptionbudget.yaml
    |   |-- route.yaml
    |   |-- service.yaml
    |   `-- servicemonitor.yaml
    |-- base-npm
    |   |-- deployment.yaml
    |   |-- kustomization.yaml
    |   |-- route.yaml
    |   `-- service.yaml
    |-- base-sts
    |   |-- hpa.yaml
    |   |-- kustomization.yaml
    |   |-- poddisruptionbudget.yaml
    |   |-- route-api.yaml
    |   |-- route-mgmt.yaml
    |   |-- service-api.yaml
    |   |-- service-hz.yaml
    |   |-- service.yaml
    |   |-- servicemonitor.yaml
    |   `-- statefulset.yaml
```

In our case we define 3 different deployment types: java, angular and statefulset

# overlays

Overlays are where we define the application. Base folders are affecting all the environments
Basically, base imports root base folder and it "kustomizes" this specific app
Environments/<env> is where we define specific things related to this environments (usually URLs, env vars, etc)

```
java-app/
|-- base
|   |-- application.properties
|   |-- kustomization.yaml
|   |-- patch_deployment.yaml
|   |-- patch_horizontalpodautoscaler.yaml
|   |-- patch_poddisruptionbudget.yaml
|   |-- patch_route.yaml
|   |-- patch_service.yaml
|   `-- patch_servicemonitor.yaml
`-- environments
    |-- dev
    |   |-- application.properties
    |   `-- kustomization.yaml
    |-- preprod
    |   |-- application.properties
    |   `-- kustomization.yaml
    |-- prod
    |   |-- application.properties
    |   `-- kustomization.yaml
    |-- sit
    |   |-- application.properties
    |   `-- kustomization.yaml
    |-- test
    |   |-- application.properties
    |   `-- kustomization.yaml
    |-- train
    |   |-- application.properties
    |   `-- kustomization.yaml
    `-- uat
        |-- application.properties
        `-- kustomization.yaml
```
