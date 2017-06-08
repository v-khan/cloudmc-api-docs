### Instances

Deploy and manage your instances. Instances are virtual machines or physical machines managed by OpenStack. 

#### List instances

```shell
curl -H "MC-Api-Key: your_api_key" \
    "https://api.your.cloudmc/v1/services/compute-os/devel/instances"
```
```json
{
    "data": [
      {
         "id": "30fca349-68b0-48c2-9ada-1f60f57fa44e",
         "name": "nginx",
         "cpuCount": 2,
         "memoryInMB": 2048,
         "state": "active",
         "flavorId": "1d547941-1738-4d7b-a70b-b52a44ff18e5",
         "flavorName": "2vCPU.2GB",
         "imageId": "68f9027d-cf64-4648-a0fa-4667d5618b6b",
         "imageName": "ubuntu",
         "networkName": "web",
         "privateIpAddress": "192.168.0.11"
      }
    ],
    "metadata": {
        "recordCount": 1
    }
}
```

<code>GET /services/<a href="#service-connections">:service_code</a>/<a href="#environments">:environment_name</a>/instances</code>

Retrieve a list of all instances in an environment.

Attributes | &nbsp;
------- | -----------
`id`<br/>*UUID* | The id of the instance
`name`<br/>*string* | The name of the instance
`state`<br/>*string* | The current state of the instance
`flavorId`<br/>*UUID* | The [flavor](#flavors) id of the instance
`flavorName`<br/>*string* | The [flavor](#flavors) name of the instance
`imageId`<br/>*UUID* | The [image](#images) id of the instance
`imageName`<br/>*string* | The [image](#images)  name of the instance
`cpuCount`<br/>*int* | The number of vCPUs associated with the instance's [flavor](#flavors)
`memoryInMB`<br/>*int* | The number of megabytes associated with the instance's [flavor](#flavors)
`networkId`<br/>*UUID* | The id of the network where instance is deployed
`networkName`<br/>*string* | The name of the network where instance is deployed
`privateIpAddress`<br/>*string* | The instance's private IP address

#### Retrieve an instance

```shell
curl -H "MC-Api-Key: your_api_key" \
    "https://api.your.cloudmc/v1/services/compute-os/devel/instances/30fca349-68b0-48c2-9ada-1f60f57fa44e"
```
```json
{
   "data": {
      "id": "30fca349-68b0-48c2-9ada-1f60f57fa44e",
      "name": "nginx",
      "cpuCount": 2,
      "memoryInMB": 2048,
      "state": "active",
      "flavorId": "1d547941-1738-4d7b-a70b-b52a44ff18e5",
      "flavorName": "2vCPU.2GB",
      "imageId": "68f9027d-cf64-4648-a0fa-4667d5618b6b",
      "imageName": "ubuntu",
      "networkName": "web",
      "privateIpAddress": "192.168.0.11"
   }
}
```

<code>GET /services/<a href="#service-connections">:service_code</a>/<a href="#environments">:environment_name</a>/instances/:id</code>

Retrieve information about an instance.

Attributes | &nbsp;
------- | -----------
`id`<br/>*UUID* | The id of the instance
`name`<br/>*string* | The name of the instance
`state`<br/>*string* | The current state of the instance
`flavorId`<br/>*UUID* | The [flavor](#flavors) id of the instance
`flavorName`<br/>*string* | The [flavor](#flavors) name of the instance
`imageId`<br/>*UUID* | The [image](#images) id of the instance
`imageName`<br/>*string* | The [image](#images)  name of the instance
`cpuCount`<br/>*int* | The number of vCPUs associated with the instance's [flavor](#flavors)
`memoryInMB`<br/>*int* | The number of megabytes associated with the instance's [flavor](#flavors)
`networkId`<br/>*UUID* | The id of the network where instance is deployed
`networkName`<br/>*string* | The name of the network where instance is deployed
`privateIpAddress`<br/>*string* | The instance's private IP address

#### Create an instance

```shell
curl -X POST \
    -H "MC-Api-Key: your_api_key" \
    -H "Content-Type: application/json" \
    -d "request_body" \
    "https://api.your.cloudmc/v1/services/compute-os/devel/instances"
# Request body example:
```
```json
{
    "name": "web1",
    "imageId": "1d547941-1738-4d7b-a70b-b52a44ff18e5",
    "flavorId": "68f9027d-cf64-4648-a0fa-4667d5618b6b",
    "networkId": "2fc5a74b-26c9-4541-af3f-84ee4c75eb0c"
}
```

<code>POST /services/<a href="#service-connections">:service_code</a>/<a href="#environments">:environment_name</a>/instances</code>

Create an instance in an environment.

Required | &nbsp;
------ | -----------
`name`<br/>*string* | Name of the instance
`imageId`<br/>*UUID* | The [image](#images) to use for this instance
`flavorId`<br/>*UUID* | The [flavor](#flavors) will determine the number of CPU and RAM of your instance
`networkId`<br/>*UUID* | The network in which the instance will be created. If you don't have a network, it can be created through the create network API.


#### Delete an instance

```shell
curl -X DELETE \
    -H "MC-Api-Key: your_api_key"
    "https://api.your.cloudmc/v1/services/compute-os/devel/instances/30fca349-68b0-48c2-9ada-1f60f57fa44e"
```

<code>DELETE /services/<a href="#service-connections">:service_code</a>/<a href="#environments">:environment_name</a>/instances/:id</code>

Delete a instance.