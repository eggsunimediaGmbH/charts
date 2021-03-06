# Calibre-Web

This is a helm chart for [Calibre-Web](https://github.com/janeczku/calibre-web).

**This chart is not maintained by the upstream project and any issues with the chart should be raised [here](https://github.com/k8s-at-home/charts/issues/new/choose)**

## TL;DR;

```shell
$ helm repo add k8s-at-home https://k8s-at-home.com/charts/
$ helm install k8s-at-home/calibre-web
```

## Storage

If you plan to use networked storage to store your media or config for Booksonic, (NFS, etc.) please take a look at the
Fast Access option in the Booksonic settings. This will help improve the perfomance of the application
by not constantly monitoring media folders. 

## Installing the Chart

To install the chart with the release name `my-release`:

```console
helm install --name my-release k8s-at-home/calibre-web
```

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
helm delete my-release --purge
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration
Read through the charts [values.yaml](https://github.com/k8s-at-home/charts/blob/master/charts/calibre-web/values.yaml)
file. It has several commented out suggested values. Most notably, these include several environment variables used to
customize the container.
Additionally you can take a look at the common library [values.yaml](https://github.com/k8s-at-home/charts/blob/master/charts/common/values.yaml) for more (advanced) configuration options.

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,
```console
helm install calibre-web \
  --set env.TZ="America/New_York" \
    k8s-at-home/calibre-web
```
Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the
chart. For example,
```console
helm install calibre-web k8s-at-home/calibre-web -f values.yaml 
```

```yaml
image:
  tag: ...
```

---
**NOTE**

If you get
```console
Error: rendered manifests contain a resource that already exists. Unable to continue with install: existing resource conflict: ...`
```
it may be because you uninstalled the chart with `skipuninstall` enabled, you need to manually delete the pvc or use `existingClaim`.

---

## Upgrading an existing Release to a new major version

A major chart version change (like 4.0.1 -> 5.0.0) indicates that there is an incompatible breaking change potentially needing manual actions.

### Upgrading from 2.x.x to 3.x.x

Due to migrating to a centralized common library some values in `values.yaml` have changed.

Examples:

* `service.port` has been moved to `service.port.port`.
* `persistence.type` has been moved to `controllerType`.

Refer to the library values.yaml for more configuration options.
