
# Working with EFS

## Launch instances in multiple AZs
1. Create a security group
aws ec2 create-security-group --group-name StorageLabs --description "Temporary SG for the Storage Service Labs"
```shell
output
{
    "GroupId": "sg-0f60b0996e1af7d45",
    "SecurityGroupArn": "arn:aws:ec2:ap-south-1:471486728421:security-group/sg-0f60b0996e1af7d45"
}
```
2. Add a rule for SSH inbound to the security group
aws ec2 authorize-security-group-ingress --group-name StorageLabs --protocol tcp --port 22 --cidr 0.0.0.0/0
```
{
    "Return": true,
    "SecurityGroupRules": [
        {
            "SecurityGroupRuleId": "sgr-0ee58e2181f9361a4",
            "GroupId": "sg-0f60b0996e1af7d45",
            "GroupOwnerId": "471486728421",
            "IsEgress": false,
            "IpProtocol": "tcp",
            "FromPort": 22,
            "ToPort": 22,
            "CidrIpv4": "0.0.0.0/0",
            "SecurityGroupRuleArn": "arn:aws:ec2:ap-south-1:471486728421:security-group-rule/sgr-0ee58e2181f9361a4"
        }
    ]
}
```
3. Launch instance in ap-south-1a
aws ec2 run-instances --image-id ami-01b6d88af12965bb6 --instance-type t3.micro --placement AvailabilityZone=ap-south-1a --security-group-ids sg-0f60b0996e1af7d45

```
{
    "GroupId": "sg-0f60b0996e1af7d45",
    "SecurityGroupArn": "arn:aws:ec2:ap-south-1:471486728421:security-group/sg-0f60b0996e1af7d45"
}
~ $ aws ec2 authorize-security-group-ingress --group-name StorageLabs --protocol tcp --port 22 --cidr 0.0.0.0/0
{
~ $ aws ec2 run-instances --image-id ami-01b6d88af12965bb6 --instance-type t3.micro --placement AvailabilityZone=ap-south-1a --security-group-ids sg-0f60b0996e1af7d45
{
    "ReservationId": "r-0f5c96f6e5e37e3fe",
    "OwnerId": "471486728421",
    "Groups": [],
    "Instances": [
        {
            "Architecture": "x86_64",
            "BlockDeviceMappings": [],
            "ClientToken": "2e79ad7e-623c-4f54-9e91-8fb2ca6f0d58",
            "EbsOptimized": false,
            "EnaSupport": true,
            "Hypervisor": "xen",
            "NetworkInterfaces": [
                {
                    "Attachment": {
                        "AttachTime": "2025-09-19T05:58:40+00:00",
                        "AttachmentId": "eni-attach-0a073c27b5b624001",
                        "DeleteOnTermination": true,
                        "DeviceIndex": 0,
                        "Status": "attaching",
                        "NetworkCardIndex": 0
                    },
                    "Description": "",
                    "Groups": [
                        {
                            "GroupId": "sg-0f60b0996e1af7d45",
                            "GroupName": "StorageLabs"
                        }
                    ],
                    "Ipv6Addresses": [],
                    "MacAddress": "02:cb:6b:b7:d1:49",
                    "NetworkInterfaceId": "eni-09f46b559b74cf503",
                    "OwnerId": "471486728421",
                    "PrivateDnsName": "ip-172-31-35-7.ap-south-1.compute.internal",
                    "PrivateIpAddress": "172.31.35.7",
                    "PrivateIpAddresses": [
                        {
                            "Primary": true,
                            "PrivateDnsName": "ip-172-31-35-7.ap-south-1.compute.internal",
                            "PrivateIpAddress": "172.31.35.7"
                        }
                    ],
                    "SourceDestCheck": true,
                    "Status": "in-use",
                    "SubnetId": "subnet-02cb3c04dd567fdcc",
                    "VpcId": "vpc-0ba4475f062f934d0",
                    "InterfaceType": "interface",
                    "Operator": {
                        "Managed": false
                    }
                }
            ],
            "RootDeviceName": "/dev/xvda",
            "RootDeviceType": "ebs",
            "SecurityGroups": [
                {
                    "GroupId": "sg-0f60b0996e1af7d45",
                    "GroupName": "StorageLabs"
                }
            ],
            "SourceDestCheck": true,
            "StateReason": {
                "Code": "pending",
                "Message": "pending"
            },
            "VirtualizationType": "hvm",
            "CpuOptions": {
                "CoreCount": 1,
                "ThreadsPerCore": 2
            },
            "CapacityReservationSpecification": {
                "CapacityReservationPreference": "open"
            },
            "MetadataOptions": {
                "State": "pending",
                "HttpTokens": "required",
                "HttpPutResponseHopLimit": 2,
                "HttpEndpoint": "enabled",
                "HttpProtocolIpv6": "disabled",
                "InstanceMetadataTags": "disabled"
            },
            "EnclaveOptions": {
                "Enabled": false
            },
            "BootMode": "uefi-preferred",
            "PrivateDnsNameOptions": {
                "HostnameType": "ip-name",
                "EnableResourceNameDnsARecord": false,
                "EnableResourceNameDnsAAAARecord": false
            },
            "MaintenanceOptions": {
                "AutoRecovery": "default",
                "RebootMigration": "default"
            },
            "CurrentInstanceBootMode": "uefi",
            "Operator": {
                "Managed": false
            },
            "InstanceId": "i-0f52cb365a600d972",
            "ImageId": "ami-01b6d88af12965bb6",
            "State": {
                "Code": 0,
                "Name": "pending"
            },
            "PrivateDnsName": "ip-172-31-35-7.ap-south-1.compute.internal",
            "PublicDnsName": "",
            "StateTransitionReason": "",
            "AmiLaunchIndex": 0,
            "ProductCodes": [],
            "InstanceType": "t3.micro",
            "LaunchTime": "2025-09-19T05:58:40+00:00",
            "Placement": {
                "AvailabilityZoneId": "aps1-az1",
                "GroupName": "",
                "Tenancy": "default",
                "AvailabilityZone": "ap-south-1a"
            },
            "Monitoring": {
                "State": "disabled"
            },
            "SubnetId": "subnet-02cb3c04dd567fdcc",
            "VpcId": "vpc-0ba4475f062f934d0",
            "PrivateIpAddress": "172.31.35.7"
        }
    ]
}
(END)
```


4. Launch instance in ap-south-1b
aws ec2 run-instances --image-id ami-01b6d88af12965bb6 --instance-type t3.micro --placement AvailabilityZone=ap-south-1b --security-group-ids sg-0f60b0996e1af7d45
```
{
    "ReservationId": "r-04c3b29ea4503c99e",
    "OwnerId": "471486728421",
    "Groups": [],
    "Instances": [
        {
            "Architecture": "x86_64",
            "BlockDeviceMappings": [],
            "ClientToken": "8f442cf7-c7d5-453c-a282-c664bce1f228",
            "EbsOptimized": false,
            "EnaSupport": true,
            "Hypervisor": "xen",
            "NetworkInterfaces": [
                {
                    "Attachment": {
                        "AttachTime": "2025-09-19T06:00:53+00:00",
                        "AttachmentId": "eni-attach-0df533e0b6aed63bb",
                        "DeleteOnTermination": true,
                        "DeviceIndex": 0,
                        "Status": "attaching",
                        "NetworkCardIndex": 0
                    },
                    "Description": "",
                    "Groups": [
                        {
                            "GroupId": "sg-0f60b0996e1af7d45",
                            "GroupName": "StorageLabs"
                        }
                    ],
                    "Ipv6Addresses": [],
                    "MacAddress": "0a:f9:a4:4e:71:f1",
                    "NetworkInterfaceId": "eni-060f147f03f636a02",
                    "OwnerId": "471486728421",
                    "PrivateDnsName": "ip-172-31-10-111.ap-south-1.compute.internal",
                    "PrivateIpAddress": "172.31.10.111",
                    "PrivateIpAddresses": [
                        {
                            "Primary": true,
                            "PrivateDnsName": "ip-172-31-10-111.ap-south-1.compute.internal",
                            "PrivateIpAddress": "172.31.10.111"
                        }
                    ],
                    "SourceDestCheck": true,
                    "Status": "in-use",
                    "SubnetId": "subnet-0d182f5216a05a5b1",
                    "VpcId": "vpc-0ba4475f062f934d0",
                    "InterfaceType": "interface",
                    "Operator": {
                        "Managed": false
                    }
                }
            ],
            "RootDeviceName": "/dev/xvda",
            "RootDeviceType": "ebs",
            "SecurityGroups": [
                {
                    "GroupId": "sg-0f60b0996e1af7d45",
                    "GroupName": "StorageLabs"
                }
            ],
            "SourceDestCheck": true,
            "StateReason": {
                "Code": "pending",
                "Message": "pending"
            },
            "VirtualizationType": "hvm",
            "CpuOptions": {
                "CoreCount": 1,
                "ThreadsPerCore": 2
            },
            "CapacityReservationSpecification": {
                "CapacityReservationPreference": "open"
            },
            "MetadataOptions": {
                "State": "pending",
                "HttpTokens": "required",
                "HttpPutResponseHopLimit": 2,
                "HttpEndpoint": "enabled",
                "HttpProtocolIpv6": "disabled",
                "InstanceMetadataTags": "disabled"
            },
            "EnclaveOptions": {
                "Enabled": false
            },
            "BootMode": "uefi-preferred",
            "PrivateDnsNameOptions": {
                "HostnameType": "ip-name",
                "EnableResourceNameDnsARecord": false,
                "EnableResourceNameDnsAAAARecord": false
            },
            "MaintenanceOptions": {
                "AutoRecovery": "default",
                "RebootMigration": "default"
            },
            "CurrentInstanceBootMode": "uefi",
            "Operator": {
                "Managed": false
            },
            "InstanceId": "i-040712d8e9986254f",
            "ImageId": "ami-01b6d88af12965bb6",
            "State": {
                "Code": 0,
                "Name": "pending"
            },
            "PrivateDnsName": "ip-172-31-10-111.ap-south-1.compute.internal",
            "PublicDnsName": "",
            "StateTransitionReason": "",
            "AmiLaunchIndex": 0,
            "ProductCodes": [],
            "InstanceType": "t3.micro",
            "LaunchTime": "2025-09-19T06:00:53+00:00",
            "Placement": {
                "AvailabilityZoneId": "aps1-az3",
                "GroupName": "",
                "Tenancy": "default",
                "AvailabilityZone": "ap-south-1b"
            },
            "Monitoring": {
                "State": "disabled"
            },
            "SubnetId": "subnet-0d182f5216a05a5b1",
            "VpcId": "vpc-0ba4475f062f934d0",
            "PrivateIpAddress": "172.31.10.111"
        }
    ]
}
(END)

```
## Create an EFS File System
1. Add a rule to the security group to allow the NFS protocol from group members

```aws ec2 authorize-security-group-ingress --group-id sg-0f60b0996e1af7d45 --protocol tcp --port 2049 --source-group sg-0f60b0996e1af7d45```
```
{
    "Return": true,
    "SecurityGroupRules": [
        {
            "SecurityGroupRuleId": "sgr-0973ef708bcaadae4",
            "GroupId": "sg-0f60b0996e1af7d45",
            "GroupOwnerId": "471486728421",
            "IsEgress": false,
            "IpProtocol": "tcp",
            "FromPort": 2049,
            "ToPort": 2049,
            "ReferencedGroupInfo": {
                "GroupId": "sg-0f60b0996e1af7d45",
                "UserId": "471486728421"
            },
            "SecurityGroupRuleArn": "arn:aws:ec2:ap-south-1:471486728421:security-group-rule/sgr-0973ef708bcaadae4"
        }
    ]
}

```
2. Create an EFS file system through the console, and add the StorageLabs security group to the mount targets for each AZ



## Mount using the NFS Client (perform steps on both instances)
1. Create an EFS mount point
mkdir ~/efs-mount-point
2. Install NFS client
sudo yum -y install nfs-utils
```
[ec2-user@ip-172-31-35-7 ~]$ mkdir ~/efs-mount-point
[ec2-user@ip-172-31-35-7 ~]$ ls
efs-mount-point
[ec2-user@ip-172-31-35-7 ~]$ sudo yam -y install nfs-utils
sudo: yam: command not found
[ec2-user@ip-172-31-35-7 ~]$ sudo yum -y install nfs-utils
Amazon Linux 2023 Kernel Livepatch reposi 227 kB/s |  23 kB     00:00    
Package nfs-utils-1:2.5.4-2.rc3.amzn2023.0.3.x86_64 is already installed.
Dependencies resolved.
Nothing to do.
Complete!
```
3. Mount using the EFS client
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-027246e577aff0d9f.efs.ap-south-1.amazonaws.com:/ ~/efs-mount-point
4. Create a file on the file system
```


```
5. Add a file system policy to enforce encryption in-transit
6. Unmount (make sure to change directory out of efs-mount-point first)
sudo umount ~/efs-mount-point
4. Mount again using the EFS client (what happens?)

## Mount using the EFS utils (perform steps on both instances)
1. Install EFS utils
sudo yum install -y amazon-efs-utils
2. Mount using the EFS mount helper
sudo mount -t efs -o tls fs-027246e577aff0d9f.efs.ap-south-1.amazonaws.com:/ ~/efs-mount-point