# ecosystem-images

All the images required for the ecosystem and built by Konflux.

## rpms.lock.yaml

Update this file the [rpm-lockfile](https://github.com/konflux-ci/rpm-lockfile-prototype) tool, with:

```
$ rpm-lockfile-prototype --image $(grep ubi-minimal opc/Dockerfile | awk '{print [}') --outfile rpms.lock.yaml rpms.in.yaml']}')
```
