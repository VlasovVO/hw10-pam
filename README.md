# hw10-pam

## Запретить всем пользователям, кроме группы admin логин в выходные и праздничные дни

Данное условие можно выполнить изменив файл `/etc/security/time.conf`
```sh
echo -e "login  ; * ; !%root ; Wk1800-0800" >> /etc/security/time.conf
```

## Дать конкретному пользователю права рута

Создаем файл `capability.conf` и добавляем в него строчку `cap_sys_admin  ivan`

В файле `/etc/pam.d/su` вносим изменения:

```
account     sufficient  pam_succeed_if.so user = ivan use_uid quiet
account     required    pam_succeed_if.so user notin root:ivan
```
