
1. Create a service account named `namaste`.

    Then: Use the service account to create a `yo-namaste` pod with `bitnami/nginx` image.

    ```examiner:execute-test
    name: conf-pod-sa
    title: Pod configured with service account
    ```

<div style="margin-top: 5em;"></div>

```section:begin
title: Solution
```

```bash
k create serviceaccount namaste
```

Then: Use the service account to create a `yo-namaste` pod with `bitnami/nginx` image.

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
