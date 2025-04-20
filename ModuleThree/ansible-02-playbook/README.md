# Домашнее задание к занятию 2 «Работа с Playbook»

1. Подготовьте свой inventory-файл prod.yml.

   [prod.yml](https://github.com/AnyaAndreenko/mnt-homeworks/blob/MNT-video/08-ansible-02-playbook/playbook/inventory/prod.yml)
   
3. Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает vector. Конфигурация vector должна деплоиться через template файл jinja2. От вас не требуется использовать все возможности шаблонизатора, просто вставьте стандартный конфиг в template файл. Информация по шаблонам по ссылке. не забудьте сделать handler на перезапуск vector в случае изменения конфигурации!

   [site.yml](https://github.com/AnyaAndreenko/mnt-homeworks/blob/MNT-video/08-ansible-02-playbook/playbook/site.yml)


4. При создании tasks рекомендую использовать модули: get_url, template, unarchive, file.
Tasks должны: скачать дистрибутив нужной версии, выполнить распаковку в выбранную директорию, установить vector.

   [site.yml](https://github.com/AnyaAndreenko/mnt-homeworks/blob/MNT-video/08-ansible-02-playbook/playbook/site.yml)

5. Запустите ansible-lint site.yml и исправьте ошибки, если они есть.
6. Попробуйте запустить playbook на этом окружении с флагом --check.

   
  ``` ann@andreenkoa:~/mnt-homeworks/08-ansible-02-playbook/playbook$ sudo ansible-playbook site.yml -i inventory/prod.yml --check```
```
PLAY [Install Clickhouse] **********************************************************************************************************************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************************************************************************************************************************

ED25519 key fingerprint is SHA256: *****.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
ok: [clickhouse-01]

TASK [Get clickhouse distrib] ******************************************************************************************************************************************************************************************************************************************
changed: [clickhouse-01] => (item=clickhouse-client)
changed: [clickhouse-01] => (item=clickhouse-server)
changed: [clickhouse-01] => (item=clickhouse-common-static)

TASK [Install clickhouse packages] *************************************************************************************************************************************************************************************************************************************
An exception occurred during task execution. To see the full traceback, use -vvv. The error was: OSError: Could not open: clickhouse-common-static-23.8.4.69.rpm clickhouse-client-23.8.4.69.rpm clickhouse-server-23.8.4.69.rpm
fatal: [clickhouse-01]: FAILED! => {"changed": false, "module_stderr": "Shared connection to 10.0.0.241 closed.\r\n", "module_stdout": "Traceback (most recent call last):\r\n  File \"/root/.ansible/tmp/ansible-tmp-1731965325.72044-1850684-83278989268047/AnsiballZ_dnf.py\", line 107, in <module>\r\n    _ansiballz_main()\r\n  File \"/root/.ansible/tmp/ansible-tmp-1731965325.72044-1850684-83278989268047/AnsiballZ_dnf.py\", line 99, in _ansiballz_main\r\n    invoke_module(zipped_mod, temp_path, ANSIBALLZ_PARAMS)\r\n  File \"/root/.ansible/tmp/ansible-tmp-1731965325.72044-1850684-83278989268047/AnsiballZ_dnf.py\", line 47, in invoke_module\r\n    runpy.run_module(mod_name='ansible.modules.dnf', init_globals=dict(_module_fqn='ansible.modules.dnf', _modlib_path=modlib_path),\r\n  File \"/usr/lib64/python3.9/runpy.py\", line 225, in run_module\r\n    return _run_module_code(code, init_globals, run_name, mod_spec)\r\n  File \"/usr/lib64/python3.9/runpy.py\", line 97, in _run_module_code\r\n    _run_code(code, mod_globals, init_globals,\r\n  File \"/usr/lib64/python3.9/runpy.py\", line 87, in _run_code\r\n    exec(code, run_globals)\r\n  File \"/tmp/ansible_ansible.builtin.dnf_payload_uzhk1t77/ansible_ansible.builtin.dnf_payload.zip/ansible/modules/dnf.py\", line 1468, in <module>\r\n  File \"/tmp/ansible_ansible.builtin.dnf_payload_uzhk1t77/ansible_ansible.builtin.dnf_payload.zip/ansible/modules/dnf.py\", line 1457, in main\r\n  File \"/tmp/ansible_ansible.builtin.dnf_payload_uzhk1t77/ansible_ansible.builtin.dnf_payload.zip/ansible/modules/dnf.py\", line 1431, in run\r\n  File \"/tmp/ansible_ansible.builtin.dnf_payload_uzhk1t77/ansible_ansible.builtin.dnf_payload.zip/ansible/modules/dnf.py\", line 1076, in ensure\r\n  File \"/tmp/ansible_ansible.builtin.dnf_payload_uzhk1t77/ansible_ansible.builtin.dnf_payload.zip/ansible/modules/dnf.py\", line 976, in _install_remote_rpms\r\n  File \"/usr/lib/python3.9/site-packages/dnf/base.py\", line 1341, in add_remote_rpms\r\n    raise IOError(_(\"Could not open: {}\").format(' '.join(pkgs_error)))\r\nOSError: Could not open: clickhouse-common-static-23.8.4.69.rpm clickhouse-client-23.8.4.69.rpm clickhouse-server-23.8.4.69.rpm\r\n", "msg": "MODULE FAILURE\nSee stdout/stderr for the exact error", "rc": 1}

PLAY RECAP *************************************************************************************************************************************************************************************************************************************************************
clickhouse-01              : ok=2    changed=1    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0  
  ``` 
   
   
7. Запустите playbook на prod.yml окружении с флагом --diff. Убедитесь, что изменения на системе произведены.
8. Повторно запустите playbook с флагом --diff и убедитесь, что playbook идемпотентен.

   
     ```ann@andreenkoa:~/mnt-homeworks/08-ansible-02-playbook/playbook$ ~/netology/homework/mnt-homeworks/08-ansible-02-playbook/playbook$ sudo ansible-playbook site.yml -i inventory/prod.yml --diff  ```


  ```PLAY [Install Clickhouse] **********************************************************************************************************************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Get clickhouse distrib] ******************************************************************************************************************************************************************************************************************************************
failed: [clickhouse-01] (item=clickhouse-client) => {"ansible_loop_var": "item", "changed": false, "dest": "./clickhouse-client-23.8.4.69.rpm", "elapsed": 4, "gid": 0, "group": "root", "item": "clickhouse-client", "mode": "0644", "msg": "Request failed: <urlopen error [Errno -2] Name or service not known>", "owner": "root", "size": 97323, "state": "file", "uid": 0, "url": "https://packages.clickhouse.com/rpm/stable/clickhouse-client-23.8.4.69.x86_64.rpm"}
failed: [clickhouse-01] (item=clickhouse-server) => {"ansible_loop_var": "item", "changed": false, "dest": "./clickhouse-server-23.8.4.69.rpm", "elapsed": 0, "gid": 0, "group": "root", "item": "clickhouse-server", "mode": "0644", "msg": "Request failed: <urlopen error [Errno -2] Name or service not known>", "owner": "root", "size": 125915, "state": "file", "uid": 0, "url": "https://packages.clickhouse.com/rpm/stable/clickhouse-server-23.8.4.69.x86_64.rpm"}
failed: [clickhouse-01] (item=clickhouse-common-static) => {"ansible_loop_var": "item", "changed": false, "dest": "./clickhouse-common-static-23.8.4.69.rpm", "elapsed": 0, "gid": 0, "group": "root", "item": "clickhouse-common-static", "mode": "0644", "msg": "Request failed: <urlopen error [Errno -2] Name or service not known>", "owner": "root", "size": 282440806, "state": "file", "uid": 0, "url": "https://packages.clickhouse.com/rpm/stable/clickhouse-common-static-23.8.4.69.x86_64.rpm"}

TASK [Get clickhouse distrib (rescue)] *********************************************************************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Install clickhouse packages] *************************************************************************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Flush handlers to restart clickhouse] ****************************************************************************************************************************************************************************************************************************

PLAY [Install vector] **************************************************************************************************************************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************************************************************************************************************************
ok: [vector-01]

TASK [Get vector distrib] **********************************************************************************************************************************************************************************************************************************************
ok: [vector-01]

TASK [Install vector packages] *****************************************************************************************************************************************************************************************************************************************
ok: [vector-01]

TASK [Flush handlers to restart vector] ********************************************************************************************************************************************************************************************************************************

TASK [Configure Vector | ensure what directory exists] *****************************************************************************************************************************************************************************************************************
--- before
+++ after
@@ -1,4 +1,4 @@
 {
     "path": "/root/vector_config",
-    "state": "absent"
+    "state": "directory"
 }

changed: [vector-01]

TASK [Configure Vector | Template config] ******************************************************************************************************************************************************************************************************************************
--- before
+++ after: /root/.ansible/tmp/ansible-local-1852938w20gcz8t/tmp2sf1rpdm/vector.yml.j2
@@ -0,0 +1,45 @@
+#TEST config from Ansible
+#                                    __   __  __
+#                                    \ \ / / / /
+#                                     \ V / / /
+#                                      \_/  \/
+#
+#                                    V E C T O R
+#                                   Configuration
+#
+# ------------------------------------------------------------------------------
+# Website: https://vector.dev
+# Docs: https://vector.dev/docs
+# Chat: https://chat.vector.dev  ```
  
  ```TASK [Install clickhouse packages] *************************************************************************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Flush handlers to restart clickhouse] ****************************************************************************************************************************************************************************************************************************

PLAY [Install vector] **************************************************************************************************************************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************************************************************************************************************************
ok: [vector-01]

TASK [Get vector distrib] **********************************************************************************************************************************************************************************************************************************************
ok: [vector-01]

TASK [Install vector packages] *****************************************************************************************************************************************************************************************************************************************
ok: [vector-01]

TASK [Flush handlers to restart vector] ********************************************************************************************************************************************************************************************************************************

TASK [Configure Vector | ensure what directory exists] *****************************************************************************************************************************************************************************************************************
ok: [vector-01]

TASK [Configure Vector | Template config] ******************************************************************************************************************************************************************************************************************************
ok: [vector-01]

PLAY RECAP *************************************************************************************************************************************************************************************************************************************************************
clickhouse-01              : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
vector-01                  : ok=5    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```
9. Подготовьте README.md-файл по своему playbook. В нём должно быть описано: что делает playbook, какие у него есть параметры и теги. Пример качественной документации ansible playbook по ссылке. Так же приложите скриншоты выполнения заданий №5-8
10. Готовый playbook выложите в свой репозиторий, поставьте тег 08-ansible-02-playbook на фиксирующий коммит, в ответ предоставьте ссылку на него.
