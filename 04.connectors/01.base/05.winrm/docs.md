---
title: Windows WinRM
taxonomy:
    category: docs
---
## WinRM ( Windows Remote Management ) Connector

With Flint's WinRM (Windows Remote Management) Connector you can execute commands on remote Windows server machine using Microsoft implementation of WS-Management Protocol.

With this document guide you will be able to work with and use a WinRM Connector.

## Design Aspects
+ Based on Standardized Microsoft implementation of WS-Management Protocol
+ Password based authentication mechanism
+ Both HTTP and HTTPS Protocol Support
+ Direct access to the command execution results from the remote server machine
+ The ability to set Connector execution timeouts
+ Synchronous/Asynchronous execution of the Connector

## Add WinRM connector

![add_winrm_connector](add-winrm-conn.png)

##### Configuration parameters
| Parameter | Description | Required |
| ------ | ----------- |
| hostname | Host name or ip-address of the host server machine to connect | true |
| username | Connect with specified username, host server machine authentication | true |
| password | Connect with specified password, host server machine authentication | true |
| protocol | Connect with specified protocol, host server machine authentication. Default value is http | false |
| command | Command to be executed on the host server machine | true |
| port | Port to connect to on the host server machine. Default value is 5985 | false |
| timeout | Execution time of the Command in milliseconds(default timeout is 60000 milliseconds) | false |

##### Example
```json
{
  "hostname": "smtp.gmail.com",
  "username": "example@gmail.com",
  "password": "example123",
  "protocol": "https",
  "command": "whoami",
  "post": 5986,
  "timeout": 60000
}
```
## Actions

### Execute commands on Remote Windows Server
Send an email

##### Request parameters
| Parameter | Description | required |
| ------ | ----------- |
| action | Specify action as “send” for sending an email message |	true |
| to | Username is the full email address of the sender's email account| true |
| from |	Usernames of email accounts for whom the email message is meant | true |
| subject	| Specify subject of an email message here|	true |
| body | Email message content mainly a text | true |
| username | Username is the full email address of the sender's email account. Not required, if already specified in configuration file |	false |
| password	| Password associated with the sender's email account. Not required, if already specified in configuration file. |	false |
| port | Port number on which the SMTP server is listening. Default port is **25** | false |
| cc | Usernames of email accounts who need to be kept informed of the email message content, but no actions required from them. Multiple usernames must be given within an array of strings | false |
| bcc |	Usernames of email accounts you don't wish the other recipients to see that you sent it to this contact. Multiple usernames must be given within an array of strings | false |
| attachments |	Files to be attached to an email message. Maximum size of a file that can be attached is 10 Mb. Multiple file names must be given within an array of strings |	false |
| content-type |	Content-type of the email body. Example : text/plain, multipart/alternative etc. Default content-type is **text/html** | false |

##### Response parameters
| Parameter | Description | required |
| ------ | ----------- |
|output	| Message stating the status of mail delivery| true |
|exit-status	| Message stating the status of mail delivery| true |
|error	| Message stating the status of mail delivery| true |


##### Example
``` ruby
response=@call.connector("my-winrm-connector")
              .set("hostname","192.168.2.64")
              .set("username","daniel")
              .set("password","daniel123")
              .set("protocol","http")
              .set("command","whoami")
              .set("port", 5986)
              .set("timeout",1000)
              .sync

#WinRM Connector Response Parameters
result=response.get("output")                    #Output
result=response.get("exit-status")               #Exit status
result=response.get("error")                     #Error output

```

## Connector request error handling
Here is how you can handle the connector requests success or failures within your Flintbit. This would help you to take appropriate action if something failed.
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
