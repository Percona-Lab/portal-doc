# Check mongodb bind IP

## Description
This advisor warns if MongoDB network binding is not set as recommended.

This helps avoid possible security breach from listening to unidentified client IP addresses. 

For more information, see the [MongoDB documentation](https://docs.mongodb.com/manual/reference/configuration-options/#mongodb-setting-net.bindIp).


## Rule
```
MONGODB_GETCMDLINEOPTS
db.adminCommand({'getCmdLineOpts':1}).parsed.net.bindIp


net = parsed.get("net", {})
            bindIP = (net.get("bindIp") == "0.0.0.0")
            bindIP = bindIP or ("bindIpAll" in net)
```

## Resolution
Follow the steps below to adjust network binding settings:

1. Adjust IP addresses in **net.bindIp** or **bindIpAll** boolean flag.
2. Edit **mongod.conf** and set the parameter below:

```
net:
  bindIp: <private IP or hostname of DB server>
  #bindIpAll: false //Any of these parameters might be enabled so adjust accordingly
```
3. Roll-restart your mongod nodes to apply the changes.
   
## Need more support from Percona?
Subscribe to Percona Platform to get database support with guaranteed SLAs or proactive database management services from the Percona team.

[Learn more :fontawesome-solid-paper-plane:](https://per.co.na/subscribe){ .md-button }
