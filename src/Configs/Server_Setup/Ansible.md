# Ansible Playbook

-----

## Debian Server Default Config:

```yml,editable
---
- hosts: [all]
  become: true
  vars_files:
    - group_vars/Ubuntu_Default.yml

  vars_prompt:
    - name: "user_name"
      prompt: Desired username?
      private: no

    - name: "hostname"
      prompt: Desired hostname?
      private: no

    - name: "ssh_port"
      prompt: Desired SSH Port?
      private: no

  vars:
    - name: Set timezone to America/Chicago
      timezone: America/Chicago

  tasks:
    - name: Update Apt.
      apt: name=aptitude update_cache=yes state=latest force_apt_get=yes

# User + Group Setup
    - name: Verify 'sudo' group
      group:
        name: sudo
        state: present

    - name: Allow paswordless sudo to sudoers group.
      lineinfile:
        path: /etc/sudoers
        state: present
        regexp: '^%sudo'
        line: '%sudo ALL=(ALL) NOPASSWD: ALL'
        validate: '/usr/sbin/visudo -cf %s'

    - name: Create User.
      user:
        name: "{{ user_name }}"
        state: present
        groups: sudo
        append: true
        create_home: true
        shell: /usr/bin/zsh

    - name: Print message.
      ansible.builtin.debug:
        msg: 'Setting hostname to: {{ hostname }}'

    - name: Set a hostname
      hostname:
        name: "{{ hostname }}"

# Package Install
    - name: Apt Update.
      apt: update_cache=yes

    - name: Apt Upgrade.
      apt:
        upgrade: 'yes'

    - name: Install Default Packages.
      apt: name={{ apt_packages }} state=latest

    - name: Remove ubuntu spyware
      apt:
        name: popularity-contest
        state: absent

    - name: Check if a reboot is needed for Debian-based systems
      stat:
        path: /var/run/reboot-required
      register: reboot_required

    - name: Reboot the server if needed
      reboot:
        msg: "Reboot initiated by Ansible because of reboot required file."
        connect_timeout: 5
        reboot_timeout: 600
        pre_reboot_delay: 0
        post_reboot_delay: 30
        test_command: whoami
      when: reboot_required.stat.exists

    - name: Remove old packages from the cache
      apt:
        autoclean: yes

    - name: Remove dependencies that are no longer needed
      apt:
        autoremove: yes
        purge: yes

    - name: Copy Dotfiles
      copy:
        dest: /home/{{ user_name }}/
        src: home/
        owner: "{{ user_name }}"
        group: "{{ user_name }}"

    - name: Delete MOTD
      file:
        path: /etc/update-motd.d/
        state: absent

    - name: Create MOTD
      file:
        path: /etc/update-motd.d/
        state: directory

    - name: Setup new motd
      copy:
        dest: /etc/update-motd.d/10-motd
        src: etc/update-motd.d/10-motd
        owner: root
        group: root
        mode: a+x

# UFW Setup
    - ufw:
        rule: allow
        port: "{{ ssh_port }}"

    - name: UFW - Deny all except SSH.
      ufw:
        state: enabled
        policy: deny
        direction: incoming

# SSH Key Exchange & Service Reload
    - name: SSH Key Exchange.
      authorized_key:
        user: "{{ user_name }}"
        state: present
        key: "{{ copy_pub_key }}"

    - name: Add hardened SSH config
      copy:
        dest: /etc/ssh/sshd_config
        src: etc/ssh/sshd_config
        owner: root
        group: root
        mode: 0600
      notify: Reload SSH

  handlers:
    - name: Reload SSH
      service:
        name: sshd
        state: reloaded

```

* Prompts for:
    * Desired Username
    * Desired SSH Port.
    * Hostname
* Installs default Packages
* Cleans package cache.
* Test reboot conditional.
* Deletes default Ubuntu MOTD. (Default phones home to load canonical ads.)
* Sets up new user w/ Passwordless `sudo`.
* Sets up default firewall rules (reject all except custom `ssh` definded earlier.)
* SSH Key-Exchange for new user.
* Reload SSH Service.

-----

## Demo:

<script id="asciicast-UoBa5Jw9R5cHHKcpi6Ey3muSC" src="https://asciinema.org/a/UoBa5Jw9R5cHHKcpi6Ey3muSC.js" data-autoplay="true" data-loop="true" async></script>
