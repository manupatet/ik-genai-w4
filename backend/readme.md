# Procedure
- Create a new EC2 instance (debian t3.small).
- Create new rule and add port 8080 to incoming security group.
- Download the .pem file from security tab.
- Copy the 'Public DNS' from 'details' of the EC2 instance.
- Run the following commands :
```
chown 400 ~/Downloads/backend-pem.pem
ssh -i ~/Downloads/backend-pem.pem admin@ec2-3-80-417-313.compute-1.amazonaws.com
```
