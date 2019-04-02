## How to use ?

* 修改 `http/ks.cfg`

請依照自已的需求修改該檔案，建議使用 **Static IP**，預設密碼為 **1qaz!QAZ**

  * DHCP:

    ```
    # Network information
    network  --bootproto=dhcp --device=enp0s3 --noipv6 --activate
    network  --hostname=baseimage
    ```

  * Static IP:

    ```
    # Network information
    network  --bootproto=static --device=enp0s3 --gateway="Default Gateway" --ip="Static IP" --nameserver=8.8.8.8 --netmask=255.255.255.0 --noipv6 --activate
    network  --hostname=baseimage
    ```

  * 新增使用者

    這裡不一定要做，看自已的需求
  
    ```
    %post
    # Install SUDO
    /usr/bin/yum -y install sudo
    
    # Create vagrant user
    /usr/sbin/useradd -m packer
    /usr/bin/echo packer | /usr/bin/passwd --stdin packer
    
    # Add vagrant user to SUDO
    echo "packer        ALL=(ALL)       NOPASSWD: ALL" >> /etc/sudoers.d/packer
    echo "Defaults:packer !requiretty"                 >> /etc/sudoers.d/packer
    chmod 0440 /etc/sudoers.d/packer
    
    %end
    ```

* 修改 `centos7_1810_root.json`

這裡能改的很多，可以自行摸索，建議可以先修改 **ssh_host** 填入自已的 IP 即可使用

```
"variables": {
  "vm_name": "Base",
  "guest_os_type": "RedHat_64",
  "iso_url": "/Users/daniel/Downloads/CentOS-7-x86_64-Minimal-1810.iso",
  "iso_checksum": "38d5d51d9d100fd73df031ffd6bd8b1297ce24660dc8c13a3b8b4534a4bd291c",
  "iso_checksum_type": "sha256",
  "ssh_host": "Your IP Address"
}
```

* 修改 `Vagrantfile`

這裡能改的很多，可以自行摸索，建議可以先修改 **config.ssh.host** 填入自已的 IP 即可使用

```
  # Setting SSH Config.
    config.ssh.host = "Your IP Address"
```

* 修改 ansible 資料夾中的 `inventory`

```
[all]
virtualbox ansible_host="Your IP Address" ansible_port=22 ansible_user=root ansible_ssh_pass=1qaz!QAZ
``` 

* 可以開始執行作業

  * 驗証設定檔是否正確

    ```
    # packer validate centos7_1810_root.json
    ```

  * Packer 建立 Box Image

    ```
    PACKER_LOG=1 packer build centos7-1810-root.json
    ```

  * 驗証 Vagrantfile 設定檔是否正確

    ```
    # vagrant validate Vagrantfile
    ```

  * 驗証 ansible 語法是否正確 

    ```
    # ansible-playbook --syntax-check ./ansible/demo.yml
    ```

  * 新增 Vagrnat Box Image

    ```
    # vagrant box add -name CentOS7 ./output/Base-CentOS-7-1810-x86_64-minimal.box
    ```

  * 執行啟動 VM

    ```
    # vagrant up
    ```

  * 關機 VM

    ```
    # vagrant halt
    ```

  * 刪除 VM
  
    ```
    # vagrant destroy -f virtualbox
    ```
