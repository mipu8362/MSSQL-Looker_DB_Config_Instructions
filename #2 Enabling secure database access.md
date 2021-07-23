# Enabling secure database access
https://docs.looker.com/setup-and-management/enabling-secure-db

**Looker-hosted instances**: Many companies prefer to use a Looker-hosted instance for the simplicity, ease of implementation, and reduced support costs. In this case, the data that passes between Looker and the database travels over the public Internet, on shared infrastructure. Consequently, it is important to ensure data security. Use one of the options on this page to ensure your network can connect securely to your Looker-hosted instance.

**Customer-hosted instances**: Customers who are hosting their own Looker instance may be on the same private network as their database. However, if that is not the case, be sure to secure your data as well, perhaps using the types of options suggested on this page. For an IP address allowlist, add to the allowlist the IP address or addresses where your Looker instance is hosted.

The options, from easiest to most difficult, are:

# Option 1: IP Address Allowlist
The first step is to limit access to your data from the network layer. We recommend granting access to your database only from specific, trusted hosts.

All network traffic from Looker will come from one of the following IP addresses, based on the region where your Looker instance is hosted. By default, this will be the United States. Add to the allowlist **each** of the IP addresses in the appropriate region listed on this page. Prohibiting traffic to your database, except from these and other trusted IP addresses, is an easy way to limit data access.




|*These allowlist IP addresses also apply for SFTP and SMTP destinations and for LDAP servers that restrict IP traffic. If you are using custom mail settings for SMTP, be sure to add Looker’s IP addresses to your SMTP server’s IP allowlist. Also, if you want to deliver content from Looker to an SFTP server, be sure to add Looker’s IP addresses to your SFTP server’s IP allowlist or inbound traffic rules. If your LDAP server restricts IP traffic, you will need to add Looker’s IP addresses to your LDAP server’s IP allowlist or inbound traffic rules.*                                                                                                                                                                                                                            |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|




## Legacy Hosting

Instances hosted on Microsoft Azure
For instances that are hosted on Azure, add to the allowlist the IP addresses that match your region:


Virginia, USA (us-east2)
52.147.190.201
