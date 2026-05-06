# Отчёт по лабораторной работе LR1.3.5
## Тема: Управление процессами и службами в Linux

### Титульный блок
- Учебное заведение: НИТУ МИСИС
- Дисциплина/курс: Прикладная информатика, 4 курс
- Лабораторная работа: **LR1.3.5 — Диагностика проблем с помощью journalctl**
- Студент: Хомяк Мария Александровна Группа: _______
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
       valid_lft 1354sec preferred_lft 1354sec
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
Mem:           1.9Gi       355Mi       1.4Gi       1.1Mi       376Mi       1.6Gi
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
Mon Mar 29 21:07:01 AM UTC 2026

Команда: systemctl --version
systemd 255 (255.4-1ubuntu8.14)
+PAM +AUDIT +SELINUX +APPARMOR +IMA +SMACK +SECCOMP +GCRYPT -GNUTLS +OPENSSL +ACL +BLKID +CURL +ELFUTILS +FIDO2 +IDN2 -IDN +IPTC +KMOD +LIBCRYPTSETUP +LIBFDISK +PCRE2 -PWQUALITY +P11KIT +QRENCODE +TPM2 +BZIP2 +LZ4 +XZ +ZLIB +ZSTD -BPF_FRAMEWORK -XKBCOMMON +UTMP +SYSVINIT default-hierarchy=unified


```

**Файлы-доказательства (по стандарту):**
- Скрин: `YYYY-MM-DD_LR1.3.5_step01.png`
- Лог: `YYYY-MM-DD_LR1.3.5_step01.log`

---

## Цель работы
Научиться использовать централизованный журнал systemd для поиска и анализа ошибок в работе служб.

---

## Задание (все подпункты)
- [x] **5.1:** `journalctl | head -20`, логи SSH за 10 минут.
- [x] **5.2:** `journalctl -f` + действия во 2-м терминале (restart ssh, ping), зафиксировать новые записи.
- [x] **5.3 (ошибка nginx):** добавить `blabla;` в конфиг, restart nginx, найти ошибку через `journalctl -u nginx -p err --since ...`, исправить и восстановить работу.
- [x] **5.4 (фильтрация):** `-p crit --since today`, `-p warning --since "1 hour ago"`, `_UID=$(id -u)`.
- [x] **5.5 (AI):** 3 вопроса (уровни логов, персистентность, поиск по PID).
- [x] **Контрольные вопросы:** 4 вопроса из ЛР 1.3.5.

---

## Критерии приёмки (чек-лист)
- [x] Все подпункты задания выполнены.
- [x] Команды выполнены корректно (нет ошибок синтаксиса, результаты логичны).
- [x] Есть минимум **2 доказательства**: (1) лог/вывод команд, (2) файл/скрин.
- [x] Доказательства названы по стандарту:
  - Скрины: `YYYY-MM-DD_LR1.3.5_stepYY.png`
  - Логи: `YYYY-MM-DD_LR1.3.5_stepYY.log`
  - Конфиги: `YYYY-MM-DD_LR1.3.5_<name>.conf`
- [x] Заполнены «Проблемы и решения», «Самопроверка», «Выводы».

---

## Ход работы (таблица журнал)
Заполняй по мере выполнения.

| Шаг | Что делал(а)                    | Команда/действие                                                                                                                                                                                                                                                            | Результат (кратко)                                                   | Доказательство (имя файла)                                             |
| --: | ------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- | ---------------------------------------------------------------------- |
|   1 | Паспорт стенда                  | uname -a<br>cat /etc/os-release<br>whoami<br>ip a<br>df -h<br>free -h<br>lsblk<br>date<br>systemctl --version                                                                                                                                                               | Паспорт успешно создан                                               | 3.5/2026-03-29_LR1.3.5_step01.log                                      |
|   2 | Базовое знакомство с journalctl | journalctl \| head -20  <br>journalctl -u ssh --since "10 minutes ago"                                                                                                                                                                                                      | Увидела системные логи, записи SSH за последние 10 мин               | 3.5/2026-03-29_LR1.3.4_step02.png                                      |
|   3 | Мониторинг в реальном времени   | Терминал 1: journalctl -f  <br>Терминал 2: sudo systemctl restart ssh                                                                                                                                                                                                       | В реальном времени появились записи о restart ssh и ping             | 3.5/2026-03-29_LR1.3.4_step30.png<br>3.5/2026-03-29_LR1.3.4_step31.png |
|   4 | Создание и диагностика ошибки   | sudo bash -c 'echo "blabla;" >> /etc/nginx/nginx.conf'  <br>sudo systemctl restart nginx  <br>systemctl status nginx  <br>journalctl -u nginx -p err --since "1 minute ago"  <br>sudo nano /etc/nginx/nginx.conf <br>sudo systemctl restart nginx<br>systemctl status nginx | Ошибка в конфиге найдена, служба восстановлена                       | 3.5/2026-03-29_LR1.3.4_step40.png<br>3.5/2026-03-29_LR1.3.4_step41.png |
|   5 | Фильтрация по уровню и времени  | journalctl -p crit --since today  <br>journalctl -p warning --since "1 hour ago"  <br>journalctl _UID=$(id -u)                                                                                                                                                              | Критические ошибки, предупреждения и логи пользователя отфильтрованы | 3.5/2026-03-29_LR1.3.4_step50.png<br>3.5/2026-03-29_LR1.3.4_step51.png |
|   6 | Работа с AI-ассистентом         | 3 вопроса про уровни логов, персистентность, поиск по PID                                                                                                                                                                                                                   | Ответы записаны в файле                                              | 3.5/2026-03-29_LR1.3.4_step06.log                                      |
|   7 | Контрольные вопросы             | 4 вопроса из ЛР 1.3.5                                                                                                                                                                                                                                                       | Ответы в лог файле                                                   | 3.5/2026-03-29_LR1.3.4_step07.log                                      |

---

## Проблемы и решения
Опиши минимум 1 проблему (если не было — напиши «Не возникали»).

- Проблема: Не возникали
- Причина (как понял): ________________________________
- Решение (что сделал): _______________________________
- Доказательство исправления: __________________________

---

## Самопроверка (✓/⚠/✗)
- Оценка: ✓
- Пояснение (1–3 строки): Все задания выполнены: логи просмотрены через journalctl, мониторинг в реальном времени протестирован, ошибка в nginx создана и найдена через фильтрацию по уровню и времени. Доказательства сохранены в логах и скриншотах.

---

## Выводы
1–5 предложений: что понял(а), чему научился(ась), где применишь.
В ходе лабораторной работы я научилась использовать journalctl для диагностики проблем в Linux: просматривать логи служб (-u), фильтровать по времени (--since) и уровню важности (-p), а также мониторить события в реальном времени (-f). Поняла разницу между уровнями логов (err, warning, crit) и освоила поиск записей по пользователю (UID). Эти навыки применимы для быстрого поиска причин сбоев служб и анализа инцидентов на серверах.

---

## Приложения
Перечисли все файлы, которые сдаёшь вместе с отчётом:

- `YYYY-MM-DD_LR1.3.5_step01.log`
- `YYYY-MM-DD_LR1.3.5_step01.png`
- ![[2026-03-29_LR1.3.5_step02.png]]
- ![[2026-03-29_LR1.3.5_step30.png]]
- ![[2026-03-29_LR1.3.5_step31.png]]
- ![[2026-03-29_LR1.3.5_step40.png]]
- ![[2026-03-29_LR1.3.5_step41.png]]
- ![[2026-03-29_LR1.3.5_step50.png]]
- ![[2026-03-29_LR1.3.5_step51.png]]