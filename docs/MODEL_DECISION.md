# AI-Assisted Coding Platform Decision

**UBC Emerging Media Lab**  
*Platform evaluation for student developer subscriptions*

---

## Executive Summary

The lab is evaluating alternatives to Cursor for AI-assisted development across web, Unity, and Unreal Engine projects. Key requirements include:

- **User management** — Easy onboarding/offboarding for semester-based student rotation
- **Cost predictability** — Direct billing through institutional AWS accounts preferred
- **Security & compliance** — UBC IT policies, no training on lab code
- **Multi-platform support** — Web (TypeScript), Unity (C#), Unreal (C++)

---

## Evaluation Criteria

| Criterion | Weight | Rationale |
|-----------|--------|-----------|
| **User management** | High | Student turnover each semester; need quick onboarding/removal |
| **Billing integration** | High | AWS consolidated billing simplifies procurement |
| **Data privacy** | Critical | Cannot use lab code or UBC data for model training |
| **Language support** | High | TypeScript, C#, C++ across multiple IDEs (VSCode, Rider, UE) |
| **Cost per user** | Medium | Budget-conscious but not the primary constraint |
| **IDE integration** | Medium | Must work with VSCode, JetBrains Rider, Visual Studio |
| **Agent/MCP support** | Low | Current Cursor workflow uses MCP tools; replacement less critical |

---

## Platform Options

### 1. Kiro (via AWS)

**Summary:** AWS-hosted AI coding assistant with IAM Identity Center integration.

**Pros:**
- ✅ **Direct AWS billing** — Costs flow through existing AWS account; no external vendor contracts
- ✅ **IAM Identity Center integration** — Centralized user management; onboard via SSO, offboard by removing IAM access
- ✅ **Compliance** — Stays within AWS environment; easier to align with UBC IT policies
- ✅ **Scalable** — Pay-as-you-go model aligns with variable student count

**Cons:**
- ❌ **Unclear feature parity** — Need to verify language support (C#, C++), IDE plugins, code completion quality
- ❌ **Integration complexity** — Requires IAM Identity Center setup if not already in use
- ❌ **Documentation/maturity** — Less established than Claude Code or GitHub Copilot

**Cost:** Variable (AWS pay-as-you-go)

**Best for:** Labs already using AWS IAM Identity Center with strong DevOps support.

---

### 2. Claude Code (Standalone SaaS)

**Summary:** Anthropic's dedicated code editor subscription.

**Pros:**
- ✅ **No training by default** — Does not use customer code for model training
- ✅ **Predictable cost** — $25/user/month (annual billing) or pay-as-you-go
- ✅ **Simple procurement** — Direct Anthropic subscription; no AWS dependency
- ✅ **Mature product** — Built on Claude's strong reasoning and code generation capabilities

**Cons:**
- ❌ **User management overhead** — Manual account provisioning; no IAM/SSO integration mentioned
- ❌ **External vendor** — Separate contract and billing; less integrated with UBC systems
- ❌ **Unknown IDE support** — Verify compatibility with Rider, Visual Studio, Unreal Editor workflows
- ❌ **Limited control** — Fewer customization options compared to self-hosted or AWS-integrated solutions

**Cost:** $25/user/month (annual) + pay-as-you-go overages

**Best for:** Teams prioritizing ease of setup and strong AI reasoning over deep AWS integration.

---

### 3. Claude Code (via AWS Bedrock)

**Summary:** Self-managed Claude Code deployment using AWS Bedrock for model hosting.

**Pros:**
- ✅ **No external accounts** — Everything runs on AWS; Bedrock hosts the Claude models
- ✅ **Direct Bedrock billing** — Consolidated with other AWS costs
- ✅ **Data residency** — All processing stays within AWS region; strong compliance story
- ✅ **Customizable** — Can tune rate limits, model versions, logging

**Cons:**
- ❌ **Manual credential management** — Requires custom OIDC + Cognito setup or per-user credential distribution
- ❌ **DevOps overhead** — Need to maintain auth, user provisioning, and Bedrock integration
- ❌ **No turnkey SSO** — Unlike Kiro's IAM Identity Center, this requires custom federation
- ❌ **Operational complexity** — Not a managed product; lab owns availability and troubleshooting

**Cost:** Variable (Bedrock usage + Cognito costs)

**Best for:** Labs with strong AWS DevOps capability and strict data residency requirements.

---

### 4. Codex (OpenAI-based)

**Summary:** OpenAI-powered code assistant (likely GitHub Copilot or similar).

**Pros:**
- ✅ **Opt-out for training** — Can configure to not use lab code for model training
- ✅ **Mature ecosystem** — Wide IDE support (VSCode, JetBrains, Visual Studio)
- ✅ **Strong code completion** — Industry-standard inline suggestions

**Cons:**
- ❌ **Higher cost** — More expensive than Claude Code (exact pricing TBD)
- ❌ **OpenAI models** — If using GPT-4, reasoning quality may vary for complex architectural tasks
- ❌ **Training opt-out** — Requires explicit configuration; default may allow training on usage data
- ❌ **Unknown user management** — Verify whether SSO/SAML or AWS IAM integration is available

**Cost:** Higher than $25/user/month (exact pricing not provided)

**Best for:** Teams already standardized on GitHub/Microsoft tooling with budget for premium AI.

---

## Analysis & Recommendations

### Key Decision Factors

1. **Do you already use AWS IAM Identity Center?**
   - **Yes** → Kiro is the strongest candidate (seamless user management, consolidated billing)
   - **No** → Standalone Claude Code is easier to adopt (no AWS setup required)

2. **What is your DevOps capacity?**
   - **High** → Claude Code via Bedrock offers maximum control and compliance
   - **Low** → Standalone Claude Code or Kiro (if IAM Identity Center is already configured)

3. **What is your IDE mix?**
   - **Primarily VSCode** → All options work
   - **JetBrains Rider (Unity/C#)** → Verify Kiro and Claude Code plugin availability
   - **Visual Studio (Unreal/C++)** → Verify Kiro and Claude Code extension support
   - **Unreal Editor** → Unlikely any option has native integration; students will use external editors

4. **How critical is MCP/agent workflow?**
   - **Critical** → None of these match Cursor's MCP ecosystem; may need to adjust standards
   - **Not critical** → Focus on code completion and chat features; remove MCP requirements from standards

### Recommended Path Forward

**Phase 1: Pilot (1-2 months)**

Run a small pilot with 3-5 students on **two platforms**:

1. **Kiro (if IAM Identity Center is available)** — Test AWS integration, user management, C#/C++ support
2. **Standalone Claude Code** — Test ease of use, code quality, student feedback

**Pilot evaluation criteria:**
- Setup time for new users
- Code completion quality (TypeScript, C#, C++)
- Student satisfaction (survey after 4 weeks)
- Actual AWS costs vs. projected
- Support responsiveness

**Phase 2: Decision (after pilot)**

Choose based on:
- If Kiro's IAM integration works smoothly → **Kiro** (best operational fit)
- If Kiro has gaps (IDE support, feature parity) → **Standalone Claude Code** (best balance of ease and quality)
- If you need maximum data control and have DevOps capacity → **Claude Code via Bedrock** (custom deployment)

**Not recommended:**
- **Codex** — More expensive, requires opt-out configuration, unclear advantages over Claude Code

---

## Missing Information

Before final decision, clarify:

- [ ] **Kiro IDE support** — Confirm plugins for VSCode, JetBrains Rider, Visual Studio
- [ ] **Kiro feature parity** — Does it support chat, inline completion, refactoring, multi-file edits?
- [ ] **Claude Code IDE support** — Verify Rider and Visual Studio extensions exist
- [ ] **Claude Code user management** — Can it integrate with SAML/SSO or GitHub Teams?
- [ ] **Codex exact product** — Is this GitHub Copilot, Codex API, or a different OpenAI offering?
- [ ] **Codex pricing** — Get precise per-user cost for comparison
- [ ] **Bedrock setup effort** — Estimate hours needed for Cognito OIDC + user provisioning automation

---

## Impact on EML Standards

Switching from Cursor will require updates to:

1. **Developer Agreement** (line 25-26) — Replace "Cursor IDE (or approved equivalent)" with chosen platform
2. **Onboarding checklist** — Update setup instructions for new platform
3. **Tree-sitter MCP requirement** — Remove if new platform lacks MCP support (lines 27, 44)
4. **Review workflow** — Replace `/review-eml` skill with platform-native review tools or external CI-based review
5. **Project template** — Update `.cursor/` folder to new platform's config directory

**Recommendation:** Keep standards **platform-agnostic** where possible. Focus on outcomes (code review, testing, documentation) rather than specific tools (Cursor agents, MCP).

---

## Cost Projection (10 students, 8 months)

| Platform | Monthly Cost | Annual Cost | Notes |
|----------|--------------|-------------|-------|
| **Kiro** | ~$150-300 | ~$1,800-3,600 | AWS usage-based; assume $15-30/user/month |
| **Claude Code** | $250 | $3,000 | $25/user × 10 users × 12 months (annual billing) |
| **Claude Code (Bedrock)** | $200-400 | $2,400-4,800 | Bedrock usage + Cognito; highly variable |
| **Codex** | $300+ | $3,600+ | Estimated >$30/user/month |

**Note:** Costs exclude DevOps time for setup and maintenance (significant for Bedrock option).

---

## Next Steps

1. **Investigate Kiro** — Schedule demo, verify IAM Identity Center compatibility, test C#/C++ support
2. **Trial Claude Code** — Sign up for one account, test in VSCode and Rider
3. **Pilot plan** — Draft 4-week pilot protocol with student feedback survey
4. **Budget approval** — Present cost comparison to lab leadership
5. **Update standards** — Once decided, revise developer-agreement.md and project template

---

**Document prepared:** September 16, 2026  
**Decision target:** End of pilot (November 2026)  
**Contact:** Project lead (your name here)
