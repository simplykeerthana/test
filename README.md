<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Agentic AI Security Architecture</title>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
            background: #f5f7fa;
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }
        
        .diagram-container {
            background: white;
            border-radius: 12px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.1);
            padding: 40px;
            max-width: 1600px;
            width: 100%;
        }
        
        h1 {
            text-align: center;
            color: #1a202c;
            margin-bottom: 10px;
            font-size: 28px;
            font-weight: 600;
        }
        
        .subtitle {
            text-align: center;
            color: #718096;
            margin-bottom: 40px;
            font-size: 14px;
        }
        
        svg {
            width: 100%;
            height: auto;
            max-width: 1500px;
            margin: 0 auto;
            display: block;
        }
        
        /* Component styles */
        .component-box {
            fill: white;
            stroke-width: 2;
            filter: drop-shadow(0 2px 4px rgba(0,0,0,0.1));
        }
        
        .user-zone { stroke: #4299e1; fill: #ebf8ff; }
        .agent-zone { stroke: #9f7aea; fill: #faf5ff; }
        .security-zone { stroke: #48bb78; fill: #f0fff4; }
        .mcp-zone { stroke: #ed8936; fill: #fffdf7; }
        .infra-zone { stroke: #718096; fill: #f7fafc; }
        
        .zone-label {
            font-size: 12px;
            font-weight: 600;
            fill: #4a5568;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        
        .component-label {
            font-size: 13px;
            font-weight: 500;
            fill: #2d3748;
        }
        
        .sub-label {
            font-size: 11px;
            fill: #718096;
        }
        
        .product-label {
            font-size: 11px;
            font-weight: 600;
            fill: white;
        }
        
        .barndoor-fill { fill: #805ad5; }
        .zenity-fill { fill: #3182ce; }
        .trojai-fill { fill: #e53e3e; }
        
        .data-flow {
            stroke: #4299e1;
            stroke-width: 2;
            fill: none;
            marker-end: url(#arrowhead-blue);
            stroke-dasharray: none;
        }
        
        .control-flow {
            stroke: #9f7aea;
            stroke-width: 2;
            fill: none;
            marker-end: url(#arrowhead-purple);
            stroke-dasharray: 5, 5;
        }
        
        .security-flow {
            stroke: #48bb78;
            stroke-width: 2;
            fill: none;
            marker-end: url(#arrowhead-green);
            stroke-dasharray: 2, 2;
        }
        
        .threat-flow {
            stroke: #e53e3e;
            stroke-width: 1.5;
            fill: none;
            marker-end: url(#arrowhead-red);
            stroke-dasharray: 3, 3;
        }
        
        .legend {
            margin-top: 30px;
            padding: 20px;
            background: #f7fafc;
            border-radius: 8px;
            border: 1px solid #e2e8f0;
        }
        
        .legend-title {
            font-weight: 600;
            color: #2d3748;
            margin-bottom: 15px;
            font-size: 14px;
        }
        
        .legend-items {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
        }
        
        .legend-item {
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 13px;
            color: #4a5568;
        }
        
        .legend-line {
            width: 40px;
            height: 2px;
            display: inline-block;
        }
        
        @media (max-width: 1200px) {
            .diagram-container {
                padding: 20px;
            }
        }
    </style>
</head>
<body>
    <div class="diagram-container">
        <h1>Agentic AI Security Architecture</h1>
        <div class="subtitle">End-to-End Security Stack with MCP Control Plane</div>
        
        <svg viewBox="0 0 1400 900" xmlns="http://www.w3.org/2000/svg">
            <!-- Define markers for arrows -->
            <defs>
                <marker id="arrowhead-blue" markerWidth="10" markerHeight="10" refX="9" refY="3" orient="auto" fill="#4299e1">
                    <polygon points="0 0, 10 3, 0 6" />
                </marker>
                <marker id="arrowhead-purple" markerWidth="10" markerHeight="10" refX="9" refY="3" orient="auto" fill="#9f7aea">
                    <polygon points="0 0, 10 3, 0 6" />
                </marker>
                <marker id="arrowhead-green" markerWidth="10" markerHeight="10" refX="9" refY="3" orient="auto" fill="#48bb78">
                    <polygon points="0 0, 10 3, 0 6" />
                </marker>
                <marker id="arrowhead-red" markerWidth="10" markerHeight="10" refX="9" refY="3" orient="auto" fill="#e53e3e">
                    <polygon points="0 0, 10 3, 0 6" />
                </marker>
                
                <!-- Gradient definitions -->
                <linearGradient id="grad-barndoor" x1="0%" y1="0%" x2="100%" y2="100%">
                    <stop offset="0%" style="stop-color:#805ad5;stop-opacity:1" />
                    <stop offset="100%" style="stop-color:#6b46c1;stop-opacity:1" />
                </linearGradient>
                <linearGradient id="grad-zenity" x1="0%" y1="0%" x2="100%" y2="100%">
                    <stop offset="0%" style="stop-color:#3182ce;stop-opacity:1" />
                    <stop offset="100%" style="stop-color:#2c5282;stop-opacity:1" />
                </linearGradient>
                <linearGradient id="grad-trojai" x1="0%" y1="0%" x2="100%" y2="100%">
                    <stop offset="0%" style="stop-color:#e53e3e;stop-opacity:1" />
                    <stop offset="100%" style="stop-color:#c53030;stop-opacity:1" />
                </linearGradient>
            </defs>
            
            <!-- User Zone -->
            <rect x="20" y="20" width="320" height="120" rx="8" class="component-box user-zone"/>
            <text x="30" y="40" class="zone-label">User Layer</text>
            
            <!-- Users/Developers -->
            <rect x="40" y="60" width="130" height="60" rx="4" fill="white" stroke="#4299e1"/>
            <text x="105" y="85" text-anchor="middle" class="component-label">End Users</text>
            <text x="105" y="105" text-anchor="middle" class="sub-label">Business Users</text>
            
            <rect x="190" y="60" width="130" height="60" rx="4" fill="white" stroke="#4299e1"/>
            <text x="255" y="85" text-anchor="middle" class="component-label">Developers</text>
            <text x="255" y="105" text-anchor="middle" class="sub-label">Citizen Devs</text>
            
            <!-- AI Agent Applications Zone -->
            <rect x="20" y="170" width="320" height="180" rx="8" class="component-box agent-zone"/>
            <text x="30" y="190" class="zone-label">AI Agent Applications</text>
            
            <!-- AI Apps -->
            <rect x="40" y="210" width="130" height="50" rx="4" fill="white" stroke="#9f7aea"/>
            <text x="105" y="235" text-anchor="middle" class="component-label">Claude Desktop</text>
            <text x="105" y="250" text-anchor="middle" class="sub-label">Anthropic MCP</text>
            
            <rect x="190" y="210" width="130" height="50" rx="4" fill="white" stroke="#9f7aea"/>
            <text x="255" y="235" text-anchor="middle" class="component-label">Cursor IDE</text>
            <text x="255" y="250" text-anchor="middle" class="sub-label">Dev Tools</text>
            
            <rect x="40" y="280" width="130" height="50" rx="4" fill="white" stroke="#9f7aea"/>
            <text x="105" y="305" text-anchor="middle" class="component-label">Copilot Studio</text>
            <text x="105" y="320" text-anchor="middle" class="sub-label">Microsoft</text>
            
            <rect x="190" y="280" width="130" height="50" rx="4" fill="white" stroke="#9f7aea"/>
            <text x="255" y="305" text-anchor="middle" class="component-label">Custom Agents</text>
            <text x="255" y="320" text-anchor="middle" class="sub-label">Enterprise Apps</text>
            
            <!-- Zenity Monitoring Layer -->
            <rect x="380" y="170" width="240" height="180" rx="8" class="component-box security-zone"/>
            <text x="390" y="190" class="zone-label">Behavioral Monitoring</text>
            
            <!-- Zenity Component -->
            <rect x="400" y="210" width="200" height="120" rx="4" fill="url(#grad-zenity)"/>
            <text x="500" y="235" text-anchor="middle" class="product-label">ZENITY Platform</text>
            <line x1="410" y1="245" x2="590" y2="245" stroke="white" stroke-width="1" opacity="0.5"/>
            
            <text x="500" y="265" text-anchor="middle" fill="white" font-size="11">• Agent Discovery</text>
            <text x="500" y="285" text-anchor="middle" fill="white" font-size="11">• Behavioral Analysis</text>
            <text x="500" y="305" text-anchor="middle" fill="white" font-size="11">• Shadow AI Detection</text>
            <text x="500" y="325" text-anchor="middle" fill="white" font-size="11">• AIDR (Detection & Response)</text>
            
            <!-- TrojAI Security Layer -->
            <rect x="660" y="170" width="240" height="180" rx="8" class="component-box security-zone"/>
            <text x="670" y="190" class="zone-label">Model Security</text>
            
            <!-- TrojAI Component -->
            <rect x="680" y="210" width="200" height="120" rx="4" fill="url(#grad-trojai)"/>
            <text x="780" y="235" text-anchor="middle" class="product-label">TROJAI Platform</text>
            <line x1="690" y1="245" x2="870" y2="245" stroke="white" stroke-width="1" opacity="0.5"/>
            
            <text x="780" y="265" text-anchor="middle" fill="white" font-size="11">• Prompt Injection Defense</text>
            <text x="780" y="285" text-anchor="middle" fill="white" font-size="11">• Jailbreak Prevention</text>
            <text x="780" y="305" text-anchor="middle" fill="white" font-size="11">• Trojan Detection</text>
            <text x="780" y="325" text-anchor="middle" fill="white" font-size="11">• Red Team Testing</text>
            
            <!-- Barndoor Control Plane -->
            <rect x="380" y="390" width="520" height="200" rx="8" class="component-box mcp-zone"/>
            <text x="390" y="410" class="zone-label">MCP Control Plane</text>
            
            <!-- Barndoor Core -->
            <rect x="400" y="430" width="480" height="140" rx="4" fill="url(#grad-barndoor)"/>
            <text x="640" y="455" text-anchor="middle" class="product-label" font-size="14">BARNDOOR AI Gateway</text>
            <line x1="410" y1="465" x2="870" y2="465" stroke="white" stroke-width="1" opacity="0.5"/>
            
            <!-- Barndoor Components -->
            <g>
                <!-- Access Control -->
                <rect x="420" y="480" width="140" height="70" rx="4" fill="white" fill-opacity="0.95"/>
                <text x="490" y="505" text-anchor="middle" class="component-label" font-size="12">Access Control</text>
                <text x="490" y="525" text-anchor="middle" class="sub-label" font-size="10">• User Auth</text>
                <text x="490" y="540" text-anchor="middle" class="sub-label" font-size="10">• RBAC</text>
                
                <!-- Policy Engine -->
                <rect x="580" y="480" width="140" height="70" rx="4" fill="white" fill-opacity="0.95"/>
                <text x="650" y="505" text-anchor="middle" class="component-label" font-size="12">Policy Engine</text>
                <text x="650" y="525" text-anchor="middle" class="sub-label" font-size="10">• Tool Rules</text>
                <text x="650" y="540" text-anchor="middle" class="sub-label" font-size="10">• Context Policies</text>
                
                <!-- MCP Registry -->
                <rect x="740" y="480" width="120" height="70" rx="4" fill="white" fill-opacity="0.95"/>
                <text x="800" y="505" text-anchor="middle" class="component-label" font-size="12">MCP Registry</text>
                <text x="800" y="525" text-anchor="middle" class="sub-label" font-size="10">• Server List</text>
                <text x="800" y="540" text-anchor="middle" class="sub-label" font-size="10">• Approval</text>
            </g>
            
            <!-- MCP Servers Zone -->
            <rect x="940" y="170" width="440" height="420" rx="8" class="component-box infra-zone"/>
            <text x="950" y="190" class="zone-label">MCP Servers & Backend Systems</text>
            
            <!-- First Party MCP Servers -->
            <g>
                <rect x="960" y="210" width="180" height="60" rx="4" fill="white" stroke="#718096"/>
                <text x="1050" y="235" text-anchor="middle" class="component-label">First-Party MCP</text>
                <text x="1050" y="255" text-anchor="middle" class="sub-label">Salesforce, GitHub, Slack</text>
            </g>
            
            <!-- Third Party MCP Servers -->
            <g>
                <rect x="1180" y="210" width="180" height="60" rx="4" fill="white" stroke="#718096"/>
                <text x="1270" y="235" text-anchor="middle" class="component-label">Third-Party MCP</text>
                <text x="1270" y="255" text-anchor="middle" class="sub-label">OSS, Custom, Community</text>
            </g>
            
            <!-- Local MCP Servers -->
            <g>
                <rect x="960" y="290" width="180" height="60" rx="4" fill="white" stroke="#718096"/>
                <text x="1050" y="315" text-anchor="middle" class="component-label">Local MCP (stdio)</text>
                <text x="1050" y="335" text-anchor="middle" class="sub-label">File System, Local DB</text>
            </g>
            
            <!-- Remote MCP Servers -->
            <g>
                <rect x="1180" y="290" width="180" height="60" rx="4" fill="white" stroke="#718096"/>
                <text x="1270" y="315" text-anchor="middle" class="component-label">Remote MCP (HTTP)</text>
                <text x="1270" y="335" text-anchor="middle" class="sub-label">Cloud APIs, SaaS</text>
            </g>
            
            <!-- Enterprise Systems -->
            <rect x="960" y="380" width="400" height="190" rx="4" fill="#f7fafc" stroke="#cbd5e0" stroke-dasharray="5,5"/>
            <text x="970" y="400" class="zone-label" font-size="11">Enterprise Backend</text>
            
            <!-- Backend Systems -->
            <rect x="980" y="420" width="110" height="50" rx="4" fill="white" stroke="#cbd5e0"/>
            <text x="1035" y="445" text-anchor="middle" class="sub-label">CRM</text>
            <text x="1035" y="460" text-anchor="middle" class="sub-label" font-size="10">Salesforce</text>
            
            <rect x="1100" y="420" width="110" height="50" rx="4" fill="white" stroke="#cbd5e0"/>
            <text x="1155" y="445" text-anchor="middle" class="sub-label">Database</text>
            <text x="1155" y="460" text-anchor="middle" class="sub-label" font-size="10">SQL/NoSQL</text>
            
            <rect x="1220" y="420" width="120" height="50" rx="4" fill="white" stroke="#cbd5e0"/>
            <text x="1280" y="445" text-anchor="middle" class="sub-label">Cloud Storage</text>
            <text x="1280" y="460" text-anchor="middle" class="sub-label" font-size="10">S3, Azure Blob</text>
            
            <rect x="980" y="490" width="110" height="50" rx="4" fill="white" stroke="#cbd5e0"/>
            <text x="1035" y="515" text-anchor="middle" class="sub-label">APIs</text>
            <text x="1035" y="530" text-anchor="middle" class="sub-label" font-size="10">REST/GraphQL</text>
            
            <rect x="1100" y="490" width="110" height="50" rx="4" fill="white" stroke="#cbd5e0"/>
            <text x="1155" y="515" text-anchor="middle" class="sub-label">Identity</text>
            <text x="1155" y="530" text-anchor="middle" class="sub-label" font-size="10">AD/Okta</text>
            
            <rect x="1220" y="490" width="120" height="50" rx="4" fill="white" stroke="#cbd5e0"/>
            <text x="1280" y="515" text-anchor="middle" class="sub-label">Productivity</text>
            <text x="1280" y="530" text-anchor="middle" class="sub-label" font-size="10">M365, Google</text>
            
            <!-- Infrastructure Security Layer -->
            <rect x="20" y="630" width="1360" height="120" rx="8" class="component-box infra-zone"/>
            <text x="30" y="650" class="zone-label">Infrastructure & Platform Security</text>
            
            <!-- Infrastructure Components -->
            <rect x="40" y="670" width="140" height="60" rx="4" fill="white" stroke="#718096"/>
            <text x="110" y="695" text-anchor="middle" class="component-label">Network Security</text>
            <text x="110" y="715" text-anchor="middle" class="sub-label">Firewall, WAF, IDS</text>
            
            <rect x="200" y="670" width="140" height="60" rx="4" fill="white" stroke="#718096"/>
            <text x="270" y="695" text-anchor="middle" class="component-label">SIEM/SOAR</text>
            <text x="270" y="715" text-anchor="middle" class="sub-label">Splunk, Sentinel</text>
            
            <rect x="360" y="670" width="140" height="60" rx="4" fill="white" stroke="#718096"/>
            <text x="430" y="695" text-anchor="middle" class="component-label">Data Protection</text>
            <text x="430" y="715" text-anchor="middle" class="sub-label">DLP, Encryption</text>
            
            <rect x="520" y="670" width="140" height="60" rx="4" fill="white" stroke="#718096"/>
            <text x="590" y="695" text-anchor="middle" class="component-label">Identity/Access</text>
            <text x="590" y="715" text-anchor="middle" class="sub-label">IAM, MFA, SSO</text>
            
            <rect x="680" y="670" width="140" height="60" rx="4" fill="white" stroke="#718096"/>
            <text x="750" y="695" text-anchor="middle" class="component-label">Cloud Security</text>
            <text x="750" y="715" text-anchor="middle" class="sub-label">CSPM, CWPP</text>
            
            <rect x="840" y="670" width="140" height="60" rx="4" fill="white" stroke="#718096"/>
            <text x="910" y="695" text-anchor="middle" class="component-label">Compliance</text>
            <text x="910" y="715" text-anchor="middle" class="sub-label">GDPR, HIPAA, SOC2</text>
            
            <!-- Monitoring & Logging -->
            <rect x="1020" y="630" width="340" height="100" rx="8" fill="white" stroke="#48bb78" stroke-width="2"/>
            <text x="1030" y="650" class="zone-label" fill="#48bb78">Centralized Monitoring & Analytics</text>
            
            <rect x="1040" y="670" width="140" height="40" rx="4" fill="#f0fff4" stroke="#48bb78"/>
            <text x="1110" y="695" text-anchor="middle" class="sub-label">Audit Logs</text>
            
            <rect x="1200" y="670" width="140" height="40" rx="4" fill="#f0fff4" stroke="#48bb78"/>
            <text x="1270" y="695" text-anchor="middle" class="sub-label">Telemetry & Metrics</text>
            
            <!-- Flow Arrows -->
            <!-- User to Apps -->
            <path d="M 180 140 L 180 210" class="data-flow"/>
            
            <!-- Apps to Zenity (monitoring) -->
            <path d="M 340 260 L 400 260" class="control-flow"/>
            
            <!-- Apps to TrojAI (through) -->
            <path d="M 340 290 Q 500 290 680 290" class="security-flow"/>
            
            <!-- Apps to Barndoor -->
            <path d="M 255 330 L 255 430 L 400 430" class="data-flow"/>
            
            <!-- Zenity monitoring Barndoor -->
            <path d="M 500 330 L 500 430" class="control-flow"/>
            
            <!-- TrojAI to Barndoor -->
            <path d="M 780 330 L 780 430" class="security-flow"/>
            
            <!-- Barndoor to MCP Servers -->
            <path d="M 880 510 L 960 510 L 960 240" class="data-flow"/>
            <path d="M 880 510 L 1180 510 L 1180 240" class="data-flow"/>
            
            <!-- MCP to Backend -->
            <path d="M 1050 350 L 1050 420" class="data-flow"/>
            <path d="M 1270 350 L 1270 420" class="data-flow"/>
            
            <!-- Infrastructure monitoring -->
            <path d="M 640 590 L 640 630" class="control-flow"/>
            <path d="M 1190 630 L 1190 570" class="control-flow"/>
            
            <!-- Threat Flow Examples -->
            <g opacity="0.7">
                <path d="M 105 140 Q 105 380 380 480" class="threat-flow"/>
                <text x="200" y="370" fill="#e53e3e" font-size="10" font-weight="600">Threat Path</text>
            </g>
            
            <!-- Labels for Key Integration Points -->
            <circle cx="500" cy="380" r="20" fill="#48bb78" opacity="0.2"/>
            <text x="500" y="385" text-anchor="middle" font-size="10" font-weight="600" fill="#48bb78">1</text>
            
            <circle cx="780" cy="380" r="20" fill="#48bb78" opacity="0.2"/>
            <text x="780" y="385" text-anchor="middle" font-size="10" font-weight="600" fill="#48bb78">2</text>
            
            <circle cx="640" cy="610" r="20" fill="#48bb78" opacity="0.2"/>
            <text x="640" y="615" text-anchor="middle" font-size="10" font-weight="600" fill="#48bb78">3</text>
            
            <!-- Integration Labels -->
            <text x="520" y="410" font-size="9" fill="#48bb78">API Integration</text>
            <text x="800" y="410" font-size="9" fill="#48bb78">Inline Scanning</text>
            <text x="660" y="640" font-size="9" fill="#48bb78">Log Aggregation</text>
            
            <!-- Security Boundaries -->
            <rect x="370" y="160" width="540" height="440" rx="12" fill="none" stroke="#e53e3e" stroke-width="2" stroke-dasharray="10,5" opacity="0.3"/>
            <text x="640" y="155" text-anchor="middle" fill="#e53e3e" font-size="11" font-weight="600">Security Perimeter</text>
            
            <!-- Trust Boundary -->
            <rect x="930" y="160" width="460" height="440" rx="12" fill="none" stroke="#2b6cb1" stroke-width="2" stroke-dasharray="10,5" opacity="0.3"/>
            <text x="1160" y="155" text-anchor="middle" fill="#2b6cb1" font-size="11" font-weight="600">Enterprise Trust Boundary</text>
        </svg>
        
        <!-- Legend -->
        <div class="legend">
            <div class="legend-title">Flow Types & Components</div>
            <div class="legend-items">
                <div class="legend-item">
                    <svg width="40" height="2"><line x1="0" y1="1" x2="40" y2="1" stroke="#4299e1" stroke-width="2"/></svg>
                    <span>Data Flow (Request/Response)</span>
                </div>
                <div class="legend-item">
                    <svg width="40" height="2"><line x1="0" y1="1" x2="40" y2="1" stroke="#9f7aea" stroke-width="2" stroke-dasharray="5,5"/></svg>
                    <span>Control/Monitoring Flow</span>
                </div>
                <div class="legend-item">
                    <svg width="40" height="2"><line x1="0" y1="1" x2="40" y2="1" stroke="#48bb78" stroke-width="2" stroke-dasharray="2,2"/></svg>
                    <span>Security Inspection</span>
                </div>
                <div class="legend-item">
                    <svg width="40" height="2"><line x1="0" y1="1" x2="40" y2="1" stroke="#e53e3e" stroke-width="1.5" stroke-dasharray="3,3"/></svg>
                    <span>Potential Threat Path</span>
                </div>
                <div class="legend-item">
                    <div style="width: 20px; height: 20px; background: linear-gradient(135deg, #805ad5, #6b46c1); border-radius: 3px;"></div>
                    <span>Barndoor Components</span>
                </div>
                <div class="legend-item">
                    <div style="width: 20px; height: 20px; background: linear-gradient(135deg, #3182ce, #2c5282); border-radius: 3px;"></div>
                    <span>Zenity Components</span>
                </div>
                <div class="legend-item">
                    <div style="width: 20px; height: 20px; background: linear-gradient(135deg, #e53e3e, #c53030); border-radius: 3px;"></div>
                    <span>TrojAI Components</span>
                </div>
            </div>
        </div>
        
        <!-- Key Integration Points -->
        <div class="legend" style="margin-top: 20px;">
            <div class="legend-title">Key Integration Points</div>
            <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 15px; margin-top: 15px;">
                <div style="display: flex; align-items: start; gap: 10px;">
                    <div style="background: #48bb78; color: white; border-radius: 50%; width: 24px; height: 24px; display: flex; align-items: center; justify-content: center; font-weight: 600; font-size: 12px; flex-shrink: 0;">1</div>
                    <div>
                        <strong>Zenity → Barndoor:</strong> Behavioral telemetry, agent discovery data, risk scores for policy updates
                    </div>
                </div>
                <div style="display: flex; align-items: start; gap: 10px;">
                    <div style="background: #48bb78; color: white; border-radius: 50%; width: 24px; height: 24px; display: flex; align-items: center; justify-content: center; font-weight: 600; font-size: 12px; flex-shrink: 0;">2</div>
                    <div>
                        <strong>TrojAI → Barndoor:</strong> Model vulnerability scores, threat intelligence, real-time blocking signals
                    </div>
                </div>
                <div style="display: flex; align-items: start; gap: 10px;">
                    <div style="background: #48bb78; color: white; border-radius: 50%; width: 24px; height: 24px; display: flex; align-items: center; justify-content: center; font-weight: 600; font-size: 12px; flex-shrink: 0;">3</div>
                    <div>
                        <strong>All → SIEM:</strong> Centralized logging, correlation, incident response orchestration
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Critical Functions -->
        <div class="legend" style="margin-top: 20px; background: #fef5e7; border-color: #f39c12;">
            <div class="legend-title" style="color: #e67e22;">🔐 Critical Security Functions by Component</div>
            <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-top: 15px;">
                <div>
                    <strong style="color: #805ad5;">Barndoor (Control Plane):</strong>
                    <ul style="margin: 5px 0; padding-left: 20px; font-size: 12px;">
                        <li>MCP traffic gatekeeping</li>
                        <li>Tool-level authorization</li>
                        <li>Policy enforcement</li>
                        <li>Audit trail generation</li>
                    </ul>
                </div>
                <div>
                    <strong style="color: #3182ce;">Zenity (Behavioral):</strong>
                    <ul style="margin: 5px 0; padding-left: 20px; font-size: 12px;">
                        <li>Agent behavior analysis</li>
                        <li>Shadow AI discovery</li>
                        <li>Runtime anomaly detection</li>
                        <li>Multi-step attack detection</li>
                    </ul>
                </div>
                <div>
                    <strong style="color: #e53e3e;">TrojAI (Model Security):</strong>
                    <ul style="margin: 5px 0; padding-left: 20px; font-size: 12px;">
                        <li>Prompt injection blocking</li>
                        <li>Jailbreak prevention</li>
                        <li>Trojan/backdoor scanning</li>
                        <li>Adversarial defense</li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</body>
</html>
