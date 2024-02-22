# Xymon extension to check RBLs.

## Usage

1.0 Copy the file "rblcheck" in /usr/lib/xymon/client/ext/rblcheck

2.0 Create the file /etc/xymon/clientlaunch.d/rblcheck.cfg and copy this inside:

[rblcheck]<br>
	#DISABLED<br>
	ENVFILE /etc/xymon/xymonclient.cfg<br>
	CMD $XYMONCLIENTHOME/ext/rblcheck<br>
	LOGFILE /var/log/xymon/xymonclient.log<br>
	INTERVAL 4h<br>

3.0 Add "rblcheck" value in host column.

4.0 Reload xymon-clien t and xymon server.
