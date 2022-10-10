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
openssl verify -crl_check -CRLfile crl_name.crl -CAfile ca-chain.crt name.crt
```



## Валидный сертификат:

### Для генарации ключа:
```
openssl genrsa -out name-valid.key 2048
```

### Для генерации запроса к Удостоверяющему центру:
```
openssl req -config openssl_valid.cnf -new -key name-valid.key -out name-valid.csr
```

### Для выпуска сертификата (intr взфт с прошлого задания):
```
openssl x509 -req -purpose -days 90 -CA name-intr.crt -CAkey name-intr.key -CAcreateserial -CAserial serial -in name-valid.csr -out name-valid.crt -extensions v3_ca -extfile openssl_valid.cnf
``` 


## Отозванный сертификат:

### Для генарации ключа:
```
openssl genrsa -out name-revoked.key 2048
```

### Для генерации запроса к Удостоверяющему центру:
```
openssl req -config openssl_revoked.cnf -new -key name-revoked.key -out name-revoked.csr
```

### Для выпуска сертификата (intr взфт с прошлого задания):
```
openssl x509 -req -purpose -days 90 -CA name-intr.crt -CAkey name-intr.key -CAcreateserial -CAserial serial -in name-revoked.csr -out name-revoked.crt -extensions v3_ca -extfile openssl_revoked.cnf
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

### Повторный выпуск crl файла (обновленного)
```
openssl ca -config openssl_crl.cnf -gencrl -x509 -out crl_name.crl
```

### Генерация chain файла (ca и intr взяты с прошлого задания)
```
cat name-ca.crt name-intr-crt > name-chain.crt
```

