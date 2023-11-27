# Disk Resizer Controller

This is a Kubernetes controller that resizes disks of pods running, if usage is above a certain threshold.

## How it works

The controller runs a CronJob every 5 minutes that lists all PersistentVolumeClaims in the cluster. For each PVC, it checks if the PVC is bound to a Pod and if the Pod is running. If so, it checks the disk usage of the Pod. If the disk usage is above 85%, it resizes the PVC to a bigger size (110%).

## Environment variables

| Name                | Description                                  | Required |
| ------------------- | -------------------------------------------- | -------- |
| `CLUSTER_NAME`      | Name of the cluster (used for notifications) | no       |
| `SENTRY_DSN`        | Sentry DSN for error reporting               | no       |
| `SLACK_WEBHOOK_URL` | Slack webhook URL for notifications          | no       |

## Contributing

PRs are welcome! Please make sure to check ESLint and Prettier before submitting a PR.

By submitting a PR, you agree to license your work under the [GNU Lesser General Public License v3.0](LICENSE).
