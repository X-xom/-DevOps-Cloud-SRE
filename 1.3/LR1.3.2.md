# Отчёт по лабораторной работе LR1.3.2
## Тема: Управление процессами и службами в Linux

### Титульный блок
- Учебное заведение: НИТУ МИСИС
- Дисциплина/курс: Прикладная информатика, 4 курс
- Лабораторная работа: **LR1.3.2 — Управление процессами и сигналы**
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
       valid_lft 2168sec preferred_lft 2168sec
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
Mem:           1.9Gi       410Mi       333Mi       980Ki       1.4Gi       1.5Gi
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
Sun Mar 29 05:13:39 AM UTC 2026

Команда: systemctl --version
systemd 255 (255.4-1ubuntu8.14)
+PAM +AUDIT +SELINUX +APPARMOR +IMA +SMACK +SECCOMP +GCRYPT -GNUTLS +OPENSSL +ACL +BLKID +CURL +ELFUTILS +FIDO2 +IDN2 -IDN +IPTC +KMOD +LIBCRYPTSETUP +LIBFDISK +PCRE2 -PWQUALITY +P11KIT +QRENCODE +TPM2 +BZIP2 +LZ4 +XZ +ZLIB +ZSTD -BPF_FRAMEWORK -XKBCOMMON +UTMP +SYSVINIT default-hierarchy=unified
```

**Файлы-доказательства (по стандарту):**
- Скрин: `YYYY-MM-DD_LR1.3.2_step01.png`
- Лог: `YYYY-MM-DD_LR1.3.2_step01.log`

---

## Цель работы
Научиться управлять процессами: отправлять сигналы, переводить процессы в фон и на передний план, корректно завершать зависшие приложения.

---

## Задание (все подпункты)
- [x] **2.1 (фон/передний план):** два `sleep 600 &`, `jobs`, `fg`, `Ctrl+Z`, `bg`, проверка `jobs`.
- [x] **2.2 (сигналы):** запусти цикл-вывод в фоне, найди PID, сделай SIGSTOP/SIGCONT, завершение SIGTERM.
- [x] **2.3 (SIGTERM vs SIGKILL):** два `sleep 200 &`, первому SIGTERM, второму SIGKILL, сравни поведение.
- [x] **2.4 (имитация «зависания»):** `cat > /dev/null &`, попробуй `kill`, затем `kill -9`, опиши алгоритм действий.
- [x] **2.5 (AI):** ответы на 3 вопроса (nohup, различие -9/-15, D-state и SIGKILL).
- [x] **Контрольные вопросы:** 4 вопроса из ЛР 1.3.2.

---

## Критерии приёмки (чек-лист)
- [x] Все подпункты задания выполнены.
- [x] Команды выполнены корректно (нет ошибок синтаксиса, результаты логичны).
- [x] Есть минимум **2 доказательства**: (1) лог/вывод команд, (2) файл/скрин.
- [x] Доказательства названы по стандарту:
  - Скрины: `YYYY-MM-DD_LR1.3.2_stepYY.png`
  - Логи: `YYYY-MM-DD_LR1.3.2_stepYY.log`
  - Конфиги: `YYYY-MM-DD_LR1.3.2_<name>.conf`
- [x] Заполнены «Проблемы и решения», «Самопроверка», «Выводы».

---

## Ход работы (таблица журнал)
Заполняй по мере выполнения.

| Шаг | Что делал(а)                         | Команда/действие                                                                                                                           | Результат (кратко)                                                              | Доказательство (имя файла)                                             |
| --: | ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
|   1 | Паспорт стенда                       | uname -a<br>cat /etc/os-release<br>whoami<br>ip a<br>df -h<br>free -h<br>lsblk<br>date<br>systemctl --version                              | Успешно зафиксированный паспорт                                                 | 3.2/2026-03-29_LR1.3.2_step01.log                                      |
|   2 | Фоновый и переднеплановый режимы     | sleep 600 &<br>sleep 600 &<br>jobs<br>fg %1<br>bg %1<br>jobs                                                                               | 2 задачи в фоне, PID показаны, fg/bg работают                                   | 3.2/2026-03-29_LR1.3.2_step02.png                                      |
|   3 | Отправка сигналов                    | while true; do echo "Работаю..."; sleep 2; done &<br>ps aux \| grep bash \| grep -v grep<br>kill -19 15564<br>kill -18 15564<br>kill 15564 | Вывод приостановлен (SIGSTOP), возобновлён (SIGCONT), завершён (SIGTERM)        | 3.2/2026-03-29_LR1.3.2_step30.png<br>3.2/2026-03-29_LR1.3.2_step31.png |
|   4 | Эксперимент с SIGTERM и SIGKILL      | sleep 200 &<br>sleep 200 &<br>kill -15 15626<br>kill -9 15627<br>ps aux \| grep sleep                                                      | SIGTERM — мягкое завершение, SIGKILL — принудительное, оба процесса остановлены | 3.2/2026-03-29_LR1.3.2_step04.png                                      |
|   5 | Моделирование "зависшего" приложения | cat > /dev/null &<br>kill 15634<br>kill -9 15634<br>ps aux \| grep cat<br>                                                                 | Процесс не реагировал на kill, завершён через kill -9                           | 3.2/2026-03-29_LR1.3.2_step05.png                                      |
|   6 | Работа с AI-ассистентом              | Вопросы про nohup, kill -9 vs -15, D-state и SIGKILL                                                                                       | Ответы записаны в лог файл                                                      | 3.2/2026-03-29_LR1.3.2_step06.log                                      |
|   7 | Контрольные вопросы                  | 4 вопроса из ЛР 1.3.2                                                                                                                      | Ответы в файле                                                                  | 3.2/2026-03-29_LR1.3.2_step07.log                                      |

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
- Пояснение (1–3 строки):  Все задания выполнены: процессы запущены в фоне, сигналы отправлены (SIGSTOP, SIGCONT, SIGTERM, SIGKILL), PID отображены явно через pgrep и jobs -l. Доказательства сохранены в логах.

---

## Выводы
1–5 предложений: что понял(а), чему научился(ась), где применишь.
В ходе лабораторной работы я научилась управлять процессами в Linux: запускать задачи в фоновом режиме (&), переключать между фоном и передним планом (fg, bg, Ctrl+Z). Освоила отправку сигналов через kill (SIGTERM, SIGKILL, SIGSTOP, SIGCONT) и поняла разницу между мягким и принудительным завершением. Узнала, что SIGKILL не работает для процессов в состоянии D (uninterruptible sleep). Эти навыки применимы для администрирования серверов и отладки зависших приложений.

---

## Приложения
Перечисли все файлы, которые сдаёшь вместе с отчётом:

- `YYYY-MM-DD_LR1.3.2_step01.log`
- `YYYY-MM-DD_LR1.3.2_step01.png`
- ![[3.2/2026-03-29_LR1.3.2_step02.png]]
- ![[2026-03-29_LR1.3.2_step30.png]]
- ![[2026-03-29_LR1.3.2_step31.png]]
- ![[3.2/2026-03-29_LR1.3.2_step04.png]]
- ![[2026-03-29_LR1.3.2_step05.png]]
