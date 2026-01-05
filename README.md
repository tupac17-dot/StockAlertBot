# StockAlertBot (Investor Assistant)

A desktop app that screens a watchlist, generates trading signals, and delivers alerts via GUI, Telegram, and Windows tray. It now supports investor-friendly modes with calmer notifications, daily digests, and per-symbol personalization.

## Key Features
- Multi-timeframe signal engine with smart cooldown and de-duplication across timeframes.
- Investor modes: Daily Investor and Long-Term with calmer per-symbol throttling.
- AI Console for scoped prompts (stocks, alerts, portfolio rules, app settings) with recommendations and audit log.
- AI Proposal workflow to preview/apply AI recommendations with rollback support.
- Daily digest (Telegram): health counts, top movers, and error summary.
- Watchlist tools: add/remove, import/export CSV, pause/mute symbols, remove stale symbols.
- Watchlist selection updates the Notes panel with the latest alert history details.
- Screener: ranks symbols with confidence breakdown (Trend/Structure/Volume/Candle/Risk).
- Price alerts: per-symbol above/below with cooldown to avoid spam, start monitoring after 10:00 ET unless AI pre-market monitoring is enabled.
- Notes alerts: create freeform notes with optional scheduled reminders (Telegram/Windows).
- Portfolio: track open positions and trade journal with persistent local storage.
- Portfolio alerts: configurable sell rules (profit target, trailing stop, daily trend break, time-based exit).
- Portfolio risk checks: market-open fall risk scoring with optional notifications.
- Personalization: per-symbol ATR stop multiplier and score bias (stored locally).
- Notifications: GUI log, Telegram, and Windows tray with per-category Telegram toggles.
- Dashboard: LIVE/STALE/OFFLINE counts, top movers, and symbols with errors.
- Backtest + Research: simulate strategies, compare runs, and export strategy research reports.
- Settings/tests: test Alerts/Yahoo/Notifications from the UI, configure AI providers and models.
- Settings transfer + sync: import/export settings or sync watchlists/alerts/personalization to an endpoint.

<img width="2002" height="1006" alt="image" src="https://github.com/user-attachments/assets/6d73f013-92c6-4f95-ab11-5189d85557ad" />

<img width="3439" height="1415" alt="image" src="https://github.com/user-attachments/assets/a78725bd-5df6-4ac9-91fa-46204a4feb20" />

<img width="3439" height="1365" alt="image" src="https://github.com/user-attachments/assets/dda7630c-6d5d-4e36-a7bf-6e28b92496dc" />


## Usage Notes
- Configure alerts in-app (Menu > Configure > Alerts) and use test buttons to verify. Toggle which alert types
  (Price Alerts, Alert Rules, Portfolio Alerts) send messages and enable/disable Windows alerts.
- Choose mode (Daily Investor / Long-Term / AI) before starting the bot.
- Right-click watchlist/screener rows for actions (mute, pause, personalize, open chart, add alert).
- Portfolio tab includes open positions, trade journal, and portfolio alerts with sell-rule rationale.
- Daily digest sends once per day after market close (Telegram).

## AI Features
### AI Console (AI Assist)
Use the AI Console to ask scoped questions about stocks, alerts, portfolio rules, or app settings. The console
injects current app context (strategy config, portfolio rules, screener weights) and keeps an audit log of
recommendations.

Example prompts:
- “Summarize my watchlist risk hotspots and suggest alert tweaks.”
- “Propose safer portfolio sell rules for high-volatility positions.”
- “Suggest alert rule changes for NVDA given recent momentum.”

Expected response structure:
- **Reason**: why the suggestion is made.
- **Update Plan**: a concrete plan or summary of what would change.
- **Recommendations**: list items with title, rationale, and impact.
- **Commands**: include `UPDATE_PORTFOLIO_RULES` parameters to enable Apply buttons in the AI Console.

### AI Proposal (Apply & Revert)
The AI Proposal dialog accepts a JSON recommendation payload, shows a preview, and applies changes only after
confirmation. Applied changes are logged and can be rolled back via **AI Console → Revert last change**.

Workflow:
1. Open **AI Proposal** from the menu to copy the current config JSON.
2. Ask your AI to return a recommendation payload (reason, updatePlan, and desired updates).
3. Paste it into the dialog, preview, then Apply.

### AI Settings
Configure your provider in **Settings → AI**:
- **Provider**: OpenAI-compatible or Ollama.
- **API URL**: endpoint for your provider.
- **API token**: auth token for hosted providers.
- **Model**: model name for completions.

### Watchlist AI Bot
Run the watchlist bot in **AI** mode to keep the alert engine in an AI-tuned profile with audit logging when
recommendations are applied.

## Telegram Commands (portfolio)
- `Open Positions NVDA` → reply with Qty, Avg Cost, Last, and P&L %.
- `All open positions` → reply with all open positions and their Qty and P&L %.
- `Add position NVDA 100qty 212.35usd` → add a new position from chat.
