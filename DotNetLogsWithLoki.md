# Using Loki to aggregate dotnet Serilog logs

- [Using Loki to aggregate dotnet Serilog logs](#using-loki-to-aggregate-dotnet-serilog-logs)
  - [Flow:](#flow)
  - [Setup Serilog](#setup-serilog)
    - [Install the following NuGet Packages](#install-the-following-nuget-packages)
    - [Configure Serilog](#configure-serilog)
  - [Setup Loki and Promtail](#setup-loki-and-promtail)
    - [1. Download Config Files](#1-download-config-files)
    - [2a. Without Docker](#2a-without-docker)
    - [2b. With Docker](#2b-with-docker)

## Flow:
logfile.txt <-- Promtail --> Loki <-- Grafana

## Setup Serilog

### Install the following NuGet Packages

- Serilog
- Serilog.Enrichers.Environment
- Serilog.Sinks.Async
- Serilog.Sinks.Console
- Serilog.Sinks.File
- SerilogWeb.Classic

### Configure Serilog

``` C#
Log.Logger = new LoggerConfiguration()
              .Enrich.WithMachineName()
              .Enrich.WithHttpRequestClientHostIP()
              .Enrich.WithHttpRequestUserAgent()
              .WriteTo.Async(writeTo => writeTo.Console())
              .WriteTo.File(@"C:\Temp\logfile.txt", rollingInterval: RollingInterval.Day)
              .CreateLogger();
          
          Log.Information("Starting Serilog...");
```

## Setup Loki and Promtail

###  1. Download Config Files
```
wget https://raw.githubusercontent.com/grafana/loki/v2.3.0/cmd/loki/loki-local-config.yaml -O loki-config.yaml

wget https://raw.githubusercontent.com/grafana/loki/v2.3.0/clients/cmd/promtail/promtail-docker-config.yaml -O promtail-config.yaml
```

### 2a. Without Docker

- [Download Loki and Promtail](https://github.com/grafana/loki/releases)
  - loki-windows-amd64.exe.zip
  - promtail-windows-amd64.exe.zip
- [Download Grafana](https://grafana.com/grafana/download?platform=windows)
- Configure Loki to point to Serilog logfile
  ``` yaml
  __path__: C:\Temp\*log
  ```
- Setup pipeline_stages to parse out lables. 
  - TODO: Fill this out for Serilog
- Start Loki
```
.\loki-windows-amd64.exe --config.file=loki-config.yaml
```
  - See if Loki is running: http://localhost:3100/metrics
- Configure promtail to push to Loki address in promtail-config.yaml
```yaml
clients:
  - url: http://localhost:3100/loki/api/v1/push
```
- Start promtail
```
.\promtail-windows-amd64.exe --config.file=promtail-config.yaml
```
- Start Grafana
  - /bin/grafana-server.exe
### 2b. With Docker

https://grafana.com/docs/loki/latest/installation/docker/#install-with-docker-compose

```
wget https://raw.githubusercontent.com/grafana/loki/v2.3.0/production/docker-compose.yaml -O docker-compose.yaml
docker-compose -f docker-compose.yaml up
```