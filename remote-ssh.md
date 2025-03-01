```bash
ssh-keygen -t rsa -b 4096 -C "example@gmail.com"
```

```bash
Generating public/private rsa key pair.
Enter file in which to save the key (/home/example/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/example/.ssh/dell_key
Your public key has been saved in /home/example/.ssh/dell_key.pub
The key fingerprint is:
SHA256:xxxxxxxxxxxxxxxxx example@gmail.com
The key's randomart image is:
+---[RSA 4096]----+
| .+O++..         |
|o+o+=.+.         |
|+EB=+.+   .   o  |
| =.++B = . o o o |
|o  .O O S . o o .|
|   . * o .   . . |
|    . . .        |
|     .           |
|                 |
+----[SHA256]-----+
```

```bash
ssh-copy-id -i ~/.ssh/dell_key.pub example@7.7.7.7
```

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

На хосте: 

0. Перенести файл без расширения .pub и chmod 600 путь до файла ключа
1. Ctrl+Shift+X - Скачать расширение Remote - SSH
2. Ctrl+Shift+P - Remote-SSH: Add New SSH Host
3. ssh -i путь до файла ключа example@7.7.7.7
4. Ввести путь до файла ключа
5. nano ~/.ssh/config
Host web-cloud
    HostName 7.7.7.7
    User example
    IdentityFile ~/.ssh/rsa_ssh
    IdentitiesOnly yes6. Ctrl+Shift+P - Remote-SSH: Connect to Host - web-cloud
7. passfrase
