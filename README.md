# alias.toml

Hand-maintained dataset of Solana validator relationships, keyed by vote account.

## Format

One file: `alias.toml`. Two entry types, each with its own metadata.

`[[group]]`: validators linked to the same entity. `anchor` is the member the group is named
after (its on-chain name is used); `votes` lists the other members.

```toml
[[group]]
anchor = "ANCHOR_VOTE_ACCOUNT"
votes = ["MEMBER_VOTE_ACCOUNT", "MEMBER_VOTE_ACCOUNT"]
[group.metadata]
level = "warning"
info = "One operator: shared withdraw authority"
details = "What was observed and how it links the members"
sources = ["https://..."]
credit = "Who found it"
```

`[[validator]]`: an entry about one vote account. It is separate from any group the vote
account belongs to and never changes the group's entry.

```toml
[[validator]]
vote = "VOTE_ACCOUNT"
[validator.metadata]
level = "note"
info = "..."
sources = ["https://..."]
```

## Metadata

Same fields for `[[group]]` and `[[validator]]` entries:

| Field | Required | Content |
|---|---|---|
| `level` | yes | `warning`, `info` or `note` (one lowercase word a-z, 16 max) |
| `info` | yes | one line, 120 characters max |
| `details` | no | one paragraph without line breaks, 500 characters max |
| `sources` | no | non-empty list of `https://` links (300 characters max each) that let anyone verify the claim |
| `credit` | no | who found it, 120 characters max |
| any other | no | e.g. `website`: text or a non-empty list of texts, 500 characters max each; name in lowercase letters, digits and `_`, 32 max |

Plain text only: no control or invisible characters, no nested tables. At most 10 extra fields
per entry and 20 items per list.

## Levels

| Level | Use |
|---|---|
| `warning` | a negative finding, e.g. several validators under one hidden operator |
| `info` | an informative fact |
| `note` | a passive remark |

## Rules

- Vote accounts only, not identity keys.
- A vote account belongs to at most one group. Do not repeat the anchor in `votes`.
- One `[[validator]]` entry per vote account.
- State only what can be verified from the listed sources.
- No personal data. Everything in this file is public.

## Contributing

Open a pull request that edits `alias.toml`, one entity per pull request. Explain in the
description how the sources support the claim. Unverifiable claims are not merged.

## License

MIT
