
1. Create a Pod named ``secure-pod``{{copy}}. Use the ``bitnami/redis``{{copy}} image. Run pod as user 1000 and group 2000.

    ```examiner:execute-test
    name: conf-secure-pod
    title: Pod runs as user 1000 and group 2000
    autostart: true
    ```

    _Note_: Remember to set the environment variable REDIS_PASSWORD, required by this particular image.

<div style="margin-top: 5em;"></div>

```section:begin
title: Solution
```

1. Create starting point pod yaml with:

    ```bash
    k run secure-pod --image=bitnami/redis --dry-run=client -o yaml > secure-pod.yaml
    ```

1. Edit `secure-pod.yaml` and add to the Pod spec a securityContext section as follows:

    ```yaml
    securityContext:
      runAsUser: 1000
      runAsGroup: 2000
    ```

1. Don't forget to add the environment variable required for the bitnami redis image:

    ```yaml
    env:
    - name: REDIS_PASSWORD
      value: hello-again
    ```

1. Finally, apply the yaml.

    ```bash
    k apply -f secure-pod.yaml
    ```

See [Set the security context for a Pod](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/#set-the-security-context-for-a-pod).

```section:end
```
