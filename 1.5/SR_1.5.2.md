# Отчёт по самостоятельной работе № 1.5.2
## Тема: Отработка работы с LVM: создание структуры

**Студент:** Хомяк Мария Александровна  
**Группа:** _____________________  
**Дата выполнения:** 26.04.2026  
**Плановое время:** 3 ч (по курсу)

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

**Вывод/лог:** `passport_1_5_2.log` *(или вставка ниже)*

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
       valid_lft 81224sec preferred_lft 81224sec
    inet6 fd17:625c:f037:2:a00:27ff:feab:bc32/64 scope global dynamic mngtmpaddr noprefixroute
       valid_lft 86349sec preferred_lft 14349sec
    inet6 fe80::a00:27ff:feab:bc32/64 scope link
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:a8:61:75 brd ff:ff:ff:ff:ff:ff
    inet 192.168.56.12/24 brd 192.168.56.255 scope global enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fea8:6175/64 scope link
       valid_lft forever preferred_lft forever
4: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    link/ether 3e:99:ef:4f:e4:37 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever

Команда: df -h
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              197M  1.2M  196M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv  9.8G  5.9G  3.4G  64% /
tmpfs                              985M     0  985M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
/dev/sdb1                          2.9G   24K  2.8G   1% /mnt/disk1
/dev/sda2                          1.8G  200M  1.5G  13% /boot
/dev/sdc1                          452M   24K  417M   1% /mnt/disk2_part1
/dev/sdc3                          974M   24K  907M   1% /mnt/disk2_part3
/dev/sdc2                          436M   34M  403M   8% /mnt/disk2_part2
/dev/sdd1                          5.0G  130M  4.9G   3% /mnt/disk3
tmpfs                              197M   12K  197M   1% /run/user/1000

Команда: free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       402Mi       1.2Gi       1.2Mi       457Mi       1.5Gi
Swap:          1.8Gi          0B       1.8Gi

Команда: lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda                         8:0    0   20G  0 disk
├─sda1                      8:1    0    1M  0 part
├─sda2                      8:2    0  1.8G  0 part /boot
└─sda3                      8:3    0 18.2G  0 part
  └─ubuntu--vg-ubuntu--lv 252:0    0   10G  0 lvm  /
sdb                         8:16   0    3G  0 disk
└─sdb1                      8:17   0    3G  0 part /mnt/disk1
sdc                         8:32   0    3G  0 disk
├─sdc1                      8:33   0  500M  0 part /mnt/disk2_part1
├─sdc2                      8:34   0  500M  0 part /mnt/disk2_part2
└─sdc3                      8:35   0    1G  0 part /mnt/disk2_part3
sdd                         8:48   0    5G  0 disk
└─sdd1                      8:49   0    5G  0 part /mnt/disk3
sr0                        11:0    1 1024M  0 rom

Команда: date
Sun Apr 26 02:59:08 AM UTC 2026

Команда: systemctl --version
systemd 255 (255.4-1ubuntu8.15)
+PAM +AUDIT +SELINUX +APPARMOR +IMA +SMACK +SECCOMP +GCRYPT -GNUTLS +OPENSSL +ACL +BLKID +CURL +ELFUTILS +FIDO2 +IDN2 -IDN +IPTC +KMOD +LIBCRYPTSETUP +LIBFDISK +PCRE2 -PWQUALITY +P11KIT +QRENCODE +TPM2 +BZIP2 +LZ4 +XZ +ZLIB +ZSTD -BPF_FRAMEWORK -XKBCOMMON +UTMP +SYSVINIT default-hierarchy=unified
```

---

## Цель работы
Освоить технологию управления логическими томами (LVM) в Linux: научиться создавать физические тома (PV), объединять их в группы томов (VG), выделять логические тома (LV), форматировать их и настраивать автоматическое монтирование. Понять преимущества гибкого управления дисковым пространством по сравнению с традиционными разделами.

---

## Задание (все подпункты)
1.  Добавьте к виртуальной машине **2 диска по 3 ГБ**.
2.  На каждом диске создайте по одному разделу, занимающему весь диск, с типом **Linux LVM** (код `8e` для MBR).
3.  Инициализируйте эти разделы как **физические тома (PV)**.
4.  Создайте **группу томов (VG)** с именем `vg_home`, включив в неё оба созданных PV.
5.  В группе `vg_home` создайте **логический том (LV)** с именем `lv_home` размером **4 ГБ**.
6.  Отформатируйте `lv_home` в файловую систему **ext4**.
7.  Примонтируйте полученный том в директорию `/home/testuser` (предварительно создав пользователя `testuser` или просто создав директорию).
8.  Настройте автоматическое монтирование этого тома в `/etc/fstab` (используйте UUID или путь к устройству `/dev/mapper/vg_home-lv_home`).
9.  Перезагрузите систему и убедитесь, что том примонтировался.
10. Выполните команды `sudo pvs`, `sudo vgs`, `sudo lvs` и сохраните их вывод для отчёта.

---

## Критерии приёмки (чек-лист)
- [x] Все подпункты задания выполнены.
- [x] Все тома/разделы созданы с корректными размерами и типами ФС.
- [x] Настроено автомонтирование через `/etc/fstab`, `sudo mount -a` без ошибок.
- [x] После перезагрузки точки монтирования активны (проверка `df -hT`).
- [x] Доказательства собраны по стандарту именования (см. ниже).

### Стандарт именования доказательств
- Скрины: `YYYY-MM-DD_1_5_2_stepYY.png`
- Логи: `YYYY-MM-DD_1_5_2_stepYY.log`
- Конфиги: `YYYY-MM-DD_1_5_2_<name>.conf`

---

## Ход работы (таблица журнал)

| Step | Что делал             | Команды                                                                          | Где доказательства                                                         | Результат (✓/⚠/✗) |
| ---: | --------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------- | :---------------: |
|   01 | Подготовка дисков     | Добавлены 2 диска по 3 ГБ. lsblk                                                 | 1.5/152/2026-04-22_1_5_2_step10.png                                        |         ✓         |
|   02 | Создание разделов LVM | sudo fdisk /dev/sdb (type 8e)<br>sudo fdisk /dev/sdc (type 8e)<br>sudo partprobe | 1.5/152/2026-04-22_1_5_2_step20.png<br>1.5/152/2026-04-22_1_5_2_step21.png |         ✓         |
|   03 | Инициализация PV      | sudo pvcreate /dev/sdb1 /dev/sdc1<br>sudo pvs                                    | 1.5/152/2026-04-22_1_5_2_step30.png                                        |         ✓         |
|   04 | <br>Создание VG       | sudo vgcreate vg_home /dev/sdb1 /dev/sdc1                                        | 1.5/152/2026-04-22_1_5_2_step40.png                                        |         ✓         |
|   05 | Создание LV           | sudo lvcreate -L 4G -n lv_home vg_home                                           | 1.5/152/2026-04-22_1_5_2_step50.png                                        |         ✓         |
|   06 | <br>Форматирование    | <br>sudo mkfs.ext4 /dev/vg_home/lv_home                                          | 1.5/152/2026-04-22_1_5_2_step60.png                                        |         ✓         |
|   07 | Монтирование          | sudo mkdir -p /home/testuser<br>sudo mount /dev/vg_home/lv_home /home/testuser   | 1.5/152/2026-04-22_1_5_2_step70.png                                        |         ✓         |
|   08 | Настройка fstab       | sudo blkid \| grep lv_home<br>sudo nano /etc/fstab                               | 1.5/152/2026-04-22_1_5_2_step80.png                                        |         ✓         |
|   09 | Проверка после ребута | sudo reboot                                                                      | 1.5/152/2026-04-22_1_5_2_step90.png                                        |         ✓         |
|   10 | <br>Итоговая проверка | sudo pvs<br>sudo vgs<br>sudo lvs                                                 | 1.5/152/2026-04-22_1_5_2_step100.png                                       |         ✓         |

---

## Проблемы и решения
> Формат: **Симптом → Диагностика (команда) → Причина → Решение → Проверка**

1.  -
2.  

---

## Самопроверка (✓/⚠/✗)
- **Самооценка:** ✓
- **Что проверить повторно, если ⚠/✗:** Ничего, всё работает стабильно.

---

## Выводы
(2–5 пунктов: что получилось, что узнал, на что обратить внимание в будущем)

---

## Приложения
- [x] `passport_1_5_2.log` - добавила вывод в начале отчёта
- [x] Логи команд: `YYYY-MM-DD_1_5_2_stepYY.log`
- [x] Скриншоты: `YYYY-MM-DD_1_5_2_stepYY.png`
- [x] Фрагмент `/etc/fstab` (только добавленные строки)
- [x] Итоговые выводы: `lsblk`, `df -hT`, `pvs/vgs/lvs` (если применимо)

---

## Контрольные вопросы / критерии
1.  Запишите полную цепочку команд от создания разделов до монтирования LVM-тома (не менее 6 команд).
2.  Сколько свободного места осталось в VG `vg_home`? Какой командой это можно проверить?
3.  В каких директориях в файловой системе Linux можно найти устройства логических томов (назовите не менее двух)?
4.  Что произойдет, если при создании LV указать размер, превышающий доступное место в VG?

**Ответы:**
1.  
fdisk /dev/sdb (создание раздела, тип 8e)
pvcreate /dev/sdb1 (инициализация PV)
vgcreate vg_home /dev/sdb1 /dev/sdc1 (создание VG)
lvcreate -L 4G -n lv_home vg_home (создание LV)
mkfs.ext4 /dev/vg_home/lv_home (форматирование)
mount /dev/vg_home/lv_home /mnt/point (монтирование)
2.  Осталось ~2 ГБ (из 6 ГБ всего выделено 4 ГБ). Проверка: sudo vgs (колонка VFree) или sudo vgdisplay.
3.  /dev/mapper/ (например, /dev/mapper/vg_home-lv_home)
/dev/<имя_VG>/ (например, /dev/vg_home/lv_home)
4.  Команда завершится ошибкой Insufficient free space, том не будет создан.

---

## Использование AI-ассистента
- Какие вопросы задавал:  Как отмонтировать разделы
- Коротко что помогло/не помогло:  
sudo umount /mnt/disk1
sudo umount /mnt/disk2_part1
sudo umount /mnt/disk2_part2
sudo umount /mnt/disk2_part3
sudo wipefs -a /dev/sdb
sudo wipefs -a /dev/sdc
