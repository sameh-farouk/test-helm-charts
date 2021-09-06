# My [Helm](https://helm.sh) Charts

This repository contains [Helm](https://helm.sh) charts for testing purposes

* [Peertube](charts/peertube/)
* [Taiga](charts/taiga)

## Installing Charts from this Repository

Add the Repository to Helm:

    helm repo add test-helm-charts https://sameh-farouk.github.io/test-helm-charts/

Install Peertube:

    helm install --name test_peertube --namespace test_peertube test-helm-charts/peertube

## uploading new charts to this Repository (Require Access)

1- you need to install [Chart Releaser](https://github.com/helm/chart-releaser)
2- clone the repo
```
git clone https://github.com/sameh-farouk/test-helm-charts.git
```
3- cd into the `test-helm-charts` directory
4 - create your new app helm chart files inside ./charts/{app_name}/

5 - excute the below commands
```sh
git checkout main
helm package charts/{app_name} --destination .deploy  # pacakge the chart
cr upload -o sameh-farouk -r test-helm-charts -t -t {github-access-token} -p .deploy  # upload the package to github releases

git checkout gh-pages
cr index -i ./index.yaml -o sameh-farouk -r test-helm-charts -t {github-access-token} -c https://sameh-farouk.github.io/test-helm-charts/ -p .deploy
git add index.yaml
git commit -m 'release 0.0.{version}'
git push origin gh-pages
```
