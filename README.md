Stackengine ETCD Demo
=====================

About
-----

This is a tech demo of using the [Factorish](http://github.com/paulczar/factorish) framework to install a CoreOS cluster running [StackEngine](http://stackengine.com) which automatically clusters itself using [Registrator].   Also included is Cadvisor for metrics and logspout for logs.

Using
-----

### Development

This will use vagrant provisioning to build a Factorish StackEngine container and then spin up all of the supporting containers.  See [Factorish](http://github.com/paulczar/factorish) on a more detailed explanation of how this works.

Simply run `$ vagrant up` and wait a few minutes for it to build out the system.  You should then be able to browse to the IP of any of the CoreOS VMs on port 8000 for Stackengine or port 8080 for cadvisor.

### Testing

This will spin up vagrant without provisioning and will then allow you to use `fleet` to schedule and run the necessary containers.

```
$ mode=test vagrant up --no-provision
$ vagrant ssh core-01
$ fleetctl submit share/contrib/fleet/systemd/*.service \
  && fleetctl start registrator@1 registrator@2 registrator@3 \
  && fleetctl start logspout@1 logspout@2 logspout@3 \
  && fleetctl start cadvisor@1 cadvisor@2 cadvisor@3 \
  && fleetctl start stackengine-controller@1 && sleep 60 \
  && fleetctl start stackengine-controller@2 stackengine-controller@3

```


Author(s)
======

Paul Czarkowski (paul@paulcz.net)

License
=======

Copyright 2014 Paul Czarkowski

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
