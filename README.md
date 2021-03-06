# STIX/MISP Security Playbook Object Conversion
 
**This repository provides a mapping table and a reference process that allows converting between STIX 2.1 Course of Action objects that make use of the [Security Playbook extension](https://github.com/fovea-research/stix2.1-coa-playbook-extension) and [MISP Security Playbook objects](https://github.com/MISP/misp-objects/blob/main/objects/security-playbook/definition.json).**

Machine-readable `security playbook` objects are used to manage, store, and share cybersecurity playbooks and orchestration workflows and can integrate with other machine-readable Cyber Threat Intelligence (CTI) objects to provide additional context and, consequently, support cybersecurity automation.
<p align="center">
  <img src="/misp-stix.png"/>
</p>


* Sharing cybersecurity playbooks using STIX 2.1 has been proposed, developed, and documented in the following GitHub repository
(https://github.com/fovea-research/stix2.1-coa-playbook-extension). In particular, the STIX 2.1 Extension Definition mechanism was used to extend the Course of Action SDO type to support including descriptive metadata about playbooks and "encapsulate" cybersecurity playbooks for sharing purposes.

* Sharing cybersecurity playbooks using MISP motivated the development of a security-playbook object and was made available in the official MISP Project GitHub
(https://github.com/MISP/misp-objects/blob/main/objects/security-playbook/definition.json).

This repository provides a mapping table that allows converting between `STIX 2.1 Course of Action objects that make use of the Security Playbook extension` and `MISP Security Playbook objects`. Specifically, the mapping table associates the properties that comprise a security playbook extension using the STIX 2.1 COA SDO and the properties that comprise a MISP security playbook object. In addition we recommend implementers to follow the conversion process below to minimize losing information during the conversion process.

A reference conversion process is as follows:

* From STIX 2.1 Course of Action object with Security Playbook extension to MISP Security Playbook object:
<p align="left">
  <img src="/stix-to-misp-translation.png"/>
</p>

* From MISP Security Playbook object to STIX 2.1 Course of Action object with Security Playbook extension:
<p align="left">
  <img src="/misp-to-stix-translation.png"/>
</p>

### Mapping table for STIX 2.1 Security Playbook extension and MISP Security Playbook object
|STIX Property Name| STIX Data Type| STIX Description | MISP Attribute Name | MISP Data Type | MISP Description |
| :--- | :--- |:--- | :--- | :--- |:--- |
|According to the STIX 2.1 specification, an Extension requires the following property: <br></br> **type** (required)|`string`|The value of this property **MUST** be *playbook*.|-|-|-|
|According to the STIX 2.1 specification, an Extension requires the following property: <br></br> **extension_type** (required) |`string`|The value of this property **MUST** be *property-extension*.|-|-|-|
|**playbook_id** (required)|`string`|A value that uniquely identifies the playbook. If the playbook itself embeds an identifier then the playbook_id **SHOULD** use the same identifier (value). If not, the producer **MAY** generate a unique identifier for the playbook.| **playbook-id** (required)| `text` | A value that uniquely identifies the playbook. If the playbook itself embeds an identifier then the playbook-id **SHOULD** use the same identifier (value). If not, the producer **MAY** generate a unique identifier for the playbook. |
|**description** (optional)|`string`|An explanation, details, and more context about what this playbook does and tries to accomplish.| **description** (optional)| `text` | An explanation, details, and more context about what this playbook does and tries to accomplish. |
| **created** (required)| `timestamp` | The time at which the extension (sub-component instance) was created. This may be different than the time at which the "parent" COA object instance was created.| -|-|-|
| **modified** (required)| `timestamp` | The time at which the extension (sub-component instance) was last modified. |||
| **revoked** (optional)| `boolean` | A boolean that identifies if the playbook (COA sub-component instance) is no longer valid.| **revoked** (optional)| `boolean` | A boolean that identifies if the playbook is no longer valid (revoked). |
| **playbook_creation_time** (optional)| `timestamp` | The time at which the playbook was originally created. | **playbook-creation-time** (optional)| `datetime` | The date and time at which the playbook was originally created. |
| **playbook_modification_time** (optional)| `timestamp` | The time at which the playbook was last modified. | **playbook-modification-time** (optional)| `datetime` | The date and time at which the playbook was last modified. |
| **playbook_valid_from** (optional)| `timestamp` | The time from which the playbook is considered valid and the steps that it contains can be executed. | **playbook-valid-from** (optional)| `datetime` | The date and time from which the playbook is considered valid and the steps that it contains can be executed. |
| **playbook_valid_until** (optional)| `timestamp` | The time from which the playbook should no longer be considered a valid playbook to be executed. | **playbook-valid-until** (optional)| `datetime` | The date and time from which the playbook should no longer be considered a valid playbook to be executed. |
| **playbook_creator** (optional)| `identifier` | The identifier of the entity that created the playbook. | **playbook-creator** (optional)| `text` | The entity that created the playbook. It can be a natural person or an organization. It may be represented using a unique identifier that identifies the creator. |
| **labels** (optional)| `list` of type `string` | A set of labels for the playbook (e.g., adversary persona names, associated groups, or malware family/variant/name that this playbook is related to). | **labels** (optional)| `text` | Labels for this playbook (e.g., adversary persona names, associated groups, malware family/variant/name that this playbook is related to). Another option is to use MISP tags, taxonomies, and galaxies. |
| **organization_type** (optional)| `list` of type `open-vocab` | The type of organization that the playbook is intended for. The value for this property **SHOULD** come from the `industry-sector-ov` open vocabulary.| **organization-type** (optional)| `text` | The type of organization that the playbook is intended for. This can be an industry sector. Another option is to use MISP tags, taxonomies, and galaxies.|
| **playbook_standard** (optional)| `string` | The standard/format/notation the playbook conforms to (e.g., CACAO, BPMN). | **playbook-standard** (optional)| `text` | The standard/format/notation the playbook conforms to (e.g., CACAO, BPMN). |
| **playbook_abstraction** (optional)| `open-vocab` | The playbook???s level of abstraction (with regards to consumption). Open Vocabulary: `[template, executable]` | **playbook-abstraction** (optional)| `text` | The playbook???s level of abstraction (with regards to consumption). Listed options: `[template, executable]` |
| **playbook_type** (optional)| `list` of type `open-vocab` | The security-related functions the playbook supports. A playbook may account for multiple types (e.g., detection and investigation). The open vocabulary is based on the available options in the CACAO standard and NIST SP 800-61 rev2. Open Vocabulary: `[notification, detection, investigation, prevention, mitigation, remediation, analysis, containment, eradication, recovery, attack]` | **playbook-type** (optional)| `text` | The security-related functions the playbook supports. A playbook may account for multiple types (e.g., detection and investigation). The listed options are based on the CACAO standard and NIST SP 800-61 rev2. Another option is to use MISP tags, taxonomies, and galaxies. Listed options: `[notification, detection, investigation, prevention, mitigation, remediation, analysis, containment, eradication, recovery, attack]` |
| **playbook_impact** (optional)| `integer` | From 0 to 100, an integer representing the impact the playbook has on the organization. A value of 0 means specifically undefined. Impact values range from 1, the lowest impact, to a value of 100, the highest. For example, a purely investigative playbook that is non-invasive could have a low impact value of 1. In contrast, a playbook that performs changes such as adding rules into a firewall should have a higher impact value. | **playbook-impact** (optional)| `text` | From 0 to 100, a value representing the impact the playbook has on the organization. A value of 0 means specifically undefined. Impact values range from 1, the lowest impact, to a value of 100, the highest. For example, a purely investigative playbook that is non-invasive could have a low impact value of 1. In contrast, a playbook that performs changes such as adding rules into a firewall should have a higher impact value. |
| **playbook_severity** (optional)| `integer` | From 0 to 100, an integer representing the seriousness of the conditions that this playbook addresses. A value of 0 means specifically undefined. Severity values range from 1, the lowest severity, to a value of 100, the highest. | **playbook-severity** (optional)| `text` | From 0 to 100, a value representing the seriousness of the conditions that this playbook addresses. A value of 0 means specifically undefined. Severity values range from 1, the lowest severity, to a value of 100, the highest. |
| **playbook_priority** (optional)| `integer` | From 0 to 100, an integer representing the priority of this playbook relative to other defined playbooks. A value of 0 means specifically undefined. Priority values range from 1, the highest priority, to a value of 100, the lowest. | **playbook-priority** (optional)| `text` | From 0 to 100, a value representing the priority of this playbook relative to other defined playbooks. A value of 0 means specifically undefined. Priority values range from 1, the highest priority, to a value of 100, the lowest. |
|-|-|-| **playbook-file** (requiredOneOf)| `attachment` | The entire playbook file/document in its native format (e.g., CACAO JSON or BPMN). |
| **playbook_bin** (optional)| `binary` | The entire playbook encoded in base64. Security playbook producers and consumers use this property to share and retrieve playbooks. | **playbook-base64** (requiredOneOf)| `text` | The entire playbook encoded in base64. |

## Acknowledgments
This research was partially supported by the research project JCOP (Grant No. INEA/CEF/ICT/A2020/2373266), funded by the European Health and Digital Executive Agency through the Connected Europe Facility (CEF) program. 
