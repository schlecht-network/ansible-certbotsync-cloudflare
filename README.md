# ansible-certbotsync-cloudflare

This role allows to automatically deploy lets encrypt certificates to multiple machines or to be more specific it prepares a ubuntu server machine to do that.

```
certificates:
  - name: "example"                                         #descriptive name for this certificate
    certbot_domains:                                        #domains/subdomains to request a cert for
      - "example.exam"
      - "*.example.exam"
    certbot_email: "example@examplemail.exam"               #email address for letsencrypt
    cloudflare_api_token: "someverylongapikey12894782375"   #cloudflare api toke (not global api key!!!)
    ssh_target_hosts:                                       #target ssh hosts to push certificates to
      - host1
    cert_ssh_copydest:                                      #destination path for the cert file (on ssh target machine)
    chain_ssh_copydest:                                     #destination path for the chain file (on ssh target machine)
    fullchain_ssh_copydest:                                 #destination path for the fullchain file (on ssh target machine)
    privkey_ssh_copydest:                                   #destination path for the privkey file (on ssh target machine)
    ssh_destination_owner: root                             #owner of the copied files (on ssh target machine)
    ssh_destination_group: root                             #group of the copied files (on ssh target machine)
    ssh_destination_mode: '0600'                            #mode (access permissions) of the copied files (on ssh target machine)
    aftercopy_ssh_restart_services:                         #services to restart after copying (on ssh target machine)
      - postfix
    netscaler:
      nsip: x.x.x.x                                 #nsip of a citrix netscaler (for netscaler target machine)
      user: nsroot                                  #netscaler user name (for netscaler target machine)
      pass: nsroot                                  #netscaler password (for netscaler target machine)
      validate_certs: no                            #validate netscaler certificate (for netscaler target machine)
  - name: "example2"
    certbot_domains:
    ...


local_ansible_user:                                         #username for execution of the certdistribution ansible playbook (global option)


strict_hostkeychecking: false/true                          #option for disabling strict host key checking (global option)
```