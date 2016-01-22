---
title: REST APIs
taxonomy:
    category: docs
---

REST API's are gateways to Flint which provide an interface to run flintbits from external systems.
This is the reference document for the REST API and resources provided by Flint.


Structure of REST URL's

To use REST API, external systems will make an HTTP request and parse the HTTP response.

Flint's REST API's use JSON or XML as a communication medium for standard HTTP Methods - Get, Post, Put and Delete.

Structure of REST URI's is as follows:

``` http
http://hostname:port/v1/bit/run/flintbox_name:flintbit_name
```
| Parameter | Description | required |
| ------ | ----------- |
| hostname | Hostname of the server on which Flint is installed ( default is localhost ) | true |
| port | REST API Port Number ( default is 3501 ) | true |
| flintbox-name | Name of the Flintbox ( Git repository ) recently created to store all the Flintbits and configured it ( mybox ) | true |
| flintbit-name | Name of the Flintbit created and added to the Flintbox ( hello.rb ) | true |
