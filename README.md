## monitoring roles with ansible

4 ansible roles 
- elastik_kibana
- fluentbit
- node_exporter
- prometheus

## Installation roles one by one


Use ansible role prometheus to install.
```bash
ansible-playbook playbook.yml -i inventory.ini --become --tags prometheus
```
```bash
ansible-playbook playbook.yml -i inventory.ini --become --tags node_exporter
```

```bash
ansible-playbook playbook.yml -i inventory.ini --become --tags elasticsearch_kibana
```
```bash
ansible-playbook playbook.yml -i inventory.ini --become --tags fluentbit
```

### Full Installation
```bash
ansible-playbook playbook.yml -i inventory.ini --become
```


#### Tested on Ubuntu 22





## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

[MIT](https://choosealicense.com/licenses/mit/)