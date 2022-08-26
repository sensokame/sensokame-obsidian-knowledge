# Principles of security
## The CIA triad
this is an information security model that is used in consideration through creating security policies.
This model consists of three sections, These sections are a continuous cycle.
### Confidentiality
This element is the protection of data from unauthorised access and misuse.
### Integrity
Integrity is the condition where information is kept accurate and consistent unless authorised changes are made.
### Availability
In order for data to be useful, it must be accessible to the user.
> Basically this triad means that data should be available to people who are authorised to access it and should only be modifiable to people who are authorised to do so.

## Principles of privileges
It is viral to correctly define the various levels of access to an information system individuals require. basically you don't give more information than needed to a user.
The levels of access are determined by two factors:
- the individual's role/function in an organisation
- the sensitivity of the information being stored.
the two concepts used to assign and manage the access are Privileged identity management (PIM) and privileged access management (PAM)
### PIM
PIM is used to translate a user's role within an organisation into an access role on a system
### PAM 
PAM is the management of the privileges a system's access role has.
> as stated earlier, we should handle access control with the principle of least privilege, users should be given the minimum amount of privileges which can then be elevated only when needed.
> PAM also encompasses enforcing security policies such as password management. 

## Threat Modelling & Incident Response
Threat modelling is the process of reviewing, improving and testing the security protocols in place.
A critical stage is identifying likely threats that an application or system may face.
A threat modelling process is very similar to risk assessment, the principles all return to:
- preparation
- identification
- mitigation
- review
an effective threat model should also include
- [[Threat Intelligence]]
- Asset identification
- mitigation capabilities
- Risk assessment

There are frameworks to help with threat models, such as STRIDE ([[spoofing]] identity, tampering with data, repudiation threats, information disclosure, [[denial of service]] and [[elevation of privileges]]) and PASTA (process for attack simulation and threat analysis)

## incidents

incidents are classified using a rating or urgency and impact using a matrix.

incidents are usually responded to by a Computer Security Incident Response Team (CSIRT) which is a prearranged group of employees with technical knowledge about the system. usually this team would take the following steps of to respond to an incident.
- Preparation
- Identification
- Containment
- Eradication
- Recovery
- Lessons Learned
