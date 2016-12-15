### automatic sync of certificates across other servers
    
Add the ssh key of a read-only gitlab user authorized on ssl-certificates repo 
    
Copy `sync-ssl-certs.sh` script to `/usr/local/bin`

Use it in a cron job like this for daily runs:

	$ sudo crontab -e
	0 3 * * * /usr/local/bin/sync-ssl-certs.sh