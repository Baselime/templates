# Templates for DynamoDB
Monitor DynamoDB Performance with the baselime dynamodb template. These queries use your CloudWatch Metrics to show you how your tables are performing

## Datasets

| Dataset | Docs  |
|---------|-------|
| cloudwatch-metrics | https://docs.baselime.io/sending-data/cloudwatch-metrics/ |

### Queries

| Name | Description | Dataset | Id |
|------|-------------|---------|----|
| DynamoDB Consumed Write Capacity | N/A | cloudwatch-metrics | dynamodb-consumed-write-capacity |
| DynamoDB Consumed Read Capacity | N/A | cloudwatch-metrics | dynamodb-consumed-read-capacity |
| Scan Latency | Duration of scans | cloudwatch-metrics | scan-latency |
| Scan Items Returned | Number of items returned by a scan | cloudwatch-metrics | scan-items-returned |
| Scans | Number of scans | cloudwatch-metrics | scan-count |
| Slow Put Item Requests | The 10 slowest Put Item requests Grouped By Table | cloudwatch-metrics | slow-put-item-requests |
| Slow Get Item Requests | The 10 slowest Put Item requests Grouped By Table | cloudwatch-metrics | slow-get-item-requests |
| Slow Update Item Requests | The 10 slowest Update Item requests Grouped By Table | cloudwatch-metrics | slow-update-item-requests |


### Alarms

| Name | Description | Triggered by | Threshold | Window |
|------|-------------|-------------|----|----------|
| Friends don't let friends run scans | If the scan count is more than 10 for a 10 minute window alert | scan-count | `> 10` | `10mins` |