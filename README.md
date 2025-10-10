# Barndoor.ai Capability Assessment & Targeted Technical Questions

## Part 1: Confirmed Barndoor Capabilities

Based on the research, here's what Barndoor **actually does**:

### Core Architecture
- **Control Plane for MCP**: Acts as a governance layer between AI apps and MCP servers
- **Gateway Model**: All MCP traffic flows through Barndoor's secure gateway
- **API Management Heritage**: Founded by team that pioneered API management for mobile apps

### Key Features Confirmed

#### 1. Access Control & Authorization
- Pre-registration/approval of all AI apps, tools, agents, and MCP servers
- User authentication through secure gateway
- Role-based access control (RBAC)
- Context-aware authorization (user + role + app + system + action)
- Ability to switch access on/off instantly

#### 2. Policy Enforcement
- Inspects and authorizes every AI agent request before execution
- Blocks destructive actions (unauthorized deletes/writes)
- Custom conditions and rules for tool usage
- Maps actions to system/role/user permissions
- Can inspect LLM tool requests and apply custom restrictions

#### 3. MCP Server Management
- Centralized registration of approved MCP servers
- Prevents connections to unapproved/random public MCP servers
- Supports both first-party (vendor) and vetted third-party servers
- Manages both internal and external AI apps

#### 4. Visibility & Monitoring
- Complete telemetry and audit trails
- Real-time alerts for anomalies
- Usage tracking and analytics
- Tracks which MCP servers are most used
- Monitors agent/client usage patterns
- Immutable logs for compliance

#### 5. Security Infrastructure
- Zero Trust Architecture
- TLS 1.3 encryption for data in transit
- OAuth 2.0 with PKCE for API authentication
- Hardware Security Modules (HSMs) for key storage
- SOC2 Type II certified
- 24/7 Security Operations Center (SOC)

## Part 2: What Barndoor Does NOT Explicitly Address

Based on the documentation, these capabilities are **not mentioned**:

### Advanced Threat Protection
- Prompt injection detection/prevention
- Tool poisoning protection
- Rug pull attack prevention
- Cross-server contamination prevention
- Command injection sanitization
- Content filtering of prompts/responses

### Runtime Security
- Behavioral anomaly detection using ML/AI
- Sandboxing of MCP servers
- Dynamic tool description monitoring
- Token theft prevention mechanisms
- Rate limiting for tool calls

### Protocol-Level Security
- Input/output content inspection
- Obfuscation detection (base64, etc.)
- Hidden instruction detection in tool descriptions
- Cross-tool interference prevention

---

## Part 3: Targeted Technical Questions for Barndoor

### A. Core Platform Architecture

**1. Gateway Implementation**
- How exactly does your secure gateway intercept MCP traffic? Is it a proxy, SDK, or agent-based approach?
- Does Barndoor require modifications to existing AI apps or MCP servers to route through your gateway?
- What happens if your gateway goes down? Is there a bypass mode or does all MCP traffic stop?

**2. Integration Requirements**
- How do you integrate with AI apps like Claude Desktop, Cursor, or custom applications?
- Do you provide SDKs or APIs that AI apps must use, or is it transparent?
- How long does typical integration take for an enterprise with 50+ AI apps?

**3. MCP Protocol Support**
- Which MCP transport mechanisms do you support (stdio, HTTP, SSE)?
- How do you handle the recent deprecation of SSE in favor of Streamable HTTP?
- Can you work with both local and remote MCP servers?

### B. Access Control & Policy Enforcement

**4. Granular Control Mechanisms**
- Can you demonstrate how custom conditions work for restricting tool usage?
- How do you parse and inspect LLM tool requests - at what layer does this happen?
- Can policies be set at different granularities (global, per-app, per-user, per-tool)?

**5. Dynamic Policy Management**
- Can policies be updated in real-time without disrupting active connections?
- Do you support time-based or context-based policies (e.g., different rules during business hours)?
- How do you handle policy conflicts when multiple rules apply?

**6. Authentication Flow**
- Walk us through the complete authentication flow when a user connects to an MCP server
- How do you handle service accounts vs. human users?
- Can you enforce step-up authentication for sensitive operations?

### C. Security Capabilities

**7. Threat Detection**
- What specific MCP-related threats can you detect today?
- Do you inspect the content of prompts and responses, or just the metadata?
- How would your platform handle a scenario where:
  - A malicious GitHub issue contains prompt injection instructions?
  - An MCP tool description is modified after approval?
  - One MCP server tries to interfere with another's operations?

**8. Data Protection**
- Where and how do you store OAuth tokens for MCP servers?
- Can you detect if sensitive data (PII, credentials) is being passed through MCP?
- Do you support data masking or redaction in transit?

**9. Incident Response**
- If you detect malicious activity, what automatic actions can be taken?
- Can you immediately revoke access to specific MCP servers or tools?
- How quickly can you deploy emergency patches for zero-day MCP vulnerabilities?

### D. Monitoring & Analytics

**10. Visibility Depth**
- What exactly is captured in your audit logs? Can you show a sample log entry?
- Can you track data lineage across multiple MCP server interactions?
- Do you provide analytics on unusual access patterns or data volumes?

**11. Alerting Capabilities**
- What types of anomalies trigger real-time alerts?
- Can alerts be customized based on specific patterns or thresholds?
- Do you integrate with enterprise SIEM platforms? Which ones?

### E. Performance & Scalability

**12. Latency Impact**
- What is the typical latency added by your gateway for an MCP request?
- Have you benchmarked performance with high-volume scenarios (1000+ requests/second)?
- Can certain trusted operations bypass inspection for performance?

**13. Scalability Architecture**
- How does your platform scale horizontally?
- What are the limits on concurrent connections, policies, or MCP servers?
- Can you deploy in multiple regions for global enterprises?

### F. Specific Threat Scenarios

**14. Demonstration Requests**
- Can you demonstrate protection against these specific scenarios:
  - **Unsanctioned MCP Server**: Employee downloads open-source MCP server and connects via Cursor
  - **Cross-tenant leak**: Like the Asana bug - how would you prevent this?
  - **Tool mutation**: MCP server changes behavior 30 days after approval
  - **Credential theft**: Malicious actor tries to exfiltrate OAuth tokens

**15. Advanced Attack Vectors**
- How would you detect/prevent:
  - Base64-encoded malicious instructions in prompts?
  - MCP servers making unexpected cross-service calls?
  - Time-delayed malicious behavior (rug pull attacks)?
  - Command injection through unsanitized tool parameters?

### G. Deployment & Operations

**16. Deployment Options**
- Can Barndoor be deployed on-premises or in a private cloud?
- What are the infrastructure requirements (compute, storage, network)?
- Do you support air-gapped environments?

**17. High Availability**
- What is your SLA for uptime?
- How do you handle failover between regions?
- Can you operate in a degraded mode if certain components fail?

### H. Roadmap & Evolution

**18. Future Capabilities**
- What security features are on your roadmap for the next 6 months?
- How are you planning to address prompt injection and tool poisoning?
- Will you support other agent protocols (Google A2A, IBM Agent Communication)?

**19. Security Research**
- Do you have a dedicated security research team for MCP threats?
- How quickly do you typically respond to new vulnerability disclosures?
- Do you participate in the MCP security community?

### I. Proof of Concept

**20. POC Structure**
- Can we run a POC with our specific MCP servers and attack scenarios?
- What support do you provide during POC?
- Can we test your emergency response procedures?
- What metrics should we use to evaluate effectiveness?

## Part 4: Red Flags to Watch For

During vendor discussions, be concerned if Barndoor:

1. **Cannot demonstrate** real-time inspection of prompt/response content
2. **Lacks mechanisms** to detect tool description changes post-approval
3. **Has no plans** to address prompt injection or tool poisoning
4. **Cannot prevent** cross-server interference or contamination
5. **Doesn't support** common MCP implementations you use
6. **Has high latency** impact (>100ms per request)
7. **Requires significant** changes to existing AI apps/MCP servers
8. **Cannot integrate** with your SIEM/security stack
9. **Has no incident** response team or procedures
10. **Cannot provide** references from similar enterprises

## Part 5: Follow-Up Areas

Based on their responses, dive deeper into:

1. **Live demonstrations** of actual threat prevention
2. **Architecture diagrams** showing data flow
3. **Customer case studies** with measurable outcomes
4. **Integration complexity** for your specific environment
5. **Total cost of ownership** including hidden costs
6. **Professional services** requirements
7. **Training and certification** for your team
8. **Compliance reports** (SOC2, penetration tests)
