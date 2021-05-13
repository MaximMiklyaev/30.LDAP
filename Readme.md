#  LDAP (Centos 7)
----------------------------------------------------------------------- 

```
LDAP
1. Установить FreeIPA
2. Написать playbook для конфигурации клиента
3*. Настроить авторизацию по ssh-ключам

В git - результирующий playbook 
```

## В процессе сделано:

- Сделан Vagrantfile и ansible плейбуки, разворачивающие готовый стенд с FreeIPA с авторизацией по ssh ключам:

- В профиле пользователя на сервере FreeIPA уже присутствует открытый ключ для возможности аутентификации на машинах домена по ключу (генерируется командой ```ssh-keygen -t rsa```)
 ![Image 1](https://raw.githubusercontent.com/MaximMiklyaev/30.LDAP/master/screenshots/freeipa.png)

 - Проверяем что все работает
 ![Image 2](https://raw.githubusercontent.com/MaximMiklyaev/30.LDAP/master/screenshots/ssh.png)

 - Также сделаны настройки чтобы пользоваль мог выполнить команды от имени суперпользователя
 ![Image 3](https://raw.githubusercontent.com/MaximMiklyaev/30.LDAP/master/screenshots/sudo.png) 



## Как запустить:
 - git clone https://github.com/MaximMiklyaev/30.LDAP.git && cd 30.LDAP && vagrant up

## Проверка работоспособности:
 - После выполнения vagrant up, необходимо в /etc/hosts на хосте добавить запись 192.168.50.10 server.test.local (это необходимо чтобы зайти на сервер через веб-интерфейс) 

 - Далее, можно перейти по ссылке https://server.test.local/ipa/ui/  (user: admin; password: qwe!23asd) и проверить настройки

 - Далее необходимо выполнить команду в директории с проектом ```ssh-add id_rsa``` (т.е. добавить сгенерированный закрытый ключ). Чтобы потом его удалить после проверки можно использовать команду ```ssh-add -d id-rsa```

 - В результате на сервер client1.test.local получиться войти без ввода пароля. ```ssh andy@192.168.50.11```
