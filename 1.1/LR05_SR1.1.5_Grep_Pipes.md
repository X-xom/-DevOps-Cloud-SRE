# Отчёт по лабораторной/самостоятельной работе 1.1.5 (LR05)

## Титульный блок

- **Тема:** Практика с `grep` и конвейерами
- **Студент:** Хомяк Мария Александровна
- **Группа/класс:** Case Lab / «Виртуализация»
- **Дата выполнения:** 2026-03-09
- **Преподаватель:** <...>

## Паспорт стенда

Выполните команды и вставьте вывод (копипаст).

```bash
uname -a
cat /etc/os-release
whoami
ip a
df -h
free -h
lsblk
date
systemctl --version || true
```

**Вывод (вставить сюда):**

```text
student@student:~$ uname -a
Linux student 6.8.0-101-generic #101-Ubuntu SMP PREEMPT_DYNAMIC Mon Feb  9 10:15:05 UTC 2026 x86_64 x86_64 x86_64 GNU/Linux


student@student:~$ cat /etc/os-release
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


student@student:~$ whoami
student


student@student:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:96:21:23 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.243/24 metric 100 brd 192.168.1.255 scope global dynamic enp0s3
       valid_lft 73447sec preferred_lft 73447sec
    inet6 fe80::a00:27ff:fe96:2123/64 scope link
       valid_lft forever preferred_lft forever
       
       
student@student:~$ df -h
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              197M  1.1M  196M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv  9.8G  4.5G  4.8G  49% /
tmpfs                              985M     0  985M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
/dev/sda2                          1.8G  104M  1.6G   7% /boot
tmpfs                              197M   12K  197M   1% /run/user/1000


student@student:~$ free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       333Mi       1.4Gi       1.0Mi       344Mi       1.6Gi
Swap:          1.9Gi          0B       1.9Gi


student@student:~$ lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda                         8:0    0   20G  0 disk
├─sda1                      8:1    0    1M  0 part
├─sda2                      8:2    0  1.8G  0 part /boot
└─sda3                      8:3    0 18.2G  0 part
  └─ubuntu--vg-ubuntu--lv 252:0    0   10G  0 lvm  /
sr0                        11:0    1 1024M  0 rom


student@student:~$ date
Mon Mar  9 04:42:47 AM UTC 2026


student@student:~$ systemctl --version || true
systemd 255 (255.4-1ubuntu8.12)
+PAM +AUDIT +SELINUX +APPARMOR +IMA +SMACK +SECCOMP +GCRYPT -GNUTLS +OPENSSL +ACL +BLKID +CURL +ELFUTILS +FIDO2 +IDN2 -IDN +IPTC +KMOD +LIBCRYPTSETUP +LIBFDISK +PCRE2 -PWQUALITY +P11KIT +QRENCODE +TPM2 +BZIP2 +LZ4 +XZ +ZLIB +ZSTD -BPF_FRAMEWORK -XKBCOMMON +UTMP +SYSVINIT default-hierarchy=unified
```

## Цель работы

Научиться эффективно искать информацию в файлах и строить цепочки команд с помощью конвейера.

## Задание (все подпункты)

Ниже — полный перечень подпунктов из задания. Отмечайте выполнение прямо в процессе.

1.  **Подготовка данных:**
    - Создайте файл `inventory.txt` в домашней папке со следующим содержимым (можно скопировать через `nano`):
        ```
        apple,15,red,fruit
        banana,8,yellow,fruit
        car,5,red,vehicle
        grape,25,purple,fruit
        truck,3,blue,vehicle
        apple,7,green,fruit
        bicycle,12,red,vehicle
        banana,10,yellow,fruit
        ```
    - Файл содержит записи о товарах: `название,количество,цвет,категория`.

2.  **Базовый поиск:**
    - Найдите все строки, содержащие "apple". Запишите команду.
    - Найдите все строки, где есть "banana", но покажите только первые 2. (Подсказка: `grep -m 2`).
    - Найдите все строки, **не содержащие** "apple". (Подсказка: `grep -v apple`).
    - Посчитайте, сколько раз встречается слово "vehicle". (Подсказка: `grep -c vehicle`).
    - Найдите все строки, содержащие "red", независимо от регистра (Red, RED). (Подсказка: `grep -i red`).

3.  **Использование конвейера:**
    - Выведите содержимое файла, отсортируйте его по первому столбцу (названию) с помощью команды `sort`, и затем найдите все строки с "apple" в отсортированном списке. Команда: `cat inventory.txt | sort | grep apple`. Посмотрите на результат. Что изменилось?
    - Найдите все фрукты (категория "fruit"), отсортируйте их по цвету (третий столбец) и покажите только первые 3. (Подсказка: `grep fruit inventory.txt | sort -t',' -k3 | head -n 3`). Разберите эту сложную команду по частям.
    - Посчитайте, сколько всего фруктов (категория "fruit") в файле, просуммировав их количество (второй столбец). **Это очень сложное задание!** Используйте `grep`, `cut` или `awk`. Попросите помощи у AI.

4.  **Работа с системными файлами:**
    - Найдите в файле `/etc/passwd` всех пользователей, у которых в качестве командной оболочки (shell) указан `/bin/bash`. *Подсказка: это последнее поле в строке.*
    - С помощью `grep` и `wc -l` посчитайте, сколько пользователей в системе используют `/bin/bash`.

## Критерии приёмки (чек-лист)

- [x] Все подпункты задания выполнены.
- [x] Команды/действия воспроизводимы (есть точные команды и пути).
- [x] Есть **минимум 2 доказательства**: лог/вывод + файл/скрин (см. ниже).
- [x] В разделе «Проблемы и решения» описаны ошибки (если были) и как исправили.

### Стандарт именования доказательств

- Скрины: `YYYY-MM-DD_LR05_stepYY.png`
- Логи: `YYYY-MM-DD_LR05_stepYY.log`
- Конфиги: `YYYY-MM-DD_LR05_<name>.conf`

## Ход работы (таблица журнал)

| Step | Действие/команда                                                                                                                                                                           | Ожидаемый результат                                                                          | Факт/вывод                                                        | Доказательство (файл/скрин/лог)          |
| ---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- | ---------------------------------------- |
|    1 | Прочитать файлы целиком и постранично, выполнить команды:<br>cat /etc/os-release<br>less /etc/os-release<br>head -n 5 /etc/os-release<br>tail -n 5 /etc/os-release                         | Научиться просматривать начало/конец файла и читать постранично                              | Кусок вывода head/tail и запись про q в отчёте LR05               | 05/2026-03-09_LR05_step01.png<br>05/LR05 |
|    2 | Найти строки и построить цепочки команд, с помощью команд:<br>grep "NAME" /etc/os-release<br>grep -c "ID" /etc/os-release<br>ls -la /etc \| grep "conf" \| head -n 5                       | Понять grep и \|, закрепить на примерах                                                      | Вывод команд с grep/pipe вставлен в отчёт LR05                    | 05/LR05                                  |
|    3 | Выполнение Практического занятие 1.1.2, часть 1, выполнить команды:<br>cat ~/inventory.txt<br>grep "apple" ~/inventory.txt<br>grep "vehicle" ~/inventory.txt<br>grep "red" ~/inventory.txt | Найти все слова из inventory.txt.                                                            | Вывод grep-команд в отчёте LR05                                   | 05/LR05                                  |
|    4 | Прочитать большой файл постранично, выполнить команды:<br>sudo ls -lh /var/log \| head -n 30<br>sudo less /var/log/auth.log                                                                | Научиться листать и искать в less                                                            | Запись в отчёт LR05: какие клавиши использовал (/, n, q)          | 05/LR05                                  |
|    5 | Понять, как быстро искать события/ошибки в логах, выполнить команды:<br>sudo grep -i "fail" /var/log/auth.log \| head -n 5<br>sudo grep -i "error" /var/log/syslog \| head -n 5            | Найти интересные строки в логах и объяснить их                                               | Вывод grep (первые строки) + 2–3 предложения вывода в отчёте LR05 | 05/2026-03-09_LR05_step02.png<br>05/LR05 |
|    6 | Найти опции команд в документации, выполнить команды:<br>man grep<br>man less                                                                                                              | Научиться пользоваться man и находить нужные опции                                           | Короткий конспект в LR05 про -i/-n и поиск в less                 | 05/LR05                                  |
|    7 | Сделать СР 1.1.5.                                                                                                                                                                          | Научиться эффективно искать информацию в файлах и строить цепочки команд с помощью конвейера | Вывод ключевых команд (grep/pipe) в отчёте LR05 + inventory.txt   | 05/LR05                                  |

## Проблемы и решения

| Проблема/ошибка | Где возникло (step) | Диагностика (что проверили) | Решение (что сделали) | Доказательство |
| --------------- | ------------------: | --------------------------- | --------------------- | -------------- |
| -               |                     |                             |                       |                |

## Самопроверка (✓/⚠/✗)

| Пункт                                                         | Самооценка (✓/⚠/✗) | Комментарий |
| ------------------------------------------------------------- | :----------------: | ----------- |
| Я выполнил(а) все подпункты задания                           |         ✓          |             |
| Я понимаю, что делает каждая ключевая команда                 |         ✓          |             |
| У меня есть минимум 2 доказательства (лог/вывод + файл/скрин) |         ✓          |             |
| Я могу воспроизвести работу с нуля по своему отчёту           |         ✓          |             |

## Выводы

- Что получилось хорошо: как быстро находить нужное в файлах, навигация в less
- Что было самым сложным: понять pipe
- Что я буду делать иначе в следующий раз: - 

## Приложения

- `...` (перечислите файлы/скрины/логи)
- ![[2026-03-09_LR05_step01.png]]
- ![[2026-03-09_LR05_step02.png]]
