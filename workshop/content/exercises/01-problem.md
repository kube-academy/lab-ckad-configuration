
1. Create a config map with the name `my-config` and value `confa=exvalue`.

    ```examiner:execute-test
    name: conf-config-map
    title: ConfigMap my-config exists
    autostart: true
    ```

<div style="margin-top: 5em;"></div>

```section:begin
title: Solution
```

```bash
k create cm my-config --from-literal=confa=exvalue
```

```section:end
```
