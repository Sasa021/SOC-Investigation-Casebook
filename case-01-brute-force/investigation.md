# Case 01: Repeated Failures Followed by Successful Sign-in

## Executive assessment

**Disposition:** True positive  
**Severity:** High  
**Confidence:** High  
**Affected identity:** `analyst@contoso.example`

Eight failed sign-ins from `203.0.113.77` were followed by a successful sign-in from the same address 1 minute and 18 seconds after the final failure. The attempt used an unmanaged Windows browser session. A later successful sign-in originated from a different address, location, client type, and managed device. The pattern is consistent with credential compromise and requires immediate identity containment.

## Alert question

Did the failed sign-in sequence represent ordinary user error, automated guessing, or a successful attack against the account?

## Evidence integrity and scope

- Source: synthetic Microsoft Entra-style sign-in records in `evidence.csv`.
- Scope: one identity, two source addresses, and a 20-minute event window.
- Limitation: no audit, mailbox, endpoint, MFA, or user interview evidence is available.
- Documentation addresses `203.0.113.0/24` and `198.51.100.0/24` are deliberately used; they are not live investigation targets.

## Timeline

| Time (UTC) | Event | Analyst interpretation |
|---|---|---|
| 08:00:11–08:08:06 | Eight failures from `203.0.113.77` | Repetition and cadence exceed a likely single typing error |
| 08:09:24 | Successful browser sign-in from the same IP | Strong indicator that a valid password was obtained or guessed |
| 08:20:09 | Successful sign-in from `198.51.100.24` on a managed iOS device | Potential legitimate user activity; creates a location/device inconsistency requiring validation |

## Analysis

### Indicators supporting malicious activity

- Eight failures target the same account within eight minutes.
- A successful sign-in follows shortly after the failures.
- The successful session uses the same source address as the failures.
- The device is unmanaged and differs from the later managed-device session.
- Location and client context differ from the later sign-in.

### Alternative explanations considered

**User mistyped a password repeatedly.** Possible, but weakened by the unmanaged-device context and the later managed-device sign-in from a different location.

**A stale application repeatedly attempted an old password.** Unlikely because the sequence ends in an interactive browser success rather than recurring background failures.

**VPN or mobile routing changed the apparent location.** Possible. Geolocation is supporting context, not proof; the investigation does not rely on location alone.

### Determination

The same-source failure-to-success sequence is the strongest evidence. With no evidence confirming legitimate use of the unmanaged device, the incident is treated as a compromised account until disproved.

## MITRE ATT&CK mapping

| Technique | ID | Evidence-based use |
|---|---|---|
| Brute Force: Password Guessing | T1110.001 | Repeated password failures against one identity |
| Valid Accounts: Cloud Accounts | T1078.004 | Successful access to a cloud application after the failures |

The mapping describes observed behaviour; it does not claim attribution or later attack stages.

## Response recommendations

### Immediate containment

1. Disable or temporarily block the affected account.
2. Revoke active sessions and refresh tokens.
3. Reset the password through a verified identity process.
4. Require MFA re-registration if compromise is confirmed.
5. Block the source indicator where policy and evidence support it, while recognising IP blocking is not sufficient containment.

### Investigation expansion

1. Contact the user through a verified channel to confirm both sign-ins.
2. Review Entra audit logs, MFA events, risky sign-ins, mailbox activity, and cloud application access.
3. Search the source address across other identities to test for password spraying.
4. Inspect post-authentication actions for persistence, data access, privilege changes, and forwarding rules.
5. Review the unmanaged device context in Microsoft Defender XDR if telemetry is available.

### Recovery and improvement

- Restore access only after identity verification and session revocation.
- Apply risk-based Conditional Access and require MFA.
- Tune the analytic rule using normal failure rates, known service accounts, and trusted network context.
- Document lessons learned and measure time to detect, contain, and recover.

## Risk rationale

The successful authentication creates potential confidentiality and integrity impact. Availability impact is currently low, but containment may briefly interrupt the user. High severity is appropriate because valid cloud access could enable data exposure, account misuse, or lateral activity.

## Analyst conclusion

This incident should be escalated and contained as a high-severity true positive. The evidence supports compromise, but the conclusion remains subject to user validation and expanded telemetry.

