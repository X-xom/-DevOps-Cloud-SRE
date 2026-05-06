# Отчёт по лабораторной работе LR1.3.3
## Тема: Управление процессами и службами в Linux

### Титульный блок
- Учебное заведение: НИТУ МИСИС
- Дисциплина/курс: Прикладная информатика, 4 курс
- Лабораторная работа: **LR1.3.3 — Эксперименты с приоритетами**
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
       valid_lft 2188sec preferred_lft 2188sec
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
Mem:           1.9Gi       399Mi       340Mi       988Ki       1.4Gi       1.5Gi
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
Sun Mar 29 06:13:20 AM UTC 2026

Команда: systemctl --version
systemd 255 (255.4-1ubuntu8.14)
+PAM +AUDIT +SELINUX +APPARMOR +IMA +SMACK +SECCOMP +GCRYPT -GNUTLS +OPENSSL +ACL +BLKID +CURL +ELFUTILS +FIDO2 +IDN2 -IDN +IPTC +KMOD +LIBCRYPTSETUP +LIBFDISK +PCRE2 -PWQUALITY +P11KIT +QRENCODE +TPM2 +BZIP2 +LZ4 +XZ +ZLIB +ZSTD -BPF_FRAMEWORK -XKBCOMMON +UTMP +SYSVINIT default-hierarchy=unified


```

**Файлы-доказательства (по стандарту):**
- Скрин: `YYYY-MM-DD_LR1.3.3_step01.png`
- Лог: `YYYY-MM-DD_LR1.3.3_step01.log`

---

## Цель работы
Экспериментально подтвердить влияние приоритета (nice) на распределение процессорного времени.

---

## Задание (все подпункты)
- [x] **3.1 (подготовка):** установить `stress` или создать `load.sh`.
- [x] **3.2 (одинаковый приоритет):** два процесса нагрузки, наблюдение в `top` (Shift+P).
- [x] **3.3 (разный приоритет):** `nice -n 19 ...`, наблюдение NI и %CPU, скрин `top`.
- [x] **3.4 (renice):** изменить nice, попытка `renice -5` без sudo (ошибка), затем с sudo.
- [x] **3.5 (выводы):** сформулировать выводы и зачем менять приоритеты.
- [x] **3.6 (AI):** 3 вопроса (планировщик и nice, почему нельзя negative, RT-приоритеты).
- [x] **Контрольные вопросы:** 4 вопроса из ЛР 1.3.3.

---

## Критерии приёмки (чек-лист)
- [x] Все подпункты задания выполнены.
- [x] Команды выполнены корректно (нет ошибок синтаксиса, результаты логичны).
- [x] Есть минимум **2 доказательства**: (1) лог/вывод команд, (2) файл/скрин.
- [x] Доказательства названы по стандарту:
  - Скрины: `YYYY-MM-DD_LR1.3.3_stepYY.png`
  - Логи: `YYYY-MM-DD_LR1.3.3_stepYY.log`
  - Конфиги: `YYYY-MM-DD_LR1.3.3_<name>.conf`
- [x] Заполнены «Проблемы и решения», «Самопроверка», «Выводы».

---

## Ход работы (таблица журнал)
Заполняй по мере выполнения.

| Шаг | Что делал(а)            | Команда/действие                                                                                                                                           | Результат (кратко)                                               | Доказательство (имя файла)                                             |
| --: | ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------------- |
|   1 | Паспорт стенда          | uname -a<br>cat /etc/os-release<br>whoami<br>ip a<br>df -h<br>free -h<br>lsblk<br>date<br>systemctl --version                                              | Успешно зафиксированный паспорт                                  | 3.3/2026-03-29_LR1.3.3_step01.log                                      |
|   2 | Подготовка              | nano ~/load.sh<br>    #!/bin/bash<br>    while true; do<br>        echo "scale=5000; 4*a(1)" \| bc -l -q > /dev/null<br>    done<br>    chmod +x ~/load.sh | Создан простой скрипт                                            | 3.3/2026-03-29_LR1.3.3_step02.png                                      |
|   3 | Эксперимент 1           | ~/load.sh &<br>~/load.sh &<br>top -> Shift + p<br>q<br>                                                                                                    | Два процесса с NI=0, CPU делится примерно 50/50                  | 3.3/2026-03-29_LR1.3.3_step03.png                                      |
|   4 | Эксперимент 2           | killall bc<br>~/load.sh &<br>nice -n 19 ~/load.sh &<br>top                                                                                                 | Процесс 1: NI=0 (~90%), Процесс 2: NI=19 (~10%)                  | 3.3/2026-03-29_LR1.3.3_step04.png                                      |
|   5 | Эксперимент 3           | ~/load.sh &<br>pgrep -a bc<br>top<br>renice +10 -p 16433<br>renice -5 -p 16433<br>sudo renice -5 -p 16433                                                  | renice +10 сработал, renice -5 без sudo — ошибка, с sudo — успех | 3.3/2026-03-29_LR1.3.3_step50.png<br>3.3/2026-03-29_LR1.3.3_step51.png |
|   6 | Выводы                  | Анализ экспериментов                                                                                                                                       | В лог файле                                                      | 3.3/2026-03-29_LR1.3.3_step06.log                                      |
|   7 | Работа с AI-ассистентом | 3 вопроса про планировщик, negative nice, RT-приоритеты                                                                                                    | Ответы записаны в файл                                           | 3.3/2026-03-29_LR1.3.3_step07.log                                      |
|   8 | Контрольные вопросы     | 4 вопроса из ЛР 1.3.3                                                                                                                                      | Ответы в файле                                                   | 3.3/2026-03-29_LR1.3.3_step08.log                                      |

---

## Проблемы и решения
Опиши минимум 1 проблему (если не было — напиши «Не возникали»).

- Проблема: Не возникали__________________________________________
- Причина (как понял): ________________________________
- Решение (что сделал): _______________________________
- Доказательство исправления: __________________________

---

## Самопроверка (✓/⚠/✗)
- Оценка: ✓
- Пояснение (1–3 строки): ______________________________
Все эксперименты выполнены: процессы с разным nice запущены, распределение CPU зафиксировано в top, renice протестирован с ошибкой и с sudo. Доказательства сохранены в логах и скриншотах.
---

## Выводы
1–5 предложений: что понял(а), чему научился(ась), где применишь.
В ходе лабораторной работы я экспериментально подтвердила влияние приоритета (nice) на распределение процессорного времени: процессы с меньшим nice value получают больше CPU. Научилась запускать процессы с заданным приоритетом (nice -n), изменять приоритет запущенных процессов (renice), и поняла, что отрицательные значения требуют прав root. Эти навыки применимы для оптимизации производительности серверов, когда критически важные процессы должны получать приоритет над фоновыми задачами.

---

## Приложения
Перечисли все файлы, которые сдаёшь вместе с отчётом:

- `YYYY-MM-DD_LR1.3.3_step01.log`
- `YYYY-MM-DD_LR1.3.3_step01.png`
- ![[2026-03-29_LR1.3.3_step02.png]]
- ![[2026-03-29_LR1.3.3_step03.png]]
- ![[2026-03-29_LR1.3.3_step04.png]]
- ![[2026-03-29_LR1.3.3_step50.png]]
- ![[2026-03-29_LR1.3.3_step51.png]]
