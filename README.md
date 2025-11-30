Nginx Role
=========

Ansible роль для установки nginx из stable ветки. Конфигурация собирается динамически из template. По умолчанию запускается установка nginx и конфигурирование из template. Это поведении можно изменить указав тэг при запуске. Также есть возможность удалить nginx при использованиии тэга.

Поддерживаемые ОС:
  - Debian 11.x - 13.x
  - Ubuntu 22.04 - 25.10
  - CentOS 7 - 9

Подробнее о версиях nginx для конкретных дистрибутивов см. на [nignx.org](https://nginx.org/en/linux_packages.html)

Requirements
------------

Для использования потребуются следующие модули:
  - ansible.builtin.apt_key
  - ansible.builtin.apt_repository
  - ansible.builtin.template
  - ansible.builtin.meta
  - ansible.builtin.apt
  - ansible.builtin.yum_repository
  - ansible.builtin.dnf


Role Variables
--------------

| Name | Description | Type | Default |
|------|-------------|------|---------|
| <a name="input_nginx_version"></a> [nginx\_version](#input\_nginx\_version) | Версия nginx для установки | `string` | `1.26.3` |
| <a name="input_nginx_user"></a> [nginx\_user](#input\_nginx\_user) | Пользователь из под которого будет работать nginx | `"string"` | `root` |
| <a name="input_rpm_gpg_key_url"></a> [rpm\_gpg\_key\_url](#input\_rpm\_gpg\_key\_url) | URL GPG ключа для подписи пакета deb | `string` | `"https://nginx.org/keys/nginx_signing.key"` |
| <a name="input_deb_gpg_key_url"></a> [deb\_gpg\_key\_url](#input\_deb\_gpg\_key\_url) | URL GPG ключа для подписи пакета rpm | `string` | `"https://nginx.org/keys/nginx_signing.key"` |
| <a name="input_deb_gpg_path"></a> [rpm\_deb\_gpg\_path](#input\_deb\_gpg\_path) | Путь сохранения GPG ключа для deb | `string` | `"/usr/share/keyrings/nginx-archive-keyring.gpg"` |

Example Playbook
----------------

Переменные можно переопределить в group_vars или указать в play.

Пример playbook:

    - hosts: web-servers
      become: true
      roles:
         - nginx

Пример запуска ansible-playbook:

  **Запуск установки и настройки nginx:**
  
    ansible-playbook -i hosts.ini site.yml

  **Запуск только установки nginx:**
  
    ansible-playbook -i hosts.ini site.yml --tags nginx_install

  **Запуск только настройки nginx:**
  
    ansible-playbook -i hosts.ini site.yml --tags nginx_conf
  
  **Удание nginx и конфигурации:**
  
    ansible-playbook -i hosts.ini site.yml --tags nginx_remove

License
-------

BSD

Author Information
------------------

Perman Maxim
maxim@7perman.ru
