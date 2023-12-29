# Ansible Role for Uninstalling Moodle

[![build](https://github.com/geoffreyvanwyk/ansible-role-moodle_uninstall/workflows/Build/badge.svg?event=push)](https://github.com/geoffreyvanwyk/ansible-role-moodle_uninstall/actions?query=workflow%3ABuild)

Uninstalls a Moodle instance by:

* removing included Apache web server configuration,
* removing cron job,
* dropping database,
* deleting the moodledata directory, and
* deleting the Moodle source code from the web document root.

## Requirements

> Any pre-requisites that may not be covered by Ansible itself or the role
> should be mentioned here. For instance, if the role uses the EC2 module, it may
> be a good idea to mention in this section that the boto package is required.

The role only uninstalls a Moodle instance served from a subdirectory, and works best when the Moodle instance was installed with [Ansible role for Moodle](https://github.com/geoffreyvanwyk/ansible-role-moodle).

The role is only tested on long-term support versions of Ubuntu that still receive standard support.

At the moment, the role only uses Apache web server which it installs itself.

The role only supports removing the included Apache web configuration as for a Moodle instance installed in a subdirectory; not the removal of a virtual host configuration.

## Role Variables

> A description of the settable variables for this role should go here,
> including any variables that are in defaults/main.yml, vars/main.yml, and any
> variables that can/should be set via parameters to the role. Any variables that
> are read from other roles and/or the global scope (ie. hostvars, group vars,
> etc.) should be mentioned here as well.

### Deployment of Source Code

```yaml
moodle_deploy_destination: /var/www/html/moodle
```

The path to the Moodle source code.

---

### Set-Up of Database

```yaml
moodle_cfg_dbtype: pgsql    # Which database service is used: pgsql or maridb.
moodle_cfg_dbname: moodle   # The name of the database.
moodle_cfg_dbuser:          # Username.
moodle_cfg_dbpass:          # Password.
```

The database user provided must have permission to drop the database. If no username and password are given, for PostgreSQL, the `postgres` user will be used; for MariaDB, the socket will be used, if possible.

---

### Web Hosting

```yaml
moodle_web_domain: 127.0.0.1          # Domain name of the web service virtual host.
moodle_web_path: moodle               # Subdirectory relative to virtual host.
```

As with the Ansible role for Moodle, These two variables are used to calculate the `moodle_instance` variable that uniquely identifies the Moodle instance. The `moodle_instance` variable is used to:

* locate the moodledata directory, unless that path is explicitly given;
* locate the included Apache configuration file;
* identify the cronjob that needs to be removed.

If the `moodle_web_path` is not given, it is calculated from the basename `moodle_deploy_destination`.

---

### Installation & Server-Side configuration

```yaml
moodle_cfg_dataroot: /var/www/moodledata
```

The path to the moodledata directory. If not given, it is calculated from the `moodle_instance` variable.

## Dependencies

> A list of other roles hosted on Galaxy should go here, plus any details in
> regards to parameters that may need to be set for other roles, or variables that
> are used from other roles.

The list of roles on which this role depends can be found in `requirements.yml` .

## Example Playbook

> Including an example of how to use your role (for instance, with variables
> passed in as parameters) is always nice for users too:

```ansible
- hosts: servers
  roles:
    - role: geoffreyvanwyk.moodle_uninstall
      moodle_web_domain: www.example.com
```

## License

Copyright &copy; 2023 Geoffrey Bernardo van Wyk [https://geoffreyvanwyk.dev](https://geoffreyvanwyk.dev)

This file is part of Ansible role geoffreyvanwyk.moodle_uninstall.

Ansible role geoffreyvanwyk.moodle_uninstall is free software: you can redistribute it
and/or modify it under the terms of the GNU General Public License as
published by the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

Ansible role geoffreyvanwyk.moodle_uninstall is distributed in the hope that it will be
useful, but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General
Public License for more details.

You should have received a copy of the GNU General Public License along with
Ansible role geoffreyvanwyk.moodle_uninstall. If not, see <https://www.gnu.org/licenses/>.

## Author Information

> An optional section for the role authors to include contact information, or a
> website (HTML is not allowed).

[Geoffrey Bernardo van Wyk](https://geoffreyvanwyk.dev) created this role in 2023.
