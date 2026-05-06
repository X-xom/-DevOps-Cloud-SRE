# Отчёт по самостоятельной работе № 1.5.3
## Тема: Самостоятельное расширение томов

**Студент:** Хомяк Мария Александровна 
**Группа:** _____________________  
**Дата выполнения:** 26,04,2026  
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

**Вывод/лог:** `passport_1_5_3.log` *(или вставка ниже)*

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
       valid_lft 85502sec preferred_lft 85502sec
    inet6 fd17:625c:f037:2:a00:27ff:feab:bc32/64 scope global dynamic mngtmpaddr noprefixroute
       valid_lft 85888sec preferred_lft 13888sec
    inet6 fe80::a00:27ff:feab:bc32/64 scope link
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:a8:61:75 brd ff:ff:ff:ff:ff:ff
    inet 192.168.56.12/24 brd 192.168.56.255 scope global enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fea8:6175/64 scope link
       valid_lft forever preferred_lft forever
4: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    link/ether d2:7e:9b:08:91:74 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever

Команда: df -h
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              197M  1.2M  196M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv  9.8G  5.9G  3.4G  64% /
tmpfs                              985M     0  985M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
/dev/mapper/vg_home-lv_home        3.9G   24K  3.7G   1% /home/testuser
/dev/sda2                          1.8G  200M  1.5G  13% /boot
tmpfs                              197M   12K  197M   1% /run/user/1000

Команда: free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       342Mi       1.4Gi       1.2Mi       382Mi       1.6Gi
Swap:          1.8Gi          0B       1.8Gi

Команда: lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda                         8:0    0   20G  0 disk
├─sda1                      8:1    0    1M  0 part
├─sda2                      8:2    0  1.8G  0 part /boot
└─sda3                      8:3    0 18.2G  0 part
  └─ubuntu--vg-ubuntu--lv 252:1    0   10G  0 lvm  /
sdb                         8:16   0    3G  0 disk
└─sdb1                      8:17   0    3G  0 part
  └─vg_home-lv_home       252:0    0    4G  0 lvm  /home/testuser
sdc                         8:32   0    3G  0 disk
└─sdc1                      8:33   0    3G  0 part
  └─vg_home-lv_home       252:0    0    4G  0 lvm  /home/testuser
sdd                         8:48   0    5G  0 disk
sr0                        11:0    1 1024M  0 rom

Команда: date
Sun Apr 26 04:29:38 AM UTC 2026

Команда: systemctl --version
systemd 255 (255.4-1ubuntu8.15)
+PAM +AUDIT +SELINUX +APPARMOR +IMA +SMACK +SECCOMP +GCRYPT -GNUTLS +OPENSSL +ACL +BLKID +CURL +ELFUTILS +FIDO2 +IDN2 -IDN +IPTC +KMOD +LIBCRYPTSETUP +LIBFDISK +PCRE2 -PWQUALITY +P11KIT +QRENCODE +TPM2 +BZIP2 +LZ4 +XZ +ZLIB +ZSTD -BPF_FRAMEWORK -XKBCOMMON +UTMP +SYSVINIT default-hierarchy=unified
```

---

## Цель работы
Научиться динамически расширять логические тома LVM и файловые системы без потери данных и остановки сервисов. Освоить добавление новых физических дисков в существующую группу томов (VG) и увеличение размера Logical Volume (LV) «на лету».

---

## Задание (все подпункты)
1.  Используйте стенд, созданный в СР 1.5.2 (должна быть VG `vg_home` и LV `lv_home` размером 4 ГБ).
2.  Добавьте к виртуальной машине **третий диск размером 3 ГБ**.
3.  Создайте на новом диске раздел LVM (тип `8e`) на весь диск.
4.  Инициализируйте этот раздел как физический том (PV).
5.  Добавьте новый PV в существующую группу томов `vg_home` (команда `vgextend`).
6.  Убедитесь, что размер VG увеличился (команда `vgs`).
7.  Расширьте логический том `lv_home` до **6 ГБ** (используйте `lvextend` с опцией `-L 6G` или `-L +2G`).
8.  Расширьте файловую систему на `lv_home`, чтобы она использовала新增ленное пространство (команда `resize2fs`).
9.  Проверьте, что размер ФС изменился (команда `df -h /home/testuser`).
10. Зафиксируйте все шаги в отчёте с выводами команд.

---

## Критерии приёмки (чек-лист)
- [x] Все подпункты задания выполнены.
- [x] Все тома/разделы созданы с корректными размерами и типами ФС.
- [x] Настроено автомонтирование через `/etc/fstab`, `sudo mount -a` без ошибок.
- [x] После перезагрузки точки монтирования активны (проверка `df -hT`).
- [x] Доказательства собраны по стандарту именования (см. ниже).

### Стандарт именования доказательств
- Скрины: `YYYY-MM-DD_1_5_3_stepYY.png`
- Логи: `YYYY-MM-DD_1_5_3_stepYY.log`
- Конфиги: `YYYY-MM-DD_1_5_3_<name>.conf`

---

## Ход работы (таблица журнал)

| Step | Что делал             | Команды                                                                 | Где доказательства                                                         | Результат (✓/⚠/✗) |
| ---: | --------------------- | ----------------------------------------------------------------------- | -------------------------------------------------------------------------- | :---------------: |
|   01 | <br>Добавление диска  | lsblk                                                                   | 1.5/153/2026-04-22_1_5_3_step10.png<br>1.5/153/2026-04-22_1_5_3_step11.png |         ✓         |
|   02 | Разметка нового диска | sudo fdisk /dev/sdd (n, p, 1, Enter, Enter, t, 8e, w)<br>sudo partprobe | 1.5/153/2026-04-22_1_5_3_step20.png                                        |         ✓         |
|   03 | Инициализация PV      | sudo pvcreate /dev/sdd1                                                 | 1.5/153/2026-04-22_1_5_3_step30.png                                        |         ✓         |
|   04 | Расширение VG         | sudo vgextend vg_home /dev/sdd1                                         | 1.5/153/2026-04-22_1_5_3_step40.png                                        |         ✓         |
|   05 | Расширение LV         | sudo lvextend -L 6G /dev/vg_home/lv_home                                | 1.5/153/2026-04-22_1_5_3_step50.png                                        |         ✓         |
|   06 | Расширение ФС         | sudo resize2fs /dev/vg_home/lv_home                                     | 1.5/153/2026-04-22_1_5_3_step60.png                                        |         ✓         |
|   07 | Проверка результата   | df -h /home/testuser                                                    | 1.5/153/2026-04-22_1_5_3_step70.png                                        |         ✓         |

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
Освоила процедуру онлайн-расширения дискового пространства в LVM. Это критически важный навык для администрирования серверов, где простой недопустим.
Узнала, что расширение состоит из двух этапов: увеличение блочного устройства (LV) через lvextend и растягивание файловой системы (resize2fs для ext4 или xfs_growfs для XFS).
Поняла, что добавление нового физического диска в VG (vgextend) мгновенно увеличивает доступное пространство для всех логических томов в этой группе.
Убедилась, что данные на разделе сохраняются при расширении, если операции выполняются корректно.

---

## Приложения
- [x] `passport_1_5_3.log - вставила в начале файла лог
- [x] Логи команд: `YYYY-MM-DD_1_5_3_stepYY.log`
- [x] Скриншоты: `YYYY-MM-DD_1_5_3_stepYY.png`
- [x] Фрагмент `/etc/fstab` (только добавленные строки)
- [x] Итоговые выводы: `lsblk`, `df -hT`, `pvs/vgs/lvs` (если применимо)

---

## Контрольные вопросы / критерии
1.  Почему после расширения LV необходимо отдельно расширять файловую систему? Что произойдет, если этого не сделать?
2.  Можно ли расширять том с XFS без размонтирования? А с ext4?
3.  Какой командой можно посмотреть, какие физические тома входят в состав группы томов?
4.  Что такое `resize2fs` и чем она отличается от `xfs_growfs`?

**Ответы:**
1.  LV — это просто блочное устройство. ФС «не знает» об изменении размера контейнера. Без resize новое пространство будет недоступно для записи, хотя физически оно есть.
2.  Да, обе поддерживают онлайн-расширение.
ext4: resize2fs /dev/vg/lv
XFS: xfs_growfs /точка/монтирования
3.  sudo pvs (кратко) или sudo pvdisplay (подробно).
4.  resize2fs — для ext2/3/4. Работает с путем к устройству (/dev/...).
xfs_growfs — только для XFS. Работает только на смонтированных ФС и требует указания точки монтирования (/mnt/...).

---

## Использование AI-ассистента
- Какие вопросы задавал:  подсказал про команду sudo partprobe, которая заставляет ядро Linux перечитать таблицу разделов на всех дисках, потому что ядро может не знать о его существовании до перезагрузки.
- Коротко что помогло/не помогло:  
