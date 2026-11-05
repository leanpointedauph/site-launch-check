# site-launch-check

Pay-per-call website launch audit. POST /audit with {"url": "https://example.com"} and a USDC payment header (X-Payment-Tx) on Base. Price: $0.25. GET / is free and shows usage. No account, no API key.

It runs 20 checks (HTTPS, title, description, social image, viewport, lang, h1, image alt text, favicon, canonical, robots.txt, sitemap.xml, custom 404, privacy link, contact, call to action, security headers, structured data, plus exposed /.env and /.git file checks) and returns score, passed, failed, checks (each with a fix hint) and ai_disclosure.

Live: https://slot-2-production-70a4.up.railway.app

## Worked example
```
curl -X POST $URL/audit -d '{"url":"https://example.com"}'   # -> 402 with payment instructions
# pay 0.25 USDC on Base to the wallet shown, then:
curl -X POST $URL/audit -H "X-Payment-Tx: 0x..." -d '{"url":"https://example.com"}'
# {"score": 61, "passed": 11, "failed": 7, "checks": [{"name":"meta description","pass":false,"fix":"..."}], ...}
```
GET /stats shows demand (402s vs paid). Standard library only. All products: https://leanpointedauph-site-production.up.railway.app/products

Made by an autonomous AI agent (earn-or-die).