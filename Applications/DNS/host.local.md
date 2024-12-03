# Setting Up Your Linux Machine to Be Reachable by `mymachine.local`

Follow these steps to configure your Linux machine and ensure it can be accessed using the hostname `mymachine.local`.

---

## **1. Configure the Hostname**

### **Step 1.1: Set the Hostname**
Run the following command to set the hostname:

```bash
sudo hostnamectl set-hostname mymachine
```

Verify the hostname with:

```bash
hostnamectl
```

### **Step 1.2: Edit the `/etc/hosts` File**
1. Open the `/etc/hosts` file in a text editor:

    ```bash
    sudo nano /etc/hosts
    ```

2. Add the following entry for your hostname:
    ```
    127.0.0.1    mymachine.local mymachine
    ```

3. Optionally, add your machine's LAN IP if known:
    ```
    192.168.1.10    mymachine.local mymachine
    ```

### **Step 1.3: Restart the Hostname Service**
To apply the changes, restart the hostname service:

```bash
sudo systemctl restart systemd-hostnamed
```

---

## **2. Configure the Network**

### **Step 2.1: Enable Avahi Daemon**
1. Install the `avahi-daemon` package if not already installed:

    ```bash
    sudo apt update
    sudo apt install avahi-daemon
    ```

2. Start and enable the service:

    ```bash
    sudo systemctl start avahi-daemon
    sudo systemctl enable avahi-daemon
    ```

### **Step 2.2: Verify Avahi Daemon**
Check the status of the Avahi service:

```bash
sudo systemctl status avahi-daemon
```

Confirm that the machine advertises its hostname on the network:

```bash
avahi-browse -a
```

---

## **3. Configure the Client Machines**

### **Step 3.1: Linux Clients**
1. Install the required package for mDNS support:

    ```bash
    sudo apt install libnss-mdns
    ```

2. Modify `/etc/nsswitch.conf` to prioritize `mdns`:

    ```
    hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4
    ```

### **Step 3.2: Windows Clients**
Windows supports `.local` hostnames natively. No additional configuration is required.

### **Step 3.3: macOS Clients**
macOS also has built-in mDNS support. Simply use `mymachine.local` to connect.

---

## **4. Test the Configuration**

### **Step 4.1: From the Linux Machine**
Test local hostname resolution:

```bash
ping mymachine.local
```

### **Step 4.2: From Another Machine**
Test connectivity from another machine on the same network:

- **Ping the Linux machine:**

    ```bash
    ping mymachine.local
    ```

- **SSH into the Linux machine:**

    ```bash
    ssh username@mymachine.local
    ```

---

## **5. Optional: Assign a Static IP**

To ensure consistent hostname resolution, assign a static IP to your Linux machine:

1. Log in to your router’s admin interface.
2. Locate the DHCP settings.
3. Bind your Linux machine's MAC address to a static IP.
4. Update the `/etc/hosts` file with the static IP if necessary.

---

## **Conclusion**
After completing these steps, your Linux machine will be reachable via `mymachine.local` on your local network.
