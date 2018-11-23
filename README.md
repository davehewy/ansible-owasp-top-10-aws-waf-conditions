# Ansible AWS WAF Conditions for OWASP top 10 (11/2018)

Just taking the time to contribute this up. Since I could not find a source for the ansible owasp top 10 waf conditions myself.

Mostly lifted from the rules found here - https://github.com/aws-samples/aws-waf-sample/blob/master/waf-owasp-top-10/owasp_10_base.yml

Example usage:

```
- hosts: localhost
  vars:
    aws_profile: some_aws_profile

  tasks:
    - name: include owasp_top_10 into waf_conditions
      include_vars:
        file: owasp-top-10-aws-waf-conditions.yml

    - name: create waf conditions
      aws_waf_condition:
        name: "{{ item.name }}"
        filters: "{{ item.filters }}"
        type: "{{ item.type }}"
        profile: "{{ aws_profile }}"
        state: "{{ item.state | default('absent') }}"
      loop: "{{ waf_conditions }}"

```