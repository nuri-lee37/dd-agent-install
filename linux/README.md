### 1. Install Datadog Agent + APM Single Step Instrumentation.

This guide is written for linux ubuntu host agent.

Reference: [https://app.datadoghq.com/account/settings/agent/latest?platform=ubuntu](https://app.datadoghq.com/account/settings/agent/latest?platform=ubuntu)

```
DD_API_KEY=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX DD_SITE="datadoghq.com" DD_APM_INSTRUMENTATION_ENABLED=host  bash -c "$(curl -L https://s3.amazonaws.com/dd-agent/scripts/install_script_agent7.sh)"
```

### 2. Add env, team and provider host tags in the agent main configuration file to identify resources.
Reference: 
[https://docs.datadoghq.com/getting_started/tagging/assigning_tags/?tab=noncontainerizedenvironments#methods-to-assign-tags](https://docs.datadoghq.com/getting_started/tagging/assigning_tags/?tab=noncontainerizedenvironments#methods-to-assign-tags)


[https://docs.datadoghq.com/agent/configuration/agent-configuration-files/?tab=agentv6v7](https://docs.datadoghq.com/agent/configuration/agent-configuration-files/?tab=agentv6v7)

```sh
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
