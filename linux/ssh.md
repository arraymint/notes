ssh仅密钥登陆

ssh-keygen -t rsa
cd ~/.ssh
cat id_rsa.pub >> authorized_keys
chmod 600 authorized_keys

/etc/sshd_config配置：
# 允许共钥
PubkeyAuthentication yes
# 禁止密码
PasswordAuthentication no

重启服务：
systemctl restart sshd.service

客户端登陆：
ssh -i key.pem root@192.168.1.1

快捷登录：
Host wang
    HostName 120.79.172.45
    Port 22
    User wang
    IdentityFile ~/.ssh/id_rsa
Host root
    HostName 120.79.172.45
    Port 22
    User root
    IdentityFile ~/.ssh/id_rsa