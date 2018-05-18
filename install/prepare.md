## Локализация

Редактируем /etc/login.conf

```
/etc/login.conf
russian|Russian Users Accounts:\
:charset=UTF-8:\
:lang=ru_RU.UTF-8:\
:tc=default:
```

Редактируем /etc/csh.cshrc

```
/etc/csh.cshrc
setenv LANG ru_RU.UTF-8
setenv LC_CTYPE ru_RU.UTF-8
setenv LC_COLLATE POSIX
setenv LC_ALL ru_RU.UTF-8
```

Если используется bash

```
/etc/profile
LANG="ru_RU.UTF-8"; export LANG
LC_CTYPE="ru_RU.UTF-8"; export LC_CTYPE
LC_COLLATE="POSIX"; export LC_COLLATE
LC_ALL="ru_RU.UTF-8"; export LC_ALL
```

Если не нужно локализовать root

```
/root/.cshrc
setenv LANG C
setenv LC_CTYPE C
setenv LC_COLLATE POSIX
setenv LC_ALL C
```
## Установка даты и времени

```
cd /usr/ports/misc/zoneinfo
make config-recursive
make install clean

cp /usr/share/zoneinfo/Europe/Moscow /etc/localtime

ntpdate ru.pool.ntp.org
```
