# Prometheus

Deleting a time series
```
$ curl -X POST -g 'http://prometheus.example.com:32647/api/v1/admin/tsdb/delete_series?match[]={instance="192.168.56.10:30285"}'
```