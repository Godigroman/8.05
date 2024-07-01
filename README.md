# Домашнее задание к занятию "`Кластеризация и балансировка нагрузки`" - `Клименко Олег`


---

### Задание 1

`Приведите ответ в свободной форме........`

1. `Запустите два simple python сервера на своей виртуальной машине на разных портах`
2. `Установите и настройте HAProxy, воспользуйтесь материалами к лекции по` [ссылке](https://github.com/netology-code/sflt-homeworks/tree/main/2) 
3. `Настройте балансировку Round-robin на 4 уровне.`
4. `На проверку направьте конфигурационный файл haproxy, скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy.`

---

```
frontend example  # секция фронтенд
        mode tcp
        bind :8088
        default_backend web_servers

backend web_servers    # секция бэкенд
        mode tcp
        balance roundrobin
        option httpchk
        http-check send meth GET uri /index.html
        server s1 127.0.0.1:8888 check
        server s2 127.0.0.1:9999 check
```
---
![](https://cdn.discordapp.com/attachments/1228819431787069484/1257308431317074031/image.png?ex=6683ef39&is=66829db9&hm=b67adaa81bc940933028be3a098b26d008d4461ec83007aef92c24f215477e4d&))`


---

### Задание 2

`Приведите ответ в свободной форме........`

1. `Запустите три simple python сервера на своей виртуальной машине на разных портах`
2. `Настройте балансировку Weighted Round Robin на 7 уровне, чтобы первый сервер имел вес 2, второй - 3, а третий - 4`
3. `HAproxy должен балансировать только тот http-трафик, который адресован домену example.local`
4. `На проверку направьте конфигурационный файл haproxy, скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy c использованием домена example.local и без него.
`
---

```
frontend example  # секция фронтенд
        mode http
        bind :8088
	acl ACL_example.com hdr(host) -i example.local
	use_backend web_servers if ACL_example.com

backend web_servers    # секция бэкенд
        mode http
        balance roundrobin
        option httpchk
        http-check send meth GET uri /index.html
        server s1 127.0.0.1:6666 weight 2 check
        server s2 127.0.0.1:8888 weight 3 check
        server s3 127.0.0.1:9999 weight 4 check
```

---
![](https://cdn.discordapp.com/attachments/1228819431787069484/1257308498551898165/image.png?ex=6683ef49&is=66829dc9&hm=cff413dfc3c839664492f8f576f53790fa608000c66bf8550c915b195d44f249&)


---
---
