` # Alt SSH for recovery.`
`sudo /usr/sbin/sshd -D -p 2222`

`https://infosec.mozilla.org/guidelines/openssh#recommended-safer-alternatives-to-ssh-agent-forwarding`

https://fedoramagazine.org/using-ansible-to-organize-your-ssh-keys-in-aws/
https://www.redhat.com/sysadmin/secure-session-recording
https://www.redhat.com/sysadmin/session-recording-tlog
https://www.redhat.com/sysadmin/basic-concepts-encryption-cryptography
https://fedoramagazine.org/network-bound-disk-encryption-with-stratis/

https://robotmoon.com/ssh-tunnels/

https://www.vultr.com/docs/how-do-i-generate-ssh-keys
https://www.vultr.com/docs/using-your-ssh-key-to-login-to-non-root-users
https://www.vultr.com/docs/how-to-use-twofactor-authentication-with-ubuntu-20-04
https://www.vultr.com/docs/how-to-configure-encrypted-ftp-for-your-web-server
https://www.vultr.com/docs/how-to-add-and-delete-ssh-keys

https://www.linode.com/docs/guides/use-public-key-authentication-with-ssh/
https://www.linode.com/docs/guides/how-to-use-fail2ban-for-ssh-brute-force-protection/
https://www.linode.com/docs/guides/using-sshfs-on-linux/

https://infosec.mozilla.org/guidelines/openssh

https://linux-audit.com/audit-and-harden-your-ssh-configuration/#ssh-basics

# Teleport
https://goteleport.com/blog/comparing-ssh-keys/
https://goteleport.com/blog/how-to-ssh-properly/
https://goteleport.com/blog/how-to-record-ssh-sessions/
https://goteleport.com/tags/ssh/
https://github.com/gravitational/teleport
https://goteleport.com/docs/getting-started/
https://goteleport.com/blog/ssh-config/

# SSH-Audit
https://github.com/arthepsy/ssh-audit
https://github.com/mozilla/ssh_scan

https://www.cloudflare.com/learning/ssl/how-does-public-key-encryption-work/

https://docs.ansible.com/ansible/latest/collections/amazon/aws/ec2_key_module.html
https://fedoramagazine.org/aws-tools-fedora/
https://github.com/dlabreu/aws/blob/master/ec2_key/playbook.yml
https://fedoramagazine.org/ssh-key-aws-regions/
https://www.redhat.com/sysadmin/ssh-dynamic-port-forwarding

# Keybase SSH
https://keybase.io/blog/keybase-ssh-ca
https://github.com/keybase/bot-sshca

# SSH Certificate Authority
https://docs.github.com/en/github/setting-up-and-managing-organizations-and-teams/about-ssh-certificate-authorities

https://docs.github.com/en/github/setting-up-and-managing-organizations-and-teams/managing-your-organizations-ssh-certificate-authorities

https://github.com/cloudtools/ssh-cert-authority

https://medium.com/better-programming/how-to-use-ssh-certificates-for-scalable-secure-and-more-transparent-server-access-720a87af6617

https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/sec-using_openssh_certificate_authentication

https://ibug.io/blog/2019/12/manage-servers-with-ssh-ca/

https://gist.github.com/kawsark/a9443692a9e4a7b1c7df253995ce864c

# TLDR
An `SSH-Certificate-Authority` will centralize the creation of `SSH` keys ensuring new users can't `read up` out of bounds. The `SSH-CA` will trust the `client` and trust the `server` without the need for the client & server to authenticate directly. This will have the added bonus of enabling faster (& Automated) user account creation and deletion.


https://github.com/willshersystems/ansible-sshd

https://infosec.mozilla.org/guidelines/

https://fedoramagazine.org/configure-ssh-proxy-server/

https://fedoramagazine.org/automating-network-devices-with-ansible/

# tmate
`https://fedoramagazine.org/enable-remote-collaboration-with-tmate-io-on-fedora/`

# StrongDM
* https://github.com/strongdm/comply
* https://www.strongdm.com/blog/who-is-on-your-soc2-team
* https://www.strongdm.com/blog/what-is-soc-2-type-2
* https://www.strongdm.com/blog/ssh-key-management
* https://www.strongdm.com/blog/difference-between-proxy-and-reverse-proxy
* https://www.strongdm.com/blog/bastion-hosts-ssh-logging
* https://www.strongdm.com/blog/scaling-your-ssh-strategy
* https://www.strongdm.com/blog/ssh-audit-log-made-simple
* https://www.strongdm.com/blog/soc-2-policy-templates
* https://www.strongdm.com/blog
* https://github.com/google/grr
