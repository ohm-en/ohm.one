---
created: 2026-09-28 10:23 1790608984
title: DNS TTL
unlisted: "false"
---
Apparently it's all about cache invalidation. I've been setting DNS records for years without really considering what "Time To Live" (aka TTL) actually meant.

I had assumed it defined how long before changes were replicated from the nameservers, but that's not exactly what's going on.

In reality, it's used to define an expiration date[^2] which is set on record retrieval. This is why DNS replication is difficult to predict; a DNS record could have been passed on at anytime—potentially with an old TTL value.

That's right, each record has its own expiration; so, if your migrating from 24hrs to 300s[^1], you'll find it can in-fact take up to 24hrs for your updated TTL to go into effect.

Furthermore, if you then change record data—like an A or AAAA, it's the same invalidation. Ideally, before your primary changes, you would first update the TTL from Y(24hrs) to a lower X(300s) and wait Y. This allows for a smother transition. 

Once your changes have been made, it's preferred to revert your TTL back to Y as there's no longer good reason to have the user's cache invalidate so frequently–it's a waste of compute.

[^1]: Sometimes referred to as "auto" (Cloudflare)

[^2]: Some user's cache may invalidate sooner. This value should be treated as the last moment the record should be considered valid.


----------------
# History
| Date                  | Change | Time    |
|-----------------------|--------|---------|
| [2026-10-05](b45fe2c) | init   | 62m 32s |
