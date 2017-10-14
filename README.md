
```bash
ansible-galaxy install -r requirements
```

This will create clone the role into the roles folder

Run then vagrant up:

```
vagrant up
```

Cleanup:

```bash
vagrant destroy -f
```

```bash
vagran ssh

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

Data directory default: `/var/lib/elasticsearch`
Log directory default: `/var/log/elasticsearch`
Config directory: `/etc/elasticsearch`


Inside the directory you can ping the nodes:

```bash
ansible node1 -m ping
node1 | SUCCESS => {
    "changed": false,
    "failed": false,
    "ping": "pong"
}
```

It is using the `ansible.cfg` file where we overwritten the inventory file (`inventory.ini`)

Install elasticsearch on the nodes:

```bash
ansible-playbook elasticsearch.yml
```