
# EC2

## EC2 Linux

### EC2 Linux - User Data Demos

- HTTPD Installation Script

    ```
    #!/bin/bash
    yum update -y
    yum install httpd -y
    service httpd start
    chkconfig httpd on
    IP_ADDR=$(curl https://checkip.amazonaws.com/)
    echo "HTTPD Server Instance running at IP $IP_ADDR" > /var/www/html/index.html
    ```

### EC2 Linux -  Tagging Root Volume - Demos

#### Demo-01

- AMI ID - ami-09e4ba81d75ebeb6a

- Policy Creation JSON Content

    ```
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Action": [
                    "ec2:Describe*",
                    "ec2:CreateTags"
                ],
                "Resource": "*",
                "Effect": "Allow"
            }
        ]
    }
    ```


- Commands
    - AWS_AVAIL_ZONE=$(curl http://169.254.169.254/latest/meta-data/placement/availability-zone)
    - echo $AWS_AVAIL_ZONE

    ```
    AWS_REGION="`echo \"$AWS_AVAIL_ZONE\" | sed 's/[a-z]$//'`"
    ```
    
    - echo $AWS_REGION
    
    - AWS_INSTANCE_ID=$(curl http://169.254.169.254/latest/meta-data/instance-id)
    - echo $AWS_INSTANCE_ID

    - ROOT_VOLUME_IDS=$(aws ec2 describe-instances --region $AWS_REGION --instance-id $AWS_INSTANCE_ID --output text --query Reservations[0].Instances[0].BlockDeviceMappings[0].Ebs.VolumeId)
    - echo $ROOT_VOLUME_IDS  


    - ROOT_VOLUME_TAG_KEY=MyRootTag
    - echo $ROOT_VOLUME_TAG_KEY

    - ROOT_VOLUME_TAG_VALUE=MyRootVolumesValue
    - echo $ROOT_VOLUME_TAG_VALUE

    - aws ec2 create-tags --resources $ROOT_VOLUME_IDS --region $AWS_REGION --tags Key=$ROOT_VOLUME_TAG_KEY,Value=$ROOT_VOLUME_TAG_VALUE


#### Demo-02
- AMI ID - ami-09e4ba81d75ebeb6a
- User Data Script

    ```
    #!/bin/bash
    AWS_AVAIL_ZONE=$(curl http://169.254.169.254/latest/meta-data/placement/availability-zone)
    AWS_REGION="`echo \"$AWS_AVAIL_ZONE\" | sed 's/[a-z]$//'`"
    AWS_INSTANCE_ID=$(curl http://169.254.169.254/latest/meta-data/instance-id)
    ROOT_VOLUME_IDS=$(aws ec2 describe-instances --region $AWS_REGION --instance-id  $AWS_INSTANCE_ID --output text --query Reservations[0].Instances[0].BlockDeviceMappings[0].Ebs.VolumeId)
    ROOT_VOLUME_TAG_KEY=MyRootTag
    ROOT_VOLUME_TAG_VALUE=MyRootVolumesValue
    aws ec2 create-tags --resources $ROOT_VOLUME_IDS --region $AWS_REGION --tags Key=$ROOT_VOLUME_TAG_KEY,Value=$ROOT_VOLUME_TAG_VALUE    
    ```

## EC2 - Windows 

### EC2 Windows - Demo

- N/A

### EC2 Windows - Tagging Root Volume

#### Demo-01

- AMI ID
    - ami-029e3dc669a519be5

- Commands
    - $AWS_AVAIL_ZONE=(curl http://169.254.169.254/latest/meta-data/placement/availability-zone).Content
    - echo $AWS_AVAIL_ZONE

    - $AWS_REGION=$AWS_AVAIL_ZONE.Substring(0,$AWS_AVAIL_ZONE.length-1)
    - echo $AWS_REGION

    - $AWS_INSTANCE_ID=(curl http://169.254.169.254/latest/meta-data/instance-id).Content
    - echo $AWS_INSTANCE_ID

    - $ROOT_VOLUME_IDS=((Get-EC2Instance -Region $AWS_REGION -InstanceId $AWS_INSTANCE_ID).Instances.BlockDeviceMappings | where-object DeviceName -match '/dev/sda1').Ebs.VolumeId
    - echo $ROOT_VOLUME_IDS

    - $tag = New-Object Amazon.EC2.Model.Tag
    - $tag.key = "MyRootTag"
    - $tag.value = "MyRootVolumesValue"
    - echo $tag
    - New-EC2Tag -Resource $ROOT_VOLUME_IDS -Region $AWS_REGION -Tag $tag


#### Demo-02

- AMI ID
    - ami-029e3dc669a519be5
- User Data Content

```
<powershell>
  $AWS_AVAIL_ZONE=(curl http://169.254.169.254/latest/meta-data/placement/availability-zone).Content
  $AWS_REGION=$AWS_AVAIL_ZONE.Substring(0,$AWS_AVAIL_ZONE.length-1)
  $AWS_INSTANCE_ID=(curl http://169.254.169.254/latest/meta-data/instance-id).Content
  $ROOT_VOLUME_IDS=((Get-EC2Instance -Region $AWS_REGION -InstanceId $AWS_INSTANCE_ID).Instances.BlockDeviceMappings | where-object DeviceName -match '/dev/sda1').Ebs.VolumeId
  $tag = New-Object Amazon.EC2.Model.Tag
  $tag.key = "MyRootTag"
  $tag.value = "MyRootVolumesValue"
  New-EC2Tag -Resource $ROOT_VOLUME_IDS -Region $AWS_REGION -Tag $tag
</powershell>
```

# CF

## Allowed Values

- N/A

## Function-Join

- N/A

## CF-SSM Parameter Integration

### Demo-01

- Parameter Store
    - Key - /gl-lab/cf/ec2-instance-type

### Read Parameter value

```
aws ssm get-parameters --names "/aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2"
```

```
aws ssm get-parameters --names "/aws/service/ami-windows-latest/Windows_Server-2016-English-Full-Base"
```


## EC2 Linux - User Data

### Demo-01

- N/A

### Demo-03

- N/A

## EC2 Windows - User Data

### Demo-01

- N/A

## TaskCat

### Demo-01

- Commands 
    ```
    sudo yum -y update
    python3 --version
    curl -O https://bootstrap.pypa.io/get-pip.py
    python3 get-pip.py --user
    pip3 install taskcat --user
    taskcat --version
    ```

    ```
    cd ~/environment/taskcat-demo-01/
    taskcat test run
    ```

    ```
    cd ~/environment/taskcat-demo-02/
    taskcat test run
    ```


