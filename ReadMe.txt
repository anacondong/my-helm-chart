Helm chart

The templates/ directory is for template files. When Helm evaluates a chart, it will send all of the files in the templates/ directory through the template rendering engine. It then collects the results of those templates and sends them on to Kubernetes.

The values.yaml file is also important to templates. This file contains the default values for a chart. These values may be overridden by users during helm install or helm upgrade.

The Chart.yaml file contains a description of the chart. You can access it from within a template. The charts/ directory may contain other charts (which we call subcharts). Later in this guide we will see how those work when it comes to template rendering.


mychart/templates/ directory, you'll notice a few files already there.

NOTES.txt: The "help text" for your chart. This will be displayed to your users when they run helm install.
deployment.yaml: A basic manifest for creating a Kubernetes deployment
service.yaml: A basic manifest for creating a service endpoint for your deployment
_helpers.tpl: A place to put template helpers that you can re-use throughout the chart


helm install full-coral ./mychart <<< install release
helm get manifest full-coral << get release
helm uninstall full-coral  << uninstall release

Value file >> built-in objects is Values. This object provides access to values passed into the chart. Its contents come from multiple sources:
The values.yaml file in the chart
If this is a subchart, the values.yaml file of a parent chart
A values file if passed into helm install or helm upgrade with the -f flag (helm install -f myvals.yaml ./mychart)
Individual parameters passed with --set (such as helm install --set foo=bar ./mychart)


** helm install geared-marsupi ./mychart --dry-run --debug ** << dry run with value
** helm install solid-vulture ./mychart --dry-run --debug --set favoriteDrink=slurm ** << run by overide with command line


ref: https://helm.sh/docs/chart_template_guide/values_files/

** For minikube
minikube start
minikube dashboard
kubectl apply -f deploy.yaml
kubectl expose deployment hello-world --type=LoadBalancer --name=my-service
kubectl get services my-service
minikube service my-service