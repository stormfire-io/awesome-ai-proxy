# 🔥 Awesome AI API Gateways & Proxy Services

A curated list of AI API gateways, proxy services, and crypto-payment LLM platforms.

Maintained by [Stormfire](https://stormfire.io). Contributions welcome via PR.

## What is an AI API gateway?

A service that lets you access multiple AI models (OpenAI, Anthropic, Google, etc.) through a single unified API. Usually adds features like:

- Unified billing across providers
- Failover / load balancing
- Caching / rate limiting
- Alternative payment methods (crypto, prepaid)
- Geographic access (for users blocked from direct providers)

## Contents

- [Gateways with Crypto Payment](#gateways-with-crypto-payment)
- [Traditional Gateways (Stripe / Card)](#traditional-gateways-stripe--card)
- [Direct Providers](#direct-providers)
- [Open Source Gateways (Self-hosted)](#open-source-gateways-self-hosted)
- [Pricing Comparison Tools](#pricing-comparison-tools)
- [Related Reading](#related-reading)

---

## Gateways with Crypto Payment

Services that accept cryptocurrency (USDT, USDC, BTC, ETH) for AI API access. Best for developers in regions where credit cards face friction.

| Service | Models | Fee | Crypto | KYC |
|---------|--------|-----|--------|-----|
| **[Stormfire](https://stormfire.io)** | 30+ | 0% | USDT (TRC20/ERC20/BEP20/Polygon) | None |
| [OpenRouter](https://openrouter.ai) | 300+ | 5.5% | USDC only | Email |
| [MixRoute](https://mixroute.com) | 200+ | varies | USDT + USDC | None |
| [Together AI](https://together.ai) | Open-source models | 0% | USDC | Email |

> **Disclaimer:** Stormfire maintains this list. We have done our best to be fair, but for the most accurate comparison, please test each service yourself. PRs welcome to correct inaccuracies or add competitors.

## Traditional Gateways (Stripe / Card)

| Service | Models | Pricing model | Special features |
|---------|--------|---------------|------------------|
| [OpenRouter](https://openrouter.ai) | 300+ | Pass-through + 5.5% | Largest model catalog |
| [Anyscale Endpoints](https://anyscale.com) | Open-source | Pay-per-token | Self-hosted option |
| [Together AI](https://together.ai) | Open-source | Pay-per-token | High-throughput inference |
| [Replicate](https://replicate.com) | Multi-modal + LLMs | Pay-per-second | Image/video focus |
| [Fireworks AI](https://fireworks.ai) | Open + frontier | Pay-per-token | Low-latency inference |

## Direct Providers

For comparison — these are the upstream providers themselves.

| Provider | Models | Billing |
|----------|--------|---------|
| [OpenAI](https://platform.openai.com) | GPT-4o, GPT-5, o1, o3 | Card (via Stripe) |
| [Anthropic](https://anthropic.com/api) | Claude 3.5, Claude 3.7 | Card (via Stripe) |
| [Google AI Studio](https://ai.google.dev) | Gemini 2 Pro, Gemini 2 Flash | Card (via Google Cloud Billing) |
| [DeepSeek](https://platform.deepseek.com) | DeepSeek v3, v4 | Card / Alipay |
| [Mistral AI](https://mistral.ai) | Mistral Large, Small | Card |
| [xAI](https://x.ai) | Grok-3 | Card |

## Open Source Gateways (Self-hosted)

Run your own gateway on your infrastructure.

| Project | Stack | Key features |
|---------|-------|--------------|
| [LiteLLM Proxy](https://github.com/BerriAI/litellm) | Python/FastAPI | 100+ providers, OpenAI-compatible |
| [New API](https://github.com/QuantumNous/new-api) | Go + React | Multi-tenant, billing, admin UI |
| [One API](https://github.com/songquanpeng/one-api) | Go + Vue | Original fork base, simpler |
| [PortkeyAI](https://github.com/Portkey-AI/gateway) | Node.js | Edge-ready, observability |
| [HelixDB](https://github.com/helixdb/helix) | Rust | High-performance edge gateway |

## Pricing Comparison Tools

| Tool | What it does |
|------|--------------|
| [Stormfire Compare](https://stormfire.io/compare) | Side-by-side: Stormfire vs OpenRouter vs MixRoute |
| [Vellum AI Leaderboard](https://www.vellum.ai/llm-leaderboard) | Model performance + cost benchmarks |
| [LLM Pricing Calculator](https://llmpricecheck.com) | Multi-provider cost estimator |
| [Artificial Analysis](https://artificialanalysis.ai) | Latency + cost + quality charts |

## Related Reading

- [The Stripe risk model and AI access](https://stormfire.io/blog/why-i-stopped-paying-for-ai-apis-with-my-credit-card)
- [OpenRouter alternative for crypto users](https://stormfire.io/blog/openrouter-alternative-crypto)
- [How to pay for ChatGPT API with USDT](https://stormfire.io/blog/pay-chatgpt-with-usdt)

## Contributing

Pull requests welcome. Please follow these rules:

- **One service per PR** for easier review
- **No paid promotion** — entries are evaluated on technical merit
- **Disclose affiliations** in PR description if you work for the service
- **Working URLs** — broken links will be flagged and removed
- **Be honest** — list both strengths and weaknesses if relevant

We will remove any service that:
- Becomes inactive (4+ weeks of downtime)
- Is found to be scam / malicious
- Misrepresents itself materially (e.g., claims "no fees" but charges hidden fees)

## License

CC0 1.0 Universal (Public Domain). Copy, modify, and use freely.

---

Made with ❤️ by [Stormfire](https://stormfire.io)
