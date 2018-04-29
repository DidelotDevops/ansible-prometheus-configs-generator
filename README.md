# Ansible Role: Prometheus configs generator

An Ansible Role that generate the prometheus.yml config file.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    prometheus_monitor_label: monitoring
    prometheus_rule_files:
    prometheus_alerting:
    prometheus_port: 9090
    prometheus_extra_scrape_configs:
    prometheus_path_to_generated_config: "{{ playbook_dir }}"

## Dependencies

None.

## Example Playbook

    - role: prometheus-configs-generator
      prometheus_path_to_generated_config: "../../docker/prometheus"
      prometheus_extra_scrape_configs:
        - job_name: 'cadvisor'
          scrape_interval: 5s
          dns_sd_configs:
            - names:
              - 'tasks.cadvisor'
                type: 'A'
                port: 8080
            static_configs:
              - targets: "{{ nodes_ips | map('regex_replace','(.*)','\\1:8080')| list }}"

## License

MIT / BSD

## Author Information

This role was created in 2018 by Didelot Kévin.
