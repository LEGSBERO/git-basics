# Практика 2. Ansible

Выполнил: Бачурин Даниил Артёмович, группа БИ-3-24-05.

Практическая работа по Ansible (12 практик) выполнена на стенде из трёх
виртуальных машин Oracle VM VirtualBox под управлением Ubuntu 24.04.5 LTS:

- `ansible-srv` — управляющий узел, 192.168.56.11, ansible-core 2.16.3;
- `node1` — управляемый узел, 192.168.56.12;
- `node2` — управляемый узел, 192.168.56.13.

Узлы объединены сетью VirtualBox Host-Only, доступ в интернет — через NAT.
На управляемых узлах агент Ansible не устанавливается: используется SSH
и интерпретатор Python 3.12.

## Состав репозитория

- `inventory.ini` — инвентарь (`local`, `dev`, общая группа `allservers`);
- `ansible.cfg` — конфигурация (инвентарь по умолчанию, журнал `ansible.log`);
- `lesson1.yml`, `lesson2.yml` — сценарии (задачи и роли);
- `lesson_vars.yml`, `lesson_prompt.yml`, `lesson_groupvars.yml` — работа с переменными;
- `example.yml` — условия `when`;
- `with_nested_example1.yml`, `with_nested2.yml` — вложенные циклы;
- `roles/myRole/` — роль (tasks, defaults, метаданные каркаса `ansible-galaxy`);
- `group_vars/`, `host_vars/` — переменные групп и хостов;
- `figures/` — скриншоты консольных сессий (рисунки 1–20 отчёта);
- `report/` — отчёт по практической работе (docx и pdf).

## Основные команды

```bash
# проверка доступности
ansible all -m ping -o

# ad-hoc создание файла
ansible all -m file -a 'path=./myfile.txt state=touch' -o

# сценарии
ansible-playbook lesson1.yml
ansible-playbook lesson2.yml
ansible-playbook lesson2.yml --tags start
ansible-playbook lesson1.yml --tags pwd
ansible-playbook lesson1.yml --skip-tags pwd

# проверка прав файла роли
ansible all -m shell -a "stat -c '%a %n' some_directory/some_file.txt"
```
