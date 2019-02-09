---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-08"

---
<!--{:new_window: target="_blank"}-->
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

# Getting started with {{site.data.keyword.siminstruanalshort}}
{: #getting_started_siminstruanalshort}

The {{site.data.keyword.sia_full}} service leverages IBM Algorithmics' sophisticated financial models to price and compute analytics on financial securities.
{:shortdesc}

The service supports the computation of securities
* In current market conditions
* Over historical market conditions
* Under an alternate set of market conditions, often referred to as a 'stress test' or 'scenario'


With 30 years of financial engineering expertise, the pricing models of IBM Algorithmics are trusted by the world's largest financial institutions to meet their risk, performance, and regulatory needs.

The {{site.data.keyword.siminstruanalshort}} service supports the computation of the theoretical or market-calibrated valuation, and all relevant associated analytics, for investment securities such as equities, fixed income, and derivatives over an alternate set of market conditions.


## Connecting to {{site.data.keyword.mfd_full_notm}}
You need to set up {{site.data.keyword.sia_full}} to connect to the {{site.data.keyword.mfd_full}}.

The {{site.data.keyword.mfd_full_notm}} provides access to financial market data required when you're working with
the financial models that are used in the {{site.data.keyword.sia_full_notm}}.

When you subscribe to the {{site.data.keyword.mfd_full_notm}}, {{site.data.keyword.sia_full_notm}}
retrieves data on your behalf. You don't interact with the {{site.data.keyword.mfd_full_notm}}
service directly. The {{site.data.keyword.mfd_full_notm}} supplies all of the data that is required to process your request to the
{{site.data.keyword.sia_full_notm}}.

The market data that is used in calculations are provided by the third-party market data provider
that is associated with the instance of {{site.data.keyword.mfd_full_notm}} with which you integrated.
To provision an instance of {{site.data.keyword.mfd_full_notm}} or to learn more about our third-party
data patterns, see the IBM Cloud catalog entry. <!-- Rob wants a link to the  IBM Cloud Catalog entry for MFD -->

For more information about the {{site.data.keyword.mfd_full_notm}}, see the [{{site.data.keyword.mfd_short}} documentation](/docs/services/managed-financial-data/index.html).
<!--For more information about the {{site.data.keyword.mfd_full_notm}}, see the [{{site.data.keyword.mfd_short}} documentation](/docs/services/managed-financial-data?topic=managed-financial-data-getting_started_mfd_short#getting_started_mfd_short).-->


Before you call the {{site.data.keyword.siminstruanalshort}} service, do the following tasks:

1. Create instances of {{site.data.keyword.siminstruanalshort}} and {{site.data.keyword.mfd_short}} service
2. Assign access policies to the users of {{site.data.keyword.siminstruanalshort}} and {{site.data.keyword.mfd_short}}
3. Authorize {{site.data.keyword.siminstruanalshort}} to use {{site.data.keyword.mfd_short}}
4. Provide the UUID instance ID for {{site.data.keyword.mfd_short}} to {{site.data.keyword.siminstruanalshort}}


## Creating service instances and getting your credentials
{: #creating_instances}

Create the service instances for {{site.data.keyword.mfd_short}} and then {{site.data.keyword.siminstruanalshort}}.

### Creating the {{site.data.keyword.mfd_short}} service instance

1. Create an instance of the {{site.data.keyword.mfd_short}} service.
2. Review the {{site.data.keyword.mfd_short}} service instance access credentials, similar to the following example:

```
{
  "apikey": "<api-key>",
  "uuid":<uuid>,
  "url:": "<service-url>"
}
```
{:codeblock}

In a later step, you'll copy the UUID for {{site.data.keyword.mfd_short}} service instance to connect it with an instance of the {{site.data.keyword.siminstruanalshort}} service.
{:tip}

### Creating the {{site.data.keyword.siminstruanalshort}} service instance

1. Create an instance of the {{site.data.keyword.siminstruanalshort}} service.
2. Review the {{site.data.keyword.siminstruanalshort}} service instance access credentials, similar to the following example:

```
{
  "apikey": "<api-key>",
  "uuid":"<uuid>",
  "url:": "<service-url>"
}
```
{:codeblock}


## Assigning access policies to users of {{site.data.keyword.siminstruanalshort}} and {{site.data.keyword.mfd_short}}
{: #assigning_access_policies}


Before you create instances of the services {{site.data.keyword.siminstruanalshort}} and {{site.data.keyword.mfd_short}}, assign access policies to the users of both services.

In this case, the steps focus on assigning an access policy to your user name.

1. In the application catalog, open the service.
2. On the service dashboard, select **Manage** > **Access (IAM)**.
3. Click **Users** and then click the hyperlink for your user name. **Tip**: If you're managing several users, you can add users to an access group and assign the access policy to the group.
4. Click **Access policies**.
5. Click **Assign access** and then click **Assign access to resources**.
6. Enter the name of your service and select the service.
7. Under "Assign service access roles", check `Reader` and then click **Assign**.

Reader access is all that you require to use {{site.data.keyword.siminstruanalshort}} and {{site.data.keyword.mfd_short}}.
The assigned access policy applies to all the resources of the service.




## Authorizing {{site.data.keyword.siminstruanalshort}} to use {{site.data.keyword.mfd_short}}
{: #authorizing_sia_for_mfd}

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

## Providing the Instance ID (UUID) for {{site.data.keyword.mfd_short}} to {{site.data.keyword.siminstruanalshort}}
{: #providing_api_key}


Ensure that the instance of {{site.data.keyword.siminstruanalshort}}, which you identified as the source service instance, has the API key for the {{site.data.keyword.mfd_short}} service instance.

1. From the Dashboard's view of your applications, select the {{site.data.keyword.siminstruanalshort}} service instance and click **Manage**.
2. In the field **Enter MFD UUID instance ID**, paste the UUID from the {{site.data.keyword.mfd_short}} service instance and click **Submit**.

You can find the MFD UUID value on the {{site.data.keyword.mfd_short}} **Manage** panel.
{:note}

## Calling the service
{: #calling_service}

You must install cURL before you can use the service.

To call the service, replace `api-key` with your service key.

The following example demonstrates the calculation of analytics on a financial security, which you specify by using an instrument identifier, under current market conditions:

```
curl -X GET -H "Authorization-api-key : <api-key>"  -H "Authorization-instance-id : <uuid>" -H "Content-Type:application/json" https://us-south.sia.cloud.ibm.com/v2/mtm/<ID_type>?ids=<id-of-instrument>
```
{:codeblock}

where `ID_type` is one of `ric`, `isin`, or  `sedol`.

See [Request examples](/docs/services/simulated-instrument-analytics/examples.html) for a set of more detailed examples.
<!--See [Request examples](/docs/services/simulated-instrument-analytics?topic=simulated-instrument-analytics-request-examples) for a set of more detailed examples.-->



### Troubleshooting the connection between {{site.data.keyword.mfd_short}} and {{site.data.keyword.siminstruanalshort}}
{: #troubleshoot_connection}

When you connect {{site.data.keyword.mfd_short}} to {{site.data.keyword.siminstruanalshort}}, you might need to troubleshoot problems with authentication and authorization.

* When the API key for the {{site.data.keyword.siminstruanalshort}} service is incorrect, you encounter an authentication issue.
* When the API key for the {{site.data.keyword.siminstruanalshort}} service is correct but the UUID key for {{site.data.keyword.mfd_short}} that you provided to the {{site.data.keyword.siminstruanalshort}} service instance is incorrect, {{site.data.keyword.siminstruanalshort}} connects but it does not connect to {{site.data.keyword.mfd_short}} properly.
* When the API key for the {{site.data.keyword.siminstruanalshort}} service is correct and the UUID for {{site.data.keyword.mfd_short}} that you provided to the {{site.data.keyword.siminstruanalshort}} service instance is also correct, but you aren't using the service instance of {{site.data.keyword.mfd_short}} that was identified as the target, {{site.data.keyword.siminstruanalshort}} connects but you encounter an authorization error.
