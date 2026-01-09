# Schema: Payer Beneficiary Endpoint (Provider View)

`[SeqNo] \t [TS] \t [+/-] \t [Hub_User_Endpoint_URL] \t [optional metadata]`

Semantics:
- Begin/maintain exchange when `+ Hub_User_Endpoint_URL` appears.
- Terminate only when `- Hub_User_Endpoint_URL` is observed from **all payer endpoints returned by the registry**.
