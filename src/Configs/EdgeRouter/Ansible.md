# EdgeRouter-Ansible

## `EdgeOS.yml`

```yml,editable
---

- name: EdgeOS Playbook
  connection: ansible.netcommon.network_cli
  gather_facts: false
  hosts: all
  tasks:

    - vyos.vyos.vyos_facts:
        gather_subset: min
        gather_network_resources: interfaces

    - name: show ethX interfaces
      vyos.vyos.vyos_command:
        commands:
        - show interfaces ethernet {{ item }}
      with_items:
      - eth0
      - eth1
      - eth2
      - eth3
      - eth4
      - eth5
      - eth6
      - switch0
      - lo

    - name: Print return information from the previous task
      ansible.builtin.debug:
        var: result
        verbosity: 2

    - debug:
        msg: "{{ ansible_facts }}"

```

-----

## Demo

<script id="asciicast-MzxU6PcNGluvAJMLWGEqxAvmA" src="https://asciinema.org/a/MzxU6PcNGluvAJMLWGEqxAvmA.js" data-autoplay="true" data-loop="true" async></script>

[Source](https://gitlab.com/matrix8967/gutter_bonez/-/raw/master/EdgeOS.yml)