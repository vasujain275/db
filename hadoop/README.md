# Hadoop (HDFS + YARN + MapReduce) Setup Using Docker

A Docker Compose setup for a single-node [Apache Hadoop](https://hadoop.apache.org/) cluster using the official `apache/hadoop` image: NameNode, DataNode, ResourceManager, NodeManager and JobHistory Server.

## Prerequisites

- Docker and Docker Compose installed on your system

## Quick Start

```bash
docker compose up -d
```

This will start:
- HDFS — NameNode + DataNode
- YARN — ResourceManager + NodeManager
- MapReduce JobHistory Server

| Service | Web UI | Port |
|---|---|---|
| NameNode | http://localhost:9870 | 9870 |
| ResourceManager | http://localhost:8088 | 8088 |
| JobHistory | http://localhost:19888 | 19888 |

No authentication by default (`dfs.permissions=false`) — local development only.

## Usage

All commands run inside the containers (the HDFS RPC port is not published):

```bash
# shell into the cluster
docker exec -it namenode bash

# work with HDFS
hdfs dfs -mkdir -p /DATA
hdfs dfs -put somefile.txt /DATA/
hdfs dfs -ls /DATA
```

### Run a MapReduce example

```bash
docker exec -it resourcemanager bash -c \
  "yarn jar /opt/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-*.jar pi 10 15"
```

Completed jobs show up in the JobHistory UI at http://localhost:19888.

## Configuration

Shared config lives in `hadoop.env` using the image's `<SITE-FILE>_<property>=<value>` convention — each line is written into the corresponding XML file under `/opt/hadoop/etc/hadoop/` at container startup. Edit it and run `docker compose up -d` again to apply.

Notable settings:
- `dfs.replication=1` — single DataNode
- `dfs.permissions=false` — no auth, dev only
- vmem/pmem checks disabled so YARN doesn't kill containers inside Docker's cgroup limits

## Data Persistence

- `namenode_data` volume → `/hadoop/dfs/name`
- `datanode_data` volume → `/hadoop/dfs/data`

The NameNode formats once on first boot into its persistent volume (`ENSURE_NAMENODE_DIR`), so restarts don't cause datanode "Incompatible clusterIDs" errors. If things do get corrupted:

```bash
docker compose down -v   # wipes both volumes and re-formats on next start
```

## Notes

- Uses floating `apache/hadoop:3` tag (currently 3.5.x)
- To scale out, duplicate the `datanode` service with unique container names/hostnames and raise `dfs.replication`
- HDFS RPC (8020) and YARN RPC (8032) are intentionally not published; clients should use `docker exec` or attach to the compose network
