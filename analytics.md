---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-21"

---

{:shortdesc: .shortdesc}
<!--{:new_window: target="_blank"}-->
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:faq: data-hd-content-type='faq'}

<!-- Link definitions -->


# Analytics
{: #analytics}
You can specify one or more `analytics` values when you submit a `POST /v2/simulate` request.
{: shortdesc}

## Field name values

This table contains 'Field Name' values that you can pass to the API for the measures (analytics), and the asset classes (Fixed Income, Equity, or Derivative) that they apply to.

|Field Name|Legacy Name|Fixed Income|Equity|Derivative|
|------------|----------|------------|------|-----------|
|[Price](#Price)|THEO/Price|X|X|X|
|[Value](#Value)|THEO/Value|X|X|X|
|[Clean Value](#Price)|THEO/Price|X|X|X|
|[Dirty Price](#Value)|THEO/Value|X|X|X|
|[Exposure](#Exposure)|THEO/Exposure|X|X|X|
|[Profit and Loss](#PnL)|POS/Unrealized Profit and Loss Theoretical|X|X|X|
|[PnL](#PnL)|POS/Unrealized Profit and Loss Theoretical|X|X|X|
|[Return](#Return)|Theo/Value@REL(scen&time,%diff)|X|X|X|
|[Yield](#Yield)|THEO/Yield|X| | |
|[Adjusted Duration](#AdjustedDuration)|THEO/Adjusted Duration|X| |X|
|[Macaulay Duration](#EffectiveDuration)|THEO/Macaulay Duration|X| |X|
|[Effective Duration](#MacaulayDuration)|THEO/Effective Duration|X| |X|
|[Monetary Duration](#MonetaryDuration)|THEO/Monetary Duration|X| |X|
|[Convexity](#Convexity)|THEO/Convexity|X| |X|
|[Effective Convexity](#EffectiveConvexity)|THEO/Effective Convexity|X| |X|
|[Monetary Convexity](#MonetaryConvexity)|THEO/Monetary Convexity|X| |X|
|[Implied Spread](#ImpliedSpread)|THEO/Implied Spread|X| |X|
|[Delta](#Delta)|THEO/Delta| | |X|
|[Gamma](#Gamma)|THEO/Gamma| | |X|
|[Rho](#Rho)|THEO/Domestic Rho| | |X|
|[Rho Domestic](#Rho)|THEO/Domestic Rho| | |X|
|[Rho Foreign](#Rho)|THEO/Foreign Rho| | |X|
|[Theta](#Theta)|THEO/Theta| | |X|
|[Vega](#Vega)|THEO/Vega| | |X|

{: caption="Table 1. {{site.data.keyword.sia_full}} field name values" caption-side="top"}

## Field name definitions

### Price
{: #Price}

**Price**, or **Clean Value**, is the price of a security excluding any accrued interest since a previous payment. For securities without periodic payments, clean price represents the current value of the security.

### Value
{: #Value}

**Value**, or **Dirty Price**, is the present value of future cash flows. Dirty price includes any accrued interest since the last periodic payment if applicable.

For Fixed Income securities, Dirty Price = Clean Price + Accrued Interest.

### Exposure
{: #Exposure}

**Exposure** is the outstanding value of a financial security. For an Equity, a Fixed Income, and other physical holdings, the Exposure would be equal to the Value of the security.

In the case of derivative securities, Exposure will represent the price * quantity of the underlying security. This is especially relevant for futures or options.

### Profit and Loss
{: #PnL}

**Profit and Loss**, or sometimes **PnL**, represents the observed change under a scenario. Financial instruments that decline in value under a scenario will have a negative PnL, and financial instruments that appreciate will have a positive PnL.

### Return
{: #Return}

**Return** is unrealized profit or loss resulting from a change under a scenario, in percentage terms.

### Yield
{: #Yield}

**Yield** is the return on a financial security in percentage terms. This value includes all of the cashflows that are returned to the holder of the security, such as coupon payments or accrued interest, and any appreciation in the value of the security.

### Adjusted Duration
{: #AdjustedDuration}

**Adjusted Duration**, sometimes referred to as Modified Duration, is a measure of the percentage change in a bond price to the change in the yield. Mathematically it can be expressed as 𝐷𝐴 = −𝑉 ∙ 𝜕𝑉/𝜕𝑌.


### Effective Duration
{: #EffectiveDuration}

**Effective Duration** is an empirically derived measure of asset price sensitivity to changes in interest rate. The main difference between the effective duration and the modified duration is the assumption regarding constant cash flow. That is, modified duration assumes that a change in the yield will not affect the cash flow (flat yield curve), whereas effective duration doesn't have that premise. The default tweak is 0.005.

𝐸𝑓𝑓 𝐷𝑢𝑟(𝑃𝑜𝑠) = 𝑉(𝑆 − 𝑇𝑤𝑒𝑎𝑘) − 𝑉(𝑆 + 𝑇𝑤𝑒𝑎𝑘) / (2×𝑇𝑤𝑒𝑎𝑘×𝑉(𝑆))

### Macaulay Duration
{: #MacaulayDuration}

**Macaulay Duration** is the weighted-average term to maturity of the cash flows from a bond. The weight of each cash flow is determined by dividing the present value of the cash flow by the price. This metric is frequently used by portfolio managers pursuing immunization strategies.


### Monetary Duration
{: #MonetaryDuration}

**Monetary Duration** is the approximate monetary price change in response to a change in yield of 100 basis points.

### Convexity
{: #Convexity}

**Convexity** is the rate of change of duration. The standard convexity measure doesn't take into account the shape of the yield curve.

### Effective Convexity
{: #EffectiveConvexity}

**Effective Convexity** is the empirically derived rate of change of duration. The standard convexity measure ignores the effects that are produced by both the shape of the yield curve and the presence of options, whereas the effective convexity measure doesn't. At the aggregation level, this field is calculated by using a weighting of instrument exposures.

𝐶𝑒 = 𝑉(𝑆−𝑇𝑤𝑒𝑎𝑘)+𝑉(𝑆+𝑇𝑤𝑒𝑎𝑘)−2×𝑉(𝑆) / (𝑇𝑤𝑒𝑎𝑘^2 × 𝑉(𝑆) × 100)

### Monetary Convexity
{: #MonetaryConvexity}

**Monetary Convexity** is the convexity of the security in price/value terms.

𝐶𝑀 =𝑉(𝑆−𝑇𝑤𝑒𝑎𝑘)+𝑉(𝑆+𝑇𝑤𝑒𝑎𝑘)−2×𝑉(𝑆) / (𝑇𝑤𝑒𝑎𝑘)^2

### Implied Spread
{: #ImpliedSpread}

**Implied Spread** is the additional interest rate that, when it is applied to the discount factor, sets the present value of future cash flows for a security equal to zero. The implied spread can be thought of as an additional, constant risk premium that is applied on top of the discount curve to achieve a theoretical value equal to the observed market spot price.

### Delta
{: #Delta}

**Delta** is the rate of change of the price of an instrument relative to changes in the price of the underlying asset, or the first derivative of the value of the instrument with respect to the underlying.

Δ = 𝜕𝑃 / 𝜕𝑆

### Gamma
{: #Gamma}

**Gamma** is a measure of the rate of change in the delta for a change in the underlying, or the second derivative of the value of the instrument with respect to the underlying value.

𝛤 = 𝜕2𝑉 / 𝜕𝑆2

<!-- ### <a id="Rho"></a>Rho -->
### Rho
{: #Rho}

**Rho** is the rate of change of the price of an instrument to change in the underlying interest rate (discount factor), or the first derivative of the value with respect to the applicable interest rate.

𝜌 = 𝜕𝑉 / 𝜕𝑟

### Theta
{: #Theta}

**Theta** measures how the value of the option changes with time. With normal model, theta is calculated empirically. For this calculation, the unit of change in time is 1 day.

&Theta; = 𝜕𝑉 / 𝜕t

### Vega
{: #Vega}

**Vega** is the rate of change of the price of an instrument to changes in volatility of the price of the underlying, or just the first derivative of the value of the instrument with respect to volatility.

𝛬 = (𝑉(1.01 ∙ 𝜎) − 𝑉(𝜎)) / 𝜎
