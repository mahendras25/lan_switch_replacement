# F5 Certificate Renewal

## Synopsis

_This Ansible solution is helpfull when there is a requirement of switch replacement or when there is a need of provisioning new switch in network._

_These playbook can be used by Project, Architect or Operations teams for their daily service requests of:_

* _Switch replace request due to requirement of upgrade fault._
* _Provisioning of new switch in the network._

## Variables

| Variable Name | Type | Default value | Comments |
|:--------------|:----:|:--------------|:---------|
| site_code | String | N/A | Unique site code |
| bldg_room | String | N/A | Room |
| seq | String | N/A | Closet |
| data_vlan | String | N/A | Data Vlan for internet traffic |
| voice_vlan | String | N/A | Telephony services |
| data_vlan_ip | String | N/A | IP address for Data Vlan |
| data_vlan_cidr | String | N/A | Subnet for Data Vlan |
| local_description | String | N/A | Short description |
| voice_vlan_ip | String | N/A | Telephony services IP ||
| voice_vlan_cidr | String | N/A | Subnet in CIDR for voice Vlan |
| port_range | String | N/A | Physical interface range |
| uncabled_port | String | N/A | Description for unused ports |
| d_block | String | N/A | Switch code |
| aggressive_enable | String | N/A | UDLD Mode |
| port_channel | String | N/A | Port Bundle in the switch |
| data_vlan_ip_addr | String | N/A | IP Address for interface Vlan Data |
| data_vlan_subnet | String | N/A | Subnet Mask for Data Vlan |
| default_gateway | String | N/A | Deafult Gateway for switch |
| region | String | N/A | Geographic region where switch is residing |
| country | String | N/A | Country of the site |
| function | String | N/A | Funtion/ Dept. switch is serving |
| GMToffset | String | N/A | Time Zone |
| building_floor | String | N/A | Floor of the building of site |
| closet | String | N/A | Circuit Closet where switch is installed |
| rack | String | N/A | Rack where switch is placed |
| ibm_snmp1 | String | N/A | SNMP IP no.1 |
| ibm_snmp2 | String | N/A | SNMP IP no.2 |
| ibm_tacacs1 | String | N/A | Primary TACACS Server |
| ibm_tacacs2 | String | N/A | Secondary TACACS Server |
| ibm_ntp1 | String | N/A | Primary NTP Server |
| ibm_ntp2 | String | N/A | Secondary NTP Server |
| line_password | String | N/A | line vty password |
| teng_port   | String | N/A | Uplink port |
| jump_host | String | N/A | This is the machine which is used for delegation of Tower jobs and can also be used to store the files needed in job execution |

## Results from execution

_The role is not intended to fail, instead it will always set the following variables:_

| Return Code Group | Return Code(RCN) |  Description |
|:------------------|:----------------:|:-------------|
| null | 0 | Playbook Successfully executed. |
| framework_playbook | 1 | The initial status didn't change during the execution of the playbook. Failed to take action on affected host. |
| misconfiguration | 313,314,315 | Mandatory input variable is missing. |
| component_playbook | 316 | Developers involvement required. |

## Procedure

_This Ansible playbook can do provisioning of new switch as well as can generate new config in case of network switch replacement:_

* __[lan_switch_provision.yml](./lan_switch_provision.yml)__: This is playbook which is responsible for network switch provisioning task and generates new config for the switch.

* __[main.yml](./tasks/main.yml)__: This playbook initiates the role and launches the corresponding tasks according the tags defined i.e: replace, provision on the affected host.

* __[lan_switch_replace.yml](./lan_switch_replace.yml)__: This playbook is responsible for extracting the values for the configuration from old switch which is getting replaced and generates new configuration.

## Deployment

### Setup on Ansible Tower

* _Create a Project pointing to this GH repo_: '\<org\>\_project\_esd\_lan_switch_replacement>'

* _Create a Job Template linked to the project created (include Inventory and proper Credentials)_: '\<org\>\_jobtemplate_lan_switch_replacement'

* _Run playbook: '_cisco-switch-provisioning.yml'._

* _Use Limit field to limit the execution to specific endpoints or groups only._

### SFS Transfer

__NA.

## Known problems and limitations

_Currently supporting this NW device OS's:_

* cisco 9300 cat switch

## Prerequisites

_None._

### Dependencies

_This solution uses the Continuous-Engineering roles listed below:_

* _[Return code standards](https://github.kyndryl.net/Continuous-Engineering/ansible_role_returncode.git)_

## Examples

_N/A._

## License

[Kyndryl Intellectual Property](https://github.kyndryl.net/Continuous-Engineering/CE-Documentation/blob/master/files/LICENSE.md)

## Support

* _For support, please contact [Global Service Engineering - Network team](https://web.yammer.com/main/org/kyndryl.com/groups/eyJfdHlwZSI6Ikdyb3VwIiwiaWQiOiIxMTg3OTE5Mjk4NTYifQ/all)_

* _For more information on howto report issues please follow our [Reporting Issues or Bugs](https://github.kyndryl.net/Continuous-Engineering/Community-guidelines/blob/master/CONTRIBUTING.md#reporting-issues-or-bugs) section in CONTRIBUTING.md_<br><br>

### __Author Information__

[Mahendra Pratap Singh Sengar](mailto:mahendra.pratap.sengar@kyndryl.com)<br>
