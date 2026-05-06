# Отчёт по самостоятельной работе № 1.5.5
## Тема: Отработка создания и использования снапшотов

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

**Вывод/лог:** `passport_1_5_5.log` *(или вставка ниже)*

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
       valid_lft 85320sec preferred_lft 85320sec
    inet6 fd17:625c:f037:2:a00:27ff:feab:bc32/64 scope global dynamic mngtmpaddr noprefixroute
       valid_lft 86344sec preferred_lft 14344sec
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

Команда: free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       370Mi       1.3Gi       1.2Mi       364Mi       1.6Gi
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
  └─vg_home-lv_test       252:1    0  1.5G  0 lvm
sr0                        11:0    1 1024M  0 rom

Команда: date
Tue Apr 27 03:33:28 AM UTC 2026

Команда: systemctl --version
systemd 255 (255.4-1ubuntu8.15)
+PAM +AUDIT +SELINUX +APPARMOR +IMA +SMACK +SECCOMP +GCRYPT -GNUTLS +OPENSSL +ACL +BLKID +CURL +ELFUTILS +FIDO2 +IDN2 -IDN +IPTC +KMOD +LIBCRYPTSETUP +LIBFDISK +PCRE2 -PWQUALITY +P11KIT +QRENCODE +TPM2 +BZIP2 +LZ4 +XZ +ZLIB +ZSTD -BPF_FRAMEWORK -XKBCOMMON +UTMP +SYSVINIT default-hierarchy=unified
```

---

## Цель работы

Освоить механизм создания мгновенных снимков (снапшотов) логических томов LVM. Научиться использовать снапшоты для двух целей: быстрого отката изменений через слияние (merge) и создания консистентных резервных копий без остановки сервисов.

---

## Задание (все подпункты)
1.  На любом существующем томе (или создайте новый небольшой LV, например, 1 ГБ) создайте директорию `project` и положите туда несколько важных (тестовых) файлов. Например:
    ```bash
    sudo mkdir /mnt/data/project
    for i in {1..5}; do echo "data $i" | sudo tee /mnt/data/project/file$i.txt; done
    ```
2.  Создайте **снапшот** этого тома размером, например, 300 МБ (имя снапшота `lv_project_snap`).
3.  **Сценарий 1: Восстановление через слияние (merge)**
    - Удалите все файлы из директории `project` на оригинальном томе.
    - Убедитесь, что снапшот содержит данные (примонтируйте его в режиме ro и проверьте).
    - Размонтируйте оригинальный том и снапшот.
    - Выполните слияние снапшота с оригиналом (`lvconvert --merge`).
    - Примонтируйте оригинал обратно и убедитесь, что файлы восстановились.
4.  **Сценарий 2: Резервное копирование из снапшота**
    - Снова создайте снапшот (или используйте новый).
    - Смонтируйте снапшот.
    - Создайте резервную копию (тарболл) данных из снапшота в домашнюю директорию пользователя.
    - Размонтируйте и удалите снапшот.
    - Убедитесь, что архив создан и содержит данные.
5.  Опишите оба сценария в отчёте.

---

## Критерии приёмки (чек-лист)
- [x] Все подпункты задания выполнены.
- [x] Все тома/разделы созданы с корректными размерами и типами ФС.
- [x] Настроено автомонтирование через `/etc/fstab`, `sudo mount -a` без ошибок.
- [x] После перезагрузки точки монтирования активны (проверка `df -hT`).
- [x] Доказательства собраны по стандарту именования (см. ниже).

### Стандарт именования доказательств
- Скрины: `YYYY-MM-DD_1_5_5_stepYY.png`
- Логи: `YYYY-MM-DD_1_5_5_stepYY.log`
- Конфиги: `YYYY-MM-DD_1_5_5_<name>.conf`

---

## Ход работы (таблица журнал)

| Step | Что делал                    | Команды                                                                                                                                                                                                               | Где доказательства                  | Результат (✓/⚠/✗) |
| ---: | ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------- | :---------------: |
|   01 | Подготовка данных            | sudo lvcreate -L 1G -n lv_data vg_home<br>sudo mkfs.ext4 /dev/vg_home/lv_data<br>sudo mount /dev/vg_home/lv_data /mnt/data<br>sudo mkdir /mnt/data/project<br>for i in {1..5}; do echo "data $i" \|                   | 1.5/155/2026-04-22_1_5_5_step10.png |         ✓         |
|   02 | Создание снапшота            | sudo lvcreate -L 300M -s -n lv_project_snap /dev/vg_home/lv_data                                                                                                                                                      | 1.5/155/2026-04-22_1_5_5_step20.png |         ✓         |
|   03 | Имитация сбоя (удаление)     | sudo rm -rf /mnt/data/project/*                                                                                                                                                                                       | 1.5/155/2026-04-22_1_5_5_step30.png |         ✓         |
|   04 | Проверка снапшота            | sudo mkdir /mnt/snap<br>sudo mount -o ro /dev/vg_home/lv_project_snap /mnt/snap<br>ls /mnt/snap/project                                                                                                               | 1.5/155/2026-04-22_1_5_5_step40.png |         ✓         |
|   05 | Слияние (Merge)              | sudo umount /mnt/data<br>sudo umount /mnt/snap<br>sudo lvconvert --merge /dev/vg_home/lv_project_snap<br>sudo mount /dev/vg_home/lv_data /mnt/data<br>ls /mnt/data/project                                            | 1.5/155/2026-04-22_1_5_5_step50.png |         ✓         |
|   06 | Бекап из снапшота о проверка | sudo lvcreate -L 300M -s -n lv_backup_snap /dev/vg_home/lv_data<br>sudo mount /dev/vg_home/lv_backup_snap /mnt/snap<br>sudo tar -czf ~/project_backup.tar.gz -C /mnt/snap project<br>tar -tzf ~/project_backup.tar.gz | 1.5/155/2026-04-22_1_5_5_step60.png |         ✓         |


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
(2–5 пунктов: что получилось, что узнал, на что обратить внимание в будущем)

---

## Приложения
- [x] `passport_1_5_5.log - в начале отчёта`
- [x] Логи команд: `YYYY-MM-DD_1_5_5_stepYY.log`
- [x] Скриншоты: `YYYY-MM-DD_1_5_5_stepYY.png`
- [x] Фрагмент `/etc/fstab` (только добавленные строки)
- [x] Итоговые выводы: `lsblk`, `df -hT`, `pvs/vgs/lvs` (если применимо)

---

## Контрольные вопросы / критерии
1.  Объясните технологию Copy-on-Write (COW) на примере работы снапшота.
2.  Почему размер снапшота (300 МБ) может стать недостаточным, если на оригинальном томе происходит много изменений?
3.  В чем преимущество создания бекапа из снапшота перед бекапом напрямую с работающего тома?
4.  Что произойдет со снапшотом, если место, выделенное для него, закончится?

**Ответы:**
1.  При создании снапшота он не копирует данные, а лишь ссылается на блоки оригинала. Когда вы изменяете файл на оригинальном томе, LVM сначала копирует старую версию блока в область снапшота (Copy-on-Write), и только потом перезаписывает блок на оригинале. Это позволяет снапшоту «помнить» состояние данных на момент своего создания.
2.  Снапшот хранит только измененные блоки оригинала. Если на основном томе запишется данных больше, чем объем снапшота (300 МБ), ему некуда будет сохранять старые версии блоков. Снапшот переполнится, станет невалидным (invalid) и будет автоматически отключен системой.
3.  Бекап с живого тома может привести к «несогласованным» данным (например, база данных может быть записана частично). Снапшот фиксирует состояние на мгновение. Читая данные из снапшота для архивации, мы получаем статичную, консистентную картину файловой системы, как если бы том был отмонтирован, но без остановки сервисов.
	1.  Снапшот перейдет в статус INVALID и будет деактивирован. Восстановить данные из такого снапшота будет невозможно, его придется удалять (lvremove).

---

## Использование AI-ассистента
- Какие вопросы задавал:  -
- Коротко что помогло/не помогло:  
