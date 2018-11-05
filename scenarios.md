---

copyright:
  years: 2018
lastupdated: "2018-11-02"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}

<!-- Link definitions -->


# Scenarios
{: #scenarios}

IBM provides a number of predefined scenario sets that you can apply by using the `ibm-scenario-set-name` parameter when you submit a `POST /v2/simulate` request.
{: shortdesc}

<!-- ##  Standard shift scenarios -->

Standard shift scenarios represent standardized shocks to risk factors. 
Standard shifts include pre-defined absolute shifts (for example, + 10 basis points 
to a curve) or relative shifts (for example, -10% to an equity index). 
As these values are standardized, scenario definitions don't need to be 
updated periodically. You can access scenario definitions in the API by including the 
scenario name in the `ibm-scenario-set-name` payload parameter.

Standard shift scenarios are often required as part of financial regulation, as well as for internal risk management reporting. 

The following are the major types of standard shift scenario sets that are available to the user:
* [Equity Standard Shift Scenarios](/docs/services/simulated-instrument-analytics/scenarios.html#eq)
* [Interest Rate Standard Shift Scenarios](/docs/services/simulated-instrument-analytics/scenarios.html#ir)
* [Credit Spread Standard Shift Scenarios](/docs/services/simulated-instrument-analytics/scenarios.html#cs)
* [FX Standard Shift Scenarios](/docs/services/simulated-instrument-analytics/scenarios.html#fx)

<!-- Note: As these -->

## Equity standard shift scenarios
{: #eq}

Each equity standard shift scenario set includes the following standard shifts:

* **Down 10%** - *A 10% decrease to the specified equity index*
* **Up 10%** - *A 10% increase to the specified equity index*
* **no changes** - *A baseline scenario with no shift to equity indexes*

The following Equity Indexes have support for standard shifts to equity scenarios:

|Scenario Set Name|Equity Index|Equity Index Ticker|Region|
|------------|----------|------------|------|-----------|
|**IBM_EquityIndexShifts_AllIndexes**|*All Supported Indexes*|N/A|All|
|**IBM_EquityIndexShifts_ADI**|*ABU DHABI SECURITIES EXCHANGE GN IDX*|ADI|EU|
|**IBM_EquityIndexShifts_AEX**|*AMSTERDAM EXCHANGE INDEX*|AEX|EU|
|**IBM_EquityIndexShifts_AORD**|*S&P ASX ALL ORD INDEX*|AORD|AP|
|**IBM_EquityIndexShifts_ATG**|*AT SE GENERAL IDX*|ATG|EU|
|**IBM_EquityIndexShifts_ATX**|*VIENNA SE AUSTRIAN TRADED IDX Index*|ATX|EU|
|**IBM_EquityIndexShifts_BFX**|*BEL-20 INDEX*|BFX|EU|
|**IBM_EquityIndexShifts_BSESN**|*S&P BSE SENSEX IDX*|BSESN|AP|
|**IBM_EquityIndexShifts_BUX**|*BUDAPEST SE IDX*|BUX|EU|
|**IBM_EquityIndexShifts_BVLG**|*PSI ALL SHARE GROSS RETURN INDEX*|BVLG|EU|
|**IBM_EquityIndexShifts_BVSP**|*SAO PAULO SE BOVESPA INDEX*|BVSP|NA|
|**IBM_EquityIndexShifts_DFMGI**|*DFM DFM GENERAL IDX*|DFMGI|EU|
|**IBM_EquityIndexShifts_EGX30**|*EGX 30 IDX*|EGX30|EU|
|**IBM_EquityIndexShifts_FCHI**|*CAC 40 INDEX*|FCHI|EU|
|**IBM_EquityIndexShifts_FTAS**|*FTSE ALL SHARE INDEX*|FTAS|EU|
|**IBM_EquityIndexShifts_FTITLMS**|*FT IT ALL SHARE IDX*|FTITLMS|EU|
|**IBM_EquityIndexShifts_GDAX**|*DEUTSCHE BORSE DAX INDEX*|GDAX|EU|
|**IBM_EquityIndexShifts_GSPTSE**|*TSX-Toronto Stock Exchange 300 Composite Index*|GSPTSE|NA|
|**IBM_EquityIndexShifts_HSI**|*HANG SENG INDEX*|HSI|AP|
|**IBM_EquityIndexShifts_IBEX**|*IBEX 35 COMPOSITE INDEX*|IBEX|EU|
|**IBM_EquityIndexShifts_IGBC**|*COLOMBIA SE GENERAL INDEX*|IGBC|NA|
|**IBM_EquityIndexShifts_IGPA**|*CHILEAN SE IGPA INDEX*|IGPA|NA|
|**IBM_EquityIndexShifts_IMOEX**|*MOEX Russia Index*|IMOEX|EU|
|**IBM_EquityIndexShifts_ISEQ**|*ISEQ OVERALL IDX*|ISEQ|EU|
|**IBM_EquityIndexShifts_JALSH**|*ALL SHARE*|JALSH|EU|
|**IBM_EquityIndexShifts_JKSE**|*JSX COMPOSITE INDEX*|JKSE|AP|
|**IBM_EquityIndexShifts_KLSE**|*FTSE BURSA MALAYSIA KLCI IDX*|KLSE|AP|
|**IBM_EquityIndexShifts_KS11**|*KOREA SE KOSPI IDX*|KS11|AP|
|**IBM_EquityIndexShifts_KSE**|*KSE 100 INDEX*|KSE|AP|
|**IBM_EquityIndexShifts_LUXX**|*LUXEMBOURG SE LUXX X INDEX*|LUXX|EU|
|**IBM_EquityIndexShifts_MXX**|*S&P/BMV IPC*|MXX|NA|
|**IBM_EquityIndexShifts_NZ50**|*NEW ZEALAND EXCH NZSX 50 FREE IDX*|NZ50|AP|
|**IBM_EquityIndexShifts_OMXCPI**|*OMXC ALL PI*|OMXCPI|EU|
|**IBM_EquityIndexShifts_OMXHPI**|*OMXH GEN PI*|OMXHPI|EU|
|**IBM_EquityIndexShifts_OMXSPI**|*OMXS ALL SHARE*|OMXSPI|EU|
|**IBM_EquityIndexShifts_OSEBX**|*OSE BENCH IND_GI*|OSEBX|EU|
|**IBM_EquityIndexShifts_PSI**|*THE PHILIPPINE STOCK EXC PSEI INDEX*|PSI|AP|
|**IBM_EquityIndexShifts_PX**|*PX-PRAGUE SE IND IDX*|PX|EU|
|**IBM_EquityIndexShifts_QSI**|*QE EXCHANGE GENERAL IDX*|QSI|EU|
|**IBM_EquityIndexShifts_SETI**|*THAILAND SET IDX*|SETI|AP|
|**IBM_EquityIndexShifts_SPX**|*S&P 500 INDEX*|SPX|NA|
|**IBM_EquityIndexShifts_SSEC**|*SHANGHAI SE COMPOSITE INDEX*|SSEC|AP|
|**IBM_EquityIndexShifts_SSMI**|*SWISS MARKET IND*|SSMI|EU|
|**IBM_EquityIndexShifts_STI**|*FTSE STRAITS TIMES IDX*|STI|EU|
|**IBM_EquityIndexShifts_SZSC1**|*SZSE CMPN INDEX*|SZSC1|AP|
|**IBM_EquityIndexShifts_TA125**|*TASE MAIN 125 IDX*|TA125|EU|
|**IBM_EquityIndexShifts_TOPX**|*TOPIX PRICE INDEX*|TOPX|AP|
|**IBM_EquityIndexShifts_TWII**|*TAIWAN SE WEIGHTED INDEX*|TWII|AP|
|**IBM_EquityIndexShifts_WIG**|*WIG POLAND INDEX*|WIG|EU|
|**IBM_EquityIndexShifts_XU100**|*BIST 100 IDX*|XU100|EU|

## Interest rate standard shift scenarios
{: #ir}

Each interest rate standard shift scenario set includes the following standard shifts:

### Parallel shock scenarios

* **Parallel 100bp shift** - *An absolute increase of 100bp to all terms on the specified interest rate curve(s)*
* **Parallel 50bp shift** - *An absolute increase of 50bp to all terms on the specified interest rate curve(s)*
* **Parallel 10bp shift** - *An absolute increase of 10bp to all terms on the specified interest rate curve(s)*
* **Parallel 1bp shift** - *An absolute increase of 1bp to all terms on the specified interest rate curve(s)*
* **Parallel 0bp shift** - *A baseline scenario with no shift to interest rate curve(s)*
* **Parallel -1bp shift** - *An absolute decrease of 1bp to all terms on the specified interest rate curve(s)*
* **Parallel -10bp shift** - *An absolute decrease of 10bp to all terms on the specified interest rate curve(s)*
* **Parallel -50bp shift** - *An absolute decrease of 50bp to all terms on the specified interest rate curve(s)*
* **Parallel -100bp shift** - *An absolute decrease of 100bp to all terms on the specified interest rate curve(s)*

### Non-parallel shock scenarios

* **Steepening** - *A non-parallel shift in which short-term interest rates rise quickly up to the 10-year term and then rise more gradually up to the 30-year term.*
* **Flattening** - *A non-parallel shift in which short-term interest rates fall quickly up to the 10-year term and then fall gradually to the 30-year term.*
* **Rotation 1** - *A non-parallel shift in which short-term rates increase by 10bps, then the change in rates drops linearly to 0 up to the 10-year term, followed by no change in rates after the 10-year term.*
* **Rotation 2** - *A non-parallel shift in which there are no changes in short-term rates up to the 2-year term, with medium rates that increase linearly out to the 30-year term.*
* **Rotation 3** - *A non-parallel shift in which short-term rates fall by 10bps, then the change in rates increases linearly to 0 up to the 10-year term, followed by no change in rates after the 10-year term. **Note:** Rotation 3 is the same as Rotation 1 in the alternative direction.*
* **Rotation 4** - *A non-parallel shift in which there are no changes in short-term rates up to the 2-year term, with medium rates that increase linearly out to the 30-year term. **Note:** Rotation 4 is the same as Rotation 2 in the alternate direction.*

### Variable factor scenarios

* **Twist Up** - *A relative shift in which interest rates twist around the 2-year term. Short-term rates fall by declining magnitudes until the 2-year term which experiences no change. Longer-term rates rise gradually up to the 30-year term to which a relative term increase of ~25% is applied.* 
* **Twist Down** - *A relative shift in which interest rates twist around the 2-year term. Short-term rates rise by decreasing magnitudes until the 2-year term which experiences no change. Longer-term rates fall by increasing magnitudes up to the 30-year term to which a relative term increase of ~25% is applied.* 
* **Butterfly Up** - *A relative shift in which interest rates twist around two curve points: the 2-year term and the 10-year term. Short-term rates fall by declining magnitudes until the 2-year term which is held constant. Medium-term rates rise with increasing magnitudes to the 5-year term, after which they begin to fall until the 10-year term which is also held constant. Long-term rates then decline with increasing magnitudes out to the 30-year term.*
* **Butterfly Down** - *A relative shift in which interest rates twist around two curve points: the 2-year term and the 10-year term. Short-term rates rise by declining magnitudes until the 2-year term which is held constant. Medium-term rates fall with increasing magnitudes to the 5-year term, after which they begin to rise until the 10-year term which is also held constant. Long-term rates then increase with increasing magnitudes out to the 30-year term.*

Interest rate curves are grouped into three types of curves: Treasury Curves, Interbank Curves, and Overnight-Index-Swap (OIS) Curves. 
The following interet rate curves have support for interest rate standard shift scenario sets:

|Scenario Set Name|Country or Region|Treasury Curves|Interbank Curves|OIS Curves
|------------|----------|------------|------|-----------|
|**IBM_InterestRateShifts_AllCurves**|*All Supported Curves*|X|X|X|
|**IBM_InterestRateShifts_TreasuryCurves**|*All Supported Curves*|X|||
|**IBM_InterestRateShifts_InterbankCurves**|*All Supported Curves*||X||
|**IBM_InterestRateShifts_OisCurves**|*All Supported Curves*|||X|
|**IBM_InterestRateShifts_AUD_treasury**|*Australia*|X|||
|**IBM_InterestRateShifts_AUD_interbank**|*Australia*||X||
|**IBM_InterestRateShifts_CAD_treasury**|*Canada*|X|||
|**IBM_InterestRateShifts_CAD_interbank**|*Canada*||X||
|**IBM_InterestRateShifts_CAD_OIS**|*Canada*|||X|
|**IBM_InterestRateShifts_CHF_treasury**|*Switzerland*|X|||
|**IBM_InterestRateShifts_CHF_interbank**|*Switzerland*||X||
|**IBM_InterestRateShifts_CHF_OIS**|*Switzerland*|||X|
|**IBM_InterestRateShifts_CNY_treasury**|*China*|X|||
|**IBM_InterestRateShifts_CNY_interbank**|*China*||X||
|**IBM_InterestRateShifts_EUR_treasury**|*Euro-Zone*|X|||
|**IBM_InterestRateShifts_EUR_interbank**|*Euro-Zone*||X||
|**IBM_InterestRateShifts_EUR_OIS**|*Euro-Zone*|||X|
|**IBM_InterestRateShifts_GBP_treasury**|*United Kingdom*|X|||
|**IBM_InterestRateShifts_GBP_interbank**|*United Kingdom*||X||
|**IBM_InterestRateShifts_GBP_OIS**|*United Kingdom*|||X|
|**IBM_InterestRateShifts_HKD_treasury**|*Hong Kong*|X|||
|**IBM_InterestRateShifts_HKD_interbank**|*Hong Kong*||X||
|**IBM_InterestRateShifts_JPY_treasury**|*Japan*|X|||
|**IBM_InterestRateShifts_JPY_interbank**|*Japan*||X||
|**IBM_InterestRateShifts_JPY_OIS**|*Japan*|||X|
|**IBM_InterestRateShifts_SGD_treasury**|*Singapore*|X|||
|**IBM_InterestRateShifts_SGD_interbank**|*Singapore*||X||
|**IBM_InterestRateShifts_USD_treasury**|*United States*|X|||
|**IBM_InterestRateShifts_USD_interbank**|*United States*||X||
|**IBM_InterestRateShifts_USD_OIS**|*United States*|||X|


## Credit spread standard shift scenarios
{: #cs}

Each credit spread standard shift scenario set includes the following standard shifts:

* **Parallel +100bps** - *A 100 basis point absolute increase to each term on the credit spread curve*
* **Parallel -100bps** - *A 100 basis point absolute decrease to each term on the credit spread curve*
* **0bp shift** - *A baseline scenario with no shift to credit spread curves*

Credit Curves are currently industry specific. All corporate fixed-income instruments with credit risk will be assigned a credit curve based on the industry sector of the issuer and the credit rating of the issuer. 
The following industry-specific credit spread curves have support for standard shift scenarios:

|Scenario Set Name|Industry Sector|AAA|AA|A|BBB|BB|B|CCC
|------------|----------|-|-|-|-|-|-|-|
|**IBM_CreditSpreadShifts_All**|*All Supported Curves*|X|X|X|X|X|X|X|
|**IBM_CreditSpreadShifts_Benchmark**|*Benchmark*|X|X|X|X|X|X|X|
|**IBM_CreditSpreadShifts_Consumer_goods**|*Consumer Goods*|X|X|X|X|X|X|X|
|**IBM_CreditSpreadShifts_Energy**|*Energy*|X|X|X|X|X|X|X|
|**IBM_CreditSpreadShifts_Financials**|*Financials*|X|X|X|X|X|X|X|
|**IBM_CreditSpreadShifts_Industrials**|*Industrials*|X|X|X|X|X|X|X|
|**IBM_CreditSpreadShifts_Insurance**|*Insurance*|X|X|X|X|X|X|X|
|**IBM_CreditSpreadShifts_Services**|*Services*|X|X|X|X|X|X|X|
|**IBM_CreditSpreadShifts_Telecommunications**|*Telecommunications*|X|X|X|X|X|X|X|
|**IBM_CreditSpreadShifts_Transportation**|*Transportation*|X|X|X|X|X|X|X|
|**IBM_CreditSpreadShifts_Utilities**|*Utilities*|X|X|X|X|X|X|X|


## Foreign exchange (FX) standard shift scenarios
{: #fx}

Each FX standard shift scenario set includes the following standard shifts:

* **USD Appreciates 10% with respect to &lt;XYZ&gt;** - *A 10% increase in the value of USD*
* **Parallel -100bps** - *A 100 basis point absolute decrease to each term on the credit spread curve*
* **0bp shift** - *A baseline scenario with no shift to credit spread curves*

In all cases, USD is assumed to be the base currency. The following foreign exchange standard shift scenarios are supported:

|Scenario Set Name|Domestic Currency|Domestic Currency Name|Foreign Currency|Foreign Currency Name
|------------|----------|------------|------------|------------|
|**IBM_FXShifts_AllCurrencies**|USD|US Dollar|*All Currencies*|*All Currencies*|
|**IBM_FXShifts_AUD_to_USD**|USD|US Dollar|AUD|Australian Dollar|
|**IBM_FXShifts_CAD_to_USD**|USD|US Dollar|CAD|Canadian Dollar|
|**IBM_FXShifts_CHF_to_USD**|USD|US Dollar|CHF|Swiss Franc|
|**IBM_FXShifts_CNY_to_USD**|USD|US Dollar|CNY|Chinese Yuan|
|**IBM_FXShifts_EUR_to_USD**|USD|US Dollar|EUR|Euro|
|**IBM_FXShifts_GBP_to_USD**|USD|US Dollar|GBP|Pound Sterling|
|**IBM_FXShifts_HKD_to_USD**|USD|US Dollar|HKD|Hong Kong Dollar|
|**IBM_FXShifts_JPY_to_USD**|USD|US Dollar|JPY|Japanese Yen|
|**IBM_FXShifts_SGD_to_USD**|USD|US Dollar|SGD|Singapore Dollar|
