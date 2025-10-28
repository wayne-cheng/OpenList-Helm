# Contributing to Helm Chart for OpenList

Please refer to [OpenList contributing guide](https://github.com/OpenListTeam/OpenList/blob/main/CONTRIBUTING.md) and follow the standard PR process.

## Check charts

```shell
helm lint charts/openlist
```

## Package charts

It will generate a packaged chart file like `openlist-{version}.tgz`.

Please upload the file to the Github Releases.

```shell
helm package charts/openlist
```

## Update `index.yaml`

```shell
helm repo index --url https://wayne-cheng.github.io/helm-chart/  --merge index.yaml .
```

Please modify the urls field in the `index.yaml` file to point to the actual file URL in the GitHub Releases.
