# Тут записаны команды для выполнения задания

## Перед началом работы:

### dir - основная директория

Желательно сделать директорию внутри данной для выполнения команд отозванных сертификатов.
В примере есть директория ```data```, в которой должны лежать ключ и сертификат, которые мы свяжем с crl.
Действия:
- Перенести ...-intr.crt и ...-intr.key в данную директорию
- Создать файл index.txt

### Просмотр содержимого файла crl-файла:
```
openssl crl -noout -text -in crl_name.crl
```

### Проверка статуса сертификата crl:
```
openssl verify -crl_check -CRLfile crl_name.crl -CAfile ca-chain.crt **?** name.crt
```



## Валидный сертификат:

### Для генарации ключа:
```
openssl genrsa -out name-valid.key 2048
```

### Для выпуска сертфииката:
```
openssl req -config openssl_valid.cnf -x509 -new -key name-valid.key -days 90 -out name-valid.crt
```



## Отозванный сертификат:

### Для генарации ключа:
```
openssl genrsa -out name-revoked.key 2048
```

### Для выпуска сертфииката:
```
openssl req -config openssl_revoked.cnf -x509 -new -key name-revored.key -days 90 -out name-revoked.crt
```



## Список отозванных сертификатов:

### Выпуск crl файла при сертификате (прописано в openssl_crl.cnf):
```
openssl ca -config openssl_crl.cnf -gencrl -out crl_name.crl
```

### Отзыв сертификата:
```
 openssl ca -config openssl_crl.cnf -revoke name-revoked.crt 
```


