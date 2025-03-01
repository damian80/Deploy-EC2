Accessing an EC2 Instance and Resolving Key File Issues

## Objective
To successfully connect to an EC2 instance using SSH after locating the private key file and troubleshooting access issues.

---

## Steps

### 1. Launch an EC2 Instance
- Follow the AWS EC2 Lab Guide.
- Use the following configurations:
  - **AMI**: Amazon Linux 2023.
  - **Instance Type**: t3.micro (Free Tier eligible).

### 2. Locate the Key File
- Use the following command to locate the private key file on your system:
  ```bash
  find ~ -name "[REDACTED].pem"
  ```
- The key file was found at: `~/.ssh/[REDACTED].pem`.

### 3. Set Correct Permissions for the Key File
- Ensure the key file has the correct permissions:
  ```bash
  chmod 400 ~/.ssh/[REDACTED].pem
  ```
- This restricts access to the file so that only the owner can read it.

### 4. Connect to the EC2 Instance via SSH
- Use the following command to connect to the EC2 instance:
  ```bash
  ssh -i ~/.ssh/[REDACTED].pem ec2-user@[REDACTED]
  ```
- Replace `[REDACTED]` with the public IP address of your EC2 instance if different.

### 5. Verify Connection
- Upon successful connection, you should see a welcome message, such as:
  ```
     ,     #_       Amazon Linux 2023
    ~\_  ####_      https://aws.amazon.com/linux/amazon-linux-2023
   ~~  \_#####\
   ~~     \###|
   ~~       \#/ ___   Welcome to EC2 instance.
    ~~       V~' '->
     ~~~         /
       ~~._.   _/
          _/ _/
        _/m/'
  ```
- The shell prompt will appear as:
  ```
  [ec2-user@ip-[REDACTED] ~]$
  ```

### 6. Terminate the Instance
- Once all tasks are complete, terminate the EC2 instance to avoid additional costs.

### Notes
- `ec2-user` is the default username for Amazon Linux. For other AMIs, this may differ (e.g., `ubuntu` for Ubuntu).
- `~/.ssh/[REDACTED].pem` is the path to your private key file.

---

## Common Issues and Solutions

### Issue: Key File Not Found
- Ensure the key file exists at the specified location (`~/.ssh/[REDACTED].pem`).
- Double-check the file name and path.

### Issue: Permission Denied (Public Key)
- Confirm the key file permissions are correct (`chmod 400`).
- Ensure the correct key file is being used.
- Verify that the public key was added to the `authorized_keys` file on the EC2 instance during setup.

### Debugging
- Use verbose mode to troubleshoot SSH issues:
  ```bash
  ssh -vvv -i ~/.ssh/[REDACTED].pem ec2-user@[REDACTED]
  ```

---

## Good Practices
- Always back up your private key securely.
- Use AWS Systems Manager (SSM) for future access to avoid key management issues.
- Regularly update and monitor the security settings of your EC2 instance.

---

## Resources
- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)
- [Amazon Linux 2023 Overview](https://aws.amazon.com/linux/amazon-linux-2023/)
