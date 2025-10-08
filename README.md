Bidirectional Anonymization Plan for SOC/LLM Integration (Updated)
The Problem
* SOC has 100+ log sources with 5,000-10,000 fields each (500K+ total fields)
* Need to send sensitive data to LLMs for analysis
* Must protect PII/sensitive data but get actionable results back with real values
* Field names are unreliable - same data appears in different fields across logs
The Solution: Value-Based Pattern Recognition + FPE
Core Concept
Raw Logs → Pattern Detection → FPE Encrypt → LLM Analysis → FPE Decrypt → Actionable Results
Key Components
1. Smart Detection Technology
* Pattern-based recognition: Detects WHAT data is (IP, email, etc.) regardless of field name
* Format-Preserving Encryption: Maintains data structure while encrypting
* Deterministic: Same value ALWAYS produces same token (preserves correlations across all logs)
* No field mapping needed: Works on value patterns, not field names
2. Four-Step Process
* Step 1: Detect sensitive values using patterns (not field names)
* Step 2: Apply FPE to identified sensitive data
* Step 3: LLM analyzes with consistent anonymized values
* Step 4: De-anonymize results back to original values
3. How It Handles Chaos
# Same IP in different fields across vendors:
Log1: {"source_ip": "192.168.1.100"}      → Encrypts to "10.23.45.67"
Log2: {"src": "192.168.1.100"}            → SAME "10.23.45.67"  
Log3: {"data_field_7": "192.168.1.100"}   → STILL "10.23.45.67"
Log4: {"status": "192.168.1.100"}         → STILL "10.23.45.67" (bad field name!)

# LLM sees consistent token, can correlate attacks
Implementation Architecture
Detection Layer: 
  Primary: Regex pattern matching for known formats
  Secondary: Entropy analysis for passwords/tokens
  Fallback: Field name hints (unreliable but helpful)

Encryption: 
  Algorithm: Format-Preserving Encryption (NIST FF3-1)
  Approach: Value-based, not field-based
  
Processing: 
  Stream-based pattern detection
  No need to know field structures
  Self-learning cache for optimization

Key Management: 
  Single master key (AWS KMS/HashiCorp Vault)
  
Scale: 
  Parallel processing with Kafka/Spark
  Pattern matching in microseconds
Why This Works for Messy SOC Data
Pattern Detection Examples
# Detects by pattern, not field name:
- IPv4: Any string matching XXX.XXX.XXX.XXX
- Email: Any string matching user@domain.com
- Credit Card: Any 16-digit pattern
- High Entropy: Likely passwords/API keys
- MAC Address: XX:XX:XX:XX:XX:XX format
Correlation Preservation
* Attacker IP 203.0.113.5 appears in 50 different logs
* Different field names: "attacker", "source", "ip_addr", "data3", etc.
* ALL encrypt to same token: 185.42.17.93
* LLM identifies it's the same attacker across all systems
* SOC analyst gets back the real IP: 203.0.113.5
Benefits
* ✅ Privacy: LLM never sees real sensitive data
* ✅ Accuracy: Pattern detection catches sensitive data in ANY field
* ✅ Correlation: Same threat actor = same token across ALL logs
* ✅ Scale: Handles 500K+ fields without knowing their names/structure
* ✅ No Mapping: No field mapping or token vault needed
* ✅ Reversibility: 100% accurate de-anonymization
* ✅ Resilience: Works even with terrible field naming conventions
Real SOC Impact
Before Analyst Sees:
Raw: Scattered data across 100 log sources with inconsistent fields
↓
Pattern detection finds "attacker@evil.com" in 23 different field names
↓
All instances encrypted to "user_a3f2@b4c5.com"
↓
LLM: "user_a3f2@b4c5.com appears in 23 systems with suspicious behavior"
↓
De-anonymized: "attacker@evil.com appears in 23 systems with suspicious behavior"
↓
SOC Action: Block attacker@evil.com across all systems
The Key Innovation
We detect sensitive data by what it IS, not where it is.
This means:
* Works with any log format (structured/unstructured)
* Handles vendor-specific weird field naming
* Preserves threat correlation across all systems
* Zero configuration per log source
* Scales to millions of fields without breaking
Bottom Line: This approach solves the real-world chaos of SOC data where the same attacker IP might be in a field called "source_ip" in one log and "misc_data_field_7" in another, while still maintaining perfect correlation for threat hunting and providing actionable intelligence to analysts.
