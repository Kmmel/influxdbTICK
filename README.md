This release provides to complete TICK-Stack (Telegraf, Influx, Chronograf and Kapacitor) as one single BOSH-release.

To get more detailed information about the single products please check the [official InfluxDB documentation](https://docs.influxdata.com/).

The project is currently under work so please feel free to add issues if you find some strange behaviour or if you miss some configurations.

## Getting started

There are some sample manifests as well as ops files included in the `manifests` folder.

Choose if you want a single VM (`singleVM.yml`) or a multi VM (`multiVM.yml`) setup and just execute `bosh -d influxdb deploy singleVM.yml` or `bosh -d influxdb deploy multiVM.yml`.

### Telegraf as addon

You can easily add `telegraf` to all your VMs to receive for example VM stats. This can be done via the addon feature of BOSH. Just take the provided `runtime-config + vars.yml` and upload it to your BOSH Director. 
Please make sure to add the `influxdb IP` to the `vars.yml` and to update your `runtime-config` with

```
bosh update-runtime-config runtime-config.yml -l vars.yml
```

Afterwards during the next deploy of a deployment telegraf will be added to your VMs. 

### Configure Telegraf to provide VM syslogs to InfluxDB

If you use the `syslog-runtime-config + vars.yml` you'll get the `syslog-forwarder` job of the `syslog-release` added to the telegraf job as well as the needed configurations. 
Please make sure to add the `influxdb IP` to the `vars.yml` and to update your `runtime-config` with

```
bosh update-runtime-config runtime-config.yml -l vars.yml
```

With that your telegraf job will provide the VM logs directly to influxDB. 

