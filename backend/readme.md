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

- Validate that shell connects to remote EC2 box (you can now diconnect and close the terminal)
- Run this same ssh command on VSC (SSH extension), and open the remote EC2 box on VSC.
- Open the terminal and run:
```
sudo apt update && sudo apt install git npm
mkdir repo/
cd repo
git clone https://github.com/manupatet/ik-genai-w4.git
cd ik-genai-w4
```

