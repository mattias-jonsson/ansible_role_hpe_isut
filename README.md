Ansible Role: ansible_role_hpe_isut
=========
Installs and configures HPE iSUT on the following Linux distributions:

<ul>
<li>Red Hat Enterprise Linux 7/8
</ul>

Requirements
------------

None.

Role Variables
--------------

Available variables are listed below, along with default values where applicable (see `defaults/main.yml`):

| Variable | Required | Default | Comments |
| -------- | -------- | ------- | -------- |
| `mode` | No | OnDemand | Selects the mode iSUT uses. Possible values are: `AutoStage` (stages components to the server), `AutoDeploy` (stages and deploys the components), `AutoDeployReboot` (stages, deploys, and if necessary, reboots the server), `OnDemand` (iSUT deploys updates when the admin issues commands). |
| `stagingdirectory` | No | /var/tmp/sut/stagingdirectory | Specifies the directory where iSUT stages components. |
| `rebootmessage` | No | Rebooting this server | Reboot message. |
| `rebootdelay` | No | 60 | The number of seconds before iSUT reboots the node. |
| `pollingintervalinminutes` | No | 5 | How frequently iSUT requests information from SUM, HPE OneView or iLO Amplifier Pack. |
| `savelogs` | No | true | Selects whether iSUT saves the log files. |
| `enableiloqueuedupdates` | No | true | Valid for iLO 5 nodes only. If true, iSUT polls the iLO for any updates in the iLO Installation Queue. |
| `ilousername` | No |  | Not yet implemented. |
| `ignorewarnings` | No | false | Ignores warnings iSUT encounters during deployment. |


Dependencies
------------

This role depends on https://github.com/mattias-jonsson/ansible_role_hpe_spp_repo

Example Playbook
----------------

Joins the system to the test.domain.com domain and also loads SSH keys from the altSecurityIdentities LDAP attribute.

    - hosts: servers

      vars:
        ansible_role_hpe_isut_options:
          mode: 'OnDemand'
          stagingdirectory: '/var/tmp/sut/stagingdirectory'
          rebootmessage: 'Rebooting this server'
          rebootdelay: '60'
          pollingintervalinminutes: '5'
          savelogs: 'true'
          enableiloqueuedupdates: 'true'
          ilousername: ''
          ignorewarnings: 'false'


      roles:
        - ansible_role_hpe_isut

License
-------

MIT

Author Information
------------------

Mattias Jonsson

