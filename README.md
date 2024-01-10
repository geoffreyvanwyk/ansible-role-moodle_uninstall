# Ansible Role for Uninstalling Moodle

![build](https://github.com/geoffreyvanwyk/ansible-role-moodle_uninstall/workflows/Build/badge.svg?event=push)

Uninstalls a Moodle instance that was installed by 
[Ansible Role for Moodle](https://github.com/geoffreyvanwyk/ansible-role-moodle)
by:

* removing included Apache web server configuration,
* removing cron job,
* dropping database,
* deleting the moodledata directory, and
* deleting the Moodle source code from the web document root.

## Requirements

> Any pre-requisites that may not be covered by Ansible itself or the role
> should be mentioned here. For instance, if the role uses the EC2 module, it may
> be a good idea to mention in this section that the boto package is required.

The role only uninstalls a Moodle instance served from a subdirectory.

The role is only tested on long-term support versions of Ubuntu that still
receive standard support.

The role only supports PostgreSQL database.

## Role Variables

> A description of the settable variables for this role should go here,
> including any variables that are in defaults/main.yml, vars/main.yml, and any
> variables that can/should be set via parameters to the role. Any variables that
> are read from other roles and/or the global scope (ie. hostvars, group vars,
> etc.) should be mentioned here as well.

None of the variables, except `moodle_cfg_dbtype` has a default value. A value
must be provided for each variable listed here.

### Web

```yaml
moodle_web_domain: ""
moodle_web_path: "
```

These two variables are used to calculate `moodle_instance` which uniquely
identifies the Moodle instance. That identity is used in the names of other
files, directories and other objects that belong to the instance.

---

### Delete Source Code

```yaml
moodle_deploy_destination: ""
```

The path to the Moodle source code.

---

### Drop Database

```yaml
moodle_cfg_dbtype: pgsql
moodle_cfg_dbname: ""
```

The `postgres` user is used to drop the database.

---

### Remove Apache configuration

```yaml
moodle_web_apache_conf: ""  # Calculated from `moodle_instance`.
```

The name of included Apache configuration file.

---

### Installation & Server-Side configuration

```yaml
moodle_cfg_dataroot: ""  # Calculated from `moodle_instance`.
```

The path to the moodledata directory.

## Dependencies

> A list of other roles hosted on Galaxy should go here, plus any details in
> regards to parameters that may need to be set for other roles, or variables that
> are used from other roles.

The list of roles and collections on which this role depends can be found in
`requirements.yml` .

## Example Playbook

> Including an example of how to use your role (for instance, with variables
> passed in as parameters) is always nice for users too:

```ansible
- hosts: servers
  roles:
    - role: geoffreyvanwyk.moodle_uninstall
      moodle_web_domain: www.example.com
      moodle_web_path: moodle
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
