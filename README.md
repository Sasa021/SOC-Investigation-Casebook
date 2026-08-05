# SOC Investigation Casebook

A practical portfolio of fictional security incidents demonstrating alert triage, KQL analysis, evidence handling, incident classification, MITRE ATT&CK mapping, and response recommendations.

This repository presents my investigation process: establish the facts, test competing explanations, document decisions, and recommend proportionate action. All evidence is synthetic and safe to publish.

## Casebook

| Case | Scenario | Status | Core capabilities |
|---|---|---|---|
| [01](case-01-brute-force/investigation.md) | Password spray followed by a successful sign-in | Complete | KQL, identity analysis, incident response, access control |
| 02 | Phishing email investigation | Planned | Header analysis, IOC extraction, user protection |
| 03 | Suspicious PowerShell activity | Planned | Process analysis, endpoint response, ATT&CK mapping |
| 04 | Impossible-travel alert | Planned | Identity investigation, false-positive analysis, account remediation |

## Case 01 outcome

Synthetic Microsoft Entra sign-in evidence shows eight failed attempts against one account from a single external address, followed by a successful sign-in from that same address. The incident is assessed as a **true positive with high severity** because the sequence is consistent with valid-account compromise and the successful session creates immediate confidentiality and integrity risk.

Key outputs:

- [Investigation narrative](case-01-brute-force/investigation.md)
- [Detection query](case-01-brute-force/detection-query.kql)
- [Synthetic evidence](case-01-brute-force/evidence.csv)
- [Incident report](case-01-brute-force/incident-report.md)
- [SC-200 and ISC2 CC alignment](docs/certification-alignment.md)

## Investigation method

1. Validate the alert and evidence source.
2. Establish a timeline and baseline.
3. Correlate identity, source, location, device, and result data.
4. Consider benign and malicious explanations.
5. Determine disposition and severity.
6. Map observed behaviour to MITRE ATT&CK.
7. Recommend containment, eradication, recovery, and improvements.

## Skills demonstrated

- Microsoft Sentinel-style KQL
- Microsoft Entra sign-in log analysis
- Alert triage and incident classification
- Timeline reconstruction and evidence-based reasoning
- Identity and access-control analysis
- MITRE ATT&CK mapping
- Risk-based containment and recovery recommendations
- Clear technical and management reporting

## Responsible-use statement

This is a defensive portfolio project. Names, domains, addresses, identifiers, and events are mostly fictional. The IP ranges use documentation-only address space. No credentials, live targets, customer information, or confidential employer data are included.

## Disclaimer

This independent project is aligned to publicly available certification objectives. It is not endorsed by, affiliated with, or an official training product of Microsoft, ISC2, or MITRE.

