# StockAlertBot (Investor Assistant)

A desktop app that screens a watchlist, generates trading signals, and delivers alerts via GUI, Telegram, and Windows tray. It now supports investor-friendly modes with calmer notifications, daily digests, and per-symbol personalization.

## Key Features
- Multi-timeframe signal engine with smart cooldown and de-duplication across timeframes.
- Investor modes: Daily Investor and Long-Term with calmer per-symbol throttling.
- AI Console for scoped prompts (stocks, alerts, portfolio rules, app settings) with recommendations and audit log.
- AI Proposal workflow to preview/apply AI recommendations with rollback support.
- Marketing website template in `marketing-site/` for hosting a product landing page with pricing and reviews.
- Daily digest (Telegram): health counts, top movers, and error summary.
- Watchlist tools: add/remove, import/export CSV, pause/mute symbols, remove stale symbols.
- Watchlist daily change refresh aligns to the current market date with sparkline resets on rollovers for clean day-change baselines.
- Watchlist selection updates the Notes panel with the latest alert history details.
- Screener: ranks symbols with confidence breakdown (Trend/Structure/Volume/Candle/Risk).
- Window sizing clamps to the primary display bounds at launch to avoid oversized windows.
- Price alerts: per-symbol above/below with cooldown to avoid spam, start monitoring after 10:00 ET unless AI pre-market monitoring is enabled.
- Notes alerts: create freeform notes with optional scheduled reminders (Telegram/Windows).
- Alert history controls: filter by symbol, status (All/SUCCEEDED/FAILED/PENDING/N/A), and market-date ranges, export CSV, delete entries, or clear the full history list.
- Alert history captures bot mode + monitoring session ID, with optional columns and CSV export fields.
- Alert history pending entries auto-close to N/A after the regular market session ends.
- Monitoring session exports: capture alerts, cached candles, settings, strategy definition + diagnostics, plus AI console/audit history with diff summaries.
- Portfolio: track open positions and trade journal with persistent local storage.
- Portfolio alerts: configurable sell rules (profit target, trailing stop, daily trend break, time-based exit) with lifecycle statuses (Validated/Invalid/Pending/N/A).
- Portfolio alerts filter by market-date range with start/end pickers defaulting to today’s market session.
- Portfolio alerts include a status dropdown (All/Validated/Invalid/Pending/N/A) to focus on validation state.
- Portfolio risk checks: market-open fall risk scoring with optional notifications.
- Personalization: per-symbol ATR stop multiplier and score bias (stored locally).
- Notifications: GUI log, Telegram, and Windows tray with per-category Telegram toggles.
- Dashboard: LIVE/STALE/OFFLINE counts, top movers, and symbols with errors.
- Dashboard Market Hours: Opens in/Closes in countdown updates automatically during the session.
- Backtest + Research: simulate strategies, compare runs, and export strategy research reports.
- Settings/tests: test Alerts/Yahoo/Notifications from the UI, configure AI providers and models.
- Settings transfer + sync: import/export settings or sync watchlists/alerts/personalization to an endpoint.
- Settings imports automatically skip unlicensed feature settings (Telegram, Windows, AI, themes, etc.).
- Help menu includes an Upgrade/Downgrade License shortcut to reapply signed licenses and refresh feature gating.
- Feature-based license packages control what features/screens unlock per customer license.
- Unlicensed views and settings are disabled with "Upgrade for this option" tooltips in the sidebar and settings dialogs.
- Portfolio screen access is gated by the `portfolio` license feature ID.

<img width="3228" height="1282" alt="image" src="https://github.com/user-attachments/assets/5840ca6c-2ec3-481b-8f4a-58a9c221cd3c" />

<img width="3226" height="1322" alt="image" src="https://github.com/user-attachments/assets/2a513a52-cae6-44b6-b824-88e0e9e906fc" />

<img width="1991" height="991" alt="image" src="https://github.com/user-attachments/assets/a4d535ab-8421-41d2-a5ea-c2c276861025" />

<img width="3233" height="1324" alt="image" src="https://github.com/user-attachments/assets/7f4178c1-8e04-4f01-ac0a-423d0e43f1e7" />

<img width="3223" height="1370" alt="image" src="https://github.com/user-attachments/assets/592886b3-a6ed-4d23-96dd-534efb1123c3" />

<img width="3232" height="1329" alt="image" src="https://github.com/user-attachments/assets/c9527d6c-df8d-4053-ab42-6a1be62bf305" />

<img width="3227" height="1336" alt="image" src="https://github.com/user-attachments/assets/d5256a89-6c78-4f48-92c8-6e34628171cc" />

<img width="3439" height="1414" alt="image" src="https://github.com/user-attachments/assets/864df441-ef3a-4144-a949-7cfee5a9a8bc" />


## Usage Notes
- Configure alerts in-app (Menu > Configure > Alerts) and use test buttons to verify. Toggle which alert types
  (Price Alerts, Alert Rules, Portfolio Alerts) send messages, enable AI messaging, and enable/disable Windows alerts.
- Price alerts wait until 10:00 ET (30 minutes after the open) unless AI pre-market monitoring is enabled in Settings > AI.
- Choose mode (Daily Investor / Long-Term / AI) before starting the bot.
- Use **Alerts → Start Monitoring Session** to begin a run, **End Monitoring Session** to lock in the end time, then export to save alerts, candles, strategy diagnostics, and settings.
- AI interactions during a session are bundled in the export (console Q&A, audit snapshots, and AI-applied deltas) so you can line them up with bot mode changes in alert history.
- Monitoring exports now include the active strategy definition and a diagnostics block (rule counts) to verify strategy loading in post-run analysis.
- Monitoring sessions and export metadata are stored locally under the `StockAlertBot` folder in your user home.
- Use the alert history table column menu to show Bot Mode and Session ID when auditing alert runs or exports.
- Alert history defaults to the current market session date; adjust the start/end date pickers to widen the range.
- Use the alert history status dropdown to focus on SUCCEEDED, FAILED, PENDING, or N/A entries; pending alerts switch to N/A after the regular close.
- Watchlist day-change values refresh when the market date rolls over, keeping daily moves aligned to the current session.
- Right-click watchlist/screener rows for actions (mute, pause, personalize, open chart, add alert, and add to off-hours exclusions).
- Off-hours exclusions (Settings → Strategy) list symbols that should skip off-hours strategy evaluation when off-hours alerts are enabled.
- Portfolio tab includes open positions, trade journal, and portfolio alerts with sell-rule rationale.
- Portfolio alerts show a status column to confirm whether triggers validated during the regular session.
- Portfolio alerts default to today’s market date; adjust start/end pickers to review prior sessions.
- Use the portfolio alerts status dropdown to focus on Validated, Invalid, Pending, or N/A entries across the alert lifecycle.
- Notes Alerts tab supports add/edit/remove notes with optional alert date/time and notification channels.
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
- “Which watchlist symbols look stretched and should get tighter alerts?”
- “Review my portfolio exposure by sector and highlight concentration risk.”
- “Summarize recent trades and flag any outsized losses to journal.”
- “Draft a trade journal entry for my last NVDA sell with key takeaways.”
- “Show my performance winners/laggards and suggest next actions.”
- “Add a price alert for AAPL below 180 and NVDA above 550.”

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
- **AI Scenarios**: optional backtest/research prompts to seed AI scenario generation.

### Watchlist AI Bot
Run the watchlist bot in **AI** mode to keep the alert engine in an AI-tuned profile with audit logging when
recommendations are applied.

## Telegram Commands (portfolio)
- `Open Positions NVDA` → reply with Qty, Avg Cost, Last, and P&L %.
- `All open positions` → reply with all open positions and their Qty and P&L %.
- `Add position NVDA 100qty 212.35usd` → add a new position from chat.

## Setting up a Telegram channel bot and obtaining a token involves a few straightforward steps. 
Here’s a concise guide to get you started and keep you in control of authentication and messaging.

What you’ll need
Telegram account
Access to BotFather (the official bot creator on Telegram)
Steps to create a bot and get the token
- Open Telegram and search for BotFather (@BotFather).
- Start a chat with BotFather and send the command: /newbot
- Follow the prompts to choose a name and a unique username for your bot.
- BotFather will provide a token after the bot is created. This token is the key that authenticates your bot with the Telegram Bot API. Keep it secret and store it securely.
- If you want the bot to operate in a Telegram channel, you’ll also need to add the bot to that channel as an administrator. This allows the bot to post messages on behalf of the channel. You can do this in the channel’s settings under Administrators, then add your bot by its username.
Understanding the token and how to use it
- The token looks like a string: something like 123456789:ABCdefGhIJKlmNoPQRstUVwxyZ. This is the credential used in API calls to send messages, manage updates, and configure webhooks. Treat it like a password.​
With the token, you can call Telegram Bot API methods (for example, to send messages, set webhooks, or get updates). The official Bot API documentation explains all available methods and usage patterns.
​
