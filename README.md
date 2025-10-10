<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MCP Security Stack - Capability Comparison</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            padding: 40px;
        }
        
        h1 {
            text-align: center;
            color: #1a202c;
            margin-bottom: 10px;
            font-size: 32px;
            font-weight: 700;
        }
        
        .subtitle {
            text-align: center;
            color: #718096;
            margin-bottom: 40px;
            font-size: 16px;
        }
        
        /* Comparison Table Styles */
        .comparison-table {
            width: 100%;
            border-collapse: separate;
            border-spacing: 0;
            margin-bottom: 40px;
            overflow: hidden;
            border-radius: 12px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.07);
        }
        
        .comparison-table thead {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        }
        
        .comparison-table th {
            padding: 20px;
            text-align: left;
            color: white;
            font-weight: 600;
            font-size: 14px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            position: sticky;
            top: 0;
            z-index: 10;
        }
        
        .comparison-table th:first-child {
            width: 30%;
            background: linear-gradient(135deg, #4a5568 0%, #2d3748 100%);
        }
        
        .vendor-header {
            text-align: center;
            position: relative;
        }
        
        .vendor-name {
            font-size: 16px;
            margin-bottom: 5px;
        }
        
        .vendor-tagline {
            font-size: 11px;
            font-weight: 400;
            opacity: 0.9;
            text-transform: none;
            letter-spacing: 0;
        }
        
        .barndoor-header {
            background: linear-gradient(135deg, #805ad5 0%, #6b46c1 100%);
        }
        
        .trojai-header {
            background: linear-gradient(135deg, #e53e3e 0%, #c53030 100%);
        }
        
        .zenity-header {
            background: linear-gradient(135deg, #3182ce 0%, #2563eb 100%);
        }
        
        .combined-header {
            background: linear-gradient(135deg, #10b981 0%, #059669 100%);
        }
        
        .comparison-table tbody tr {
            border-bottom: 1px solid #e5e7eb;
            transition: background-color 0.2s;
        }
        
        .comparison-table tbody tr:hover {
            background-color: #f9fafb;
        }
        
        .comparison-table td {
            padding: 16px 20px;
            vertical-align: middle;
        }
        
        .threat-category {
            font-weight: 600;
            color: #2d3748;
            font-size: 14px;
        }
        
        .threat-description {
            font-size: 11px;
            color: #718096;
            margin-top: 2px;
        }
        
        .category-group {
            background: #f7fafc;
            font-weight: 700;
            color: #1a202c;
            text-transform: uppercase;
            font-size: 12px;
            letter-spacing: 1px;
        }
        
        .category-group td {
            padding: 12px 20px;
            border-top: 2px solid #cbd5e0;
            border-bottom: 2px solid #cbd5e0;
        }
        
        /* Capability Indicators */
        .capability {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            padding: 6px 12px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
            min-width: 100px;
            justify-content: center;
        }
        
        .cap-strong {
            background: linear-gradient(135deg, #10b981 0%, #059669 100%);
            color: white;
        }
        
        .cap-moderate {
            background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);
            color: white;
        }
        
        .cap-partial {
            background: linear-gradient(135deg, #8b5cf6 0%, #7c3aed 100%);
            color: white;
        }
        
        .cap-weak {
            background: linear-gradient(135deg, #fbbf24 0%, #f59e0b 100%);
            color: #92400e;
        }
        
        .cap-none {
            background: #f3f4f6;
            color: #9ca3af;
            border: 1px solid #e5e7eb;
        }
        
        .cap-logging {
            background: linear-gradient(135deg, #60a5fa 0%, #3b82f6 100%);
            color: white;
        }
        
        .cap-prevention {
            background: linear-gradient(135deg, #34d399 0%, #10b981 100%);
            color: white;
        }
        
        .cap-detection {
            background: linear-gradient(135deg, #a78bfa 0%, #8b5cf6 100%);
            color: white;
        }
        
        .cap-monitoring {
            background: linear-gradient(135deg, #60a5fa 0%, #3b82f6 100%);
            color: white;
        }
        
        .cap-complete {
            background: linear-gradient(135deg, #10b981 0%, #059669 100%);
            color: white;
            border: 2px solid #047857;
            font-weight: 700;
        }
        
        /* Icons */
        .icon {
            font-size: 16px;
        }
        
        /* Summary Cards */
        .summary-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-bottom: 40px;
        }
        
        .summary-card {
            background: white;
            border-radius: 12px;
            padding: 24px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.07);
            border: 2px solid transparent;
            transition: all 0.3s;
        }
        
        .summary-card:hover {
            transform: translateY(-4px);
            box-shadow: 0 12px 24px rgba(0,0,0,0.15);
        }
        
        .card-barndoor {
            border-color: #805ad5;
            background: linear-gradient(135deg, #faf5ff 0%, #f3e8ff 100%);
        }
        
        .card-trojai {
            border-color: #e53e3e;
            background: linear-gradient(135deg, #fef2f2 0%, #fee2e2 100%);
        }
        
        .card-zenity {
            border-color: #3182ce;
            background: linear-gradient(135deg, #eff6ff 0%, #dbeafe 100%);
        }
        
        .card-header {
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 16px;
        }
        
        .card-icon {
            width: 50px;
            height: 50px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            color: white;
        }
        
        .icon-barndoor {
            background: linear-gradient(135deg, #805ad5 0%, #6b46c1 100%);
        }
        
        .icon-trojai {
            background: linear-gradient(135deg, #e53e3e 0%, #c53030 100%);
        }
        
        .icon-zenity {
            background: linear-gradient(135deg, #3182ce 0%, #2563eb 100%);
        }
        
        .card-title {
            font-size: 18px;
            font-weight: 700;
            color: #1a202c;
        }
        
        .card-subtitle {
            font-size: 12px;
            color: #718096;
            margin-top: 2px;
        }
        
        .strengths-list {
            list-style: none;
            padding: 0;
        }
        
        .strengths-list li {
            padding: 8px 0;
            font-size: 13px;
            color: #4a5568;
            padding-left: 24px;
            position: relative;
        }
        
        .strengths-list li:before {
            content: "✓";
            position: absolute;
            left: 0;
            font-weight: bold;
        }
        
        .card-barndoor .strengths-list li:before {
            color: #805ad5;
        }
        
        .card-trojai .strengths-list li:before {
            color: #e53e3e;
        }
        
        .card-zenity .strengths-list li:before {
            color: #3182ce;
        }
        
        /* Legend */
        .legend {
            background: #f7fafc;
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 30px;
        }
        
        .legend-title {
            font-weight: 700;
            color: #1a202c;
            margin-bottom: 15px;
            font-size: 14px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        
        .legend-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
        }
        
        .legend-item {
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        /* Insights Box */
        .insights-box {
            background: linear-gradient(135deg, #fef3c7 0%, #fde68a 100%);
            border: 2px solid #f59e0b;
            border-radius: 12px;
            padding: 24px;
            margin-top: 40px;
        }
        
        .insights-title {
            font-size: 18px;
            font-weight: 700;
            color: #92400e;
            margin-bottom: 16px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .insights-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 16px;
        }
        
        .insight-item {
            background: white;
            border-radius: 8px;
            padding: 12px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        
        .insight-label {
            font-size: 11px;
            color: #92400e;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin-bottom: 4px;
        }
        
        .insight-value {
            font-size: 20px;
            font-weight: 700;
            color: #1a202c;
        }
        
        @media (max-width: 768px) {
            .container {
                padding: 20px;
            }
            
            .comparison-table {
                font-size: 12px;
            }
            
            .comparison-table th,
            .comparison-table td {
                padding: 10px;
            }
            
            .capability {
                min-width: auto;
                padding: 4px 8px;
                font-size: 10px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🛡️ MCP Security Stack - Capability Comparison</h1>
        <div class="subtitle">Comprehensive Analysis of Security Coverage Across Barndoor, TrojAI, and Zenity</div>
        
        <!-- Summary Cards -->
        <div class="summary-grid">
            <div class="summary-card card-barndoor">
                <div class="card-header">
                    <div class="card-icon icon-barndoor">🚪</div>
                    <div>
                        <div class="card-title">Barndoor AI</div>
                        <div class="card-subtitle">MCP Control Plane & Governance</div>
                    </div>
                </div>
                <ul class="strengths-list">
                    <li>Centralized MCP gateway control</li>
                    <li>Strong access control & RBAC</li>
                    <li>Policy enforcement at protocol level</li>
                    <li>Comprehensive audit logging</li>
                    <li>Tool-level authorization</li>
                </ul>
            </div>
            
            <div class="summary-card card-trojai">
                <div class="card-header">
                    <div class="card-icon icon-trojai">🔬</div>
                    <div>
                        <div class="card-title">TrojAI</div>
                        <div class="card-subtitle">AI Model Security & Defense</div>
                    </div>
                </div>
                <ul class="strengths-list">
                    <li>Prompt injection prevention</li>
                    <li>Trojan & backdoor detection</li>
                    <li>Jailbreak defense</li>
                    <li>Red team testing capabilities</li>
                    <li>Adversarial attack protection</li>
                </ul>
            </div>
            
            <div class="summary-card card-zenity">
                <div class="card-header">
                    <div class="card-icon icon-zenity">👁️</div>
                    <div>
                        <div class="card-title">Zenity</div>
                        <div class="card-subtitle">Agent Behavioral Analytics</div>
                    </div>
                </div>
                <ul class="strengths-list">
                    <li>Real-time behavioral monitoring</li>
                    <li>Shadow AI discovery</li>
                    <li>Autonomous agent tracking</li>
                    <li>Multi-step attack detection</li>
                    <li>Intent-based analysis</li>
                </ul>
            </div>
        </div>
        
        <!-- Legend -->
        <div class="legend">
            <div class="legend-title">Capability Levels</div>
            <div class="legend-grid">
                <div class="legend-item">
                    <span class="capability cap-strong">Strong</span>
                    <span>Primary capability, best-in-class</span>
                </div>
                <div class="legend-item">
                    <span class="capability cap-moderate">Moderate</span>
                    <span>Good coverage, secondary focus</span>
                </div>
                <div class="legend-item">
                    <span class="capability cap-partial">Partial</span>
                    <span>Limited coverage</span>
                </div>
                <div class="legend-item">
                    <span class="capability cap-none">None</span>
                    <span>Not covered</span>
                </div>
                <div class="legend-item">
                    <span class="capability cap-complete">Complete</span>
                    <span>Full stack coverage</span>
                </div>
            </div>
        </div>
        
        <!-- Main Comparison Table -->
        <table class="comparison-table">
            <thead>
                <tr>
                    <th>Threat Category</th>
                    <th class="vendor-header barndoor-header">
                        <div class="vendor-name">BARNDOOR</div>
                        <div class="vendor-tagline">Control Plane</div>
                    </th>
                    <th class="vendor-header trojai-header">
                        <div class="vendor-name">TROJAI</div>
                        <div class="vendor-tagline">Model Security</div>
                    </th>
                    <th class="vendor-header zenity-header">
                        <div class="vendor-name">ZENITY</div>
                        <div class="vendor-tagline">Behavioral</div>
                    </th>
                    <th class="vendor-header combined-header">
                        <div class="vendor-name">COMBINED</div>
                        <div class="vendor-tagline">Full Stack</div>
                    </th>
                </tr>
            </thead>
            <tbody>
                <!-- Access & Authorization -->
                <tr class="category-group">
                    <td colspan="5">Access & Authorization</td>
                </tr>
                <tr>
                    <td>
                        <div class="threat-category">Access Control</div>
                        <div class="threat-description">User authentication, RBAC, identity management</div>
                    </td>
                    <td align="center"><span class="capability cap-strong">✓ Strong</span></td>
                    <td align="center"><span class="capability cap-none">— None</span></td>
                    <td align="center"><span class="capability cap-moderate">◐ Moderate</span></td>
                    <td align="center"><span class="capability cap-complete">✓✓ Complete</span></td>
                </tr>
                <tr>
                    <td>
                        <div class="threat-category">Policy Enforcement</div>
                        <div class="threat-description">Rule engine, context policies, compliance</div>
                    </td>
                    <td align="center"><span class="capability cap-strong">✓ Strong</span></td>
                    <td align="center"><span class="capability cap-none">— None</span></td>
                    <td align="center"><span class="capability cap-moderate">◐ Moderate</span></td>
                    <td align="center"><span class="capability cap-complete">✓✓ Complete</span></td>
                </tr>
                
                <!-- AI/Model Threats -->
                <tr class="category-group">
                    <td colspan="5">AI/Model Security Threats</td>
                </tr>
                <tr>
                    <td>
                        <div class="threat-category">Prompt Injection</div>
                        <div class="threat-description">Direct & indirect prompt manipulation</div>
                    </td>
                    <td align="center"><span class="capability cap-none">— None</span></td>
                    <td align="center"><span class="capability cap-strong">✓ Strong</span></td>
                    <td align="center"><span class="capability cap-strong">✓ Strong</span></td>
                    <td align="center"><span class="capability cap-complete">✓✓ Complete</span></td>
                </tr>
                <tr>
                    <td>
                        <div class="threat-category">Tool Poisoning</div>
                        <div class="threat-description">Malicious tool descriptions, hidden instructions</div>
                    </td>
                    <td align="center"><span class="capability cap-none">— None</span></td>
                    <td align="center"><span class="capability cap-strong">✓ Strong</span></td>
                    <td align="center"><span class="capability cap-detection">⚡ Detection</span></td>
                    <td align="center"><span class="capability cap-complete">✓✓ Complete</span></td>
                </tr>
                <tr>
                    <td>
                        <div class="threat-category">Trojan/Backdoors</div>
                        <div class="threat-description">Hidden model triggers, poisoned training</div>
                    </td>
                    <td align="center"><span class="capability cap-none">— None</span></td>
                    <td align="center"><span class="capability cap-strong">✓ Strong</span></td>
                    <td align="center"><span class="capability cap-none">— None</span></td>
                    <td align="center"><span class="capability cap-complete">✓✓ Complete</span></td>
                </tr>
                <tr>
                    <td>
                        <div class="threat-category">Jailbreaking</div>
                        <div class="threat-description">Bypassing model safety guardrails</div>
                    </td>
                    <td align="center"><span class="capability cap-none">— None</span></td>
                    <td align="center"><span class="capability cap-strong">✓ Strong</span></td>
                    <td align="center"><span class="capability cap-moderate">◐ Moderate</span></td>
                    <td align="center"><span class="capability cap-complete">✓✓ Complete</span></td>
                </tr>
                
                <!-- Behavioral & Runtime -->
                <tr class="category-group">
                    <td colspan="5">Behavioral & Runtime Security</td>
                </tr>
                <tr>
                    <td>
                        <div class="threat-category">Behavioral Analysis</div>
                        <div class="threat-description">Anomaly detection, pattern analysis</div>
                    </td>
                    <td align="center"><span class="capability cap-none">— None</span></td>
                    <td align="center"><span class="capability cap-none">— None</span></td>
                    <td align="center"><span class="capability cap-strong">✓ Strong</span></td>
                    <td align="center"><span class="capability cap-complete">✓✓ Complete</span></td>
                </tr>
                <tr>
                    <td>
                        <div class="threat-category">Shadow AI/MCP</div>
                        <div class="threat-description">Unsanctioned agents, rogue MCP servers</div>
                    </td>
                    <td align="center"><span class="capability cap-moderate">◐ Moderate</span></td>
                    <td align="center"><span class="capability cap-none">— None</span></td>
                    <td align="center"><span class="capability cap-strong">✓ Strong</span></td>
                    <td align="center"><span class="capability cap-complete">✓✓ Complete</span></td>
                </tr>
                <tr>
                    <td>
                        <div class="threat-category">Autonomous Agents</div>
                        <div class="threat-description">Always-on agents, triggered workflows</div>
                    </td>
                    <td align="center"><span class="capability cap-none">— None</span></td>
                    <td align="center"><span class="capability cap-none">— None</span></td>
                    <td align="center"><span class="capability cap-strong">✓ Strong</span></td>
                    <td align="center"><span class="capability cap-complete">✓✓ Complete</span></td>
                </tr>
                <tr>
                    <td>
                        <div class="threat-category">Multi-Step Attacks</div>
                        <div class="threat-description">Chained exploits, complex attack patterns</div>
                    </td>
                    <td align="center"><span class="capability cap-none">— None</span></td>
                    <td align="center"><span class="capability cap-moderate">◐ Moderate</span></td>
                    <td align="center"><span class="capability cap-strong">✓ Strong</span></td>
                    <td align="center"><span class="capability cap-complete">✓✓ Complete</span></td>
                </tr>
                
                <!-- MCP-Specific -->
                <tr class="category-group">
                    <td colspan="5">MCP Protocol Security</td>
                </tr>
                <tr>
                    <td>
                        <div class="threat-category">MCP Server Control</div>
                        <div class="threat-description">Registry, approval, sanctioned servers</div>
                    </td>
                    <td align="center"><span class="capability cap-strong">✓ Strong</span></td>
                    <td align="center"><span class="capability cap-none">— None</span></td>
                    <td align="center"><span class="capability cap-moderate">◐ Moderate</span></td>
                    <td align="center"><span class="capability cap-complete">✓✓ Complete</span></td>
                </tr>
                <tr>
                    <td>
                        <div class="threat-category">Tool Authorization</div>
                        <div class="threat-description">Tool-level permissions, request filtering</div>
                    </td>
                    <td align="center"><span class="capability cap-strong">✓ Strong</span></td>
                    <td align="center"><span class="capability cap-none">— None</span></td>
                    <td align="center"><span class="capability cap-partial">○ Partial</span></td>
                    <td align="center"><span class="capability cap-complete">✓✓ Complete</span></td>
                </tr>
                <tr>
                    <td>
                        <div class="threat-category">Rug Pull Attacks</div>
                        <div class="threat-description">Time-delayed malicious changes</div>
                    </td>
                    <td align="center"><span class="capability cap-none">— None</span></td>
                    <td align="center"><span class="capability cap-none">— None</span></td>
                    <td align="center"><span class="capability cap-monitoring">🔍 Monitoring</span></td>
                    <td align="center"><span class="capability cap-complete">✓✓ Complete</span></td>
                </tr>
                <tr>
                    <td>
                        <div class="threat-category">Cross-Server Contamination</div>
                        <div class="threat-description">Inter-server interference, tool shadowing</div>
                    </td>
                    <td align="center"><span class="capability cap-partial">○ Partial</span></td>
                    <td align="center"><span class="capability cap-none">— None</span></td>
                    <td align="center"><span class="capability cap-detection">⚡ Detection</span></td>
                    <td align="center"><span class="capability cap-complete">✓✓ Complete</span></td>
                </tr>
                
                <!-- Data Protection -->
                <tr class="category-group">
                    <td colspan="5">Data Protection & Privacy</td>
                </tr>
                <tr>
                    <td>
                        <div class="threat-category">Data Leakage</div>
                        <div class="threat-description">Exfiltration, unauthorized access, PII exposure</div>
                    </td>
                    <td align="center"><span class="capability cap-logging">📝 Logging</span></td>
                    <td align="center"><span class="capability cap-prevention">🛡️ Prevention</span></td>
                    <td align="center"><span class="capability cap-detection">⚡ Detection</span></td>
                    <td align="center"><span class="capability cap-complete">✓✓ Complete</span></td>
                </tr>
                <tr>
                    <td>
                        <div class="threat-category">Compliance & Audit</div>
                        <div class="threat-description">Regulatory compliance, audit trails</div>
                    </td>
                    <td align="center"><span class="capability cap-strong">✓ Strong</span></td>
                    <td align="center"><span class="capability cap-moderate">◐ Moderate</span></td>
                    <td align="center"><span class="capability cap-strong">✓ Strong</span></td>
                    <td align="center"><span class="capability cap-complete">✓✓ Complete</span></td>
                </tr>
                <tr>
                    <td>
                        <div class="threat-category">Token/Credential Theft</div>
                        <div class="threat-description">OAuth token security, API key protection</div>
                    </td>
                    <td align="center"><span class="capability cap-moderate">◐ Moderate</span></td>
                    <td align="center"><span class="capability cap-partial">○ Partial</span></td>
                    <td align="center"><span class="capability cap-detection">⚡ Detection</span></td>
                    <td align="center"><span class="capability cap-complete">✓✓ Complete</span></td>
                </tr>
            </tbody>
        </table>
        
        <!-- Key Insights -->
        <div class="insights-box">
            <div class="insights-title">
                <span>💡</span>
                <span>Critical Insights & Coverage Analysis</span>
            </div>
            <div class="insights-grid">
                <div class="insight-item">
                    <div class="insight-label">Barndoor Alone</div>
                    <div class="insight-value">35%</div>
                    <div class="threat-description">Infrastructure control only</div>
                </div>
                <div class="insight-item">
                    <div class="insight-label">TrojAI Alone</div>
                    <div class="insight-value">30%</div>
                    <div class="threat-description">Model threats only</div>
                </div>
                <div class="insight-item">
                    <div class="insight-label">Zenity Alone</div>
                    <div class="insight-value">35%</div>
                    <div class="threat-description">Behavioral threats only</div>
                </div>
                <div class="insight-item">
                    <div class="insight-label">Barndoor + TrojAI</div>
                    <div class="insight-value">60%</div>
                    <div class="threat-description">Missing behavioral</div>
                </div>
                <div class="insight-item">
                    <div class="insight-label">Barndoor + Zenity</div>
                    <div class="insight-value">65%</div>
                    <div class="threat-description">Missing model security</div>
                </div>
                <div class="insight-item">
                    <div class="insight-label">All Three Combined</div>
                    <div class="insight-value">95%+</div>
                    <div class="threat-description">Complete coverage</div>
                </div>
            </div>
        </div>
        
        <!-- Recommendation Box -->
        <div class="legend" style="margin-top: 30px; background: linear-gradient(135deg, #f0fdf4 0%, #dcfce7 100%); border: 2px solid #10b981;">
            <div class="legend-title" style="color: #059669;">✅ Deployment Recommendations</div>
            <div style="display: grid; gap: 12px; margin-top: 15px;">
                <div style="padding: 12px; background: white; border-radius: 8px; border-left: 4px solid #10b981;">
                    <strong style="color: #059669;">Minimum Viable Security:</strong>
                    <span style="color: #4a5568;">Barndoor (control) + Zenity (visibility) = 65% coverage for basic protection</span>
                </div>
                <div style="padding: 12px; background: white; border-radius: 8px; border-left: 4px solid #f59e0b;">
                    <strong style="color: #d97706;">Recommended Setup:</strong>
                    <span style="color: #4a5568;">All three platforms for comprehensive defense-in-depth (95%+ coverage)</span>
                </div>
                <div style="padding: 12px; background: white; border-radius: 8px; border-left: 4px solid #3b82f6;">
                    <strong style="color: #2563eb;">Phased Approach:</strong>
                    <span style="color: #4a5568;">Start with Barndoor → Add Zenity (Month 1) → Add TrojAI (Month 2)</span>
                </div>
            </div>
        </div>
    </div>
</body>
</html>
