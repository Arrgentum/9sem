## Для первой чассти задания

### Запустить на одном терминле данную команду

```kotlin
tshark -w /tmp/Alex_acl.pcapng --color -V -P -i lo -i wlp2s0  -f 'host ident.me or localhost  or httpbin.org'
```

### Запустить на втором термиле следующие команды

```kotlin
curl --proxy localhost:3128 --head -L ident.me -A "votintsevak"
```

```kotlin
curl --proxy localhost:3128 --head -L 'httpbin.org/get?bio=votintsevak'
```

### Заверщить выполнений первой команды ctr-C,

### Запустить wireshark с фильтрами снизу

## Второе задание

### На первом терминале запускаешь команду

```kotlin
tshark -w /tmp/Alex_ua.pcapng --color -V -P -i lo -i wlp2s0  -f 'host ident.me or localhost  or httpbin.org'
```

### На втором терминале команду

```kotlin
curl --proxy localhost:3128 --head -L httpbin.org/ip
```

## Wireshark filters
filters == (tcp || http)
