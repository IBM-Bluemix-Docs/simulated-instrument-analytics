# Readme

## Usage of official names in the documentation

In the markdown documentation for SIA, we use variables (also known as content references or just _conrefs_) to refer to these official names of the service.

Official service names are defined in the conref file at https://github.ibm.com/cloud-doc-build/markdown/blob/master/cloudoeconrefs.yml.

See the IBM Cloud team's usage guidance at [Using conrefs for product names](https://console.test.cloud.ibm.com/docs/developing/writing/conrefs.html#keywords).

As of Nov-7-2018 we have these names that are defined:

### SIA official names

```
  siminstruanalshort:
    Simulated Instrument Analytics
  sia_full:
    IBM&reg; Simulated Instrument Analytics API
  sia_full_notm:
    IBM Simulated Instrument Analytics API
```

For SIA docs, we use the full name with the trademark (that is, `sia_full`) on the page at the first mention of the service.
For subsequent mentions on the same page, we use the short name.
In headings or titles, use the short name `siminstruanalshort`) or the no trademark name (`sia_full_notm`).



### MFD official names

For MFD, we have two variations of the name.

1. IBM Cloud

```
  mfd_full:
    IBM&reg; Managed Financial Data API
  mfd_full_notm:
    IBM Managed Financial Data API
  mfd_short:
    Managed Financial Data
```

When we refer specifically to the IBM Cloud service,
we use the full name with the trademark (that is, `mfd_full`) on the page at the first mention of the service.
For subsequent mentions of the IBM Cloud service on the same page, we use the short name (`siminstruanalshort`).
In headings or titles, use the short name `siminstruanalshort`) or the no trademark name (`sia_full_notm`). It is a judgment call but I think that using the short name is cleaner in a title, especially with the long names that we have for these services.

2. IBM Marketplace

```
  mfd_marketplace_full:
    IBM&reg; Managed Financial Data
  mfd_marketplace_full_notm:
    IBM Managed Financial Data
  mfd_marketplace_short:
    Managed Financial Data
```

When we refer specifically to the IBM Cloud service,
we use the full name with the trademark (that is, `mfd_marketplace_full`) on the page at the first mention of the service.
For subsequent mentions of the IBM Cloud service on the same page, we use the short name (`mfd_marketplace_short`).
In headings and titles, use the short name `mfd_marketplace_short`) or the no trademark name (`mfd_marketplace_full_notm`). It is a judgment call but I posit that using the short name is cleaner in a title, especially with the long names that we have for these services.

### Using short name for MFD

When we speak generically about both the cloud and marketplace offerings, we'll use `mfd_short` in favor of `mfd_marketplace_short` unless there is a clear reason why we should use `mfd_marketplace_short`.

As of Nov-7-2018, both of these short names resolve to "Managed Financial Data".
