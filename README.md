# Track AI Traffic in GA4

How to see visits from ChatGPT, Perplexity, Claude, Gemini and Copilot in Google Analytics 4, with a copy-paste regex and a short checklist.

Written by [Farman Rind](https://farmanrind.com). Last checked: 16 November 2026. Compiled from the sources listed at the bottom. GA4 changes often, so check each step against your own property.

## The problem

Many AI visits are filed under Referral or Direct, so AI traffic stays hidden inside generic channels. GA4 now has a default channel called `AI Assistant`, but it does not cover everything:

- Google's documentation names ChatGPT, Gemini, DeepSeek, Copilot and Grok. Perplexity and Claude are not on that list and usually land in Referral.
- Sessions from Google AI Overviews and AI Mode are counted as Organic Search, so this method cannot separate them.

## Step 1: See what GA4 already shows

1. Open Reports, then Acquisition, then Traffic acquisition.
2. Change the primary dimension to `Session source / medium`.
3. Search for `chatgpt`, `perplexity`, `claude`, `gemini` and `copilot`.

You will usually see rows such as `chatgpt.com / referral` or `perplexity.ai / referral`. Note the exact source names in your own data.

## Step 2: Create a custom channel group

1. Go to Admin, then Data display, then Channel groups (older guides call this Custom channel groups).
2. Create a new channel group and add a channel named `AI Referrals`.
3. Set the condition to `Source` matches regex, and paste the regex below.
4. Drag the new channel above Referral. Order matters, because a session is placed in the first channel it matches.
5. Save.

## The regex

```
.*(chatgpt\.com|chat\.openai\.com|perplexity\.ai|claude\.ai|gemini\.google\.com|copilot\.microsoft\.com|deepseek\.com|grok\.com).*
```

Some guides also match broad strings such as `openai.com` or `anthropic.com`. Those can catch visits that are not from a chat assistant, so this version stays strict. If your Session source report shows other AI domains, add them separated by `|`.

## Step 3: Check it works

- Filter Session source for `chatgpt.com` and confirm those sessions appear in the new channel.
- Add up the sessions for each AI source in Session source / medium and compare with the channel total.
- Review the list every quarter. New assistants and new referrer domains appear often.

## Limits to know

- Some AI visits arrive without a referrer and show up as Direct.
- ChatGPT citation links can carry `utm_source=chatgpt.com`, so check source and medium together.
- Only a small share of AI answers lead to a click, so traffic understates visibility. Track citations separately (see the [GEO Playbook](https://github.com/farmanrind76/geo-playbook)).
- AI Overviews and AI Mode sit inside Organic Search.

## What to report each month

- Sessions by AI source
- Top landing pages from AI sources
- Engagement rate and key events (conversions) for the AI channel, compared with Organic Search
- Notes on any new AI domain you found in the source report

## Sources

- [Search Engine Journal: GA4's AI Assistant channel undercounts your AI traffic](https://searchenginejournal.com/ga4s-ai-assistant-channel-undercounts-your-ai-traffic-how-to-build-one-that-doesnt/580133)
- [Terminus: AI traffic in GA4, the native channel and the one you build](https://www.terminusapp.com/blog/ai-traffic-channel-in-ga4/)
- [Wellows: track AI referral traffic in GA4](https://wellows.com/blog/track-ai-referral-traffic-ga4/)
- [Frostbite Marketing: how to track AI search traffic in GA4](https://frostbitemarketing.com/resources/how-to-track-ai-search-traffic-in-ga4/)

## Use it

Free to use and share with credit. Spotted a missing AI domain or a changed menu path? Open an issue and I will update it.
