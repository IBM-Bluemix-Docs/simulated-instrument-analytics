---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-24"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:download: .download}

# Getting started with {{site.data.keyword.siminstruanalshort}}
{: #getting_started_siminstruanalshort}

The {{site.data.keyword.siminstruanalshort}} service leverages IBM Algorithmics' sophisticated financial models to price and compute analytics on financial securities.
{:shortdesc}

The service supports the computation of securities
* In current market conditions
* Over historical market conditions
* Under an alternate set of market conditions, often referred to as a 'stress test' or 'scenario'


With 30 years of financial engineering expertise, the pricing models of IBM Algorithmics are trusted by the world's largest financial institutions to meet their risk, performance, and regulatory needs.

The {{site.data.keyword.siminstruanalshort}} service supports the computation of the theoretical or market-calibrated valuation, and all relevant associated analytics, for investment securities such as equities, fixed income, and derivatives over an alternate set of market conditions.

## Before you begin

You must obtain access to the {{site.data.keyword.siminstruanalshort}} service and call API methods. To use the {{site.data.keyword.siminstruanalshort}} REST API, make sure that you understand the basics of RESTful web services and JSON representations.

You must install cURL before you can use the service.

**Important:** If you plan on using {{site.data.keyword.siminstruanalshort}} with the 
{{site.data.keyword.mfd_full_notm}} service, see [Connecting to {{site.data.keyword.mfd_short}}](/docs/services/simulated-instrument-analytics/connect_services.html) for more information on what steps you need to take.


## Getting your credentials

1. Create an instance of the service.
2. Review the service instance access credentials, similar to the following example:

```
{
  "accessToken": "<api-key>",
  "uri": "https://sia.cloud.ibm.com"
}
```
{:codeblock}

## Calling the Service

To call the service, replace `api-key` with your service key.

The following example demonstrates the calculation of analytics on a financial security, which you specify by using an instrument identifier, under current market conditions:

```
curl -X GET -H "X-ibm-api-key : <api-key>" -H https://sia.cloud.ibm.com/api/v2/mtm/<ID_type>?ids:<id-of-instrument>
```
{:codeblock}

where `ID_type` is one of `ric`, `isin`, `sedol`, or `ticker`.

## Example 1: Computing current analytics on multiple instruments
{: #t0_pricing_no_scenarios}
<!--Postman example name is "t0 instrument pricing" -->


The following example demonstrates a call to get current (time zero or t0) analytics on a financial security by using a GET request:

```
curl -X GET -H "X-ibm-api-key: <api-key>" https://sia.cloud.ibm.com/v2/mtm/isin?ids=<id-of-instrument-1>,<id-of-instrument-2>

```
{:codeblock}


The following example shows a response to a successful request:

```
{
    "results": [
        {
            "Currency": "USD",
            "Simulation Date": "2018/10/03",
            "ID": "<id-of-instrument-1>",
            "Value": "96.168075",
            "Name": "NAB    1.875 07/12/21 MTN"
        },
        {
            "Currency": "USD",
            "Simulation Date": "2018/10/03",
            "ID": "<id-of-instrument-2>",
            "Value": "98.65441111",
            "Name": "OMC    3.650 11/01/24 '24"
        }
    ]
}
```
{:codeblock}

### Computing multiple analytics on an instrument


Perhaps your use case requires multiple analytics to be computed on one or more instruments. To do so, use a POST request. Replace `api-key` with your service key.
The following example shows a request for the computation of multiple analytics on a single financial instrument, which is specified by its instrument identifier:

```
curl -X POST https://sia.cloud.ibm.com/v2/simulate -H "X-ibm-api-key : <api-key>" -H 'Content-Type: application/json'  -H 'cache-control: no-cache' -d '{ "id-list": [{ "id": "IBM", "type":"ric" }],"analytics" : "Dirty Price,Clean Price,Effective Duration,Dirty Price"}'
```
{:codeblock}

**Note**: In this case, we are passing multiple arrays in the request body (for example, `analytics` _and_ `id-list`) to the service.

The following example shows a response to a successful request:

```
{
    "results": [
        {
            "Simulation Date": "2018/10/10",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "147.24",
            "Currency": "USD",
            "Effective Duration": "0",
            "Dirty Price": "147.24",
            "ID": "IBM"
        }
    ]
}
```
{:codeblock}

### Computing multiple analytics on multiple instruments
<!--Postman example is "t0 multiple instrument pricing" -->

To request one or more analytics across multiple instruments in a single request, you must enhance the POST request to include a list of instruments.
```
curl -X POST https://sia.cloud.ibm.com/v2/simulate -H "X-ibm-api-key: <api-key>" -H 'Content-Type: application/json'  -H 'cache-control: no-cache'  -d '{ "id-list": [{ "id": "IBM", "type":"ric" }, { "id": "US59022CAJ27", "type":"isin" }], "analytics" : "Dirty Price,Clean Price,Effective Duration,Dirty Price" }'
```
{:codeblock}

The following example shows a response to a successful request for multiple instruments and multiple analytics:
```
{
    "results": [
        {
            "Simulation Date": "2018/10/10",
            "Name": "BAC    6.110 01/29/37",
            "Clean Price": "112.8938",
            "Currency": "USD",
            "Effective Duration": "11.52261095",
            "Dirty Price": "114.09882778",
            "ID": "US59022CAJ27"
        },
        {
            "Simulation Date": "2018/10/10",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "147.24",
            "Currency": "USD",
            "Effective Duration": "0",
            "Dirty Price": "147.24",
            "ID": "IBM"
        }
    ]
}
```
{:codeblock}

## Example 2: Computing historical analytics on instruments
{: #historical_pricing_no_scenarios}

To calculate analytics for dates in the past, issue a POST request.

### Computing historical analytics for one or more instruments
<!--Postman example name is "historical multiple instrument pricing" -->

You can submit a request to the service to compute historical analytics for one or more instruments 
and multiple analytics by issuing a POST request.
To use this example to test the service, replace `api-key`, specify one or more instrument identifiers, and specify the `valuation-date` (in YYYY-MM-DD format) in the POST request.

```
curl -X POST https://sia.cloud.ibm.com/v2/simulate -H "X-ibm-api-key: <api-key>" -H 'Content-Type: application/json'  -H 'cache-control: no-cache'  -d { "id-list": [{ "id": "IBM", "type":"ric" }, { "id": "US59022CAJ27", "type":"isin" }], "valuation-date" : "2018-08-01"}'
```
{:codeblock}


The following example shows a response to a successful request:

```
{
    "results": [
        {
            "Currency": "USD",
            "Simulation Date": "2018/08/01",
            "ID": "US59022CAJ27",
            "Value": "116.01114444",
            "Name": "BAC    6.110 01/29/37"
        },
        {
            "Currency": "USD",
            "Simulation Date": "2018/08/01",
            "ID": "IBM",
            "Value": "143.5",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD"
        }
    ]
}
```
{:codeblock}

## Example 3: Calculating analytics under a stress test
{: #t0_pricing_with_scenarios}
<!--Postman example name is "t0 scenario pricing" -->


To observe how an instrument might behave under an alternate set of market conditions (a "stress test"), you can submit a 
POST request and specify multiple dates in the `simulation_days` field.
To use this example to test the service, replace `api-key` with your service key, specify one or more instruments in the `id-list`, specify one or more analytics, specify a scenario set name, and specify multiple `simulation_days`.
<!--To create a scenario file, you can prepare one yourself or use the [{{site.data.keyword.predmarketscenario_short}} service](/docs/services/PredictiveMarketScenarios/index.html).-->

```
curl -X POST https://sia.cloud.ibm.com/v2/simulate -H "X-ibm-api-key: <api-key>" -H 'Content-Type: application/json'  -H 'cache-control: no-cache' -d '{ "id-list": [{ "id": "IBM", "type":"ric" }],  "analytics" : "Dirty Price,Clean Price, Effective Duration,Scenario Set Name, Scenario Name", "ibm-scenario-set-name" : "IBM_EquityIndexShifts_AllCurves", "simulation-days" : "0,6,13,18,30" }'
```
{:codeblock}

where each one of the `simulation_days` values as an array of trigger times.

The following example shows a response to a successful request:

```
{
    "results": [
        {
            "Simulation Date": "2018/10/10",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "162.12517071",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes up 10%",
            "Effective Duration": "0",
            "Dirty Price": "162.12517071",
            "Simulation Days": "Day 0",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/10/16",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "177.7155609",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes up 10%",
            "Effective Duration": "0",
            "Dirty Price": "177.7155609",
            "Simulation Days": "Day 6",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/10/23",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "183.20087854",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes up 10%",
            "Effective Duration": "0",
            "Dirty Price": "183.20087854",
            "Simulation Days": "Day 13",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/10/28",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "185.08620297",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes up 10%",
            "Effective Duration": "0",
            "Dirty Price": "185.08620297",
            "Simulation Days": "Day 18",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/11/09",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "183.5082429",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes up 10%",
            "Effective Duration": "0",
            "Dirty Price": "183.5082429",
            "Simulation Days": "Day 30",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/10/10",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "147.24",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes with no changes",
            "Effective Duration": "0",
            "Dirty Price": "147.24",
            "Simulation Days": "Day 0",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/10/16",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "147.24",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes with no changes",
            "Effective Duration": "0",
            "Dirty Price": "147.24",
            "Simulation Days": "Day 6",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/10/23",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "147.24",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes with no changes",
            "Effective Duration": "0",
            "Dirty Price": "147.24",
            "Simulation Days": "Day 13",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/10/28",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "147.24",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes with no changes",
            "Effective Duration": "0",
            "Dirty Price": "147.24",
            "Simulation Days": "Day 18",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/11/09",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "147.24",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes with no changes",
            "Effective Duration": "0",
            "Dirty Price": "147.24",
            "Simulation Days": "Day 30",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/10/10",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "130.97000969",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes down 10%",
            "Effective Duration": "0",
            "Dirty Price": "130.97000969",
            "Simulation Days": "Day 0",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/10/16",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "120.73811924",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes down 10%",
            "Effective Duration": "0",
            "Dirty Price": "120.73811924",
            "Simulation Days": "Day 6",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/10/23",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "113.75018057",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes down 10%",
            "Effective Duration": "0",
            "Dirty Price": "113.75018057",
            "Simulation Days": "Day 13",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/10/28",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "116.14304851",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes down 10%",
            "Effective Duration": "0",
            "Dirty Price": "116.14304851",
            "Simulation Days": "Day 18",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/11/09",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "118.78049806",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes down 10%",
            "Effective Duration": "0",
            "Dirty Price": "118.78049806",
            "Simulation Days": "Day 30",
            "ID": "IBM"
        }
    ]
}
```
{:codeblock}

<!-- **Note**: The "BASE" scenario is the baseline scenario with no alterations to the initial set of assumptions. Any P&L or return analytics are computed against the values that are computed in the BASE scenario. -->

## Example 4: Calculating historical analytics under a stress test
{: #historical_pricing_with_scenarios}
<!--Postman example name is "historical scenario pricing" -->


To observe how an instrument might behave under an alternate set of market conditions (a "stress test") *for a date in the past*, you can submit POST requests and specify a `valuation-date` (in YYYY-MM-DD format) and multiple `simulation_days`. This type of request is commonly issued to generate end-of-month or end-of-quarter reports, or to perform backtesting analysis.

To use this example to test the service, replace `api-key` with your service key, specify one or more instrument identifiers, specify one or more analytics, specify a scenario set name, and specify the `valuation-date` and multiple `simulation_days` (as numbers).

<!--
To create a scenario file, you can prepare one yourself or use the [{{site.data.keyword.predmarketscenario_short}} service](/docs/services/PredictiveMarketScenarios/index.html).
-->

```
curl -X POST https://sia.cloud.ibm.com/v2/simulate -H "X-ibm-api-key: <api-key>" -H 'Content-Type: application/json'  -H 'cache-control: no-cache' -d '{ "id-list": [{ "id": "IBM", "type":"ric" }],  "analytics" : "Dirty Price,Clean Price, Effective Duration", "ibm-scenario-set-name" : "IBM_EquityIndexShifts_AllCurves", "valuation-date" : "2018-08-01",  "simulation-days" : "0,13,30" }'
```
{:codeblock}


The following example shows a response to a successful request:

```
{
    "results": [
        {
            "Simulation Date": "2018/08/01",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "157.55270325",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes up 10%",
            "Effective Duration": "0",
            "Dirty Price": "157.55270325",
            "Simulation Days": "Day 0",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/08/14",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "171.81319378",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes up 10%",
            "Effective Duration": "0",
            "Dirty Price": "171.81319378",
            "Simulation Days": "Day 13",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/08/31",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "180.14843374",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes up 10%",
            "Effective Duration": "0",
            "Dirty Price": "180.14843374",
            "Simulation Days": "Day 30",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/08/01",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "143.5",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes with no changes",
            "Effective Duration": "0",
            "Dirty Price": "143.5",
            "Simulation Days": "Day 0",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/08/14",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "143.5",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes with no changes",
            "Effective Duration": "0",
            "Dirty Price": "143.5",
            "Simulation Days": "Day 13",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/08/31",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "143.5",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes with no changes",
            "Effective Duration": "0",
            "Dirty Price": "143.5",
            "Simulation Days": "Day 30",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/08/01",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "128.09257551",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes down 10%",
            "Effective Duration": "0",
            "Dirty Price": "128.09257551",
            "Simulation Days": "Day 0",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/08/14",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "120.12863488",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes down 10%",
            "Effective Duration": "0",
            "Dirty Price": "120.12863488",
            "Simulation Days": "Day 13",
            "ID": "IBM"
        },
        {
            "Simulation Date": "2018/08/31",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Clean Price": "109.47029497",
            "Scenario Set Name": "Shifts to all equity indexes",
            "Currency": "USD",
            "Scenario Name": "All equity indexes down 10%",
            "Effective Duration": "0",
            "Dirty Price": "109.47029497",
            "Simulation Days": "Day 30",
            "ID": "IBM"
        }
    ]
}
```
{:codeblock}


## Resources
{: #resources}

<!--
### Example scenario files

[curve_shifts_sample.csv](http://public.dhe.ibm.com/software/analytics/solutions/en/fintech/curve_shifts_sample.csv) is a scenario sample file representing different interest rate curve movements with both parallel and non-parallel shifts.

[stresstests_sample.csv](http://public.dhe.ibm.com/software/analytics/solutions/en/fintech/stresstests_sample.csv) is a scenario sample file representing a hypothetical flight to quality, whereby treasury curves fall, swap rates rise, and equities drop 10%.
-->
<!--
### Instruments

A list of instruments is available [here](http://public.dhe.ibm.com/software/analytics/solutions/en/fintech/Sample_Instrument_Universe.xlsx).
-->

### Field Name values

This table contains 'Field Name' values that you can pass to the API for the measures (analytics), and the asset classes (Fixed Income, Equity, or Derivative) that they apply to.

|Measure Name|Field Name|Fixed Income|Equity|Derivatives|
|------------|----------|------------|------|-----------|
|Accrued Interest|THEO/Accrued Interest|X| | |
|Clean Value|THEO/Price|X|X|X|
|Dirty Value|THEO/Value|X|X|X|
|Exposure|THEO/Exposure|X|X|X|
|Yield|THEO/Yield|X| | |
|Macaulay Duration|THEO/Macaulay Duration|X| |X|
|Adjusted Duration|THEO/Adjusted Duration|X| |X|
|Effective Duration|THEO/Effective Duration|X| |X|
|Spread Duration|THEO/Adjusted Duration2|X| |X|
|Effective Convexity|THEO/Effective Convexity|X| |X|
|Delta|THEO/Delta| | |X|
|Domestic Rho|THEO/Domestic Rho| | |X|
|Gamma|THEO/Gamma| | |X|
|Theta|THEO/Theta| | |X|
|Vega|THEO/Vega| | |X|
|P&amp;L|POS/Unrealized Profit and Loss Theoretical|X|X|X|
|Return|Theo/Value@REL(scen&time,%diff)|X|X|X|
{: caption="Table 1. {{site.data.keyword.siminstruanalshort}} field name values" caption-side="top"}

