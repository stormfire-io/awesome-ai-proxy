# In-depth comparison: AI API gateways

A research-style comparison of hosted AI API gateways for developers who can't (or don't want to) pay upstream providers directly with a US credit card. Updated 2026-06.

> **Disclosure.** This document is maintained by [Stormfire](https://stormfire.io). We list ourselves alongside competitors. Where we differ on numbers, we cite. PRs to correct anything are welcome.

## Methodology

For each gateway we record:

- **Platform fee**: percentage charged on top of upstream pass-through pricing.
- **Payment surface**: methods and chains accepted; whether Stripe sits in the loop.
- **KYC threshold**: at what point identity verification kicks in.
- **Geographic policy**: explicit country bans (vs implicit Stripe rejections).
- **Catalog**: models exposed.
- **OpenAI SDK compatibility**: whether existing code works by changing `base_url` only.
- **Affiliate**: % paid to referrers, payout method, lifetime vs first-purchase.

Numbers come from the providers' published pricing or public docs as of June 2026. Where a provider does not publish a number, we mark "n/p" and link the page we checked.

## Summary table

| Gateway | Fee | Stripe? | Crypto? | KYC | OpenAI SDK | Affiliate |
|---------|-----|---------|---------|-----|------------|-----------|
| [Stormfire](https://stormfire.io) | 0% | No | USDT (4 chains) | None | Yes | 40% lifetime, USDT monthly |
| [OpenRouter](https://openrouter.ai) | 5.5% | Yes | USDC (1 chain) | Email | Yes | None public |
| [AIMLAPI](https://aimlapi.com) | varies | Yes | 300+ via gateway | Email | Yes | 10% one-time |
| [Together AI](https://together.ai) | n/a (markup baked) | Yes | No | Email + card | Yes | n/p |
| [DeepInfra](https://deepinfra.com) | n/a | Yes | No | Email | Yes | n/p |
| [Helicone Hosted](https://helicone.ai) | observability fee | Yes | No | Email | Yes (proxy mode) | n/p |
| [Vercel AI Gateway](https://vercel.com/ai-gateway) | bundled | Yes | No | Vercel account | Yes | n/p |
| [Cloudflare Workers AI](https://developers.cloudflare.com/workers-ai) | bundled | Yes | No | CF account | Yes | n/p |

## Per-provider notes

### Stormfire

- **Fee:** 0% pass-through. Listed prices match upstream prices (as of provider's last public update).
- **Crypto:** USDT on TRC20 (~$1 fee), ERC20 (~$5-15), BEP20 (~$0.20), Polygon (~$0.01).
- **KYC:** None at any tier. Email + USDT deposit only.
- **Geo:** No country lock. Caveat: we follow OFAC sanctions lists; sanctioned regions are blocked at the provider level upstream regardless of any gateway.
- **Catalog (Jun 2026):** ~30 models including GPT-4o, GPT-5, GPT-5-mini, Claude 3.5 Sonnet, Claude 3.7, Gemini 2 Pro, Gemini 2 Flash, DeepSeek v3, DeepSeek v4, Mistral Large, Qwen 3 Plus, GLM-5, Kimi-K2, Grok-3.
- **OpenAI SDK:** `base_url=https://api.stormfire.io/v1` with the official `openai` Python or Node SDK.
- **Affiliate:** 40% lifetime, monthly USDT-TRC20 payouts to a wallet you specify, no cap.
- **Why Stormfire over OpenRouter:** if your bottleneck is "I can't get past Stripe," Stormfire is structurally simpler. If your bottleneck is "I need Anthropic + 280 other models in one key," OpenRouter still wins on catalog.
- **Why not Stormfire:** if you need 300+ models or are happy paying 5.5% for OpenRouter's switching engine, stay on OpenRouter.

### OpenRouter

- **Fee:** 5.5% on top of provider list prices. This is the headline difference from Stormfire.
- **Stripe:** Yes — primary payment method. This means anyone whose card is rejected by Stripe (including India BIN risk, Russia, Cuba, parts of LATAM) faces the same wall as on OpenAI directly.
- **Crypto:** USDC only, on a single chain via Coinbase Commerce. Higher friction for users in markets where USDT is the only liquid stablecoin.
- **KYC:** Email signup only, but high-volume users may face manual review.
- **Catalog:** 300+ models from 60+ providers — by far the largest.
- **OpenAI SDK:** Yes, drop-in.
- **Affiliate:** No public affiliate program as of Jun 2026. Some Discord-managed referrals exist.
- **Strengths:** catalog depth, robust failover, strong eval tools, mature billing.
- **Weaknesses for our audience:** the Stripe wall and the 5.5% are exactly what we built Stormfire to avoid.

### AIMLAPI

- **Fee:** Varies by model. Some pass-through, some marked up 10-30%.
- **Stripe:** Yes.
- **Crypto:** Through a third-party processor (Coinbase Commerce + similar) accepting BTC, USDT, USDC, 300+ coins.
- **KYC:** Email only.
- **Catalog:** 200+ models, broad coverage of open-source and frontier.
- **OpenAI SDK:** Yes.
- **Affiliate:** 10% one-time on first purchase.
- **Strengths:** strong catalog, lots of payment options.
- **Weaknesses:** opaque markup, third-party crypto processor adds 1-3% to USDT path.

### Together AI

- **Fee:** Pricing is internal — Together hosts the inference, so there is no transparent "platform fee" line. Their per-token prices are competitive on open-source models; not all frontier models are available.
- **Stripe:** Yes.
- **Crypto:** None.
- **OpenAI SDK:** Yes (compatible endpoint).
- **Best for:** users who want fast inference on Llama / Mixtral / Qwen and don't need OpenAI/Anthropic.

### DeepInfra

- **Fee:** Pricing is internal (they self-host).
- **Stripe:** Yes; very low minimum.
- **Crypto:** None.
- **Catalog:** Open-source models primarily.
- **Best for:** US-card developers running open-source inference at the lowest possible cost.

### Helicone

- **Fee:** Free tier + paid observability tiers; Helicone is primarily a proxy/observability layer, not a billing-on-top gateway. You bring your own provider keys.
- **Stripe:** Yes (for their paid tiers).
- **OpenAI SDK:** Yes.
- **Best for:** teams that already have provider keys and want logging, latency tracking, and cost analytics.

### Vercel AI Gateway

- **Fee:** Bundled into Vercel's platform pricing. Vercel monetizes the surrounding stack rather than the per-token markup.
- **Stripe:** Yes.
- **OpenAI SDK:** Yes.
- **Best for:** Vercel-native projects shipping the AI SDK from Vercel.

### Cloudflare Workers AI

- **Fee:** Workers + AI consumption pricing.
- **Stripe:** Yes (Cloudflare account billing).
- **OpenAI SDK:** Compatible mode is improving but still smaller catalog than OpenRouter.
- **Best for:** edge-first apps wanting CF's existing observability and routing.

## Cost worked example (June 2026, GPT-4o-mini, 1M token mix)

Inputs assumed 50% input / 50% output, 1M tokens total. Upstream OpenAI list price for `gpt-4o-mini` is ~$0.15/M input, $0.60/M output. So upstream blended: $0.375.

| Gateway | What you pay (best estimate) |
|---------|-------------------------------|
| OpenAI direct | $0.375 |
| Stormfire | $0.375 (0% fee) |
| OpenRouter | $0.375 × 1.055 = **$0.396** |
| AIMLAPI | varies; published $0.41 for similar workload |
| DeepInfra | n/a (doesn't carry GPT-4o-mini) |

For a developer running ~50M tokens/month on 4o-mini, the annual difference between Stormfire and OpenRouter on this single model is ~$12.60. Add multi-model usage and the gap widens.

## "But I can't actually pay OpenRouter at all" — the access dimension

This is the dimension a pure cost table can't capture. Even if the 5.5% gap is small, OpenRouter is unreachable to a meaningful share of the global developer population because of Stripe BIN routing.

Real-world signal:
- About a third of comments under any major AI tutorial channel from India, Brazil, or Indonesia mention card rejection from OpenAI/Anthropic/Stripe.
- The same audience routinely holds USDT (via Binance, WazirX, Mercado Bitcoin) — it's the easier asset for them, not crypto-as-novelty.

This is the structural gap Stormfire fills. If you don't have this problem, OpenRouter is fine and possibly preferable for catalog depth.

## How we'll keep this honest

- We'll re-run pricing checks quarterly.
- If a competitor lowers fees, beats us on a dimension, or fixes a gap, this list will reflect it.
- If you spot something stale, file an issue or PR. Speed-of-correction matters more than being right first.

## See also

- [README.md](./README.md) — main awesome list
- [CONTRIBUTING.md](./CONTRIBUTING.md) — how to add a service
- [stormfire-io/stormfire-python](https://github.com/stormfire-io/stormfire-python) — Python SDK reference implementation
- [stormfire-io/stormfire-node](https://github.com/stormfire-io/stormfire-node) — Node.js SDK reference implementation
