# Beaten-Down Hunter 🔻

Strict dislocation scanner for finding genuinely beaten-down US stocks worth selling long-dated puts on.

## What it does

Scans ~300 US large-cap stocks daily and surfaces 3-7 candidates that:

1. **Pass hard quality gates** — $5B+ cap, 1M+ volume, $5+ price, P/E ≤70, positive FCF, analyst above hold, EPS growth >0%, options chain available
2. **Are genuinely dislocated** — at least 3 of 6 oversold signals fired in the last 14 days (RSI<35, below SMA50 by 10%+, lower Bollinger touched, 1mo perf <-10%, near 52w low, 5y all-time low)
3. **Still in the zone** — current price within 15% of 14-day low (not already recovered)
4. **Pass Claude review** — Claude Opus 4.7 grades each pick STRONG BUY / BUY / SKIP. Only STRONG BUY and BUY make the cut.

## Output

Daily HTML report at `docs/latest.html` (published via GitHub Pages).

Each pick shows:
- Big ticker + scores + bargain price
- 🔻 "DOWN X% from high" pill
- Visual checklist of which dislocation signals fired
- Plain-English company description (Claude)
- Plain-English bullets explaining WHY beaten down + recovery thesis (Claude)
- Long-dated put trade (9-12mo) with safety score (X/10)
- Hero stats: % off 52w high, days oversold, recovery momentum, IV rank
- Support floor ladder + April 2025 tariff stress test
- Sharpened indicator bars (52w range, 50/200 DMA, RSI, Bollinger)
- Latest news with Claude sentiment classification

## Architecture

- `beaten_down_hunter.py` — main scanner
- `render.py` — HTML rendering
- `claude_scorer.py` — Claude API integration
- `.github/workflows/daily.yml` — runs Mon-Fri at 13:00 UTC

## Companion repo

Pairs with [Premium-Hunter](https://github.com/ashimparti/Premium-Hunter) which scans pre-earnings IV opportunities. Together they cover both setups: earnings-driven IV spikes (Premium Hunter) and deep dislocation (Beaten-Down Hunter).
