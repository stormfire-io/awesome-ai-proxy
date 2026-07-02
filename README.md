# 🔥 Awesome AI API Gateways

> A curated list of AI API gateways, proxy services, crypto-payment LLM platforms, and self-hosted alternatives. Maintained by [Stormfire](https://stormfire.io).

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

## What is an AI API gateway?

An AI API gateway is a service that sits between your application and one or more AI providers (OpenAI, Anthropic, Google, etc.), giving you a single endpoint for many models. Common reasons to use one:

- **Unified billing** across multiple providers
- **Failover and load balancing** between models or providers
- **Geographic access** when your country's payment infrastructure can't reach the upstream
- **Alternative payment methods** (crypto, prepaid, regional methods)
- **Caching and rate limiting** at the gateway layer
- **Observability** — logs, metrics, cost attribution per app or user

This list catalogs services we believe are worth comparing, both hosted and self-hosted.

## Contents

- [Hosted Gateways — Crypto Payment](#hosted-gateways--crypto-payment)
- [Hosted Gateways — Traditional (Card/Stripe)](#hosted-gateways--traditional-cardstripe)
- [Hosted Gateways — Open-Source Model Focus](#hosted-gateways--open-source-model-focus)
- [Self-Hosted Gateways](#self-hosted-gateways)
- [Free-Tier Aggregator Gateways](#free-tier-aggregator-gateways)
- [Direct Providers (for comparison)](#direct-providers-for-comparison)
- [Pricing & Latency Comparison Tools](#pricing--latency-comparison-tools)
- [Articles & Reading](#articles--reading)
- [Contributing](#contributing)
- [License](#license)

---

## Hosted Gateways — Crypto Payment

Services that accept cryptocurrency as the primary or only payment method. Best for developers in regions where Stripe / cards face friction.

| Service | Models | Platform Fee | Crypto Accepted | KYC | Min. Top-up |
|---------|--------|--------------|-----------------|-----|-------------|
| **[Stormfire](https://stormfire.io)** | 30+ | 0% | USDT (TRC20/ERC20/BEP20/Polygon) | None | $15 USDT |
| [OpenRouter](https://openrouter.ai) | 300+ | 5.5% | USDC only | Email | $10 USDC |
| [MixRoute](https://mixroute.com) | 200+ | varies | USDT + USDC | None | $10 |

> ℹ️ **Stormfire maintains this list.** We've done our best to be accurate and fair. PRs welcome to correct numbers, add competitors, or update offerings.

## Hosted Gateways — Traditional (Card/Stripe)

| Service | Models | Pricing Model | Special Features |
|---------|--------|---------------|------------------|
| [OpenRouter](https://openrouter.ai) | 300+ | Pass-through + 5.5% | Largest model catalog, OAuth flows |
| [Anyscale Endpoints](https://anyscale.com) | Open-source | Pay-per-token | Self-hosted upgrade path |
| [Together AI](https://together.ai) | Open-source | Pay-per-token | High-throughput inference |
| [Replicate](https://replicate.com) | Multi-modal + LLMs | Pay-per-second | Image / video focus, custom models |
| [Fireworks AI](https://fireworks.ai) | Open + frontier | Pay-per-token | Low-latency inference, function calling |
| [Groq](https://groq.com) | Llama / Mixtral | Pay-per-token | Hardware-accelerated inference |
| [Perplexity API](https://docs.perplexity.ai) | Online + Llama | Pay-per-token | Built-in web search |
| [DeepInfra](https://deepinfra.com) | Open-source | Pay-per-token | Cheap inference, no minimums |
| [TogetherAI](https://api.together.xyz) | Open-source | Pay-per-token | Compatible with OpenAI SDK |
| [CoderPlan](https://coderplan.ai) | Claude/GPT/Gemini/DeepSeek/Grok | Pay-per-token | Alipay/WeChat payment; China market; HK/SG nodes |

## Hosted Gateways — Open-Source Model Focus

| Service | Models | Notable |
|---------|--------|---------|
| [Hugging Face Inference Endpoints](https://huggingface.co/inference-endpoints) | All HF models | Closest to "Hugging Face hosted" |
| [Modal](https://modal.com) | Custom containers | Better for inference platforms than pure API |
| [Banana](https://www.banana.dev) | Custom models | Container-first, GPU autoscale |
| [Replicate](https://replicate.com) | Public + private models | Strongest community library |
| [RunPod Serverless](https://www.runpod.io) | Custom | GPU-on-demand with cold-start optimizations |

## Self-Hosted Gateways

Run your own gateway on your infrastructure. Best for orgs that need full data control, on-premise inference, or want to wrap multiple providers behind one API.

| Project | Stack | Key Features | Stars |
|---------|-------|--------------|-------|
| [LiteLLM Proxy](https://github.com/BerriAI/litellm) | Python / FastAPI | 100+ providers, OpenAI-compatible, observability | 14k+ |
| [New API](https://github.com/QuantumNous/new-api) | Go + React | Multi-tenant, billing, admin UI, OneAPI fork | 8k+ |
| [One API](https://github.com/songquanpeng/one-api) | Go + Vue | Original fork base, simpler, very mature | 18k+ |
| [Portkey Gateway](https://github.com/Portkey-AI/gateway) | Node.js | Edge-ready, observability, fallback logic | 6k+ |
| [Helicone](https://github.com/Helicone/helicone) | TypeScript | Observability layer, supports any upstream | 3k+ |
| [LangFuse](https://github.com/langfuse/langfuse) | TypeScript | Tracing + analytics, can sit alongside gateway | 6k+ |
| [Kong AI Gateway](https://docs.konghq.com/hub/kong-inc/ai-proxy/) | Lua / OpenResty | Enterprise gateway plugin for AI | n/a |

## Free-Tier Aggregator Gateways

Self-hosted projects that work by stitching together free tiers from multiple providers. Different from traditional self-hosted gateways: the value proposition is "don't pay, route through free quotas" rather than "unify billing across paid providers."

Best for hobby projects, learning, and personal use. **Not suitable for production** — free tiers have unpredictable availability, no SLA, and ToS that may prohibit aggregation.

| Project | Stack | Approach | Notable |
|---------|-------|----------|---------|
| [OmniRoute](https://github.com/diegosouzapw/OmniRoute) | TypeScript | 160+ providers / 50+ free sources; RTK+Caveman compression saves 15-95% tokens | Routes Claude Code / Codex / Cursor / Cline / Copilot through free Claude/GPT/Gemini tiers; Desktop + PWA |
| [freellmapi](https://github.com/tashfeenahmed/freellmapi) | Python | Aggregates 16 free-tier providers behind one OpenAI-compatible `/v1` endpoint | ~1.7B tokens/month aggregate free budget; minimal config |
| [GPT4Free](https://github.com/xtekky/gpt4free) | Python | Reverse-engineers public chat UIs to expose a free API | Long-running flagship of the category; cat-and-mouse with providers |

> ⚠️ **Note on ToS:** Most free-tier aggregators sit in legally gray territory. Provider ToS typically prohibits programmatic aggregation of personal free quotas for redistribution. Use at your own risk for personal / learning purposes; do not rely on these for paying customers.

## Direct Providers (for comparison)

For reference — the upstream providers themselves.

| Provider | Models | Billing | Restrictions |
|----------|--------|---------|--------------|
| [OpenAI](https://platform.openai.com) | GPT-4o, GPT-5, o1, o3 | Card via Stripe | Stripe risk model rejects 30+ countries |
| [Anthropic](https://anthropic.com/api) | Claude 3.5, Claude 3.7 | Card via Stripe | Same Stripe issues |
| [Google AI Studio](https://ai.google.dev) | Gemini 2 Pro, Flash | Google Cloud Billing | Free tier, then Cloud Billing |
| [DeepSeek](https://platform.deepseek.com) | DeepSeek v3, v4 | Card / Alipay | China-based, but accepts intl cards |
| [Mistral AI](https://mistral.ai) | Mistral Large, Small | Card | Mostly EU-friendly |
| [xAI](https://x.ai) | Grok-3 | Card | US-leaning, limited geos |
| [Cohere](https://cohere.com) | Command R+ | Card | Enterprise-friendly |

## Pricing & Latency Comparison Tools

| Tool | What it does |
|------|--------------|
| [Stormfire Compare](https://stormfire.io/compare) | Side-by-side: Stormfire vs OpenRouter vs MixRoute |
| [Vellum AI Leaderboard](https://www.vellum.ai/llm-leaderboard) | Model performance + cost benchmarks |
| [Artificial Analysis](https://artificialanalysis.ai) | Latency + cost + quality charts |
| [LLM Pricing Calculator](https://llmpricecheck.com) | Multi-provider cost estimator |
| [Helicone Cost Calculator](https://www.helicone.ai/llm-cost) | Real-time LLM cost calculator |

## Articles & Reading

Foundational and recent writing on AI API access, gateway design, and crypto payment for AI:

- [Why I Stopped Paying for AI APIs with My Credit Card](https://stormfire.io/blog/why-i-stopped-paying-for-ai-apis-with-my-credit-card) — The Stripe risk model and AI access. *(Stormfire blog)*
- [OpenRouter Alternative for Crypto Users](https://stormfire.io/blog/openrouter-alternative-crypto) — Side-by-side comparison and migration guide. *(Stormfire blog)*
- [How to Pay for ChatGPT API with USDT](https://stormfire.io/blog/pay-chatgpt-with-usdt) — Step-by-step guide. *(Stormfire blog)*
- [Awesome Crypto AI](https://github.com/crypto-ai/awesome-crypto-ai) — Tangent list on AI x Crypto. *(Community)*

> If you've written a high-quality, technically substantive article on these topics, open a PR.

## Contributing

Pull requests welcome. Please follow these rules to keep the list high-signal:

1. **One service per PR** for easier review.
2. **No paid promotion.** Entries are evaluated on technical merit only.
3. **Disclose affiliations** in the PR description if you work for the service. We'll still review fairly, but transparency matters.
4. **Working URLs.** Broken links will be flagged and removed in periodic sweeps.
5. **Be honest.** Mention weaknesses where they exist (high fees, limited geo, slow inference). This list is meant to help readers decide.
6. **Markdown table format.** Follow existing column conventions.
7. **No SEO spam.** Listings that exist primarily to promote a service without adding catalogue value will be rejected.

### What we'll remove

Entries are removed when they:

- Become inactive (4+ weeks of downtime, abandoned site)
- Are found to be scam or malicious (rug-pulled, phishing, credential theft)
- Materially misrepresent their offering (e.g., claim "no fees" but charge hidden fees)
- Stop maintaining the underlying service

## License

[CC0 1.0 Universal (Public Domain)](https://creativecommons.org/publicdomain/zero/1.0/). Copy, modify, and republish freely. Attribution appreciated but not required.

---

<div align="center">

**Maintained by [Stormfire](https://stormfire.io)** · [Telegram](https://t.me/stormfireai) · [Compare](https://stormfire.io/compare) · [FAQ](https://stormfire.io/faq)

Made with ❤️ in Tokyo

</div>

