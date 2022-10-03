# Тут записаны команды для выполнения задания
 
## Проверка сертификата:

### Вывод содержимого сертификата:

```
openssl x509 -text -noout -in name.crt
```

### Проверка содержимого сертификата:

```
openssl verify -verbose -CAfile testCA.crt testCA.crt
```





## Для Корневого сертификата:

### Для генерации ключа:
```
openssl genrsa -aes256 -out name-ca.key 4096
```

### Для выпуска сертфииката:
```
openssl req -config openssl_ca.cnf -x509 -new -key name-ca.key -days 1100 -out name-ca.crt
```





## Для Промежуточного сертификата:

### Для генарации ключа:
```
openssl genrsa -aes256 -out name-intr.key 4096
```

### Для генерации запроса к Удостоверяющему центру:
```
openssl req -config openssl_intr.cnf -new -key name-intr.key -out name-intr.csr
```

### Для выпуска сертификата:
```
openssl x509 -req -purpose -days 365 -CA name-ca.crt -CAkey name-ca.key -Cacreateserial -CAserial serial -in name-intr.csr -out name-intr.crt -extensions v3_ca -extfile openssl_intr.cnf
``` 





## Для Базового сертификата:

### Для генарации ключа:
```
openssl genrsa -out name-basic.key 2048
```

### Для генерации запроса к Удостоверяющему центру:
```
openssl req -config openssl_basic.cnf -new -key name-basic.key -out name-basic.csr
```

### Для выпуска сертификата:
```
openssl x509 -req -purpose -days 90 -CA name-intr.crt -CAkey name-intr.key -Cacreateserial -CAserial serial -in name-basic.csr -out name-basic.crt -extensions v3_ca -extfile openssl_basic.cnf
``` 
