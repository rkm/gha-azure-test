# gha-azure-test

Demo of connecting GitHub Actions with the Azure CLI.

## Setup

-   https://github.com/Azure/login#configure-deployment-credentials
    ```console
    $ az ad sp create-for-rbac \
        --name "gha-azure-test" \
        --sdk-auth true \
        --role Contributor \
        --scopes /subscriptions/{subscription-id}
    ```
    This returns JSON object with required credentials.
-   Provide this to GitHub Actions via repository secret. In GitHub repo, go to
    Settings -> Secrets -> Add secret. Create a new secret named
    `AZURE_CREDENTIALS` and paste the JSON from above.
-   View all created credentials in portal under Active Directory -> App
    Registrations -> All applications.
-   Be careful of sensitive output from `az` command being stored in GHA logs...
-   The `--scopes` argument above can be restricted further to a specific
    resource group or resource (e.g. to allow start/stop of a specific VM only)
-   For the extra-paranoid:
    ```console
    $ az logout && az cache purge && az account clear
    ```
