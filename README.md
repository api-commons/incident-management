# Incident Management

The common incident-management vocabulary -- incidents and the updates posted as they unfold, the services they affect, the on-call schedules and escalation policies that page people, the status pages that tell customers and the postmortems that follow -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Incident Management, Incident Response, On-Call, Alerting, Status Page, Status Pages, SRE, Site Reliability Engineering in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
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
