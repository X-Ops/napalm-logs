# napalm-logs

napalm-logs is a Python library that listens to syslog messages from network
devices and returns strucuted data following the [OpenConfig](http://www.openconfig.net/)
or [IETF](https://github.com/YangModels/yang/tree/master/standard/ietf) YANG models.


<img src="logo.png" data-canonical-src="logo.png" width="300" />

The outgoing objects are published via ZeroMQ, Kafka, or other usual transport
options. It is easy enough to switch between transports and pluggable to add
others such as Google Datastore, RabbitMQ, etc.

Similarly, the syslog messages can be received via UDP, TCP, or different
services, such as  Kafka, etc.

New platforms can be easily added, just referencing the path to the
YAML configuration file.

Requirements
------------

- PyYAML
- PyZMQ
- PyNaCl
- u-msgpack-python

Installation
------------

```
pip install napalm-logs
```

Output object example
---------------------

```json
{
  "ip": "127.0.0.1",
  "host": "re0.edge01.bjm01",
  "message_details": {
    "processId": "2902",
    "error": "BGP_PREFIX_THRESH_EXCEEDED",
    "pri": "149",
    "processName": "rpd",
    "host": "re0.edge01.bjm01",
    "time": "12:45:19",
    "date": "Mar 30",
    "message": "1.2.3.4 (External AS 15169): Configured maximum prefix-limit threshold(160) exceeded for inet-unicast nlri: 181 (instance master)"
  },
  "open_config": {
    "bgp": {
      "neighbors": {
        "neighbor": {
          "1.2.3.4": {
            "neighbor-address": "1.2.3.4",
            "state": {
              "peer-as": 15169
            },
            "afi-safis": {
              "afi-safi": {
                "inet": {
                  "state": {
                    "prefixes": {
                      "received": 181
                    }
                  },
                  "ipv4-unicast": {
                    "prefix-limit": {
                      "state": {
                        "max-prefixes": 160
                      }
                    }
                  },
                  "afi-safi-name": "inet"
                }
              }
            }
          }
        }
      }
    }
  },
  "timestamp": "1490877919"
}
```
