---
title: Adding worknodes to grid
taxonomy:
    category: docs
---

## Flint Grid

Adding more than one node to grid gives you lot of advantages:

* Makes the setup highly available.
* Automatically load balance flintbit jobs.
* Automatically load balance connector requests.
* Makes Connectors and Listeners highly available.


## Add nodes in cluster.xml
To setup a grid, all the flint worknode hostnames must be configured in cluster.xml file

``` xml
<tcp-ip enabled="true" connection-timeout-seconds="10">
      <member>worknode1.example.com</member>                      <!--hostname of the server itself-->
      <member>worknode2.example.com</member>                       <!--hostname of the other server-->
</tcp-ip>
```


This will enable flint to identify fellow worknodes and connect to them.

## Configure group in cluster.xml

All nodes of a grid must have same **name** and **password** in cluster.xml file

``` xml
<group>
  <!--
    Grid Name: Name of grid keep it unique if you have multiple grids in same network
    Grid password: All nodes must have same password to join in a grid
  -->
  <name>dev</name>
  <password>dev-pass</password>
</group>

```

> This is all you need to do for grid configuration.

---

## Automatic Work Nodes Discovery (Optional)

If you want a dynamic grid and let flint automatically discover worknodes then you must configure **multicast** option in **cluster.xml**.
You also need to configure **multicast-group** and **multicast-port**.

Make sure you **disable** tcp-ip option in cluster.xml before doing this configuration.

>>>>> To make this work the network must have multicast communication enabled.


``` xml
<!--
  Enable multicast grid detection. Your network must support multicast.
-->
<multicast enabled="true">
  <multicast-group>224.2.2.3</multicast-group>
  <multicast-port>54327</multicast-port>
</multicast>
```
