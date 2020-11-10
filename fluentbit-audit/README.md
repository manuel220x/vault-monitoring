## Audit Logs to NewRelic using FluentBit
This tiny docker image can start a container that listens for logs on TCP and forward those to NewRelic setting a couple of parameters

### 1. Update your key on the configuration file
Get your NewRelic license key and add it into the configuration

### 2. Build the image
```bash
docker build -t fluentbit:local .
```

### 3. Start the container
```bash
docker run -p 127.0.0.1:24224:24224 -d --name fluentbit fluentbit:local
```


### 4. Enable the audit logs
In this case, I started the container in the same VM as Vault
```bash
vault audit enable socket address=127.0.0.1:24224 socket_type=tcp
```


At this point all your logs will be available in newrelic
