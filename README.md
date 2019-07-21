ansible-gs-iss
=========

![Insurgency Sandstorm](https://steamcdn-a.akamaihd.net/steam/apps/581320/header.jpg)

This role installs a Insurgency Sandstorm server.  

The server can be configured through variables of this role.  
For security reasons, the game server will be running as the system user `steam`.  
A script to `[start|stop|restart|update]` the server will be placed on the target machine.  
If this role is executed without any further configuration, it will set up a server with all default parameters.  
You can find a reference on what parameters you can use and how you need to specify them in this Google doc from the developers: [Google Doc](https://docs.google.com/document/d/1GDLg5p9jjeIya7EgBk0ibzDtDlyQ-U_jpspOzby-JmM/edit)

Requirements
------------

- A user with permissions to execute `sudo` commands without being prompted for password confirmation  
  This user is used to set up the server.


Role Variables
--------------
| Name | Description | Default value |
|---|---|---|
| gsGSLT | Steam game server token. [Doc](https://steamcommunity.com/dev/managegameservers) | <none - __required__ to be set> |
| gsServerName | The name of the server | "ISS Serevr deployed with the ansible role siw36.ansible_gs_iss" |
| gsGamePort | The main server port | 27102 |
| gsQueryPort | The server query port. Used to get information about the server status | 27131 |
| gsAdminList | A list of SteamID64 account IDs that should get admin privileges on the server | <none - not required> |
| gsMapCycleList | A list of maps for the server to cycle through | All maps and modes |
| gsAdditionalParameters | Additional start parameters for the server | <none - not required> |
| gsCustomConfig | Set this parameter to `true` if you have written a custom configuration file in `<role path>/files/custom_Game.ini` | false |
| gsConfigChange | Set this parameter if you want to restart the server with a new custom config file without the installation tasks | false |

Dependencies
------------

This role depends on the following ansible role:
- `siw36.ansible_steamcmd`

Installation:
```bash
# Specify a target directory
ansible-galaxy install -r requirements.yml -p ../roles/
# Install the role to the default ansible role directory
ansible-galaxy install -r requirements.yml
```

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: gameserver-iss
  become: true
  gather_facts: true
  roles:
    - siw36.ansible_steamcmd
    - siw36.ansible_gs_iss
```

License
-------

GNU General Public License v3.0

Author Information
------------------

Created by Robin 'siw36' Klussmann (07/2019)
