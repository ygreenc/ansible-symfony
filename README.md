# Symfony2 Deployment role

Ripped from [Blacklight](http://www.blacklight.co.za).

Ansible role for deploying Symfony2 apps

```
project
    releases
        release
    shared
        app
            config
                parameters.yml
            logs
        web
            uploads
    current // This will be a symlink to the latest release
```

The role also has error checking in place. If any of the steps fail the role will delete the newly created release folder
and stop execution. If the deploy was successful the role will remove old releases.

Requirements
------------

The only requirement is Ansbile >= 1.2.

Installation
------------

```
TODO ansible-galaxy
```

Role Variables
--------------

| Variable | Default | Description |
| -------- | ------- | ----------- |
| symfony_root_dir | \<none\>(Required) | Project root directory |
| symfony_repo | \<none\>(Required) | Repository url |
| symfony_branch | master | Branch to checkout |
| symfony_strategy | git | Checkout Strategy (git\|svn\|hg) |
| symfony_local_root | / | Local root to symfony project (relative to playbook) |
| symfony_env | prod | Symfony environment for commands |
| symfony_composer_path | false | If false, will download composer into the project root |
| symfony_composer_options | --no-dev --no-interaction --optimize-autoloader | Flags for composer |
| symfony_assets_options | '' | Flags to add to assetic:dump command |
| symfony_php_path | /usr/bin/php | Path to PHP (used when downloading composer) |
| symfony_releases | 5 | Amount of releases to keep |
| perform_doctrine_migrations | False | Run doctrine migrations |

Example Playbook
----------------

```yml
---
- hosts: web
  vars:
    symfony_root_dir: /var/www/example
    symfony_repo: git@github.com/example/example-project.git
    symfony_composer_options: '--no-dev --optimize-autoloader --no-interaction'
    ansible_ssh_user: root

  roles:
    - ygreenc.symfony2
```

License
-------

MIT
