### vsftpd
yum install -y vsftpd

systemctl enable vsftpb
systemctl start vsftpb

netstat -ltn -> we will see port 21 now listening

ls /etc/vsftpd
vim /etc/vsftpd/vsftpd.conf
