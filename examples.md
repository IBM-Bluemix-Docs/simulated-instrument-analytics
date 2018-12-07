---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-03"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:download: .download}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:faq: data-hd-content-type='faq'}

# Request examples

These sample requests supplement the simple example provided in [Getting started with {{site.data.keyword.siminstruanalshort}}](/docs/services/simulated-instrument-analytics/index.html).



## Example 1: Computing current analytics on multiple instruments
{: #t0_pricing_no_scenarios}
<!--Postman example name is "t0 instrument pricing" -->


The following example demonstrates a call to get current (time zero or t0) analytics on a financial security by using a GET request:

```
curl -X GET -H "X-ibm-api-key: <api-key>" -H "Content-Type:application/json" https://us-south.sia.cloud.ibm.com/v2/mtm/isin?ids=<id-of-instrument-1>,<id-of-instrument-2>

```
{:codeblock}


The following example shows a response to a successful request:

```
{
    "results": [
        {
            "Currency": "USD",
            "Simulation Date": "2018-10-10",
            "ID": "<id-of-instrument-1>",
            "Value": "96.168075",
            "Name": "NAB    1.875 07/12/21 MTN"
        },
        {
            "Currency": "USD",
            "Simulation Date": "2018-10-10",
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
curl -X POST https://us-south.sia.cloud.ibm.com/v2/simulate -H "X-ibm-api-key : <api-key>" -H "Content-Type:application/json"  -d '{ "id-list": [{ "id": "IBM", "type":"ric" }],"analytics" : ["Price","Delta"]}'
```
{:codeblock}

**Note**: In this case, we are passing multiple arrays in the request body (for example, `analytics` _and_ `id-list`) to the service.

The following example shows a response to a successful request:

```
{
    "results": [
        {
            "Simulation Date": "2018-10-10",
            "Name": "INTERNATIONAL BUSINESS MACHINES ORD",
            "Price": "147.24",
            "Currency": "USD",
            "Delta": "0",
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
curl -X POST https://us-south.sia.cloud.ibm.com/v2/simulate -H "X-ibm-api-key: <api-key>" -H "Content-Type:application/json"  -d '{ "id-list": [{ "id": "IBM", "type":"ric" }, { "id": "US59022CAJ27", "type":"isin" }], "analytics" : ["Dirty Price","Clean Price","Effective Duration"] }'
```
{:codeblock}

The following example shows a response to a successful request for multiple instruments and multiple analytics:
```
{
    "results": [
        {
            "Simulation Date": "2018-10-10",
            "Name": "BAC    6.110 01/29/37",
            "Clean Price": "112.8938",
            "Currency": "USD",
            "Effective Duration": "11.52261095",
            "Dirty Price": "114.09882778",
            "ID": "US59022CAJ27"
        },
        {
            "Simulation Date": "2018-10-10",
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
curl -X POST https://us-south.sia.cloud.ibm.com/v2/simulate -H "X-ibm-api-key: <api-key>" -H "Content-Type:application/json"  -d { "id-list": [{ "id": "IBM", "type":"ric" }, { "id": "US59022CAJ27", "type":"isin" }], "valuation-date" : "2018-10-10"}'
```
{:codeblock}


The following example shows a response to a successful request:

```
{
    "results": [
        {
            "Currency": "USD",
            "Simulation Date": "2018-10-10",
            "ID": "US59022CAJ27",
            "Value": "116.01114444",
            "Name": "BAC    6.110 01/29/37"
        },
        {
            "Currency": "USD",
            "Simulation Date": "2018-10-10",
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
POST request and specify multiple days in the future by using the `simulation-days` field.
To use this example to test the service, replace `api-key` with your service key, specify one or more instruments in the `id-list`, specify one or more analytics, specify a scenario set name, and specify multiple `simulation-days`.
<!--To create a scenario file, you can prepare one yourself or use the [{{site.data.keyword.predmarketscenario_short}} service](/docs/services/PredictiveMarketScenarios/index.html).-->

```
curl -X POST https://us-south.sia.cloud.ibm.com/v2/simulate -H "X-ibm-api-key: <api-key>" -H "Content-Type:application/json" -d '{ "id-list": [{ "id": "IBM", "type":"ric" }],  "analytics" : ["Dirty Price","Clean Price", "Effective Duration"],"ibm-scenario-set-name" : "IBM_EquityIndexShifts_AllCurves", "simulation-days" : [0,6,13,18,30] }'
```
{:codeblock}

where each one of the `simulation-days` values is an array of future simulation times relative to the `valuation-date`.

The following example shows a response to a successful request:

```
{
    "results": [
        {
            "Simulation Date": "2018-10-10",
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
            "Simulation Date": "2018-10-16",
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
            "Simulation Date": "2018-10-23",
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
            "Simulation Date": "2018-10-28",
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
            "Simulation Date": "2018-11-09",
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
            "Simulation Date": "2018-10-10",
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
            "Simulation Date": "2018-10-16",
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
            "Simulation Date": "2018-10-23",
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
            "Simulation Date": "2018-10-28",
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
            "Simulation Date": "2018-11-09",
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
            "Simulation Date": "2018-10-10",
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
            "Simulation Date": "2018-10-16",
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
            "Simulation Date": "2018-10-23",
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
            "Simulation Date": "2018-10-28",
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
            "Simulation Date": "2018-11-09",
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

<!-- **Note**: The "BASE" scenario is the baseline scenario with no alterations to the initial set of assumptions. Any profit and loss or return analytics are computed against the values that are computed in the BASE scenario. -->

## Example 4: Calculating historical analytics under a stress test
{: #historical_pricing_with_scenarios}
<!--Postman example name is "historical scenario pricing" -->


To observe how an instrument might behave under an alternate set of market conditions (a "stress test") *for a date in the past*, you can submit POST requests and specify a `valuation-date` (in YYYY-MM-DD format) and multiple `simulation-days`. This type of request is commonly issued to generate end-of-month or end-of-quarter reports, or to perform backtesting analysis.

To use this example to test the service, replace `api-key` with your service key, specify one or more instrument identifiers, specify one or more analytics, specify a scenario set name, and specify the `valuation-date` and multiple `simulation-days` (as numbers).

<!--
To create a scenario file, you can prepare one yourself or use the [{{site.data.keyword.predmarketscenario_short}} service](/docs/services/PredictiveMarketScenarios/index.html).
-->

```
curl -X POST https://us-south.sia.cloud.ibm.com/v2/simulate -H "X-ibm-api-key: <api-key>" -H "Content-Type:application/json" -d '{ "id-list": [{ "id": "IBM", "type":"ric" }],  "analytics" : ["Dirty Price","Clean Price","Effective Duration"], "ibm-scenario-set-name" : "IBM_EquityIndexShifts_AllCurves", "valuation-date" : "2018-10-10",  "simulation-days" : [0,13,30] }'
```
{:codeblock}


The following example shows a response to a successful request:

```
{
    "results": [
        {
            "Simulation Date": "2018-10-10",
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
            "Simulation Date": "2018-10-23",
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
            "Simulation Date": "2018-11-09",
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
            "Simulation Date": "2018-10-10",
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
            "Simulation Date": "2018-10-23",
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
            "Simulation Date": "2018-11-09",
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
            "Simulation Date": "2018-10-10",
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
            "Simulation Date": "2018-10-23",
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
            "Simulation Date": "2018-11-09",
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

