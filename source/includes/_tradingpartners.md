## Trading Partners
> example fetching trading partner information

```shell
curl -i -H "Authorization: Bearer $ACCESS_TOKEN" https://platform.pokitdok.com/api/v4/tradingpartners/
```
```python
pd.trading_partners()
```
        
> example fetching information for a specific trading partner

```shell
curl -i -H "Authorization: Bearer $ACCESS_TOKEN" https://platform.pokitdok.com/api/v4/tradingpartners/aetna
```
```python
pd.trading_partners('aetna')
```
*Available modes of operation: real-time*

The Trading Partners endpoint provides access to the collection of PokitDok's trading
partners PokitDok.

Available Trading Partner endpoints:

Endpoint | HTTP Method | Description
-------- | ----------- | -----------
/tradingpartners/ | GET | Get a list of trading partners.
/tradingpartners/{id} | GET | Retreive the data for a specified trading partner; the ID is the PokitDok trading partner id.


The /tradingpartners/ response contains the following parameters:

Parameter | Type | Description
--------- | ---- | -----------
id | {string} | The "trading_partner_id" used in requests/EDI files to identify this trading partner.
is_enabled | {boolean} | Indicates if the connection to this trading partner is enabled.
name | {string} | Full name for the trading partner.
supported_transactions | {array} | Identifies the x12 transaction sets (270, 276, 837, etc.) the trading partner supports. The list of supported transactions also indicates the API Endpoints that are enabled for the trading partner. If the trading partner supports 270 transactions, you may use that trading_partner_id with the eligibility API. If 276 transactions are supported, you may use that trading_partner_id with the claim status API. If 837 transactions are supported, you may use that trading_partner_id with the claims API.
enrollment_required | {array} | Identifies the x12 transaction sets (270, 276, 837, etc.) that require additional enrollment steps before they may be used by your API application. Contact us if you'd like to use a transaction with a trading partner that requires enrollment prior to use.
metrics | {object} | When a specific trading partner id is requested and metrics are available, they will be included in the response. Timings are in milliseconds unless otherwise specified.
metrics.real_time_response_average | {float} | The average response time (milliseconds) for requests to this trading partner.
metrics.real_time_response_percentiles | {object} | Provides a percentile rank of the trading partner's response times, with the following groupings: 50%, 75%, and 95%.
monitoring | {object} | When a specific trading partner id is requested and monitoring data is available, monitoring information will be included in the response. Each key in the monitoring section corresponds to the name of an API where connectivity is enabled (e.g. authorizations, claim_status, eligibility, etc). Each API name will be associated with a monitoring status value and a timestamp to indicate when the status was last updated.
monitoring.{api_name}.status | {string} | The most recent status for the trading partner/API combination as returned by our monitoring system. Possible values include: available, unavailable, delayed, and unknown. A status of "available" indicates that the trading partner is operating normally based successful transactions executing within their average response time range. A status of "unavailable" indicates that the trading partner is unable to respond normally at that time. This may be due to scheduled or unplanned downtime. A status of "delayed" indicates that the trading partner is able to respond successfully to requests but that response times are higher than their average response time. A status of "unknown" will be returned for new trading partners that have just been added to the system and also for cases where the monitoring system encounters an exception and is unable to determine the current status.
monitoring.{api_name}.last_updated | {string} | The date the monitoring status was last updated (ISO 8601 format).
