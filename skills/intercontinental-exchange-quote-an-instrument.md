---
name: Quote an ICE instrument
description: Discover an instrument on an ICE exchange and fetch its current market quote via the Consolidated Feed API.
api: openapi/intercontinental-exchange-market-data-api-openapi.yml
operations: [listExchanges, listInstruments, getQuotes]
generated: '2026-07-22'
method: generated
---

# Quote an ICE instrument

Use the ICE Consolidated Feed API (base URL `https://api.theice.com`) to find an instrument and get its quote.

## Auth

Every request needs credentials issued through the ICE Developer Center (https://developer.theice.com/hc/en-us — registration required). Send either an API key or a bearer token in the `Authorization` header (see `authentication/intercontinental-exchange-authentication.yml`).

## Steps

1. **Find the exchange.** Call `listExchanges` (`GET /reference/exchanges`) to list exchanges operated by ICE with their exchange codes and available product types.
2. **Find the instrument.** Call `listInstruments` (`GET /marketdata/instruments`) with optional `exchange` and `productType` query filters to locate the instrument and capture its identifier.
3. **Get the quote.** Call `getQuotes` (`GET /marketdata/quotes`) with the required `instrumentId` query parameter. The response carries bid, ask, last trade, and volume.

## Rules

- All operations are read-only GETs; there is no idempotency-key contract (see `conventions/intercontinental-exchange-conventions.yml`).
- Quotes may be real-time or delayed depending on your ICE Data Services entitlements.
- Check the ICE Status Center (https://www.ice.com/status) if requests fail unexpectedly.
