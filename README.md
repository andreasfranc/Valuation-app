<!DOCTYPE html>
<html lang="no">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aprila Bank - Selskapsverdivurdering</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Helvetica Neue', 'Segoe UI', Arial, sans-serif;
            background: linear-gradient(135deg, #6E4B37 0%, #CF6833 50%, #C8A578 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: #FDFDFC;
            border-radius: 16px;
            padding: 0;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.15);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #000000, #6E4B37);
            color: #FDFDFC;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><defs><pattern id="grid" width="10" height="10" patternUnits="userSpaceOnUse"><path d="M 10 0 L 0 0 0 10" fill="none" stroke="rgba(253,253,252,0.1)" stroke-width="0.5"/></pattern></defs><rect width="100" height="100" fill="url(%23grid)" /></svg>') repeat;
            opacity: 0.3;
        }

        .logo-section {
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 20px;
            position: relative;
            z-index: 1;
        }

        .header h1 {
            font-size: 2.2em;
            font-weight: 600;
            position: relative;
            z-index: 1;
            color: #FDFDFC;
        }

        .header p {
            opacity: 0.9;
            font-size: 1.1em;
            margin-top: 10px;
            position: relative;
            z-index: 1;
            color: #E6E3DB;
        }

        .content {
            padding: 40px;
        }

        .search-section {
            background: #E6E3DB;
            padding: 30px;
            border-radius: 12px;
            margin-bottom: 30px;
            border: 1px solid #C8A578;
        }

        .search-section h2 {
            color: #6E4B37;
            margin-bottom: 20px;
            font-size: 1.5em;
            font-weight: 600;
        }

        .search-form {
            display: flex;
            gap: 15px;
            margin-bottom: 20px;
        }

        input[type="text"], input[type="number"] {
            flex: 1;
            padding: 16px 20px;
            border: 2px solid #C8A578;
            border-radius: 8px;
            font-size: 16px;
            transition: all 0.3s ease;
            background: #FDFDFC;
            color: #000000;
        }

        input[type="text"]:focus, input[type="number"]:focus {
            outline: none;
            border-color: #CF6833;
            box-shadow: 0 0 0 3px rgba(207, 104, 51, 0.1);
        }

        .btn-primary {
            background: #000000;
            color: #FDFDFC;
            border: none;
            padding: 16px 32px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            transition: all 0.3s ease;
            text-transform: none;
            letter-spacing: 0.3px;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
            background: #333333;
        }

        .btn-primary:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }

        .results-section {
            display: none;
        }

        .company-info {
            background: #FDFDFC;
            padding: 30px;
            border-radius: 12px;
            margin-bottom: 30px;
            border: 1px solid #E6E3DB;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
        }

        .company-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            flex-wrap: wrap;
            gap: 15px;
            padding-bottom: 20px;
            border-bottom: 2px solid #E6E3DB;
        }

        .company-name {
            font-size: 1.8em;
            color: #CF6833;
            font-weight: 600;
        }

        .org-number {
            color: #6E4B37;
            font-size: 1.1em;
            font-weight: 500;
        }

        .financial-data {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            margin-bottom: 20px;
        }

        .financial-item {
            background: #E6E3DB;
            padding: 20px;
            border-radius: 8px;
            border-left: 4px solid #CF6833;
            transition: all 0.3s ease;
            position: relative;
        }

        .financial-item:hover {
            background: #E0DDD4;
            transform: translateY(-2px);
            border-left-color: #C8A578;
        }

        .financial-item label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #6E4B37;
            font-size: 14px;
            position: relative;
        }

        .tooltip-icon {
            display: inline-block;
            margin-left: 5px;
            width: 16px;
            height: 16px;
            background: #C8A578;
            color: #FDFDFC;
            border-radius: 50%;
            text-align: center;
            line-height: 16px;
            font-size: 12px;
            font-weight: bold;
            cursor: help;
            position: relative;
        }

        .tooltip {
            visibility: hidden;
            width: 250px;
            background-color: #000000;
            color: #FDFDFC;
            text-align: left;
            border-radius: 6px;
            padding: 10px;
            position: absolute;
            z-index: 1000;
            bottom: 125%;
            left: 50%;
            margin-left: -125px;
            opacity: 0;
            transition: opacity 0.3s;
            font-size: 12px;
            line-height: 1.4;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }

        .tooltip::after {
            content: "";
            position: absolute;
            top: 100%;
            left: 50%;
            margin-left: -5px;
            border-width: 5px;
            border-style: solid;
            border-color: #000000 transparent transparent transparent;
        }

        .tooltip-icon:hover .tooltip {
            visibility: visible;
            opacity: 1;
        }

        .financial-item input {
            width: 100%;
            padding: 12px 16px;
            border: 1px solid #C8A578;
            border-radius: 6px;
            font-size: 16px;
            transition: border-color 0.3s ease;
            background: #FDFDFC;
            color: #000000;
        }

        .financial-item input:focus {
            outline: none;
            border-color: #CF6833;
        }

        .assumptions-section {
            background: #F5F2ED;
            padding: 25px;
            border-radius: 8px;
            margin: 20px 0;
            border-left: 4px solid #C8A578;
        }

        .assumptions-section h4 {
            color: #6E4B37;
            margin-bottom: 15px;
            font-size: 1.1em;
        }

        .assumptions-explanation {
            background: #FDFDFC;
            padding: 20px;
            border-radius: 8px;
            margin-top: 20px;
            border: 1px solid #C8A578;
            display: none;
        }

        .assumptions-toggle {
            background: #E6E3DB;
            padding: 15px 20px;
            border-radius: 8px;
            margin-top: 15px;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 1px solid #C8A578;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .assumptions-toggle:hover {
            background: #E0DDD4;
            border-color: #CF6833;
        }

        .assumptions-toggle-title {
            color: #6E4B37;
            font-weight: 600;
            font-size: 14px;
        }

        .assumptions-toggle-icon {
            color: #CF6833;
            font-size: 18px;
            transition: transform 0.3s ease;
        }

        .assumptions-toggle.active .assumptions-toggle-icon {
            transform: rotate(180deg);
        }

        .assumptions-explanation.show {
            display: block;
            animation: slideDown 0.3s ease-out;
        }

        @keyframes slideDown {
            from {
                opacity: 0;
                max-height: 0;
                padding-top: 0;
                padding-bottom: 0;
            }
            to {
                opacity: 1;
                max-height: 500px;
                padding-top: 20px;
                padding-bottom: 20px;
            }
        }

        .assumptions-explanation h5 {
            color: #CF6833;
            font-size: 1.1em;
            margin-bottom: 15px;
            font-weight: 600;
        }

        .assumptions-explanation p {
            color: #6E4B37;
            line-height: 1.6;
            margin-bottom: 15px;
            font-size: 14px;
        }

        .assumptions-explanation ul {
            color: #6E4B37;
            line-height: 1.6;
            margin-left: 20px;
            margin-bottom: 15px;
            font-size: 14px;
        }

        .assumptions-explanation li {
            margin-bottom: 10px;
        }

        .assumptions-explanation strong {
            color: #CF6833;
            font-weight: 600;
        }

        .assumptions-explanation em {
            font-style: italic;
            opacity: 0.9;
        }

        .assumptions-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
        }

        .valuation-section {
            background: #FDFDFC;
            padding: 40px;
            border-radius: 12px;
            border: 1px solid #E6E3DB;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
        }

        .valuation-section h3 {
            color: #CF6833;
            font-size: 1.8em;
            margin-bottom: 30px;
            font-weight: 600;
            text-align: center;
        }

        .valuation-methods {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
            margin-bottom: 30px;
        }

        .method-card {
            background: #E6E3DB;
            padding: 25px;
            border-radius: 12px;
            border: 1px solid #C8A578;
            transition: all 0.3s ease;
            position: relative;
        }

        .method-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(207, 104, 51, 0.1);
            background: #E0DDD4;
        }

        .method-title {
            font-size: 1.3em;
            font-weight: 600;
            color: #6E4B37;
            margin-bottom: 15px;
            position: relative;
        }

        .method-value {
            font-size: 2em;
            font-weight: bold;
            color: #CF6833;
            margin-bottom: 10px;
        }

        .method-description {
            color: #6E4B37;
            font-size: 0.9em;
            line-height: 1.4;
            opacity: 0.8;
        }

        .final-valuation {
            background: linear-gradient(135deg, #CF6833, #6E4B37);
            color: #FDFDFC;
            padding: 30px;
            border-radius: 12px;
            text-align: center;
            margin-top: 30px;
            box-shadow: 0 8px 25px rgba(207, 104, 51, 0.2);
        }

        .recommendations-section {
            background: #F8F6F0;
            padding: 30px;
            border-radius: 12px;
            margin-top: 30px;
            border: 1px solid #E6E3DB;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
        }

        .recommendations-section h3 {
            color: #CF6833;
            font-size: 1.8em;
            margin-bottom: 25px;
            font-weight: 600;
            text-align: center;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .recommendation-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 20px;
            margin-bottom: 25px;
        }

        .recommendation-card {
            background: #FDFDFC;
            padding: 25px;
            border-radius: 12px;
            border-left: 4px solid #CF6833;
            transition: all 0.3s ease;
            position: relative;
        }

        .recommendation-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(207, 104, 51, 0.1);
            border-left-color: #C8A578;
        }

        .recommendation-title {
            font-size: 1.2em;
            font-weight: 600;
            color: #6E4B37;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .recommendation-content {
            color: #6E4B37;
            line-height: 1.6;
            font-size: 14px;
        }

        .impact-metric {
            background: #E6E3DB;
            padding: 15px;
            border-radius: 8px;
            margin-top: 15px;
            text-align: center;
        }

        .impact-value {
            font-size: 1.4em;
            font-weight: bold;
            color: #CF6833;
            margin-bottom: 5px;
        }

        .impact-description {
            font-size: 12px;
            color: #6E4B37;
            opacity: 0.8;
        }

        .financing-cta {
            background: linear-gradient(135deg, #000000, #6E4B37);
            color: #FDFDFC;
            padding: 25px;
            border-radius: 12px;
            text-align: center;
            margin-top: 20px;
            position: relative;
            overflow: hidden;
        }

        .financing-cta::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><defs><pattern id="dots" width="20" height="20" patternUnits="userSpaceOnUse"><circle cx="10" cy="10" r="1.5" fill="rgba(253,253,252,0.1)"/></pattern></defs><rect width="100" height="100" fill="url(%23dots)" /></svg>') repeat;
            opacity: 0.3;
        }

        .financing-cta h4 {
            font-size: 1.3em;
            margin-bottom: 15px;
            position: relative;
            z-index: 1;
        }

        .financing-cta p {
            opacity: 0.9;
            margin-bottom: 20px;
            position: relative;
            z-index: 1;
        }

        .cta-button {
            background: #CF6833;
            color: #FDFDFC;
            border: none;
            padding: 12px 24px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            transition: all 0.3s ease;
            position: relative;
            z-index: 1;
        }

        .cta-button:hover {
            background: #C8A578;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(207, 104, 51, 0.3);
        }

        .final-value {
            font-size: 2.5em;
            font-weight: bold;
            margin-bottom: 10px;
            color: #FDFDFC;
        }

        .final-range {
            font-size: 1.2em;
            opacity: 0.9;
            color: #E6E3DB;
        }

        .loading {
            display: none;
            text-align: center;
            padding: 50px;
            background: #FDFDFC;
            border-radius: 12px;
            border: 1px solid #E6E3DB;
        }

        .spinner {
            border: 4px solid #E6E3DB;
            border-top: 4px solid #CF6833;
            border-radius: 50%;
            width: 50px;
            height: 50px;
            animation: spin 1s linear infinite;
            margin: 0 auto 20px;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .error {
            background: #F8E8E3;
            color: #8B0000;
            padding: 20px;
            border-radius: 8px;
            margin: 20px 0;
            border: 1px solid #E8C8C3;
            border-left: 4px solid #CF6833;
        }

        .warning {
            background: #FDF8F0;
            color: #6E4B37;
            padding: 20px;
            border-radius: 8px;  
            margin: 20px 0;
            border: 1px solid #F0E6D6;
            border-left: 4px solid #C8A578;
        }

        .powered-by {
            text-align: center;
            padding: 20px;
            color: #6E4B37;
            font-size: 14px;
            background: #E6E3DB;
            border-top: 1px solid #C8A578;
        }

        /* Accent elements with Aprila colors */
        .accent-rust {
            color: #CF6833;
        }

        .accent-gold {
            color: #C8A578;
        }

        .accent-earth {
            color: #6E4B37;
        }

        /* Section dividers */
        .section-divider {
            height: 2px;
            background: linear-gradient(90deg, #CF6833, #C8A578, #6E4B37);
            margin: 30px 0;
            border-radius: 1px;
        }

        @media (max-width: 768px) {
            .search-form {
                flex-direction: column;
            }
            
            .company-header {
                flex-direction: column;
                text-align: center;
            }
            
            .financial-data, .valuation-methods {
                grid-template-columns: 1fr;
            }

            .logo-section {
                flex-direction: column;
                gap: 15px;
            }

            .aprila-logo {
                margin-right: 0;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <div class="logo-section">
                <div>
                    <h1>Nysgjerrig på hva selskapet ditt er verdt?</h1>
                    <p>Vi gjør en vurdering basert på klassiske verdsettelsesmetoder</p>
                </div>
            </div>
        </div>
        
        <div class="content">
            <div class="search-section">
                <h2>🎯 Søk etter selskap</h2>
                <div class="search-form">
                    <input type="text" id="searchInput" placeholder="Skriv inn organisasjonsnummer eller selskapsnavn..." required>
                    <button type="button" class="btn-primary" id="searchBtn">Finn ditt selskap</button>
                </div>
                <div class="warning">
                    <strong>Merk:</strong> Dette er en demo-versjon. I produksjon ville dette være integrert med Enin og finansielle datakilder for nøyaktig verdivurdering.
                </div>
            </div>

            <div class="loading" id="loading">
                <div class="spinner"></div>
                <p>Henter selskapsdata og markedsdata...</p>
            </div>

            <div class="results-section" id="resultsSection">
                <div class="company-info">
                    <div class="company-header">
                        <div>
                            <div class="company-name" id="companyName">-</div>
                            <div class="org-number" id="orgNumber">-</div>
                        </div>
                    </div>
                    
                    <h3 class="accent-rust" style="margin-bottom: 25px;">💼 Finansielle nøkkeltall for verdivurdering</h3>
                    <div class="financial-data">
                        <div class="financial-item">
                            <label for="revenue">
                                Omsetning (NOK)
                                <span class="tooltip-icon">?
                                    <span class="tooltip">Selskapets totale inntekter fra salg av varer og tjenester i løpet av regnskapsåret.</span>
                                </span>
                            </label>
                            <input type="number" id="revenue" placeholder="0" min="0">
                        </div>
                        <div class="financial-item">
                            <label for="ebitda">
                                EBITDA (NOK)
                                <span class="tooltip-icon">?
                                    <span class="tooltip">Earnings Before Interest, Taxes, Depreciation and Amortization. Viser driftsresultat før renter, skatt og avskrivninger.</span>
                                </span>
                            </label>
                            <input type="number" id="ebitda" placeholder="0">
                        </div>
                        <div class="financial-item">
                            <label for="netIncome">
                                Årsresultat (NOK)
                                <span class="tooltip-icon">?
                                    <span class="tooltip">Selskapets endelige resultat etter alle kostnader, renter og skatt. Dette er "bunnlinjen" i resultatregnskapet.</span>
                                </span>
                            </label>
                            <input type="number" id="netIncome" placeholder="0">
                        </div>
                        <div class="financial-item">
                            <label for="totalAssets">
                                Sum eiendeler (NOK)
                                <span class="tooltip-icon">?
                                    <span class="tooltip">Totalverdien av alle selskapets eiendeler inkludert anleggsmidler, omløpsmidler og immaterielle eiendeler.</span>
                                </span>
                            </label>
                            <input type="number" id="totalAssets" placeholder="0" min="0">
                        </div>
                        <div class="financial-item">
                            <label for="equity">
                                Egenkapital (NOK)
                                <span class="tooltip-icon">?
                                    <span class="tooltip">Eierens andel av selskapet. Beregnes som eiendeler minus gjeld. Viser selskapets nettoformue.</span>
                                </span>
                            </label>
                            <input type="number" id="equity" placeholder="0">
                        </div>
                        <div class="financial-item">
                            <label for="debt">
                                Totalgjeld (NOK)
                                <span class="tooltip-icon">?
                                    <span class="tooltip">Summen av all gjeld selskapet har, både kortsiktig og langsiktig gjeld til kreditorer og långivere.</span>
                                </span>
                            </label>
                            <input type="number" id="debt" placeholder="0" min="0">
                        </div>
                        <div class="financial-item">
                            <label for="fcf">
                                Fri kontantstrøm (NOK)
                                <span class="tooltip-icon">?
                                    <span class="tooltip">Kontanter generert fra drift minus nødvendige investeringer. Viser hvor mye kontanter som er tilgjengelig for utbytte og vekst.</span>
                                </span>
                            </label>
                            <input type="number" id="fcf" placeholder="0">
                        </div>
                        <div class="financial-item">
                            <label for="growthRate">
                                Forventet vekstrate (%)
                                <span class="tooltip-icon">?
                                    <span class="tooltip">Estimert årlig vekst i inntekter og kontantstrøm. Baseres på historisk utvikling og markedsutsikter.</span>
                                </span>
                            </label>
                            <input type="number" id="growthRate" placeholder="5" step="0.1">
                        </div>
                    </div>

                    <div class="section-divider"></div>

                    <div class="assumptions-section">
                        <h4 class="accent-earth">📈 Verdsettelsesforutsetninger</h4>
                        <div class="assumptions-grid">
                            <div class="financial-item">
                                <label for="wacc">
                                    WACC - Kapitalkostnad (%)
                                    <span class="tooltip-icon">?
                                        <span class="tooltip">Weighted Average Cost of Capital. Gjennomsnittlig kostnad for selskapets finansiering (egenkapital og gjeld). Brukes som diskonteringsrente.</span>
                                    </span>
                                </label>
                                <input type="number" id="wacc" placeholder="8.5" step="0.1">
                            </div>
                            <div class="financial-item">
                                <label for="terminalGrowth">
                                    Terminal vekstrate (%)
                                    <span class="tooltip-icon">?
                                        <span class="tooltip">Forventet langsiktig vekstrate etter den eksplisitte prognoseperioden. Vanligvis satt til inflasjonsnivå eller BNP-vekst.</span>
                                    </span>
                                </label>
                                <input type="number" id="terminalGrowth" placeholder="2.5" step="0.1">
                            </div>
                            <div class="financial-item">
                                <label for="industryPE">
                                    Bransje P/E ratio
                                    <span class="tooltip-icon">?
                                        <span class="tooltip">Price-to-Earnings ratio for sammenlignbare selskaper i samme bransje. Viser hvor mye investorer betaler per krone i resultat.</span>
                                    </span>
                                </label>
                                <input type="number" id="industryPE" placeholder="15" step="0.1">
                            </div>
                            <div class="financial-item">
                                <label for="industryEVEBITDA">
                                    Bransje EV/EBITDA
                                    <span class="tooltip-icon">?
                                        <span class="tooltip">Enterprise Value delt på EBITDA for sammenlignbare selskaper. Viser selskapets totale verdi relativt til driftsresultat.</span>
                                    </span>
                                </label>
                                <input type="number" id="industryEVEBITDA" placeholder="8" step="0.1">
                            </div>
                        </div>
                        
                        <div class="assumptions-toggle" id="assumptionsToggle" onclick="toggleAssumptionsExplanation()">
                            <span class="assumptions-toggle-title">📊 Hvor kommer disse tallene fra?</span>
                            <span class="assumptions-toggle-icon">▼</span>
                        </div>
                        
                        <div class="assumptions-explanation" id="assumptionsExplanation">
                            <h5>📊 Hvor kommer disse tallene fra?</h5>
                            <p>Verdsettelsesforutsetningene er automatisk kalibrert basert på selskapets bransjetilhørighet og sammenlignbare selskaper:</p>
                            <ul>
                                <li><strong>WACC (Kapitalkostnad):</strong> Beregnes ut fra bransjerisiko, risikofi rente (norske statsobligasjoner) og markedsrisikopremie. Teknologi- og fintech-selskaper har høyere WACC på grunn av økt risiko.</li>
                                <li><strong>Terminal vekstrate:</strong> Settes vanligvis til langsiktig inflasjonsmål (2-3%) eller forventet BNP-vekst for Norge, da selskaper ikke kan vokse raskere enn økonomien på lang sikt.</li>
                                <li><strong>Bransje P/E ratio:</strong> Basert på gjennomsnitt av børsnoterte selskaper i samme bransje. Hentes fra Oslo Børs og internasjonale markeder for sammenlignbare selskaper.</li>
                                <li><strong>EV/EBITDA multiplikator:</strong> Industristandard fra transaksjonsdata og børsnoterte sammenlignbare selskaper. Justeres for selskapets størrelse og vekstprofil.</li>
                            </ul>
                            <p><em>Du kan justere disse verdiene manuelt hvis du har spesifikke markedsinnsikter eller ønsker å teste ulike scenarioer.</em></p>
                        </div>
                    </div>
                    
                    <button onclick="calculateValuation()" class="btn-primary" id="calculateBtn">💰 Beregn Selskapsverdivurdering</button>
                </div>

                <div class="valuation-section" id="valuationSection" style="display: none;">
                    <h3>💎 Selskapsverdivurdering</h3>
                    
                    <div class="valuation-methods" id="valuationMethods">
                        <!-- Methods will be populated by JavaScript -->
                    </div>

                    <div class="final-valuation" id="finalValuation">
                        <div class="final-value" id="finalValue">-</div>
                        <div class="final-range" id="finalRange">-</div>
                        <p style="margin-top: 15px; opacity: 0.9;">Vektet gjennomsnitt basert på klassiske verdsettelsesmetoder</p>
                    </div>

                    <div class="recommendations-section" id="recommendationsSection" style="display: none;">
                        <h3>🚀 Verdidrivende tiltak for økt selskapsverdivurdering</h3>
                        <div class="recommendation-cards" id="recommendationCards">
                            <!-- Recommendations will be populated by JavaScript -->
                        </div>
                        <div class="financing-cta">
                            <h4>💰 Finansiering for vekstmuligheter</h4>
                            <p>Aprila Bank kan tilby kortsiktig kassekresditt og finansieringsløsninger som gir deg fleksibilitet til å gripe investeringsmuligheter som driver topplinjevekst og øker selskapsverdien.</p>
                            <button class="cta-button" onclick="alert('Kontakt Aprila Bank for skreddersydd finansieringsløsning!')">Kontakt oss for finansiering</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="powered-by">
            <span class="accent-rust">Powered by Aprila Bank ASA</span>
        </div>
    </div>

    <script>
        // Mock data with more comprehensive financial information
        const mockCompanies = {
            '123456789': {
                name: 'Teknologi Innovasjon AS',
                orgNumber: '123456789',
                revenue: 50000000,
                ebitda: 12000000,
                netIncome: 8000000,
                totalAssets: 35000000,
                equity: 25000000,
                debt: 10000000,
                fcf: 9000000,
                growthRate: 12,
                sector: 'Technology'
            },
            '987654321': {
                name: 'Handel & Service AS',
                orgNumber: '987654321',
                revenue: 25000000,
                ebitda: 3500000,
                netIncome: 2000000,
                totalAssets: 15000000,
                equity: 8000000,
                debt: 7000000,
                fcf: 2500000,
                growthRate: 6,
                sector: 'Retail'
            },
            'eksempel as': {
                name: 'Eksempel Manufacturing AS',
                orgNumber: '555666777',
                revenue: 75000000,
                ebitda: 8000000,
                netIncome: 3500000,
                totalAssets: 45000000,
                equity: 20000000,
                debt: 25000000,
                fcf: 4000000,
                growthRate: 4,
                sector: 'Manufacturing'
            },
            'aprila test': {
                name: 'Aprila Test Fintech AS',
                orgNumber: '444555666',
                revenue: 15000000,
                ebitda: 5000000,
                netIncome: 3000000,
                totalAssets: 12000000,
                equity: 9000000,
                debt: 3000000,
                fcf: 3500000,
                growthRate: 25,
                sector: 'Fintech'
            }
        };

        // Add event listeners when DOM is ready
        document.addEventListener('DOMContentLoaded', function() {
            const searchBtn = document.getElementById('searchBtn');
            const searchInput = document.getElementById('searchInput');
            
            if (searchBtn) {
                searchBtn.addEventListener('click', searchCompany);
            }
            
            if (searchInput) {
                searchInput.addEventListener('keypress', function(e) {
                    if (e.key === 'Enter') {
                        searchCompany();
                    }
                });
            }
            
            // Set default assumptions
            setDefaultAssumptions();
            
            // Allow users to modify financial data and recalculate
            document.querySelectorAll('input[type="number"]').forEach(input => {
                input.addEventListener('input', function() {
                    const valuationSection = document.getElementById('valuationSection');
                    if (valuationSection) {
                        valuationSection.style.display = 'none';
                    }
                });
            });
        });

        function setDefaultAssumptions() {
            const wacc = document.getElementById('wacc');
            const terminalGrowth = document.getElementById('terminalGrowth');
            const industryPE = document.getElementById('industryPE');
            const industryEVEBITDA = document.getElementById('industryEVEBITDA');
            
            if (wacc) wacc.value = 8.5;
            if (terminalGrowth) terminalGrowth.value = 2.5;
            if (industryPE) industryPE.value = 15;
            if (industryEVEBITDA) industryEVEBITDA.value = 8;
        }

        function searchCompany() {
            const searchInput = document.getElementById('searchInput');
            const loading = document.getElementById('loading');
            const resultsSection = document.getElementById('resultsSection');
            const searchBtn = document.getElementById('searchBtn');
            
            if (!searchInput) {
                console.log("Search input not found");
                return;
            }
            
            const searchTerm = searchInput.value.trim().toLowerCase();
            console.log("Searching for:", searchTerm);
            
            if (!searchTerm) {
                alert("Vennligst skriv inn et søkeord");
                return;
            }
            
            // Show loading
            if (loading) loading.style.display = 'block';
            if (resultsSection) resultsSection.style.display = 'none';
            if (searchBtn) searchBtn.disabled = true;
            
            // Simulate API call delay
            setTimeout(() => {
                let company = null;
                
                console.log("Available companies:", Object.keys(mockCompanies));
                
                // Search by org number or name (direct match)
                if (mockCompanies[searchTerm]) {
                    company = mockCompanies[searchTerm];
                    console.log("Direct match found:", company.name);
                } else {
                    // Search by name (partial match)
                    for (let key in mockCompanies) {
                        const companyName = mockCompanies[key].name.toLowerCase();
                        console.log("Checking company:", companyName, "against:", searchTerm);
                        if (companyName.includes(searchTerm)) {
                            company = mockCompanies[key];
                            console.log("Partial match found:", company.name);
                            break;
                        }
                    }
                }
                
                if (loading) loading.style.display = 'none';
                if (searchBtn) searchBtn.disabled = false;
                
                if (company) {
                    console.log("Displaying company:", company.name);
                    displayCompany(company);
                } else {
                    console.log("No company found for:", searchTerm);
                    showError('Fant ikke selskap i våre registre. Prøv med: "123456789", "987654321", "Eksempel AS" eller "Aprila Test" for demo.');
                }
            }, 1500);
        }

        function displayCompany(company) {
            const resultsSection = document.getElementById('resultsSection');
            const valuationSection = document.getElementById('valuationSection');
            const recommendationsSection = document.getElementById('recommendationsSection');
            
            // Hide any previous error messages
            const errorDiv = document.getElementById('errorMessage');
            if (errorDiv) {
                errorDiv.style.display = 'none';
            }
            
            // Show company info section
            const companyInfo = resultsSection.querySelector('.company-info');
            if (companyInfo) {
                companyInfo.style.display = 'block';
            }
            
            // Safely update company info
            const companyNameEl = document.getElementById('companyName');
            const orgNumberEl = document.getElementById('orgNumber');
            
            if (companyNameEl) companyNameEl.textContent = company.name;
            if (orgNumberEl) orgNumberEl.textContent = `Org.nr: ${company.orgNumber}`;
            
            // Safely populate financial data (no formatting)
            const fields = ['revenue', 'ebitda', 'netIncome', 'totalAssets', 'equity', 'debt', 'fcf', 'growthRate'];
            fields.forEach(field => {
                const element = document.getElementById(field);
                if (element && company[field] !== undefined) {
                    element.value = company[field];
                }
            });
            
            // Set sector-specific assumptions
            setSectorAssumptions(company.sector);
            
            // Store sector for recommendations
            window.currentSector = company.sector;
            
            if (resultsSection) resultsSection.style.display = 'block';
            if (valuationSection) valuationSection.style.display = 'none';
            if (recommendationsSection) recommendationsSection.style.display = 'none';
        }

        function setSectorAssumptions(sector) {
            const assumptions = {
                'Technology': { wacc: 9.5, pe: 20, evEbitda: 12 },
                'Fintech': { wacc: 10.0, pe: 25, evEbitda: 15 },
                'Manufacturing': { wacc: 8.0, pe: 12, evEbitda: 6 },
                'Retail': { wacc: 8.5, pe: 15, evEbitda: 8 }
            };
            
            const sectorData = assumptions[sector] || assumptions['Manufacturing'];
            
            const waccEl = document.getElementById('wacc');
            const peEl = document.getElementById('industryPE');
            const evEbitdaEl = document.getElementById('industryEVEBITDA');
            
            if (waccEl) waccEl.value = sectorData.wacc;
            if (peEl) peEl.value = sectorData.pe;
            if (evEbitdaEl) evEbitdaEl.value = sectorData.evEbitda;
        }

        function calculateValuation() {
            // Get financial data - simple parseFloat without formatting
            const revenue = parseFloat(document.getElementById('revenue').value) || 0;
            const ebitda = parseFloat(document.getElementById('ebitda').value) || 0;
            const netIncome = parseFloat(document.getElementById('netIncome').value) || 0;
            const totalAssets = parseFloat(document.getElementById('totalAssets').value) || 0;
            const equity = parseFloat(document.getElementById('equity').value) || 0;
            const debt = parseFloat(document.getElementById('debt').value) || 0;
            const fcf = parseFloat(document.getElementById('fcf').value) || 0;
            const growthRate = parseFloat(document.getElementById('growthRate').value) || 5;
            
            // Get assumptions
            const wacc = parseFloat(document.getElementById('wacc').value) || 8.5;
            const terminalGrowth = parseFloat(document.getElementById('terminalGrowth').value) || 2.5;
            const industryPE = parseFloat(document.getElementById('industryPE').value) || 15;
            const industryEVEBITDA = parseFloat(document.getElementById('industryEVEBITDA').value) || 8;
            
            if (revenue === 0 || netIncome === 0) {
                showError('Omsetning og årsresultat må være fylt ut for å beregne verdivurdering.');
                return;
            }
            
            // Calculate different valuation methods
            const valuations = {
                dcf: calculateDCF(fcf, growthRate, wacc, terminalGrowth),
                pe: calculatePEValuation(netIncome, industryPE),
                evEbitda: calculateEVEBITDA(ebitda, industryEVEBITDA, debt),
                bookValue: equity,
                assetBased: totalAssets * 0.8, // Assuming 20% discount for liquidation
                revenueMultiple: revenue * getRevenueMultiple(growthRate)
            };
            
            displayValuation(valuations);
            generateRecommendations(revenue, ebitda, netIncome, equity, debt, growthRate, window.currentSector || 'Technology');
        }

        function calculateDCF(fcf, growthRate, wacc, terminalGrowth) {
            if (fcf <= 0) return 0;
            
            const projectionYears = 5;
            let presentValue = 0;
            
            // Project cash flows for 5 years
            for (let year = 1; year <= projectionYears; year++) {
                const projectedFCF = fcf * Math.pow(1 + growthRate/100, year);
                const discountFactor = Math.pow(1 + wacc/100, year);
                presentValue += projectedFCF / discountFactor;
            }
            
            // Terminal value
            const terminalFCF = fcf * Math.pow(1 + growthRate/100, projectionYears) * (1 + terminalGrowth/100);
            const terminalValue = terminalFCF / ((wacc/100) - (terminalGrowth/100));
            const discountedTerminalValue = terminalValue / Math.pow(1 + wacc/100, projectionYears);
            
            return presentValue + discountedTerminalValue;
        }

        function calculatePEValuation(netIncome, pe) {
            return netIncome * pe;
        }

        function calculateEVEBITDA(ebitda, multiple, debt) {
            const enterpriseValue = ebitda * multiple;
            return Math.max(0, enterpriseValue - debt); // Equity value
        }

        function getRevenueMultiple(growthRate) {
            if (growthRate >= 20) return 3.0;
            if (growthRate >= 15) return 2.5;
            if (growthRate >= 10) return 2.0;
            if (growthRate >= 5) return 1.5;
            return 1.0;
        }

        function displayValuation(valuations) {
            const valuationSection = document.getElementById('valuationSection');
            const valuationMethods = document.getElementById('valuationMethods');
            const finalValue = document.getElementById('finalValue');
            const finalRange = document.getElementById('finalRange');
            
            // Clear previous results
            if (valuationMethods) valuationMethods.innerHTML = '';
            
            const methods = [
                { 
                    key: 'dcf', 
                    title: 'DCF-verdi', 
                    description: 'Diskontert kontantstrøm-modell',
                    tooltip: 'Beregner nåverdien av fremtidige kontantstrømmer diskontert med kapitalkostnaden (WACC). Regnes som den mest fundamentale verdsettelsesmetoden.'
                },
                { 
                    key: 'pe', 
                    title: 'P/E-verdi', 
                    description: 'Pris/resultat-multiplikator',
                    tooltip: 'Multipliserer årsresultatet med bransje P/E-ratio. Basert på hva investorer er villige til å betale for lignende selskaper.'
                },
                { 
                    key: 'evEbitda', 
                    title: 'EV/EBITDA-verdi', 
                    description: 'Enterprise value multiplikator',
                    tooltip: 'Beregner enterprise value basert på EBITDA og bransje-multiplikator, deretter trekkes gjeld fra for å få egenkapitalverdi.'
                },
                { 
                    key: 'bookValue', 
                    title: 'Bokført verdi', 
                    description: 'Egenkapital fra balansen',
                    tooltip: 'Bokført egenkapitalverdi fra balansen. Representerer historisk verdi av eierens investeringer minus akkumulerte tap.'
                },
                { 
                    key: 'assetBased', 
                    title: 'Aktivabasert verdi', 
                    description: 'Likvidasjonsverdi av eiendeler',
                    tooltip: 'Estimerer verdien ved salg av alle eiendeler. Bruker 80% av bokført verdi for å reflektere realistisk salgsverdi.'
                },
                { 
                    key: 'revenueMultiple', 
                    title: 'Omsetning-multiplikator', 
                    description: 'Basert på omsetning og vekst',
                    tooltip: 'Multipliserer omsetning med en faktor basert på vekstrate. Høyere vekst gir høyere multiplikator (1x-3x av omsetning).'
                }
            ];
            
            methods.forEach(method => {
                const value = valuations[method.key];
                const methodCard = document.createElement('div');
                methodCard.className = 'method-card';
                methodCard.innerHTML = `
                    <div class="method-title">
                        ${method.title}
                        <span class="tooltip-icon">?
                            <span class="tooltip">${method.tooltip}</span>
                        </span>
                    </div>
                    <div class="method-value">${formatCurrency(value)}</div>
                    <div class="method-description">${method.description}</div>
                `;
                if (valuationMethods) valuationMethods.appendChild(methodCard);
            });
            
            // Calculate weighted average (give more weight to DCF and P/E)
            const weights = {
                dcf: 0.3,
                pe: 0.25,
                evEbitda: 0.2,
                bookValue: 0.1,
                assetBased: 0.05,
                revenueMultiple: 0.1
            };
            
            let weightedSum = 0;
            let totalWeight = 0;
            
            Object.keys(valuations).forEach(key => {
                if (valuations[key] > 0) {
                    weightedSum += valuations[key] * weights[key];
                    totalWeight += weights[key];
                }
            });
            
            const average = totalWeight > 0 ? weightedSum / totalWeight : 0;
            const values = Object.values(valuations).filter(v => v > 0);
            const min = Math.min(...values);
            const max = Math.max(...values);
            
            if (finalValue) finalValue.textContent = formatCurrency(average);
            if (finalRange) finalRange.textContent = `Verdiområde: ${formatCurrency(min)} - ${formatCurrency(max)}`;
            
            if (valuationSection) {
                valuationSection.style.display = 'block';
                valuationSection.scrollIntoView({ behavior: 'smooth' });
            }
        }

        function formatCurrency(value) {
            if (value >= 1000000000) {
                return `${(value / 1000000000).toFixed(1)}B NOK`;
            } else if (value >= 1000000) {
                return `${(value / 1000000).toFixed(1)}M NOK`;
            } else if (value >= 1000) {
                return `${(value / 1000).toFixed(0)}k NOK`;
            }
            return `${Math.round(value)} NOK`;
        }

        function showError(message) {
            const resultsSection = document.getElementById('resultsSection');
            if (resultsSection) {
                // Instead of overwriting the entire section, just show error above it
                let errorDiv = document.getElementById('errorMessage');
                if (!errorDiv) {
                    errorDiv = document.createElement('div');
                    errorDiv.id = 'errorMessage';
                    errorDiv.className = 'error';
                    resultsSection.insertBefore(errorDiv, resultsSection.firstChild);
                }
                errorDiv.innerHTML = `<strong>Feil:</strong> ${message}`;
                resultsSection.style.display = 'block';
                
                // Hide other sections when showing error
                const companyInfo = resultsSection.querySelector('.company-info');
                const valuationSection = document.getElementById('valuationSection');
                const recommendationsSection = document.getElementById('recommendationsSection');
                
                if (companyInfo) companyInfo.style.display = 'none';
                if (valuationSection) valuationSection.style.display = 'none';
                if (recommendationsSection) recommendationsSection.style.display = 'none';
            }
        }

        function generateRecommendations(revenue, ebitda, netIncome, equity, debt, growthRate, sector) {
            const recommendationsSection = document.getElementById('recommendationsSection');
            const recommendationCards = document.getElementById('recommendationCards');
            
            if (!recommendationCards) return;
            
            // Clear previous recommendations
            recommendationCards.innerHTML = '';
            
            // Calculate key metrics for analysis
            const ebitdaMargin = revenue > 0 ? (ebitda / revenue) * 100 : 0;
            const netMargin = revenue > 0 ? (netIncome / revenue) * 100 : 0;
            const debtToEquity = equity > 0 ? debt / equity : 0;
            const revenueSize = revenue / 1000000; // in millions
            
            // Generate sector-specific recommendations
            let recommendations = [];
            
            // Revenue Growth Recommendations
            if (growthRate < 10) {
                recommendations.push({
                    icon: '📈',
                    title: 'Øk topplinjevekst',
                    content: getSectorSpecificGrowthAdvice(sector, revenueSize),
                    impact: calculateRevenueGrowthImpact(revenue, growthRate),
                    impactLabel: 'Potensiell verdiøkning'
                });
            }
            
            // Market Expansion
            if (revenueSize < 100 && growthRate > 5) {
                recommendations.push({
                    icon: '🌍',
                    title: 'Markedsekspansjon',
                    content: `Med ${growthRate}% vekst er selskapet modent for ekspansjon. Invester i nye markeder, produktlinjer eller geografiske områder. Kortsiktig kassekresditt kan finansiere markedsføring og salgsaktiviteter som driver omsetningsvekst.`,
                    impact: revenue * 0.3, // 30% potential increase
                    impactLabel: 'Markedsekspansjon potensial'
                });
            }
            
            // Operational Efficiency
            if (ebitdaMargin < getSectorBenchmark(sector).ebitdaMargin) {
                recommendations.push({
                    icon: '⚡',
                    title: 'Forbedre operasjonell effektivitet',
                    content: getEfficiencyAdvice(sector, ebitdaMargin),
                    impact: revenue * (getSectorBenchmark(sector).ebitdaMargin - ebitdaMargin) / 100,
                    impactLabel: 'EBITDA-forbedring potensial'
                });
            }
            
            // Investment & Technology
            if (sector === 'Technology' || sector === 'Fintech') {
                recommendations.push({
                    icon: '💻',
                    title: 'Teknologi- og innovasjonsinvesteringer',
                    content: `Invester i FoU, teknologioppgraderinger og digitalisering. Dette kan øke produktiviteten med 15-25% og åpne nye inntektsstrømmer. Kortsiktig finansiering kan dekke utviklingskostnader før inntektene realiseres.`,
                    impact: revenue * 0.2,
                    impactLabel: 'Teknologi-investering potensial'
                });
            }
            
            // Working Capital Optimization
            if (debtToEquity > 0.5) {
                recommendations.push({
                    icon: '💰',
                    title: 'Optimaliser arbeidskapital',
                    content: `Med gjeld/egenkapital på ${debtToEquity.toFixed(1)}, kan bedre kontantstrømstyring og arbeidskapitaloptimalisering frigjøre midler. Kortsiktig kassekresditt kan gi fleksibilitet til å optimalisere leverandørbetalinger og lagernivåer.`,
                    impact: debt * 0.1,
                    impactLabel: 'Arbeidskapital-optimalisering'
                });
            }
            
            // Select top 3 most relevant recommendations
            recommendations = recommendations.slice(0, 3);
            
            // Display recommendations
            recommendations.forEach(rec => {
                const card = document.createElement('div');
                card.className = 'recommendation-card';
                card.innerHTML = `
                    <div class="recommendation-title">
                        <span>${rec.icon}</span>
                        ${rec.title}
                    </div>
                    <div class="recommendation-content">${rec.content}</div>
                    <div class="impact-metric">
                        <div class="impact-value">${formatCurrency(rec.impact)}</div>
                        <div class="impact-description">${rec.impactLabel}</div>
                    </div>
                `;
                recommendationCards.appendChild(card);
            });
            
            if (recommendationsSection) {
                recommendationsSection.style.display = 'block';
            }
        }

        function getSectorSpecificGrowthAdvice(sector, revenueSize) {
            const advice = {
                'Technology': `Fokuser på produktutvikling og kundeakquisisjon. Med ${revenueSize.toFixed(0)}M NOK i omsetning, kan strategiske investeringer i salg og markedsføring øke veksten til 15-20%. Kortsiktig finansiering kan dekke investeringer i salgsressurser og produktlansering.`,
                'Fintech': `Utvid kundebasen gjennom digitale kanaler og partnerskaper. Invester i compliance og regulatorisk etterlevelse for å åpne nye markeder. Kassekresditt kan finansiere teknologiutvikling og markedsføring som driver kundevekst.`,
                'Manufacturing': `Automatiser produksjon og utvid kapasitet. Invester i utstyr og teknologi som øker produksjonsvolum og kvalitet. Kortsiktig finansiering kan dekke maskininnkjøp og lagerutbygging før økt salg realiseres.`,
                'Retail': `Ekspander distribution og forbedre kundeopplevelse. Invester i e-handel, lagerstyring og markedsføring. Sesongfinansiering kan hjelpe med lagerkjøp og markedsføringskampanjer som driver salg.`
            };
            
            return advice[sector] || advice['Technology'];
        }

        function getEfficiencyAdvice(sector, currentMargin) {
            return `Din EBITDA-margin på ${currentMargin.toFixed(1)}% er under bransjesnittet. Fokuser på kostnadsoptimalisering, automatisering og prosessforbedringer. Kortsiktig finansiering kan dekke investeringer i effektivitetstiltak som gir rask avkastning.`;
        }

        function getSectorBenchmark(sector) {
            const benchmarks = {
                'Technology': { ebitdaMargin: 25 },
                'Fintech': { ebitdaMargin: 30 },
                'Manufacturing': { ebitdaMargin: 15 },
                'Retail': { ebitdaMargin: 10 }
            };
            
            return benchmarks[sector] || benchmarks['Technology'];
        }

        function calculateRevenueGrowthImpact(revenue, currentGrowth) {
            const targetGrowth = Math.max(currentGrowth + 5, 12); // Increase by 5% or to 12% minimum
            const currentValue = revenue * 15; // Simple P/E multiple
            const improvedValue = revenue * (1 + targetGrowth/100) * 15;
            return improvedValue - currentValue;
        }

        function toggleAssumptionsExplanation() {
            const toggle = document.getElementById('assumptionsToggle');
            const explanation = document.getElementById('assumptionsExplanation');
            
            if (!toggle || !explanation) return;
            
            const isActive = toggle.classList.contains('active');
            
            if (isActive) {
                // Hide explanation
                toggle.classList.remove('active');
                explanation.classList.remove('show');
                setTimeout(() => {
                    explanation.style.display = 'none';
                }, 300);
            } else {
                // Show explanation
                toggle.classList.add('active');
                explanation.style.display = 'block';
                setTimeout(() => {
                    explanation.classList.add('show');
                }, 10);
            }
        }
    </script>
</body>
</html>
