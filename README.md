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
    This returns JSON object with required credentials.
-   Provide this to GitHub Actions via repository secret. In GitHub repo, go to
    Settings -> Secrets -> Add secret. Create a new secret named
    `AZURE_CREDENTIALS` and paste the JSON from above.
-   View all created credentials in portal under Active Directory -> App
    Registrations -> All applications.
-   Be careful of sensitive output from `az` command being stored in GHA logs...
