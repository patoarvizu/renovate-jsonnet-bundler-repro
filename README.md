# renovate-jsonnet-bundler-repro

## Steps to reproduce

1. Install [k3d](https://github.com/rancher/k3d).
2. Install [Helmfile](https://github.com/roboll/helmfile).
3. Get a GitHub access token, export it into the `GITHUB_COM_TOKEN` variable, e.g. `export GITHUB_COM_TOKEN=<token>`.
4. Set `KUBECONFIG` to `~/.k3d/k3s-default-config`, e.g. `export KUBECONFIG=~/.k3d/k3s-default-config`.
5. Run `make start`.
6. Wait for the first Renovate pod to run in the `renovate` namespace, e.g. with `kubectl -n renovate get pods`.
7. Once the first pod successfully runs, check the logs with `kubectl -n renovate logs ...`.
8. You should see a message along the lines of: `DEBUG: Dependency jsonnet-libs has unsupported value master (repository=patoarvizu/renovate-jsonnet-bundler-repro)`
9. And another one like the following:
```
DEBUG: packageFiles with updates (repository=patoarvizu/renovate-jsonnet-bundler-repro)
       "config": {
         "jsonnet-bundler": [
           {
             "packageFile": "jsonnetfile.json",
             "deps": [
               {
                 "depName": "jsonnet-libs",
                 "lookupName": "https://github.com/grafana/jsonnet-libs",
                 "currentValue": "master",
                 "managerData": {"subdir": "ksonnet-util"},
                 "depIndex": 0,
                 "updates": [],
                 "warnings": [],
                 "versioning": "semver",
                 "skipReason": "invalid-value"
               }
             ]
           }
         ]
       }
```