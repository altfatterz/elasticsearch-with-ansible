### Getting started guide

```bash
ansible-galaxy install -r requirements.yml
```

This will clone the [ansible-elasticsearch](https://github.com/elastic/ansible-elasticsearch) repository into the `roles` folder. Note that this folder should not be checked in into the repository.

In order start up 3 VMs use:

```
vagrant up
```

SSH into one of the VMs:

```bash
vagran ssh node1
```

Check that you can connect to the nodes:

```bash
ansible all -m ping
node1 | SUCCESS => {
    "changed": false,
    "failed": false,
    "ping": "pong"
}
node3 | SUCCESS => {
    "changed": false,
    "failed": false,
    "ping": "pong"
}
node2 | SUCCESS => {
    "changed": false,
    "failed": false,
    "ping": "pong"
}
```

And the nodes can also ping between each other:

```bash
vagrant ssh node1
PING node2 (172.28.128.12) 56(84) bytes of data.
64 bytes from node2 (172.28.128.12): icmp_seq=1 ttl=64 time=0.293 ms
...
```

Install an elasticsearch cluster on these 3 nodes. Issue this command from your host:

```bash
ansible-playbook elasticsearch.yml
```

Check that elasticsearch is provisioned. Login to a node:

```bash
[vagrant@elasticsearch ~]$ curl localhost:9200
```

```json
{
  "name" : "elasticsearch-node1",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "uxSRuRgXQ4eKA7D2-JmuBQ",
  "version" : {
    "number" : "5.6.3",
    "build_hash" : "1a2f265",
    "build_date" : "2017-10-06T20:33:39.012Z",
    "build_snapshot" : false,
    "lucene_version" : "6.6.1"
  },
  "tagline" : "You Know, for Search"
}
```

Check the cluster nodes
```bash
[vagrant@elasticsearch ~]$ curl localhost:9200/_cat/nodes

172.28.128.13 11 95 2 0.32 0.21 0.10 mdi - node3
172.28.128.12 12 94 0 0.07 0.11 0.07 mdi * node2
172.28.128.11 14 96 0 0.02 0.14 0.12 mdi - node1
```

Configured directories on the nodes:

Data directory default: `/opt/elasticsearch/data`
Log directory default: `/opt/elasticsearch/logs`
Config directory: `/etc/elasticsearch`

It is using the `ansible.cfg` file where we overwritten the inventory file (`inventory.ini`)

Cleanup:

```bash
vagrant destroy -f
```