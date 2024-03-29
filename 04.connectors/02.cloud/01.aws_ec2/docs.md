---
title: AWS EC2
taxonomy:
    category: docs
---

With Flint's AWS-EC2 Connector you can launch and manage server instances in Amazon data centers.

With this document, we will be able to use and work with the AWS-EC2 Connector.

## Design Aspects
Perform all standard application operations like Instance, Security Group and Resource Tagging operations available through the Amazon EC2 web services. Some of them are listed below:

* Create instance, security groups and resource tags
* Describe instance, security groups and resource tags
* Delete instance, security groups and resource tags
* Stop instance
* Terminate instance
* Modify instance attributes Also,
* The ability to set Connector execution timeouts
* Synchronous / Asynchronous execution of the Connector



## Connector Configuration

![add_aws_ec2_connector](aws_ec2_conn.png)

##### Configuration parameters
| Parameter | Description | Required |
| ------ | ----------- |
| access-key | Amazon Web Services account Access-key Credentials | true: config/request |
| security-key | Amazon Web Services account Security-key Credentials | true: config/request|

##### Example
``` json
{
  "access-key": "BQBIJKQHGGHHGF3KL5SGQ",
  "security-key": "i2+pesMfdgfdgasdfqwegfdddfg6Qo+fgfdgeHKfdgdfgH0mev"
}
```

## Actions

#### create-instance
Create Instance on AWS-EC2 from given details.

##### Request parameters
| Parameter | Description | Required |
| ------ | ----------- |
| connector_name | Name of the AWS-EC2 Connector to be configured. | true |
| action | Contains the name of the operation: create-instance | true |
| image-id | Specifies the unique ID for the AMI(Amazon Machine Images) | true |
| instance-type | Specifies the type of the instance Valid values are: m1.small, m1.large, m1.xlarge, c1.medium, c1.xlarge, m2.2xlarge, m2.4xlarge, t2.micro | true |
| min-instance | Specifies the minimum number of instances to launch, If Amazon EC2 cannot launch the value specified in the (min-count) element, no instances are launched. Valid values: Any value between 1 and the maximum number of instances allowed for your Amazon EC2 account | false |
| max-instance | Specifies the maximum number of instances to launch, If Amazon EC2 cannot launch the value specified in the (max-count) element, the largest possible number greater than that specified in the (min-count) element is launched. Valid values: Any value between 1 and the maximum number of instances allowed for your Amazon EC2 account | true |
| availability-zone | Specifies the placement constraints or availability zones for launching the required instances For example, us-east-1a is a sample value for the availability zone element. (Default: us-east-1a) | false |
| region | Specifies the region for performing operations on Amazon EC2 (Default value: us-east-1) | true |
| key-name | Specifies the name of the key pair | false |
| subnet-id | Specifies the subnet ID for the Amazon Virtual Private Cloud within which to launch the instance or instances | false |
| access-key | Specifies the credentials for signing the connector request | false |
| security-key | Specifies the credentials for signing the connector request | false |

##### Response parameters
| Parameter | Description  |
| ------ | ----------- |
| instance-info | Amazon EC2 created instance info set |

##### Example
``` ruby
response = @call.connector("amazon-ec2")
                    .set("action","create-instance")
                    .set("image-id","ami-dc1c2b8e")
                    .set("instance-type","t2.micro")
                    .set("min-instance",1)
                    .set("max-instance",1)
                    .set("region","us-east-1")
                    .set("availability-zone","us-east-1a")
                    .set("key-name","flint-test")
                    .set("subnet-id","subnet-4d3c2b1a")
                    .set("security-key","i2+pesMfdgfdgasdfqwegfdddfg6Qo+fgfdgeHKfdgdfgH0mev")
                    .set("access-key","BQBIJKQHGGHHGF3KL5SGQ")
                    .timeout(120000)
                    .sync

#Amazon EC2 Connector Response Meta Parameters
response_exitcode = response.exitcode                   #Exit status code
response_message = response.message                     #Execution status messages
 
#Amazon EC2 Connector Response Parameters
instance_info = response.get("instance-info")           #Amazon EC2 created instance info set
 
instance_info.each do |instance|
	@log.info("Amazon EC2 Instance ID : #{instance.get("instance-id")} | 
							Instance Type : #{instance.get("instance-type")} |
							Instance public IP : #{instance.get("public-ip")} |
							Instance private IP : #{instance.get("private-ip")} ") 
end
```

#### start-instances
Start Instance on AWS-EC2 from given details.

##### Request parameters
| Parameter | Description | Required |
| ------ | ----------- |
| connector_name | Name of the AWS-EC2 Connector to be configured. | true |
| action | Contains the name of the operation: start-instances | true |
| instance-id | Contains one or more instance IDs corresponding to the instances that you want to start, supplied within an array of strings | true  |
| region | Specifies the region for performing operations on Amazon EC2 (Default value: us-east-1) | true |
| access-key | Specifies the credentials for signing the connector request | false |
| security-key | Specifies the credentials for signing the connector request | false |

##### Response parameters
| Parameter | Description  |
| ------ | ----------- |
| started-instances-set | Amazon EC2 started instance info set |

##### Example
``` ruby
response = @call.connector("amazon-ec2")
                    .set("action","start-instances")
                    .set("instance_id","i-1a2b3cd")
                    .set("region","us-east-1")
                    .set("security-key","i2+pesMfdgfdgasdfqwegfdddfg6Qo+fgfdgeHKfdgdfgH0mev")
                    .set("access-key","BQBIJKQHGGHHGF3KL5SGQ")
                    .timeout(120000)
                    .sync

#Amazon EC2 Connector Response Meta Parameters
response_exitcode = response.exitcode                #Exit status code
response_message = response.message                  #Execution status messages
 
#Amazon EC2 Connector Response Parameters
instances_set=response.get("started-instances-set")  #Set of Amazon EC2 started instances
 
instances_set.each do |instance_id|
	@log.info("Amazon EC2 Instance current state : #{instance_id.get("current-state")} |
							previous state : #{instance_id.get("previous-state")} |
							Instance id : #{instance_id.get("instance-id")}")
end
```

#### stop-instances
Stop Instance on AWS-EC2 from given details.

##### Request parameters
| Parameter | Description | Required |
| ------ | ----------- |
| connector_name | Name of the AWS-EC2 Connector to be configured. | true |
| action | Contains the name of the operation: stop-instances | true |
| instance-id | Contains one or more instance IDs corresponding to the instances that you want to stop, supplied within an array of strings | true  |
| region | Specifies the region for performing operations on Amazon EC2 (Default value: us-east-1) | true |
| access-key | Specifies the credentials for signing the connector request | false |
| security-key | Specifies the credentials for signing the connector request | false |

##### Response parameters
| Parameter | Description  |
| ------ | ----------- |
| stop-instance-list | Amazon EC2 stopped instance info set |

##### Example
``` ruby
response = @call.connector("amazon-ec2")
                    .set("action","stop-instances")
                    .set("instance_id","i-1a2b3cd")
                    .set("region","us-east-1")
                    .set("security-key","i2+pesMfdgfdgasdfqwegfdddfg6Qo+fgfdgeHKfdgdfgH0mev")
                    .set("access-key","BQBIJKQHGGHHGF3KL5SGQ")
                    .timeout(120000)
                    .sync
#Amazon EC2 Connector Response Meta Parameters
response_exitcode = response.exitcode               #Exit status code
response_message = response.message                 #Execution status messages
 
#Amazon EC2 Connector Response Parameters
instances_set=response.get("stop-instance-list")    #Set of Amazon EC2 stopped instances
 
instances_set.each do |instance_id|
	@log.info("Amazon EC2 Instance current state : #{instance_id.get("current-state")} |
						previous state : #{instance_id.get("previous-state")} |
						Instance ID : #{instance_id.get("instance-id")}")
end
 
```

#### terminate-instances
Terminate Instance on AWS-EC2 from given details.

##### Request parameters
| Parameter | Description | Required |
| ------ | ----------- |
| connector_name | Name of the AWS-EC2 Connector to be configured. | true |
| action | Contains the name of the operation: terminate-instances | true |
| instance-id | Contains one or more instance IDs corresponding to the instances that you want to terminate, supplied within an array of strings | true  |
| region | Specifies the region for performing operations on Amazon EC2 (Default value: us-east-1) | true |
| access-key | Specifies the credentials for signing the connector request | false |
| security-key | Specifies the credentials for signing the connector request | false |

##### Response parameters
| Parameter | Description  |
| ------ | ----------- |
| terminated-instance-set | Amazon EC2 terminated instance info set |

##### Example
``` ruby
response = @call.connector("amazon-ec2")
                    .set("action","terminate-instances")
                    .set("instance_id","i-1a2b3cd")
                    .set("region","us-east-1")
                    .set("security-key","i2+pesMfdgfdgasdfqwegfdddfg6Qo+fgfdgeHKfdgdfgH0mev")
                    .set("access-key","BQBIJKQHGGHHGF3KL5SGQ")
                    .timeout(120000)
                    .sync

#Amazon EC2 Connector Response Meta Parameters
response_exitcode = response.exitcode                    #Exit status code
response_message = response.message                      #Execution status messages
 
#Amazon EC2 Connector Response Parameters
instances_set = response.get("terminated-instance-set")  #Set of Amazon EC2 terminated instances
 
instances_set.each do |instance_id|
	@log.info("Amazon EC2 Instance current state :  #{instance_id.get("current-state")} |
									previous state : #{instance_id.get("previous-state")}
									Instance ID :    #{instance_id.get("instance-id")}")
end
```

#### reboot-instances
Reboot Instance on AWS-EC2 from given details.

##### Request parameters
| Parameter | Description | Required |
| ------ | ----------- |
| connector_name | Name of the AWS-EC2 Connector to be configured. | true |
| action | Contains the name of the operation: reboot-instances | true |
| instance-id | Contains one or more instance IDs corresponding to the instances that you want to reboot, supplied within an array of strings | true  |
| region | Specifies the region for performing operations on Amazon EC2 (Default value: us-east-1) | true |
| access-key | Specifies the credentials for signing the connector request | false |
| security-key | Specifies the credentials for signing the connector request | false |

##### Response parameters
| Parameter | Description  |
| ------ | ----------- |
| reboot-instance-id | Amazon EC2 rebooted instance info set |

##### Example
``` ruby
response = @call.connector("amazon-ec2")
                    .set("action","reboot-instances")
                    .set("instance_id","i-1a2b3cd")
                    .set("region","us-east-1")
                    .set("security-key","i2+pesMfdgfdgasdfqwegfdddfg6Qo+fgfdgeHKfdgdfgH0mev")
                    .set("access-key","BQBIJKQHGGHHGF3KL5SGQ")
                    .timeout(120000)
                    .sync
                    

#Amazon EC2 Connector Response Meta Parameters
response_exitcode = response.exitcode                   #Exit status code
response_message = response.message                     #Execution status messages
 
#Amazon EC2 Connector Response Parameters
instances_set=response.get("reboot-instance-id")        #Set of Amazon EC2 rebooted instances
 
instances_set.each do |instance_id|
	@log.info("Amazon EC2 rebooted instance : #{instance_id.to_s}")
end 
```

#### describe-instances
Describe Instance on AWS-EC2 from given details.

##### Request parameters
| Parameter | Description | Required |
| ------ | ----------- |
| connector_name | Name of the AWS-EC2 Connector to be configured. | true |
| action | Contains the name of the operation: describe-instances | true |
| instance-id | Contains one or more instance IDs corresponding to the instances that you want to describe, supplied within an array of strings | true  |
| region | Specifies the region for performing operations on Amazon EC2 (Default value: us-east-1) | true |
| access-key | Specifies the credentials for signing the connector request | false |
| security-key | Specifies the credentials for signing the connector request | false |

##### Response parameters
| Parameter | Description  |
| ------ | ----------- |
| reboot-instance-id | Amazon EC2 rebooted instance info set |

##### Example
``` ruby
response = @call.connector("amazon-ec2")
                    .set("action","describe-instances")
                    .set("instance_id","i-1a2b3cd")
                    .set("region","us-east-1")
                    .set("security-key","i2+pesMfdgfdgasdfqwegfdddfg6Qo+fgfdgeHKfdgdfgH0mev")
                    .set("access-key","BQBIJKQHGGHHGF3KL5SGQ")
                    .timeout(120000)
                    .sync
                    

#Amazon EC2 Connector Response Meta Parameters
response_exitcode = response.exitcode                   #Exit status code
response_message = response.message                     #Execution status messages
instances_set = response.get("instances-info")           #Set of Amazon EC2 instances

instances_set.each do |instance|
	@log.info("Amazon EC2 instance image id :	#{instance.get("image-id")} |
								public ip :	#{instance.get("public-ip")} |
								instance type :	#{instance.get("instance-type")} |
								key-name :	#{instance.get("key-name")} |
								private ip :	#{instance.get("private-ip")} |
								hypervisor :	#{instance.get("hypervisor")} |
								kernel id :  #{instance.get("kernel-id")} |
								instance id :  #{instance.get("instance-id")} |
								architecture :  #{instance.get("architecture")} |
								client-token :  #{instance.get("client-token")} |
								instance-lifecycle :  #{instance.get("instance-lifecycle")} |
								platform :  #{instance.get("platform")} |
								state code :  #{instance.get("instance-state-code")} |
								state name :  #{instance.get("instance-state-name")} |
								ramdisk id :  #{instance.get("ramdisk-id")} |
								ebs optimized :  #{instance.get("ebs-optimized")} |
								placement tenancy :  #{instance.get("placement-tenancy")} |
								placement group name :  #{instance.get("placement-group-name")} |
								public DNS name :  #{instance.get("public-DNSname")} |
								root device name :  #{instance.get("root-device-name")} |
								root device type :  #{instance.get("root-device-type")} |
								launch time :  #{instance.get("launch-time")} |
								subnet id :  #{instance.get("subnet-id")} |
								virtualization type :  #{instance.get("virtualization-type")} |
								vpc id :  #{instance.get("vpc-id")} |
								ami launch index :  #{instance.get("ami-launch-index")} |")
end

```

#### list
List Instance on AWS-EC2 from given details.

##### Request parameters
| Parameter | Description | Required |
| ------ | ----------- |
| connector_name | Name of the AWS-EC2 Connector to be configured. | true |
| action | Contains the name of the operation: list | true |
| region | Specifies the region for performing operations on Amazon EC2 (Default value: us-east-1) | true |
| access-key | Specifies the credentials for signing the connector request | false |
| security-key | Specifies the credentials for signing the connector request | false |

##### Response parameters
| Parameter | Description  |
| ------ | ----------- |
| instance-list | Amazon EC2 instance info set |

##### Example
``` ruby
 response = @call.connector("amazon-ec2")
                    .set("action","list")
                    .set("region","us-east-1")
                    .set("security-key","i2+pesMfdgfdgasdfqwegfdddfg6Qo+fgfdgeHKfdgdfgH0mev")
                    .set("access-key","BQBIJKQHGGHHGF3KL5SGQ")
                    .timeout(120000)
                    .sync
                    
#Amazon EC2 Connector Response Meta Parameters
response_exitcode = response.exitcode               #Exit status code
response_message = response.message                 #Execution status messages
 
#Amazon EC2 Connector Response Parameters
instances_list=response.get("instance-list")        #List of Amazon EC2 instances
 
instances_list.each do |instance_id|
	@log.info("Amazon EC2 instance : #{instance_id.to_s}")
end

```

#### create-security-group
Create security group on AWS-EC2 from given details.

##### Request parameters
| Parameter | Description | Required |
| ------ | ----------- |
| connector_name | Name of the AWS-EC2 Connector to be configured. | true |
| action | Contains the name of the operation: create-security-group | true |
| group-name | Specifies the name of the security group Valid values: alphanumeric characters, spaces, dashes, underscores | true |
| group-description | Specifies the description for the security group Valid values: alphanumeric characters, spaces, dashes, underscores | true |
| region | Specifies the region for performing operations on Amazon EC2 (Default value: us-east-1) | true |
| access-key | Specifies the credentials for signing the connector request | false |
| security-key | Specifies the credentials for signing the connector request | false |

##### Response parameters
| Parameter | Description  |
| ------ | ----------- |
| group-id | Amazon EC2 security group id |

##### Example
``` ruby
 response = @call.connector("amazon-ec2")
                    .set("action","create-security-group")
                    .set("region","us-east-1")
                    .set("group-name","flint-group")
                    .set("group-description","flint security group")
                    .set("security-key","i2+pesMfdgfdgasdfqwegfdddfg6Qo+fgfdgeHKfdgdfgH0mev")
                    .set("access-key","BQBIJKQHGGHHGF3KL5SGQ")
                    .timeout(120000)
                    .sync

#Amazon EC2 Connector Response Meta Parameters
response_exitcode = response.exitcode        #Exit status code
response_message = response.message          #Execution status messages
 
#Amazon EC2 Connector Response Parameters
group_id = response.get("group-id")          #Group id of Amazon EC2 Security group
```

#### describe-security-group
Describe security group on AWS-EC2 from given details.

##### Request parameters
| Parameter | Description | Required |
| ------ | ----------- |
| connector_name | Name of the AWS-EC2 Connector to be configured. | true |
| action | Contains the name of the operation: describe-security-group | true |
| group-name | Specifies the name of the security group Valid values: alphanumeric characters, spaces, dashes, underscores | true |
| region | Specifies the region for performing operations on Amazon EC2 (Default value: us-east-1) | true |
| access-key | Specifies the credentials for signing the connector request | false |
| security-key | Specifies the credentials for signing the connector request | false |

##### Response parameters
| Parameter | Description  |
| ------ | ----------- |
| security-group-info | Amazon EC2 security group info |

##### Example
``` ruby
response = @call.connector("amazon-ec2")
                    .set("action","describe-security-group")
                    .set("region","us-east-1")
                    .set("group-name","flint-group")
                    .set("security-key","i2+pesMfdgfdgasdfqwegfdddfg6Qo+fgfdgeHKfdgdfgH0mev")
                    .set("access-key","BQBIJKQHGGHHGF3KL5SGQ")
                    .timeout(120000)
                    .sync

#Amazon EC2 Connector Response Meta Parameters
response_exitcode = response.exitcode                    #Exit status code
response_message = response.message                      #Execution status messages
 
#Amazon EC2 Connector Response Parameters
security_group_info=response.get("security-group-info")  #Set of Amazon EC2 security groups details
 
security_group_info.each do |group_info|
	@log.info("Amazon EC2 Security group owner ID : #{group_info.get("owner-id")} |
									group name : #{group_info.get("group-name")} |
									group description : #{group_info.get("group-description")} |
									group vpc ID : #{group_info.get("vpc-id")} |
									group ID : #{group_info.get("group-id")} |
									group IP Permissions Egress : #{group_info.get("ip-permissions-egress")} |
									group Tags : #{group_info.get("tags")} |
									group IP Permissions : #{group_info.get("ip-permissions")} |")
end

```

#### delete-security-group
Delete security group on AWS-EC2 from given details.

##### Request parameters
| Parameter | Description | Required |
| ------ | ----------- |
| connector_name | Name of the AWS-EC2 Connector to be configured. | true |
| action | Contains the name of the operation: delete-security-group | true |
| group-name | Specifies the name of the security group Valid values: alphanumeric characters, spaces, dashes, underscores | true |
| region | Specifies the region for performing operations on Amazon EC2 (Default value: us-east-1) | true |
| access-key | Specifies the credentials for signing the connector request | false |
| security-key | Specifies the credentials for signing the connector request | false |


##### Example
``` ruby

response = @call.connector("amazon-ec2")
                    .set("action","delete-security-group")
                    .set("region","us-east-1")
                    .set("group-name","flint-group")
                    .set("security-key","i2+pesMfdgfdgasdfqwegfdddfg6Qo+fgfdgeHKfdgdfgH0mev")
                    .set("access-key","BQBIJKQHGGHHGF3KL5SGQ")
                    .timeout(120000)
                    .sync

#Amazon EC2 Connector Response Meta Parameters
response_exitcode = response.exitcode                    #Exit status code
response_message = response.message                      #Execution status messages
```

#### allocate-address
Allocate address on AWS-EC2 from given details.

##### Request parameters
| Parameter | Description | Required |
| ------ | ----------- |
| connector_name | Name of the AWS-EC2 Connector to be configured. | true |
| action | Contains the name of the operation: allocate-address | true |
| region | Specifies the region for performing operations on Amazon EC2 (Default value: us-east-1) | true |
| access-key | Specifies the credentials for signing the connector request | false |
| security-key | Specifies the credentials for signing the connector request | false |

##### Response parameters
| Parameter | Description  |
| ------ | ----------- |
| public-ip | Allocated Public IP of Amazon EC2 |

##### Example
``` ruby
response = @call.connector("amazon-ec2")
                    .set("action","allocate-address")
                    .set("region","us-east-1")
                    .set("security-key","i2+pesMfdgfdgasdfqwegfdddfg6Qo+fgfdgeHKfdgdfgH0mev")
                    .set("access-key","BQBIJKQHGGHHGF3KL5SGQ")
                    .timeout(120000)
                    .sync


#Amazon EC2 Connector Response Meta Parameters
response_exitcode = response.exitcode        #Exit status code
response_message = response.message          #Execution status messages
 
#Amazon EC2 Connector Response Parameters
public_ip = response.get("public-ip")        #Allocated Public IP of Amazon EC2

```

#### release-address
Release address on AWS-EC2 from given details.

##### Request parameters
| Parameter | Description | Required |
| ------ | ----------- |
| connector_name | Name of the AWS-EC2 Connector to be configured. | true |
| action | Contains the name of the operation: release-address | true |
| public-ip | Specifies the IP address that you want to release | true |
| region | Specifies the region for performing operations on Amazon EC2 (Default value: us-east-1) | true |
| access-key | Specifies the credentials for signing the connector request | false |
| security-key | Specifies the credentials for signing the connector request | false |


##### Example
``` ruby
response = @call.connector("amazon-ec2")
                    .set("action","release-address")
                    .set("public-ip","52.73.64.13")
                    .set("region","us-east-1")
                    .set("security-key","i2+pesMfdgfdgasdfqwegfdddfg6Qo+fgfdgeHKfdgdfgH0mev")
                    .set("access-key","BQBIJKQHGGHHGF3KL5SGQ")
                    .timeout(120000)
                    .sync

#Amazon EC2 Connector Response Meta Parameters
response_exitcode = response.exitcode        #Exit status code
response_message = response.message          #Execution status messages

```
#### associate-address
Associate address on AWS-EC2 from given details.

##### Request parameters
| Parameter | Description | Required |
| ------ | ----------- |
| connector_name | Name of the AWS-EC2 Connector to be configured. | true |
| action | Contains the name of the operation: associate-address | true |
| public-ip | Specifies the IP address that you want to release | true |
| instance-id | Specifies the instance to associate with the IP address | true |
| region | Specifies the region for performing operations on Amazon EC2 (Default value: us-east-1) | true |
| access-key | Specifies the credentials for signing the connector request | false |
| security-key | Specifies the credentials for signing the connector request | false |


##### Example
``` ruby
response = @call.connector("amazon-ec2")
                    .set("action","associate-address")
                    .set("instance-id","i-1a2b3cd")
                    .set("public-ip","52.73.64.13")
                    .set("region","us-east-1")
                    .set("security-key","i2+pesMfdgfdgasdfqwegfdddfg6Qo+fgfdgeHKfdgdfgH0mev")
                    .set("access-key","BQBIJKQHGGHHGF3KL5SGQ")
                    .timeout(120000)
                    .sync

#Amazon EC2 Connector Response Meta Parameters
response_exitcode = response.exitcode        #Exit status code
response_message = response.message          #Execution status messages
```

#### disassociate-address
Disassociate address on AWS-EC2 from given details.

##### Request parameters
| Parameter | Description | Required |
| ------ | ----------- |
| connector_name | Name of the AWS-EC2 Connector to be configured. | true |
| action | Contains the name of the operation: disassociate-address | true |
| public-ip | Specifies the IP address that you want to Disassociate | true |
| region | Specifies the region for performing operations on Amazon EC2 (Default value: us-east-1) | true |
| access-key | Specifies the credentials for signing the connector request | false |
| security-key | Specifies the credentials for signing the connector request | false |


##### Example
``` ruby

response = @call.connector("amazon-ec2")
                    .set("action","disassociate-address")
                    .set("public-ip","52.73.64.13")
                    .set("region","us-east-1")
                    .set("security-key","i2+pesMfdgfdgasdfqwegfdddfg6Qo+fgfdgeHKfdgdfgH0mev")
                    .set("access-key","BQBIJKQHGGHHGF3KL5SGQ")
                    .timeout(120000)
                    .sync

#Amazon EC2 Connector Response Meta Parameters
response_exitcode = response.exitcode        #Exit status code
response_message = response.message          #Execution status messages
```

#### describe-addresses
Describe address on AWS-EC2 from given details.

##### Request parameters
| Parameter | Description | Required |
| ------ | ----------- |
| connector_name | Name of the AWS-EC2 Connector to be configured. | true |
| action | Contains the name of the operation: describe-addresses | true |
| public-ip | Specifies the IP address that you want to Describe | true |
| region | Specifies the region for performing operations on Amazon EC2 (Default value: us-east-1) | true |
| access-key | Specifies the credentials for signing the connector request | false |
| security-key | Specifies the credentials for signing the connector request | false |

##### Response parameters
| Parameter | Description  |
| ------ | ----------- |
| public-ips-set | set of public IP of amazon EC2 account |

##### Example
``` ruby
response = @call.connector("amazon-ec2")
                    .set("action","describe-addresses")
                    .set("public-ip","52.73.64.13")
                    .set("region","us-east-1")
                    .set("security-key","i2+pesMfdgfdgasdfqwegfdddfg6Qo+fgfdgeHKfdgdfgH0mev")
                    .set("access-key","BQBIJKQHGGHHGF3KL5SGQ")
                    .timeout(120000)
                    .sync

#Amazon EC2 Connector Response Meta Parameters
response_exitcode = response.exitcode            #Exit status code
response_message = response.message              #Execution status messages
 
public_ips_set = response.get("public-ips-set")  #set of public IP of amazon EC2 account
```

#### create-tags
Create tags AWS-EC2 from given details.

##### Request parameters
| Parameter | Description | Required |
| ------ | ----------- |
| connector_name | Name of the AWS-EC2 Connector to be configured. | true |
| action | Contains the name of the operation: create-tags | true |
| resource-id | Specifies the id of resource to which you want to add tags | true |
| tag-key | Specifies the tag key which you want to assign | true |
| tag-value | Specifies the tag value which you want to assign | true |
| region | Specifies the region for performing operations on Amazon EC2 (Default value: us-east-1) | true |
| access-key | Specifies the credentials for signing the connector request | false |
| security-key | Specifies the credentials for signing the connector request | false |


##### Example
``` ruby
response = @call.connector("amazon-ec2")
                    .set("action","create-tags")
                    .set("resource-id","i-1a2b3cd")
                    .set("tag-key","name")
                    .set("tag-value","flint-vm")
                    .set("region","us-east-1")
                    .set("security-key","i2+pesMfdgfdgasdfqwegfdddfg6Qo+fgfdgeHKfdgdfgH0mev")
                    .set("access-key","BQBIJKQHGGHHGF3KL5SGQ")
                    .timeout(120000)
                    .sync


#Amazon EC2 Connector Response Meta Parameters
response_exitcode = response.exitcode            #Exit status code
response_message = response.message              #Execution status messages
```

#### delete-tags
Delete tags on AWS-EC2 from given details.

##### Request parameters
| Parameter | Description | Required |
| ------ | ----------- |
| connector_name | Name of the AWS-EC2 Connector to be configured. | true |
| action | Contains the name of the operation: delete-tags | true |
| resource-id | Specifies the id of resource from which you want to remove tags | true |
| tag-key | Specifies the tag key which you want to remove | true |
| tag-value | Specifies the tag value which you want to remove | true |
| region | Specifies the region for performing operations on Amazon EC2 (Default value: us-east-1) | true |
| access-key | Specifies the credentials for signing the connector request | false |
| security-key | Specifies the credentials for signing the connector request | false |

##### Example
``` ruby
response = @call.connector("amazon-ec2")
                    .set("action","delete-tags")
                    .set("resource-id","i-1a2b3cd")
                    .set("tag-key","name")
                    .set("tag-value","flint-vm")
                    .set("region","us-east-1")
                    .set("security-key","i2+pesMfdgfdgasdfqwegfdddfg6Qo+fgfdgeHKfdgdfgH0mev")
                    .set("access-key","BQBIJKQHGGHHGF3KL5SGQ")
                    .timeout(120000)
                    .sync

#Amazon EC2 Connector Response Meta Parameters
response_exitcode = response.exitcode            #Exit status code
response_message = response.message              #Execution status messages

```



#### describe-tags
Describe tags on AWS-EC2 from given details.

##### Request parameters
| Parameter | Description | Required |
| ------ | ----------- |
| connector_name | Name of the AWS-EC2 Connector to be configured. | true |
| action | Contains the name of the operation: describe-tags | true |
| resource-id | Specifies the id of resource from which you want to describe tags | true |
| resource-type | Specifies the resource type from which you want to describe tags | true |
| tag-value | Specifies the tag value which you want to remove | true |
| region | Specifies the region for performing operations on Amazon EC2 (Default value: us-east-1) | true |
| access-key | Specifies the credentials for signing the connector request | false |
| security-key | Specifies the credentials for signing the connector request | false |

##### Response parameters
| Parameter | Description  |
| ------ | ----------- |
| tag-set | set of resource tags of amazon EC2 account |

##### Example
``` ruby
response = @call.connector("amazon-ec2")
                    .set("action","describe-tags")
                    .set("resource-id","i-1a2b3cd")
                    .set("resource-type","instance")
                    .set("region","us-east-1")
                    .set("security-key","i2+pesMfdgfdgasdfqwegfdddfg6Qo+fgfdgeHKfdgdfgH0mev")
                    .set("access-key","BQBIJKQHGGHHGF3KL5SGQ")
                    .timeout(120000)
                    .sync

#Amazon EC2 Connector Response Meta Parameters
response_exitcode = response.exitcode        #Exit status code
response_message = response.message          #Execution status messages

tags_set = response.get("tag-set")	#set of resource tags of amazon EC2 account
```

## Connector request error handling
This is how success or failures can be handled for the connector requests within your Flintbit. This would help to take appropriate action if something failed.
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
