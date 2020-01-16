# Publishing chart to chart repository

## Prerequisites
- having localy installed helm version v3 or higher
- having installed and configered helm push plugin [INFO ](https://github.com/chartmuseum/helm-push) 
- having credentials for helm repository
- having configured statfishx repository locally pointing to statfishx chart repository. Currently it is [https://charts.dev.statfish.io   ](https://charts.dev.statfish.io   ) 

## Tag the repo with helm version tag

Detarmine the chart version you want to use for storing the Jupyterhub chart in the repository. You can start with getting latest version of the chart in the repository and incresing the minor number
```
$ hem repo update
$ helm search repo statfishx/jupyterhub
NAME                    CHART VERSION   APP VERSION     DESCRIPTION                
statfishx/jupyterhub     1.0.0           0.9.6  Multi-user Jupyter installation
```
```
git tag helm_version_1.0.1
```

## Gather all the chart dependencies
`helm dependency update`

## Verify the content of the directory

Check the files in the jupyterhub directory and its subdirectories and make sure that no unwanted files/directories gets packed into chart. If you have some files that you don't want to loose, but you don't want to pack them into chart either, move them outdise of jupyterhub directory.

## Push the chart to repository

Specifying same version as used for git tag, push the chart to repository.
```
$ helm push . statfishx --version 1.0.0
Pushing jupyterhub-1.0.0.tgz to statfishx...
Done.
```