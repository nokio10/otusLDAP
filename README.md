# otusLDAP

## Задание 

1. Установить FreeIPA;
2. Написать Ansible playbook для конфигурации клиента;
3*. Настроить аутентификацию по SSH-ключам;
4**. Firewall должен быть включен на сервере и на клиенте.
Формат сдачи ДЗ - vagrant + ansible

## Решение

Стенд с FreeIPA сервером и клиентом разворачивается командой ```vagrant up```

```
root@ubuntu:~/otusLDAP# vagrant up
Bringing machine 'ldapserver' up with 'virtualbox' provider...
Bringing machine 'ldapclient' up with 'virtualbox' provider...
==> ldapserver: Importing base box 'centos7'...
==> ldapserver: Matching MAC address for NAT networking...
==> ldapserver: Setting the name of the VM: otusLDAP_ldapserver_1659017708198_58996
==> ldapserver: Clearing any previously set network interfaces...
==> ldapserver: Preparing network interfaces based on configuration...
    ldapserver: Adapter 1: nat
    ldapserver: Adapter 2: intnet
==> ldapserver: You are trying to forward to privileged ports (ports <= 1024). Most
==> ldapserver: operating systems restrict this to only privileged process (typically
==> ldapserver: processes running as an administrative user). This is a warning in case
==> ldapserver: the port forwarding doesn't work. If any problems occur, please try a
==> ldapserver: port higher than 1024.
==> ldapserver: Forwarding ports...
    ldapserver: 443 (guest) => 443 (host) (adapter 1)
    ldapserver: 22 (guest) => 2222 (host) (adapter 1)
==> ldapserver: Running 'pre-boot' VM customizations...
==> ldapserver: Booting VM...
==> ldapserver: Waiting for machine to boot. This may take a few minutes...
    ldapserver: SSH address: 127.0.0.1:2222
    ldapserver: SSH username: vagrant
    ldapserver: SSH auth method: private key
    ldapserver:
    ldapserver: Vagrant insecure key detected. Vagrant will automatically replace
    ldapserver: this with a newly generated keypair for better security.
    ldapserver:
    ldapserver: Inserting generated public key within guest...
    ldapserver: Removing insecure key from the guest if it's present...
    ldapserver: Key inserted! Disconnecting and reconnecting using new SSH key...
==> ldapserver: Machine booted and ready!
==> ldapserver: Checking for guest additions in VM...
    ldapserver: No guest additions were detected on the base box for this VM! Guest
    ldapserver: additions are required for forwarded ports, shared folders, host only
    ldapserver: networking, and more. If SSH fails on this machine, please install
    ldapserver: the guest additions and repackage the box to continue.
    ldapserver:
    ldapserver: This is not an error message; everything may continue to work properly,
    ldapserver: in which case you may ignore this message.
==> ldapserver: Setting hostname...
==> ldapserver: Configuring and enabling network interfaces...
==> ldapserver: Rsyncing folder: /root/otusLDAP/ => /vagrant
==> ldapserver: Running provisioner: ansible...
    ldapserver: Running ansible-playbook...

PLAY [ldapserver] **************************************************************

TASK [Gathering Facts] *********************************************************
ok: [ldapserver]

TASK [stop chronyd] ************************************************************
changed: [ldapserver]

TASK [start firewalld] *********************************************************
changed: [ldapserver]

TASK [add firewalld rules] *****************************************************
changed: [ldapserver]

TASK [firewalld reload] ********************************************************
changed: [ldapserver]

TASK [Set a hostname] **********************************************************
changed: [ldapserver]

TASK [install packages] ********************************************************
changed: [ldapserver]

TASK [update packages] *********************************************************
changed: [ldapserver]

TASK [Edit /etc/hosts] *********************************************************
changed: [ldapserver]

TASK [Install pip] *************************************************************
changed: [ldapserver]

TASK [Install pexpect] *********************************************************
changed: [ldapserver]

TASK [Init ipa-server] *********************************************************
changed: [ldapserver]

TASK [admin login] *************************************************************
changed: [ldapserver]

TASK [Add user ldapclient] *****************************************************
changed: [ldapserver]
[WARNING]: Could not match supplied host pattern, ignoring: ldapclient

PLAY [ldapclient] **************************************************************
skipping: no hosts matched

PLAY RECAP *********************************************************************
ldapserver                 : ok=14   changed=13   unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

==> ldapclient: Importing base box 'centos7'...
==> ldapclient: Matching MAC address for NAT networking...
==> ldapclient: Setting the name of the VM: otusLDAP_ldapclient_1659018487401_87449
==> ldapclient: Fixed port collision for 22 => 2222. Now on port 2200.
==> ldapclient: Clearing any previously set network interfaces...
==> ldapclient: Preparing network interfaces based on configuration...
    ldapclient: Adapter 1: nat
    ldapclient: Adapter 2: intnet
==> ldapclient: Forwarding ports...
    ldapclient: 22 (guest) => 2200 (host) (adapter 1)
==> ldapclient: Running 'pre-boot' VM customizations...
==> ldapclient: Booting VM...
==> ldapclient: Waiting for machine to boot. This may take a few minutes...
    ldapclient: SSH address: 127.0.0.1:2200
    ldapclient: SSH username: vagrant
    ldapclient: SSH auth method: private key
    ldapclient:
    ldapclient: Vagrant insecure key detected. Vagrant will automatically replace
    ldapclient: this with a newly generated keypair for better security.
    ldapclient:
    ldapclient: Inserting generated public key within guest...
    ldapclient: Removing insecure key from the guest if it's present...
    ldapclient: Key inserted! Disconnecting and reconnecting using new SSH key...
==> ldapclient: Machine booted and ready!
==> ldapclient: Checking for guest additions in VM...
    ldapclient: No guest additions were detected on the base box for this VM! Guest
    ldapclient: additions are required for forwarded ports, shared folders, host only
    ldapclient: networking, and more. If SSH fails on this machine, please install
    ldapclient: the guest additions and repackage the box to continue.
    ldapclient:
    ldapclient: This is not an error message; everything may continue to work properly,
    ldapclient: in which case you may ignore this message.
==> ldapclient: Setting hostname...
==> ldapclient: Configuring and enabling network interfaces...
==> ldapclient: Rsyncing folder: /root/otusLDAP/ => /vagrant
==> ldapclient: Running provisioner: ansible...
    ldapclient: Running ansible-playbook...

PLAY [ldapserver] **************************************************************
skipping: no hosts matched

PLAY [ldapclient] **************************************************************

TASK [Gathering Facts] *********************************************************
ok: [ldapclient]

TASK [Set a hostname] **********************************************************
changed: [ldapclient]

TASK [install packages] ********************************************************
changed: [ldapclient]

TASK [Install pip] *************************************************************
changed: [ldapclient]

TASK [Install pexpect] *********************************************************
changed: [ldapclient]

TASK [Edit /etc/hosts] *********************************************************
changed: [ldapclient]

TASK [stop chronyd] ************************************************************
changed: [ldapclient]

TASK [start firewalld] *********************************************************
changed: [ldapclient]

TASK [Init ipa-client] *********************************************************
changed: [ldapclient]

TASK [ssh-keygen] **************************************************************
changed: [ldapclient]

TASK [kinit ldapclient] ********************************************************
changed: [ldapclient]

TASK [create /home/ldapclient/.ssh/] *******************************************
changed: [ldapclient]

TASK [copy ssh key] ************************************************************
changed: [ldapclient]

TASK [add ssh key to ldap] *****************************************************
changed: [ldapclient]

PLAY RECAP *********************************************************************
ldapclient                 : ok=14   changed=13   unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

Проверяю работу после установки. 

```
root@ubuntu:~/otusLDAP# vagrant ssh ldapclient
Last login: Thu Jul 28 14:49:35 2022 from 10.0.2.2
[vagrant@ldapclient ~]$ hostname
ldapclient.otusldap.test
[vagrant@ldapclient ~]$ sudo -i
[root@ldapclient ~]# ssh ldapclient@ldapclient.otusldap.test
Last failed login: Thu Jul 28 14:50:08 UTC 2022 from 192.168.50.11 on ssh:notty
There was 1 failed login attempt since the last successful login.
-sh-4.2$
[root@ldapclient ~]# kinit admin
Password for admin@OTUSLDAP.TEST:
[root@ldapclient ~]# ipa user-find ldapclient
--------------
1 user matched
--------------
  User login: ldapclient
  First name: ldap
  Last name: client
  Home directory: /home/ldapclient
  Login shell: /bin/sh
  Principal name: ldapclient@OTUSLDAP.TEST
  Principal alias: ldapclient@OTUSLDAP.TEST
  Email address: ldapclient@otusldap.test
  UID: 762200001
  GID: 762200001
  SSH public key fingerprint: SHA256:hMZYT6kzoAZkvZsGKrVaCJIjj87bX9HYIsUdWaxCim4 ldapclient@otusldap.test (ssh-rsa)
  Account disabled: False
----------------------------
Number of entries returned 1
----------------------------
[root@ldapclient ~]# kinit ldapclient
Password for ldapclient@OTUSLDAP.TEST:
[root@ldapclient ~]# kinit ldapclient
Password for ldapclient@OTUSLDAP.TEST:
kinit: Password incorrect while getting initial credentials
```
