# Ansible Role: gitlab ci pipelines exporter

**Disclaimer:** This project is heavily influenced by [cloudalchemy/ansible-node-exporter](https://github.com/cloudalchemy/ansible-node-exporter)
and mostly just replaced the exporter names and variables.

## Description

Deploy prometheus [gitlab ci pipelines exporter](https://github.com/mvisonneau/gitlab-ci-pipelines-exporter) using ansible.

## Requirements

- Ansible >= 2.7

## Role Variables

All variables that can be overridden are stored in [defaults/main.yml](defaults/main.yml) and are listed in the table below.

| Name | Default Value | Description |
| ---- | ------------- | ----------- |
| `gitlab_ci_pipelines_exporter_version` | 0.5.2 | GitLab CI Pipelines exporter package version. Also accepts 'latest' as parameter. |
| `gitlab_ci_pipelines_exporter_binary_local_dir` | "" | Enables the use of local packages instead of those distributed on github. The parameter may be set to a directory where the `gitlab-ci-pipelines-exporter` binary is stored on the host where ansible is run. This overrides the `gitlab_ci_pipelines_exporter_version` parameter. |
| `gitlab_ci_pipelines_exporter_server_listen_address` | ":8080" | Address on which gitlab ci pipelines exporter will listen. |
| `gitlab_ci_pipelines_exporter_gitlab_url` | "https://gitlab.com" | URL of your GitLab instance. |
| `gitlab_ci_pipelines_exporter_gitlab_token` | "" | The token to use to authenticate against the GitLab API (requires `read_api` and `read_repository` permissions). |
| `gitlab_ci_pipelines_exporter_gitlab_health_url` | "{{ gitlab_ci_pipelines_exporter_gitlab_url }}/-/health" | Alternative URL for determining health of GitLab API for the readiness probe. |
| `gitlab_ci_pipelines_exporter_enable_health_check` | true | Enable verification of readiness for target GitLab instance. |
| `gitlab_ci_pipelines_exporter_enable_tls_verify` | true | Enable TLS verification for target GitLab instance (handy when self-hosting). |
| `gitlab_ci_pipelines_exporter_garbage_collect` | {} | When to garbage collect information. See [here](https://github.com/mvisonneau/gitlab-ci-pipelines-exporter/blob/main/docs/configuration_syntax.md?plain=1#L149) for configuration syntax. |
| `gitlab_ci_pipelines_exporter_project_defaults` | {} | Default [settings](https://github.com/mvisonneau/gitlab-ci-pipelines-exporter/blob/main/docs/configuration_syntax.md?plain=1#198) which can be overridden at the project or wildcard level. |
| `gitlab_ci_pipelines_exporter_projects` | [] | The list of projects you want to monitor. See [here](https://github.com/mvisonneau/gitlab-ci-pipelines-exporter/blob/main/docs/configuration_syntax.md?plain=1#305) for configuration syntax. |
| `gitlab_ci_pipelines_exporter_wildcards` | [] | Settings to dynamically fetch projects to monitor. See [here](https://github.com/mvisonneau/gitlab-ci-pipelines-exporter/blob/main/docs/configuration_syntax.md?plain=1#412) for configuration syntax. |

## Example

### Playbook

Use it in a playbook as follows:

```yaml
- hosts: all
  become: true
  roles:
    - cluttrdev.gitlab_ci_pipelines_exporter
  vars:
    gitlab_ci_pipelines_exporter_gitlab_url: "https://gitlab.example.com"
    gitlab_ci_pipelines_exporter_gitlab_token: "<your token>"
```

## License

This project is licensed under MIT License. See [LICENSE](/LICENSE) for more details.

