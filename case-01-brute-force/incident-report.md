# Incident Report IR-2026-001

## Summary

On 28 July 2026, synthetic identity telemetry recorded eight failed authentication attempts against `analyst@contoso.example`, followed by a successful sign-in from the same external address. The successful session originated from an unmanaged Windows browser. The event is classified as a high-severity true positive pending expanded evidence and user validation.

## Classification

| Field | Value |
|---|---|
| Category | Credential attack / account compromise |
| Severity | High |
| Status | Escalated for containment |
| Confidence | High |
| Data affected | Unknown |
| Business impact | Potential unauthorised access to cloud data and services |

## Detection and analysis

The detection correlates repeated failures with a later success for the same user and source address. The short interval, unmanaged-device context, and differing later sign-in context increase confidence. Location data is treated only as supporting evidence because VPNs and carrier routing can affect geolocation.

## Actions required

| Priority | Owner | Action | Completion evidence |
|---|---|---|---|
| P1 | Identity team | Block account and revoke sessions | Entra action record |
| P1 | Service desk | Verify user and reset credentials | Verified ticket notes |
| P1 | SOC | Hunt source across identities and applications | Saved hunting results |
| P2 | SOC | Review post-authentication activity | Investigation timeline |
| P2 | Security engineering | Assess MFA and Conditional Access coverage | Control review |

## Communication

Notify the incident lead, identity team, service desk, and data owner according to the incident response plan. Escalate to privacy, legal, or management if evidence indicates regulated-data access or material business impact.

## Closure criteria

- The affected identity has been verified and secured.
- Tokens and sessions have been revoked.
- Malicious persistence and post-authentication activity have been assessed.
- Required notifications are complete.
- Detection tuning and lessons learned are documented.

