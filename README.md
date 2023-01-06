# Simple and effective plugin based log parser to ban IP addresses with PF
There must be a pf table called brutes
```
# declare a brutes table
table <brutes> persist
# block any brutes
block log quick from <brutes> to any
block log quick from any to <brutes>
# the pf throttle overflow into brutes for ssh connections
pass in log on egress inet proto tcp from ! <brutes> to port ssh modulate state \
   (max-src-conn 1, max-src-conn-rate 1/86400, overload <brutes> flush global)
```
## Plugins
To enable any of the following plugins
### dovecot
```
echo brutifuld dovecot \& >> /etc/rc.local
```
### roundcube
```
echo brutifuld roundcube \& >> /etc/rc.local
```
### opensmtpd
```
echo brutifuld smtpd-invalid \& >> /etc/rc.local
echo brutifuld smtpd-password \& >> /etc/rc.local
```
### sshd
```
echo brutifuld sshd \& >> /etc/rc.local
```
