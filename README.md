# Ansible

## 1. install Ansible on Ubuntu-16 and CentOS-7
![install Ansible on Ubuntu-16 and CentOS-7](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/blob/master/install%20ansible%20CentOS.jpg)
![install Ansible on Ubuntu-16 and CentOS-7](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/blob/master/install%20ansible%20Ubuntu.jpg)

## 2. install Ansible on Amazon Linux via PIP
\$ sudo pip install ansible
![install Ansible on Amazon Linux via PIP](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/blob/master/install%20ansible%20on%20Amazon%20Linux%20via%20PIP.jpg)
\$ which ansible <br>
/usr/local/bin/ansible <br>
\$ ansible --version <br>
ansible 2.9.9 <br>

## 3. Ansible connect to Amazon Linux Clients
![Ansible connect to Amazon Linux Clients](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/blob/master/Ansible%20connect%20to%20Amazon%20Linux%20Clients.jpg)

## 4. Ansible connect to Amazon Windows Clients
![Ansible connect to Amazon Windows Clients](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/blob/master/Ansible%20connect%20to%20Amazon%20Windows%20Clients.jpg)

## 5. Create example Ansible Inventory file 
![hosts.txt](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/blob/master/hosts.txt)

## 6. Ansible. Runing Ad-Hoc commands
\$ ansible-inventory --list<br>

### 6.1 Запуск Ad-Hoc комманд
\$ ansible all -m shell -a "ls -ls /home"
            -m ping
            -m setup
### 6.2 Копирование с Мастера на все Ноды
\$ ansible prod_servers -m copy -a "src=privet.txt dest=/home mode=777" -b
### 6.3 удаление файла на всех Нодах
ansible all -m file -a "path=/home/privet.txt state=absent" -b
### 6.4 Загрузка файла с сайта
\$ ansible all -m get_url -a "url=https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/blob/master/install%20ansible%20Ubuntu.jpg dest=/home" -b
### 6.5 Удаление файла
\$ ansible all -m file -a "path=/home/install%20ansible%20Ubuntu.jpg state=absent" -b
### 6.6 Подключиться к сайту
\$ ansible all -m uri -a "url=http://www.adv-it.net"
### 6.7 Подключиться к сайту и прочитать контент
\$ ansible all -m uri -a "url=http://www.adv-it.net return_content=yes"
### 6.8 Установка httpd
\$ ansible all -m yum -a "name=httpd state=latest" -b
### 6.9 Запуск httpd и включение автозапуска при старте ОС
ansible all -m service -a "name=httpd state=started enabled=yes" -b
### 6.10 Удаление httpd
\$ ansible all -m yum -a "name=httpd state=removed" -b
### 6.11 дебаггинг
\$ ansible staging_servers -m shell -a "ls /var" -vvv
### 6.12 встроенный справочник
\$ ansible-doc -l | grep ec2

## 7. Ansible - Правила Формата YAML
![myfile.yml](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/blob/master/myfile.yml)


## 8. Ansible - Перенос переменных из Inventory файла hosts.txt в group_vars/
![hosts.txt](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/blob/master/ansible/hosts.txt)

![group_vars директория](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/tree/master/ansible/group_vars) содержащая файлы с переменными 
![ALL_SERVERS_DB](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/blob/master/ansible/group_vars/ALL_SERVERS_DB)

![PROD_SERVERS_WEB](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/blob/master/ansible/group_vars/PROD_SERVERS_WEB)

![STAGING_SERVERS_WEB](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/blob/master/ansible/group_vars/STAGING_SERVERS_WEB) 
результат проверяем коммандами:
\$ ansible-inventory --list 
и
\$ tree

## 9. Ansible - Playbooks
![Test Connection to my servers](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/blob/master/playbooks/playbook1.yml)

![Install default Apache Web Server](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/blob/master/playbooks/playbook2.yml)

![Install Apache and Upload my Web Page. Reload Apache when Web Page changed](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/blob/master/playbooks/playbook3.yml)

## 10. Ansible - Playbook Variables Debag Set_fact Register
![Playbook Variables Debag Set_fact Register](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/blob/master/playbooks/playbook_Variables_Debag_Set_fact_Register.yml)

## 12. Ansible - Блоки и Условия – Block-When
![Playbook Block-When](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/blob/master/playbooks/playbook5.yml)

## 13. Ansible - Циклы – Loop, With_Items, Until, With_fileglob
![Playbook simple loop](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/blob/master/playbooks/playbookloop.yml)
<br>
![Playbook upload many files with loop](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/blob/master/playbooks/playbook6.yml)
 ## 14. Ansible - Шаблоны - Jinja Template
![Playbook upload many files Jinja template](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/blob/master/playbooks/playbook7.yml)
 ## 15. Ansible - Создание Ролей - Roles
![roles/deploy_apache_web](https://github.com/zuFrost/Ansible-install-Ubuntu-and-CentOS/tree/master/ansible/MyWebSite2/roles/deploy_apache_web)
## 16. Ansible - Внешние переменные - extra-vars
В playbook объявляем переменную hosts: "{{ MYHOSTS }}" <br>
playbook вызываем с дополнительными переменными переменной ansible-playbook playbook6.yml --extra-var "MYHOSTS=PROD owner=Alex"<br>
возможны параметры:<br> 
--extra-var <br>
--extra-vars <br>
-e <br>
![playbook с использованием внешних переменных](https://github.com/zuFrost/Ansible/blob/master/playbooks/playbook-extra-var.yml)
## 17. Ansible - Использование Import, Include
  tasks:<br>
  \- name: Ping test<br>
    ping:<br>

  \- include: create_folders.yml<br>
  \- include: create_files.yml mytext="Privet ot KRD RUS"<br>
  
 ![Основной playbook7_includes.yml](https://github.com/zuFrost/Ansible/blob/master/playbooks/playbook7_includes.yml) <br>
 ![подключаемый create_files.yml](https://github.com/zuFrost/Ansible/blob/master/playbooks/create_files.yml) <br>
 ![подключаемый  create_folders.yml](https://github.com/zuFrost/Ansible/blob/master/playbooks/create_folders.yml) <br>
 ## 18. Ansible - Перенаправление выполнения Task из Playbook на определённый сервер - delegate_to
 команды:<br>
 delegate_to: 127.0.0.1<br>
 run_once: true<br>
 ![playbook8_delegate.yml](https://github.com/zuFrost/Ansible/blob/master/playbooks/playbook8_delegate.yml)<br>
 ## 19. Ansible - Перехват и Контроль ошибок
 команды:<br>
 any_errors_fatal: true <br>
 failed_when: "'World' in results.stdout" <br>
 failed_when: results.rc == 0 <br>
 ignore_errors: yes<br>
 ![playbook_errorhandling.yml](https://github.com/zuFrost/Ansible/blob/master/playbooks/playbook_errorhandling.yml)
 ## 20. Ansible - Хранение Секретов - ansible-vault
 комманды:
 #### Создание
 \$ ansible-vault create mysecret.txt<br>
 #### Просмотр
 \$ ansible-vault view mysecret.txt<br>
 #### Редактирование
 \$ ansible-vault edit mysecret.txt<br>
 #### Смена пароля
 \$ ansible-vault rekey mysecret.txt<br>
 #### Зашифровать ранее созданный playbook
 \$ ansible-vault encrypt playbook_vault.yml<br>
 #### Расшифровка ранее зашифрованного файла (снятие пароля)
 \$ ansible-vault decrypt playbook_vault.yml<br>
 #### Запуск зашифрованного playbook
 \$ ansible-playbook playbook_vault.yml --ask-vault-pass
 #### Запуск зашифрованного playbook без запроса пароля, с указанием файла, где хранится пароль
 \$ ansible-playbook playbook_vault.yml --vault-password-file mypass.txt
 #### Зашифровать строку
 \$ ansible-vault encrypt_string
 \$ ansible-vault encrypt_string --stdin-name "Mypassword"<br>
 \$ echo -n "!#%#$SECRETWORD$@$" | ansible-vault encrypt_string<br>
 полученную зашифрованную строку вставляем вместо пароля в playbook<br>
 ![playbook_vault.yml](https://github.com/zuFrost/Ansible/blob/master/playbooks/playbook_vault.yml)<br>
 ## 21. Ansible - Dynamic Inventory AWS - Amazon Web Services - ec2.py
 ![Inventory script example: AWS EC2](https://docs.ansible.com/ansible/latest/user_guide/intro_dynamic_inventory.html#inventory-script-example-aws-ec2) <br>
 ![файлы локально](https://github.com/zuFrost/Ansible/tree/master/AWS%20EC2%20inventory) <br> 
 export AWS_ACCESS_KEY_ID='AK123' <br>
 export AWS_SECRET_ACCESS_KEY='abc123' <br>
 \$ ec2.py --list <br>
 \$ ec2.py --list --refresh-cache <br>


 
 
 
