# Schema: Signal + Channel

> DEMIURGE-004

## Signal

A message between agents or departments.

```yaml
Signal:
  id: string                # uuid
  type: enum                # direct | group | dept_broadcast | cross_dept
  sender_id: string         # Agent id
  sender_dept_id: string    # optional context
  recipients:
    - type: enum            # agent | department | channel
      id: string
  channel_id: string        # optional, if routed via channel
  payload: object           # structured JSON per SignalType schema
  priority: enum            # normal | urgent | critical
  quorum_required: string   # Quorum id or null
  routing_tags: string[]    # Router dispatch hints
  created_at: iso8601
  expires_at: iso8601       # deadline for reaction
  status: enum              # pending | delivered | quorum_met | expired | escalated
  reactions: Reaction[]     # agent responses
```

## Reaction

An agent's response to a signal.

```yaml
Reaction:
  agent_id: string
  reacted_at: iso8601
  action: enum              # ack | approve | reject | delegate | complete
  payload: object           # optional structured response
  within_sla: boolean
```

## Channel

Communication pathway signals travel through.

```yaml
Channel:
  id: string
  name: string
  type: enum                # direct | group | dept | broadcast | cross_dept
  members:
    - type: enum            # agent | department
      id: string
  router_id: string         # Router agent managing this channel
  retention_days: int       # default 90
  allowed_signal_types: string[]
  description: string
```

## Signal type matrix

| type | Scope | Example |
|------|-------|---------|
| direct | Agent → Agent | Sales lead → proposal drafter |
| group | Agent → named group | Marketing content review circle |
| dept_broadcast | Agent → whole dept | Product insight to all Marketing |
| cross_dept | Dept → Dept | Marketing content-ready → Sales |

## Payload conventions

All payloads include:

```json
{
  "signal_version": "1.0",
  "subject": "string",
  "body": "string or markdown",
  "artifacts": [{"path": "...", "type": "markdown|json|url"}],
  "correlation_id": "uuid",
  "source_run_id": "cron or manual run id"
}
```

## Priority handling

| priority | Router behavior |
|----------|-----------------|
| normal | Next cadence slot or within 4h |
| urgent | Within 1h, notify if unacked |
| critical | Immediate dispatch, escalate at 30m |

## Validation checklist

- [ ] Every cross_dept signal has routing_tags
- [ ] expires_at set for urgent/critical
- [ ] payload validates against SignalType schema
- [ ] sender is active agent
