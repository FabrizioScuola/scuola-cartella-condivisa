Linux centos 7

Server 
i5 intel
RAM 4Gb
SSD 128GB OS Linux
HDD 1TB x 2 (RAID 1)



yum install samba samba-client samba-common

systemctl enable smb.service
systemctl enable nmb.service
systemctl restart smb.service
systemctl restart nmb.service

mv /etc/samba/smb.conf /etc/samba/smb.conf.bak

[global]
workgroup = WORKGROUP
server string = Samba Server %v
netbios name = centos
security = user
map to guest = bad user
dns proxy = no

# Share Read/Write
#mkdir -p /samba/share_read_write
#chown -R nobody:nobody /samba/share_read_write/
#chcon -t samba_share_t /samba/share_read_write/

[share_read_write]
path = /samba/share_read_write
browsable = yes
guest ok = yes
writable = yes

# Share Read
#mkdir -p /samba/share_read
#chown -R nobody:nobody /samba/share_read/
#chcon -t samba_share_t /samba/share_read/

[share_read]
path = /samba/share_read
browsable =yes
guest ok = yes
read only = yes

