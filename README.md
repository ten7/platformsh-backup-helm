# Platform.sh-backup-helm

A helm chart to backup your Platform.sh sites to S3 or SFTP from Kubernetes

## How it works

This chart provisions a cronjob which runs the [`ten7/platformsh-backup`](https://hub.docker.com/repository/docker/ten7/platformsh-backup) container. It uses the [`terminus`](https://Platform.sh.io/docs/terminus) command to create and download backups to the container's ephemeral storage. Once downloaded, the backup is them uploaded to zero or more remote servers. Each "remote" can be either and S3 bucket, or an SFTP server.

## Features

* Uses Platform.sh's own tools to perform the backup.
* Supports multiple S3 and SFTP destinations.
* A number of database backups can be retained, and old backups are deleted automatically.
* Can be installed multiple times in the same namespace, with different schedules, allowing you to make hourly/daily/weekly/monthly backups.

## Requirements

* The container must have sufficient local storage to save the backup while downloading and uploading.
* A `platform` CLI Token must be provisioned for the site.
* Connection and credentials for target S3 and/or SFTP providers.

## Installation

```shell
helm repo add platformsh-backup https://ten7.github.io/platformsh-backup-helm/
helm repo update
helm upgrade --install platformsh-backup platformsh-backup/platformsh-backup --namespace=my-namespace -f path/to/my-values.yml
```

## Configuration

For a full list of values, see [values.yaml](https://raw.githubusercontent.com/ten7/platformsh-backup-helm/main/charts/platformsh-backup/values.yaml).

## License

Gitea Backup is licensed under GPLv3. See [LICENSE](https://raw.githubusercontent.com/ten7/platformsh-backup-helm/main/LICENSE) for the complete language.
