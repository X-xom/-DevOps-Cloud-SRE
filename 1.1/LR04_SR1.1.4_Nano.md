# Отчёт по лабораторной/самостоятельной работе 1.1.4 (LR04)

## Титульный блок

- **Тема:** Знакомство с текстовым редактором (nano)
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
student@student:~/documents/work/reports/2025$ uname -a
Linux student 6.8.0-101-generic #101-Ubuntu SMP PREEMPT_DYNAMIC Mon Feb  9 10:15:05 UTC 2026 x86_64 x86_64 x86_64 GNU/Linux


student@student:~/documents/work/reports/2025$ cat /etc/os-release
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


student@student:~/documents/work/reports/2025$ whoami
student


student@student:~/documents/work/reports/2025$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:96:21:23 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.243/24 metric 100 brd 192.168.1.255 scope global dynamic enp0s3
       valid_lft 79971sec preferred_lft 79971sec
    inet6 fe80::a00:27ff:fe96:2123/64 scope link
       valid_lft forever preferred_lft forever
       
       
student@student:~/documents/work/reports/2025$ df -h
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              197M  1.1M  196M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv  9.8G  4.5G  4.8G  49% /
tmpfs                              985M     0  985M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
/dev/sda2                          1.8G  104M  1.6G   7% /boot
tmpfs                              197M   12K  197M   1% /run/user/1000


student@student:~/documents/work/reports/2025$ free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       350Mi       1.4Gi       1.0Mi       332Mi       1.6Gi
Swap:          1.9Gi          0B       1.9Gi


student@student:~/documents/work/reports/2025$ lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda                         8:0    0   20G  0 disk
├─sda1                      8:1    0    1M  0 part
├─sda2                      8:2    0  1.8G  0 part /boot
└─sda3                      8:3    0 18.2G  0 part
  └─ubuntu--vg-ubuntu--lv 252:0    0   10G  0 lvm  /
sr0                        11:0    1 1024M  0 rom


student@student:~/documents/work/reports/2025$ date
Mon Mar  9 02:54:03 AM UTC 2026


student@student:~/documents/work/reports/2025$ systemctl --version || true
systemd 255 (255.4-1ubuntu8.12)
+PAM +AUDIT +SELINUX +APPARMOR +IMA +SMACK +SECCOMP +GCRYPT -GNUTLS +OPENSSL +ACL +BLKID +CURL +ELFUTILS +FIDO2 +IDN2 -IDN +IPTC +KMOD +LIBCRYPTSETUP +LIBFDISK +PCRE2 -PWQUALITY +P11KIT +QRENCODE +TPM2 +BZIP2 +LZ4 +XZ +ZLIB +ZSTD -BPF_FRAMEWORK -XKBCOMMON +UTMP +SYSVINIT default-hierarchy=unified
```

## Цель работы

Научиться создавать и редактировать текстовые файлы прямо в терминале с помощью редактора `nano`.

## Задание (все подпункты)

Ниже — полный перечень подпунктов из задания. Отмечайте выполнение прямо в процессе.

1.  **Изучение теории:**
    - Откройте `man nano` и бегло просмотрите раздел. Найдите список основных сочетаний клавиш.
    - Запомните (или запишите) основные комбинации:
        - `Ctrl+O` — сохранить файл (WriteOut).
        - `Ctrl+X` — выйти (eXit).
        - `Ctrl+K` — вырезать текущую строку (Kut).
        - `Ctrl+U` — вставить (Uncut).
        - `Ctrl+W` — поиск (Where is).
        - `Ctrl+\` — замена (Replace).
        - `Alt+N` (или `Alt+#`) — показать номера строк.

2.  **Создание и редактирование:**
    - Создайте файл `todo.txt` в своей домашней папке: `nano todo.txt`
    - Внесите в него список из 5 дел на завтра. Каждое дело — с новой строки.
    - Сохраните файл (`Ctrl+O`) и выйдите (`Ctrl+X`).
    - Просмотрите содержимое файла с помощью `cat`.
    - Снова откройте файл `nano todo.txt`.
    - Добавьте в самый конец файла шестое дело.
    - Удалите третью строку (дело №3). *Подсказка: поставьте курсор на эту строку и нажмите `Ctrl+K`.*
    - Вставьте обратно то, что удалили, в конец файла (`Ctrl+U`).
    - Найдите слово (например, "купить") с помощью `Ctrl+W`.
    - Попробуйте заменить одно слово на другое с помощью `Ctrl+\`. Следуйте инструкциям внизу экрана.
    - Сохраните изменения и выйдите.

3.  **Практика с номерами строк:**
    - Откройте любой системный файл, например, `/etc/hosts`: `sudo nano /etc/hosts` (`sudo` нужен для редактирования системных файлов).
    - Включите отображение номеров строк (если ещё не включено).
    - Перейдите к строке номер 5. *В `nano` нет прямого перехода по номеру, но можно посчитать. Это упражнение на внимательность.*

4.  **Создание скрипта (пропедевтика):**
    - Создайте файл `hello.sh` в домашней папке.
    - Напишите в нём следующие строки:
        ```bash
        #!/bin/bash
        # Это мой первый скрипт
        echo "Привет, мир!"
        echo "Я учусь работать в Linux!"
        ```
    - Сохраните файл.
    - Сделайте его исполняемым: `chmod +x hello.sh` (команда `chmod` будет изучаться позже, просто выполните).
    - Запустите скрипт: `./hello.sh`. Он должен вывести две строки.

## Критерии приёмки (чек-лист)

- [x] Все подпункты задания выполнены.
- [x] Команды/действия воспроизводимы (есть точные команды и пути).
- [x] Есть **минимум 2 доказательства**: лог/вывод + файл/скрин (см. ниже).
- [x] В разделе «Проблемы и решения» описаны ошибки (если были) и как исправили.

### Стандарт именования доказательств

- Скрины: `YYYY-MM-DD_LR04_stepYY.png`
- Логи: `YYYY-MM-DD_LR04_stepYY.log`
- Конфиги: `YYYY-MM-DD_LR04_<name>.conf`

## Ход работы (таблица журнал)

| Step | Действие/команда                                                                                                                    | Ожидаемый результат                                            | Факт/вывод                                 | Доказательство (файл/скрин/лог)                                |
| ---: | ----------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- | ------------------------------------------ | -------------------------------------------------------------- |
|    1 | Запомнить базовые клавиши nano, выполнить команду:<br>man nano                                                                      | Выучить базовые клавиши nano                                   | Список клавиш записанный в отчёт LR04      | 04/LR04                                                        |
|    2 | Записать в файле несколько строк и сохранить, выполнить команды:<br>cd ~<br>nano notes_nano.txt<br>cat notes_nano.txt               | Созданный файл notes_nano.txt, с содержанием введённого текста | Вывод команды cat notes_nano.txt           | 04/2026-03-09_LR04_step01.png                                  |
|    3 | Создать и запустить скрипт при помощи команд:<br>touch hello.sh<br>nano hello.sh<br>chmod +x hello.sh<br>./hello.sh<br>cat hello.sh | Скрипт запускается и выдаёт ожидаемый результат                | Вывод cat скрипта и вывод запуска ./скрипт | 04/2026-03-09_LR04_step02.png<br>04/2026-03-09_LR04_step03.png |
|    4 | Быстро находить и править нужное место в файле при помощи Ctrl+W, выполнить команды:<br>nano notes_nano.txt<br>cat notes_nano.txt   | Научиться искать и править текст в nano                        | Копия вывода cat после изменений           | 04/2026-03-09_LR04_step04.png                                  |

## Проблемы и решения

| Проблема/ошибка | Где возникло (step) | Диагностика (что проверили) | Решение (что сделали) | Доказательство |
| --------------- | ------------------: | --------------------------- | --------------------- | -------------- |
| -               |                     |                             |                       |                |

## Самопроверка (✓/⚠/✗)

| Пункт                                                         | Самооценка (✓/⚠/✗) | Комментарий                                                                    |
| ------------------------------------------------------------- | :----------------: | ------------------------------------------------------------------------------ |
| Я выполнил(а) все подпункты задания                           |         ✓          | Некоторые пункты в md и docx файле различались(я выбрала делать по docx файлу) |
| Я понимаю, что делает каждая ключевая команда                 |         ✓          |                                                                                |
| У меня есть минимум 2 доказательства (лог/вывод + файл/скрин) |         ✓          |                                                                                |
| Я могу воспроизвести работу с нуля по своему отчёту           |         ✓          |                                                                                |

## Выводы

- Что получилось хорошо: работать в nano, запомнила быстрые команды( сочетания клавиш) для управления там.
- Что было самым сложным: -
- Что я буду делать иначе в следующий раз: -

## Приложения

- `...` (перечислите файлы/скрины/логи)
- ![[2026-03-09_LR04_step01.png]]
- ![[2026-03-09_LR04_step02.png]]
- ![[2026-03-09_LR04_step03.png]]
- ![[2026-03-09_LR04_step04.png]]