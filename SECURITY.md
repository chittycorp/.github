# Security Policy - ChittyCorp

## Our Commitment

ChittyCorp builds tools for trust, proof, and fair compensation. Security is not an afterthought—it's foundational to our mission.

**From our principles:**
- **Privacy with Proof** - Content can remain private while proofs remain verifiable
- **Human Safety & Dignity** - No coercion, surveillance abuse, or harm
- **Transparency over Theater** - Decisions and flows are explainable and auditable

## Supported Projects

Security support varies by project maturity:

| Project | Status | Support Level |
|---------|--------|---------------|
| ChittyCan | Production (v0.4.x) | Full security support |
| ChittyID | Production | Full security support |
| ChittyAuth | Production | Full security support |
| ChittyConnect | Production | Full security support |
| ChittyChain | Mainnet Beta (Q3 2025) | Beta security support |
| ChittyDNA | Development | Best-effort |
| ChittyPay | Planned | Not yet supported |

## Reporting a Vulnerability

**Please DO NOT report security vulnerabilities through public GitHub issues.**

### Critical Path: GitHub Security Advisories

1. Navigate to the affected repository's security tab
2. Click "Report a vulnerability"
3. Provide:
   - Description of the vulnerability
   - Steps to reproduce
   - Potential impact
   - Affected versions
   - Suggested fix (if you have one)

### Alternative: Email

**Email:** security@chitty.cc

**Include:**
- Repository/service affected
- Description of vulnerability
- Steps to reproduce
- Potential impact (especially if affects: identity, evidence chain, on-chain data, payments)
- Your contact information for follow-up

### Special Categories

**ChittyChain / Smart Contract Vulnerabilities**
- Email: security@chitty.cc with subject `[CHAIN-CRITICAL]`
- Include: contract address, network, exploit scenario, potential fund impact

**ChittyID / Identity System**
- Email: security@chitty.cc with subject `[IDENTITY-CRITICAL]`
- Include: ID format affected, collision scenario, privacy breach potential

**Attribution/DNA Extraction**
- Email: security@chitty.cc with subject `[ATTRIBUTION-CRITICAL]`
- Include: How contributions could be extracted without consent/attribution

## Response Timeline

| Severity | Initial Response | Fix Timeline | Disclosure |
|----------|-----------------|--------------|------------|
| Critical | 4 hours | 24-48 hours | Coordinated, 7-14 days after fix |
| High | 24 hours | 7 days | Coordinated, 30 days after fix |
| Medium | 48 hours | 14 days | Coordinated, 60 days after fix |
| Low | 7 days | 30 days | Coordinated, 90 days after fix |

**Critical** = Identity collision, chain manipulation, fund theft, PII exposure, silent extraction

**High** = Attribution bypass, auth bypass, DOS on critical path, data corruption

**Medium** = Privilege escalation, CSRF, XSS with limited impact

**Low** = Information disclosure, non-critical DOS

## Disclosure Policy

We follow **coordinated disclosure**:

1. You report the vulnerability privately
2. We confirm and investigate (within response timeline)
3. We develop and test a fix
4. We deploy the fix to production
5. We coordinate disclosure timing with you
6. We publish a security advisory
7. We credit you in the advisory (unless you prefer anonymity)

**Please give us reasonable time to fix before public disclosure.**

## Security Best Practices

### For Users

**API Keys and Tokens**
```bash
# ✅ GOOD: Store credentials in config (not tracked by git)
can config  # Stores in ~/.config/chitty/config.json
chmod 600 ~/.config/chitty/config.json

# ❌ BAD: Don't commit credentials
git add config.json  # If it contains API keys - DON'T DO THIS
```

**ChittyID Usage**
```bash
# ✅ GOOD: Always use central service
curl -X POST https://id.chitty.cc/api/v2/chittyid/mint

# ❌ BAD: Never generate IDs locally
# (breaks determinism, creates collision risk)
```

**Evidence Chain of Custody**
```bash
# ✅ GOOD: Freeze before mint (dual-immutability)
# Off-chain freeze (7 days) → On-chain mint

# ❌ BAD: Skipping freeze period
# (violates immutability guarantees)
```

### For Developers

**Dependencies**
```bash
# Audit before every commit
npm audit

# Fix critical/high immediately
npm audit fix

# Check for supply chain attacks
npm audit signatures
```

**Secrets in Code**
```typescript
// ✅ GOOD: Environment variables
const apiKey = process.env.CHITTYCAN_TOKEN;

// ❌ BAD: Hardcoded secrets
const apiKey = "sk-1234567890";  // NEVER
```

**Smart Contract Development**
```solidity
// ✅ GOOD: Checks-Effects-Interactions pattern
function mint(bytes32 hash) external {
    require(eligibleForMint[hash], "Not eligible");
    eligibleForMint[hash] = false;  // Effect
    _mint(msg.sender, hash);        // Interaction
}

// ❌ BAD: Reentrancy vulnerability
function mint(bytes32 hash) external {
    _mint(msg.sender, hash);
    eligibleForMint[hash] = false;  // Too late!
}
```

**Input Validation**
```typescript
// ✅ GOOD: Validate all inputs
function validateChittyID(id: string): boolean {
  const pattern = /^01-[CE]-[A-Z]{3}-[0-9]{4}-[PTOCL]-[0-9]{4}-[0-9]{2}-[A-Z0-9]$/;
  return pattern.test(id) && verifyChecksum(id);
}

// ❌ BAD: Trust user input
const id = userInput;  // Injection risk
```

## Known Security Considerations

### ChittyID
- **ID Format Predictability** - IDs are deterministic; sequence from drand is public
- **Mitigation** - Geographic domain + lifecycle stage + checksum prevent practical collision
- **Risk** - Low (cryptographically sound)

### ChittyChain
- **Off-Chain Data Availability** - Evidence stored off-chain (IPFS + Postgres)
- **Mitigation** - Redundant pinning, hash on-chain, merkle proofs
- **Risk** - Medium (requires robust IPFS strategy)

### ChittyCan Gateway
- **Token Transmission** - Tokens in HTTP headers
- **Mitigation** - HTTPS required, tokens hashed before storage (SHA-256)
- **Risk** - Low (standard practice)

### Attribution Graph (ChittyDNA)
- **Privacy vs Audit Tradeoff** - Attribution requires tracking contributions
- **Mitigation** - Hash-and-prove, encrypted components, ZK proofs (v3)
- **Risk** - Medium (active research area)

## Security Features by Project

### ChittyCan (v0.4.0)
- ✅ Token hashing (SHA-256)
- ✅ HTTPS enforcement
- ✅ Config file permissions (600)
- ✅ OAuth support
- ✅ Dependency auditing

### ChittyID (Production)
- ✅ Drand beacon for randomness
- ✅ Dual-immutability (7-day freeze)
- ✅ Checksum validation
- ✅ Chain of custody logging
- 🚧 zk-CID research (2026)

### ChittyChain (Beta)
- ✅ Dual-signature (foundation + validator)
- ✅ Merkle proofs
- ✅ IPFS content addressing
- 🚧 Slashing (Phase 2+)
- 🚧 Smart contract audit (Q3 2025)

## Compliance & Audits

### Current Status
- **GDPR/CCPA:** PII stored off-chain; right-to-erasure removes raw data, hash remains
- **SOC 2 Type II:** Target Q1 2026
- **ISO/IEC 27001:** ISMS roadmap in progress
- **Smart Contract Audit:** Scheduled Q3 2025 (pre-mainnet)

### Audit Partners
- Smart contract audits: TBD (Q3 2025)
- Financial audits: Quarterly (post-DAO launch)
- Penetration testing: Annual + post-major-release

## Bug Bounty Program

**Status:** Launching Q4 2025

**Scope (planned):**
- ChittyChain smart contracts
- ChittyID collision/forgery
- ChittyCan gateway bypass
- Attribution extraction

**Rewards (planned):**
- Critical: $5,000 - $25,000
- High: $1,000 - $5,000
- Medium: $500 - $1,000
- Low: $100 - $500

**Pre-launch:** We appreciate security researchers and will:
- Credit you in security advisories
- Send ChittyCorp swag for valid reports
- Prioritize your contributions for bounty program beta access

## Security Hall of Fame

We recognize security researchers who responsibly disclose vulnerabilities:

<!-- This section will be updated as we receive reports -->

*No vulnerabilities reported yet*

---

## Emergency Contacts

- **General Security:** security@chitty.cc
- **Smart Contract Emergency:** security@chitty.cc with `[CHAIN-CRITICAL]`
- **Identity System Emergency:** security@chitty.cc with `[IDENTITY-CRITICAL]`
- **Attribution/Extraction:** security@chitty.cc with `[ATTRIBUTION-CRITICAL]`

---

**Questions?** Email security@chitty.cc

**Last Updated:** 2025-01-04
**Next Review:** 2025-04-04 (quarterly)

---

*"Privacy with proof. Transparency over theater."* - ChittyFoundation Principles
