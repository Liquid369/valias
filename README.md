# alias.toml

Hand-maintained dataset of Solana validator relationships, keyed by vote account.

## Format

One file: `alias.toml`. Two entry types.

`[[group]]`: validators operated by the same entity. `anchor` is the member the group is named
after (its on-chain name is used); `votes` lists the other members.

```toml
[[group]]
anchor = "ANCHOR_VOTE_ACCOUNT"
votes = ["MEMBER_VOTE_ACCOUNT", "MEMBER_VOTE_ACCOUNT"]
[group.metadata]
info = "One operator: shared withdraw authority"
details = "What was observed and how it links the members"
sources = ["https://..."]
credit = "Who found it"
```

`[[validator]]`: a note about one validator. If it is also in a group, its fields override the
group's fields of the same name.

```toml
[[validator]]
vote = "VOTE_ACCOUNT"
[validator.metadata]
info = "..."
sources = ["https://..."]
```

## Metadata

Exactly these fields, nothing else:

| Field | Required | Content |
|---|---|---|
| `info` | yes | one line, 120 characters max |
| `details` | no | 500 characters max |
| `sources` | no | list of links that let anyone verify the claim |
| `credit` | no | who found it, 120 characters max |

Plain text only, no control characters.

## Rules

- Vote accounts only, not identity keys.
- A vote account belongs to at most one group. Do not repeat the anchor in `votes`.
- State only what can be verified from the listed sources.
- No personal data. Everything in this file is public.

## Contributing

Open a pull request that edits `alias.toml`, one entity per pull request. Explain in the
description how the sources support the claim. Unverifiable claims are not merged.

## License

MIT
