### 1. Install Datadog Agent + APM Single Step Instrumentation
` ` `
DD_API_KEY=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX DD_SITE="datadoghq.com" DD_APM_INSTRUMENTATION_ENABLED=host  bash -c "$(curl -L https://s3.amazonaws.com/dd-agent/scripts/install_script_agent7.sh)"
` ` ` 