# test

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Security Product Evaluation Dashboard</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #f0f2f5;
            color: #1e3a5f;
        }
        
        .dashboard {
            max-width: 1920px;
            margin: 0 auto;
            padding: 20px;
        }
        
        .header {
            background: linear-gradient(135deg, #1e3a5f 0%, #2c5282 100%);
            color: white;
            padding: 25px 30px;
            border-radius: 10px;
            margin-bottom: 25px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        
        .header h1 {
            font-size: 28px;
            font-weight: 300;
            letter-spacing: 1px;
        }
        
        .header .subtitle {
            font-size: 14px;
            opacity: 0.9;
            margin-top: 5px;
        }
        
        .kpi-row {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 25px;
        }
        
        .kpi-card {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 4px rgba(30,58,95,0.1);
            border-left: 4px solid #1e3a5f;
            transition: transform 0.2s, box-shadow 0.2s;
        }
        
        .kpi-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(30,58,95,0.15);
        }
        
        .kpi-label {
            font-size: 12px;
            color: #6b7280;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin-bottom: 8px;
        }
        
        .kpi-value {
            font-size: 32px;
            font-weight: 600;
            color: #1e3a5f;
        }
        
        .kpi-change {
            font-size: 12px;
            margin-top: 5px;
            color: #10b981;
        }
        
        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
            margin-bottom: 25px;
        }
        
        .panel {
            background: white;
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 2px 4px rgba(30,58,95,0.1);
        }
        
        .panel-title {
            font-size: 18px;
            font-weight: 600;
            color: #1e3a5f;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 2px solid #e5e7eb;
        }
        
        .status-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
        }
        
        .status-item {
            display: flex;
            align-items: center;
            padding: 15px;
            background: #f8fafc;
            border-radius: 8px;
            border: 1px solid #e5e7eb;
        }
        
        .status-icon {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 15px;
            font-weight: bold;
            font-size: 16px;
        }
        
        .status-icon.research { background: #dbeafe; color: #1e40af; }
        .status-icon.poc { background: #fef3c7; color: #d97706; }
        .status-icon.procurement { background: #d1fae5; color: #065f46; }
        .status-icon.deployed { background: #e0e7ff; color: #3730a3; }
        
        .category-chart {
            height: 300px;
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .donut-chart {
            position: relative;
            width: 200px;
            height: 200px;
        }
        
        .donut-chart svg {
            transform: rotate(-90deg);
        }
        
        .chart-legend {
            margin-left: 40px;
        }
        
        .legend-item {
            display: flex;
            align-items: center;
            margin-bottom: 12px;
        }
        
        .legend-color {
            width: 12px;
            height: 12px;
            border-radius: 2px;
            margin-right: 10px;
        }
        
        .product-table {
            width: 100%;
            margin-top: 25px;
        }
        
        .product-table table {
            width: 100%;
            border-collapse: collapse;
        }
        
        .product-table th {
            background: #1e3a5f;
            color: white;
            padding: 12px;
            text-align: left;
            font-weight: 500;
            font-size: 14px;
        }
        
        .product-table td {
            padding: 12px;
            border-bottom: 1px solid #e5e7eb;
            font-size: 14px;
        }
        
        .product-table tr:hover {
            background: #f8fafc;
        }
        
        .vendor-logo {
            width: 80px;
            height: 30px;
            object-fit: contain;
            background: #f8fafc;
            padding: 5px;
            border-radius: 4px;
        }
        
        .status-badge {
            display: inline-block;
            padding: 4px 12px;
            border-radius: 12px;
            font-size: 12px;
            font-weight: 500;
        }
        
        .status-badge.research { background: #dbeafe; color: #1e40af; }
        .status-badge.poc { background: #fef3c7; color: #d97706; }
        .status-badge.procurement { background: #d1fae5; color: #065f46; }
        .status-badge.deployed { background: #e0e7ff; color: #3730a3; }
        
        .link-button {
            display: inline-block;
            padding: 4px 8px;
            background: #1e3a5f;
            color: white;
            text-decoration: none;
            border-radius: 4px;
            font-size: 12px;
            margin-right: 5px;
        }
        
        .link-button:hover {
            background: #2c5282;
        }
        
        .timeline-section {
            margin-top: 25px;
        }
        
        .timeline-bar {
            background: #f8fafc;
            border-radius: 8px;
            padding: 20px;
            margin-bottom: 15px;
            border: 1px solid #e5e7eb;
        }
        
        .timeline-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;
        }
        
        .progress-bar {
            height: 8px;
            background: #e5e7eb;
            border-radius: 4px;
            overflow: hidden;
        }
        
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #1e3a5f, #2c5282);
            border-radius: 4px;
            transition: width 0.3s ease;
        }
        
        .filters {
            display: flex;
            gap: 15px;
            margin-bottom: 25px;
            padding: 15px;
            background: white;
            border-radius: 10px;
            box-shadow: 0 2px 4px rgba(30,58,95,0.1);
        }
        
        .filter-item {
            display: flex;
            flex-direction: column;
        }
        
        .filter-label {
            font-size: 12px;
            color: #6b7280;
            margin-bottom: 5px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        
        .filter-select {
            padding: 8px 12px;
            border: 1px solid #e5e7eb;
            border-radius: 6px;
            background: white;
            color: #1e3a5f;
            font-size: 14px;
            cursor: pointer;
        }
        
        .vendor-showcase {
            display: flex;
            gap: 20px;
            padding: 20px;
            background: #f8fafc;
            border-radius: 8px;
            overflow-x: auto;
        }
        
        .vendor-card {
            min-width: 120px;
            padding: 15px;
            background: white;
            border-radius: 8px;
            text-align: center;
            border: 1px solid #e5e7eb;
        }
        
        .vendor-card img {
            width: 80px;
            height: 40px;
            object-fit: contain;
            margin-bottom: 8px;
        }
        
        .vendor-name {
            font-size: 12px;
            color: #6b7280;
        }
    </style>
</head>
<body>
    <div class="dashboard">
        <!-- Header -->
        <div class="header">
            <h1>Security Product Evaluation Dashboard</h1>
            <div class="subtitle">Real-time tracking of security technology evaluations and deployments</div>
        </div>
        
        <!-- Filters -->
        <div class="filters">
            <div class="filter-item">
                <span class="filter-label">Category</span>
                <select class="filter-select">
                    <option>All Categories</option>
                    <option>AI/ML Security</option>
                    <option>Cloud Security</option>
                    <option>Identity & Access</option>
                    <option>Data Protection</option>
                </select>
            </div>
            <div class="filter-item">
                <span class="filter-label">Status</span>
                <select class="filter-select">
                    <option>All Status</option>
                    <option>Researching</option>
                    <option>In POC</option>
                    <option>Procurement</option>
                    <option>Deployed</option>
                </select>
            </div>
            <div class="filter-item">
                <span class="filter-label">Priority</span>
                <select class="filter-select">
                    <option>All Priorities</option>
                    <option>High</option>
                    <option>Medium</option>
                    <option>Low</option>
                </select>
            </div>
            <div class="filter-item">
                <span class="filter-label">Owner</span>
                <select class="filter-select">
                    <option>All Owners</option>
                    <option>Security Architecture</option>
                    <option>Cloud Security</option>
                    <option>AppSec Team</option>
                </select>
            </div>
        </div>
        
        <!-- KPI Cards -->
        <div class="kpi-row">
            <div class="kpi-card">
                <div class="kpi-label">Total in Pipeline</div>
                <div class="kpi-value">43</div>
                <div class="kpi-change">↑ 5 from last month</div>
            </div>
            <div class="kpi-card">
                <div class="kpi-label">Active POCs</div>
                <div class="kpi-value">8</div>
                <div class="kpi-change">2 completing this week</div>
            </div>
            <div class="kpi-card">
                <div class="kpi-label">Awaiting Decision</div>
                <div class="kpi-value">12</div>
                <div class="kpi-change">3 urgent</div>
            </div>
            <div class="kpi-card">
                <div class="kpi-label">Deployed YTD</div>
                <div class="kpi-value">15</div>
                <div class="kpi-change">75% success rate</div>
            </div>
            <div class="kpi-card">
                <div class="kpi-label">Avg. Eval Time</div>
                <div class="kpi-value">47<span style="font-size: 16px; font-weight: 400;"> days</span></div>
                <div class="kpi-change">↓ 8 days improved</div>
            </div>
        </div>
        
        <!-- Main Content Grid -->
        <div class="main-content">
            <!-- Status Distribution -->
            <div class="panel">
                <h2 class="panel-title">Evaluation Status Overview</h2>
                <div class="status-grid">
                    <div class="status-item">
                        <div class="status-icon research">12</div>
                        <div>
                            <div style="font-weight: 600;">Researching</div>
                            <div style="font-size: 12px; color: #6b7280;">Initial Assessment</div>
                        </div>
                    </div>
                    <div class="status-item">
                        <div class="status-icon poc">8</div>
                        <div>
                            <div style="font-weight: 600;">In POC/Pilot</div>
                            <div style="font-size: 12px; color: #6b7280;">Testing Phase</div>
                        </div>
                    </div>
                    <div class="status-item">
                        <div class="status-icon procurement">5</div>
                        <div>
                            <div style="font-weight: 600;">Procurement</div>
                            <div style="font-size: 12px; color: #6b7280;">Contract Negotiation</div>
                        </div>
                    </div>
                    <div class="status-item">
                        <div class="status-icon deployed">18</div>
                        <div>
                            <div style="font-weight: 600;">Deployed</div>
                            <div style="font-size: 12px; color: #6b7280;">In Production</div>
                        </div>
                    </div>
                </div>
            </div>
            
            <!-- Category Distribution -->
            <div class="panel">
                <h2 class="panel-title">Products by Category</h2>
                <div class="category-chart">
                    <div class="donut-chart">
                        <svg width="200" height="200" viewBox="0 0 200 200">
                            <circle cx="100" cy="100" r="80" fill="none" stroke="#e5e7eb" stroke-width="40"/>
                            <circle cx="100" cy="100" r="80" fill="none" stroke="#1e3a5f" stroke-width="40" 
                                stroke-dasharray="125 377" stroke-dashoffset="0"/>
                            <circle cx="100" cy="100" r="80" fill="none" stroke="#2c5282" stroke-width="40" 
                                stroke-dasharray="75 377" stroke-dashoffset="-125"/>
                            <circle cx="100" cy="100" r="80" fill="none" stroke="#4a6fa5" stroke-width="40" 
                                stroke-dasharray="63 377" stroke-dashoffset="-200"/>
                            <circle cx="100" cy="100" r="80" fill="none" stroke="#7494c0" stroke-width="40" 
                                stroke-dasharray="50 377" stroke-dashoffset="-263"/>
                            <circle cx="100" cy="100" r="80" fill="none" stroke="#9bb3d3" stroke-width="40" 
                                stroke-dasharray="44 377" stroke-dashoffset="-313"/>
                        </svg>
                    </div>
                    <div class="chart-legend">
                        <div class="legend-item">
                            <div class="legend-color" style="background: #1e3a5f;"></div>
                            <span>Cloud Security (12)</span>
                        </div>
                        <div class="legend-item">
                            <div class="legend-color" style="background: #2c5282;"></div>
                            <span>AI/ML Security (8)</span>
                        </div>
                        <div class="legend-item">
                            <div class="legend-color" style="background: #4a6fa5;"></div>
                            <span>Identity & Access (7)</span>
                        </div>
                        <div class="legend-item">
                            <div class="legend-color" style="background: #7494c0;"></div>
                            <span>Data Protection (6)</span>
                        </div>
                        <div class="legend-item">
                            <div class="legend-color" style="background: #9bb3d3;"></div>
                            <span>Endpoint Security (10)</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Vendor Showcase -->
        <div class="panel">
            <h2 class="panel-title">Featured Vendors in Evaluation</h2>
            <div class="vendor-showcase">
                <div class="vendor-card">
                    <div style="height: 40px; background: #f0f0f0; border-radius: 4px; display: flex; align-items: center; justify-content: center; color: #666; font-size: 10px;">CrowdStrike</div>
                    <div class="vendor-name">Endpoint</div>
                </div>
                <div class="vendor-card">
                    <div style="height: 40px; background: #f0f0f0; border-radius: 4px; display: flex; align-items: center; justify-content: center; color: #666; font-size: 10px;">Palo Alto</div>
                    <div class="vendor-name">Network</div>
                </div>
                <div class="vendor-card">
                    <div style="height: 40px; background: #f0f0f0; border-radius: 4px; display: flex; align-items: center; justify-content: center; color: #666; font-size: 10px;">Wiz</div>
                    <div class="vendor-name">Cloud</div>
                </div>
                <div class="vendor-card">
                    <div style="height: 40px; background: #f0f0f0; border-radius: 4px; display: flex; align-items: center; justify-content: center; color: #666; font-size: 10px;">Okta</div>
                    <div class="vendor-name">Identity</div>
                </div>
                <div class="vendor-card">
                    <div style="height: 40px; background: #f0f0f0; border-radius: 4px; display: flex; align-items: center; justify-content: center; color: #666; font-size: 10px;">SentinelOne</div>
                    <div class="vendor-name">EDR</div>
                </div>
                <div class="vendor-card">
                    <div style="height: 40px; background: #f0f0f0; border-radius: 4px; display: flex; align-items: center; justify-content: center; color: #666; font-size: 10px;">Snyk</div>
                    <div class="vendor-name">AppSec</div>
                </div>
                <div class="vendor-card">
                    <div style="height: 40px; background: #f0f0f0; border-radius: 4px; display: flex; align-items: center; justify-content: center; color: #666; font-size: 10px;">Darktrace</div>
                    <div class="vendor-name">AI Security</div>
                </div>
                <div class="vendor-card">
                    <div style="height: 40px; background: #f0f0f0; border-radius: 4px; display: flex; align-items: center; justify-content: center; color: #666; font-size: 10px;">Zscaler</div>
                    <div class="vendor-name">SASE</div>
                </div>
            </div>
        </div>
        
        <!-- Product Pipeline Table -->
        <div class="panel product-table">
            <h2 class="panel-title">Active Product Pipeline</h2>
            <table>
                <thead>
                    <tr>
                        <th>TLM#</th>
                        <th>Product</th>
                        <th>Vendor Logo</th>
                        <th>Category</th>
                        <th>Status</th>
                        <th>Owner</th>
                        <th>Days in Status</th>
                        <th>Documentation</th>
                        <th>Priority</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>TLM-2025-001</td>
                        <td>Falcon Platform</td>
                        <td><div style="width: 80px; height: 30px; background: #f0f0f0; border-radius: 4px; display: flex; align-items: center; justify-content: center; color: #666; font-size: 10px;">CrowdStrike</div></td>
                        <td>Endpoint Security</td>
                        <td><span class="status-badge poc">In POC</span></td>
                        <td>John Smith</td>
                        <td>15</td>
                        <td>
                            <a href="#" class="link-button">Confluence</a>
                            <a href="#" class="link-button">SharePoint</a>
                        </td>
                        <td style="color: #dc2626; font-weight: 600;">High</td>
                    </tr>
                    <tr>
                        <td>TLM-2025-002</td>
                        <td>Prisma Cloud</td>
                        <td><div style="width: 80px; height: 30px; background: #f0f0f0; border-radius: 4px; display: flex; align-items: center; justify-content: center; color: #666; font-size: 10px;">Palo Alto</div></td>
                        <td>Cloud Security</td>
                        <td><span class="status-badge research">Researching</span></td>
                        <td>Sarah Johnson</td>
                        <td>8</td>
                        <td>
                            <a href="#" class="link-button">Confluence</a>
                        </td>
                        <td style="color: #f59e0b; font-weight: 600;">Medium</td>
                    </tr>
                    <tr>
                        <td>TLM-2025-003</td>
                        <td>Wiz Platform</td>
                        <td><div style="width: 80px; height: 30px; background: #f0f0f0; border-radius: 4px; display: flex; align-items: center; justify-content: center; color: #666; font-size: 10px;">Wiz</div></td>
                        <td>Cloud Security</td>
                        <td><span class="status-badge procurement">Procurement</span></td>
                        <td>Mike Chen</td>
                        <td>22</td>
                        <td>
                            <a href="#" class="link-button">Confluence</a>
                            <a href="#" class="link-button">SharePoint</a>
                        </td>
                        <td style="color: #dc2626; font-weight: 600;">High</td>
                    </tr>
                    <tr>
                        <td>TLM-2025-004</td>
                        <td>Workforce Identity</td>
                        <td><div style="width: 80px; height: 30px; background: #f0f0f0; border-radius: 4px; display: flex; align-items: center; justify-content: center; color: #666; font-size: 10px;">Okta</div></td>
                        <td>Identity & Access</td>
                        <td><span class="status-badge deployed">Deployed</span></td>
                        <td>Lisa Wong</td>
                        <td>5</td>
                        <td>
                            <a href="#" class="link-button">Confluence</a>
                            <a href="#" class="link-button">SharePoint</a>
                        </td>
                        <td style="color: #10b981; font-weight: 600;">Low</td>
                    </tr>
                    <tr>
                        <td>TLM-2025-005</td>
                        <td>Singularity XDR</td>
                        <td><div style="width: 80px; height: 30px; background: #f0f0f0; border-radius: 4px; display: flex; align-items: center; justify-content: center; color: #666; font-size: 10px;">SentinelOne</div></td>
                        <td>Endpoint Security</td>
                        <td><span class="status-badge poc">In POC</span></td>
                        <td>David Park</td>
                        <td>31</td>
                        <td>
                            <a href="#" class="link-button">Confluence</a>
                        </td>
                        <td style="color: #f59e0b; font-weight: 600;">Medium</td>
                    </tr>
                </tbody>
            </table>
        </div>
        
        <!-- Timeline Section -->
        <div class="panel timeline-section">
            <h2 class="panel-title">Key Milestones & Deadlines</h2>
            <div class="timeline-bar">
                <div class="timeline-header">
                    <div>
                        <strong>CrowdStrike Falcon</strong> - POC Completion
                        <div style="font-size: 12px; color: #6b7280;">Target: Jan 31, 2025</div>
                    </div>
                    <div style="color: #10b981; font-size: 14px;">On Track</div>
                </div>
                <div class="progress-bar">
                    <div class="progress-fill" style="width: 75%;"></div>
                </div>
            </div>
            <div class="timeline-bar">
                <div class="timeline-header">
                    <div>
                        <strong>Wiz Platform</strong> - Contract Negotiation
                        <div style="font-size: 12px; color: #6b7280;">Target: Feb 15, 2025</div>
                    </div>
                    <div style="color: #f59e0b; font-size: 14px;">At Risk</div>
                </div>
                <div class="progress-bar">
                    <div class="progress-fill" style="width: 45%;"></div>
                </div>
            </div>
            <div class="timeline-bar">
                <div class="timeline-header">
                    <div>
                        <strong>Darktrace PREVENT</strong> - Initial Assessment
                        <div style="font-size: 12px; color: #6b7280;">Target: Mar 1, 2025</div>
                    </div>
                    <div style="color: #10b981; font-size: 14px;">On Track</div>
                </div>
                <div class="progress-bar">
                    <div class="progress-fill" style="width: 20%;"></div>
                </div>
            </div>
        </div>
    </div>
</body>
</html>
