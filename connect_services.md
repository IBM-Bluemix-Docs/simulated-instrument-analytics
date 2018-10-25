---

copyright:
  years: 2018
lastupdated: "2018-10-24"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:download: .download}

# Connecting to {{site.data.keyword.mfd_short}}
{: #connecting_to_mfd_short}

The {{site.data.keyword.sia_full_notm}} can be set up to connect to the {{site.data.keyword.mfd_full_notm}}.
{:shortdesc}

The {{site.data.keyword.mfd_full_notm}} provides access to financial market data required when you're working with 
the financial models that are used in the {{site.data.keyword.sia_full_notm}}.

When you subscribe to the {{site.data.keyword.mfd_full_notm}}, you can have {{site.data.keyword.sia_full_notm}} 
retrieve data on your behalf. In this case, as the user, you don't interact with the {{site.data.keyword.mfd_full_notm}} 
service directly. The {{site.data.keyword.mfd_full_notm}} supplies all of the data that is required to process your request to the 
{{site.data.keyword.sia_full_notm}}.

The market data that is used in calculations are provided by the third-party market data provider 
that is associated with the instance of {{site.data.keyword.mfd_full_notm}} with which you integrated. 
To provision an instance of {{site.data.keyword.mfd_full_notm}} or to learn more about our third-party 
data patterns, see the IBM Cloud Catalog entry. <!-- Rob wants a link to the  IBM Cloud Catalog entry for MFD -->


## Before you begin

You must obtain access to the {{site.data.keyword.siminstruanalshort}} service and the {{site.data.keyword.mfd_short}} service. 
To use the {{site.data.keyword.siminstruanalshort}} REST API, make sure that you understand the basics of RESTful web services and JSON representations.

<!-- You must install cURL before you can use the service. -->

## Getting your credentials

1. Create an instance of the {{site.data.keyword.mfd_short}} service.
2. Review the {{site.data.keyword.mfd_short}} service instance access credentials, similar to the following example:

```
{
  "apikey": "<api-key>",
  "url:": "<service-url>"
}
```
{:codeblock}

In a later step, you will copy the API key for {{site.data.keyword.mfd_short}} service instance to connect it with an instance of the {{site.data.keyword.siminstruanalshort}} service.

3. Create an instance of the {{site.data.keyword.siminstruanalshort}} service.
4. Review the {{site.data.keyword.siminstruanalshort}} service instance access credentials, similar to the following example:

```
{
  "apikey": "<api-key>",
  "url:": "<service-url>"
}
```
{:codeblock}

## Authorizing {{site.data.keyword.siminstruanalshort}} to use {{site.data.keyword.mfd_short}} 

In this case, you're authorizing a single instance of {{site.data.keyword.siminstruanalshort}} to work with a specific instance of {{site.data.keyword.mfd_short}}.

1. On the service dashboard, select **Manage** > **Access (IAM)**.
2. Click **Authorizations**.
3. Click **Create**.
4. For the Source service, select `Simulated Instruments Analytics`.
5. For the Source service instance, select the instance of {{site.data.keyword.siminstruanalshort}} from the list that you created in the previous steps.
6. For the Target service, select `Managed Financial Data`.
7. For the Target service instance, select the instance of {{site.data.keyword.mfd_short}} from the list that you created in the previous steps.
8. Under Assign service access roles, check **Reader**.
9. Click **Authorize**. 

## Provide the API key {{site.data.keyword.mfd_short}} to {{site.data.keyword.siminstruanalshort}}

Ensure that the instance of {{site.data.keyword.siminstruanalshort}}, which you identified as the source service instance, has the API key for the {{site.data.keyword.mfd_short}} service instance. 

1. From the Dashboard's view of your applications, select the {{site.data.keyword.siminstruanalshort}} service instance and click **Manage**.
2. In the field **Enter MFD api key**, paste the API key from the {{site.data.keyword.mfd_short}} service instance and click **Submit**.



## Calling the Service

To call the service, replace `api-key` with the service key.

The following example demonstrates the calculation of analytics on a financial security, which you specify by using an instrument identifier, under current market conditions:

```
curl -X GET -H "X-ibm-api-key: <api-key>" -H https://sia.cloud.ibm.com/v2/mtm/<id-of-instrument>
```
{:codeblock}

## Troubleshooting

When you connect {{site.data.keyword.mfd_short}} to {{site.data.keyword.siminstruanalshort}}, you may need to troubleshoot problems with authentication and authorization.

* When the API key for the {{site.data.keyword.siminstruanalshort}} service is incorrect, you encounter an authentication issue.
* When the API key for the {{site.data.keyword.siminstruanalshort}} service is correct but the API key for {{site.data.keyword.mfd_short}} that you provided to the {{site.data.keyword.siminstruanalshort}} service instance is incorrect, {{site.data.keyword.siminstruanalshort}} connects but it does not connect to {{site.data.keyword.mfd_short}} properly.
* When the API key for the {{site.data.keyword.siminstruanalshort}} service is correct and the API key for {{site.data.keyword.mfd_short}} that you provided to the {{site.data.keyword.siminstruanalshort}} service instance is also correct, but you aren't using the service instance of {{site.data.keyword.mfd_short}} that was identified as the target, {{site.data.keyword.siminstruanalshort}} connects but you encounter an authorization error.