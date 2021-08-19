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

Returns JSON object with required credentials.

View in portal under Active Directory -> App Registrations -> All applications.

In GitHub repo. Settings -> Secrets -> Add secret. Create a new secret named
`AZURE_CREDENTIALS` and paste the JSON from above.

Be careful of sensitive output from `az` command being stored in GHA logs...
