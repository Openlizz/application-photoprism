<h1 align="center">Lizz compatible Photoprism application</h1>

Lizz compatible application to add the [Photoprism application](https://photoprism.app/) to a Lizz managed Kubernetes cluster.

To learn more about Lizz, see the [documentation](https://openlizz.com).

## Requirements

To add the application, you first need to have a [Kubernetes cluster initialized with Lizz](https://openlizz.com/docs/guides/init).
You also need to have the [Lizz CLI installed](https://openlizz.com/docs/installation).

## Add the application

To add the application to your cluster, run the following:

```bash
lizz add github \
    --owner=$GITHUB_USER  \
    --fleet=fleet \
    --origin-url=https://github.com/openlizz/application-photoprism \
    --path=./default \
    --destination=photoprism \
    --personal
```

Check the [guide](https://openlizz.com/docs/guides/add) to understand how works the lizz add command.

> **Note**
> You can adapt the command depending on your use case. See the [command API](https://openlizz.com/docs/cli/lizz_add_github) for more information.

Reconcile the fleet repository to deploy the application using [Flux](https://fluxcd.io/):

```
flux reconcile source git flux-system
```

Check the pods with:

```
kubectl get pod -n photoprism
```

The output should be similar to:

```
NAMESPACE       NAME                                        READY   STATUS    RESTARTS      AGE
photoprism      photoprism-86b879b6b7-xtx5d                 1/1     Running   0             2m55s
```
    
## Usage

Access the application using port-forwarding or using the ingress created.
You should access the Photoprism log in page, log in using the admin account and the admin password (the admin password is shown in the lizz add command output).

Once you are logged in, refer to the [Photoprism user manuel](https://docs.photoprism.app/user-guide/) to learn how to use Photoprism.

## Acknowledgements

This repository is only a wrapper to the [Helm chart](https://github.com/k8s-at-home/charts/tree/master/charts/stable/photoprism) of the [Photoprism application](https://photoprism.app/) to help its deployment in a Kubernetes cluster managed by Lizz.

Therefore, the credit goes to the developers and maintainers of the application and the chart.