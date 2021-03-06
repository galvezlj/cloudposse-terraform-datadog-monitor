## Memory Usage

Terraform module to configure Memory Usage Datadog monitor


## Usage

Create Datadog Memory Usage monitor for all hosts:

```hcl
module "datadog_memory_usage_global" {
  source             = "git::https://github.com/cloudposse/terraform-datadog-monitor.git//modules/memory?ref=master"
  namespace          = "cp"
  stage              = "prod"
  name               = "app"
  attributes         = ["global"]
  datadog_api_key    = "xxxxxxxxxxxxxxxxxxxxx"
  datadog_app_key    = "xxxxxxxxxxxxxxxxxxxxx"
  ok_threshold       = "104857600"
  warning_threshold  = "54857600"
  critical_threshold = "24857600"
}
```

Create Datadog Memory Usage monitor for tagged hosts:

```hcl
module "datadog_memory_usage_us_east_1" {
  source             = "git::https://github.com/cloudposse/terraform-datadog-monitor.git//modules/memory?ref=master"
  namespace          = "cp"
  stage              = "prod"
  name               = "app"
  attributes         = ["us-east-1"]
  datadog_api_key    = "xxxxxxxxxxxxxxxxxxxxx"
  datadog_app_key    = "xxxxxxxxxxxxxxxxxxxxx"
  ok_threshold       = "104857600"
  warning_threshold  = "54857600"
  critical_threshold = "24857600"
  selector           = ["region:us-east-1"]
}
```


## Inputs

|  Name                          |  Default                          |  Description                                                                                                                    | Required |
|:-------------------------------|:---------------------------------:|:--------------------------------------------------------------------------------------------------------------------------------|:--------:|
| `namespace`                    | ``                                | Namespace (_e.g._ `cp` or `cloudposse`)                                                                                         | Yes      |
| `stage`                        | ``                                | Stage (_e.g._ `prod`, `dev`, `staging`)                                                                                         | Yes      |
| `name`                         | ``                                | Application or solution name (_e.g._ `app`)                                                                                     | Yes      |
| `attributes`                   | `[]`                              | Additional attributes (_e.g._ `global` or `us-eat-1`)                                                                           | No       |
| `tags`                         | `{}`                              | Additional tags (_e.g._ `map("BusinessUnit","XYZ")`                                                                             | No       |
| `delimiter`                    | `-`                               | Delimiter to be used between `name`, `namespace`, `stage`, `attributes`                                                         | No       |
| `datadog_api_key`              | ``                                | Datadog API key. This can also be set via the DATADOG_API_KEY environment variable                                              | Yes      |
| `datadog_app_key`              | ``                                | Datadog APP key. This can also be set via the DATADOG_APP_KEY environment variable                                              | Yes      |
| `monitor_enabled`              | `true`                            | State of the monitor                                                                                                            | No       |
| `monitor_silenced`             | `1`                               | Each scope will be muted until the given POSIX timestamp or forever if the value is 0                                           | No       |
| `alert_type`                   | `metric alert`                    | Type of the monitor (_e.g._ `metric alert`, `service check`, `event alert`, `query alert`)                                      | Yes      |
| `notify_no_data`               | `false`                           | A flag indicating whether this monitor will notify when data stops reporting                                                    | No       |
| `new_host_delay`               | `300`                             | Time (in seconds) to allow a host to boot and applications to fully start before starting the evaluation of monitor results     | No       |
| `renotify_interval`            | `60`                              | The number of minutes after the last notification before a monitor will re-notify on the current status. It will only re-notify if it's not resolved | No       |
| `period`                       | `10m`                             | Monitoring period in minutes                                                                                                    | No       |
| `ok_threshold`                 | `104857600`                       | Memory usage OK threshold in bytes                                                                                              | No       |
| `warning_threshold`            | `54857600`                        | Memory usage warning threshold in bytes                                                                                         | No       |
| `critical_threshold`           | `24857600`                        | Memory usage critical threshold in bytes                                                                                        | No       |
| `datadog_monitor_tags`         | `["system", "memory"]`            | Configurable labels that can be applied to monitor                                                                              | No       |
| `selector`                     | `["*"]`                           | Selector for enabling monitor for specific hosts, host tags                                                                     | No       |
| `notify`                       | ``                                | Notification email, hipchat or slack user/channel                                                                               | No       |
| `escalation_notify`            | ``                                | Escalation notification email, hipchat or slack user/channel                                                                    | No       |
| `group_by`                     | `{host}`                          | Monitor query group by selector                                                                                                 | No       |
| `remediation`                  | ``                                | URL to internal documentation for instructions as to how to remediate                                                           | No       |


## Outputs

| Name                        | Description                             |
|:----------------------------|:----------------------------------------|
| `memory_usage_id`           | ID of Memory Usage monitor              |
