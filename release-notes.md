---

copyright:
  years: 2018
lastupdated: "2018-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:faq: data-hd-content-type='faq'}

<!-- Link definitions -->

<!-- based on https://github.ibm.com/Bluemix-Docs/visual-recognition/blob/staging/release-notes.md -->


# Release notes

The following new features and changes to the service are available.
{: shortdesc}

<!--
## Beta features
{: #beta}

{{site.data.keyword.IBM_notm}} releases services, features, and language support for your evaluation that are classified as beta. These features might be unstable, might change frequently, and might be discontinued with short notice. Beta features also might not provide the same level of performance or compatibility that generally available features provide and are not intended for use in a production environment. Beta features are supported only on [developerWorks Answers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/topics/visual-recognition.html){: new_window}.
-->

## Changes
{: #changelog}

The following new features and changes to the service are available.

### 30 October 2018
{: #30october2018}

- **Integration with {{site.data.keyword.mfd_full_notm}}** 
    - The {{site.data.keyword.sia_full}} service integrates with {{site.data.keyword.mfd_full}}. 
      If you subscribe to the {{site.data.keyword.mfd_short}} service, when you run {{site.data.keyword.siminstruanalshort}} requests, you can then retrieve financial data from the {{site.data.keyword.mfd_full_notm}} service.
      See [Connecting to {{site.data.keyword.siminstruanalshort}}](/docs/services/simulated-instrument-analytics/connect_services.html) for more information.


- **Combined services**
    - The experimental services {{site.data.keyword.instranalshort}}, {{site.data.keyword.simhistinstruanalshort}}, and {{site.data.keyword.hisinstranalshort}} have been combined into the {{site.data.keyword.siminstruanalshort}} service. Now all operations that you previously performed using the endpoints are now supported in {{site.data.keyword.siminstruanalshort}}. The services {{site.data.keyword.instranalshort}}, {{site.data.keyword.simhistinstruanalshort}}, and {{site.data.keyword.hisinstranalshort}} are now deprecated.
    - The service URL for {{site.data.keyword.siminstruanalshort}} is now ```https://sia.cloud.ibm.com```
    - The endpoints for these services are now ```v2/simulate``` and ```v2/mtm```

- **Support for instruments**
    - {{site.data.keyword.siminstruanalshort}} supports instruments of the following `ID_TYPE` values:
        -  ```isin``` (International Securities Identification Number)
        -  ```ric``` (Reuters Instrument Code)
        -  ```sedol``` (Stock Exchange Daily Official List)
        -  ```ticker``` (ticker symbol)

- **Support for CSV-format responses**
    - You can return responses in CSV format. Use the query parameter ```response_format``` and set it as follows: ```response_format=CSV```
