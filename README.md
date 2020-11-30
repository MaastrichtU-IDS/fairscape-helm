# FAIRscape Helm chart

[![Validate Helm chart](https://github.com/MaastrichtU-IDS/fairscape-helm/workflows/Validate%20Helm%20chart/badge.svg)](https://github.com/MaastrichtU-IDS/fairscape-helm/actions?query=workflow%3A%22Validate+Helm+chart%22)

Some links:

* FAIRscape publication: https://www.biorxiv.org/content/10.1101/2020.08.10.244947v3.full.pdf
* FAIRscape GitHub repositories: https://github.com/fairscape
* Data Science Research Infrastructure (DSRI, OpenShift cluster) documentation: https://maastrichtu-ids.github.io/dsri-documentation/

## Defining a Helm chart

To redeploy easily FAIRscape on any Kubernetes cluster.

###  Documentation to create a [Helm](https://helm.sh/) chart

* `Helm create` docs: https://helm.sh/docs/helm/helm_create/
* Create Helm chart (Bitnami): https://docs.bitnami.com/tutorials/create-your-first-helm-chart/
* Helm tips and trick: https://helm.sh/docs/howto/charts_tips_and_tricks/

### How to build the Helm chart

* Define parameters go to `values.yaml` (variables and their values to be used by the templates)
* Then the deployment is defined in `templates/deployment.yaml` and can use variables defined in `values.yaml`
* `Charts/` folder is for external charts dependencies (if we want to define FAIRscape using multiple charts for modularity)

TODO: define OpenShift Route in the Helm chart

* cf. https://www.ibm.com/cloud/blog/deploying-helm-charts-on-openshift
* https://artifacthub.io/packages/helm/appuio/openshift-route
* Example `openshift-route` chart: https://github.com/appuio/charts/tree/master/openshift-route

### Install and run the chart

Check if the Helm chart is properly defined:

```bash
helm lint fairscape
```

To run the chart in dry-run mode:

```bash
helm install --dry-run --debug ./fairscape --set service.internalPort=8080 --generate-name
```

Deploy the chart on OpenShift:

```bash
helm install fairscape ./fairscape --set service.type=NodePort,serviceAccount.name=anyuid,openshiftRoute.enabled=true
```

> We override `service.type` and `serviceAccount.name` from the `values.yaml` file

Upgrade the deployed chart:

```bash
helm upgrade fairscape ./fairscape --set service.type=NodePort,serviceAccount.name=anyuid,openshiftRoute.enabled=true
```

Uninstall the chart:

```bash
helm uninstall fairscape
```

### Known issues

Deploying OpenShift Route: https://bugzilla.redhat.com/show_bug.cgi?id=1773682

cf issue: https://github.com/openshift/origin/issues/24060

Helm Swagger API validation reject when we provide an empty string as host `""`

```yaml
spec:
  host: {{ .Values.openshiftRoute.host }}
```

> Current fix: `host` is hardcoded as `""` in the template instead of using value from `values.yaml`

## Setup the triplestore

Recommended to use [Stardog](https://www.stardog.com/) (licensed triplestore) for its path explanation feature

* Academic trial (1 year): https://www.stardog.com/academic-trial/
  * Request academic trial: https://community.stardog.com/t/academic-license/1883/7 (use academic email)
* Setup instructions: https://www.stardog.com/docs/#_starting_stardog