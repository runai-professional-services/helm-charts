### Metrics Collection Helm Chart

#### How to Install

1. Add the repo and update

`helm repo add metrics https://runai-professional-services.github.io/helm-charts/ && helm repo update`

2. Export the values file and add your application credentials

`helm show values metrics/consumption-report > metrics.yaml`

3. Install the helm chart

`helm upgrade -i metrics -n runai metrics/consumption-report -f metrics.yaml`
