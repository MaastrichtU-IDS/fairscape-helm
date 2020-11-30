# FAIRscape on the Data Science Research Infrastructure

* FAIRscape publication: https://www.biorxiv.org/content/10.1101/2020.08.10.244947v3.full.pdf
* FAIRscape GitHub repositories: https://github.com/fairscape
* Data Science Research Infrastructure (DSRI) documentation: https://maastrichtu-ids.github.io/dsri-documentation/

## Setup the triplestore

Recommended to use [Stardog](https://www.stardog.com/) (licensed triplestore) for its path explanation feature

* Academic trial (1 year): https://www.stardog.com/academic-trial/
  * Request academic trial: https://community.stardog.com/t/academic-license/1883/7 (use academic email)
* Setup instructions: https://www.stardog.com/docs/#_starting_stardog

## Define Helm chart

https://helm.sh/

* `Helm create` docs: https://helm.sh/docs/helm/helm_create/
* Create Helm chart (Bitnami): https://docs.bitnami.com/tutorials/create-your-first-helm-chart/
* Helm tips and trick: https://helm.sh/docs/howto/charts_tips_and_tricks/

Notes:

* The template parameters go to `values.yml`
* Define multiple images in `values.yml`: https://stackoverflow.com/questions/61044345/how-to-pass-multiple-docker-images-through-values-yml-to-template-yml-in-helm