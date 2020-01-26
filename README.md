eclipse-mosquitto-mqtt-broker-helm-chart
============
Simple Helm Chart for Eclipse Mosquitto MQTT Broker

# NOTE: This repo is under development. Do not use on production.

## Prerequisites
- > Running Kubernetes Cluster
- > Helm 2.10+
- > Helm and Kubernetes cluster integration
- > Private Helm Chart Repo (Currently we are using Chartmuseum)
- > [Helm push plugin] (https://github.com/chartmuseum/helm-push)

### Steps
#### 1. Build the helm package and push to the private helm chart repo
```sh
$ helm repo add chartmuseum http://localhost:8080
$ helm package eclipse-mosquitto
$ helm push eclipse-mosquitto chartmuseum
```

#### 2. Create Self-signed certificates for CA, Server and Client
NOTE: Check the `certs/make-keys.sh` content first
```sh
$ cd certs
$ ./make-keys.sh 
```

#### 3. Configure values 
```sh
$ cd certs
$ ./make-keys.sh 
```

#### 4. Deploy the relase with helm
```sh
$ cd certs
$ ./make-keys.sh 
```


### Helm Chart Parameters
The following table lists the configurable parameters of the eclipse-mosquitto chart and their default values.

| Parameter                                    | Description                                      | Default                                                 |
| -------------------------------------------- | ------------------------------------------------ | ------------------------------------------------------- |
| `replicaCount`                               | Replica count                                    | `1`                                                     |
| `image.repository`                           | eclipse-mosquitto Image name                     | `eclipse-mosquitto`                                     |
| `image.tag`                                  | eclipse-mosquitto Image tag                      | `1.6.7`                                                 |
| `image.pullPolicy`                           | Image pull policy                                | `IfNotPresent`                                          |
| `image.pullSecrets`                          | Specify docker-registry secret names as an array | `nil`                                                   |
| `image.debug`                                | Specify if debug values should be set            | `false`                                                 |
| `nameOverride`                               | String to partially override eclipse-mosquitto.fullname template with a string (will prepend the release name) | `nil` |
| `fullnameOverride`                           | String to fully override eclipse-mosquitto.fullname template with a string                                     | `nil` |
| `container.ports.mqtt.name`                  | mqtt container port name                         | `mqtt`                                                  |
| `container.ports.mqtt.port`                  | mqtt container port                              | `1884`                                                  |
| `container.ports.mqtts.name`                 | mqtt container secure port name                  | `mqtts`                                                 |
| `container.ports.mqtts.port`                 | mqtt container secure port                       | `1883`                                                  |
| `service.type`                               | Kubernetes Service type                          | `ClusterIP`                                             |
| `service.ports.mqtt.name`                    | mqtt port name                                   | `mqtt`                                                  |
| `service.ports.mqtt.port`                    | mqtt port                                        | `1884`                                                  |
| `service.ports.mqtts.name`                   | mqtt secure port name                            | `mqtts`                                                 |
| `service.ports.mqtts.port`                   | mqtt secure port                                 | `1883`                                                  |
| `persistence.enabled`                        | Use a PVC to persist data                        | `true`                                                  |
| `persistence.storageClass`                   | Storage class of backing PVC                     | `standard`                                              |
| `persistence.accessMode`                     | Use volume as ReadOnly or ReadWrite              | `ReadWriteOnce`                                         |
| `persistence.size`                           | Size of data volume                              | `8Gi`                                                   |
| `persistence.annotations`                    | Persistence annotations                          | {}                                                   |
| `securityContext.enabled`                    | Enable security context                          | `false`                                                 |
| `securityContext.fsGroup`                    | Group ID for the container                       | `999`                                                   |
| `securityContext.runAsUser`                  | User ID for the container                        | `999`                                                   |
| `resources`                                  | resource needs and limits to apply to the pod    | {}                                                      |
| `nodeSelector`                               | Node labels for pod assignment                   | {}                                                      |
| `affinity`                                   | Affinity settings for pod assignment             | {}                                                      |
| `tolerations`                                | Toleration labels for pod assignment             | []                                                      |
| `ingress.enabled`                            | Enable ingress resource for Management console   | `false`                                                 |
| `ingress.hosts[0].host`                      | Hostname to your mqtt installation           | `nil`                                                   |
| `ingress.hosts[0].paths[0]`                  | Path within the url structure                    | `/`                                                     |
| `ingress.annotations`                        | ingress annotations                              | {}                                                      |



## Source of Self-signed certificates creation script
Thanks to @suru-dissanaike for [gist](https://gist.github.com/suru-dissanaike/4344f572b14c108fc3312fc4fcc3d138)

## License
Copyright (c) 2020 [CloudNesil](https://cloudnesil.com)

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
