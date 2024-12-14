
# Contents / Commands

- CIDR to IP Range Conversion
    - https://www.ipaddressguide.com/cidr

- Key Pair
    - gl-lab-03

- Upload the file
    - Change Permission
        - chmod 400 ./gl-lab-03.pem
    - Using SCP to upload the files
        - scp -i ./gl-lab-03.pem ./CF-Template-Files/v2-Work/CF1.json ec2-user@54.163.46.248:~

        - scp -i ./gl-lab-03.pem ./CF-Template-Files/v2-Work/CF2.json ec2-user@54.163.46.248:~
            
- Verify the Upload Operation
    - SSH Connect to EC2
        - ssh -i ./gl-lab-03.pem ec2-user@54.163.46.248

- Supply permission to EC2 instance
    - aws configure

    - Details
        - AWS Access Key ID : 
            - Refer 'accessid' in the Nuvepro Console
        - AWS Secret Access Key : 
            - Refer 'accesskey' in the Nuvepro Console
        - Default Region: us-east-1
        - Default output format : json

- Execute the CF files
    - CF1.json
        - aws cloudformation create-stack --stack-name gl-lab-03-stack --template-body file://./CF1.json

    - CF2.json
        - aws cloudformation create-stack --stack-name gl-lab-03-stack --template-body file://./CF2.json

- Screenshots
    - Screenshot #1
        - CF1.json edited with the changes

    - Screenshot #2
        - CF2.json edited with the changes
    
    - Screenshot #3
        - Subnet creation page

    - Screenshot #4
        - Response of the CF create stack command with CF1.json

    - Screenshot #5
        - Response of the CF create stack command with CF2.json
        
    - Screenshot #6
        - Events log of CF showing security group name as 'WebServerSecurityGroup'

    - Screenshot #7
        - Response from EC2 Server 1

    - Screenshot #8
        - Response from EC2 Server 2
        



