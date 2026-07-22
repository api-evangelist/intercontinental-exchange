---
name: Pull historical market data
description: Retrieve historical OHLC, volume, and open interest for an ICE instrument over a date range via the Consolidated Feed API.
api: openapi/intercontinental-exchange-market-data-api-openapi.yml
operations: [listInstruments, getMarketHistory]
generated: '2026-07-22'
method: generated
---

# Pull historical market data

Use the ICE Consolidated Feed API (base URL `https://api.theice.com`) to fetch history for an instrument.

## Auth

Send an API key or bearer token in the `Authorization` header; credentials come from the ICE Developer Center (https://developer.theice.com/hc/en-us). See `authentication/intercontinental-exchange-authentication.yml`.

## Steps

1. **Resolve the instrument.** Call `listInstruments` (`GET /marketdata/instruments`), filtering with `exchange` / `productType` query parameters, and capture the instrument identifier.
2. **Fetch history.** Call `getMarketHistory` (`GET /marketdata/history`) with the required `instrumentId` and optional `startDate` / `endDate` (ISO dates). The response carries OHLC prices, volume, and open interest.

## Rules

- Read-only surface; safe to retry (see `conventions/intercontinental-exchange-conventions.yml`).
- Keep date ranges bounded — historical entitlements vary by ICE Data Services subscription.
