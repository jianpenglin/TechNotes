# FTP 配置

Redhait6.5 Linux Ftp 配置步骤.

[TOC]

## 理论基础

- 命令端口
- 数据端口
- 主动模式（PORT）
- 被动模式（PASV）
- 命令
    - USER
    - PASS
    - SIZE
    - CWD
    - PASV
    - PORT
    - PETR
    - STOR
    - REST
    - QUIT

## FTP服务安装启动

- 可以使用yum命令直接安装ftp
`yum install vsftpd `
- 开启关闭命令
`service vsftpd start`
`service vsftpd stop`


## FTP虚拟用户配置

### 添加账号
增加用户
 root用户执行
```
# useradd -d /home/test  -s /sbin/nologin test //增加用户test，并制定test用户的主目录为/home/test
# passwd test //为test设置密码
# chown -R virtusers.virtusers /data1/ftp
```

### 修改VSFTPD配置

`vi /etc/vsftpd/vsftpd.conf`
```
anonymous_enable=NO   //不允许匿名账号访问
local_enable=YES    //本地用户可以访问(采用虚拟账号访问时，这个参数也要开启（虚拟账号要寄宿本地账号），虽然开启但是本地账号是不可以登陆的)
write_enable=YES     //可写可上传。这个参数是全局配置，否则上传和下载都会报错550！
local_umask=022
listen_port=218 //监听的ftp端口
ftp_data_port=208
pasv_min_port=1888  //分配给ftp账号的最小端口。被动模式下的配置
pasv_max_port=1889  //分配给ftp账号的最大端口。每个账号分配一个端口，即最大允许2个ftp账号连接。
anon_upload_enable=NO
anon_mkdir_write_enable=NO
dirmessage_enable=YES
xferlog_enable=YES
connect_from_port_20=YES    //通过20端口传输数据
chown_uploads=NO
chroot_local_user=YES
xferlog_file=/var/log/vsftpd.log
xferlog_std_format=YES
nopriv_user=virtusers
async_abor_enable=YES
ascii_upload_enable=YES
ascii_download_enable=YES
ftpd_banner=Welcome to blah FTP service ^_^   //登陆FTP时显示的欢迎信息
chroot_list_enable=NO   //限制所有的本地用户在自家目录,即用户登陆系统后锁定在自家目录。虚拟主机配置下，在下面两个chroot配置后，这个参数必须为NO，否则登陆FTP后还可以访问其他目录！
ls_recurse_enable=NO
listen=YES
pam_service_name=vsftpd //指定PAM配置文件，即下面的/etc/pam.d/vsftpd文件要和这里指定的一致。
userlist_enable=YES
tcp_wrappers=YES
guest_enable=YES      //启用虚拟用户 若这个值设定为 YES 时，那么任何非 anonymous 登入的账号，均会被假设成为 guest (访客) 至于访客在 vsftpd 当中，预设会取得 ftp 这个使用者的相关权限。但可以透过 guest_username 来修改
guest_username=virtusers    //将虚拟用户映射为本地[virtusers]用户（前提是local_enable=YES）
virtual_use_local_privs=YES  //这个参数一定要加上，虚拟用户和本地用户有相同的权限；否则ftp连上后不能上传，报错550权限拒绝！
user_config_dir=/etc/vsftpd/vconf   //指定不同虚拟用户配置文件的存放路径
#pasv_address=127.0.0.1
reverse_lookup_enable=NO
```

### 修改防火墙

`cat /etc/sysconfig/iptables`
```
A INPUT -s 10.68.250.13 -m state --state NEW -m tcp -p tcp --dport 2021 -j ACCEPT
-A INPUT -s 10.68.250.13 -m state --state NEW -m tcp -p tcp --dport 40001:40100 -j ACCEPT
```

### 设置虚拟FTP账号


1. 虚拟账号它不是真实存在于系统中的，即/etc/passwd文件里没有的，它是借助于宿主账号virtusers。 奇数行是账号，偶数行是密码
```
[root@hems vsftpd]# cat virtusers
ltehems
ltehems1
ftpuser
123456
docuser
123456
docadmin
docadmin1
```

2. 生成虚拟用户口令的db文件(设置600权限)
```
[root@hems vsftpd]# db_load -T -t hash -f /etc/vsftpd/virtusers /etc/vsftpd/virtusers.db
[root@hems vsftpd]# chmod 600 /etc/vsftpd/virtusers.db
```

3. 锁定目录（非必要）
```
[root@hems vsftpd]# cat /etc/vsftpd/chroot_list     //将虚拟用户放在这个列表文件里，说明这些用户登陆后都只能锁定到对应主目录内
docuser
```

4. 配置虚拟配置文件

```
[root@hems vsftpd]# mkdir vconf      //此目录名是在vsftpd.conf配置中指定的，里面是虚拟用户配置文件（文件名是虚拟用户名）
[root@hems vconf]# pwd
/etc/vsftpd/vconf
[root@hems vconf]# cat ltehems 
local_root=/data1/ftp  //指定虚拟账号登陆后的主目录，目录权限要是宿主账号nobody，这样就可以实现账号映射
anonymous_enable=NO
write_enable=YES     //写权限
local_umask=022
anon_upload_enable=NO   //上传权限
anon_mkdir_write_enable=NO  //创建目录权限
anon_other_write_enable=NO    //删除和重命名权限
idle_session_timeout=300
data_connection_timeout=90
max_clients=1
max_per_ip=1
local_max_rate=0
pam_service_name=vsftpd
chroot_local_user=YES
virtual_use_local_privs=NO // 如果是NO使用anon权限，否则使用主账号权限
```

5. 系统其他配置
```
[root@hems vsftpd]#  ll /lib64/security/pam_userdb.so
[root@hems vsftpd]# cat /etc/pam.d/vsftpd //注释原先内容修改如下
#%PAM-1.0
auth    required /lib64/security/pam_userdb.so db=/etc/vsftpd/virtusers
account required /lib64/security/pam_userdb.so db=/etc/vsftpd/virtusers
```
```
[root@hems vsftpd]# cat /etc/passwd|grep virtusers
virtusers:x:501:501::/data1/ftp:/sbin/nologin
```
```
[root@hems vsftpd]# chown -R virtusers.virtusers /data1/document     //设置虚拟账号hqsbcms指定的主目录的权限为virtusers，这样就可以映射到宿主账号virtusers
[root@hems data1]# ll
鎬荤敤閲24
drwxr-xr-x   3 root      root      4096 11鏈27 17:07 backup
drwxr-xr-x   2 root      root      4096 3鏈  9 2018 blank
drwxr-xr-x   3 virtusers virtusers 4096 1鏈  3 10:53 document
drwxr-xr-x. 15 virtusers virtusers 4096 4鏈 13 2018 ftp
drwxr-xr-x   7 virtusers virtusers 4096 12鏈 3 11:12 north
drwxr-xr-x   9 root      root      4096 4鏈 13 2018 transit
[root@hems vsftpd]# chmod -R 700 /data1/document
           
[root@hems vsftpd]# /etc/init.d/vsftpd start
   
[root@bastion-IDC vsftpd]# ll /data1/ftp/
```



### 建立一个新的FTP账号

root用户执行
```
# useradd -d /data1/document docadmin //增加用户docadmin，并制定test用户的主目录为/data1/document
# passwd docadmin //为docadmin设置密码
```
```
setfacl -R -m u:admin:rwx /data1/document　　　　　　　 --赋权admin账号对于document目录的权限   rwx   只读  只写   执行权限
vi /etc/vsftpd/user_list  //添加新增的用户名
```
主配置文件
```
anonymous_enable=NO
local_enable=YES
write_enable=YES
local_umask=022
listen_port=218
ftp_data_port=208
pasv_min_port=1888
pasv_max_port=1889
anon_upload_enable=NO
anon_mkdir_write_enable=NO
dirmessage_enable=YES
xferlog_enable=YES
connect_from_port_20=YES
chown_uploads=NO
chroot_local_user=YES
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd/chroot_list
xferlog_file=/var/log/vsftpd.log
xferlog_std_format=YES
nopriv_user=virtusers
async_abor_enable=YES
ascii_upload_enable=YES
ascii_download_enable=YES
ftpd_banner=Welcome to blah FTP service ^_^
chroot_list_enable=NO
ls_recurse_enable=NO
listen=YES
pam_service_name=vsftpd
userlist_enable=YES
userlist_deny=NO
userlist_file=/etc/vsftpd/user_list
tcp_wrappers=YES
guest_enable=YES
guest_username=virtusers
virtual_use_local_privs=YES
user_config_dir=/etc/vsftpd/vconf
#pasv_address=127.0.0.1
reverse_lookup_enable=NO
```
重启vsftpd服务后发现还是无法使用，通过如下修改可以使用
```
[root@hems vsftpd]# vi /etc/pam.d/vsftpd
#%PAM-1.0
#auth    required /lib64/security/pam_userdb.so db=/etc/vsftpd/virtusers
#account required /lib64/security/pam_userdb.so db=/etc/vsftpd/virtusers
session optional pam_keyinit.so force revoke
auth required pam_listfile.so item=user sense=deny file=/etc/vsftpd/ftpusers onerr=succeed
auth required pam_shells.so
auth include password-auth
account include password-auth
session required pam_loginuid.so
session include password-auth
```
得出结论vsftpd虚拟用户和本地用户不能共存。有可以共存的策略把`required`改成`sufficient`
```
auth sufficient pam_userdb.so db=/etc/vsftpd/vuser_passwd
account sufficient pam_userdb.so db=/etc/vsftpd/vuser_passwd
session optional pam_keyinit.so force revoke
auth required pam_listfile.so item=user sense=deny file=/etc/vsftpd/ftpusers onerr=succeed
auth required pam_shells.so
auth include password-auth
account include password-auth
session required pam_loginuid.so
session include password-auth
```


## FTP用户配置

Content.

## See also

- 
