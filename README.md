<p align=center><img src="https://github.com/vdbio/versiondb_samples/blob/5495aa3f54628e3d8f633f1e5bbd68f44ed7f7c8/logo.jpg" width="20%"></p>

# VersionDB Samples

The following dataset is compiled from sample data available on https://versiondb.io/ between September 2025 and January 2026.

## Overview

| Archive | Unique Domains | Total URLs | Crawl Period |
|---|---|---|---|
| `2026_jan.zip` | 52,700 | 136,500 | January 12 – 14, 2026 |
| `2025_dec.zip` | 67,094 | 190,790 | December 4 – 6, 2025 |
| `2025_nov.zip` | 144,516 | 427,962 | November 11 – 16, 2025 |
| `2025_oct.zip` | 50,000 | 192,374 | October 5 – 12, 2025 |
| `2025_sept.zip` | 50,000 | 263,427 | September 5 – 12, 2025 |
| **Total** | **364,310** | **1,211,053** | |

## Data Format

The data is structured as nested JSON. The top-level key is a domain (e.g. `"yadays.it"`), the second-level key is a URL path (e.g. `"/"`), and the value is a snapshot object representing the state of that URL at crawl time.

```json
{
  "yadays.it": {
    "/": {
      "date": "2026-01-13T13:03:20Z",
      "httpProtocol": "http/1.1, tls/1.3",
      "httpStatus": 200,
      "ipAddress": "95.174.23.179",
      "httpHeaderHash": "4CRXGIK5JWT5Q4DXRPGIKIAWDGROZ3G3",
      "httpHeaderTechnologies": [
        "MySQL",
        "WordPress",
        "PHP:7.3.33",
        "Apache HTTP Server"
      ],
      "httpHeaderUrls": [],
      "httpHeaderByteSize": 570,
      "httpBodyHash": "CNNHFRWVCI6UVQ2UIDKOCTYZXG4BMHF5",
      "httpBodyTechnologies": [
        "PHP",
        "jQuery",
        "WordPress:5.5.17",
        "Contact Form 7:5.3",
        "MySQL",
        "YouTube",
        "Three.js",
        "A-Frame:1.0.4",
        "Google Analytics"
      ],
      "httpBodyUrls": [
        "https://yadays.it/universita-bocconi/",
        "https://yadays.it/nuova-zelanda-otumoetai-college/",
        "https://yadays.it/canada-ottawa-carleton-district-school-board/",
        "..."
      ],
      "httpBodyMetaTags": {},
      "httpBodyByteSize": 84710,
      "httpBodyPageTitle": "YA!DAYS 2020 – YouAbroad"
    }
  }
}
```

## Schema

| Field | Type | Description |
|---|---|---|
| `date` | `string` (ISO 8601) | UTC timestamp of when the snapshot was captured. |
| `httpProtocol` | `string` | The negotiated HTTP protocol and TLS version. |
| `httpStatus` | `integer` | HTTP response status code returned by the server. |
| `ipAddress` | `string` | The resolved IP address of the server that handled the request. |
| `httpHeaderHash` | `string` | Base32-encoded SHA1 hash of the response headers. |
| `httpHeaderTechnologies` | `[]string` | Technologies or software identified from response headers. |
| `httpHeaderUrls` | `[]string` | URLs found in response headers. |
| `httpHeaderByteSize` | `integer` | Size of the raw response headers in bytes. |
| `httpBodyHash` | `string` | Base32-encoded SHA1 hash of the response body. |
| `httpBodyTechnologies` | `[]string` | Technologies or frameworks identified from the response body. |
| `httpBodyUrls` | `[]string` | URLs extracted from the response body. |
| `httpBodyMetaTags` | `object` | Key-value map of HTML `<meta>` tags parsed from the response body. |
| `httpBodyByteSize` | `integer` | Size of the response body in bytes. |
| `httpBodyPageTitle` | `string (nullable)` | Text content of the HTML `<title>` element. Only `null` when the page had no `<title>` tag. |