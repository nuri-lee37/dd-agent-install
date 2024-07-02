### 1. Install Datadog Agent + APM Single Step Instrumentation. Add the Datadog Helm Repository.

This guide is written for EKS environment.


Reference: [https://app.datadoghq.com/account/settings/agent/latest?platform=kubernetes](https://app.datadoghq.com/account/settings/agent/latest?platform=kubernetes)

Sample Code: [https://github.com/DataDog/apm-tutorial-java-host](https://github.com/DataDog/apm-tutorial-java-host)

```
helm repo add datadog https://helm.datadoghq.com
helm repo update
kubectl create secret generic datadog-secret --from-literal api-key=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```

*** The application must be deployed in a different namespace than the datadog agent is deployed.

### 2. Configure datadog-values.yaml. You can also define team, env and provider tags for the resource recognition.
```
targetSystem: "linux"
clusterAgent:
  replicas: 2
  createPodDisruptionBudget: true
  admissionController:
    enabled: true
    mutateUnlabelled: true
datadog:
  apiKeyExistingSecret: datadog-secret
  apm:
    instrumentation:
      enabled: true
    portEnabled: true
  tags:
    - "team:infra"
    - "env:prod"
    - "provider:aws"
```

### 3. Deploy Agent with the above configuration file
`helm install datadog-agent -f datadog-values.yaml datadog/datadog`


### 4. Check datadog agent installation status
`kubectl exec -it <Datadog Agent POD_NAME> -- agent status`

Reference: [https://docs.datadoghq.com/agent/configuration/agent-commands/?tab=agentv6v7#agent-status-and-information](https://docs.datadoghq.com/agent/configuration/agent-commands/?tab=agentv6v7#agent-status-and-information)