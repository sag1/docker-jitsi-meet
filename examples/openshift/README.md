# Install guide for OpenShift / OKD

## Configuration
Adjust the .env file in the root dir to match your needs.

Some configurations are required:
```bash
# The base for all domains used in the template
DOMAIN=example.com

# The REST API has to be activated because it's used by the liveness and readiness probes
JVB_ENABLE_APIS=rest

# The JVB ports have to be 30000 or higher because NodePort is used for them
JVB_PORT=30000
JVB_TCP_PORT=30000
```

## Build
To build the template you have to use use [spiff++](https://github.com/mandelsoft/spiff). It combines all the manifests into one OpenShift Template.

```console
make build
```

## Deployment
```console
oc process -f jitsi.yaml --ignore-unknown-parameters --param-file ../../.env | oc apply -f -
```

## Currently not working
- Let's Encrypt (cron needs root access - please use something else like [openshift-acme](https://github.com/tnozicka/openshift-acme))
- Set amount of replicas via .env file
- Jibri (You have to grant the container access to the host paths. PR welcome!)
- Jigasi (untested - if you can confirm that it works please create a PR to remove it from the list)
- Etherpad (depends on: [etherpad-lite/pull/3765](https://github.com/ether/etherpad-lite/pull/3765) and [etherpad-lite/pull/3766](https://github.com/ether/etherpad-lite/pull/3766))
