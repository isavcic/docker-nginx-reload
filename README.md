****docker-nginx-reload****

Super micro Sidecar container for K8s nginx CRL reload with image size of 1.9MB.
It exposes HTTP API endpoint which triggers CRL fetching from Vault and updating CRL file. Then thanks to K8s [Shated process namespaces  between Containers in a Pod](https://kubernetes.io/docs/tasks/configure-pod-container/share-process-namespace/) sents reload signal to nginx in order to re-load CRL file.

## Configuration

The service is configured using the environment variables presented in the
following table. Note that any unset variables will be replaced with their
default values.

| Variable                            | Description                                                | Default               |
|-------------------------------------|------------------------------------------------------------|-----------------------|
| VAULT_API_URL                         | [Vault instance API CRL read endpoint](https://www.vaultproject.io/api/secret/pki/index.html#read-crl)                                           | "http://locahost/v1/pki/crl/pem" 
| VAULT_API_TOKEN                       | Vault instance access token  | "123"                 |
| CRL_FILE_PATH                         | Path to CRL pem file                                          | "crl.pem"                  |
| CMD_TO_EXEC                           | Its a regex which looks for PID's looping over all running processes and finds the ones which cmdline matches the regex provided.              | ".*nginx.*"             |
| API_PORT                              |   API listening port                                  | "8000"              |
| API_ENDPOINT                       | API Endpoint                                        |    "/reload"                   |
