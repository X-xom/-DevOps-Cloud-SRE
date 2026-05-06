# Отчёт по самостоятельной работе № 1.5.6
## Тема: Проектирование и создание структуры для веб-сервера

**Студент:** Хомяк Мария Александровна 
**Группа:** _____________________  
**Дата выполнения:** 27.04.2026
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

**Вывод/лог:** `passport_1_5_6.log` *(или вставка ниже)*

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
       valid_lft 80422sec preferred_lft 80422sec
    inet6 fd17:625c:f037:2:a00:27ff:feab:bc32/64 scope global dynamic mngtmpaddr noprefixroute
       valid_lft 86182sec preferred_lft 14182sec
    inet6 fe80::a00:27ff:feab:bc32/64 scope link
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:a8:61:75 brd ff:ff:ff:ff:ff:ff
    inet 192.168.56.12/24 brd 192.168.56.255 scope global enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fea8:6175/64 scope link
       valid_lft forever preferred_lft forever
4: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    link/ether ee:e5:fd:09:55:b9 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever

Команда: df -h
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              197M  1.2M  196M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv  9.8G  6.0G  3.3G  65% /
tmpfs                              985M     0  985M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
/dev/mapper/vg_home-lv_home        5.9G   24K  5.6G   1% /home/testuser
/dev/sda2                          1.8G  200M  1.5G  13% /boot
tmpfs                              197M   12K  197M   1% /run/user/1000
/dev/mapper/vg_home-lv_data        974M   48K  907M   1% /mnt/data

Команда: free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       413Mi       490Mi       1.2Mi       1.2Gi       1.5Gi
Swap:          1.8Gi          0B       1.8Gi

Команда: lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda                         8:0    0   20G  0 disk
├─sda1                      8:1    0    1M  0 part
├─sda2                      8:2    0  1.8G  0 part /boot
└─sda3                      8:3    0 18.2G  0 part
  └─ubuntu--vg-ubuntu--lv 252:2    0   10G  0 lvm  /
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
  └─vg_home-lv_data       252:3    0    1G  0 lvm  /mnt/data
sr0                        11:0    1 1024M  0 rom

Команда: date
Tue Apr 28 04:55:06 AM UTC 2026

Команда: systemctl --version
systemd 255 (255.4-1ubuntu8.15)
+PAM +AUDIT +SELINUX +APPARMOR +IMA +SMACK +SECCOMP +GCRYPT -GNUTLS +OPENSSL +ACL +BLKID +CURL +ELFUTILS +FIDO2 +IDN2 -IDN +IPTC +KMOD +LIBCRYPTSETUP +LIBFDISK +PCRE2 -PWQUALITY +P11KIT +QRENCODE +TPM2 +BZIP2 +LZ4 +XZ +ZLIB +ZSTD -BPF_FRAMEWORK -XKBCOMMON +UTMP +SYSVINIT default-hierarchy=unified
```

---

## Цель работы
Спроектировать и реализовать отказоустойчивую структуру хранения данных для веб-сервера с использованием LVM. Разделить корневые файлы, логи и пользовательские данные на независимые логические тома с разными файловыми системами (ext4 и XFS) для оптимизации производительности и надежности.

---

## Задание (все подпункты)
Вы — системный администратор. Вам нужно подготовить сервер для размещения веб-сайта (nginx + PHP + база данных на том же сервере для упрощения). В вашем распоряжении **два диска по 5 ГБ**.

Спроектируйте и создайте структуру LVM, которая будет удовлетворять следующим требованиям:

-   Корневые файлы веб-сервера (обычно `/var/www`) должны находиться на отдельном томе. Размер — **1 ГБ**, ФС — **ext4**.
-   Логи веб-сервера и системы (предположим, они будут в `/var/log/www`) должны быть на отдельном томе. Размер — **2 ГБ**, ФС — **XFS** (так как логи могут быть большими, и важно не потерять записи при сбое).
-   Данные сайта (пользовательский контент, загрузки) должны быть на отдельном томе. Используйте **всё оставшееся пространство**, ФС — **ext4**.
-   Все тома должны быть созданы с использованием LVM.
-   Необходимо настроить автоматическое монтирование при загрузке.
-   Имена томов и группы томов выберите осмысленно (например, `vg_web`, `lv_www_root`, `lv_www_logs`, `lv_www_data`).

**Порядок действий (рекомендуемый):**
1.  Создайте на двух дисках разделы LVM (тип `8e`).
2.  Создайте PV, VG.
3.  Создайте LV с указанными размерами.
4.  Отформатируйте их в соответствующие ФС.
5.  Создайте точки монтирования (директории) и примонтируйте тома.
6.  Пропишите монтирование в `/etc/fstab`.
7.  Проверьте, что после перезагрузки всё работает.

---

## Критерии приёмки (чек-лист)
- [x] Все подпункты задания выполнены.
- [x] Все тома/разделы созданы с корректными размерами и типами ФС.
- [x] Настроено автомонтирование через `/etc/fstab`, `sudo mount -a` без ошибок.
- [x] После перезагрузки точки монтирования активны (проверка `df -hT`).
- [x] Доказательства собраны по стандарту именования (см. ниже).

### Стандарт именования доказательств
- Скрины: `YYYY-MM-DD_1_5_6_stepYY.png`
- Логи: `YYYY-MM-DD_1_5_6_stepYY.log`
- Конфиги: `YYYY-MM-DD_1_5_6_<name>.conf`

---

## Ход работы (таблица журнал)

| Step | Что делал             | Команды                                                                                                                                                                                       | Где доказательства                  | Результат (✓/⚠/✗) |
| ---: | --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------- | :---------------: |
|   01 | <br>Подготовка дисков | <br>Добавлены sde, sdf (5 ГБ).<br>sudo fdisk /dev/sde (type 8e)<br>sudo fdisk /dev/sdf (type 8e)                                                                                              | 1.5/156/2026-04-22_1_5_6_step10.png |         ✓         |
|   02 | Создание PV и VG      | <br>sudo pvcreate /dev/sde1 /dev/sdf1<br>sudo vgcreate vg_web /dev/sde1 /dev/sdf1                                                                                                             | 1.5/156/2026-04-22_1_5_6_step20.png |         ✓         |
|   03 | Создание LV           | sudo lvcreate -L 1G -n lv_www_root vg_web<br>sudo lvcreate -L 2G -n lv_www_logs vg_web<br>sudo lvcreate -l 100%FREE -n lv_www_data vg_web<br>sudo lvs                                         | 1.5/156/2026-04-22_1_5_6_step30.png |         ✓         |
|   04 | Форматирование ФС     | sudo mkfs.ext4 /dev/vg_web/lv_www_root<br>sudo mkfs.xfs /dev/vg_web/lv_www_logs<br>sudo mkfs.ext4 /dev/vg_web/lv_www_data                                                                     | 1.5/156/2026-04-22_1_5_6_step40.png |         ✓         |
|   05 | Монтирование          | sudo mkdir -p /var/www /var/log/www<br>sudo mount ... lv_www_root /var/www<br>sudo mount ... lv_www_logs /var/log/www<br>sudo mkdir /var/www/data<br>sudo mount ... lv_www_data /var/www/data | 1.5/156/2026-04-22_1_5_6_step50.png |         ✓         |
|   06 | Настройка fstab       | sudo blkid \| grep vg_web<br>Добавление UUID в /etc/fstab<br>sudo mount -a                                                                                                                    | 1.5/156/2026-04-22_1_5_6_step60.png |         ✓         |
|   07 | Проверка работы       | sudo reboot<br>df -hT \| grep vg_web<br>sudo lsblk                                                                                                                                            | 1.5/156/2026-04-22_1_5_6_step70.png |         ✓         |

---

## Проблемы и решения
> Формат: **Симптом → Диагностика (команда) → Причина → Решение → Проверка**

Симптом: Ошибка mount: /var/www/data: mount point does not exist при попытке примонтировать том с данными.
Диагностика: Проверила наличие директории командой ls -ld /var/www/data.
Причина: Я прописала путь монтирования в /etc/fstab и пыталась монтировать вручную, но забыла предварительно создать саму директорию-контейнер.
Решение: Создала недостающую директорию командой sudo mkdir -p /var/www/data.
Проверка: Повторная команда sudo mount /dev/vg_web/lv_www_data /var/www/data выполнилась успешно, том доступен.  

---

## Самопроверка (✓/⚠/✗)
- **Самооценка:** ✓
- **Что проверить повторно, если ⚠/✗:** _______________________________________

---

## Выводы
Спроектировала модульную структуру для веб-сервера, разделив данные, логи и системные файлы на независимые LV.
Обоснованно выбрала ФС: XFS для логов (скорость записи), ext4 для данных (надежность и снапшоты).
Освоила использование -l 100%FREE для занятия всего остатка места в VG без ручных расчетов.
Настроила автозагрузку через UUID, что гарантирует стабильность при изменении порядка дисков.


---

## Приложения
- [x] `passport_1_5_6.log - в начале отчёта`
- [x] Логи команд: `YYYY-MM-DD_1_5_6_stepYY.log`
- [x] Скриншоты: `YYYY-MM-DD_1_5_6_stepYY.png`
- [x] Фрагмент `/etc/fstab` (только добавленные строки)
- [x] Итоговые выводы: `lsblk`, `df -hT`, `pvs/vgs/lvs` (если применимо)

---

## Контрольные вопросы / критерии
1.  Почему для логов была выбрана XFS, а для данных — ext4? Обоснуйте.
2.  Сколько свободного места осталось в VG после выполнения задания? Как вы можете его использовать в будущем?
3.  Какие команды вы использовали для просмотра итоговой структуры?
4.  Как бы вы изменили структуру, если бы дисков было не два, а один, но размером 10 ГБ?

**Ответы:**
1.  XFS быстрее работает с большими файлами и параллельной записью (идеально для логов). Ext4 надежнее для мелких файлов и поддерживает снапшоты (важно для бэкапа сайта).
2.  Места не осталось (занято 100%FREE). Для расширения нужно добавить новый физический диск в VG (vgextend) и затем расширить нужный LV.
3. lsblk (дерево устройств), df -hT (точки монтирования и типы ФС), sudo lvs и sudo vgs (параметры LVM).
4.  Технически команды те же (один PV вместо двух). Но теряется отказоустойчивость: поломка единственного диска уничтожит все данные сразу.
5.  

---

## Использование AI-ассистента
- Какие вопросы задавал: как решить проблему с sudo mount /dev/vg_web/lv_www_data /var/www/data
- Коротко что помогло/не помогло:  рассказал какие команды нужно использовать что б решить проблему
