# Example: Provider↔Hub Endpoint Exchange

**Provider discovers:** `Hub_User_Endpoint_URL`

1) Provider → Hub (announce + share provider manifest URL)

```
POST Hub_User_Endpoint_URL
Content-Type: application/x-www-form-urlencoded

table=https://prov.com/stp/provider_manifest
```

2) Hub → Provider (fetch provider manifest)

```
GET https://prov.com/stp/provider_manifest?since_id=0
Accept: application/stp+tsv; schema=endpoint_manifest; version=1
```

3) Provider → Hub (fetch hub manifest)

```
GET Hub_User_Endpoint_URL?since_id=0
Accept: application/stp+tsv; schema=endpoint_manifest; version=1
```

If hub endpoints change, hub notifies provider:

```
POST https://prov.com/notify
Content-Type: application/x-www-form-urlencoded

table=https://hub.com/stp/hub_manifest
```

Provider re-GETs hub manifest (authoritative).
