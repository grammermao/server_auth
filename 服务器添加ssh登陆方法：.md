## 服务器添加ssh登陆方法：

- **本地生成公钥私钥**

  ```
  ssh-keygen -t rsa -C  'grammermao@gmail.com'
  ```

- **上传公钥到服务器端**

  ```
  scp ~/.ssh/id_rsa.pub <用户名>@<ip地址>:/root/id_rsa.pub 
  scp -P <端口号> ~/.ssh/id_rsa.pub <用户名>@<ip地址>:/home/id_rsa.pub
  ```

- 把公钥追加到服务器ssh认证文件中：

  > 如果没有`authorized_keys`，请执行命令 `ssh localhost`

  ```
  cat /home/id_rsa.pub >> ~/authorized_keys
  ```

- 需要配置sshd_config文件

  ```
  RSAAuthentication yes # 开启密钥登入的认证方式
  PubkeyAuthentication yes # 开启密钥登入的认证方式
  PermitRootLogin yes #此处请留意 root 用户能否通过 SSH 登录，默认为yes：
  PasswordAuthentication yes #当我们完成全部设置并以密钥方式登录成功后，可以禁用密码登录。这里我们先不禁用，先允许密码登陆
  ```

- 配置快捷登陆

  ```
  Host            alias            #自定义别名
  HostName        hostname         #替换为你的ssh服务器ip或domain
  Port            port             #ssh服务器端口，默认为22
  User            user             #ssh服务器用户名
  IdentityFile    ~/.ssh/id_rsa    #第一个步骤生成的公钥文件对应的私钥文件
  ```

**如果/root下面没有.ssh/authorized_keys文件，则再root下面执行命令`ssh -p33888 localhost`**

## Q&A

- firewall-cmd --zone=public --list-ports
- firewall-cmd --zone=public --add-port=xxx/tct
- systemctl restart firewalld