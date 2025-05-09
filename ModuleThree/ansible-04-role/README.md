# Домашнее задание к занятию 4 «Работа с roles»
Ваша цель — разбить ваш playbook на отдельные roles.

Задача — сделать roles для ClickHouse, Vector и LightHouse и написать playbook для использования этих ролей.

Ожидаемый результат — существуют три ваших репозитория: два с roles и один с playbook.

```
ann@andreenkoa:~/mnt-homeworks/08-ansible-04-role/playbook$ ansible-galaxy install -r requirements.yml
Starting galaxy role install process
- clickhouse (1.13) is already installed, skipping.
- vector is already installed, skipping.
- extracting lighthouse to /home/ann/.ansible/roles/lighthouse
- lighthouse was installed successfully
ann@andreenkoa:~/mnt-homeworks/08-ansible-04-role/playbook$
```

Ссылка на мой playbook https://github.com/AnyaAndreenko/mnt-homeworks/tree/MNT-video/08-ansible-04-role/playbook

Ссылка на мой lighthouse https://github.com/AnyaAndreenko/lighthouse-role

Ссылка на мой vector https://github.com/AnyaAndreenko/vector-role
