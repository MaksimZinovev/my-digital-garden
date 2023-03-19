---
{"dg-publish":true,"permalink":"/digital-garden/create-subdomain-in-hostinger-and-connect-to-vercel-app/","created":"","updated":""}
---

Links: [[digital-garden/digital garden MOC\|digital garden MOC]]


# create subdomain in Hostinger and connect to Vercel app


Main steps

1. Create subdomain in hostinger: Hostinger dashboard > clickworks.me > Manager > Domains > subdomains > enter subdomain > Create
2. Create custom domain in Vercel: Vercel project > Settings > add subdomain 'garden.clickworks.me' > add > Copy nameservers (e.g. `ns1.vercel-dns.com`)
3. Add NS record in Hostinger > Type > NS > Name garden > Content  `ns1.vercel-dns.com`
5. Find Add A record in Vercel: Vercel > Domains > clicckworks.me > DNS Records > find A record > copy `76.76.21.21`
6. Add A record in Hostinger > Type > A > Name garden > Content  `76.76.21.21


![[create subdomain in hostinger and connect to vercel app-1679197910118.jpeg\|create subdomain in hostinger and connect to vercel app-1679197910118.jpeg]]


![[create subdomain in hostinger and connect to vercel app-1679198097025.jpeg\|create subdomain in hostinger and connect to vercel app-1679198097025.jpeg]]