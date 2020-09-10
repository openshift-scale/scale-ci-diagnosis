# Dockerfile for scale-ci-diagnosis

FROM grafana/grafana:latest

USER root

MAINTAINER Red Hat OpenShift Performance and Scale

# Setup dashboard provider and prometheus as the default datasource
COPY datasource.yaml /etc/grafana/provisioning/datasources/datasource.yaml
COPY provider.yaml /etc/grafana/provisioning/dashboards/provider.yaml

# Setup dashboards - load openshift performance and scale default dashboards
RUN apk add --no-cache git && git clone https://github.com/cloud-bulldozer/arsenal /tmp/arsenal && mkdir -p /etc/grafana/provisioning/dashboards && cp /tmp/arsenal/openshift-performance-dashboard/grafana/on-cluster-latest.json /etc/grafana/provisioning/dashboards/on-cluster-latest.json && cp /tmp/arsenal/openshift-performance-dashboard/grafana/etcd-on-cluster-dashboard.json /etc/grafana/provisioning/dashboards/etcd-on-cluster-dashboard.json
