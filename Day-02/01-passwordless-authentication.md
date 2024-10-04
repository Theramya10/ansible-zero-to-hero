# How to setup Passwordless Authentication

## EC2 Instances

### Using Public Key

```
ssh-copy-id -f "-o IdentityFile <PATH TO PEM FILE>" ubuntu@<INSTANCE-PUBLIC-IP>
```

- ssh-copy-id: This is the command used to copy your public key to a remote machine.
- -f: This flag forces the copying of keys, which can be useful if you have keys already set up and want to overwrite them.
- "-o IdentityFile <PATH TO PEM FILE>": This option specifies the identity file (private key) to use for the connection. The -o flag passes this option to the underlying ssh command.
- ubuntu@<INSTANCE-IP>: This is the username (ubuntu) and the IP address of the remote server you want to access.

### Using Password 

- Go to the file `/etc/ssh/sshd_config.d/60-cloudimg-settings.conf`
- Update `PasswordAuthentication yes`
- Restart SSH -> `sudo systemctl restart ssh`

Before running above step run the below command 1st.

How to Add SSH .pem File for EC2 Access
Follow these steps to add your SSH .pem file and avoid manually entering the key each time you connect to your EC2 instance:

# 1. Add the SSH key to the SSH agent
sudo ssh-add ~/Downloads/id_rsa.pem

# 2. Move the SSH key to the .ssh directory
mv ~/Downloads/id_rsa.pem ~/.ssh/id_rsa.pem

# 3. Set correct permissions for the private key (restrict access)
chmod 400 ~/.ssh/id_rsa.pem

# 4. Add the key to the SSH agent again (if necessary)
sudo ssh-add ~/.ssh/id_rsa.pem

Now, you should be able to log in to your EC2 instance without entering the key each time:
ssh ec2-user@<your-ec2-public-ip>
