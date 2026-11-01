# geoip-city-data

Sharded binary index of the **DB-IP IP to City Lite** database (2026-11 edition),
compiled for the GeoIP API worker. The worker fetches these files through the
jsDelivr CDN (`https://cdn.jsdelivr.net/gh/binbin7418-dotcom/geoip-city-data@main/dbip/...`).

## Layout

- `dbip/meta.json` — index metadata (row counts, shard layout, format).
- `dbip/v4-NNN.bin` — IPv4 shards (224 files). Records are (start, dictId)
  pairs; a record covers [start, next record's start). dictId 0 = no data.
- `dbip/v6-HHHH.bin` — IPv6 shards (82 files), keyed by the first two address
  bytes; records are (16-byte start, dictId).
- `dbip/dict-idx-K.bin`, `dbip/dict-str-K.bin` — city dictionary shards
  (9 + 9 files): region/city strings plus coordinates and country codes.

## License and attribution

The underlying database is the free **IP to City Lite** database by DB-IP,
licensed under the Creative Commons Attribution 4.0 International License
(CC BY 4.0). You are free to use and redistribute this data, provided you give
attribution to DB-IP.com.

> IP Geolocation by DB-IP — https://db-ip.com
> Source database: https://db-ip.com/db/download/ip-to-city-lite

The compiled index in this repository is a redistribution of that database in
a derived binary format and carries the same attribution requirement.
