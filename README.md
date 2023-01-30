# templates
The baselime ORL default templates


```yaml
highest-billed-invocations:
  type: query
  properties:
    name: Highest Billed Duration Invocations
    description: Invocations with the highed billed duration
    parameters:
      datasets:
        - lambda-logs
      calculations:
        - MAX(@billedDuration)
        - P99(@billedDuration)
      filters:
        - "@type = REPORT"
      groupBy:
        limit: 5
        orderBy: P99(@billedDuration)
        type: string
        value: $baselime.namespace
lambda-cold-start-duration:
  type: query
  properties:
    name: Duration of lambda cold-starts
    description: Statistics on the duration of lambda cold starts across the application
    parameters:
      datasets:
        - lambda-logs
      calculations:
        - MAX(@initDuration)
        - MIN(@initDuration)
        - P99(@initDuration)
      filters:
        - "@type = REPORT"
      groupBy:
        limit: 5
        orderBy: P99(@initDuration)
        type: string
        value: $baselime.namespace
lambda-errors:
  type: query
  properties:
    name: Events with LogLevel ERROR
    description: Count of the number of events with LogLevel ERROR
    parameters:
      datasets:
        - lambda-logs
      calculations:
        - COUNT
      filters:
        - LogLevel = ERROR
      groupBy:
        limit: 10
        orderBy: COUNT
        type: string
        value: $baselime.namespace
lambda-invocations-durations:
  type: query
  properties:
    name: Duration of lambda invocations
    description: Statistics on the duration of lambda invocations across the application
    parameters:
      datasets:
        - lambda-logs
      calculations:
        - MAX(@duration)
        - P99(@duration)
      filters:
        - "@type = REPORT"
      groupBy:
        limit: 5
        orderBy: P99(@duration)
        type: string
        value: $baselime.namespace
timeouts:
  type: query
  properties:
    name: Invocations that Timed Out
    description: Invocations that reported a time out
    parameters:
      datasets:
        - lambda-logs
      calculations:
        - COUNT
      filters:
        - "@message INCLUDES Task timed out"
      groupBy:
        limit: 5
        orderBy: COUNT
        type: string
        value: $baselime.namespace

timeouts-alert:
  type: alert
  properties:
    description: There were more than 5 timeouts over the past 30mins
    name: Lambda invocations timeouts
    parameters:
      frequency: 30mins
      query: !ref timeouts
      threshold: "> 5"
      window: 30mins
    channels:
      - type: slack
        targets:
          - baselime-alerts


lambda-errors-alert:
  type: alert
  properties:
    description: There were more than {{ threshold }} errors over the past 30mins
    name: Errors during Lambda invocations
    parameters:
      frequency: 30mins
      query: !ref lambda-errors
      threshold: "> {{ threshold }}"
      window: 30mins
    channels:
      - type: slack
        targets:
          - baselime-alerts

```