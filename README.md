# tld-blacklist
A massive .tld blacklist with both a raw and a `*@*.xyz` version for exim4.

Follow these instructions https://forum.hestiacp.com/t/ban-block-an-email-address/5553/2 to implement the exim4 blacklist.


1. Create a file called 'customglobalblacklist' within /etc/exim4/
2. Go in HestiaCP - Settings - Exim4 (edit). This will edit the file: /etc/exim4/exim4.conf.template
3. Add the following rule just above the accept hosts = : line from the acl_check_rcpt block:

        # CUSTOM ADDED ACL
 	      deny senders	= /etc/exim4/customglobalblacklist
 	      message	= You have been blacklisted for sending SPAM.
        # END
