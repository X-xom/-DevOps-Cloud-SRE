# Отчёт по лабораторной работе LR1.3.1
## Тема: Управление процессами и службами в Linux

### Титульный блок
- Учебное заведение: НИТУ МИСИС
- Дисциплина/курс: Прикладная информатика, 4 курс
- Лабораторная работа: **LR1.3.1 — Исследование процессов в системе**
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
Linux student 6.8.0-101-generic #101-Ubuntu SMP PREEMPT_DYNAMIC Mon Feb  9 10:15:05 UTC 2026 x86_64 x86_64 x86_64 GNU/Linux

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
    inet 172.20.10.9/28 metric 100 brd 172.20.10.15 scope global dynamic enp0s3
       valid_lft 3446sec preferred_lft 3446sec
    inet6 fe80::a00:27ff:fe96:2123/64 scope link 
       valid_lft forever preferred_lft forever

Команда: df -h
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              197M  1.1M  196M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv  9.8G  5.1G  4.2G  56% /
tmpfs                              985M     0  985M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
/dev/sda2                          1.8G  200M  1.5G  13% /boot
tmpfs                              197M   12K  197M   1% /run/user/1000

Команда: free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       390Mi       371Mi       988Ki       1.4Gi       1.5Gi
Swap:          1.9Gi       268Ki       1.9Gi

Команда: lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda                         8:0    0   20G  0 disk 
├─sda1                      8:1    0    1M  0 part 
├─sda2                      8:2    0  1.8G  0 part /boot
└─sda3                      8:3    0 18.2G  0 part 
  └─ubuntu--vg-ubuntu--lv 252:0    0   10G  0 lvm  /
sr0                        11:0    1 1024M  0 rom  

Команда: date
Sun Mar 29 03:22:19 AM UTC 2026

Команда: systemctl --version
systemd 255 (255.4-1ubuntu8.14)
+PAM +AUDIT +SELINUX +APPARMOR +IMA +SMACK +SECCOMP +GCRYPT -GNUTLS +OPENSSL +ACL +BLKID +CURL +ELFUTILS +FIDO2 +IDN2 -IDN +IPTC +KMOD +LIBCRYPTSETUP +LIBFDISK +PCRE2 -PWQUALITY +P11KIT +QRENCODE +TPM2 +BZIP2 +LZ4 +XZ +ZLIB +ZSTD -BPF_FRAMEWORK -XKBCOMMON +UTMP +SYSVINIT default-hierarchy=unified


```

**Файлы-доказательства (по стандарту):**
- Скрин: `YYYY-MM-DD_LR1.3.1_step01.png`
- Лог: `YYYY-MM-DD_LR1.3.1_step01.log`

---

## Цель работы
Научиться получать информацию о процессах, анализировать их атрибуты, строить дерево процессов.

---

## Задание (все подпункты)
- [x] **1.1 (ps):** `ps aux` (первые 5 строк), процесс PID=1, процессы моего пользователя, процесс с максимальным RSS.
- [x] **1.2 (pstree):** `pstree`, `pstree -p`, родитель моего shell.
- [x] **1.3 (поиск по имени):** запусти приложение, найди PID через `ps aux | grep`, закрой и проверь исчезновение.
- [x] **1.4 (состояния):** `sleep 300 &`, найди STAT, найди `sleep` в `pstree` и родителя.
- [x] **1.5 (AI):** ответы на 3 вопроса про VSZ/RSS, STAT-символы, поиск процессов пользователя.
- [x] **Контрольные вопросы:** 4 вопроса из ЛР 1.3.1.

---

## Критерии приёмки (чек-лист)
- [x] Все подпункты задания выполнены.
- [x] Команды выполнены корректно (нет ошибок синтаксиса, результаты логичны).
- [x] Есть минимум **2 доказательства**: (1) лог/вывод команд, (2) файл/скрин.
- [x] Доказательства названы по стандарту:
  - Скрины: `YYYY-MM-DD_LR1.3.1_stepYY.png`
  - Логи: `YYYY-MM-DD_LR1.3.1_stepYY.log`
  - Конфиги: `YYYY-MM-DD_LR1.3.1_<name>.conf`
- [x] Заполнены «Проблемы и решения», «Самопроверка», «Выводы».

---

## Ход работы (таблица журнал)
Заполняй по мере выполнения.

| Шаг | Что делал(а)                   | Команда/действие                                                                                                                                                                    | Результат (кратко)                                                            | Доказательство (имя файла)                                             |
| --: | ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
|   1 | Паспорт стенда                 | uname -a<br>cat /etc/os-release<br>whoami<br>ip a<br>df -h<br>free -h<br>lsblk<br>date<br>systemctl --version                                                                       | Определена ОС Ubuntu 24.04, ядро 6.8.0                                        | 3.1/2026-03-29_LR1.3.1_step01.log                                      |
|   2 | Знакомство с ps                | ps aux \| head -5  <br>ps -p 1 -o pid,user,cmd  <br>ps -u $USER  <br>ps aux --sort=-rss \| head -10  <br>pstree  <br>pstree -p  <br>sleep 300 &  <br>ps aux \| grep sleep  <br>jobs | PID 1 — systemd, найдены процессы пользователя, определён процесс с макс. RSS | 3.1/2026-03-29_LR1.3.1_step01.png                                      |
|   3 | Анализ дерева процессов        | pstree<br>pstree -p<br>echo $PPID                                                                                                                                                   | Построено дерево, найден родитель shell (sshd/login)                          | 3.1/2026-03-29_LR1.3.1_step20.png<br>3.1/2026-03-29_LR1.3.1_step21.png |
|   4 | Поиск процессов по имени       | top &<br>ps aux \| grep top<br>kill -9 15017<br>ps aux \| grep top<br>                                                                                                              | PID калькулятора = 15017, после остановки — не найден                         | 3.1/2026-03-29_LR1.3.1_step03.png                                      |
|   5 | Работа с состояниями процессов | sleep 300 &<br>ps aux \| grep sleep<br>pstree -p \| grep -B2 sleep<br>pstree -p -s                                                                                                  | PID sleep = 15037, STAT = S, родитель = bash (PID 1091)                       | 3.1/2026-03-29_LR1.3.1_step04.png                                      |
|   6 | Работа с AI-ассистентом        | Записать ответы в отчёт                                                                                                                                                             | Успешно созданный файл с ответами от AI                                       | 3.1/2026-03-29_LR1.3.1_step05.log                                      |
|   7 | Контрольные вопросы            | Ответить на вопросы                                                                                                                                                                 | Успешно созданный файл с ответами                                             | 3.1/2026-03-29_LR1.3.1_step06.log                                      |

---

## Проблемы и решения
Опиши минимум 1 проблему (если не было — напиши «Не возникали»).

- Проблема: Открытое приложение( например xclock &) не отображалось в ps aux
- Причина (как понял): в моей среде нет графической оболочки
- Решение (что сделал): пришлось запустить просто top &
- Доказательство исправления: 
  student@student:~/lab$ xclock &
[1] 15014
student@student:~/lab$ Error: Can't open display:
^C
[1]+  Exit 1                  xclock
student@student:~/lab$ top &
[1] 15017

---

## Самопроверка (✓/⚠/✗)
- Оценка: ✓ 
- Пояснение (1–3 строки): ______________________________
Все задания выполнены: процессы найдены через ps и pstree, PID отображены явно (pgrep, ps -o pid), состояния процессов проверены, скрипты созданы и протестированы. Доказательства сохранены в логах и скриншотах по стандарту.
---

## Выводы
1–5 предложений: что понял(а), чему научился(ась), где применишь.
В ходе лабораторной работы я научилась анализировать процессы в Linux: определять PID, PPID, состояния (S, R, Z) и иерархию с помощью ps, pstree и pgrep. Освоила запуск задач в фоновом режиме (&), управление ими через jobs/kill и мониторинг нагрузки через htop. Поняла разницу между виртуальной (VSZ) и резидентной (RSS) памятью, а также роль процесса с PID=1 (systemd). Эти навыки применимы для администрирования серверов, отладки приложений и диагностики производительности системы.

---

## Приложения
Перечисли все файлы, которые сдаёшь вместе с отчётом:

- `YYYY-MM-DD_LR1.3.1_step01.log`
- `YYYY-MM-DD_LR1.3.1_step01.png`
- ![[2026-03-29_LR1.3.1_step01.png]]
- ![[2026-03-29_LR1.3.1_step20.png]]
- ![[2026-03-29_LR1.3.1_step21.png]]
- ![[2026-03-29_LR1.3.1_step03.png]]
- ![[2026-03-29_LR1.3.1_step04.png]]
