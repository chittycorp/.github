# Getting Support - ChittyCorp

## Support Channels

### GitHub Discussions (Primary)
For questions, feature requests, and community discussion:
- [ChittyCan Discussions](https://github.com/chittycorp/chittycan/discussions)
- [General ChittyCorp Discussions](https://github.com/orgs/chittycorp/discussions)

### Email
- **General Questions:** dev@chitty.cc
- **Security Issues:** security@chitty.cc (see [SECURITY.md](SECURITY.md))
- **Licensing/Commercial:** licensing@chitty.cc
- **Conduct Issues:** conduct@chitty.cc

### Website
- **Corporate:** https://chittycorp.com
- **Documentation:** https://github.com/chittycorp/chittycan#readme

## Support by Product

### ChittyCan (AI Gateway + CLI)
- **Docs:** [README](https://github.com/chittycorp/chittycan#readme)
- **Issues:** [Report a bug](https://github.com/chittycorp/chittycan/issues/new?template=bug_report.yml)
- **Parity Failures:** [24hr SLA](https://github.com/chittycorp/chittycan/issues/new?template=parity_failure.yml)
- **Discussions:** [Ask a question](https://github.com/chittycorp/chittycan/discussions)

### ChittyID (Identity System)
- **Production URL:** https://id.chitty.cc
- **Docs:** Coming soon
- **Issues:** Email dev@chitty.cc

### ChittyChain (Evidence Blockchain)
- **Status:** Mainnet Beta Q3 2025
- **Docs:** Coming soon
- **Issues:** Email dev@chitty.cc

### ChittyAuth (OAuth/JWT)
- **Production URL:** https://auth.chitty.cc
- **Docs:** Coming soon
- **Issues:** Email dev@chitty.cc

## Common Questions

### Q: What's the difference between immutable, soft, and hard minting?

**A:** ChittyCorp uses a tri-minting process:

1. **Immutable (Off-Chain)** - 7-day freeze in database with integrity hash
2. **Soft (Certificated)** - Certificate issued, auditable but not yet on-chain
3. **Hard (On-Chain)** - Final settlement on ChittyChain, tamper-proof

This graduated approach balances speed, cost, and finality.

### Q: How do I migrate from OpenAI to ChittyCan?

**A:** Three lines of code:
```python
import openai
openai.api_base = "http://localhost:8787/v1"  # Your gateway
openai.api_key = "your-chittycan-token"
# Everything else works unchanged!
```

See [Migration Playbook](https://github.com/chittycorp/chittycan/blob/main/docs/MIGRATION_PLAYBOOK.md)

### Q: How do I get a ChittyID?

**A:** Never generate locally! Always use the central service:
```bash
curl -X POST https://id.chitty.cc/api/v2/chittyid/mint \
  -H "Authorization: Bearer $TOKEN" \
  -d '{"entity":"PERSON"}'
```

### Q: What's PDX?

**A:** Portable DNA eXchange - our spec for exporting/importing your decision patterns and contributions. Enables true data portability with proof of origin.

### Q: Do I need a commercial license?

**A:**
- **ChittyCan v0.4.x:** MIT - free for all use
- **ChittyCan v0.5.0+:** AGPL v3 - free for open-source, commercial license required for closed-source deployments
- **ChittyOS Services:** AGPL v3 + Commercial dual licensing

[Contact licensing@chitty.cc](mailto:licensing@chitty.cc) for commercial inquiries.

### Q: How does attribution → compensation work?

**A:**
1. Contributions are recorded with ChittyDNA IDs
2. Usage is tracked on-chain via ChittyChain
3. Impact is measured (outcomes, not just output)
4. Loyalty payments are distributed via ChittyPay (coming 2026)
5. Full audit trail proves who did what

### Q: Is my data private?

**A:**
- **Off-chain:** PII encrypted, stored locally or in your vault
- **On-chain:** Only hashes and proofs (no raw PII)
- **Privacy with Proof:** You can prove facts without revealing content (ZK proofs in v3)

## Response Times

| Channel | Expected Response |
|---------|------------------|
| GitHub Issues (bug) | 48 hours |
| Parity Failure | 24 hours |
| Security Critical | 4 hours |
| GitHub Discussions | 2-3 days |
| Email (dev@) | 3-5 days |
| Email (licensing@) | 24 hours |

*Note: These are targets, not guarantees. We're a small team building big things.*

## Self-Service Resources

### Documentation
- [ChittyCan README](https://github.com/chittycorp/chittycan#readme)
- [Migration Playbook](https://github.com/chittycorp/chittycan/blob/main/docs/MIGRATION_PLAYBOOK.md)
- [Competitive Analysis](https://github.com/chittycorp/chittycan/blob/main/docs/COMPETITIVE_ANALYSIS.md)
- [Contributing Guide](https://github.com/chittycorp/chittycan/blob/main/CONTRIBUTING.md)

### Code Examples
- [Parity Tests (Python)](https://github.com/chittycorp/chittycan/blob/main/tests/parity_py.py)
- [Parity Tests (Node)](https://github.com/chittycorp/chittycan/blob/main/tests/parity_node.js)
- [Benchmarks](https://github.com/chittycorp/chittycan/tree/main/benchmarks)

### Troubleshooting

**ChittyCan not found after install:**
```bash
# Reinstall with verbose output
npm install -g chittycan --verbose

# Check installation
which can
can --version
```

**Config file permissions:**
```bash
chmod 600 ~/.config/chitty/config.json
```

**Database connection errors (ChittyOS services):**
```bash
# Verify connection
psql $NEON_DATABASE_URL -c "SELECT 1"

# Check secrets
wrangler secret list | grep NEON
```

**Token validation failures:**
```bash
# Verify token is active
curl https://auth.chitty.cc/api/v1/validate \
  -H "Authorization: Bearer $TOKEN"
```

## Feature Requests

Use the appropriate issue template:
- [ChittyCan Feature Request](https://github.com/chittycorp/chittycan/issues/new?template=feature_request.yml)
- [General Discussion](https://github.com/orgs/chittycorp/discussions)

Include:
- The problem you're solving
- Your proposed solution
- Why this is valuable
- Your use case

## Commercial Support

For enterprise support, SLA guarantees, and custom development:

**Email:** licensing@chitty.cc

**Include:**
- Company name and size
- Use case (self-host, SaaS, internal tools, multi-tenant)
- Timeline and requirements
- Budget expectations

## Contributing

Want to help improve support?

- Improve docs: [CONTRIBUTING.md](https://github.com/chittycorp/chittycan/blob/main/CONTRIBUTING.md)
- Answer questions in [Discussions](https://github.com/orgs/chittycorp/discussions)
- Write tutorials and blog posts
- Report unclear documentation

---

**Last Updated:** 2025-01-04

*"No Corporate Theater - if it didn't ship or save time/money/risk, it doesn't count."* - ChittyCorp Operating Tenets
