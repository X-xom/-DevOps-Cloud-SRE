# Отчёт по лабораторной/самостоятельной работе 1.1.3 (LR03)

## Титульный блок

- **Тема:** Создание и управление файлами
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
       valid_lft 85618sec preferred_lft 85618sec
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
Mem:           1.9Gi       352Mi       1.4Gi       1.0Mi       328Mi       1.6Gi
Swap:          1.9Gi          0B       1.9Gi


student@student:~$ lsblk
NAME                MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda                   8:0    0   20G  0 disk
├─sda1                8:1    0    1M  0 part
├─sda2                8:2    0  1.8G  0 part /boot
└─sda3                8:3    0 18.2G  0 part
  └─ubuntu--vg-ubuntu--lv
                    252:0    0   10G  0 lvm  /
sr0                  11:0    1 1024M  0 rom


student@student:~$ date
Mon Mar  9 01:19:55 AM UTC 2026


student@student:~$ systemctl --version || true
systemd 255 (255.4-1ubuntu8.12)
+PAM +AUDIT +SELINUX +APPARMOR +IMA +SMACK +SECCOMP +GCRYPT -GNUTLS +OPENSSL +ACL +BLKID +CURL +ELFUTILS +FIDO2 +IDN2 -IDN +IPTC +KMOD +LIBCRYPTSETUP +LIBFDISK +PCRE2 -PWQUALITY +P11KIT +QRENCODE +TPM2 +BZIP2 +LZ4 +XZ +ZLIB +ZSTD -BPF_FRAMEWORK -XKBCOMMON +UTMP +SYSVINIT default-hierarchy=unified
```

## Цель работы

Отработать команды создания, копирования, перемещения и удаления файлов и директорий.

## Задание (все подпункты)

Ниже — полный перечень подпунктов из задания. Отмечайте выполнение прямо в процессе.

1.  Создайте в своей домашней папке вложенную структуру каталогов:
    `documents/work/reports/2025/`
2.  Перейдите в папку `2025`.
3.  Создайте файл `january_report.txt`.
4.  Наполните его несколькими строками текста. Можно использовать `echo`:
    ```bash
    echo "Отчет за январь." > january_report.txt
    echo "Продажи: 1 000 000 руб." >> january_report.txt
    echo "Прибыль: 200 000 руб." >> january_report.txt
    ```
    Обратите внимание: `>` перезаписывает файл, `>>` добавляет в конец.
5.  Создайте точную копию этого файла с именем `february_report_draft.txt` в той же папке.
6.  Переместите файл `february_report_draft.txt` на уровень выше (в папку `reports`). Используйте относительные пути.
7.  Переименуйте `january_report.txt` в `march_report.txt`.
8.  Создайте в папке `2025` пустой файл `temp.txt`.
9.  Скопируйте файл `march_report.txt` в папку `documents` (корень вашей структуры) под именем `report_archive.txt`.
10. Создайте в папке `work` новую папку `archive`.
11. Переместите все файлы с расширением `.txt` из папки `work` (и всех её подпапок) в папку `work/archive`. **Это сложное задание. Подумайте, как его выполнить. Подсказка: может пригодиться команда `find`.**
12. Удалите папку `work/reports` (она должна стать пустой после перемещения файлов).
13. Удалите папку `work/archive` (она не пустая). Используйте правильную команду.

## Критерии приёмки (чек-лист)

- [x] Все подпункты задания выполнены.
- [x] Команды/действия воспроизводимы (есть точные команды и пути).
- [x] Есть **минимум 2 доказательства**: лог/вывод + файл/скрин (см. ниже).
- [x] В разделе «Проблемы и решения» описаны ошибки (если были) и как исправили.

### Стандарт именования доказательств

- Скрины: `YYYY-MM-DD_LR03_stepYY.png`
- Логи: `YYYY-MM-DD_LR03_stepYY.log`
- Конфиги: `YYYY-MM-DD_LR03_<name>.conf`

## Ход работы (таблица журнал)

| Step | Действие/команда                                                                                                                                                                                                                                                                                                                                                       | Ожидаемый результат                                   | Факт/вывод                         | Доказательство (файл/скрин/лог)                                |
| ---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- | ---------------------------------- | -------------------------------------------------------------- |
|    1 | Прочтение Лекции 1.1.3., ответить на вопросы и сделать конспект                                                                                                                                                                                                                                                                                                        | Ответы на вопросы "Проверь себя" и конспект в LR03    | Файл с ответами и конспект         | 03/LR03                                                        |
|    2 | Создать в домашней папке структуру, выполнить команды:<br>cd ~<br>mkdir -p documents/work/reports/2025<br>cd documents/work/reports/2025<br>pwd<br>ls -la                                                                                                                                                                                                              | Созданная структура, проверка pwd                     | Вывод pwd и ls -la                 | 03/2026-03-09_LR03_step01.png<br>03/2026-03-09_LR03_step02.png |
|    3 | Отработать создание файла и добавление строк через echo с помощью команд:<br>touch january_report.txt<br>echo "January report" > january_report.txt<br>echo "Line 1" >> january_report.txt<br>echo "Line 2" >> january_report.txt<br>cat january_report.txt                                                                                                            | Файл создан и содержит строки                         | January report<br>Line 1<br>Line 2 | 03/2026-03-09_LR03_step03.png                                  |
|    4 | ***Начиная с этого момента, задания в md и docx расходятся, я выполняла согласно заданиям в docx файле.***<br>Научиться управлять файлами с помощью cp и mv, выполнить команды:<br>mkdir -p ~/backup<br>cp january_report.txt ~/backup/january_report_copy.txt<br>mv ~/backup/january_report_copy.txt ~/backup/january_report_ARCHIVE.txt<br>ls -la<br>ls -la ~/backup | Файл скопирован и переименован, видно результат в ls. | Вывод ls -la                       | 03/2026-03-09_LR03_step04.png                                  |
|    5 | Научиться удалять файлы аккуратно с помощью команд:<br>touch temp1.txt temp2.txt<br>ls -la<br>rm temp1.txt temp2.txt<br>ls -la                                                                                                                                                                                                                                         | Временные файлы удалены, остальные файлы целы         | Вывод ls -la до и после rm         | 03/2026-03-09_LR03_step05.png<br>03/2026-03-09_LR03_step06.png |

## Проблемы и решения

| Проблема/ошибка | Где возникло (step) | Диагностика (что проверили) | Решение (что сделали) | Доказательство |
| --------------- | ------------------: | --------------------------- | --------------------- | -------------- |
| -               |                     |                             |                       |                |

## Самопроверка (✓/⚠/✗)

| Пункт                                                         | Самооценка (✓/⚠/✗) | Комментарий         |
| ------------------------------------------------------------- | :----------------: | ------------------- |
| Я выполнил(а) все подпункты задания                           |         ✓          | Согласно файлу docx |
| Я понимаю, что делает каждая ключевая команда                 |         ✓          |                     |
| У меня есть минимум 2 доказательства (лог/вывод + файл/скрин) |         ✓          |                     |
| Я могу воспроизвести работу с нуля по своему отчёту           |         ✓          |                     |

## Выводы

- Что получилось хорошо: Разобраться во взаимодействии с файлами(удаление, перемещение)
- Что было самым сложным: Понять какому файлу следовать, md или docx(я выбрала docx)
- Что я буду делать иначе в следующий раз: -

## Приложения

- `...` (перечислите файлы/скрины/логи)
- ![[2026-03-09_LR03_step01.png]]
- ![[2026-03-09_LR03_step02.png]]
- ![[2026-03-09_LR03_step03.png]]
- ![[2026-03-09_LR03_step04.png]]
- ![[2026-03-09_LR03_step05.png]]
- ![[2026-03-09_LR03_step06.png]]
