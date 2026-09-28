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
remarks = "operator and evidence summary"
source = "https://..."
```

`[[validator]]`: remarks about one validator. If it is also in a group, its keys override the
group's keys of the same name.

```toml
[[validator]]
vote = "VOTE_ACCOUNT"
[validator.metadata]
remarks = "..."
source = "https://..."
```

## Rules

- Vote accounts only, not identity keys.
- A vote account belongs to at most one group. Do not repeat the anchor in `votes`.
- `metadata`: a few short text fields. Always include `source`: a link, or how the claim can be verified.
- No personal data. Everything in this file is public.

## Contributing

Open a pull request that edits `alias.toml`, one entity per pull request. State the evidence in
the description. Unverifiable claims are not merged.

## License

MIT
