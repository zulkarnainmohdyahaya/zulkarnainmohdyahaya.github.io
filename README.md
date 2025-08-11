<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Business Tracker Suite - ROI Calculator & P&L Tracker</title>
    <style>
        * {
            box-sizing: border-box;
        }
        
        body {
            font-family: Arial, sans-serif;
            max-width: 100%;
            margin: 0 auto;
            padding: 10px;
            background-color: #f5f5f5;
        }

        /* Tab Navigation Styles */
        .tab-container {
            background: white;
            border-radius: 10px 10px 0 0;
            padding: 0;
            margin-bottom: 0;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            max-width: 1200px;
            margin-left: auto;
            margin-right: auto;
        }

        .tab-navigation {
            display: flex;
            border-bottom: 3px solid #3498db;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 10px 10px 0 0;
        }

        .tab-button {
            flex: 1;
            padding: 15px 20px;
            background: transparent;
            border: none;
            color: white;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
        }

        .tab-button:first-child {
            border-radius: 10px 0 0 0;
        }

        .tab-button:last-child {
            border-radius: 0 10px 0 0;
        }

        .tab-button:hover {
            background: rgba(255,255,255,0.1);
        }

        .tab-button.active {
            background: white;
            color: #2c3e50;
        }

        .tab-button.active::after {
            content: '';
            position: absolute;
            bottom: -3px;
            left: 0;
            right: 0;
            height: 3px;
            background: #3498db;
        }

        /* Content Container */
        .content-container {
            background: white;
            border-radius: 0 0 10px 10px;
            padding: 0;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            max-width: 1200px;
            margin-left: auto;
            margin-right: auto;
        }

        .tab-content {
            display: none;
            padding: 20px;
        }

        .tab-content.active {
            display: block;
        }

        /* ROI Calculator Styles */
        .roi-container {
            max-width: 100%;
        }

        .roi-container .header {
            text-align: center;
            color: #2c3e50;
            margin-bottom: 20px;
        }

        .roi-container .header h1 {
            font-size: 1.5em;
            margin: 10px 0;
        }

        .roi-container .header p {
            font-size: 0.9em;
            margin: 5px 0;
        }

        .roi-container table {
            width: 100% !important;
            border-collapse: collapse !important;
            margin-bottom: 15px;
            font-size: 0.85em;
            table-layout: fixed !important;
            max-width: 100%;
        }

        .roi-container th, .roi-container td {
            border: 1px solid #ddd !important;
            padding: 8px !important;
            text-align: left !important;
            width: 25% !important;
            word-wrap: break-word;
            vertical-align: middle !important;
            height: 45px !important;
            min-height: 45px !important;
            max-height: auto;
            box-sizing: border-box !important;
            overflow: hidden;
        }

        .roi-container .formula-cell,
        .roi-container td:nth-child(2),
        .roi-container td:nth-child(3),
        .roi-container input[type="number"] {
            text-align: center !important;
        }

        .roi-container .input-cell {
            text-align: center !important;
            background-color: #ecf0f1 !important;
        }

        .roi-container table tr th:nth-child(1),
        .roi-container table tr td:nth-child(1) {
            width: 30% !important;
        }

        .roi-container table tr th:nth-child(2),
        .roi-container table tr td:nth-child(2) {
            width: 25% !important;
        }

        .roi-container table tr th:nth-child(3),
        .roi-container table tr td:nth-child(3) {
            width: 25% !important;
        }

        .roi-container table tr th:nth-child(4),
        .roi-container table tr td:nth-child(4) {
            width: 20% !important;
        }

        .roi-container th {
            background-color: #3498db !important;
            color: white !important;
            font-weight: bold !important;
            font-size: 0.75em !important;
            height: 45px !important;
            line-height: 1.2;
            text-align: center !important;
        }

        .roi-container .formula-cell {
            background-color: #e8f5e8 !important;
        }

        .roi-container .highlight {
            background-color: #fff3cd !important;
            font-weight: bold !important;
        }

        .roi-container .breakdown {
            background-color: #f8f9fa !important;
        }

        .roi-container input {
            width: 70% !important;
            max-width: 70px !important;
            padding: 4px !important;
            border: 1px solid #ccc !important;
            border-radius: 4px !important;
            text-align: center !important;
            font-size: 0.8em !important;
            box-sizing: border-box !important;
            margin: 0 auto !important;
            display: block !important;
        }

        .roi-container input[type="text"] {
            width: 80% !important;
            max-width: 100px !important;
            text-align: left !important;
        }

        .roi-container .profit-positive {
            color: #27ae60;
            font-weight: bold;
        }

        .roi-container .profit-negative {
            color: #e74c3c;
            font-weight: bold;
        }

        .roi-container .section-title {
            background-color: #f8f9fa !important;
            color: #000000 !important;
            text-align: center !important;
            font-weight: bold !important;
            font-size: 0.9em !important;
            border: 1px solid #dee2e6 !important;
        }

        .roi-container .verification {
            background-color: #e3f2fd;
            border-left: 4px solid #2196f3;
        }

        .roi-container .warning {
            background-color: #fff3e0;
            border-left: 4px solid #ff9800;
        }

        .roi-container .toggle-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 8px;
            margin: 8px 0;
            text-align: center;
        }

        .roi-container .toggle-switch {
            position: relative;
            display: inline-block;
            width: 50px;
            height: 28px;
        }

        .roi-container .toggle-switch input {
            opacity: 0;
            width: 0;
            height: 0;
        }

        .roi-container .slider {
            position: absolute;
            cursor: pointer;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: #ccc;
            transition: .4s;
            border-radius: 28px;
        }

        .roi-container .slider:before {
            position: absolute;
            content: "";
            height: 20px;
            width: 20px;
            left: 4px;
            bottom: 4px;
            background-color: white;
            transition: .4s;
            border-radius: 50%;
        }

        .roi-container input:checked + .slider {
            background-color: #2196F3;
        }

        .roi-container input:checked + .slider:before {
            transform: translateX(22px);
        }

        .roi-container .input-mode-label {
            font-weight: bold;
            color: #2c3e50;
            font-size: 0.85em;
            text-align: center;
        }

        .roi-container .ads-input-section {
            background-color: #f0f8ff;
            border: 2px solid #2196F3;
            border-radius: 8px;
            padding: 8px;
            text-align: center;
        }

        .roi-container .reference-links {
            font-size: 10px;
            color: #666;
            margin-top: 3px;
            line-height: 1.2;
            text-align: center;
        }

        .roi-container .reference-links a {
            color: #2196F3;
            text-decoration: none;
            margin: 0 5px;
            display: inline-block;
            padding: 2px 4px;
            border-radius: 3px;
            background: rgba(33, 150, 243, 0.1);
        }

        .roi-container .reference-links a:hover {
            background: rgba(33, 150, 243, 0.2);
            text-decoration: underline;
        }

        .roi-container .fee-note {
            background-color: #f8f9fa;
            border-left: 3px solid #2196F3;
            padding: 6px;
            margin: 4px 0;
            font-size: 10px;
            text-align: center;
        }

        .roi-container .editable-text {
            cursor: text;
            padding: 6px;
            border: 1px dashed #ccc;
            background-color: #f9f9f9;
            text-align: center;
        }

        .roi-container .editable-text:hover {
            background-color: #e6f3ff;
            border-color: #2196F3;
        }

        .roi-container .editable-text:focus {
            outline: 2px solid #2196F3;
            background-color: #f0f8ff;
        }

        /* P&L Tracker Styles */
        .pnl-container h1 {
            color: #2c3e50;
            text-align: center;
            margin-bottom: 30px;
            border-bottom: 3px solid #3498db;
            padding-bottom: 10px;
        }
        
        .pnl-container .section {
            margin-bottom: 25px;
            padding: 20px;
            border-radius: 8px;
            border-left: 4px solid #3498db;
        }
        
        .pnl-container .input-section {
            background-color: #ecf0f1;
        }
        
        .pnl-container .results-section {
            background-color: #e8f8f5;
        }
        
        .pnl-container .cash-section {
            background-color: #fef9e7;
        }
        
        .pnl-container h3 {
            color: #2c3e50;
            margin-top: 0;
            font-size: 18px;
        }
        
        .pnl-container .input-group {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-bottom: 15px;
        }
        
        .pnl-container .input-row {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 10px;
        }
        
        .pnl-container label {
            font-weight: bold;
            color: #34495e;
            flex: 1;
        }
        
        .pnl-container input {
            width: 120px;
            padding: 8px;
            border: 2px solid #bdc3c7;
            border-radius: 5px;
            text-align: right;
            font-size: 14px;
        }
        
        .pnl-container input:focus {
            border-color: #3498db;
            outline: none;
        }
        
        .pnl-container .result-row {
            display: flex;
            flex-direction: column;
            padding: 8px 0;
            border-bottom: 1px solid #ecf0f1;
        }
        
        .pnl-container .result-main {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 3px;
        }
        
        .pnl-container .result-label {
            font-weight: bold;
            color: #2c3e50;
        }
        
        .pnl-container .result-value {
            font-weight: bold;
            color: #27ae60;
            font-size: 16px;
        }
        
        .pnl-container .negative {
            color: #e74c3c !important;
        }
        
        .pnl-container .profit-highlight {
            background-color: #d5f4e6;
            padding: 15px;
            border-radius: 8px;
            margin: 10px 0;
            border: 2px solid #27ae60;
        }
        
        .pnl-container .loss-highlight {
            background-color: #fadbd8;
            padding: 15px;
            border-radius: 8px;
            margin: 10px 0;
            border: 2px solid #e74c3c;
        }
        
        .pnl-container .breakeven-value {
            font-weight: bold;
            color: #3498db !important;
            font-size: 16px;
        }
        
        .pnl-container .month-input {
            text-align: center;
            margin-bottom: 20px;
        }
        
        .pnl-container .month-input select {
            padding: 10px;
            font-size: 16px;
            border-radius: 5px;
            border: 2px solid #3498db;
        }
        
        .pnl-container .calculate-btn {
            background: #3498db;
            color: white;
            padding: 12px 30px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            cursor: pointer;
            display: block;
            margin: 20px auto;
            transition: background 0.3s;
        }
        
        .pnl-container .summary {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            margin-top: 20px;
        }

        /* Mobile Responsive */
        @media (max-width: 768px) {
            body {
                padding: 5px !important;
            }
            
            .tab-button {
                padding: 12px 10px;
                font-size: 14px;
            }
            
            .roi-container .header h1 {
                font-size: 1.2em !important;
            }
            
            .roi-container .header p {
                font-size: 0.75em !important;
            }
            
            .roi-container table {
                font-size: 0.7em !important;
                margin-bottom: 10px !important;
            }
            
            .roi-container th, .roi-container td {
                padding: 4px !important;
                height: 35px !important;
                min-height: 35px !important;
                font-size: 0.75em !important;
                line-height: 1.1 !important;
            }
            
            .roi-container th {
                font-size: 0.65em !important;
                padding: 4px 2px !important;
                height: 35px !important;
            }
            
            .roi-container input {
                width: 60% !important;
                max-width: 50px !important;
                font-size: 0.7em !important;
                padding: 3px !important;
            }
            
            .roi-container input[type="text"] {
                width: 70% !important;
                max-width: 70px !important;
            }
            
            .roi-container .toggle-switch {
                width: 35px !important;
                height: 20px !important;
            }
            
            .roi-container .slider:before {
                height: 14px !important;
                width: 14px !important;
            }
            
            .roi-container input:checked + .slider:before {
                transform: translateX(15px) !important;
            }
            
            .roi-container .reference-links {
                font-size: 8px !important;
            }
            
            .roi-container .fee-note {
                font-size: 8px !important;
                padding: 3px !important;
            }

            .pnl-container .input-group {
                grid-template-columns: 1fr;
                gap: 10px;
            }
        }
    </style>
</head>
<body>
    <!-- Tab Navigation -->
    <div class="tab-container">
        <div class="tab-navigation">
            <button class="tab-button active" onclick="switchTab('roi')">
                🔍 ROI Calculator
            </button>
            <button class="tab-button" onclick="switchTab('pnl')">
                📊 P&L Tracker
            </button>
        </div>
    </div>

    <!-- Content Container -->
    <div class="content-container">
        <!-- ROI Calculator Tab -->
        <div id="roi-tab" class="tab-content active">
            <div class="roi-container">
                <div class="header">
                    <h1>🇲🇾 ZUL ROAS ROI CALCULATOR</h1>
                    <p>Comprehensive TikTok Shop Analysis - Business Optimization Tool</p>
                </div>

                <!-- Product Information -->
                <table>
                    <tr class="section-title">
                        <td colspan="4">📦 PRODUCT INFORMATION</td>
                    </tr>
                    <tr>
                        <th>Item</th>
                        <th>Value</th>
                        <th>Type</th>
                        <th>Notes</th>
                    </tr>
                    <tr>
                        <td>Product Name</td>
                        <td class="input-cell"><input type="text" id="productName" value="Product Name" style="width: 150px;"></td>
                        <td>INPUT</td>
                        <td>Your product name</td>
                    </tr>
                    <tr>
                        <td>Target Market</td>
                        <td class="input-cell"><input type="text" id="targetMarket" value="Malaysia" style="width: 100px;"></td>
                        <td>INPUT</td>
                        <td>Your target market</td>
                    </tr>
                </table>

                <!-- Revenue Section -->
                <table>
                    <tr class="section-title">
                        <td colspan="4">💰 REVENUE & PRICING STRUCTURE</td>
                    </tr>
                    <tr>
                        <th>Item</th>
                        <th>Amount (RM)</th>
                        <th>Type</th>
                        <th>Notes</th>
                    </tr>
                    <tr>
                        <td>Selling Price per Unit</td>
                        <td class="input-cell"><input type="number" id="sellingPrice" value="14.50" step="0.01"></td>
                        <td>INPUT</td>
                        <td>Base revenue per sale</td>
                    </tr>
                    <tr>
                        <td>Shipping Fee (Customer Pays)</td>
                        <td class="input-cell"><input type="number" id="shippingFee" value="4.90" step="0.01"></td>
                        <td>INPUT</td>
                        <td>Additional customer cost</td>
                    </tr>
                    <tr class="highlight">
                        <td><strong>Total Customer Payment</strong></td>
                        <td class="formula-cell" id="totalPayment">19.40</td>
                        <td>AUTO</td>
                        <td>Selling Price + Shipping Fee</td>
                    </tr>
                </table>

                <!-- Cost Structure -->
                <table>
                    <tr class="section-title">
                        <td colspan="4">📋 DETAILED COST BREAKDOWN</td>
                    </tr>
                    <tr>
                        <th>Cost Category</th>
                        <th>Rate/Amount</th>
                        <th>Amount (RM)</th>
                        <th>Notes</th>
                    </tr>
                    <tr class="breakdown">
                        <td colspan="4"><strong>PRODUCT COSTS</strong></td>
                    </tr>
                    <tr>
                        <td>Cost of Goods Sold (COGS)</td>
                        <td class="input-cell"><input type="number" id="cogs" value="2.00" step="0.01"></td>
                        <td class="formula-cell" id="cogsAmount">2.00</td>
                        <td>Manufacturing/procurement cost</td>
                    </tr>
                    <tr>
                        <td>Fulfillment Cost</td>
                        <td class="input-cell"><input type="number" id="fulfillment" value="0.50" step="0.01"></td>
                        <td class="formula-cell" id="fulfillmentAmount">0.50</td>
                        <td>Pick, pack, ship to customer</td>
                    </tr>
                    <tr>
                        <td contenteditable="true" class="editable-text">Additional Product Cost 1</td>
                        <td class="input-cell"><input type="number" id="additionalProduct1" value="0.00" step="0.01"></td>
                        <td class="formula-cell" id="additionalProduct1Amount">0.00</td>
                        <td>Custom cost (optional)</td>
                    </tr>
                    <tr>
                        <td contenteditable="true" class="editable-text">Additional Product Cost 2</td>
                        <td class="input-cell"><input type="number" id="additionalProduct2" value="0.00" step="0.01"></td>
                        <td class="formula-cell" id="additionalProduct2Amount">0.00</td>
                        <td>Custom cost (optional)</td>
                    </tr>
                    <tr>
                        <td contenteditable="true" class="editable-text">Additional Product Cost 3</td>
                        <td class="input-cell"><input type="number" id="additionalProduct3" value="0.00" step="0.01"></td>
                        <td class="formula-cell" id="additionalProduct3Amount">0.00</td>
                        <td>Custom cost (optional)</td>
                    </tr>
                    <tr class="breakdown">
                        <td colspan="4"><strong>PLATFORM FEES</strong></td>
                    </tr>
                    <tr>
                        <td>Transaction Fee</td>
                        <td class="input-cell"><input type="number" id="transactionRate" value="3.78" step="0.01">%</td>
                        <td class="formula-cell" id="transactionAmount">0.73</td>
                        <td>% dari total customer payment
                            <div class="fee-note">
                                <strong>📋 Fee Details Reference:</strong>
                                <div class="reference-links">
                                    <a href="https://seller-my.tiktok.com/university/course?learning_id=7692879306114818&role=1&course_type=1&from=search&content_id=7753792938985218&identity=1" target="_blank">Fee Details Guide</a>
                                </div>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td>Marketplace Commission</td>
                        <td class="input-cell"><input type="number" id="marketplaceRate" value="11.34" step="0.01">%</td>
                        <td class="formula-cell" id="marketplaceAmount">1.64</td>
                        <td>% dari selling price
                            <div class="fee-note">
                                <strong>💼 Commission Fee Reference:</strong>
                                <div class="reference-links">
                                    <a href="https://seller-my.tiktok.com/university/essay?course_type=1&from=search&identity=1&knowledge_id=6907739532281602&role=1" target="_blank">Marketplace Commission Guide</a>
                                </div>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td>BXP Service Fee</td>
                        <td class="input-cell"><input type="number" id="bxpRate" value="3.24" step="0.01">%</td>
                        <td class="formula-cell" id="bxpAmount">0.47</td>
                        <td>% dari selling price
                            <div class="fee-note">
                                <strong>🚚 Shipping Program Fee Reference:</strong>
                                <div class="reference-links">
                                    <a href="https://seller-my.tiktok.com/university/essay?knowledge_id=3919892927842049&role=1&course_type=1&from=search&identity=1" target="_blank">Shipping Program Fee Guide</a>
                                </div>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td>Affiliate Fee</td>
                        <td class="input-cell"><input type="number" id="affiliateRate" value="5.00" step="0.01">%</td>
                        <td class="formula-cell" id="affiliateAmount">0.73</td>
                        <td>% dari selling price</td>
                    </tr>
                    <tr>
                        <td contenteditable="true" class="editable-text">Additional Platform Fee 1</td>
                        <td class="input-cell"><input type="number" id="additionalPlatform1Rate" value="0.00" step="0.01">%</td>
                        <td class="formula-cell" id="additionalPlatform1Amount">0.00</td>
                        <td>Custom platform fee (optional)</td>
                    </tr>
                    <tr>
                        <td contenteditable="true" class="editable-text">Additional Platform Fee 2</td>
                        <td class="input-cell"><input type="number" id="additionalPlatform2Rate" value="0.00" step="0.01">%</td>
                        <td class="formula-cell" id="additionalPlatform2Amount">0.00</td>
                        <td>Custom platform fee (optional)</td>
                    </tr>
                    <tr>
                        <td contenteditable="true" class="editable-text">Additional Platform Fee 3</td>
                        <td class="input-cell"><input type="number" id="additionalPlatform3Rate" value="0.00" step="0.01">%</td>
                        <td class="formula-cell" id="additionalPlatform3Amount">0.00</td>
                        <td>Custom platform fee (optional)</td>
                    </tr>
                    <tr class="highlight">
                        <td><strong>Total Fixed Costs</strong></td>
                        <td></td>
                        <td class="formula-cell" id="totalFixedCosts">6.07</td>
                        <td>All costs excluding ads</td>
                    </tr>
                </table>

                <!-- Enhanced Advertising Costs with Toggle -->
                <table>
                    <tr class="section-title">
                        <td colspan="4">📢 ADVERTISING COST STRUCTURE - ENHANCED</td>
                    </tr>
                    <tr class="ads-input-section">
                        <td colspan="4">
                            <div class="toggle-container">
                                <span class="input-mode-label" id="inputModeLabel">Input Mode: Percentage</span>
                                <label class="toggle-switch">
                                    <input type="checkbox" id="adsInputToggle">
                                    <span class="slider"></span>
                                </label>
                                <span style="font-size: 12px; color: #666;">Toggle: % ↔ RM Amount</span>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <th>Ads Component</th>
                        <th>Rate/Amount</th>
                        <th>Amount (RM)</th>
                        <th>Notes</th>
                    </tr>
                    <tr>
                        <td>Ads Spend</td>
                        <td class="input-cell">
                            <input type="number" id="adsRate" value="25.00" step="0.01" style="display: inline;">
                            <span id="adsRateUnit">%</span>
                            <input type="number" id="adsAmount" value="3.63" step="0.01" style="display: none;">
                            <span id="adsAmountUnit" style="display: none;">RM</span>
                        </td>
                        <td class="formula-cell" id="adsAmountDisplay">3.63</td>
                        <td id="adsNotes">% dari selling price</td>
                    </tr>
                    <tr>
                        <td>SST on Ads</td>
                        <td class="input-cell"><input type="number" id="sstRate" value="8.00" step="0.01">%</td>
                        <td class="formula-cell" id="sstAmount">0.29</td>
                        <td>% dari ads cost</td>
                    </tr>
                    <tr>
                        <td>WHT (if applicable)</td>
                        <td class="input-cell"><input type="number" id="wht" value="0.32" step="0.01"></td>
                        <td class="formula-cell" id="whtAmount">0.32</td>
                        <td>Withholding tax</td>
                    </tr>
                    <tr>
                        <td contenteditable="true" class="editable-text">Additional Ads Cost 1</td>
                        <td class="input-cell"><input type="number" id="additionalAds1" value="0.00" step="0.01"></td>
                        <td class="formula-cell" id="additionalAds1Amount">0.00</td>
                        <td>Custom ads cost (optional)</td>
                    </tr>
                    <tr>
                        <td contenteditable="true" class="editable-text">Additional Ads Cost 2</td>
                        <td class="input-cell"><input type="number" id="additionalAds2" value="0.00" step="0.01"></td>
                        <td class="formula-cell" id="additionalAds2Amount">0.00</td>
                        <td>Custom ads cost (optional)</td>
                    </tr>
                    <tr>
                        <td contenteditable="true" class="editable-text">Additional Ads Cost 3</td>
                        <td class="input-cell"><input type="number" id="additionalAds3" value="0.00" step="0.01"></td>
                        <td class="formula-cell" id="additionalAds3Amount">0.00</td>
                        <td>Custom ads cost (optional)</td>
                    </tr>
                    <tr class="highlight">
                        <td><strong>Total Advertising Costs</strong></td>
                        <td></td>
                        <td class="formula-cell" id="totalAdsCosts">4.24</td>
                        <td>All ads-related costs</td>
                    </tr>
                    <tr style="background-color: #f0f8ff;">
                        <td colspan="4">
                            <strong>💡 Quick Reference:</strong>
                            <span id="quickRef">25.0% = RM3.63 pure ads cost</span>
                        </td>
                    </tr>
                </table>

                <!-- Profitability Analysis -->
                <table>
                    <tr class="section-title">
                        <td colspan="4">📈 COMPREHENSIVE PROFITABILITY ANALYSIS</td>
                    </tr>
                    <tr>
                        <th>Metric</th>
                        <th>Amount (RM)</th>
                        <th>Percentage (%)</th>
                        <th>Interpretation</th>
                    </tr>
                    <tr>
                        <td>Gross Revenue</td>
                        <td class="formula-cell" id="grossRevenue">14.50</td>
                        <td>100.00%</td>
                        <td>Base selling price</td>
                    </tr>
                    <tr>
                        <td>Total All Costs</td>
                        <td class="formula-cell" id="totalAllCosts">10.31</td>
                        <td class="formula-cell" id="totalCostsPercent">71.1%</td>
                        <td>Fixed + Variable costs</td>
                    </tr>
                    <tr class="highlight">
                        <td><strong>Net Profit per Sale</strong></td>
                        <td class="formula-cell" id="netProfit">4.19</td>
                        <td class="formula-cell" id="profitMargin">28.9%</td>
                        <td>Actual earnings per sale</td>
                    </tr>
                </table>

                <!-- KPI Dashboard -->
                <table>
                    <tr class="section-title">
                        <td colspan="4">🎯 KEY PERFORMANCE INDICATORS DASHBOARD</td>
                    </tr>
                    <tr>
                        <th>KPI</th>
                        <th>Current Value</th>
                        <th>Breakeven Target</th>
                        <th>Formula & Notes</th>
                    </tr>
                    <tr>
                        <td><strong>ROAS</strong></td>
                        <td class="formula-cell" id="currentROAS">4.00</td>
                        <td class="formula-cell" id="breakevenROAS">1.86</td>
                        <td>Revenue ÷ Pure Ads Cost<br><em>RM revenue per RM1 ads</em></td>
                    </tr>
                    <tr>
                        <td><strong>TikTok GMV Max ROI</strong></td>
                        <td class="formula-cell" id="tiktokROI">4.00</td>
                        <td class="formula-cell" id="tiktokBreakevenROI">1.86</td>
                        <td>Gross Revenue ÷ Pure Ads Cost<br><em>TikTok's official calculation</em></td>
                    </tr>
                    <tr>
                        <td><strong>Standard Business ROI</strong></td>
                        <td class="formula-cell" id="standardROI">1.15</td>
                        <td class="formula-cell" id="standardBreakevenROI">0.00</td>
                        <td>Net Profit ÷ Pure Ads Cost<br><em>True business profitability</em></td>
                    </tr>
                    <tr>
                        <td><strong>Cost Per Order (CPO)</strong></td>
                        <td class="formula-cell" id="costPerOrder">4.24</td>
                        <td class="formula-cell" id="maxCPO">8.43</td>
                        <td>Total ads cost per sale<br><em>Customer acquisition cost</em></td>
                    </tr>
                </table>

                <!-- Breakeven Analysis with Verification -->
                <table>
                    <tr class="section-title">
                        <td colspan="4">⚖️ DETAILED BREAKEVEN ANALYSIS & VERIFICATION</td>
                    </tr>
                    <tr>
                        <th>Breakeven Component</th>
                        <th>Amount (RM)</th>
                        <th>Percentage (%)</th>
                        <th>Explanation</th>
                    </tr>
                    <tr class="verification">
                        <td><strong>Revenue Available for Ads</strong></td>
                        <td class="formula-cell" id="availableForAds">8.43</td>
                        <td class="formula-cell" id="availablePercent">58.1%</td>
                        <td>Revenue - All Fixed Costs</td>
                    </tr>
                    <tr class="verification">
                        <td><strong>Max Pure Ads Cost</strong></td>
                        <td class="formula-cell" id="maxPureAds">7.80</td>
                        <td class="formula-cell" id="maxPureAdsPercent">53.8%</td>
                        <td>Available ÷ (1 + SST%)</td>
                    </tr>
                    <tr class="verification">
                        <td><strong>SST on Max Ads</strong></td>
                        <td class="formula-cell" id="maxSST">0.62</td>
                        <td>4.3%</td>
                        <td>Max Pure Ads × SST%</td>
                    </tr>
                    <tr class="verification">
                        <td><strong>Total Max Ads Cost</strong></td>
                        <td class="formula-cell" id="totalMaxAds">8.42</td>
                        <td class="formula-cell" id="totalMaxAdsPercent">58.1%</td>
                        <td>Max Pure + SST + WHT</td>
                    </tr>
                </table>

                <!-- Verification Table -->
                <table>
                    <tr class="section-title">
                        <td colspan="4">✅ BREAKEVEN VERIFICATION - ALL COSTS INCLUDED</td>
                    </tr>
                    <tr class="verification">
                        <th>Cost Category</th>
                        <th>At Current</th>
                        <th>At Breakeven</th>
                        <th>Verification</th>
                    </tr>
                    <tr>
                        <td>COGS</td>
                        <td class="formula-cell" id="currentCOGS">2.00</td>
                        <td class="formula-cell" id="breakevenCOGS">2.00</td>
                        <td>✅ Included</td>
                    </tr>
                    <tr>
                        <td>Fulfillment</td>
                        <td class="formula-cell" id="currentFulfillment">0.50</td>
                        <td class="formula-cell" id="breakevenFulfillment">0.50</td>
                        <td>✅ Included</td>
                    </tr>
                    <tr>
                        <td>Platform Fees</td>
                        <td class="formula-cell" id="currentPlatformFees">3.57</td>
                        <td class="formula-cell" id="breakevenPlatformFees">3.57</td>
                        <td>✅ Included</td>
                    </tr>
                    <tr>
                        <td>Pure Ads Cost</td>
                        <td class="formula-cell" id="currentPureAds">3.63</td>
                        <td class="formula-cell" id="breakevenPureAds">7.80</td>
                        <td>✅ Variable</td>
                    </tr>
                    <tr>
                        <td>SST on Ads</td>
                        <td class="formula-cell" id="currentSST">0.29</td>
                        <td class="formula-cell" id="breakevenSST">0.62</td>
                        <td>✅ Calculated</td>
                    </tr>
                    <tr>
                        <td>WHT</td>
                        <td class="formula-cell" id="currentWHT">0.32</td>
                        <td class="formula-cell" id="breakevenWHT">0.32</td>
                        <td>✅ Included</td>
                    </tr>
                    <tr class="highlight">
                        <td><strong>TOTAL COSTS</strong></td>
                        <td class="formula-cell" id="verifyCurrentTotal">10.31</td>
                        <td class="formula-cell" id="verifyBreakevenTotal">14.81</td>
                        <td><strong>✅ Complete</strong></td>
                    </tr>
                    <tr class="highlight">
                        <td><strong>NET PROFIT</strong></td>
                        <td class="formula-cell" id="verifyCurrentProfit">4.19</td>
                        <td class="formula-cell" id="verifyBreakevenProfit">-0.31</td>
                        <td>Status Check</td>
                    </tr>
                </table>

                <!-- Comparative Analysis -->
                <table>
                    <tr class="section-title">
                        <td colspan="4">📊 TIKTOK vs BUSINESS PERSPECTIVE</td>
                    </tr>
                    <tr>
                        <th>Metric</th>
                        <th>TikTok Platform View</th>
                        <th>Business Reality</th>
                        <th>Key Difference</th>
                    </tr>
                    <tr>
                        <td><strong>ROI Calculation</strong></td>
                        <td>Gross Revenue ÷ Pure Ads</td>
                        <td>Net Profit ÷ Pure Ads</td>
                        <td>Revenue vs Profit focus</td>
                    </tr>
                    <tr>
                        <td><strong>Current Performance</strong></td>
                        <td class="formula-cell profit-positive" id="tiktokCurrentPerf">4.00 (Excellent)</td>
                        <td class="formula-cell profit-positive" id="businessCurrentPerf">1.15 (Profitable)</td>
                        <td>TikTok looks more impressive</td>
                    </tr>
                    <tr>
                        <td><strong>Breakeven Target</strong></td>
                        <td class="formula-cell" id="tiktokBreakevenTarget">1.86</td>
                        <td class="formula-cell" id="businessBreakevenTarget">0.00</td>
                        <td>Different thresholds</td>
                    </tr>
                    <tr>
                        <td><strong>Scaling Headroom</strong></td>
                        <td id="tiktokScalingHeadroom">ROAS can drop to 1.86</td>
                        <td id="businessScalingHeadroom">Can scale to 53.8% ads</td>
                        <td>Different scaling metrics</td>
                    </tr>
                </table>

                <!-- Comprehensive Scenario Analysis -->
                <table>
                    <tr class="section-title">
                        <td colspan="9">🔄 COMPREHENSIVE SCENARIO ANALYSIS</td>
                    </tr>
                    <tr>
                        <th>Ads %</th>
                        <th>Pure Ads (RM)</th>
                        <th>Total Ads (RM)</th>
                        <th>Total Costs (RM)</th>
                        <th>ROAS</th>
                        <th>TikTok ROI</th>
                        <th>Standard ROI</th>
                        <th>Net Profit (RM)</th>
                        <th>Status</th>
                    </tr>
                    <tbody id="scenarioTable">
                        <!-- Scenarios will be populated by JavaScript -->
                    </tbody>
                </table>

                <!-- Business Insights -->
                <table>
                    <tr class="section-title">
                        <td colspan="4">💡 BUSINESS INSIGHTS & RECOMMENDATIONS</td>
                    </tr>
                    <tr>
                        <th>Insight Category</th>
                        <th>Current Status</th>
                        <th>Recommendation</th>
                        <th>Action Item</th>
                    </tr>
                    <tr>
                        <td>Profitability Health</td>
                        <td class="formula-cell" id="healthStatus">✅ Healthy</td>
                        <td>Maintain current efficiency</td>
                        <td>Monitor profit margins</td>
                    </tr>
                    <tr>
                        <td>Scaling Potential</td>
                        <td class="formula-cell" id="scalingRoom">28.8% room</td>
                        <td>Gradual scaling recommended</td>
                        <td>Increase ads by 5-10%</td>
                    </tr>
                    <tr>
                        <td>Platform Performance</td>
                        <td class="formula-cell" id="platformPerf">Excellent ROI 4.00</td>
                        <td>Leverage for negotiations</td>
                        <td>Request better rates</td>
                    </tr>
                    <tr>
                        <td>Risk Assessment</td>
                        <td class="formula-cell" id="riskLevel">🟢 Low Risk</td>
                        <td>Safe to scale</td>
                        <td>Test higher budgets</td>
                    </tr>
                </table>
            </div>
        </div>

        <!-- P&L Tracker Tab -->
        <div id="pnl-tab" class="tab-content">
            <div class="pnl-container">
                <h1>Monthly Business P&L Tracker</h1>
                <p style="text-align: center; color: #7f8c8d; font-style: italic;">Business - Tracking Untung/Rugi</p>
                
                <div class="month-input">
                    <label for="month">Bulan: </label>
                    <select id="month">
                        <option value="Januari">Januari 2025</option>
                        <option value="Februari">Februari 2025</option>
                        <option value="Mac" selected>Mac 2025</option>
                        <option value="April">April 2025</option>
                        <option value="Mei">Mei 2025</option>
                        <option value="Jun">Jun 2025</option>
                        <option value="Julai">Julai 2025</option>
                        <option value="Ogos">Ogos 2025</option>
                        <option value="September">September 2025</option>
                        <option value="Oktober">Oktober 2025</option>
                        <option value="November">November 2025</option>
                        <option value="Disember">Disember 2025</option>
                    </select>
                </div>

                <!-- INPUT SECTION -->
                <div class="section input-section">
                    <h3>📊 DATA INPUT - REVENUE</h3>
                    <div class="input-group">
                        <div>
                            <div class="input-row">
                                <label>Total Orders Value (RM):</label>
                                <input type="number" id="ordersValue" step="0.01" placeholder="12000">
                            </div>
                            <div class="input-row">
                                <label>Less: Affiliate Fees (RM):</label>
                                <input type="number" id="affiliateFees" step="0.01" placeholder="1500">
                            </div>
                            <div class="input-row">
                                <label>Monthly Settlement (RM):</label>
                                <input type="number" id="settlement" step="0.01" placeholder="9000">
                            </div>
                        </div>
                        <div>
                            <div class="input-row">
                                <label>Total Units Sold:</label>
                                <input type="number" id="unitsSold" placeholder="200">
                            </div>
                        </div>
                    </div>
                </div>

                <div class="section input-section">
                    <h3>💰 DATA INPUT - COSTS</h3>
                    <div class="input-group">
                        <div>
                            <div class="input-row">
                                <label>Total COGS (RM):</label>
                                <input type="number" id="cogsPnl" step="0.01" placeholder="4000">
                            </div>
                            <div class="input-row">
                                <label>Monthly Ads Spend (RM):</label>
                                <input type="number" id="adsSpend" step="0.01" placeholder="1200">
                            </div>
                            <div class="input-row">
                                <label>Platform Fee (RM):</label>
                                <input type="number" id="platformFeePnl" step="0.01" placeholder="255">
                            </div>
                        </div>
                        <div>
                            <div class="input-row">
                                <label>Fulfillment Cost/Unit (RM):</label>
                                <input type="number" id="fulfillmentPerUnit" step="0.01" placeholder="3.50">
                            </div>
                            <div class="input-row">
                                <label>DST Total (RM):</label>
                                <input type="number" id="dst" step="0.01" placeholder="340">
                            </div>
                            <div class="input-row">
                                <label>Monthly Overhead (RM):</label>
                                <input type="number" id="overhead" step="0.01" placeholder="800">
                            </div>
                        </div>
                    </div>
                    
                    <!-- OVERHEAD BREAKDOWN -->
                    <div style="margin-top: 15px; padding: 15px; background-color: #f8f9fa; border-radius: 5px; border: 1px solid #dee2e6;">
                        <h4 style="margin: 0 0 10px 0; color: #495057; font-size: 14px;">💡 Overhead Breakdown (Optional Details):</h4>
                        <div class="input-group">
                            <div>
                                <div class="input-row">
                                    <label style="font-size: 13px;">Rent/Storage (RM):</label>
                                    <input type="number" id="overheadRent" step="0.01" placeholder="300">
                                </div>
                                <div class="input-row">
                                    <label style="font-size: 13px;">Utilities (RM):</label>
                                    <input type="number" id="overheadUtilities" step="0.01" placeholder="150">
                                </div>
                                <div class="input-row">
                                    <label style="font-size: 13px;">Staff/Commission (RM):</label>
                                    <input type="number" id="overheadStaff" step="0.01" placeholder="250">
                                </div>
                            </div>
                            <div>
                                <div class="input-row">
                                    <label style="font-size: 13px;">Phone/Internet (RM):</label>
                                    <input type="number" id="overheadComms" step="0.01" placeholder="80">
                                </div>
                                <div class="input-row">
                                    <label style="font-size: 13px;">Banking/Fees (RM):</label>
                                    <input type="number" id="overheadBanking" step="0.01" placeholder="20">
                                </div>
                                <div class="input-row">
                                    <label style="font-size: 13px;">Others (RM):</label>
                                    <input type="number" id="overheadOthers" step="0.01" placeholder="0">
                                </div>
                            </div>
                        </div>
                        <div style="text-align: center; margin-top: 10px;">
                            <button type="button" onclick="calculateOverheadTotal()" style="background: #6c757d; color: white; border: none; padding: 5px 15px; border-radius: 3px; font-size: 12px;">Auto-fill Total Overhead</button>
                        </div>
                    </div>
                </div>

                <button class="calculate-btn" onclick="calculateMetrics()">🧮 CALCULATE UNTUNG/RUGI</button>

                <!-- RESULTS SECTION -->
                <div class="section results-section">
                    <h3>📈 TRUE BUSINESS PERFORMANCE</h3>
                    <div class="result-row">
                        <div class="result-main">
                            <span class="result-label">Gross Revenue (after affiliate):</span>
                            <span class="result-value" id="grossRevenuePnl">RM 0.00</span>
                        </div>
                        <small style="color: #7f8c8d; font-style: italic;">Formula: Orders Value - Affiliate Fees</small>
                    </div>
                    <div class="result-row">
                        <div class="result-main">
                            <span class="result-label">Revenue per Unit:</span>
                            <span class="result-value" id="revenuePerUnit">RM 0.00</span>
                        </div>
                        <small style="color: #7f8c8d; font-style: italic;">Formula: Gross Revenue ÷ Units Sold</small>
                    </div>
                    <div class="result-row">
                        <div class="result-main">
                            <span class="result-label">Total Cost per Unit:</span>
                            <span class="result-value" id="costPerUnitPnl">RM 0.00</span>
                        </div>
                        <small style="color: #7f8c8d; font-style: italic;">Formula: (COGS + Ads + Platform Fee + DST + Overhead) ÷ Units + Fulfillment/Unit</small>
                    </div>
                    <div class="result-row">
                        <div class="result-main">
                            <span class="result-label">Affiliate Fee %:</span>
                            <span class="result-value" id="affiliatePercentage">0.0%</span>
                        </div>
                        <small style="color: #7f8c8d; font-style: italic;">Formula: (Affiliate Fees ÷ Orders Value) × 100</small>
                    </div>
                    
                    <div id="profitResult" class="profit-highlight">
                        <div class="result-row">
                            <div class="result-main">
                                <span class="result-label">UNTUNG/RUGI per Unit:</span>
                                <span class="result-value" id="profitPerUnitPnl">RM 0.00</span>
                            </div>
                            <small style="color: #2c3e50; font-weight: bold;">Formula: Revenue per Unit - Total Cost per Unit</small>
                        </div>
                        <div class="result-row">
                            <div class="result-main">
                                <span class="result-label">Total Monthly UNTUNG/RUGI:</span>
                                <span class="result-value" id="totalProfitPnl">RM 0.00</span>
                            </div>
                            <small style="color: #2c3e50; font-weight: bold;">Formula: Profit per Unit × Units Sold</small>
                        </div>
                        <div class="result-row">
                            <div class="result-main">
                                <span class="result-label">Profit Margin:</span>
                                <span class="result-value" id="profitMarginPnl">0.0%</span>
                            </div>
                            <small style="color: #2c3e50; font-weight: bold;">Formula: (Total Profit ÷ Gross Revenue) × 100</small>
                        </div>
                    </div>
                </div>

                <!-- CASH FLOW SECTION -->
                <div class="section cash-section">
                    <h3>💳 CASH FLOW POSITION</h3>
                    <div class="result-row">
                        <div class="result-main">
                            <span class="result-label">Settlement Received:</span>
                            <span class="result-value" id="settlementReceived">RM 0.00</span>
                        </div>
                        <small style="color: #7f8c8d; font-style: italic;">Formula: Direct input - duit actually masuk</small>
                    </div>
                    <div class="result-row">
                        <div class="result-main">
                            <span class="result-label">Pending Collections:</span>
                            <span class="result-value" id="pendingCollections">RM 0.00</span>
                        </div>
                        <small style="color: #7f8c8d; font-style: italic;">Formula: Gross Revenue - Settlement</small>
                    </div>
                    <div class="result-row">
                        <div class="result-main">
                            <span class="result-label">Cash Profit (from settlement):</span>
                            <span class="result-value" id="cashProfit">RM 0.00</span>
                        </div>
                        <small style="color: #7f8c8d; font-style: italic;">Formula: Settlement - Total All Costs</small>
                    </div>
                    <div class="result-row">
                        <div class="result-main">
                            <span class="result-label">Cash Profit Margin:</span>
                            <span class="result-value" id="cashMargin">0.0%</span>
                        </div>
                        <small style="color: #7f8c8d; font-style: italic;">Formula: (Cash Profit ÷ Settlement) × 100</small>
                    </div>
                </div>

                <!-- BREAKEVEN ANALYSIS -->
                <div class="section" style="background-color: #fff3cd; border-left: 4px solid #ffc107;">
                    <h3>⚖️ BREAKEVEN ANALYSIS</h3>
                    <div class="result-row">
                        <div class="result-main">
                            <span class="result-label">Breakeven Units (Monthly):</span>
                            <span class="breakeven-value" id="breakevenUnits">0</span>
                        </div>
                        <small style="color: #856404; font-weight: bold;">Formula: Fixed Costs ÷ (Revenue per Unit - Variable Cost per Unit)</small>
                    </div>
                    <div class="result-row">
                        <div class="result-main">
                            <span class="result-label">Breakeven Revenue (Monthly):</span>
                            <span class="breakeven-value" id="breakevenRevenuePnl">RM 0.00</span>
                        </div>
                        <small style="color: #856404; font-weight: bold;">Formula: Breakeven Units × Revenue per Unit</small>
                    </div>
                    <div class="result-row">
                        <div class="result-main">
                            <span class="result-label">Units Above/Below Breakeven:</span>
                            <span class="result-value" id="unitsVsBreakeven">0</span>
                        </div>
                        <small style="color: #856404; font-weight: bold;">Formula: Actual Units - Breakeven Units</small>
                    </div>
                    <div class="result-row">
                        <div class="result-main">
                            <span class="result-label">Safety Margin:</span>
                            <span class="result-value" id="safetyMargin">0.0%</span>
                        </div>
                        <small style="color: #856404; font-weight: bold;">Formula: ((Actual Units - Breakeven Units) ÷ Actual Units) × 100</small>
                    </div>
                </div>

                <div class="summary" id="summary">
                    <h3>📋 RINGKASAN BULAN INI</h3>
                    <p id="summaryText">Masukkan data untuk melihat ringkasan performance.</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Tab switching functionality
        function switchTab(tabName) {
            // Hide all tab contents
            const tabContents = document.querySelectorAll('.tab-content');
            tabContents.forEach(content => {
                content.classList.remove('active');
            });
            
            // Remove active class from all tab buttons
            const tabButtons = document.querySelectorAll('.tab-button');
            tabButtons.forEach(button => {
                button.classList.remove('active');
            });
            
            // Show selected tab content
            document.getElementById(tabName + '-tab').classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
            
            // Trigger calculations for the active tab
            if (tabName === 'roi') {
                updateCalculations();
            } else if (tabName === 'pnl') {
                calculateMetrics();
            }
        }

        // ROI Calculator JavaScript
        let isAmountMode = false;

        function toggleAdsInput() {
            const toggle = document.getElementById('adsInputToggle');
            const adsRate = document.getElementById('adsRate');
            const adsRateUnit = document.getElementById('adsRateUnit');
            const adsAmount = document.getElementById('adsAmount');
            const adsAmountUnit = document.getElementById('adsAmountUnit');
            const inputModeLabel = document.getElementById('inputModeLabel');
            const adsNotes = document.getElementById('adsNotes');

            isAmountMode = toggle.checked;

            if (isAmountMode) {
                // Switch to Amount mode
                adsRate.style.display = 'none';
                adsRateUnit.style.display = 'none';
                adsAmount.style.display = 'inline';
                adsAmountUnit.style.display = 'inline';
                inputModeLabel.textContent = 'Input Mode: Amount (RM)';
                adsNotes.textContent = 'Direct amount input';
            } else {
                // Switch to Percentage mode
                adsRate.style.display = 'inline';
                adsRateUnit.style.display = 'inline';
                adsAmount.style.display = 'none';
                adsAmountUnit.style.display = 'none';
                inputModeLabel.textContent = 'Input Mode: Percentage (%)';
                adsNotes.textContent = '% dari selling price';
            }
        }

        function updateCalculations() {
            // Get input values
            const sellingPrice = parseFloat(document.getElementById('sellingPrice').value) || 0;
            const shippingFee = parseFloat(document.getElementById('shippingFee').value) || 0;
            const cogs = parseFloat(document.getElementById('cogs').value) || 0;
            const fulfillment = parseFloat(document.getElementById('fulfillment').value) || 0;
            const additionalProduct1 = parseFloat(document.getElementById('additionalProduct1').value) || 0;
            const additionalProduct2 = parseFloat(document.getElementById('additionalProduct2').value) || 0;
            const additionalProduct3 = parseFloat(document.getElementById('additionalProduct3').value) || 0;
            const transactionRate = parseFloat(document.getElementById('transactionRate').value) || 0;
            const marketplaceRate = parseFloat(document.getElementById('marketplaceRate').value) || 0;
            const bxpRate = parseFloat(document.getElementById('bxpRate').value) || 0;
            const affiliateRate = parseFloat(document.getElementById('affiliateRate').value) || 0;
            const additionalPlatform1Rate = parseFloat(document.getElementById('additionalPlatform1Rate').value) || 0;
            const additionalPlatform2Rate = parseFloat(document.getElementById('additionalPlatform2Rate').value) || 0;
            const additionalPlatform3Rate = parseFloat(document.getElementById('additionalPlatform3Rate').value) || 0;
            const sstRate = parseFloat(document.getElementById('sstRate').value) || 0;
            const wht = parseFloat(document.getElementById('wht').value) || 0;
            const additionalAds1 = parseFloat(document.getElementById('additionalAds1').value) || 0;
            const additionalAds2 = parseFloat(document.getElementById('additionalAds2').value) || 0;
            const additionalAds3 = parseFloat(document.getElementById('additionalAds3').value) || 0;

            // Calculate ads amount based on input mode
            let pureAdsAmount;
            let adsRate;

            if (isAmountMode) {
                // Amount mode: get amount, calculate percentage
                pureAdsAmount = parseFloat(document.getElementById('adsAmount').value) || 0;
                adsRate = sellingPrice > 0 ? (pureAdsAmount / sellingPrice) * 100 : 0;
                // Update the percentage field (for reference)
                document.getElementById('adsRate').value = adsRate.toFixed(2);
            } else {
                // Percentage mode: get percentage, calculate amount
                adsRate = parseFloat(document.getElementById('adsRate').value) || 0;
                pureAdsAmount = sellingPrice * (adsRate / 100);
                // Update the amount field (for reference)
                document.getElementById('adsAmount').value = pureAdsAmount.toFixed(2);
            }

            // Calculate derived values
            const totalPayment = sellingPrice + shippingFee;
            const transactionAmount = totalPayment * (transactionRate / 100);
            const marketplaceAmount = sellingPrice * (marketplaceRate / 100);
            const bxpAmount = sellingPrice * (bxpRate / 100);
            const affiliateAmount = sellingPrice * (affiliateRate / 100);
            const additionalPlatform1Amount = sellingPrice * (additionalPlatform1Rate / 100);
            const additionalPlatform2Amount = sellingPrice * (additionalPlatform2Rate / 100);
            const additionalPlatform3Amount = sellingPrice * (additionalPlatform3Rate / 100);
            const platformFees = transactionAmount + marketplaceAmount + bxpAmount + affiliateAmount + additionalPlatform1Amount + additionalPlatform2Amount + additionalPlatform3Amount;
            
            const totalFixedCosts = cogs + fulfillment + additionalProduct1 + additionalProduct2 + additionalProduct3 + platformFees;
            
            const sstAmount = pureAdsAmount * (sstRate / 100);
            const totalAdsCosts = pureAdsAmount + sstAmount + wht + additionalAds1 + additionalAds2 + additionalAds3;
            
            const totalAllCosts = totalFixedCosts + totalAdsCosts;
            const netProfit = sellingPrice - totalAllCosts;
            const profitMargin = (netProfit / sellingPrice) * 100;
            const totalCostsPercent = (totalAllCosts / sellingPrice) * 100;

            // KPIs
            const currentROAS = pureAdsAmount > 0 ? sellingPrice / pureAdsAmount : 0;
            const tiktokROI = currentROAS;
            const standardROI = pureAdsAmount > 0 ? netProfit / pureAdsAmount : 0;
            const costPerOrder = totalAdsCosts;

            // Breakeven calculations
            const availableForAds = sellingPrice - totalFixedCosts;
            const maxPureAds = (availableForAds - wht - additionalAds1 - additionalAds2 - additionalAds3) / (1 + sstRate / 100);
            const maxSST = maxPureAds * (sstRate / 100);
            const totalMaxAds = maxPureAds + maxSST + wht + additionalAds1 + additionalAds2 + additionalAds3;
            const breakevenROAS = maxPureAds > 0 ? sellingPrice / maxPureAds : 0;
            const maxPureAdsPercent = (maxPureAds / sellingPrice) * 100;

            // Update display function
            const updateElement = (id, value, suffix = '') => {
                const element = document.getElementById(id);
                if (element) {
                    const numValue = parseFloat(value) || 0;
                    element.textContent = numValue.toFixed(2) + suffix;
                }
            };

            // Update all displays
            updateElement('totalPayment', totalPayment);
            updateElement('cogsAmount', cogs);
            updateElement('fulfillmentAmount', fulfillment);
            updateElement('additionalProduct1Amount', additionalProduct1);
            updateElement('additionalProduct2Amount', additionalProduct2);
            updateElement('additionalProduct3Amount', additionalProduct3);
            updateElement('transactionAmount', transactionAmount);
            updateElement('marketplaceAmount', marketplaceAmount);
            updateElement('bxpAmount', bxpAmount);
            updateElement('affiliateAmount', affiliateAmount);
            updateElement('additionalPlatform1Amount', additionalPlatform1Amount);
            updateElement('additionalPlatform2Amount', additionalPlatform2Amount);
            updateElement('additionalPlatform3Amount', additionalPlatform3Amount);
            updateElement('totalFixedCosts', totalFixedCosts);
            updateElement('adsAmountDisplay', pureAdsAmount);
            updateElement('sstAmount', sstAmount);
            updateElement('whtAmount', wht);
            updateElement('additionalAds1Amount', additionalAds1);
            updateElement('additionalAds2Amount', additionalAds2);
            updateElement('additionalAds3Amount', additionalAds3);
            updateElement('totalAdsCosts', totalAdsCosts);
            updateElement('grossRevenue', sellingPrice);
            updateElement('totalAllCosts', totalAllCosts);
            updateElement('totalCostsPercent', totalCostsPercent, '%');
            updateElement('netProfit', netProfit);
            updateElement('profitMargin', profitMargin, '%');
            
            // KPIs
            updateElement('currentROAS', currentROAS);
            updateElement('tiktokROI', tiktokROI);
            updateElement('standardROI', standardROI);
            updateElement('costPerOrder', costPerOrder);
            
            // Breakeven
            updateElement('breakevenROAS', breakevenROAS);
            updateElement('tiktokBreakevenROI', breakevenROAS);
            updateElement('standardBreakevenROI', '0.00');
            updateElement('maxCPO', totalMaxAds);
            updateElement('availableForAds', availableForAds);
            updateElement('availablePercent', ((availableForAds / sellingPrice) * 100), '%');
            updateElement('maxPureAds', maxPureAds);
            updateElement('maxPureAdsPercent', maxPureAdsPercent, '%');
            updateElement('maxSST', maxSST);
            updateElement('totalMaxAds', totalMaxAds);
            updateElement('totalMaxAdsPercent', ((totalMaxAds / sellingPrice) * 100), '%');

            // Verification section
            updateElement('currentCOGS', cogs);
            updateElement('breakevenCOGS', cogs);
            updateElement('currentFulfillment', fulfillment);
            updateElement('breakevenFulfillment', fulfillment);
            updateElement('currentPlatformFees', platformFees);
            updateElement('breakevenPlatformFees', platformFees);
            updateElement('currentPureAds', pureAdsAmount);
            updateElement('breakevenPureAds', maxPureAds);
            updateElement('currentSST', sstAmount);
            updateElement('breakevenSST', maxSST);
            updateElement('currentWHT', wht);
            updateElement('breakevenWHT', wht);
            updateElement('verifyCurrentTotal', totalAllCosts);
            updateElement('verifyBreakevenTotal', (totalFixedCosts + totalMaxAds));
            updateElement('verifyCurrentProfit', netProfit);
            updateElement('verifyBreakevenProfit', (sellingPrice - totalFixedCosts - totalMaxAds));

            // Business insights
            const healthStatus = netProfit > 0 ? '✅ Healthy' : '❌ Unhealthy';
            const scalingRoom = (maxPureAdsPercent - adsRate).toFixed(1) + '% room';
            const platformPerf = 'Excellent ROI ' + tiktokROI.toFixed(2);
            const riskLevel = standardROI > 0.5 ? '🟢 Low Risk' : standardROI > 0 ? '🟡 Medium Risk' : '🔴 High Risk';
            
            // Update insights with safe checks
            const healthElement = document.getElementById('healthStatus');
            const scalingElement = document.getElementById('scalingRoom');
            const platformElement = document.getElementById('platformPerf');
            const riskElement = document.getElementById('riskLevel');
            
            if (healthElement) healthElement.textContent = healthStatus;
            if (scalingElement) scalingElement.textContent = scalingRoom;
            if (platformElement) platformElement.textContent = platformPerf;
            if (riskElement) riskElement.textContent = riskLevel;

            // Update quick reference
            const quickRefElement = document.getElementById('quickRef');
            if (quickRefElement) {
                quickRefElement.textContent = `${adsRate.toFixed(1)}% = RM${pureAdsAmount.toFixed(2)} pure ads cost`;
            }

            // Update TikTok vs Business Perspective table
            const tiktokCurrentElement = document.getElementById('tiktokCurrentPerf');
            const businessCurrentElement = document.getElementById('businessCurrentPerf');
            const tiktokBreakevenElement = document.getElementById('tiktokBreakevenTarget');
            const businessBreakevenElement = document.getElementById('businessBreakevenTarget');
            const tiktokScalingElement = document.getElementById('tiktokScalingHeadroom');
            const businessScalingElement = document.getElementById('businessScalingHeadroom');
            
            if (tiktokCurrentElement) {
                const tiktokStatus = currentROAS >= 3 ? 'Excellent' : currentROAS >= 2 ? 'Good' : currentROAS >= 1 ? 'Fair' : 'Poor';
                tiktokCurrentElement.textContent = `${currentROAS.toFixed(2)} (${tiktokStatus})`;
            }
            
            if (businessCurrentElement) {
                const businessStatus = standardROI >= 1 ? 'Profitable' : standardROI >= 0 ? 'Breakeven' : 'Loss';
                businessCurrentElement.textContent = `${standardROI.toFixed(2)} (${businessStatus})`;
                businessCurrentElement.className = standardROI >= 0 ? 'formula-cell profit-positive' : 'formula-cell profit-negative';
            }
            
            if (tiktokBreakevenElement) {
                tiktokBreakevenElement.textContent = breakevenROAS.toFixed(2);
            }
            
            if (businessBreakevenElement) {
                businessBreakevenElement.textContent = '0.00';
            }
            
            if (tiktokScalingElement) {
                tiktokScalingElement.textContent = `ROAS can drop to ${breakevenROAS.toFixed(2)}`;
            }
            
            if (businessScalingElement) {
                businessScalingElement.textContent = `Can scale to ${maxPureAdsPercent.toFixed(1)}% ads`;
            }

            // Color profit based on positive/negative
            const profitElement = document.getElementById('netProfit');
            if (profitElement) {
                profitElement.className = netProfit > 0 ? 'formula-cell profit-positive' : 'formula-cell profit-negative';
            }

            // Update scenario table
            updateScenarioTable(sellingPrice, totalFixedCosts, sstRate, wht, additionalAds1, additionalAds2, additionalAds3);
        }

        function updateScenarioTable(sellingPrice, totalFixedCosts, sstRate, wht, additionalAds1, additionalAds2, additionalAds3) {
            const scenarioTable = document.getElementById('scenarioTable');
            if (!scenarioTable) return;
            
            scenarioTable.innerHTML = '';

            const scenarios = [10, 15, 20, 25, 30, 35, 40, 45, 50, 55];
            
            // Add actual breakeven percentage
            const availableForAds = sellingPrice - totalFixedCosts;
            const maxPureAds = (availableForAds - wht - additionalAds1 - additionalAds2 - additionalAds3) / (1 + sstRate / 100);
            const breakevenPercent = (maxPureAds / sellingPrice) * 100;
            
            // Add breakeven to scenarios if not already there
            if (!scenarios.includes(Math.round(breakevenPercent))) {
                scenarios.push(parseFloat(breakevenPercent.toFixed(1)));
                scenarios.sort((a, b) => a - b);
            }

            scenarios.forEach(adsPercent => {
                const pureAdsAmount = sellingPrice * (parseFloat(adsPercent) / 100);
                const sstAmount = pureAdsAmount * (sstRate / 100);
                const totalAdsAmount = pureAdsAmount + sstAmount + wht + additionalAds1 + additionalAds2 + additionalAds3;
                const totalCosts = totalFixedCosts + totalAdsAmount;
                const netProfit = sellingPrice - totalCosts;
                const roas = pureAdsAmount > 0 ? sellingPrice / pureAdsAmount : 0;
                const tiktokROI = roas;
                const standardROI = pureAdsAmount > 0 ? netProfit / pureAdsAmount : 0;
                
                let status = '';
                let statusClass = '';
                
                if (netProfit > 0.05) {
                    status = '✅ Profitable';
                    statusClass = 'profit-positive';
                } else if (Math.abs(netProfit) <= 0.05) {
                    status = '⚖️ Breakeven';
                    statusClass = '';
                } else {
                    status = '❌ Loss';
                    statusClass = 'profit-negative';
                }

                // Special highlighting for breakeven
                if (Math.abs(parseFloat(adsPercent) - breakevenPercent) < 0.5) {
                    status = '⚖️ TRUE BREAKEVEN';
                    statusClass = 'highlight';
                }

                const row = `
                    <tr class="breakdown ${statusClass === 'highlight' ? 'highlight' : ''}">
                        <td>${parseFloat(adsPercent).toFixed(1)}%</td>
                        <td>RM ${pureAdsAmount.toFixed(2)}</td>
                        <td>RM ${totalAdsAmount.toFixed(2)}</td>
                        <td>RM ${totalCosts.toFixed(2)}</td>
                        <td>${roas.toFixed(2)}</td>
                        <td>${tiktokROI.toFixed(2)}</td>
                        <td class="${statusClass}">${standardROI.toFixed(2)}</td>
                        <td class="${statusClass}">RM ${netProfit.toFixed(2)}</td>
                        <td class="${statusClass}"><strong>${status}</strong></td>
                    </tr>
                `;
                scenarioTable.innerHTML += row;
            });
        }

        // P&L Tracker JavaScript
        function calculateMetrics() {
            // Get input values
            const ordersValue = parseFloat(document.getElementById('ordersValue').value) || 0;
            const affiliateFees = parseFloat(document.getElementById('affiliateFees').value) || 0;
            const settlement = parseFloat(document.getElementById('settlement').value) || 0;
            const unitsSold = parseInt(document.getElementById('unitsSold').value) || 0;
            const cogsPnl = parseFloat(document.getElementById('cogsPnl').value) || 0;
            const adsSpend = parseFloat(document.getElementById('adsSpend').value) || 0;
            const platformFeePnl = parseFloat(document.getElementById('platformFeePnl').value) || 0;
            const fulfillmentPerUnit = parseFloat(document.getElementById('fulfillmentPerUnit').value) || 0;
            const dst = parseFloat(document.getElementById('dst').value) || 0;
            const overhead = parseFloat(document.getElementById('overhead').value) || 0;

            // Calculate metrics
            const grossRevenue = ordersValue - affiliateFees;
            const revenuePerUnit = unitsSold > 0 ? grossRevenue / unitsSold : 0;
            const cogsPerUnit = unitsSold > 0 ? cogsPnl / unitsSold : 0;
            const adsPerUnit = unitsSold > 0 ? adsSpend / unitsSold : 0;
            const platformPerUnit = unitsSold > 0 ? platformFeePnl / unitsSold : 0;
            const dstPerUnit = unitsSold > 0 ? dst / unitsSold : 0;
            const overheadPerUnit = unitsSold > 0 ? overhead / unitsSold : 0;
            
            const totalCostPerUnit = cogsPerUnit + adsPerUnit + platformPerUnit + fulfillmentPerUnit + dstPerUnit + overheadPerUnit;
            const profitPerUnit = revenuePerUnit - totalCostPerUnit;
            const totalProfit = profitPerUnit * unitsSold;
            const profitMargin = grossRevenue > 0 ? (totalProfit / grossRevenue) * 100 : 0;
            
            const affiliatePercentage = ordersValue > 0 ? (affiliateFees / ordersValue) * 100 : 0;
            const pendingCollections = grossRevenue - settlement;
            
            // Calculate breakeven analysis
            const variableCostPerUnit = cogsPerUnit + fulfillmentPerUnit;
            const fixedCosts = adsSpend + platformFeePnl + dst + overhead;
            const contributionMarginPerUnit = revenuePerUnit - variableCostPerUnit;
            
            const breakevenUnits = contributionMarginPerUnit > 0 ? fixedCosts / contributionMarginPerUnit : 0;
            const breakevenRevenue = breakevenUnits * revenuePerUnit;
            const unitsVsBreakeven = unitsSold - breakevenUnits;
            const safetyMargin = unitsSold > 0 ? ((unitsVsBreakeven / unitsSold) * 100) : 0;

            // Calculate ROI
            const totalInvestment = adsSpend + cogsPnl; // Investment in ads + inventory
            const roi = totalInvestment > 0 ? ((totalProfit / totalInvestment) * 100) : 0;

            // Calculate cash metrics
            const totalCosts = cogsPnl + adsSpend + platformFeePnl + (fulfillmentPerUnit * unitsSold) + dst + overhead;
            const cashProfit = settlement - totalCosts;
            const cashMargin = settlement > 0 ? (cashProfit / settlement) * 100 : 0;

            // Update display
            document.getElementById('grossRevenuePnl').textContent = `RM ${grossRevenue.toFixed(2)}`;
            document.getElementById('revenuePerUnit').textContent = `RM ${revenuePerUnit.toFixed(2)}`;
            document.getElementById('costPerUnitPnl').textContent = `RM ${totalCostPerUnit.toFixed(2)}`;
            document.getElementById('affiliatePercentage').textContent = `${affiliatePercentage.toFixed(1)}%`;
            
            document.getElementById('profitPerUnitPnl').textContent = `RM ${profitPerUnit.toFixed(2)}`;
            document.getElementById('totalProfitPnl').textContent = `RM ${totalProfit.toFixed(2)}`;
            document.getElementById('profitMarginPnl').textContent = `${profitMargin.toFixed(1)}%`;
            
            document.getElementById('settlementReceived').textContent = `RM ${settlement.toFixed(2)}`;
            document.getElementById('pendingCollections').textContent = `RM ${pendingCollections.toFixed(2)}`;
            document.getElementById('cashProfit').textContent = `RM ${cashProfit.toFixed(2)}`;
            document.getElementById('cashMargin').textContent = `${cashMargin.toFixed(1)}%`;

            // Update breakeven analysis
            document.getElementById('breakevenUnits').textContent = breakevenUnits.toFixed(0);
            document.getElementById('breakevenRevenuePnl').textContent = `RM ${breakevenRevenue.toFixed(2)}`;
            document.getElementById('unitsVsBreakeven').textContent = unitsVsBreakeven >= 0 ? `+${unitsVsBreakeven.toFixed(0)}` : unitsVsBreakeven.toFixed(0);
            document.getElementById('safetyMargin').textContent = `${safetyMargin.toFixed(1)}%`;

            // Color coding for profit/loss and breakeven
            const profitElements = ['profitPerUnitPnl', 'totalProfitPnl', 'profitMarginPnl'];
            const cashElements = ['cashProfit', 'cashMargin'];
            const breakevenElements = ['unitsVsBreakeven', 'safetyMargin'];
            
            profitElements.forEach(id => {
                const element = document.getElementById(id);
                if (totalProfit < 0) {
                    element.classList.add('negative');
                } else {
                    element.classList.remove('negative');
                }
            });

            cashElements.forEach(id => {
                const element = document.getElementById(id);
                if (cashProfit < 0) {
                    element.classList.add('negative');
                } else {
                    element.classList.remove('negative');
                }
            });

            // Color coding for breakeven analysis
            breakevenElements.forEach(id => {
                const element = document.getElementById(id);
                if (unitsVsBreakeven < 0) {
                    element.classList.add('negative');
                } else {
                    element.classList.remove('negative');
                }
            });

            // Update profit result section styling
            const profitResult = document.getElementById('profitResult');
            if (totalProfit < 0) {
                profitResult.className = 'loss-highlight';
            } else {
                profitResult.className = 'profit-highlight';
            }

            // Update summary
            const month = document.getElementById('month').value;
            let summaryText = `<strong>Bulan ${month}:</strong><br>`;
            
            if (totalProfit > 0) {
                summaryText += `✅ UNTUNG: RM ${totalProfit.toFixed(2)} (${profitMargin.toFixed(1)}%)<br>`;
                summaryText += `💰 Cash in hand: RM ${cashProfit.toFixed(2)}<br>`;
                summaryText += `📊 ROI: ${roi.toFixed(1)}% return on investment<br>`;
                summaryText += `⏳ Pending: RM ${pendingCollections.toFixed(2)}<br>`;
                summaryText += `🛡️ Safety Margin: ${safetyMargin.toFixed(1)}% above breakeven<br>`;
                summaryText += `🎯 Breakeven: ${breakevenUnits.toFixed(0)} units (sold ${unitsSold})<br>`;
                summaryText += `💡 Overhead: RM ${overhead.toFixed(2)} (RM ${overheadPerUnit.toFixed(2)}/unit)`;
            } else {
                summaryText += `❌ RUGI: RM ${Math.abs(totalProfit).toFixed(2)}<br>`;
                summaryText += `💸 Kena improve marketing atau kurang costs!<br>`;
                summaryText += `📊 ROI: ${roi.toFixed(1)}% (negative return)<br>`;
                summaryText += `🎯 Need ${breakevenUnits.toFixed(0)} units to breakeven (sold ${unitsSold})<br>`;
                summaryText += `💡 Overhead burden: RM ${overheadPerUnit.toFixed(2)}/unit`;
            }
            
            document.getElementById('summaryText').innerHTML = summaryText;
        }

        function calculateOverheadTotal() {
            const rent = parseFloat(document.getElementById('overheadRent').value) || 0;
            const utilities = parseFloat(document.getElementById('overheadUtilities').value) || 0;
            const staff = parseFloat(document.getElementById('overheadStaff').value) || 0;
            const comms = parseFloat(document.getElementById('overheadComms').value) || 0;
            const banking = parseFloat(document.getElementById('overheadBanking').value) || 0;
            const others = parseFloat(document.getElementById('overheadOthers').value) || 0;
            
            const total = rent + utilities + staff + comms + banking + others;
            document.getElementById('overhead').value = total.toFixed(2);
            
            // Trigger recalculation
            calculateMetrics();
        }

        // Initialize page
        document.addEventListener('DOMContentLoaded', function() {
            // Add event listeners to all ROI Calculator number inputs
            const roiTab = document.getElementById('roi-tab');
            if (roiTab) {
                roiTab.querySelectorAll('input[type="number"]').forEach(input => {
                    input.addEventListener('input', updateCalculations);
                });
            }

            // Add event listeners to all P&L Tracker inputs
            const pnlTab = document.getElementById('pnl-tab');
            if (pnlTab) {
                pnlTab.querySelectorAll('input').forEach(input => {
                    input.addEventListener('input', calculateMetrics);
                });
            }

            // Add event listener for ROI toggle
            const adsToggle = document.getElementById('adsInputToggle');
            if (adsToggle) {
                adsToggle.addEventListener('change', function() {
                    toggleAdsInput();
                    updateCalculations();
                });
            }

            // Initial setup
            toggleAdsInput();
            updateCalculations();
        });
    </script>
</body>
</html>
