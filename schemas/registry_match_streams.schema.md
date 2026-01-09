# Schema: Registry Match Streams

**Purpose:** registry output crosswalks that tell participants which endpoints to monitor.

### Payer match stream
`[Beneficiary_Endpoint_URL] → [Hub_User_Endpoint_URLs...]`

### Provider match stream
`[Patient_Endpoint_URL] → [Payer_Beneficiary_Endpoint_URLs...]`

### Hub match stream
`[User_Endpoint_URL] → [Payer_Beneficiary_Endpoint_URLs...]`

STP row format is identical to core STP (`+` replace, `-` delete).
