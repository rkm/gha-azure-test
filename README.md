# gha-azure-test

Test GitHub Actions with Azure CLI.

## Setup

-   https://github.com/Azure/login#configure-deployment-credentials

```console
$ az ad sp create-for-rbac \
    --name "{sp-name}" \
    --sdk-auth \
    --role contributor \
    --scopes /subscriptions/{subscription-id}
```
