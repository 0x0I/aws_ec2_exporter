<p><img src="https://cdn.worldvectorlogo.com/logos/prometheus.svg" alt="Prometheus logo" title="prometheus" align="left" height="70" /></p>
<p><img src="https://adamtheautomator.com/content/images/2019/07/prod-art-aws-600-width-1200.png" alt="aws logo" title="aws" align="right" height="80" /></p>

# aws_ec2_exporter
A prometheus exporter providing metrics for AWS EC2 compute resource specifications and capacity profiling.

[![Go Report Card](https://goreportcard.com/badge/github.com/0x0I/aws-ec2-exporter)](https://goreportcard.com/report/github.com/0x0I/aws-ec2-exporter)
[![GoDoc](https://godoc.org/github.com/0x0I/aws-ec2-exporter?status.svg)](https://godoc.org/github.com/0x0I/aws-ec2-exporter)

Exposes compute resource statistics of AWS EC2 machine instance-types, images and regions from the AWS EC2 API to a Prometheus compatible endpoint.

## Description

The application can be run in a number of ways, the main consumption is the Docker hub image `0x0I/aws-ec2-exporter`.

**Required**
* `AWS_ACCESS_KEY_ID`      // API access key id of your AWS cloud account
* `AWS_SECRET_ACCESS_KEY`  // API access key secret of youur AWS cloud account

**Optional**
* `METRICS_PATH`          // Path under which to expose metrics. Defaults to `/metrics`
* `LISTEN_PORT`           // Port on which to expose metrics. Defaults to 9174
* `LOG_LEVEL`             // Set the logging level. Defaults to `Info`

## Install and deploy

Run manually from Docker Hub:
```
podman run -d -e AWS_ACCESS_KEY_ID="XXXXXXXX" -e AWS_SECRET_ACCESS_KEY="XXXXXXX" -p 9686:9686 0Iabs/aws-ec2-exporter
```

Build a docker image:
```
podman build -t <image-name> .
podman run -d -e AWS_ACCESS_KEY_ID="XXXXXXXX" -e AWS_SECRET_ACCESS_KEY="XXXXXXX" -p 9686:9686 <image-name>
```

## Docker compose

```
aws-ec2-exporter:
    tty: true
    stdin_open: true
    environment:
      - AWS_ACCESS_KEY_ID="XXXXXXXX"
      - AWS_SECRET_ACCESS_KEY="XXXXXXX"
    expose:
      - 9686:9686
    image: 0Iabs/aws-ec2-exporter:latest
```

## Metrics

Metrics will be made available on port 9686 by default, or you can pass environment variable ```LISTEN_ADDRESS``` to override this. An example printout of the metrics you should expect to see can be found in `METRICS.md`.
