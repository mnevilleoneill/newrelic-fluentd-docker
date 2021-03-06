# Fluentd Docker Image for New Relic Logs

newrelic-fluentd-docker is a custom Docker image that runs [Fluentd](https://www.fluentd.org/), listens for log events from containers running the [Fluentd logging driver](https://docs.docker.com/config/containers/logging/fluentd/), and forwards them to New Relic. The image can be customized to support additional use cases (e.g. tailing files on a container host, receiving and forwarding syslog input).


## Usage

### Default Configuration

The command below configures the container to receive and forward log events from other Docker containers running the Fluentd logging driver:

```bash 
docker run --name="newrelic-fluentd-docker" --restart=always -d -p 24224:24224 \
-e "API_KEY=<YOUR API INSERT KEY>" -e "BASE_URI=<YOUR HTTP ENDPOINT>" \ 
-e "LOG_LEVEL=<YOUR DEFAULT LOG LEVEL>" newrelic/newrelic-fluentd-docker:latest
```
### Custom Configuration
1. Clone this repository:
```bash
  $ git clone https://github.com/newrelic/newrelic-fluentd-docker
```
2. Replace the default `fluent.conf` with your custom Fluentd configuration.
3. Build your custom Fluentd image:
```bash
docker build . -t newrelic-fluentd-docker
```
## Configuration

###  Environment Variables


| Property | Description | Default Value | Required or Optional
|---|---|---|---|
| API_KEY | Your New Relic API [insert key](https://docs.newrelic.com/docs/insights/insights-api/get-data/query-insights-event-data-api#register)|-|Required 
| BASE_URI | New Relic [ingestion endpoint](https://docs.newrelic.com/docs/logs/new-relic-logs/log-api/introduction-log-api#endpoint)|`https://log-api.newrelic.com/log/v1`|Optional
| LOG_LEVEL | Fluentd [log level](https://docs.fluentd.org/deployment/logging#log-level)|`warn`|Optional

### Getting Your Keys

* You can retrieve your New Relic Insights [insert key](https://docs.newrelic.com/docs/insights/insights-api/get-data/query-insights-event-data-api#register) from the following location:
`https://insights.newrelic.com/accounts/<YOUR ACCOUNT ID>/manage/api_keys`

