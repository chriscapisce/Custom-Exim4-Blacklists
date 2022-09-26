# Custom Exim4 Blacklists

A few blacklists exim4.

### 1/3 How to implement the exim4 blacklist(s) (into HestiaCP):
Source: https://forum.hestiacp.com/t/ban-block-an-email-address/5553/2

1. Create a file called 'customglobaltldblacklist' within /etc/exim4/
2. Go in HestiaCP - Settings - Exim4 (edit). This will edit the file: /etc/exim4/exim4.conf.template
3. Add the following rule just above the accept hosts = : line from the acl_check_rcpt block:

        # CUSTOM ADDED ACL
	   deny senders	        = /etc/exim4/customglobaltldblacklist
	   message	        = You have been blacklisted for sending SPAM.
	   deny senders	        = /etc/exim4/customglobaldomainblacklist
	   message	        = You have been blacklisted for sending SPAM.
	   deny senders	        = /etc/exim4/customglobalemailblacklist
	   message	        = You have been blacklisted for sending SPAM.
        # END

It will look like this:
	
	acl_check_rcpt:

        # CUSTOM ADDED ACL
           deny senders	        = /etc/exim4/customglobaltldblacklist
	   message	        = You have been blacklisted for sending SPAM.
	   deny senders	        = /etc/exim4/customglobaldomainblacklist
	   message	        = You have been blacklisted for sending SPAM.
	   deny senders	        = /etc/exim4/customglobalemailblacklist
	   message	        = You have been blacklisted for sending SPAM.
        # END

	accept hosts = :
        
4. Update the Exim4 configuration:
 
        root@host:~$	update-exim4.conf

5. Restart the exim4 service:
        
        root@host:~$	systemctl restart exim4.service

### 2/3 How to format the exim4 blacklist:
Source: https://marc.info/?l=exim-users&m=146279505017913&w=2

Both names and wildcards (*) such as the following work:

	name@*.tld
	*@name.tld
	*@*.tld
	
### 3/3: How to update/ edit the exim4 blacklist:

1. Add records to the blacklist (customglobalblacklist)

		root@host:~$	cd /etc/exim4/ 
		root@host:~$ 	nano customglobaltldblacklist

2. Update the Exim4 configuration:

		root@host:~$	update-exim4.conf

3. Restart the exim4 service:

		root@host:~$	systemctl restart exim4.service

