# RBLCheck for Xymon

RBLCheck checks IPv4 addresses against DNS blocklists and reports the results in the Xymon `rblcheck` column.

## Install on Debian

1. Install the `bind9-dnsutils` package if `dig` is unavailable.
2. Edit the `ips` array in `rblcheck` and replace the example address with the public IPv4 addresses to monitor.
3. Install the script as an executable Xymon client extension:

   ```bash
   sudo install -m 0755 rblcheck /usr/lib/xymon/client/ext/rblcheck
   ```

4. Create `/etc/xymon/clientlaunch.d/rblcheck.cfg`:

   ```ini
   [rblcheck]
   ENVFILE /etc/xymon/xymonclient.cfg
   CMD $XYMONCLIENTHOME/ext/rblcheck
   LOGFILE /var/log/xymon/xymonclient.log
   INTERVAL 4h
   ```

   Make sure the active Xymon launcher includes the task file. The column appears on the reporting host after Xymon receives the first status. Each status is valid for eight hours.

Preview the report under the Xymon account without publishing it:

```bash
sudo -u xymon /usr/lib/xymon/client/ext/rblcheck --stdout
```

## Read the report

- **Green** means every check on the enabled lists completed without a listing.
- **Yellow** means a check was inconclusive or a provider failed its self-test, with no confirmed listing.
- **Red** means at least one listing was confirmed. The **Delisting** column links to the provider's lookup or removal page.

Sender Score and SpamRATS are optional. To enable Sender Score, register the resolver used by Xymon with Validity and set `RBLCHECK_SENDERSCORE=1` in the task environment. To enable SpamRATS, configure a resolver that meets SpamRATS requirements and set `RBLCHECK_SPAMRATS_KEY` in that environment. Keep the key out of the repository.
