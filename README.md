# kube-slack

kube-slack is a monitoring service for Kubernetes. When a pod has failed,
it will publish a message in Slack channel.

![Screenshot](http://i.imgur.com/em62l25.png)

## Usage

Load this ReplicationController into your Kubernetes.

```yml
apiVersion: v1
kind: ReplicationController
metadata:
  name: kube-slack
spec:
  replicas: 1
  template:
    metadata:
      name: kube-slack
      labels:
        app: kube-slack
    spec:
      containers:
      - name: kube-slack
        image: willwill/kube-slack:latest
        env:
        - name: SLACK_URL
          value: https://TEAMNAME.slack.com/services/hooks/SERVICE-NAME?token=TOKEN
```

The token can be generated by adding integration in Slack.

Additionally, the following environment variables can be used:

- `TICK_RATE`: How often to update in milliseconds. (Default to 15000 or 15s)
- `NAMESPACE`: What namespace to watch (default to default namespace). To watch multiple namespaces, spawn multiple instances.
- `KIBANA_URL`: If you have Kibana logs collector setup, enter base URI for Kibana (eg. https://kibana.example.com). This will add a link to Kibana logs of the failing pod.

## License

[MIT License](LICENSE)
