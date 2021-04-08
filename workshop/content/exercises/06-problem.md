
1. Create a service account named ``namaste``{{copy}}.

1. Use the service account to create a Pod named ``yo-namaste``{{copy}} with image ``bitnami/nginx``{{copy}}.

```examiner:execute-test
name: conf-pod-sa
title: Pod configured with service account
autostart: true
```

<div style="margin-top: 5em;"></div>

```section:begin
title: Solution
```

1. Create the service account:

    ```bash
    k create serviceaccount namaste
    ```

1. Use the service account to create a `yo-namaste` pod with `bitnami/nginx` image.

    ```bash
    k run yo-namaste --image=bitnami/nginx --serviceaccount=namaste
    ```

    Alternatively generate the base pod yaml and set the `serviceAccountName` field in the pod spec.

    Try this:

    ```terminal:execute
    command: k explain pod.spec.serviceAccountName
    ```

```section:end
```
