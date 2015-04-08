#CentOS-7中firewall-cmd命令
在 CentOS 7
暫時開放 ftp 服務
`# firewall-cmd --add-service=ftp`

永久開放 ftp 服務
`# firewall-cmd --add-service=ftp --permanent`
永久關閉
`# firewall-cmd --remove-service=ftp --permanent`
success

讓設定生效
# systemctl restart firewalld

檢視設定是否生效
# iptables -L -n | grep 21
ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0            tcp dpt:21 ctstate NEW
檢查防火牆狀態
# firewall-cmd --state
running

# systemctl stop firewalld
# firewall-cmd --state
not running


# firewall-cmd --list-all
public (default)
  interfaces:
  sources:
  services: dhcpv6-client ftp ssh
  ports:
  masquerade: no
  forward-ports:
  icmp-blocks:
  rich rules:

在 FirewallD 的服務名稱
# firewall-cmd --get-service
amanda-client bacula bacula-client dhcp dhcpv6 dhcpv6-client dns ftp high-availability http https imaps ipp ipp-client ipsec kerberos kpasswd ldap ldaps libvirt libvirt-tls mdns mountd ms-wbt mysql nfs ntp openvpn pmcd pmproxy pmwebapi pmwebapis pop3s postgresql proxy-dhcp radius rpc-bind samba samba-client smtp ssh telnet tftp tftp-client transmission-client vnc-server wbem-https

查詢服務的啟用狀態
# firewall-cmd --query-service ftp
yes
# firewall-cmd --query-service ssh
yes
# firewall-cmd --query-service samba
no
# firewall-cmd --query-service http
no

自行加入要開放的 Port
```js
    # firewall-cmd --add-port=3128/tcp
    # firewall-cmd --list-all
    public (default)
      interfaces:
      sources:
      services: dhcpv6-client ftp ssh
      ports: 3128/tcp
      masquerade: no
      forward-ports:
      icmp-blocks:
      rich rules:
```
