#### Professional Services  Helm Charts

### Metrics Consumption Report Chart

## How to Install

1. Install the Helm cli:

```
$ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
$ chmod 700 get_helm.sh
$ ./get_helm.sh
```

2. Add the metrics repository and perform a Helm upgrade.

`helm repo add metrics https://runai-professional-services.github.io/helm-charts/ && helm repo update`

3. Export the values file we will add your application credentials at a later step.

`helm show values metrics/consumption-report > metrics.yaml`

4. Create an application. This is used to provide credentials for API access. Here is the
documentation on how to create an `application` in Run:ai.

`https://docs.run.ai/v2.19/admin/authentication/applications/?h=applications`

5. Make sure to provide your `application` with the appropriate role to provide access to
those resources when making an API call.

6. Modify the `metrics.yaml`, make sure to update the following fields: The clientID and
clientSecret are the credentials from the `application` you created in step 4.

```
# Run:ai application credentials. Please provision a application to provide api access for the script.
credentials:
  clientId: "<name-of-application>"
  clientSecret: "<seceret-generated-on-creation>"
  baseUrl: "<base-url-to-runai>"

cron:
  # Define how often the metrics job is ran. Default is every midnight.
  schedule: "0 0 * * *"
```


7. Install the Helm chart with the following command:

`helm upgrade -i metrics -n runai . -f ./metrics.yaml`

8. You should now have the following installed:
    a. cronjob in the `runai` namespace called `metrics-consumption-report`. You can manually
    run the cronjob with the following command `kubectl create job <job-name> --from=cronjob/metrics-consumption-report`

9. During the install NOTES are provided on additional functionality. You can always view the
notes by running:
`helm upgrade -i metrics -n runai . -f ./metrics.yaml --dry-run`

## How to uninstall the Helm chart
1. You can delete the helm chart if needed by running the following
`helm delete metrics -n runai`
