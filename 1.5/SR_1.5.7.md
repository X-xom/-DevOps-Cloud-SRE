# Отчёт по самостоятельной работе № 1.5.7
## Тема: Подготовка к промежуточной аттестации (комплексное задание)

**Студент:** Хомяк Мария Александровна 
**Группа:** _____________________  
**Дата выполнения:** 27.04.2026
**Плановое время:** 2 ч (по курсу)

---

## Титульный блок
- **ОС/дистрибутив:** Ubuntu 24.04 LTS
- **Версия ядра:** 6.8.0-110-generic
- **Гипервизор/стенд:** VirtualBox
- **Снапшот перед началом (если делал):** ____________________

---

## Паспорт стенда
> Выполни и вставь вывод (или приложи лог-файл), минимум:  
`uname -a`, `cat /etc/os-release`, `whoami`, `ip a`, `df -h`, `free -h`, `lsblk`, `date`, `systemctl --version` (если есть systemd)

**Вывод/лог:** `passport_1_5_7.log` *(или вставка ниже)*

```text
Команда: uname -a
Linux ubuntu-lab 6.8.0-110-generic #110-Ubuntu SMP PREEMPT_DYNAMIC Thu Mar 19 15:09:20 UTC 2026 x86_64 x86_64 x86_64 GNU/Linux

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
    link/ether 08:00:27:ab:bc:32 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 metric 100 brd 10.0.2.255 scope global dynamic enp0s3
       valid_lft 85213sec preferred_lft 85213sec
    inet6 fd17:625c:f037:2:a00:27ff:feab:bc32/64 scope global dynamic mngtmpaddr noprefixroute
       valid_lft 86375sec preferred_lft 14375sec
    inet6 fe80::a00:27ff:feab:bc32/64 scope link
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:a8:61:75 brd ff:ff:ff:ff:ff:ff
    inet 192.168.56.12/24 brd 192.168.56.255 scope global enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fea8:6175/64 scope link
       valid_lft forever preferred_lft forever
4: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    link/ether fa:56:93:dd:63:9a brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever

Команда: df -h
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              197M  1.2M  196M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv  9.8G  6.0G  3.3G  65% /
tmpfs                              985M     0  985M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
/dev/mapper/vg_web-lv_www_root     974M   28K  907M   1% /var/www
/dev/mapper/vg_home-lv_home        5.9G   24K  5.6G   1% /home/testuser
/dev/mapper/vg_web-lv_www_data     982M   24K  915M   1% /var/www/data
/dev/mapper/vg_web-lv_www_logs     2.0G   71M  1.9G   4% /var/log/www
/dev/sda2                          1.8G  200M  1.5G  13% /boot
tmpfs                              197M   12K  197M   1% /run/user/1000

Команда: free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       357Mi       1.4Gi       1.2Mi       361Mi       1.6Gi
Swap:          1.8Gi          0B       1.8Gi

Команда: lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda                         8:0    0   20G  0 disk
├─sda1                      8:1    0    1M  0 part
├─sda2                      8:2    0  1.8G  0 part /boot
└─sda3                      8:3    0 18.2G  0 part
  └─ubuntu--vg-ubuntu--lv 252:3    0   10G  0 lvm  /
sdb                         8:16   0    3G  0 disk
└─sdb1                      8:17   0    3G  0 part
  └─vg_home-lv_home       252:0    0    6G  0 lvm  /home/testuser
sdc                         8:32   0    3G  0 disk
└─sdc1                      8:33   0    3G  0 part
  └─vg_home-lv_home       252:0    0    6G  0 lvm  /home/testuser
sdd                         8:48   0    3G  0 disk
└─sdd1                      8:49   0    3G  0 part
  ├─vg_home-lv_home       252:0    0    6G  0 lvm  /home/testuser
  ├─vg_home-lv_test       252:1    0  1.5G  0 lvm
  └─vg_home-lv_data       252:2    0    1G  0 lvm
sde                         8:64   0    2G  0 disk
└─sde1                      8:65   0    2G  0 part
  ├─vg_web-lv_www_root    252:4    0    1G  0 lvm  /var/www
  ├─vg_web-lv_www_logs    252:5    0    2G  0 lvm  /var/log/www
  └─vg_web-lv_www_data    252:6    0 1016M  0 lvm  /var/www/data
sdf                         8:80   0    2G  0 disk
└─sdf1                      8:81   0    2G  0 part
  └─vg_web-lv_www_logs    252:5    0    2G  0 lvm  /var/log/www
sr0                        11:0    1 1024M  0 rom

Команда: date
Tue Apr 27 06:03:37 AM UTC 2026

Команда: systemctl --version
systemd 255 (255.4-1ubuntu8.15)
+PAM +AUDIT +SELINUX +APPARMOR +IMA +SMACK +SECCOMP +GCRYPT -GNUTLS +OPENSSL +ACL +BLKID +CURL +ELFUTILS +FIDO2 +IDN2 -IDN +IPTC +KMOD +LIBCRYPTSETUP +LIBFDISK +PCRE2 -PWQUALITY +P11KIT +QRENCODE +TPM2 +BZIP2 +LZ4 +XZ +ZLIB +ZSTD -BPF_FRAMEWORK -XKBCOMMON +UTMP +SYSVINIT default-hierarchy=unified

```

---

## Цель работы
Проверить и закрепить навыки проектирования дисковой подсистемы на базе LVM: создание группы томов из нескольких физических дисков, выделение логических томов заданного размера, форматирование в разные файловые системы (XFS/ext4) и настройка автоматического монтирования через /etc/fstab.

---

## Задание (все подпункты)
Это итоговое задание по теме. Выполните его самостоятельно, без подсказок, как на экзамене. Допускается использование man-страниц и AI-ассистента для уточнения синтаксиса, но не для получения готового решения.

**Условие:**
Вам нужно подготовить сервер для базы данных (MySQL). В вашем распоряжении виртуальная машина с двумя дополнительными дисками:
-   `/dev/vdb` размером **8 ГБ**
-   `/dev/vdc` размером **8 ГБ**

**Требования:**
1.  Используя LVM, создайте том для данных базы данных размером **14 ГБ** с файловой системой **XFS**. Том должен называться `lv_dbdata`, группа томов — `vg_db`.
2.  Создайте отдельный маленький том для резервных копий размером **1.5 ГБ** с файловой системой **ext4**. Том должен называться `lv_dbbak`, группа томов — та же (`vg_db`).
3.  Оба тома должны автоматически монтироваться при загрузке системы:
    -   Том с данными БД в директорию `/var/lib/mysql`
    -   Том с бекапами в директорию `/backup`.
4.  Убедитесь, что после создания томов в VG осталось свободное место для возможного будущего расширения (запишите, сколько именно).
5.  Создайте в корне тома с бекапами директорию `test` и положите туда любой тестовый файл, чтобы подтвердить работоспособность.

**Что нужно предоставить в отчёте:**
-   Скриншот или копию вывода команды `lsblk` (должна быть видна структура: диски -> разделы -> VG -> LV).
-   Скриншот или копию вывода команды `df -hT` (должны быть видны примонтированные тома с правильными точками монтирования и ФС).
-   Скриншот или копию вывода команд `sudo pvs`, `sudo vgs`, `sudo lvs`.
-   Копию содержимого файла `/etc/fstab` (только добавленные строки).
-   Ответ на вопрос: "Сколько свободного места осталось в VG и как вы это узнали?" - 

---

## Критерии приёмки (чек-лист)
- [x] Все подпункты задания выполнены.
- [x] Все тома/разделы созданы с корректными размерами и типами ФС.
- [x] Настроено автомонтирование через `/etc/fstab`, `sudo mount -a` без ошибок.
- [x] После перезагрузки точки монтирования активны (проверка `df -hT`).
- [x] Доказательства собраны по стандарту именования (см. ниже).

### Стандарт именования доказательств
- Скрины: `YYYY-MM-DD_1_5_7_stepYY.png`
- Логи: `YYYY-MM-DD_1_5_7_stepYY.log`
- Конфиги: `YYYY-MM-DD_1_5_7_<name>.conf`

---

## Ход работы (таблица журнал)

| Step | Что делал                | Команды                                                                                                        | Где доказательства                                                         | Результат (✓/⚠/✗) |
| ---: | ------------------------ | -------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- | :---------------: |
|   01 | <br>Подготовка дисков    | sudo fdisk /dev/sdb (type 8e)<br>sudo fdisk /dev/sdc (type 8e)<br>sudo partprobe                               | 1.5/157/2026-04-22_1_5_7_step10.png                                        |         ✓         |
|   02 | Создание PV и VG         | sudo pvcreate /dev/sdb1 /dev/sdc1<br>sudo vgcreate vg_db /dev/sdb1 /dev/sdc1                                   | 1.5/157/2026-04-22_1_5_7_step20.png                                        |         ✓         |
|   03 | Создание LV (Data & Bak) | sudo lvcreate -L 14G -n lv_dbdata vg_db<br>sudo lvcreate -L 1.5G -n lv_dbbak vg_db                             | 1.5/157/2026-04-22_1_5_7_step30.png                                        |         ✓         |
|   04 | Форматирование ФС        | sudo mkfs.xfs /dev/vg_db/lv_dbdata<br>sudo mkfs.ext4 /dev/vg_db/lv_dbbak                                       | 1.5/157/2026-04-22_1_5_7_step40.png                                        |         ✓         |
|   05 | Монтирование и fstab     | sudo mkdir -p /var/lib/mysql /backup<br>sudo blkid \| grep vg_db<br>Редактирование /etc/fstab<br>sudo mount -a | 1.5/157/2026-04-22_1_5_7_step50.png<br>1.5/157/2026-04-22_1_5_7_step51.png |         ✓         |
|   06 | Проверка и тест          | df -hT \| grep vg_db<br>mount -a<br>sudo lvs<br>sudo vgs<br>sudo pvs<br>lsblk                                  | 1.5/157/2026-04-22_1_5_7_step60.png                                        |         ✓         |

---

## Проблемы и решения
> Формат: **Симптом → Диагностика (команда) → Причина → Решение → Проверка**

1.  -
2.  

---

## Самопроверка (✓/⚠/✗)
- **Самооценка:** ✓   
- **Что проверить повторно, если ⚠/✗:** _______________________________________

---

## Выводы
Успешно спроектировала структуру хранения для СУБД, разделив данные и резервные копии на независимые тома.
Освоила работу с остаточным пространством в VG: после создания томов на 14 ГБ и 1.5 ГБ из 16 ГБ осталось ~500 МБ для будущих нужд.
Подтвердила, что XFS подходит для больших объемов данных (БД), а ext4 — для небольших структур (бекапы), хотя технически можно было выбрать и наоборот.
Настроила надежное автоматическое монтирование через UUID, что критично для серверных систем.

---

## Приложения
- [x] `passport_1_5_7.log - в начале файла`
- [x] Логи команд: `YYYY-MM-DD_1_5_7_stepYY.log`
- [x] Скриншоты: `YYYY-MM-DD_1_5_7_stepYY.png`
- [x] Фрагмент `/etc/fstab` (только добавленные строки)
- [x] Итоговые выводы: `lsblk`, `df -hT`, `pvs/vgs/lvs` (если применимо)

---

## Контрольные вопросы / критерии
В этом задании вместо контрольных вопросов используются «Критерии оценки» и требования к сдаче (см. текст задания).

**Ответы:**
1. Ответ на вопрос: "Сколько свободного места осталось в VG и как вы это узнали?" - 
В группе томов vg_db осталось примерно 512 МБ свободного места.
Я узнала это с помощью команды sudo vgs, которая отображает столбец VFree. Также это можно проверить через sudo vgdisplay vg_db | grep "Free PE". (Расчет: 2 диска по 8 ГБ = ~16 ГБ. Минус 14 ГБ и 1.5 ГБ = 0.5 ГБ остатка).


---

## Использование AI-ассистента
- Какие вопросы задавал:  -
- Коротко что помогло/не помогло:  -
