# Ansible Role: Apache Solr

[![Build Status](https://img.shields.io/travis/rwanyoike/ansible-role-solr.svg)](https://travis-ci.org/rwanyoike/ansible-role-solr) [![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/rwanyoike/ansible-role-solr/master/LICENSE)

Installs and configures [Apache Solr](https://lucene.apache.org/solr/) on RHEL/CentOS ~~or Debian/Ubuntu~~.

Tested with Solr 5.x.

## Requirements

- Java. You can easily install Java using the [rwanyoike.java](https://github.com/rwanyoike/ansible-role-java) role.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
# Version that should be installed
solr_version: 5.3.1
```

See [https://www.us.apache.org/dist/lucene/solr/](https://www.us.apache.org/dist/lucene/solr/) for a listing of available versions (e.g. `5.2.1`, `5.3.1`).

```yaml
# Directory to extract the Solr installation archive
solr_install_dir: /opt
# Directory for live / writable Solr files
solr_write_dir: /var/solr

# User to own the Solr files and run the Solr process
solr_user: solr
# Service name
solr_service: solr

# Port Solr should bind to
solr_bind_port: 8983
```

Solr includes a [service installation script](https://cwiki.apache.org/confluence/display/solr/Taking+Solr+to+Production#TakingSolrtoProduction-ServiceInstallationScript) (`bin/install_solr_service.sh`) to help install Solr as a service on Linux. The script creates a symbolic link to the versioned directory of Solr. For instance, if you run the role with `solr_version: 5.2.1`, then the following directory structure will be used:

```
/opt/solr-5.2.1
/opt/solr -> /opt/solr-5.2.1
```

Using a symbolic link insulates any scripts from being dependent on the specific Solr version.

## Dependencies

None

## Example Playbook

```yaml
- hosts: webservers

  vars_files:
    - vars/main.yml

  roles:
    - role: rwanyoike.java
    - role: rwanyoike.solr
```

Inside `vars/main.yml:`

```yaml
solr_version: 5.2.1

# ... etc ...
```

## License

MIT

## Author Information

This role was created in 2015 by [Raymond Wanyoike](https://github.com/rwanyoike).
