# Specifities of this deployment
## Intro
This deployment uses GraphDB fe (free edition) as graph data base for mataphactory. It deviates in some points from `/service-template`, since the latter makes use of official graphdb docker images and only  images for se (standard edition) and ee (enterprise edition) exist – and not for fe.


## Modifications
these modifications where needed to make it work with fe:
### Add GraphDB free folder


Ontotext maintains the GitHub repository [graphdb-docker](https://github.com/Ontotext-AD/graphdb-docker) with configuration for GraphDB fe. This helps to build GraphDB fe directly from docker-compose instead of using an image. To do so, copy over all files and folders of [graphdb-docker](https://github.com/Ontotext-AD/graphdb-docker) into `/metaphactory-graphdb/graph-db-fe`

### Use build instead of image

In `kleio-deployment-2/docker-compose.overwrite.yml` point to the new folder and builds the image from there: 
```yml
  graphdb:
    # graphdb overwrites here
    # from https://github.com/Ontotext-AD/graphdb-docker
    build:
      context: ../metaphactory-graphdb/graph-db-fe
      dockerfile: Dockerfile
      args:
        version: 9.6.0
```


### Comment out GraphDB image
In `/metaphactory-graphdb/docker-compose.yml` Unfortunately it is not possible to remove config parameter using the overwrite.yml. Therefore uncomment the image definition, so that the image is built  according to the overwrite above:
```yml
# image: "${GRAPHDB_IMAGE}" 
```



### Change GraphDB repository type for free edition 
Because the free edition does not allow replication repository type, change this file
- `kleio-deployment-2/database-config/graphdb-config/graphdb-repository-config.ttl`

I changed thre repository type according to the example:
  - `metaphactory-graphdb/graph-db-fe/preload/graphdb-repo-free.ttl`

Remark: ONLY change this, if deploying graphdb free edition! otherwise add licence and use default graphdb-repository-config.ttl

### Open port 7200
In order to expose GraphDB as such (not only through metaphactory), open the port 7200 here 
- `kleio-deployment-2/database-config/docker-compose.graphdb.yml`

