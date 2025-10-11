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

Build the MCP server:

```
cd gdrive-mcp-server
npm install && npm run build
mkdir credentials
export GOOGLE_APPLICATION_CREDENTIALS=.credentials/gcp_oauth_keys.json
```

Drag and drop the `gcp_oauth_keys.json` file (that we obtained from GCP), into the newly created `credentials` folder.

Run this command to obtain access token from Google: `node dist/index.js auth`

This will open a browser for you and ask you to login with your Google credentials. If successful, it will create a file `gdrive-server-credentials.json` in `credentials` directory.
Export these credentials, and run the MCP Server:
```
export MCP_GDRIVE_CREDENTIALS=credentials/.gdrive-server-credentials.json
node dist/index.js
```

This should start the MCP server locally on your EC2 instance \[Should show this output: `Starting Google Drive MCP server`/]

The backend runs the MCP server as a local internal process when it starts. Therefore, we need to copy these credentials to backend server also.

```
mkdir ../backend/credentials
cp -r credentials/ ../backend/
```


