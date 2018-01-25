# PCF Dashboards
These are Datadog Dashboards for PCF environments using the metrics coming through the Datadog firehose nozzle. These are only a small subset of those OOTB Dashboards offered by Datadog, but it is an ever growing collection. The original effort comes from Pivotal themselves at https://github.com/pivotal-cf/metrics-datadog-dashboard -- we're also considering and looking at the PCF's CloudOps team dashboard collection at https://github.com/pivotal-cf-experimental/datadog-config-oss/.

To get a JSON representation of an existing dashboard, run `ruby get_screenboard [screenboard_id]` or `ruby get_all_screenboards` if you don't know the screenboard_id.

# CF RabbitMQ example dashboard
To upload a dashboard to Datadog:

1. Set your DATADOG_APP_KEY and DATADOG_API_KEY in your environment (you can find them under Integrations > APIs)

    ```
    export DATADOG_API_KEY=theapikey
    export DATADOG_APP_KEY=theappkey
    ```

1. Run `ruby import_static_screenboard [FILENAME]`, passing in the name of the file that contains your dashboard configuration. See `dashboards/rabbitmq.json` for an example.

# CF Redis example dashboard
To upload a dashboard to Datadog:

1. Set your DATADOG_APP_KEY and DATADOG_API_KEY in your environment (you can find them under Integrations > APIs)

    ```
    export DATADOG_API_KEY=theapikey
    export DATADOG_APP_KEY=theappkey
    ```

1. Replace occurences of `<< MetricPrefix >>` with the `MetricPrefix` defined in your [firehose nozzle config](https://github.com/cloudfoundry-incubator/datadog-firehose-nozzle).
  1. _Chris Kelner: This has been done and committed to this repo; using the default prefix `cloudfoundry.nozzle.*`; this information was retained for posterity_
1. Run `ruby import_static_screenboard [FILENAME]`, passing in the name of the file that contains your dashboard configuration. See `dashboards/redis.json` for an example.

# CF Mysql example dashboard
To upload a dashboard to Datadog:

1. Edit `config/mysql_dashboard.yml` with:
  - MySQL VM guids, ie. `628fd3ea-bd68-43fb-9ac7-e6dc68523f87`
  - MySQL deployment name, ie. `p-mysql`
  - Nozzle name, ie. `datadog.nozzle`
1. Set your DATADOG_APP_KEY and DATADOG_API_KEY in your environment (you can find them under Integrations > APIs)

    ```
    export DATADOG_API_KEY=theapikey
    export DATADOG_APP_KEY=theappkey
    ```
1. Run `gem install dogapi erubis`
1. Run `ruby import_mysql_dashboard`

# CF BOSH System Metrics Dashboard
Taken from the [Pivotal CloudOps team repository](https://github.com/pivotal-cf-experimental/datadog-config-oss/blob/master/dashboard_templates/shared/bosh_system_metrics.json.erb)

This is a hardcoded example for `wtcdev2` - but should leverage similar pattern
to the MySQL example for reusability.

1. Set your DATADOG_APP_KEY and DATADOG_API_KEY in your environment (you can find them under Integrations > APIs)

    ```
    export DATADOG_API_KEY=theapikey
    export DATADOG_APP_KEY=theappkey
    ```
1. Run `ruby import_static_timeboard dashboards/bosh_system_metrics.json`
