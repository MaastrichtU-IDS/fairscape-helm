# FAIRscape on the Data Science Research Infrastructure

* FAIRscape publication: https://www.biorxiv.org/content/10.1101/2020.08.10.244947v3.full.pdf
* FAIRscape GitHub repositories: https://github.com/fairscape
* Data Science Research Infrastructure (DSRI) documentation: https://maastrichtu-ids.github.io/dsri-documentation/

## Setup the triplestore

Recommended to use [Stardog](https://www.stardog.com/) (licensed triplestore) for its path explanation feature

* Academic trial (1 year): https://www.stardog.com/academic-trial/
  * Request academic trial: https://community.stardog.com/t/academic-license/1883/7 (use academic email)
* Setup instructions: https://www.stardog.com/docs/#_starting_stardog

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

### Install and run the chart

To run the chart in dry-run mode:

```bash
helm install --dry-run --debug ./fairscape --set service.internalPort=8080
```

Deploy the chart:

```bash
helm install example ./fairscape --set service.type=NodePort
```

