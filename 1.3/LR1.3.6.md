# Отчёт по лабораторной работе LR1.3.6
## Тема: Управление процессами и службами в Linux

### Титульный блок
- Учебное заведение: НИТУ МИСИС
- Дисциплина/курс: Прикладная информатика, 4 курс
- Лабораторная работа: **LR1.3.6 — Создание собственного systemd-юнита (итоговый проект)**
- Студент: Хомяк Мария Александровна  Группа: _______
- Преподаватель: _______________________________
- Дата: 2026-03-29

---

## Паспорт стенда
> Принцип: «ни одного действия без доказательства». Вставь **вывод команд** в блоки ниже и сохрани лог-файл.

**Команды паспорта (копипаст):**
```bash
uname -a
cat /etc/os-release
whoami
ip a
df -h
free -h
lsblk
date
systemctl --version  # если есть systemd
```

**Вывод команд (вставь сюда):**
```text
Команда: uname -a
Linux student 6.8.0-106-generic #106-Ubuntu SMP PREEMPT_DYNAMIC Fri Mar  6 07:58:08 UTC 2026 x86_64 x86_64 x86_64 GNU/Linux

Команда: cat /etc/os-release
PRETTY_NAME="Ubuntu 24.04.4 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04.4 LTS (Noble Numbat)"
VERSION_CODENAME=noble
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=noble
LOGO=ubuntu-logo

Команда: whoami
student

Команда: ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:96:21:23 brd ff:ff:ff:ff:ff:ff
    inet 10.90.142.10/24 metric 100 brd 10.90.142.255 scope global dynamic enp0s3
       valid_lft 2590sec preferred_lft 2590sec
    inet6 fe80::a00:27ff:fe96:2123/64 scope link 
       valid_lft forever preferred_lft forever

Команда: df -h
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              197M  1.1M  196M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv  9.8G  5.2G  4.2G  56% /
tmpfs                              985M     0  985M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
/dev/sda2                          1.8G  200M  1.5G  13% /boot
tmpfs                              197M   12K  197M   1% /run/user/1000

Команда: free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       366Mi       1.3Gi       1.1Mi       435Mi       1.6Gi
Swap:          1.9Gi          0B       1.9Gi

Команда: lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda                         8:0    0   20G  0 disk 
├─sda1                      8:1    0    1M  0 part 
├─sda2                      8:2    0  1.8G  0 part /boot
└─sda3                      8:3    0 18.2G  0 part 
  └─ubuntu--vg-ubuntu--lv 252:0    0   10G  0 lvm  /
sr0                        11:0    1 1024M  0 rom  

Команда: date
Mon Mar 29 23:46:24 AM UTC 2026

Команда: systemctl --version
systemd 255 (255.4-1ubuntu8.14)
+PAM +AUDIT +SELINUX +APPARMOR +IMA +SMACK +SECCOMP +GCRYPT -GNUTLS +OPENSSL +ACL +BLKID +CURL +ELFUTILS +FIDO2 +IDN2 -IDN +IPTC +KMOD +LIBCRYPTSETUP +LIBFDISK +PCRE2 -PWQUALITY +P11KIT +QRENCODE +TPM2 +BZIP2 +LZ4 +XZ +ZLIB +ZSTD -BPF_FRAMEWORK -XKBCOMMON +UTMP +SYSVINIT default-hierarchy=unified


```

**Файлы-доказательства (по стандарту):**
- Скрин: `YYYY-MM-DD_LR1.3.6_step01.png`
- Лог: `YYYY-MM-DD_LR1.3.6_step01.log`

---

## Цель работы
Создать собственную службу (демона) и управлять ею через systemd.

---

## Задание (все подпункты)
- [x] **6.1 (скрипт):** создать `my_daemon.sh`, писать в `/tmp/my_daemon.log` каждые 10 секунд, сделать `chmod +x`, проверить ручной запуск.
- [x] **6.2 (юнит):** создать `/etc/systemd/system/my-daemon.service` с секциями [Unit]/[Service]/[Install].
- [x] **6.3 (запуск/отладка):** `daemon-reload`, `start`, `status`, проверка лога, `journalctl -u my-daemon -f`.
- [x] **6.4 (управление):** stop/start, `enable`, `is-enabled`.
- [x] **6.5 (опционально):** reboot и проверка автозапуска.
- [x] **6.6 (AI):** 3 вопроса (строки юнита, Type=forking, почему падает как служба).
- [x] **Контрольные вопросы:** 4 вопроса из ЛР 1.3.6.

---

## Критерии приёмки (чек-лист)
- [x] Все подпункты задания выполнены.
- [x] Команды выполнены корректно (нет ошибок синтаксиса, результаты логичны).
- [x] Есть минимум **2 доказательства**: (1) лог/вывод команд, (2) файл/скрин.
- [x] Доказательства названы по стандарту:
  - Скрины: `YYYY-MM-DD_LR1.3.6_stepYY.png`
  - Логи: `YYYY-MM-DD_LR1.3.6_stepYY.log`
  - Конфиги: `YYYY-MM-DD_LR1.3.6_<name>.conf`
- [x] Заполнены «Проблемы и решения», «Самопроверка», «Выводы».

---

## Ход работы (таблица журнал)
Заполняй по мере выполнения.

| Шаг | Что делал(а)            | Команда/действие                                                                                                                                                                                 | Результат (кратко)                                               | Доказательство (имя файла)                                             |
| --: | ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------- | ---------------------------------------------------------------------- |
|   1 | Паспорт стенда          | uname -a<br>cat /etc/os-release<br>whoami<br>ip a<br>df -h<br>free -h<br>lsblk<br>date<br>systemctl --version                                                                                    | Успешно создан паспорт                                           | 3.6/2026-03-29_LR1.3.6_step01.log                                      |
|   2 | Создание скрипта        | nano ~/my_daemon.sh, chmod +x ~/my_daemon.sh, ./my_daemon.sh &, cat /tmp/my_daemon.log                                                                                                           | Скрипт создан, исполняемый, записывает лог каждые 10 сек         | 3.6/2026-03-29_LR1.3.6_step02.png                                      |
|   3 | Создание юнита          | sudo nano /etc/systemd/system/my-daemon.service                                                                                                                                                  | Файл юнита создан в /etc/systemd/system/                         | 3.6/2026-03-29_LR1.3.6_step03.png                                      |
|   4 | Запуск и отладка        | sudo systemctl daemon-reload, sudo systemctl start my-daemon, systemctl status my-daemon, tail -f /tmp/my_daemon.log, journalctl -u my-daemon -f                                                 | Служба активна (running), лог записывается                       | 3.6/2026-03-29_LR1.3.6_step40.png<br>3.6/2026-03-29_LR1.3.6_step41.png |
|   5 | Управление службой      | tail -3 /tmp/my_daemon.log<br>sudo systemctl stop my-daemon<br>tail -3 /tmp/my_daemon.log<br>sudo systemctl start my-daemon<br>sudo systemctl enable my-daemon<br>systemctl is-enabled my-daemon | Служба останавливается/запускается, автозапуск включён (enabled) | 3.6/2026-03-29_LR1.3.6_step05.png                                      |
|   6 | Работа с AI-ассистентом | 3 вопроса про строки юнита, Type=forking, отладку службы                                                                                                                                         | Ответы записаны в файл                                           | 3.6/2026-03-29_LR1.3.6_step06.log                                      |
|   7 | Контрольные вопросы     | 4 вопроса из ЛР 1.3.6                                                                                                                                                                            | Ответы в лог файле                                               | 3.6/2026-03-29_LR1.3.6_step07.log                                      |

---

## Проблемы и решения
Опиши минимум 1 проблему (если не было — напиши «Не возникали»).

- Проблема: При запуске службы my-daemon служба постоянно перезапускалась (счётчик restart counter is at 77+) с ошибкой status=203/EXEC и Failed with result 'exit-code'. Служба не могла работать стабильно.
- Причина (как понял): systemd не мог исполнить скрипт напрямую через ExecStart=/home/student/my_daemon.sh. Для bash-скриптов требуется явное указание интерпретатора, так как systemd не использует переменные окружения из .bashrc.
- Решение (что сделал): 
#Было:
ExecStart=/home/student/my_daemon.sh
#Стало:
ExecStart=/bin/bash /home/student/my_daemon.sh
- Доказательство исправления: student@student:~$ systemctl status my-daemon
● my-daemon.service - Мой первый демон
     Loaded: loaded (/etc/systemd/system/my-daemon.service; disabled; preset: enabled)
     Active: active (running) since Mon 2026-03-30 05:50:27 UTC; 4s ago
   Main PID: 2723 (bash)
      Tasks: 2 (limit: 2263)
     Memory: 556.0K
        CPU: 6ms
     CGroup: /system.slice/my-daemon.service
             ├─2723 /bin/bash /home/student/my_daemon.sh
             └─2726 sleep 10

Mar 30 05:50:27 student systemd1: Started my-daemon.service - Мой первый демон.

student@student:~$ journalctl -u my-daemon -n 5 --no-pager
Mar 30 05:50:27 student systemd1: Started my-daemon.service - Мой первый демон.
(Ошибки 203/EXEC больше нет)

---

## Самопроверка (✓/⚠/✗)
- Оценка: ✓ 
- Пояснение (1–3 строки): Все задания выполнены: скрипт создан и работает, юнит настроен со всеми секциями, служба запускается/останавливается через systemctl, автозапуск включён, логи пишутся. Доказательства сохранены в логах и скриншотах.

---

## Выводы
1–5 предложений: что понял(а), чему научился(ась), где применишь.
В ходе лабораторной работы я научилась создавать собственные systemd-юниты: написала скрипт-демон, создала файл службы с секциями Unit, Service, Install, настроила автозапуск и перезапуск при сбоях. Освоила команды daemon-reload, systemctl start/stop/enable, а также диагностику через journalctl -u. Поняла важность указания правильных путей, прав доступа и пользователя для запуска службы. Эти навыки применимы для создания собственных демонов, автоматизации задач и управления службами на серверах.

---

## Приложения
Перечисли все файлы, которые сдаёшь вместе с отчётом:

- `YYYY-MM-DD_LR1.3.6_step01.log`
- `YYYY-MM-DD_LR1.3.6_step01.png`
- ![[2026-03-29_LR1.3.6_step02.png]]
- ![[2026-03-29_LR1.3.6_step03.png]]
- ![[2026-03-29_LR1.3.6_step40.png]]
- ![[2026-03-29_LR1.3.6_step41.png]]
- ![[2026-03-29_LR1.3.6_step05.png]]
