API Gateway Throttling

- Backend (Lambda/Database) ko sudden traffic surge (tufan) se bachane ke liye gate par speed-breaker lagana.

- Throttling: Limits lagana (e.g., max 1,000 req/sec) taake extra requests ruk jayen (Error 429) aur backend crash na ho.



So:

> API Gateway = It manages/receives API requests and sends them to your backend.

It is NOT your application itself.


24-August-2026
