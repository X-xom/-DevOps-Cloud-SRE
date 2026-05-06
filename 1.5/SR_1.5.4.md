# Отчёт по самостоятельной работе № 1.5.4
## Тема: Отработка уменьшения тома (только для ext4)

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

**Вывод/лог:** `passport_1_5_4.log` *(или вставка ниже)*

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
       valid_lft 84864sec preferred_lft 84864sec
    inet6 fd17:625c:f037:2:a00:27ff:feab:bc32/64 scope global dynamic mngtmpaddr noprefixroute
       valid_lft 86308sec preferred_lft 14308sec
    inet6 fe80::a00:27ff:feab:bc32/64 scope link
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:a8:61:75 brd ff:ff:ff:ff:ff:ff
    inet 192.168.56.12/24 brd 192.168.56.255 scope global enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fea8:6175/64 scope link
       valid_lft forever preferred_lft forever
4: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    link/ether 8e:13:e8:a7:e1:bf brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever

Команда: df -h
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              197M  1.2M  196M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv  9.8G  6.0G  3.4G  64% /
tmpfs                              985M     0  985M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
/dev/mapper/vg_home-lv_home        5.9G   24K  5.6G   1% /home/testuser
/dev/sda2                          1.8G  200M  1.5G  13% /boot
tmpfs                              197M   12K  197M   1% /run/user/1000

Команда: free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       349Mi       1.4Gi       1.2Mi       362Mi       1.6Gi
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
  └─vg_home-lv_home       252:0    0    6G  0 lvm  /home/testuser
sdc                         8:32   0    3G  0 disk
└─sdc1                      8:33   0    3G  0 part
  └─vg_home-lv_home       252:0    0    6G  0 lvm  /home/testuser
sdd                         8:48   0    3G  0 disk
└─sdd1                      8:49   0    3G  0 part
  └─vg_home-lv_home       252:0    0    6G  0 lvm  /home/testuser
sr0                        11:0    1 1024M  0 rom

Команда: date
Sun Apr 26 05:25:46 AM UTC 2026

Команда: systemctl --version
systemd 255 (255.4-1ubuntu8.15)
+PAM +AUDIT +SELINUX +APPARMOR +IMA +SMACK +SECCOMP +GCRYPT -GNUTLS +OPENSSL +ACL +BLKID +CURL +ELFUTILS +FIDO2 +IDN2 -IDN +IPTC +KMOD +LIBCRYPTSETUP +LIBFDISK +PCRE2 -PWQUALITY +P11KIT +QRENCODE +TPM2 +BZIP2 +LZ4 +XZ +ZLIB +ZSTD -BPF_FRAMEWORK -XKBCOMMON +UTMP +SYSVINIT default-hierarchy=unified
```

---

## Цель работы
Научиться безопасно уменьшать размер логических томов (LV) и файловых систем ext4. Освоить строгий порядок действий: проверка ФС, уменьшение файловой системы, затем уменьшение блочного устройства, чтобы избежать потери данных.

---

## Задание (все подпункты)
**ВНИМАНИЕ:** Уменьшение тома — рискованная операция. Выполняйте её только на тестовых данных, которые не жалко потерять. Все команды выполняйте внимательно.

1.  Создайте в существующей VG (можно использовать `vg_home` или создать новую VG для экспериментов) отдельный логический том размером **2 ГБ** с именем `lv_test` и файловой системой **ext4**.
2.  Примонтируйте его, например, в `/mnt/test`.
3.  Наполните том данными: скопируйте туда содержимое директории `/etc` (или несколько крупных файлов):
    ```bash
    sudo cp -r /etc /mnt/test/
    ```
4.  Убедитесь, что данные скопированы (проверьте размер командой `du -sh /mnt/test`).
5.  Выполните процедуру **уменьшения тома до 1.5 ГБ**:
    - Размонтируйте том.
    - Проверьте файловую систему (`e2fsck -f`).
    - Уменьшите ФС до 1.5 ГБ.
    - Уменьшите LV до 1.5 ГБ.
    - Примонтируйте том обратно.
6.  Проверьте целостность данных. Например, сравните исходную директорию `/etc` с скопированной:
    ```bash
    diff -r /etc /mnt/test/etc
    ```
    Команда не должна выдать различий (или выдать минимум, связанный с временными файлами).
7.  Зафиксируйте все шаги в отчёте.

---

## Критерии приёмки (чек-лист)
- [x] Все подпункты задания выполнены.
- [x] Все тома/разделы созданы с корректными размерами и типами ФС.
- [x] Настроено автомонтирование через `/etc/fstab`, `sudo mount -a` без ошибок.
- [x] После перезагрузки точки монтирования активны (проверка `df -hT`).
- [x] Доказательства собраны по стандарту именования (см. ниже).

### Стандарт именования доказательств
- Скрины: `YYYY-MM-DD_1_5_4_stepYY.png`
- Логи: `YYYY-MM-DD_1_5_4_stepYY.log`
- Конфиги: `YYYY-MM-DD_1_5_4_<name>.conf`

---

## Ход работы (таблица журнал)

| Step | Что делал                          | Команды                                                                                                                                                                                              | Где доказательства               | Результат (✓/⚠/✗) |
| ---: | ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------- | :---------------: |
|   01 | <br>Создание LV (2 ГБ)             | sudo lvcreate -L 2G -n lv_test vg_home<br>sudo mkfs.ext4 /dev/vg_home/lv_test                                                                                                                        | ![[2026-04-22_1_5_4_step10.png]] |         ✓         |
|   02 | Монтирование                       | sudo mkdir /mnt/test<br>sudo mount /dev/vg_home/lv_test /mnt/test                                                                                                                                    | ![[2026-04-22_1_5_4_step20.png]] |         ✓         |
|   03 | Заполнение данными                 | sudo cp -r /etc /mnt/test/<br>du -sh /mnt/test/etc                                                                                                                                                   | ![[2026-04-22_1_5_4_step30.png]] |         ✓         |
|   04 | Проверка перед shrink              | df -h /mnt/test                                                                                                                                                                                      | ![[2026-04-22_1_5_4_step40.png]] |         ✓         |
|   05 | Уменьшение и обратное монтирование | sudo umount /mnt/test<br>sudo e2fsck -f /dev/vg_home/lv_test<br>sudo resize2fs /dev/vg_home/lv_test 1500M<br>sudo lvreduce -L 1.5G /dev/vg_home/lv_test<br>sudo mount /dev/vg_home/lv_test /mnt/test | ![[2026-04-22_1_5_4_step50.png]] |         ✓         |
|   06 | Проверка целостности               | diff -r /etc /mnt/test/etc                                                                                                                                                                           | ![[2026-04-22_1_5_4_step60.png]] |         ✓         |

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
Освоила безопасное уменьшение тома LVM с ФС ext4. Главное правило: сначала сжимаем файловую систему (resize2fs), потом блочное устройство (lvreduce).
Убедилась, что операция требует обязательного размонтирования тома и предварительной проверки целостности (e2fsck -f).
Поняла, что XFS не поддерживает уменьшение, поэтому для таких экспериментов нужна только ext4.
Данные после процедуры shrink сохранились полностью, служебные изменения в /etc/lvm подтверждают успешное выполнение операции.

---

## Приложения
- [x] `passport_1_5_4.log - в начале отчёта`
- [x] Логи команд: `YYYY-MM-DD_1_5_4_stepYY.log`
- [x] Скриншоты: `YYYY-MM-DD_1_5_4_stepYY.png`
- [x] Фрагмент `/etc/fstab` (только добавленные строки)
- [x] Итоговые выводы: `lsblk`, `df -hT`, `pvs/vgs/lvs` (если применимо)

---

## Контрольные вопросы / критерии
1.  Почему для XFS невозможно выполнить уменьшение тома? Какие архитектурные особенности это вызывают?
2.  Зачем нужна команда `e2fsck -f` перед уменьшением ФС? Что будет, если её пропустить?
3.  В каком порядке выполняются действия при уменьшении и при увеличении тома? Сравните.
4.  Можно ли уменьшить том, на котором в данный момент находятся открытые файлы?

**Ответы:**
1.  Архитектура XFS не поддерживает алгоритмы безопасного сжатия метаданных. Разработчики не реализовали эту функцию из-за высокого риска необратимой потери данных при сбоях.
2.  Она исправляет ошибки файловой системы перед перемещением блоков данных. Без неё resize2fs может повредить структуру ФС. Утилита отказывается работать без чистой ФС.
3.  
Увеличение: Сначала LV (lvextend), потом ФС (resize2fs).
Уменьшение: Сначала ФС (resize2fs), потом LV (lvreduce).
4.  Нет. Уменьшение ext4 требует обязательного размонтирования (umount). Онлайн-уменьшение не поддерживается.

---

## Использование AI-ассистента
- Какие вопросы задавал:  -
- Коротко что помогло/не помогло:  -
