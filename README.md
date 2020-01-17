# Ansible role `zabbix-server`

Ansible role for a full zabbix-server (4.4 version) with a RedHat-based Linux distribution (CentOS, Fedora, RHEL, ...). Specifically, the responsibilities of this role are to monitor the:
- Networks
- Servers
- Virtual machines
- Cloud services

## Requirements

No requirements needed. Zabbix, MariaDB and PHP are included in this role.

## Role Variables

| Variable                      | Default                | Comments (type)  |
| :---                          | :---                   | :---             |
| `zabbix_server_repo`          | -   zabbixserver       | Name of the Zabbix Official Repository that provides RPM packages for Red Hat Enterprise Linux.                                        |
| `zabbix_server_ip`            | -                      | The IP of the Zabbix Server to reach it. |
| `zabbix_server_database_name` | -   zabbix             | The name of the MySQL database. |
| `zabbix_server_dbpassword`    | -   root               | Password of the MySQL database with default name 'zabbix'. |
| `zabbix_server_database_user` | -   root               | Database user to connect to the MySQL database.  |
| `zabbix_server_database_host` | -   127.0.0.1          | The localhost address, this is not the same as the ip of the Zabbix server. |
| `zabbix_server_database_port` | -   3306               | When there are multiple options for databases, this can change. If you use MySQL/mariadb, keep the default. |
| `zabbix_server_database_schema` | -                    | Name of the database schema that will be installed and configured with the zabbix server. |
| `zabbix_server_port`          | -  10051               | (scalar) PURPOSE |
| `zabbix_server_domain`        | -                      | Domain name of the network where you want to set up the server. example: avalon.lan|
| `zabbix_server_user`          | -     Admin             | This is the default user to login with Zabbix. User "Admin" is a Zabbix superuser. User "guest" is a special default user. If you want to change this settings, you can do this after you login with the superuser (Admin). |
| `zabbix_server_name`          | -     zabbixserver     | Name of the Zabbix Server  |
| `zabbix_server_allowroot`     | -     1                | The default value is "1", this will run the Zabbix Server as 'root'. When you change the value to "0", it will not be possible to run the server as root.|
| `zabbix_server_logpath`       | -  /var/log/networkmonitor/zabbixS.log   | The path to the file where you can read the logs. The best option if you are going to create a path yourself is to keep "/var/log/". |
| `php_date_timezone`           | -  Europe/Brussels     | De tijdzone is belangrijk om goed in te stellen om door de prerequisites van Zabbix te gaan. Wanneer dit niet goed is ingesteld zal hij falen. Meer info kan op volgende website vinden. <https://www.php.net/manual/en/timezones.php/> |

**Remarks**

(1) At this moment it is not yet possible to choose a version of Zabbix. Version 4.4 will be installed in a total server package without an agent.  

(2) The Zabbix repository and MariaDB will be installed from the Zabbix website and yum repository, so this could take a while. It won't take long, so please be patient and your patience will be rewarded.  

(3) Like said in the comments, when you are on the Zabbix login page. You have to login with username: **Admin** and password: **zabbix**.  

(4) If you want to monitor some servers, you have to add an extra role named 'Zabbix Agent'.  

## Useful paths*

| Variable                           | Path (type)            |
| :---                               | :---                   |
| `zabbix_server_dbsocket`           | /var/lib/mysql/mysql.sock |
| `zabbix_server_config_server`      | /etc/zabbix/zabbix_server.conf |
| `zabbix_server_socketDir`          | /var/run/zabbix                |
| `zabbix_server_logfile`            | /var/log/zabbix/zabbix_server.log |
| `php_ini_filename`                 | /etc/php.ini                      |
| `mariadb_config_network`           | /etc/my.cnf.d/network.cnf          |
| `mariadb_config_server`            | /etc/my.cnf.d/server.cnf           |
| `mariadb_config_custom`            | /etc/my.cnf.d/custom.cnf           |

*There is no way to modify these paths. We do this for your user-friendliness. The paths you are looking for can be found above. 

## Dependencies

No dependencies.

## Example Playbook Vagrant
**Below is the minimum configuration required to get the role working.**  
```yaml
zabbix_server_ip: 172.16.192.25  
zabbix_server_database_schema: Zabbix  

mariadb_databases:  
  - name: zabbix  

mariadb_root_password: 'root'  
mariadb_users:  
  - name: zabbix  
    password: 'root'  
    priv: 'zabbix.*:ALL'  
```

## Testing

There are no tests written in Vagrant or Docker for this Zabbix server. Do you feel called upon to add value to this role? Feel free to write the necessary tests and get into our "List of Fame". 

## Contributing

Issues, feature requests, ideas are appreciated and can be posted in the Issues section.

Pull requests are also very welcome. The best way to submit a PR is by first creating a fork of this Github project, then creating a topic branch for the suggested change and pushing that branch to your own fork. Github can then easily create a PR based on that branch. Don't forget to add your name to the contributor list below!

## License

2-clause BSD license, see [LICENSE.md](LICENSE.md)

## Contributors/List of Fame

- [Arno Van Nieuwenhove](https://github.com/ArnoVanNieuwenhove) (maintainer)
- [Cedric Detemmerman](maintainer)
- [Bert Van Vreckem](https://github.com/bertvv/) (mariadb/teacher)