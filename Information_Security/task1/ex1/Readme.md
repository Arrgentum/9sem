Тут записаны команды для выполнения задания



1) Для Корневого сертификата:

Для генерации ключа:
```
openssl genrsa -aes256 -out testCA.key 4096
```

Для выпуска сертфииката:
```
openssl req -config openssl_ca.cnf -x509 -new -key testCA.key -days 1100 -out testCA.crt
```





2) Для Промежуточного сертификата:

Для генарации ключа:
```
openssl genrsa -aes256 -out testCA.key 4096
```

Для генерации запроса к Удостоверяющему центру:
```
openssl req -config openssl_intr.cnf -new -key test.key -out test.csr
```

Для выпуска сертификата:
```
openssl x509 -req -purpose -days 365 -CA testCA.crt -CAkey testCA.key -Cacreateserial -CAserial serial -in test.csr -out test.crt -extensions v3_ca -extfile openssl_intr.cnf
``` 





3) Для Базового сертификата:

Для генарации ключа:
```
openssl genrsa -out testCA.key 2048
```

Для генерации запроса к Удостоверяющему центру:
```
openssl req -config openssl_basic.cnf -new -key test.key -out test.csr
```

Для выпуска сертификата:
```
openssl x509 -req -purpose -days 90 -CA testCA.crt -CAkey testCA.key -Cacreateserial -CAserial serial -in test.csr -out test.crt -extensions v3_ca -extfile openssl_basic.cnf
``` 
