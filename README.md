# radius


Configuring a RADIUS server on Windows Server 2012 R2 and adding Cisco switches as clients involves several steps. RADIUS (Remote Authentication Dial-In User Service) is commonly used for centralized authentication and authorization. Below is a step-by-step guide:

### Configuring RADIUS Server on Windows Server 2012 R2:

#### 1. Install the Network Policy Server (NPS) Role:

- Open "Server Manager" on your Windows Server.
- Select "Manage" > "Add Roles and Features."
- Choose "Network Policy and Access Services" during the installation process.
- Install the "Network Policy Server" role.

#### 2. Configure RADIUS Server:

- Open "Network Policy Server" from "Server Manager."
- In the left pane, right-click on "RADIUS Clients" and choose "New."
- Enter the required information for your Cisco switch as a RADIUS client, including the IP address and shared secret.

#### 3. Create Network Policies:

- In "Network Policy Server," go to "Policies" in the left pane.
- Right-click on "Network Policies" and choose "New."
- Create a policy for RADIUS clients. Define conditions, constraints, and settings based on your requirements.

#### 4. Configure Connection Request Policies:

- In "Network Policy Server," go to "Policies" > "Connection Request Policies."
- Right-click and choose "New." Set conditions to match your network requirements.

#### 5. Configure RADIUS Accounting (optional):

- If you need accounting information, configure RADIUS accounting. In "Network Policy Server," go to "Policies" > "Connection Request Policies" > [Your Policy] > "Settings" > "Accounting."

### Adding Cisco Switch as a RADIUS Client:

#### 1. Access Cisco Switch Configuration Mode:

- Log in to your Cisco switch via SSH, Telnet, or console connection.

#### 2. Enter Global Configuration Mode:

```bash
enable
configure terminal
```

#### 3. Configure RADIUS Settings:

```bash
radius-server host [RADIUS Server IP] auth-port 1812 acct-port 1813
radius-server key [Shared Secret]
```

Replace `[RADIUS Server IP]` with your Windows Server IP and `[Shared Secret]` with the secret you set during the RADIUS client configuration on the Windows Server.

#### 4. Enable RADIUS Authentication:

```bash
aaa new-model
aaa authentication login default group radius local
aaa authentication enable default group radius enable
```

#### 5. Save Configuration:

```bash
write memory
```

These steps should configure your Cisco switch as a RADIUS client to the Windows Server 2012 R2 NPS. Adjust the IP addresses, shared secrets, and other parameters based on your network setup.

Always remember to follow best practices for security, such as using strong shared secrets and restricting access to RADIUS communication.
