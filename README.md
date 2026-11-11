# Incident Management

The common incident-management vocabulary -- incidents and the updates posted as they unfold, the services they affect, the on-call schedules and escalation policies that page people, the status pages that tell customers and the postmortems that follow -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Incident Management, Incident Response, On-Call, Alerting, Status Page, Status Pages, SRE, Site Reliability Engineering in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| incident | 27 | 24 | id 88%, name 71%, severity 71%, status 71%, created_at 58% | incidents 24, incident 6 |
| incident_update | 10 | 7 | created_at 86%, id 86%, body 57% | updates 3, events 3, notes 2, incident_updates 2 |
| service | 11 | 10 | name 100%, description 80%, id 70%, created_at 50% | services 8, components 3, service 1, business_services 1 |
| on_call_schedule | 11 | 11 | name 91%, id 82%, description 64%, time_zone 64%, created_at 55% | schedules 10, on-calls 2, oncalls 1, oncall 1 |
| escalation_policy | 7 | 7 | name 100%, id 71%, description 57%, rules 57% | escalation_policies 3, escalations 3, escalation-policies 1 |
| status_page | 10 | 10 | name 80%, id 70%, subdomain 60% | status-pages 5, status_pages 3, statuspages 2, pages 1 |

Cohort: 75 providers with harvested OpenAPI, 28 crosswalks. Of the providers exposing a incident: 63% create, 78% list, 82% fetch, 44% update, 41% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- An incident agrees on id, title, severity, status and created_at: PagerDuty, incident.io, FireHydrant and Opsgenie map 80-100% of it -- they share the shape of an outage.
- On-call schedules and escalation policies agree almost completely where they exist -- name, description, time zone, rules -- and PagerDuty's shape is everyone's.
- Postmortems are barely published (3 providers): the retrospective lives in a document, not an API.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [arazzo.yml](arazzo.yml) -- reference workflows composed only of the shared operations (compositions, not measurements).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- An ITSM incident (ServiceNow) is a ticket and stays in the help-desk context; an incident here is an operational one -- something is broken and people are paged.
- Security incidents from SOAR and XDR platforms are kept as incidents: same lifecycle, though their event timelines carry security context.
- Updates cover incident updates, timeline events, notes and log entries beneath an incident.
- Status-page components are services: the thing customers see as up or down.
- Schedules, on-calls and rotations are one concept, `on_call_schedule`.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
