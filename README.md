<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ZUL ROAS ROI CALCULATOR</title>
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
            text-align: center;
        }
        
        .container {
            background: white;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            margin-bottom: 15px;
            width: 100%;
            max-width: 1200px;
            margin-left: auto;
            margin-right: auto;
        }
        
        .header {
            text-align: center;
            color: #2c3e50;
            margin-bottom: 20px;
        }
        
        .header h1 {
            font-size: 1.5em;
            margin: 10px 0;
        }
        
        .header p {
            font-size: 0.9em;
            margin: 5px 0;
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 15px;
            font-size: 0.85em;
        }
        
        th, td {
            border: 1px solid #ddd;
            padding: 6px;
            text-align: center;
        }
        
        th {
            background-color: #3498db;
            color: white;
            font-weight: bold;
            font-size: 0.8em;
        }
        
        .input-cell {
            background-color: #ecf0f1;
        }
        
        .formula-cell {
            background-color: #e8f5e8;
        }
        
        .highlight {
            background-color: #fff3cd;
            font-weight: bold;
        }
        
        .breakdown {
            background-color: #f8f9fa;
        }
        
        input {
            width: 70px;
            padding: 4px;
            border: 1px solid #ccc;
            border-radius: 4px;
            text-align: center;
            font-size: 0.9em;
        }
        
        input[type="text"] {
            width: 100px;
        }
        
        .profit-positive {
            color: #27ae60;
            font-weight: bold;
        }
        
        .profit-negative {
            color: #e74c3c;
            font-weight: bold;
        }
        
        .section-title {
            background-color: #2c3e50;
            color: white;
            text-align: center;
            font-weight: bold;
            font-size: 0.9em;
        }
        
        .verification {
            background-color: #e3f2fd;
            border-left: 4px solid #2196f3;
        }
        
        .warning {
            background-color: #fff3e0;
            border-left: 4px solid #ff9800;
        }
        
        .toggle-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 8px;
            margin: 8px 0;
            text-align: center;
        }
        
        .toggle-switch {
            position: relative;
            display: inline-block;
            width: 50px;
            height: 28px;
        }
        
        .toggle-switch input {
            opacity: 0;
            width: 0;
            height: 0;
        }
        
        .slider {
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
        
        .slider:before {
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
        
        input:checked + .slider {
            background-color: #2196F3;
        }
        
        input:checked + .slider:before {
            transform: translateX(22px);
        }
        
        .input-mode-label {
            font-weight: bold;
            color: #2c3e50;
            font-size: 0.85em;
            text-align: center;
        }
        
        .ads-input-section {
            background-color: #f0f8ff;
            border: 2px solid #2196F3;
            border-radius: 8px;
            padding: 8px;
            text-align: center;
        }
        
        .reference-links {
            font-size: 10px;
            color: #666;
            margin-top: 3px;
            line-height: 1.2;
            text-align: center;
        }
        
        .reference-links a {
            color: #2196F3;
            text-decoration: none;
            margin: 0 5px;
            display: inline-block;
            padding: 2px 4px;
            border-radius: 3px;
            background: rgba(33, 150, 243, 0.1);
        }
        
        .reference-links a:hover {
            background: rgba(33, 150, 243, 0.2);
            text-decoration: underline;
        }
        
        .fee-note {
            background-color: #f8f9fa;
            border-left: 3px solid #2196F3;
            padding: 6px;
            margin: 4px 0;
            font-size: 10px;
            text-align: center;
        }
        
        .editable-text {
            cursor: text;
            padding: 6px;
            border: 1px dashed #ccc;
            background-color: #f9f9f9;
            text-align: center;
        }
        
        .editable-text:hover {
            background-color: #e6f3ff;
            border-color: #2196F3;
        }
        
        .editable-text:focus {
            outline: 2px solid #2196F3;
            background-color: #f0f8ff;
        }
        
        /* Mobile Responsive */
        @media (max-width: 768px) {
            body {
                padding: 5px;
            }
            
            .container {
                padding: 10px;
                margin-bottom: 10px;
            }
            
            .header h1 {
                font-size: 1.3em;
            }
            
            .header p {
                font-size: 0.8em;
            }
            
            table {
                font-size: 0.75em;
            }
            
            th, td {
                padding: 4px;
            }
            
            th {
                font-size: 0.7em;
            }
            
            input {
                width: 60px;
                font-size: 0.8em;
                padding: 3px;
            }
            
            input[type="text"] {
                width: 80px;
            }
            
            .toggle-switch {
                width: 40px;
                height: 24px;
            }
            
            .slider:before {
                height: 16px;
                width: 16px;
            }
            
            input:checked + .slider:before {
                transform: translateX(16px);
            }
            
            .reference-links {
                font-size: 9px;
            }
            
            .fee-note {
                font-size: 9px;
                padding: 4px;
            }
        }
        
        /* Extra Small Mobile */
        @media (max-width: 480px) {
            .header h1 {
                font-size: 1.1em;
            }
            
            table {
                font-size: 0.7em;
            }
            
            th, td {
                padding: 3px;
            }
            
            input {
                width: 50px;
                font-size: 0.75em;
            }
            
            input[type="text"] {
                width: 70px;
            }
            
            .toggle-container {
                gap: 5px;
            }
            
            .input-mode-label {
                font-size: 0.75em;
            }
        }
        
        /* Large tablets and up - keep centered */
        @media (min-width: 769px) {
            body {
                padding: 20px;
            }
            
            .container {
                max-width: 1200px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
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
                <td class="input-cell"><input type="text" id="productName" value="Perfume Pheromone" style="width: 150px;"></td>
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

    <script>
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

        // Add event listeners to all inputs
        document.addEventListener('DOMContentLoaded', function() {
            // Add event listeners to all number inputs
            document.querySelectorAll('input[type="number"]').forEach(input => {
                input.addEventListener('input', updateCalculations);
            });

            // Add event listener for toggle
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
