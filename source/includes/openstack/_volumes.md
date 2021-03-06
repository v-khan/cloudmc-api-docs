### Volumes

Volumes are block-level storage devices that can be attached to instances.

#### List volumes

```shell
curl -H "MC-Api-Key: your_api_key" \
    "https://api.your.cloudmc/v1/services/compute-os/devel/volumes"
```
```json
{
   "data": [
      {
        "id": "52cfc2f8-5b1f-4833-83cd-a77f55c5ed24",
        "name": "web-data",
        "description": "Storage for the web server",
        "state": "available",
        "sizeInGB": 50
      }
   ],
   "metadata": {
      "recordCount": 1
   }
}
```

<code>GET /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/volumes</code>

Retrieve a list of volumes

Attributes | &nbsp;
------- | -----------
`id`<br/>*UUID* | The volume's id
`name`<br/>*string* | The volume name
`description`<br/>*string* | The volume's description
`sizeInGB`<br/>*integer* | The volume's size in GB
`state`<br/>*string* | The volume's state

#### Retrieve a volume

```shell
curl -H "MC-Api-Key: your_api_key" \
    "https://api.your.cloudmc/v1/services/compute-os/devel/volumes/52cfc2f8-5b1f-4833-83cd-a77f55c5ed24"
```
```json
{
    "data": {
      "id": "52cfc2f8-5b1f-4833-83cd-a77f55c5ed24",
      "name": "web-data",
      "description": "Storage for the web server",
      "state": "available",
      "sizeInGB": 50
    }
}
```

<code>GET /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/volumes/:id</code>

Retrieve a volume

Attributes | &nbsp;
------- | -----------
`id`<br/>*UUID* | The volume's id
`name`<br/>*string* | The volume name
`description`<br/>*string* | The volume's description
`sizeInGB`<br/>*integer* | The volume's size in GB
`state`<br/>*string* | The volume's state

#### Create a volume

```shell
curl -X POST \
    -H "MC-Api-Key: your_api_key" \
    -H "Content-Type: application/json" \
    -d "request_body" \
    "https://api.your.cloudmc/v1/services/compute-os/devel/volumes"
# Request should look like this:
```
```json
{
   "name": "mysql",
   "description": "Production MySQL data",
   "sizeInGB":20
}
```

<code>POST /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/volumes</code>

Create a volume

Required attributes                | Description                         
---------------------------------- | -----------------------------------
`name`<br/>*string*                | The volume name                             
`description`<br/>*string*         | The volume description
`sizeInGB`<br/>*integer*           | The volume's size in GB


Optional | &nbsp;
------ | -----------
`volume`<br/>*Volume* | A volume object containing either `id` or `sizeInGB`. If an `id` is provided, it will attach the existing volume to the instance after creation. If the `sizeInGB` is provided, it will create a new volume and attach it to the instance after creation.

#### Delete a volume

```shell
curl -X DELETE \
    -H "MC-Api-Key: your_api_key" \
    "https://api.your.cloudmc/v1/services/compute-os/devel/volumes/52cfc2f8-5b1f-4833-83cd-a77f55c5ed24"
```

<code>DELETE /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/volumes/:id</code>

Delete a volume

#### Attach a volume to an instance

```shell
curl -X POST \
    -H "MC-Api-Key: your_api_key" \
    -H "Content-Type: application/json" \
    -d "request_body" \
    "https://api.your.cloudmc/v1/services/compute-os/devel/volumes/52cfc2f8-5b1f-4833-83cd-a77f55c5ed24?operation=attach"
# Request should look like this:
```
```json
{
   "instanceId": "449efafc-0a6f-4f9e-9602-4b9ac2400abd",
}
```

<code>POST /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/volumes/:id?operation=attach</code>

Attach a volume to an instance

Required attributes                | Description                         
---------------------------------- | -----------------------------------
`instanceId`<br/>*UUID*            | The instance id

#### Detach a volume from an instance

```shell
curl -X POST \
    -H "MC-Api-Key: your_api_key" \
    "https://api.your.cloudmc/v1/services/compute-os/devel/volumes/52cfc2f8-5b1f-4833-83cd-a77f55c5ed24?operation=detach"
```

<code>POST /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/volumes/:id?operation=detach</code>

Detach a volume from an instance