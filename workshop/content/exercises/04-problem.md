
1. Create a pod manifest file ``limited-pod.yaml``{{copy}} with name ``limited-pod``{{copy}} and image ``bitnami/kubectl``{{copy}}. Set memory request at `100Mi` and limit at `200Mi`. You do not need to create the pod.

    ```examiner:execute-test
    name: conf-limited-pod
    title: Pod yaml has specified resource memory requests and limits
    autostart: true
    ```

<div style="margin-top: 5em;"></div>

```section:begin
title: Solution
```

```bash
k run limited-pod --image=bitnami/kubectl \
  --requests=memory=100Mi \
  --limits=memory=200Mi \
  --dry-run=client -o yaml > limited-pod.yaml
```

Alternatively..

1. Create base pod manifest:

    ```bash
    k run limited-pod --image=bitnami/kubectl --dry-run=client -o yaml > limited-pod.yaml
    ```

1. Edit manifest and add resources section to container specification:

    ```yaml
    resources:
      requests:
        memory: "100Mi"
      limits:
        memory: "200Mi"
    ```

1. Finally, apply the yaml.

    ```bash
    k apply -f limited-pod.yaml
    ```

See [Managing Resources for Containers](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#meaning-of-memory).

```section:end
```
