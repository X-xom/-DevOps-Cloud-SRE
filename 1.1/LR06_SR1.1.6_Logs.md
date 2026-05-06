# Отчёт по лабораторной/самостоятельной работе 1.1.6 (LR06)

## Титульный блок

- **Тема:** Анализ системных логов
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
       valid_lft 86279sec preferred_lft 86279sec
    inet6 fe80::a00:27ff:fe96:2123/64 scope link
       valid_lft forever preferred_lft forever
       
       
student@student:~$ df -h
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              197M  1.1M  196M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv  9.8G  4.6G  4.8G  49% /
tmpfs                              985M     0  985M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
/dev/sda2                          1.8G  104M  1.6G   7% /boot
tmpfs                              197M   12K  197M   1% /run/user/1000


student@student:~$ free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       316Mi       1.5Gi       1.0Mi       264Mi       1.6Gi
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
Mon Mar  9 08:02:34 PM UTC 2026


student@student:~$ systemctl --version || true
systemd 255 (255.4-1ubuntu8.12)
+PAM +AUDIT +SELINUX +APPARMOR +IMA +SMACK +SECCOMP +GCRYPT -GNUTLS +OPENSSL +ACL +BLKID +CURL +ELFUTILS +FIDO2 +IDN2 -IDN +IPTC +KMOD +LIBCRYPTSETUP +LIBFDISK +PCRE2 -PWQUALITY +P11KIT +QRENCODE +TPM2 +BZIP2 +LZ4 +XZ +ZLIB +ZSTD -BPF_FRAMEWORK -XKBCOMMON +UTMP +SYSVINIT default-hierarchy=unified
```

## Цель работы

Научиться извлекать полезную информацию из системных логов для диагностики событий.

## Задание (все подпункты)

Ниже — полный перечень подпунктов из задания. Отмечайте выполнение прямо в процессе.

1.  **Подготовка:**
    - Перейдите в каталог `/var/log`.
    - Изучите список файлов логов с помощью `ls -lh`. Обратите внимание на размеры файлов и даты их последнего изменения.

2.  **Анализ лога аутентификации:**
    - Найдите файл, отвечающий за логирование событий входа в систему. Обычно это `auth.log` (Ubuntu/Debian) или `secure` (CentOS/RHEL). Далее будем называть его `auth.log`.
    - Просмотрите последние 20 строк этого файла с помощью `tail -n 20`.
    - Найдите все строки, связанные с процессом SSH (ключевое слово "sshd").
    - Найдите все неудачные попытки входа (ключевая фраза "Failed password"). Запишите одну из таких строк и попробуйте понять, что в ней написано (время, с какого IP, под каким пользователем).
    - Найдите все успешные входы (ключевая фраза "Accepted password").

3.  **Мониторинг в реальном времени:**
    - Откройте **два** окна терминала и подключитесь к своей ВМ в обоих (или используйте два разных подключения, если работаете по SSH).
    - В первом окне выполните команду: `sudo tail -f /var/log/auth.log`.
    - Во втором окне попробуйте подключиться к этой же ВМ по SSH ещё раз (самому к себе) или просто выполните `sudo -i` (переключитесь на root), а затем `exit`.
    - Наблюдайте, как во первом окне появляются новые записи в реальном времени.
    - Прервите просмотр в первом окне (`Ctrl+C`).

4.  **Расследование инцидента:**
    - Используя `grep` и `less`, найдите в логе события, которые происходили в последний час. *Подсказка: обратите внимание на формат времени в логах. Обычно это "Месяц День ЧЧ:ММ:СС".*
    - Попробуйте найти какую-либо необычную активность или ошибки.

## Критерии приёмки (чек-лист)

- [x] Все подпункты задания выполнены.
- [x] Команды/действия воспроизводимы (есть точные команды и пути).
- [x] Есть **минимум 2 доказательства**: лог/вывод + файл/скрин (см. ниже).
- [x] В разделе «Проблемы и решения» описаны ошибки (если были) и как исправили.

### Стандарт именования доказательств

- Скрины: `YYYY-MM-DD_LR06_stepYY.png`
- Логи: `YYYY-MM-DD_LR06_stepYY.log`
- Конфиги: `YYYY-MM-DD_LR06_<name>.conf`

## Ход работы (таблица журнал)

| Step | Действие/команда                                                                                                                                                                                                                                                                                                 | Ожидаемый результат                                           | Факт/вывод                                                      | Доказательство (файл/скрин/лог)                                           |
| ---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- | --------------------------------------------------------------- | ------------------------------------------------------------------------- |
|    1 | Найти, где лежат логи и какие из них актуальные/большие при помощи команд:<br>cd /var/log<br>sudo ls -lh \| head -n 30                                                                                                                                                                                           | Видно логи и есть понимаешь, как оценивать их по размеру/дате | Вывод ls -lh (кусок) + описание 3 выбранных файла в отчёте LR06 | 06/2026-03-09_LR06_step01.png<br>06/LR06                                  |
|    2 | Найти успешные и неуспешные попытки входа с помощью команд:<br>sudo ls -lh /var/log \| grep auth<br>sudo grep -i "sshd" /var/log/auth.log \| tail -n 20<br>sudo grep -i "Accepted" /var/log/auth.log \| tail -n 10<br>sudo grep -i "Failed" /var/log/auth.log \| tail -n 10<br>sudo tail -n 20 /var/log/auth.log | Найти записи о входах и понять разницу Accepted vs Failed     | Вывод команд + 2–3 предложения вывода в отчёте LR06             | 06/2026-03-09_LR06_step02.png<br>06/2026-03-09_LR06_step03.png<br>06/LR06 |
|    3 | Найти проблемы по ключевым словам с помощью:<br>sudo ls -lh /var/log \| grep syslog<br>sudo grep -Ei "error\|warn\|failed" /var/log/syslog \| head -n 5                                                                                                                                                          | Научиться быстро находить подозрительные строки в syslog      | Вывод grep (5 строк) в отчёте LR06                              | 06/LR06                                                                   |
|    4 | Открыть auth.log и найти слово error при помощи команд:<br>sudo less /var/log/syslog                                                                                                                                                                                                                             | Прочитать логи постранично и найти внутри error               | Запись в отчёт LR06 что искал и что нашёл                       | 06/LR06                                                                   |
|    5 | Сделать тест при помощи команды:<br>sudo tail -n 50 /var/log/auth.log \| grep -i sshd \| head -n 5                                                                                                                                                                                                               | Успешно проведённый тест                                      | Вывод мини-теста в отчёте LR06                                  | 06/LR06                                                                   |

## Проблемы и решения

| Проблема/ошибка | Где возникло (step) | Диагностика (что проверили) | Решение (что сделали) | Доказательство |
| --------------- | ------------------: | --------------------------- | --------------------- | -------------- |
| -               |                     |                             |                       |                |

## Самопроверка (✓/⚠/✗)

| Пункт                                                         | Самооценка (✓/⚠/✗) | Комментарий                                             |
| ------------------------------------------------------------- | :----------------: | ------------------------------------------------------- |
| Я выполнил(а) все подпункты задания                           |         ✓          | В md и docx задания различаются(я делала по docx файлу) |
| Я понимаю, что делает каждая ключевая команда                 |         ✓          |                                                         |
| У меня есть минимум 2 доказательства (лог/вывод + файл/скрин) |         ✓          |                                                         |
| Я могу воспроизвести работу с нуля по своему отчёту           |         ✓          |                                                         |

## Выводы

- Что получилось хорошо: находить слова в log файлах
- Что было самым сложным: комбинировать команды при помощи pipe
- Что я буду делать иначе в следующий раз: - 

## Приложения

- `...` (перечислите файлы/скрины/логи)
- ![[2026-03-09_LR06_step01.png]]
- ![[2026-03-09_LR06_step02.png]]
- ![[2026-03-09_LR06_step03.png]]
