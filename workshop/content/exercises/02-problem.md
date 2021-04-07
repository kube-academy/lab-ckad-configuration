
```examiner:execute-test
name: conf-setup
title: Initialize
autostart: true
cascade: true
```

1. A config map named `al-conf` has been created.

    ```terminal:execute
    command: k get cm
    title: Verify that the config map exists
    ```

    Expose the value of `al-user` to a pod named `al-pod` as the environment variable name `AL_USER`. Use `bitnami/redis` as the image for the pod.

    Note: To function, the `bitnami/redis` [requires setting the environment variable named REDIS_PASSWORD](https://github.com/bitnami/bitnami-docker-redis#setting-the-server-password-on-first-run)

    ```examiner:execute-test
    name: conf-config-map-as-env
    title: Pod has environment variable with value from config map entry
    ```

<div style="margin-top: 5em;"></div>

```section:begin
title: Solution
```

1. Create starting point pod yaml with:

    ```bash
    k run al-pod --image=bitnami/redis --dry-run=client -o yaml > al-pod.yaml
    ```

1. Edit `al-pod.yaml` and add an `env` section (to the container specification) to configure the environment variable, as follows:

    ```yaml
    env:
    - name: REDIS_PASSWORD
      value: howdy
    - name: AL_USER
      valueFrom:
        configMapKeyRef:
          name: al-conf
          key: al-user
    ```

    See [Use ConfigMap-defined environment variables in Pod commands](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/#use-configmap-defined-environment-variables-in-pod-commands).

1. Finally, apply the yaml.

    ```bash
    k apply -f al-pod.yaml
    ```

```section:end
```
