# My First Elasticsearch Cluster using Docker Compose

## 1. Documentation

I have followed the [Official Documentation of Elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html#docker-compose-file) to start this two-node Elasticsearch cluster with Kibana. 

## 2. Install Docker Compose

In my case I'm using [Docker Desktop](https://www.docker.com/products/docker-desktop/), managed from Windows Subsystem for Linux (Ubuntu-22.04 LTS), which incorporates Docker Compose.

> :warning: WARNING: Make sure to allocate at least 4GB of memory to Docker Desktop. You can adjust memory usage in Docker Desktop by going to **Settings > Resources**.

> :warning: WARNING2: The `vm.max_map_count` kernel setting must be set to at least `262144`, if not, it can cause problems.
>
>- To set it just in your current terminal thread execute the following command:
>```bash
>vm.max_map_count=262144
>```
>- To set it permanently on you Linux System add the following line at the end of the file `/etc/sysctl.conf`
>```bash
>vm.max_map_count=262144
>```

## 3. Run the containers using Docker Compose

To start the cluster, run the following command from the project directory:

```bash
docker-compose up -d
```

To test everything is running OK you can:

- After the cluster has started, open http://localhost:5601 in a web browser to access Kibana.
- After the cluster has started, execute in some terminal:
```bash
curl -XGET -k -u elastic:changeme https://localhost:9200/_cluster/health
```

When shut down your computer, you can execute the following command to, smoothly, stop the containers without losing the important data (it is stored in the Docker Volumes so it is persisted in the Linux System):
```bash
docker-compose down
```

To delete the network, containers, and volumes when you stop the cluster, specify the -v option:
```bash
docker-compose down -v
```

## 4. Advices to run Elasticsearh in Production Environments

### 4.1 Always bind data volumes

You should use a volume bound on `/usr/share/elasticsearch/data` for the following reasons:

1. The data of your Elasticsearch node won’t be lost if the container is killed
2. Elasticsearch is I/O sensitive and the Docker storage driver is not ideal for fast I/O
3. It allows the use of advanced Docker volume plugins

## 5. Next Steps
|  TO DO | Status |
| ------ | -----  |
| Add more advices for Production Environments | PENDING |
| Play more with the data and the Cluster | PENDING |
