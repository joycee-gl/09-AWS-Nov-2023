
# Contents / Commands

- AWS CLI
  - Download Link
    - <https://awscli.amazonaws.com/AWSCLIV2.msi>

- Python
  - Download Link
    - <https://www.python.org/downloads/>

- EC2 Launch Commands

  - Public IP Check
    - <https://checkip.amazonaws.com/>

  - EC2 AMI
    - ami-0b72821e2f351e396
    - Note
      - Amazon linux 2023 AMI in N Virginia

- Python App
  - Download URL
    - <https://d6opu47qoi4ee.cloudfront.net/loadbalancer/simuapp-v1.zip>

  - Additional Commands
    - sed -i "s=MOD_APPLICATION_NAME=$APP_NAME=g" templates/index.html
    - nohup python3 simu_app.py >> application.log 2>&1 &
