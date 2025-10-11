# Preperatory Procedure to bring up an instance from scratch

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

## Here starts the procedure for Codespaces (does not need preperatory steps dure to Dockerfile config)

Run these commands to setup the box for the build.

```
cd gdrive-mcp-server
npm install && npm run build
mkdir .credentials
export GOOGLE_APPLICATION_CREDENTIALS=.credentials/gcp_oauth_keys.json
export MCP_GDRIVE_CREDENTIALS=.credentials/.gdrive-server-credentials.json
```

Copy (Drag and drop) the `gcp_oauth_keys.json` file (that we obtained from GCP, rename if necessary), into the newly created `.credentials` folder.

Run this command to obtain access token from Google: 
```
node dist/index.js auth
```

This will open a browser for you and ask you to login with your Google credentials. If successful, it will create a file `gdrive-server-credentials.json` in `credentials` directory.

We're ready to run the server: `node dist/index.js`

This should start the MCP server locally on the box \[With this output: `Starting Google Drive MCP server`/]

The backend runs the MCP server as a local internal process when it starts. Therefore, we need to copy these credentials to backend server also.

```
mkdir ../backend/credentials
cp -r credentials/ ../backend/
```
