---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-04"

keywords: financial risk, getting started

subcollection: simulated-instrument-analytics

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

## Assigning access policies to users of {{site.data.keyword.siminstruanalshort}} and {{site.data.keyword.mfd_short}}
{: #assigning_access_policies}


Before you create instances of the services {{site.data.keyword.siminstruanalshort}} and {{site.data.keyword.mfd_short}}, assign access policies to the users of both services.

In this case, the steps focus on assigning an access policy to your user name.


<!-- 1. In the application catalog, open the service. -->

1. On the service dashboard, select **Manage** > **Access (IAM)**.
1. Click **Users** and then click the hyperlink for your user name.

 If you're managing several users, you can add users to an access group and assign the access policy to the group.
{:tip}
1. Click **Access policies**.
1. Assign access to all instances of the {{site.data.keyword.mfd_short}} service.
 1. Click **Assign access** and then click **Assign access to resources**.
 1. Enter the name of the {{site.data.keyword.mfd_short}} service.
 1. Grant yourself access to all instances of the service.
 1. Under "Assign service access roles", check `Reader` and then click **Assign**.
1. Assign access to all instances of the  {{site.data.keyword.siminstruanalshort}} service.
 1. Click **Assign access** and then click **Assign access to resources**.
 1. Enter the name of the {{site.data.keyword.siminstruanalshort}} service.
 1.  Grant yourself access to all instances of the service.
 1. Under "Assign service access roles", check `Reader` and then click **Assign**.

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

For more information about the {{site.data.keyword.mfd_full_notm}}, see the [{{site.data.keyword.mfd_short}} documentation](/docs/services/managed-financial-data?topic=managed-financial-data-getting_started_mfd_short#getting_started_mfd_short).


Before you call the {{site.data.keyword.siminstruanalshort}} service, do the following tasks:

1. Create instances of the {{site.data.keyword.mfd_short}} service and the {{site.data.keyword.siminstruanalshort}} service.
2. Authorize {{site.data.keyword.siminstruanalshort}} to use {{site.data.keyword.mfd_short}}.
3. Provide the UUID instance ID for {{site.data.keyword.mfd_short}} to {{site.data.keyword.siminstruanalshort}}.


## Creating service instances and getting your credentials
{: #creating_instances}

Create the service instances for {{site.data.keyword.mfd_short}} and then {{site.data.keyword.siminstruanalshort}}.

### Creating the {{site.data.keyword.mfd_short}} service instance

1. Create an instance of the {{site.data.keyword.mfd_short}} service.
2. For the instance of the {{site.data.keyword.mfd_short}}  service, click **Manage**.
3. Copy the value of the **UUID**.

Record the UUID value. In a later step, you'll copy the UUID for the {{site.data.keyword.mfd_short}} service instance to connect it with an instance of the {{site.data.keyword.siminstruanalshort}} service.
{:tip}

### Creating the {{site.data.keyword.siminstruanalshort}} service instance

1. Create an instance of the {{site.data.keyword.siminstruanalshort}} service.
1. For the instance of the {{site.data.keyword.siminstruanalshort}} service, click **Manage**.
1. Paste the UUID value of the {{site.data.keyword.mfd_short}} service instance and click **Submit**.
1. In **Service credentials**, click **New credential** and **Add** a credential for the {{site.data.keyword.siminstruanalshort}} service instance.
1. Review the {{site.data.keyword.siminstruanalshort}} service instance credentials, which appear similar to the following example, and copy the value of the `apikey` and record it for future reference:

```
{
  "apikey": "<api-key>",
  "iam_apikey_description":"<iam-apikey-description>",
  "iam_apikey_name":"<iam-apikey-name>",
  "iam_role_crn":"<iam-role-crn>",
  "iam_serviceid_crn":"<iam-serviceid-crn>",
  "url:": "<service-url>"
}
```
{:codeblock}


## Authorizing {{site.data.keyword.siminstruanalshort}} to use {{site.data.keyword.mfd_short}}
{: #authorizing_sia_for_mfd}

In this case, you're authorizing a single instance of {{site.data.keyword.siminstruanalshort}} to work with a specific instance of {{site.data.keyword.mfd_short}}.

1. On the service dashboard, select **Manage** > **Access (IAM)**.
1. Click **Authorizations**.
1. Click **Create**.
1. For the Source service, select `Simulated Instruments Analytics API`.
1. For the Source service instance, select the instance of {{site.data.keyword.siminstruanalshort}} from the list that you created in the previous steps or leave the value empty to apply to any service of this type.
1. For the Target service, select `Managed Financial Data API`.
1. For the Target service instance, select the instance of {{site.data.keyword.mfd_short}} from the list that you created in the previous steps or leave the value empty to apply to any service of this type.
1. Under Assign service access roles, check **Reader**.
1. Click **Authorize**.

## Providing the Instance ID (UUID) for {{site.data.keyword.mfd_short}} to {{site.data.keyword.siminstruanalshort}}
{: #providing_api_key}


Ensure that the instance of {{site.data.keyword.siminstruanalshort}}, which you identified as the source service instance, has the API key for the {{site.data.keyword.mfd_short}} service instance.

1. From the Dashboard's view of your applications, select the {{site.data.keyword.siminstruanalshort}} service instance and click **Manage**.
1. In the field **Enter MFD UUID instance ID**, paste the UUID from the {{site.data.keyword.mfd_short}} service instance and click **Submit**.

You can find the MFD UUID value on the {{site.data.keyword.mfd_short}} **Manage** panel.
{:note}

## Calling the service
{: #calling_service}

<!--You must install cURL before you can use the service.-->

To call the service, replace `api-key` with your service key.

The following example assumes that you have installed cURL.

The following example demonstrates the calculation of analytics on a financial security, which you specify by using an instrument identifier, under current market conditions:

```
curl -X GET -H "Authorization-api-key : <api-key>"  -H "Authorization-instance-id : <uuid>" -H "Content-Type:application/json" https://us-south.sia.cloud.ibm.com/v2/mtm/<ID_type>?ids=<id-of-instrument>
```
{:codeblock}

where `ID_type` is one of `ric`, `isin`, or  `sedol`.

<!-- See [Request examples](/docs/services/simulated-instrument-analytics/examples.html) for a set of more detailed examples. -->
See [Request examples](/docs/services/simulated-instrument-analytics?topic=simulated-instrument-analytics-request-examples) for a set of more detailed examples.



### Troubleshooting the connection between {{site.data.keyword.mfd_short}} and {{site.data.keyword.siminstruanalshort}}
{: #troubleshoot_connection}

When you connect {{site.data.keyword.mfd_short}} to {{site.data.keyword.siminstruanalshort}}, you might need to troubleshoot problems with authentication and authorization.

* When the API key for the {{site.data.keyword.siminstruanalshort}} service is incorrect, you encounter an authentication issue.
* When the API key for the {{site.data.keyword.siminstruanalshort}} service is correct but the UUID key for {{site.data.keyword.mfd_short}} that you provided to the {{site.data.keyword.siminstruanalshort}} service instance is incorrect, {{site.data.keyword.siminstruanalshort}} connects but it does not connect to {{site.data.keyword.mfd_short}} properly.
* When the API key for the {{site.data.keyword.siminstruanalshort}} service is correct and the UUID for {{site.data.keyword.mfd_short}} that you provided to the {{site.data.keyword.siminstruanalshort}} service instance is also correct, but you aren't using the service instance of {{site.data.keyword.mfd_short}} that was identified as the target, {{site.data.keyword.siminstruanalshort}} connects but you encounter an authorization error.
