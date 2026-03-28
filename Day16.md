**Task: Firewall Configuration**

The Nautilus system administrators team has rolled out a web UI application for their backup utility on the Nautilus application server 2 within the Stratos Datacenter. This application runs on port 5003and appropriate firewall rules must be configured to allow incoming traffic. To achieve this, firewalld needs to be installed and configured on the application server. To ensure proper functionality, the following requirements have been identified:
Install and enable the firewalld service.
Allow all incoming connections on port 5003/tcp.
Ensure the zone is set to public.

**Solution:**

To secure the backup utility's web UI on App Server 2, you will need to install, activate, and configure firewalld. In the Stratos Datacenter, firewalld acts as a dynamic manager for the underlying iptables rules, making it easier to manage ports and zones.

1. Install and Enable Firewalld
First, ensure the package is installed and set to start automatically upon boot.

# Install the package
sudo yum install -y firewalld

# Start the service and enable it for boot
sudo systemctl start firewalld
sudo systemctl enable firewalld
2. Configure the Port and Zone
By default, the active zone is usually public, but we will explicitly target it to fulfill the requirement. The --permanent flag is essential here; without it, your rules will vanish the next time the server reboots.

# Add port 5003/tcp to the public zone
sudo firewall-cmd --zone=public --add-port=5003/tcp --permanent
3. Apply the Changes
Adding a "permanent" rule does not apply it to the running configuration immediately. You must reload the service to inject the new rules into the active firewall state.

sudo firewall-cmd --reload
4. Verification
It is a best practice in the Nautilus project to verify your work before moving to the next task. Run the following command to see all active rules for the public zone:

sudo firewall-cmd --zone=public --list-all
Expected Output:

Plaintext
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: eth0
  sources: 
  services: dhcpv6-client ssh
  ports: 5003/tcp
  protocols: 
  masquerade: no
  forward-ports: 
  source-ports: 
  icmp-blocks: 
  rich rules:
(The ports: 5003/tcp line confirms the backup utility UI can now receive incoming traffic.)

