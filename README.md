## monitoring roles with ansible

4 ansible roles 
- elastik_kibana
- fluentbit
- node_exporter
- prometheus


## Installation roles one by one

#### role  prometheus

Use ansible role prometheus to install.
```bash
ansible-playbook playbook.yml -i inventory.ini --become --tags 
```

```bash

PLAY [all] ******************************************************************************************************************************************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************************************************************************************************************
[WARNING]: Platform linux on host ubuntu is using the discovered Python interpreter at /usr/bin/python3.12, but future installation of another Python interpreter could change the meaning of that path. See https://docs.ansible.com/ansible-
core/2.17/reference_appendices/interpreter_discovery.html for more information.
ok: [ubuntu]

TASK [prometheus : Создание пользователя и группы для Prometheus] ***********************************************************************************************************************************************************************************
ok: [ubuntu]

TASK [prometheus : Создание необходимых директорий] *************************************************************************************************************************************************************************************************
ok: [ubuntu] => (item=/etc/prometheus)
ok: [ubuntu] => (item=/var/lib/prometheus)

TASK [prometheus : Проверка наличия файла Prometheus на удаленной машине] ***************************************************************************************************************************************************************************
ok: [ubuntu]

TASK [prometheus : Копирование локального архива Prometheus] ****************************************************************************************************************************************************************************************
skipping: [ubuntu]

TASK [prometheus : Распаковка архива Prometheus] ****************************************************************************************************************************************************************************************************
ok: [ubuntu]

TASK [prometheus : Копирование бинарных файлов Prometheus] ******************************************************************************************************************************************************************************************
ok: [ubuntu] => (item=prometheus)
ok: [ubuntu] => (item=promtool)

TASK [prometheus : Копирование консолей и библиотек] ************************************************************************************************************************************************************************************************
ok: [ubuntu] => (item=consoles)
ok: [ubuntu] => (item=console_libraries)

TASK [prometheus : Копирование файла конфигурации Prometheus] ***************************************************************************************************************************************************************************************
changed: [ubuntu]

TASK [prometheus : Копирование systemd сервиса Prometheus] ******************************************************************************************************************************************************************************************
ok: [ubuntu]

TASK [prometheus : Перезагрузка демона systemd] *****************************************************************************************************************************************************************************************************
changed: [ubuntu]

TASK [prometheus : Включение и запуск сервиса Prometheus] *******************************************************************************************************************************************************************************************
ok: [ubuntu]

RUNNING HANDLER [prometheus : Restart Prometheus] ***************************************************************************************************************************************************************************************************
changed: [ubuntu]

PLAY RECAP ******************************************************************************************************************************************************************************************************************************************
ubuntu                     : ok=12   changed=3    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0  
```

#### role  node_exporter

Use ansible role node_exporter to install.
```bash
ansible-playbook playbook.yml -i inventory.ini --become --tags 
```

```bash
PLAY [all] ******************************************************************************************************************************************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************************************************************************************************************
[WARNING]: Platform linux on host ubuntu is using the discovered Python interpreter at /usr/bin/python3.12, but future installation of another Python interpreter could change the meaning of that path. See https://docs.ansible.com/ansible-
core/2.17/reference_appendices/interpreter_discovery.html for more information.
ok: [ubuntu]

TASK [node_exporter : Создание пользователя и группы для Node Exporter] *****************************************************************************************************************************************************************************
ok: [ubuntu]

TASK [node_exporter : Проверка наличия файла node_exporter на удаленной машине] *********************************************************************************************************************************************************************
ok: [ubuntu]

TASK [node_exporter : Копирование локального архива node_exporter.tar.gz] ***************************************************************************************************************************************************************************
skipping: [ubuntu]

TASK [node_exporter : Распаковка архива Node Exporter] **********************************************************************************************************************************************************************************************
ok: [ubuntu]

TASK [node_exporter : Копирование бинарного файла Node Exporter] ************************************************************************************************************************************************************************************
ok: [ubuntu]

TASK [node_exporter : Копирование systemd сервиса Node Exporter] ************************************************************************************************************************************************************************************
ok: [ubuntu]

TASK [node_exporter : Перезагрузка демона systemd] **************************************************************************************************************************************************************************************************
changed: [ubuntu]

TASK [node_exporter : Включение и запуск сервиса Node Exporter] *************************************************************************************************************************************************************************************
ok: [ubuntu]

TASK [node_exporter : Обновление конфигурации Prometheus с новым хостом] ****************************************************************************************************************************************************************************
ok: [ubuntu]

PLAY RECAP ******************************************************************************************************************************************************************************************************************************************
ubuntu                     : ok=9    changed=1    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0   
```











## Test 

```bash
curl http://34.195.198.183:9090/api/v1/targets
```

```

{"status":"success","data":{"activeTargets":[{"discoveredLabels":{"__address__":"localhost:9090","__metrics_path__":"/metrics","__scheme__":"http","__scrape_interval__":"15s","__scrape_timeout__":"10s","job":"prometheus"},"labels":{"instance":"localhost:9090","job":"prometheus"},"scrapePool":"prometheus","scrapeUrl":"http://localhost:9090/metrics","globalUrl":"http://ip-172-16-1-218:9090/metrics","lastError":"","lastScrape":"2024-10-21T13:38:03.124796571Z","lastScrapeDuration":0.003960981,"health":"up","scrapeInterval":"15s","scrapeTimeout":"10s"}],"droppedTargets":[]}}%  

```

## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

[MIT](https://choosealicense.com/licenses/mit/)