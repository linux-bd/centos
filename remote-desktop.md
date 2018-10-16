## [Centos Remote Desktop Connection](https://www.youtube.com/watch?v=zjt1-7Msscs)

* [chcon](https://unix.stackexchange.com/questions/274360/chcon-cant-apply-partial-context-to-unlabeled-file-usr-sbin-xrdp)

```sh
yum -y update
yum -y groupinstall "GNOME Desktop" "Administration Tools"

ls -sf /lib/systemd/system/graphical.target /etc/systemd/system/default.target
init 6 [optional]

yum -y install epel-release
yum -y update
yum clean all
yum -y install xrdp tigervnc-server

chcon -h system_u:object_r:bin_t:s0 /usr/sbin/xrdp
chcon -h system_u:object_r:bin_t:s0 /usr/sbin/xrdp-sesman

systemctl start firewalld
firewall-cmd --permanent --zone=public --add-port=3389/tcp
firewall-cmd --reload
systemctl enable xrdp
systemctl start xrdp

netstat -antup | grep xrdp
```
