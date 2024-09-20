Ansible Role: Outline
=========

Deploy [Outline](https://www.getoutline.com/) in Docker.

Requirements
------------

None.

Role Variables
--------------

The following variables need to be set to use the role.

    outline_docker_outline_secret_key:
    outline_docker_outline_utils_key:
    outline_docker_postgres_password:

Available variables are listed below, along with default values (see defaults/main.yml):

    outline_docker_network: outline

Docker network for used for the container stack.

    outline_docker_postgres_volume: outline-postgres
    outline_docker_postgres_container: outline-postgres
    outline_docker_postgres_image_name: postgres
    outline_docker_postgres_image_tag: latest
    outline_docker_postgres_user: outline
    outline_docker_postgres_database: outline

Configuration for the postgres container.

    outline_docker_redis_container: outline-redis
    outline_docker_redis_image_name: redis
    outline_docker_redis_image_tag: latest

Configuration for the redis container.

    outline_docker_outline_volume: outline-storage
    outline_docker_outline_container: outline-outline
    outline_docker_outline_image_name: docker.getoutline.com/outlinewiki/outline
    outline_docker_outline_image_tag: latest

Configuration for the outline container.

    outline_docker_outline_node_environment: production
    outline_docker_outline_database_url: postgres://{{ outline_docker_postgres_user }}:{{ outline_docker_postgres_password }}@{{ outline_docker_postgres_container }}:5432/{{ outline_docker_postgres_database }}
    outline_docker_outline_database_connection_pool_min: ""
    outline_docker_outline_database_connection_pool_max: ""
    outline_docker_outline_pgsslmode: disable
    outline_docker_outline_redis_url: redis://{{ outline_docker_redis_container }}:6379
    outline_docker_outline_outline_url: "http://localhost:3000"
    outline_docker_outline_outline_port: 3000
    outline_docker_outline_file_storage_local_root_dir: /var/lib/outline/data
    outline_docker_outline_file_storage_upload_max_size: 262144000

These variables are required as documented in [.env.samle](https://github.com/outline/outline/blob/main/.env.sample).

You can set authentication and optional environment variables using ansible variables in the format `outline_docker_outline_<variable_name>`, corresponding to environment variables like `VARIABLE_NAME`. For example, `outline_docker_outline_slack_verification_token` maps to `SLACK_VERIFICATION_TOKEN`.

Dependencies
------------

Docker on the host that runs the outline container.

Example Playbook
----------------

```yaml
- hosts: all
  roles:
    - role: tomhesse.outline
```

License
-------

MIT / BSD

Author Information
------------------

This role was created in 2024 by [tomhesse](https://www.tomhesse.xyz/).
