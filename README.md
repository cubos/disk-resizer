# Disk Resizer Controller

This is a Kubernetes controller that resizes disks of pods running, if usage is above a certain threshold.

## How it works

The controller runs a CronJob every 5 minutes that lists all PersistentVolumeClaims in the cluster. For each PVC, it checks if the PVC is bound to a Pod and if the Pod is running. If so, it checks the disk usage of the Pod. If the disk usage is above 85%, it resizes the PVC to a bigger size (110%).

## Installing on your cluster

[Helm](https://helm.sh) is the recommended way to install the controller on your cluster.

```bash
helm install disk-resizer-controller oci://ghcr.io/cubos/charts/disk-resizer-controller \
  --namespace kube-system \
  --set secrets.env.CLUSTER_NAME=your-cluster-name \
  --set secrets.env.SLACK_WEBHOOK_URL="https://hooks.slack.com/services/your/slack/webhook/url" \
  --version <version>
```

## Environment variables

| Name                | Description                                  | Required |
| ------------------- | -------------------------------------------- | -------- |
| `CLUSTER_NAME`      | Name of the cluster (used for notifications) | no       |
| `SENTRY_DSN`        | Sentry DSN for error reporting               | no       |
| `SLACK_WEBHOOK_URL` | Slack webhook URL for notifications          | no       |

## Contributing

PRs are welcome! Please make sure to check ESLint and Prettier before submitting a PR.

By submitting a PR, you agree to license your work under the [GNU Lesser General Public License v3.0](LICENSE).
