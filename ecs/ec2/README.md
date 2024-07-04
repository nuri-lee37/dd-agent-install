### 1. Install Datadog Agent Infra + APM + NPM/Live Process + Log.

This guide is written for ecs ec2 amazon linux 1 environment.

Reference: [https://docs.datadoghq.com/containers/amazon_ecs/?tab=awscli](https://docs.datadoghq.com/containers/amazon_ecs/?tab=awscli)

Create and add an ECS task definition by using [datadog-agent-ecs1.json](https://github.com/nuri-lee37/dd-agent-install/blob/main/ecs/ec2/datadog-agent-ecs1.json) file.

### 2. Edit the task definition file.
- Replace DD_API_KEY from the file. 
- Set the DD_SITE environment based on your [datadog site](https://docs.datadoghq.com/getting_started/site/#access-the-datadog-site).
- Optionally, add a DD_TAGS.

### 3. (Optional) To deploy on an ECS Anywhere cluster, add the following line to your ECS task definition.
`"requiresCompatibilities": ["EXTERNAL"]`

### 4. (Optional) To add an Agent health check, add the following line to your ECS task definition:

```
"healthCheck": {
  "retries": 3,
  "command": ["CMD-SHELL","agent health"],
  "timeout": 5,
  "interval": 30,
  "startPeriod": 15
}
```
### 5. After you have created your task definition file, execute the following command to register the file in AWS.


`aws ecs register-task-definition --cli-input-json file://<path to datadog-agent-ecs.json>`

### 6. Run the agent as a daemon service.
Please refer to this [document](https://docs.datadoghq.com/containers/amazon_ecs/?tab=awscli#run-the-agent-as-a-daemon-service).





