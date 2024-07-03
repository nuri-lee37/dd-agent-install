### 1. Install Datadog Agent + APM Single Step Instrumentation + NPM/Live Process.

This guide is written for linux ubuntu host agent.

Reference: [https://app.datadoghq.com/account/settings/agent/latest?platform=ubuntu](https://app.datadoghq.com/account/settings/agent/latest?platform=ubuntu)

You can customize the instrumentation option. For example, the below example will install Java APM trace library 1.36.0 version. Please refer to the above reference link.

```
DD_API_KEY=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX DD_SITE="datadoghq.com" DD_APM_INSTRUMENTATION_ENABLED=host DD_APM_INSTRUMENTATION_LIBRARIES=java:v1.36.0 bash -c "$(curl -L https://s3.amazonaws.com/dd-agent/scripts/install_script_agent7.sh)"
```

### 2. Add env, team and provider host tags in the [agent main configuration file](https://docs.datadoghq.com/agent/configuration/agent-configuration-files/?tab=agentv6v7) /etc/datadog-agent/datadog.yaml to identify resources.
Reference: 
[https://docs.datadoghq.com/getting_started/tagging/assigning_tags/?tab=noncontainerizedenvironments#methods-to-assign-tags](https://docs.datadoghq.com/getting_started/tagging/assigning_tags/?tab=noncontainerizedenvironments#methods-to-assign-tags)

```
tags:
  - "team:infra"
  - "env:prod"
  - "provider:aws"
```

### 3. Restart the agent so that the change is reflected
Reference: [https://docs.datadoghq.com/agent/configuration/agent-commands/?tab=agentv6v7#restart-the-agent](https://docs.datadoghq.com/agent/configuration/agent-commands/?tab=agentv6v7#restart-the-agent)


`sudo service datadog-agent restart`

### 4. Check datadog agent installation status
`sudo datadog-agent status`

### 5. Install NPM
Reference: [https://docs.datadoghq.com/network_monitoring/performance/setup/?tab=agentlinux](https://docs.datadoghq.com/network_monitoring/performance/setup/?tab=agentlinux)

#### 5-1. Copy the system-probe example configuration:
```sudo -u dd-agent install -m 0640 /etc/datadog-agent/system-probe.yaml.example /etc/datadog-agent/system-probe.yaml```


#### 5-2. Edit `/etc/datadog-agent/system-probe.yaml` to set the enable flag to true:

```
network_config:   # use system_probe_config for Agent's older than 7.24.1
  ## @param enabled - boolean - optional - default: false
  ## Set to true to enable Network Performance Monitoring.
  #
  enabled: true
```


#### 5-3. Restart the datadog agent.
`sudo service datadog-agent restart`

### 6. Install Live Process.
Reference: [https://docs.datadoghq.com/infrastructure/process/?tab=linuxwindows#installation](https://docs.datadoghq.com/infrastructure/process/?tab=linuxwindows#installation)

#### 6-1. Edit `/etc/datadog-agent/datadog.yaml` to set the following parameter to true:

```
process_config:
  process_collection:
    enabled: true
```

#### 6-2. Restart the datadog agent.
`sudo service datadog-agent restart`

