Fail2Ban Filter for Ninjafirewall WP Log Files
==============================================

Note: _This will only work if you have full access to your web server's `/etc/fail2ban/` files._

How to use:

* Install [Ninjafirewall WP](https://wordpress.org/plugins/ninjafirewall/) to your WordPress web site.
* Copy [/filter.d/ninjafirewall-logs.conf](https://github.com/wpkc/fail2ban-filter-ninjafirewall-logs/blob/master/filter.d/ninjafirewall-logs.conf) from this repository to `/etc/fail2ban/filter.d/`
* Add a `[ninjafirewall-logs]` section to the Jails section of your `/etc/fail2ban/jail.local` file...
```python
	[ninjafirewall-logs]
	port = http,https
	filter = ninjafirewall-logs
	logpath = /var/www/vhosts/mydomain.com/public_html/wp-content/nfwlog/firewall_*.php
	maxretry = 3
	enabled = true
```
* Restart Fail2Ban: `service fail2ban restart`


Additional Notes:

* Keep the maxretry override value low; 2 or 3 is good. Ninjafirewall is detecting critical or high severity attacks, not accidental password errors by humans.
* If using CloudFlare on the web site, please see the [fail2ban-action-cloudflare-restv4](https://github.com/wpkc/fail2ban-action-cloudflare-restv4) repository for an updated CloudFlare action configuration file.

More info: <https://www.kazimer.com/fail2ban-filter-recipe-ninjafirewall-logs/>
