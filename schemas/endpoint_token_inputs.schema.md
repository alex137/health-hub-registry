# Schema: Endpoint→Token Inputs (Registry Inputs)

**Purpose:** allows payers/providers/hubs to publish endpoint URLs keyed by ephemeral match tokens.

STP rows:

`[SeqNo] \t [TS] \t [+/-] \t [Endpoint_URL] \t [EMTP_Tokens...]`

- Primary key: `Endpoint_URL`
- Record: whitespace-separated token list (hex)
- `- Endpoint_URL` revokes the binding
