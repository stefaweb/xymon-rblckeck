# Installation Guide for RBLCheck Integration with Xymon

This guide outlines the steps to integrate the `rblcheck` script with your Xymon monitoring system.

## 1.0 Copy the RBLCheck Script

First, you need to place the `rblcheck` script into the Xymon client extensions directory.

```bash
cp rblcheck /usr/lib/xymon/client/ext/rblcheck
```markdown

## 2.0 Configure the Client Launch Settings

Create a new configuration file for `rblcheck` under the Xymon client launch configurations.

1. Create the file `/etc/xymon/clientlaunch.d/rblcheck.cfg`.
2. Insert the following configuration:

```ini
[rblcheck]
#DISABLED
ENVFILE /etc/xymon/xymonclient.cfg
CMD $XYMONCLIENTHOME/ext/rblcheck
LOGFILE /var/log/xymon/xymonclient.log
INTERVAL 4h
```

## 3.0 Update Xymon Host Configuration

Add the `rblcheck` column to the hosts you wish to monitor for RBL listings. This is usually done in the Xymon hosts configuration file.

## 4.0 Reload Xymon Services

For the changes to take effect, you need to reload both the Xymon client and the Xymon server services.

Depending on your system, this can typically be done with commands like:

```bash
systemctl restart xymon-client
systemctl restart xymon-server
```

Or, if your system uses a different service management system, use the appropriate commands to restart the Xymon client and server.

---

After completing these steps, your Xymon system should start monitoring the specified hosts for RBL listings using the `rblcheck` script.
```

Note: Adjust the markdown code blocks as needed, depending on your specific GitHub repository setup. This markdown layout provides a structured way to document the installation and setup process for users.
