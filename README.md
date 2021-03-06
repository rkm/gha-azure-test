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
    This returns a JSON object with the required credentials.
-   Provide this to GitHub Actions via a repository secret. In GitHub, go to the
    repository Settings -> Secrets -> Add secret. Create a new secret named
    `AZURE_CREDENTIALS` and paste the JSON from the above command.

## Notes

-   View all created credentials in the Azure Portal under Active Directory ->
    App Registrations -> All applications. Alternatively under Subscriptions ->
    (select subscription) -> Access control (IAM) -> Role assignments.
    -   _NOTE_ Depending on how you delete the credentials, an orphaned identity
        might be left in the Role assignments list. See
        [here](https://purple.telstra.com/blog/removing-unknown-azure-rbac-role-assignments-with-powershell)
        for details on how to clean these up.
-   Be careful of sensitive output from `az` commands being stored in GHA logs
-   The `--scopes` argument above can be restricted further to a specific
    resource group or resource (e.g. to allow start/stop of a specific VM only)
-   For the extra-paranoid:
    ```console
    $ az logout && az cache purge && az account clear
    ```
