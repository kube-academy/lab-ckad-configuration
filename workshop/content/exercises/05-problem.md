
1. Create a secret `db-secret` with value `MYSQL_ROOT_PASSWORD=YoYoSecret` and `MYSQL_PASSWORD=XoXoPassword`.

1. Create a configmap named `db-config` with value `MYSQL_USER=k8s` and `MYSQL_DATABASE=newdb`.

1. Create a pod named `mydb` with image `bitnami/mysql` and expose all values of `db-secret` and `db-config` as environment variables to the pod.

```examiner:execute-test
name: conf-db-pod
title: Mysql Pod configured with environment variables from config map and secrets
autostart: true
```

<div style="margin-top: 5em;"></div>

```section:begin
title: Solution
```

1. Create the secret

    ```bash
    k create secret generic db-secret --from-literal=MYSQL_ROOT_PASSWORD=YoYoSecret --from-literal=MYSQL_PASSWORD=XoXoPassword
    ```

1. Create a configmap named `db-config` with value `MYSQL_USER=k8s` and `MYSQL_DATABASE=newdb`.

    ```bash
    k create cm db-config --from-literal=MYSQL_USER=k8s --from-literal=MYSQL_DATABASE=newdb
    ```

1. Create a pod named `mydb` with image `bitnami/mysql` and expose all values of `db-secret` and `db-config` as environment variables to the pod.

    1. Create base pod manifest:

        ```bash
        k run mydb --image=bitnami/mysql --dry-run=client -o yaml > mydb.yaml
        ```

    1. Edit `mydb.yaml` and add an `envFrom` section (to the container specification) to configure the environment variables, as follows:

        ```yaml
        envFrom:
        - configMapRef:
            name: db-config
        - secretRef:
            name: db-secret
        ```

    1. Finally, apply the yaml.

        ```bash
        k apply -f mydb.yaml
        ```

See [configure all key value pairs in a config map as container environment variables](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/#configure-all-key-value-pairs-in-a-configmap-as-container-environment-variables) and [Secrets use case: as container environment variables](https://kubernetes.io/docs/concepts/configuration/secret/#use-cases).

```section:end
```
