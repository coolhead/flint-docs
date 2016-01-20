---
title: File
taxonomy:
    category: docs
---
## File Connector

With Flint's File Connector you can perform read, write, append and delete operations on a file. You can configure your connector with Flint's File Connector to suite your special demands without the need to extend or replace any inbuilt code. After configuring, with your scripting skills Flint will automate the workflow.Thus, without any compromise Performance, Stability and Flexibility all are packaged into Flint's File Connector.

With this document guide you will be able to work with and use a File Connector.While you start configuring the connector, this document will guide you through File Connector request and response parameters.


## Configuring file connector
No additional configuration is required for file connector

![add_file_connector](add-file-conn.png)

## Actions

### Read a file: read
Read a file form local file system

``` ruby
response = @call.connector("file_connecor_name")
                .set("action","read")
                .set("file","/path/of/file/to/read")
                .sync

response_file = response.get("file")  #File read
file_content = response.get("body")  #Response Body, data read from the file
```
### Write to a file: write
Write content to file
``` ruby
response = @call.connector("file_connecor_name")
                .set("action","write")
                .set("file","/file/to/write")
                .set("data","some data to write")
                .sync

```
### Append to a file: append
Append content to file
``` ruby
response = @call.connector("file_connecor_name")
                .set("action","append")
                .set("file","/file/to/append")
                .set("data","some data to append")
                .sync

```

### Delete a file: delete
Delete a file
``` ruby
response = @call.connector("file_connecor_name")
                .set("action","delete")
                .set("file","/file/to/delete")
                .sync

```

## Connector response
Here is how to interpret connector response.
``` ruby
if response.exitcode == 0               # 0 is success.
  puts "success"
  # take action in case of success
else                                    # non zero means fail
  puts "fail"
  puts "Reason:" + response.message     # get the reason of failure
  ## Take action in case of failure
end

```
