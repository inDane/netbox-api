# netbox-api

A [Hermes Agent](https://github.com/NousResearch/hermes-agent) skill for driving a NetBox instance over its REST API — batch device relocations, renames, cable sweeps, and IP assignment, with the pre-verify / read-back discipline that keeps batch writes auditable.

Verified against NetBox 4.6.8 (field behavior checked against the tagged upstream source).

## Install (Hermes)

```bash
# subscribe to this repo as a skill tap
hermes skills tap add <owner>/netbox-api

# then install the skill
hermes skills install netbox-api
```

## What's inside

```
skills/netbox-api/
├── SKILL.md                                  # main skill: field gotchas, common ops, pagination
├── references/
│   ├── netbox-api.md                         # field-level quick reference
│   └── batch-device-operations.md            # full verified recipe (21-node relocate, 68-cable sweep)
└── scripts/
    └── netbox_api.py                         # minimal REST CLI (get/patch/delete/all, follows `next`)
```

## Script usage

```bash
export NETBOX_BASE=https://netbox.example.com
# token: --token *** flag or ~/.config/netbox/token (chmod 600)

netbox_api.py all "/api/dcim/devices/?limit=500&fields=name,rack,position,site"
netbox_api.py patch /api/dcim/devices/42/ '{"position": 7}'
```

## ClawHub

Importable via [ClawHub's GitHub import](https://clawhub.ai/import) (public, non-fork repo owned by the account importing it).
