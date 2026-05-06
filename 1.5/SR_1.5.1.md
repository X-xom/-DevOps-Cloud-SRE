# Отчёт по самостоятельной работе № 1.5.1
## Тема: Отработка создания разделов и файловых систем на виртуальных дисках

**Студент:** Хомяк Мария Александровна  
**Группа:** _____________________  
**Дата выполнения:** 22,04,2026  
**Плановое время:** 3 ч (по курсу)

---

## Титульный блок
- **ОС/дистрибутив:** ____________________
- **Версия ядра:** 6.8.0-110-generic  *(uname -r)*
- **Гипервизор/стенд:** ____________________
- **Снапшот перед началом (если делал):** ____________________

---

## Паспорт стенда[[]]
> Выполни и вставь вывод (или приложи лог-файл), минимум:  
`uname -a`, `cat /etc/os-release`, `whoami`, `ip a`, `df -h`, `free -h`, `lsblk`, `date`, `systemctl --version` (если есть systemd)

**Вывод/лог:** `passport_1_5_1.log` *(или вставка ниже)*

```text
Команда: uname -a
Linux ubuntu-lab 6.8.0-107-generic #107-Ubuntu SMP PREEMPT_DYNAMIC Fri Mar 13 19:51:50 UTC 2026 x86_64 x86_64 x86_64 GNU/Linux

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
       valid_lft 79762sec preferred_lft 79762sec
    inet6 fd17:625c:f037:2:a00:27ff:feab:bc32/64 scope global dynamic mngtmpaddr noprefixroute
       valid_lft 86287sec preferred_lft 14287sec
    inet6 fe80::a00:27ff:feab:bc32/64 scope link
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:a8:61:75 brd ff:ff:ff:ff:ff:ff
    inet 192.168.56.12/24 brd 192.168.56.255 scope global enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fea8:6175/64 scope link
       valid_lft forever preferred_lft forever
4: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    link/ether ca:5e:04:1d:2c:86 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever

Команда: df -h
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              197M  1.2M  196M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv  9.8G  5.9G  3.4G  64% /
tmpfs                              985M     0  985M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
/dev/sda2                          1.8G  200M  1.5G  13% /boot
tmpfs                              197M   12K  197M   1% /run/user/1000

Команда: free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       444Mi       183Mi       1.1Mi       1.5Gi       1.5Gi
Swap:          1.8Gi       268Ki       1.8Gi

Команда: lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda                         8:0    0   20G  0 disk
├─sda1                      8:1    0    1M  0 part
├─sda2                      8:2    0  1.8G  0 part /boot
└─sda3                      8:3    0 18.2G  0 part
  └─ubuntu--vg-ubuntu--lv 252:0    0   10G  0 lvm  /
sdb                         8:16   0    3G  0 disk
└─sdb1                      8:17   0    3G  0 part
sdc                         8:32   0    3G  0 disk
├─sdc1                      8:33   0  500M  0 part
├─sdc2                      8:34   0  500M  0 part
└─sdc3                      8:35   0    1G  0 part
sdd                         8:48   0    5G  0 disk
sr0                        11:0    1 1024M  0 rom

Команда: date
Thu Apr 22 01:24:05 AM UTC 2026

Команда: systemctl --version
systemd 255 (255.4-1ubuntu8.15)
+PAM +AUDIT +SELINUX +APPARMOR +IMA +SMACK +SECCOMP +GCRYPT -GNUTLS +OPENSSL +ACL +BLKID +CURL +ELFUTILS +FIDO2 +IDN2 -IDN +IPTC +KMOD +LIBCRYPTSETUP +LIBFDISK +PCRE2 -PWQUALITY +P11KIT +QRENCODE +TPM2 +BZIP2 +LZ4 +XZ +ZLIB +ZSTD -BPF_FRAMEWORK -XKBCOMMON +UTMP +SYSVINIT default-hierarchy=unified
```

---

## Цель работы
Научиться создавать разделы дисков с разными таблицами разделов (MBR и GPT), форматировать их в различные файловые системы (ext4, XFS), монтировать их вручную и настраивать автоматическое монтирование через /etc/fstab с использованием UUID.

---

## Задание (все подпункты)
1.  Добавьте к вашей виртуальной машине **3 виртуальных диска** по 2 ГБ каждый.
2.  На первом диске (`/dev/vdb`):
    - Создайте таблицу разделов **MBR**.
    - Создайте один первичный раздел на весь диск.
    - Отформатируйте его в файловую систему **ext4**.
3.  На втором диске (`/dev/vdc`):
    - Создайте таблицу разделов **GPT**.
    - Разбейте диск на 3 раздела: **500 МБ**, **500 МБ**, **1 ГБ** (оставшееся место). Тип разделов оставьте по умолчанию (Linux filesystem).
    - Отформатируйте первый раздел в **ext4**, второй — в **XFS**, третий — в **ext4**.
4.  На третьем диске (`/dev/vdd`):
    - Создайте таблицу разделов **GPT**.
    - Создайте один раздел на весь диск.
    - Отформатируйте его в файловую систему **XFS**.
5.  Создайте точки монтирования:
    - `/mnt/disk1` для первого диска
    - `/mnt/disk2_part1`, `/mnt/disk2_part2`, `/mnt/disk2_part3` для разделов второго диска
    - `/mnt/disk3` для третьего диска
6.  Примонтируйте **все созданные разделы** вручную и проверьте, что они доступны для записи (создайте тестовые файлы).
7.  Настройте **автоматическое монтирование** при загрузке системы:
    - Для каждого раздела получите его **UUID**.
    - Добавьте соответствующие записи в файл `/etc/fstab`.
    - Используйте опции монтирования `defaults 0 2` для всех разделов, кроме случая, если раздел с XFS — для него можно оставить `defaults 0 2`.
8.  Перезагрузите виртуальную машину и убедитесь, что все разделы примонтировались автоматически.
9.  Удалите тестовые файлы (необязательно, но можно).

---

## Критерии приёмки (чек-лист)
- [x] Все подпункты задания выполнены.
- [x] Все тома/разделы созданы с корректными размерами и типами ФС.
- [x] Настроено автомонтирование через `/etc/fstab`, `sudo mount -a` без ошибок.
- [x] После перезагрузки точки монтирования активны (проверка `df -hT`).
- [x] Доказательства собраны по стандарту именования (см. ниже).

### Стандарт именования доказательств
- Скрины: `2026-04-22_1_5_1_step10.png`
- Логи: `YYYY-MM-DD_1_5_1_stepYY.log`
- Конфиги: `YYYY-MM-DD_1_5_1_<name>.conf`

---

## Ход работы (таблица журнал)

| Step | Что делал                                                                                  | Команды                                                                                                                                                                                       | Где доказательства                                                         | Результат (✓/⚠/✗) |
| ---: | ------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- | :---------------: |
|   01 | Добавила 3 диска в VirtualBox и проверила их видимость в ОС.                               | lsblk  <br>sudo fdisk -l                                                                                                                                                                      | 1.5/151/2026-04-2_1_5_1_step10.png.png                                     |         ✓         |
|   02 | Диск 1 (/dev/sdb): Создала MBR, один первичный раздел на весь диск, форматирование в ext4. | sudo fdisk /dev/sdb<br>(в fdisk: o, n, Enter, Enter, Enter, w)<br>sudo mkfs.ext4 /dev/sdb1                                                                                                    | 1.5/151/2026-04-22_1_5_1_step20.png                                        |         ✓         |
|   03 | Диск 2 (/dev/sdc): Создала GPT, 3 раздела (500M, 500M, остальное) +форматирование.         | sudo fdisk /dev/sdc<br>внутри: g, n (+500M), n (+500M), n (остаток), p, w<br>sudo mkfs.ext4 /dev/vdc1<br>sudo mkfs.xfs /dev/vdc2<br>sudo mkfs.ext4 /dev/vdc3<br>                              | 1.5/151/2026-04-22_1_5_1_step30.png<br>1.5/151/2026-04-22_1_5_1_step31.png |         ✓         |
|   04 | Диск 3 (/dev/sdd): Создала GPT, один раздел на весь диск, форматирование в XFS.            | sudo fdisk /dev/vdc<br>Внутри: g, n,w<br>sudo mkfs.xfs /dev/vdd1<br>                                                                                                                          | 1.5/151/2026-04-22_1_5_1_step40.png                                        |         ✓         |
|   05 | Создала точки монтирования                                                                 | sudo mkdir -p /mnt/disk1 /mnt/disk2_part1 /mnt/disk2_part2 /mnt/disk2_part3 /mnt/disk3<br>ls -l /mnt/                                                                                         | 1.5/151/2026-04-22_1_5_1_step50.png                                        |         ✓         |
|   06 | Примонтировала вручную точки                                                               | sudo mount /dev/sdb1 /mnt/disk1<br>sudo mount /dev/sdc1 /mnt/disk2_part1<br>sudo mount /dev/sdc2 /mnt/disk2_part2<br>sudo mount /dev/sdc3 /mnt/disk2_part3<br>sudo mount /dev/sdd1 /mnt/disk3 | 1.5/151/2026-04-22_1_5_1_step60.png                                        |         ✓         |
|   07 | Получил UUID и настроил /etc/fstab.                                                        | sudo blkid<br>sudo nano /etc/fstab<br>sudo mount -a                                                                                                                                           | 1.5/151/2026-04-22_1_5_1_step70.png                                        |         ✓         |
|   08 | Перезагрузка и проверка автомонтирования.                                                  | sudo reboot<br>df -hT                                                                                                                                                                         | 1.5/151/2026-04-22_1_5_1_step80.png                                        |         ✓         |

---

## Проблемы и решения
> Формат: **Симптом → Диагностика (команда) → Причина → Решение → Проверка**

1.  Симптом: Диски определились как sdb/sdc/sdd, а не vdb/vdc/vdd.
Диагностика: lsblk показал имена sd*.
Причина: В VirtualBox диски были подключены к контроллеру SATA по умолчанию.
Решение: Использовал имена sd* в командах. Для будущих работ можно изменить тип контроллера на VirtIO в настройках ВМ.
Проверка: lsblk корректно отображает диски.
2.  

---

## Самопроверка (✓/⚠/✗)
- **Самооценка:** ✓
- **Что проверить повторно, если ⚠/✗:** _______________________________________

---

## Выводы
Освоила создание разделов с помощью fdisk (для MBR) и parted (для GPT). parted удобнее для скриптов и точного указания размеров в МиБ.
Узнала, что для разных ФС нужны разные утилиты форматирования (mkfs.ext4, mkfs.xfs).
Поняла важность использования UUID в /etc/fstab: имена устройств (/dev/sdb1) могут измениться при добавлении новых дисков, а UUID остаются постоянными.
Научилась проверять корректность /etc/fstab командой mount -a перед перезагрузкой, чтобы избежать проблем с загрузкой системы.

---

## Приложения
- [x] `passport_1_5_1.log` - вставила в начало отчёта
- [x] Логи команд: `YYYY-MM-DD_1_5_1_stepYY.log`
- [x] Скриншоты: `YYYY-MM-DD_1_5_1_stepYY.png`
- [x] Фрагмент `/etc/fstab` (только добавленные строки)
- [x] Итоговые выводы: `lsblk`, `df -hT`, `pvs/vgs/lvs` (если применимо)

---

## Контрольные вопросы / критерии
1.  В чем принципиальная разница между таблицами разделов MBR и GPT? Для диска какого размера вы бы выбрали MBR и почему?
2.  Что такое UUID и почему рекомендуется использовать его в `/etc/fstab` вместо имени устройства (например, `/dev/vdb1`)?
3.  Какая команда позволяет посмотреть список всех блочных устройств в виде дерева?
4.  Что произойдет, если в `/etc/fstab` допущена синтаксическая ошибка? Как восстановить работоспособность системы?

**Ответы:**
1.  MBR поддерживает диски до 2 ТБ и максимум 4 первичных раздела. GPT поддерживает диски любого размера и неограниченное число разделов. MBR выбирают только для совместимости со старым BIOS или дисками < 2 ТБ; в остальных случаях — GPT.
2.  UUID — уникальный идентификатор раздела. Его используют вместо имени устройства (например, /dev/sdb1), потому что имена могут измениться при добавлении новых дисков, а UUID остаётся постоянным, что предотвращает ошибки монтирования.
3.  Команда lsblk.
4.  Ошибка в fstab: Система может не загрузиться или перейти в аварийный режим. Для восстановления нужно перемонтировать корень на запись (mount -o remount,rw /), исправить или закомментировать ошибочную строку в /etc/fstab и перезагрузиться.

---

## Использование AI-ассистента
- Какие вопросы задавал:  Как интерпретировать имена дисков sdb вместо vdb; какие команды использовать для GPT разметки; как правильно оформить fstab
- Коротко что помогло/не помогло:  Помогло разъяснение разницы между контроллерами SATA и VirtIO, а также готовые шаблоны команд для parted и fstab
