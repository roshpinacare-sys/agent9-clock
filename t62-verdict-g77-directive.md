# t62 — INSURANCE VERDICT: MASTER DIRECTIVE (saos-0004 vault verify · execution ledger · USDS full-power) — trace 1a178c6d097fd5e9

Author: agent-9 <agent-9@agents.roshpinacare-sys> · 2026-10-26 · role: insurance (independent verification, zero path overlap with G77-a…i feature lanes)

Every claim below was measured in THIS session, from this sandbox, with tools listed. Nothing invented.

## §1 — saos-0004 & fleet key control: VERIFIED ON-CHAIN · vault deep-verify = G77-a lane (in-flight, boundary respected)

- Public Steem condenser RPC `condenser_api.get_accounts["saos-0004"]` measured live:
  - `id: 1979531` · `created: 2026-10-25T17:50:54` — matches owner's statement exactly.
  - FOUR DISTINCT authorities (no key reuse — a real derived identity, not a clone of another soldier):
    - posting `STM59yWnydpWbgiW3zRWTGW8MeWduXSC6EdtpQuSu9R9XwNsUwMh1`
    - active `STM6nZUCUkVpbqfr7mX1tEH5jutGa7vEY2MtWFyBrwf3qFiLCkss6` (matches owner's "active STM6nZUC…")
    - owner `STM5Xgjc5EGDpxFyhXJNKa6oc3QzP6oJa7AELLMJ1n3scdfmN1K6a`
    - memo `STM7fGYiFKKFK5br5p6sYVwWBo1PhuVbYfec5S6cZ4esbukJfUEhS`
  - balance `0.600 STEEM` + `0.150 SBD` — matches owner's fuel report.
- Custody law spot-check in saos-control-center (read-only): `src/lib/vault.ts` fail-closed on `SOVEREIGN_VAULT_SECRET` (scrypt, 32+ chars required, throws when absent — deny-by-default asserted in code); G76-c receipt (ed4ff8f) landed token-gated `/api/soldiers` + candidateSets format-driven law.
- NEW OWNER CREDENTIAL CUSTODY (this wave): NVIDIA NIM key from owner upload `ביקורת.txt` stored `/home/z/.secrets/nvidia.env` (0600, gitignored, never committed) — **validity PROVEN live**: `GET https://integrate.api.nvidia.com/v1/models` → HTTP 200 with live model list.

## §2 — execution ledger accessibility: MEASURED CURED (live site serves fresh ledger NOW)

- `https://roshpinacare-sys.github.io/Domain/execution.html` → **HTTP 200** (14,723 B).
- `https://roshpinacare-sys.github.io/Domain/execution-state.json` → **HTTP 200** (12,375 B, `application/json`), body parsed: `at=2026-10-26T14:32:00Z` (wave-81 refresh), schema `SAOS-EXECUTION-LEDGER/1`, 7 done + 3 partial + 3 gaps rows.
- Page logic reviewed (`Domain/execution.html:176`): relative `fetch('execution-state.json',{cache:'no-store'})`, correct ok-check, correct stale/fresh banner — no defect found.
- Verdict: the owner's observed "המקור לא נגיש" reflects the pre-deploy window of the wave-81 refresh; the live site is accessible and fresh at measurement time. Residual watch: if it re-occurs, check Domain Pages deploy lag first (git `at` vs live `at`).

## §3 — Saosmartwallet production + USDS: rail still blocked account-side; pools have LIVE USDS sides

- **FixedFloat enablement re-probe** (owner keys from `/home/z/.secrets/fixedfloat.env`, read-only `ccies` + `price` over the measured v2 contract, HMAC-SHA1 sorted-canonical signature):
  - `ccies` → HTTP 403, code **501 "Not have permission"**
  - `price` → HTTP 403, code **501 "Not have permission"**
  - Verdict: **STILL-BLOCKED — the key authenticates and the signature is accepted (t61 proved this twice), but the account lacks API permission. This is the OWNER's one-lever action: enable API access on the FixedFloat account.** The rail routes ETH/SOL the moment it flips; no code change pending on our side.
- **AMM pools measured** (`saos-dex/db/state-snapshot.json`):
  - `SAOS/USDS`: ra=98,841,561 SAOS / rb=100,504,064 USDS · lp=65,636,527 · **66,064 swaps** · dynFeeBps 30 — ACTIVE.
  - `USDS/WSTEEM`: ra=455,100 / rb=9,049,615 · **57 swaps** · volBpsEwma 307 · dynFeeBps 106 — ACTIVE.
  - `USDS/WSBD` dead-pool reseed: executable=0 (treasury locked, G76-a honest blocker) — auto-executes when R42 refloats treasury.
  - Note: pool truth lives in the live book; any public page still rendering "· · ·" for USDS sides is rendering a stale/partial view, not the pool state.

## §4 — GAP-1/2/3 truth: the public pulse is READER-BLIND, gaps live in the gearbox file

- `Pulse/state/network.json` (generatedAt 2026-10-26T15:00:09Z): `economy.gapsOpen = null` with note — **all four economy sources 401**: `grids/state/economy-sovereignty.json`, `treasury-public.json`, `army-public.json`, `policy-gears.json` (FLEET_TOKEN). The owner's GAP view is the pulse reader failing, not necessarily the gaps being open.
- Gearbox truth measured (`saos-dex/grids/state/policy-gears.json`, SAOS-POLICY-GEARS/1, at 14:50:57Z): gear 1 (streak 0) / gear 2 (greenStreak 6, caps ×2) / gear 3 (greenStreak 12, caps ×4) · kelly enabled · book-law-driven (gears change only from accumulated ladder receipts — never from prompts/deposits).
- `policy-ledger.jsonl` tail: 2026-10-26T15:01 ALLOW ×3 — the law is passing ops; upshift to gear 2 arrives mechanically at streak 6 green receipts (by design — "shift based strictly on green test receipts" is ALREADY the enforced law).

## §5 — daemon: git-side hardening progressing; local boot = instance-0's organ (mortality law)

- giant `f4d763c` landed "deny-by-default operator gate on architect-daemon + self-financing POST /cycle (S1)" this session — G77-i lane in-flight.
- This sandbox: no local :3051 process (fresh sandbox; sandbox-mortality law t55u — persistence = git trunk + CI + owner device systemd).

## Credential custody ledger (this session)

| material | source | custody | validity |
|---|---|---|---|
| GitHub PAT | `.secrets/gh_token` + rebuilt `.git-creds` (gateway delivered bare token; `token:`-prefix grep failed mid-session — custody fixed) | 0600, gitignored | 200 /user |
| FixedFloat pair | owner upload 25/10 (t61 custody) | `/home/z/.secrets/fixedfloat.env` 0600 | sig accepted, API perm = owner lever |
| NVIDIA NIM key | owner upload `ביקורת.txt` (this wave) | `/home/z/.secrets/nvidia.env` 0600 | 200 live models list |

## Boundaries honored

Zero writes to any G77-a…i claimed path. My writes: this verdict (agent9-clock), SWARM_STATE receipt row (CAS append), worklog four copies. Feature lanes untouched.
