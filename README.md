<p align="center">
  <img src="https://raw.githubusercontent.com/omkarcloud/botasaurus/master/images/mascot.png" alt="airbnb scraper" />
</p>
<div align="center" style="margin-top: 0;">
  <h1>✨ Airbnb Scraper 🤖</h1>
  <p><strong>Scrape Airbnb listings, live nightly prices, availability, amenities, host profiles, and reviews in real time — across 67 country sites. Clean JSON, no blocks, no proxies.</strong></p>
</div>
<em>
  <h5 align="center">(Programming Language - Python 3)</h5>
</em>
<p align="center">
  <a href="#">
    <img alt="airbnb-scraper forks" src="https://img.shields.io/github/forks/omkarcloud/airbnb-scraper?style=for-the-badge" />
  </a>
  <a href="#">
    <img alt="Repo stars" src="https://img.shields.io/github/stars/omkarcloud/airbnb-scraper?style=for-the-badge&color=yellow" />
  </a>
</p>
<p align="center">
  <img src="https://views.whatilearened.today/views/github/omkarcloud/airbnb-scraper.svg" width="80px" height="28px" alt="View" />
</p>

Airbnb Scraper turns any Airbnb location into clean JSON, pulled live — no blocks, no proxies to manage. Autocomplete a place name, list every home for it with live nightly prices, and pull full room details — amenities, sleeping arrangement, house rules, category ratings, the host profile, and every photo — all via one API.

Prices and availability come back numeric, computed for the exact check-in/check-out you pass, so you can compare, monitor, and analyze rates programmatically instead of scraping HTML yourself.

It works across **67 Airbnb country domains** — `airbnb.com`, `airbnb.co.uk`, `airbnb.fr`, `airbnb.co.in`, `airbnb.com.au`, and 62 more — and every response comes back in that country site's language and currency.

- **Rated Excellent — 4.6 based on 25 reviews** on [Trustpilot](https://www.trustpilot.com/review/omkar.cloud). Our open source work is sponsored by [1000+ devs on GitHub](https://github.com/sponsors/omkarcloud).

[![Try the Airbnb Scraper API in the live playground — free, no signup](https://img.shields.io/badge/%E2%96%B6%20Playground-Run%20a%20live%20request%2C%20free-brightgreen?style=for-the-badge)](https://www.omkar.cloud/tools/airbnb-scraper-api/playground?utm_source=github&utm_medium=cpc&utm_content=badge)

[![Free Plan: 200 requests per month](https://img.shields.io/badge/Free%20tier-200%20requests%2Fmonth-blue?style=for-the-badge)](#pricing)

The same scraper is also available on **Apify** and **RapidAPI**:

[![Run on Apify](https://img.shields.io/badge/Run%20on-Apify-blue)](https://apify.com/omkar-cloud/airbnb-scraper) [![Run on RapidAPI](https://img.shields.io/badge/Run%20on-RapidAPI-blue?logo=rapidapi)](https://rapidapi.com/Chetan11dev/api/airbnb-scraper)

## Example: Airbnb Room Data in One Request

One request to the room details API:

```
GET https://airbnb-scraper-api.omkar.cloud/airbnb/rooms/details?query=42433166&checkin=2026-09-05&checkout=2026-09-08
```

```json
{
  "id": "42433166",
  "name": "FacesOasis Blue Room #2, Lower Full Bed #2 of 4",
  "link": "https://www.airbnb.com/rooms/42433166",
  "property_type": "Shared room in home",
  "person_capacity": 1,
  "bedrooms": null,
  "beds": 1,
  "bathrooms": 3,
  "overview": ["1 double bed", "3 shared bathrooms"],
  "rating": 4.62,
  "reviews_count": 34,
  "category_ratings": {
    "cleanliness": 4.2,
    "accuracy": 4.7,
    "check_in": 4.6,
    "communication": 4.6,
    "location": 4.5,
    "value": 4.5
  },
  "is_guest_favorite": false,
  "is_available": true,
  "price": {
    "amount": 153,
    "currency": "USD",
    "qualifier": "for 3 nights",
    "original_amount": null,
    "breakdown": [
      { "description": "3 nights x $50.78", "amount": 152.35 }
    ]
  },
  "location": { "name": "Oakland, California, United States", "latitude": 37.80345, "longitude": -122.29667 },
  "host": {
    "id": "195751579",
    "name": "FacesOasis",
    "is_superhost": false,
    "is_verified": true,
    "response_rate": 100,
    "response_time": "within an hour",
    "years_hosting": 6
  }
}
```

*Trimmed for readability — the full response has 30+ fields including the description, every amenity grouped by category, sleeping arrangement, house rules, safety items, cancellation policy, co-hosts, and all photos. See the [sample response](#rooms-details) in the API reference.*

Pass `checkin` and `checkout` to price the stay; omit them and a representative upcoming stay is used automatically, so a price still comes back.

**[Run this exact request in the Playground — no signup, no key →](https://www.omkar.cloud/tools/airbnb-scraper-api/playground?utm_source=github&utm_medium=cpc&utm_content=example)**

The playground comes prefilled with this request and runs it against the live API in your browser. The JSON it returns is identical to what the API returns.

## Start Getting Data in Minutes

Python and Node.js integration examples are available for every endpoint in the playground, so you can get Airbnb data in minutes instead of days.

```python
import requests

# Scrape a full Airbnb room profile with live price and availability
response = requests.get(
    "https://airbnb-scraper-api.omkar.cloud/airbnb/rooms/details",
    params={
        "query": "42433166",
        "checkin": "2026-09-05",
        "checkout": "2026-09-08",
    },
    headers={"API-Key": "YOUR_API_KEY"},
)

print(response.json())
```

## The Typical Flow

The three endpoints chain naturally:

1. **Rooms Autocomplete** — turn a place name (`new york`) into a searchable location with its Google `place_id`.
2. **Rooms Search** — feed that location in and get every home, 18 per page, with live nightly prices.
3. **Rooms Details** — take any listing's `id` and pull the full room profile, priced for your dates.

## API Reference

All endpoints are GET requests against `https://airbnb-scraper-api.omkar.cloud`, authenticated with the `API-Key` header, returning JSON.

Language and currency are set by the `domain` parameter (default `airbnb.com`) — pass any of the [67 supported domains](#supported-domains) to get results from that country's Airbnb site.

### Rooms Autocomplete

▶ [Try it live in the Playground →](https://www.omkar.cloud/tools/airbnb-scraper-api/playground?utm_source=github&utm_medium=cpc&utm_content=endpoint-autocomplete)

```
GET https://airbnb-scraper-api.omkar.cloud/airbnb/rooms/autocomplete?query=new+york
```

Autocomplete a place name into matching Airbnb locations. Each result carries its Google place ID, coordinates, bounding box, and a ready-to-use rooms-search link — pass the `full_name` and `google_place_id` straight into Rooms Search.

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `query` | Yes | — | Partial or full place name (e.g. `new york`, `paris`). |
| `num_results` | No | `10` | Maximum number of locations to return (`1`–`20`). |
| `domain` | No | `airbnb.com` | Airbnb country domain — sets the result language. |

<details>
<summary>Sample Response (click to expand)</summary>

```json
{
  "domain": "airbnb.com",
  "query": "new york",
  "locale": "en",
  "country": "US",
  "currency": "USD",
  "count": 10,
  "results": [
    {
      "name": "New York City, NY",
      "full_name": "New York City, New York, United States",
      "link": "https://www.airbnb.com/s/New-York-City--New-York--United-States/homes?place_id=ChIJOwg_06VPwokRYv534QaPC8g&query=New+York+City%2C+New+York%2C+United+States",
      "google_place_id": "ChIJOwg_06VPwokRYv534QaPC8g",
      "country_code": "US",
      "types": ["locality", "political"],
      "suggestion_type": "LOCATION",
      "coordinates": { "latitude": 40.6971415, "longitude": -73.979506 },
      "bounding_box": {
        "southwest": { "latitude": 40.476578, "longitude": -74.258843 },
        "northeast": { "latitude": 40.917705, "longitude": -73.700169 }
      },
      "is_location_only": true
    }
  ]
}
```

</details>

---

### Rooms Search

▶ [Try it live in the Playground →](https://www.omkar.cloud/tools/airbnb-scraper-api/playground?utm_source=github&utm_medium=cpc&utm_content=endpoint-search)

```
GET https://airbnb-scraper-api.omkar.cloud/airbnb/rooms/search?query=New+York+City,+New+York,+United+States&place_id=ChIJOwg_06VPwokRYv534QaPC8g
```

List every home for a location, 18 per page (Airbnb serves ~15 pages) with `next`/`previous` pagination links. Pass `query` (ideally the `full_name` from Rooms Autocomplete) plus its `place_id` for the most accurate results.

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `query` | Yes | — | Location name — ideally the `full_name` from Rooms Autocomplete. |
| `place_id` | No | — | Google place ID from Rooms Autocomplete (`google_place_id`). Recommended. |
| `page` | No | `1` | Page number, 18 homes per page (`1`–`50`). |
| `checkin` / `checkout` | No | — | Trip dates (`YYYY-MM-DD`), passed together. Omit and Airbnb prices against representative upcoming dates. |
| `adults` | No | — | Number of adult guests (`0`–`16`). |
| `children` | No | — | Number of child guests (`0`–`15`). |
| `infants` | No | — | Number of infant guests (`0`–`5`). |
| `pets` | No | — | Number of pets (`0`–`5`). |
| `price_min` / `price_max` | No | — | Nightly price filter, in the domain's currency. |
| `domain` | No | `airbnb.com` | Airbnb country domain — sets language and currency. |

<details>
<summary>Sample Response (click to expand)</summary>

```json
{
  "count": 270,
  "per_page": 18,
  "current_page": 1,
  "total_pages": 15,
  "next": "https://airbnb-scraper-api.omkar.cloud/airbnb/rooms/search?query=New+York+City%2C+New+York%2C+United+States&place_id=ChIJOwg_06VPwokRYv534QaPC8g&domain=airbnb.com&page=2",
  "previous": null,
  "domain": "airbnb.com",
  "query": "New York City, New York, United States",
  "place_id": "ChIJOwg_06VPwokRYv534QaPC8g",
  "currency": "USD",
  "results": [
    {
      "id": "598499099324319670",
      "name": "Midtown 3double beds Studio",
      "title": "Apartment in New York",
      "link": "https://www.airbnb.com/rooms/598499099324319670",
      "summary": ["3 double beds", "1 bath"],
      "bedrooms": null,
      "beds": 3,
      "bathrooms": 1,
      "rating": 4.79,
      "reviews_count": 265,
      "is_superhost": false,
      "is_guest_favorite": true,
      "price": {
        "amount": 961,
        "currency": "USD",
        "qualifier": "for 5 nights",
        "original_amount": null,
        "breakdown": [
          { "description": "5 nights x $193.80", "amount": 969 },
          { "description": "Early booking discount", "amount": -8.9 },
          { "description": "Price after discount", "amount": 960.1 }
        ],
        "checkin": "2026-11-15",
        "checkout": "2026-11-20"
      },
      "coordinates": { "latitude": 40.7472, "longitude": -73.9878 },
      "images": [
        "https://a0.muscache.com/im/pictures/miso/Hosting-598499099324319670/original/38a18926-fe28-4946-a7a2-20d3daa1fdd9.jpeg"
      ]
    }
  ]
}
```

</details>

---

### Rooms Details

▶ [Try it live in the Playground →](https://www.omkar.cloud/tools/airbnb-scraper-api/playground?utm_source=github&utm_medium=cpc&utm_content=endpoint-details)

```
GET https://airbnb-scraper-api.omkar.cloud/airbnb/rooms/details?query=42433166
```

Full details for one room. `query` accepts a numeric room id or any Airbnb `/rooms/<id>` URL. Pass `checkin` + `checkout` to also get `price` and `is_available` (a representative upcoming stay is used when omitted) — `price` will be absent if the room is unavailable for those dates.

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `query` | Yes | — | Room id (e.g. `42433166`) or `/rooms/<id>` URL. |
| `checkin` / `checkout` | No | — | Trip dates (`YYYY-MM-DD`), passed together — the stay `price` and `is_available` are computed for. |
| `adults` | No | `1` | Number of adult guests the price is computed for (`1`–`16`). |
| `children` | No | — | Number of child guests (`0`–`15`). |
| `infants` | No | — | Number of infant guests (`0`–`5`). |
| `pets` | No | — | Number of pets (`0`–`5`). |
| `domain` | No | `airbnb.com` | Airbnb country domain — sets language and currency. |

Returns 30+ fields: property type and capacity, description, amenities grouped by category, sleeping arrangement, house rules, safety items, category ratings, cancellation policy, the host profile (with co-hosts and response stats), live price/availability, and all photos.

<details>
<summary>Sample Response (click to expand)</summary>

```json
{
  "domain": "airbnb.com",
  "currency": "USD",
  "checkin": "2026-09-05",
  "checkout": "2026-09-08",
  "id": "42433166",
  "name": "FacesOasis Blue Room #2, Lower Full Bed #2 of 4",
  "link": "https://www.airbnb.com/rooms/42433166",
  "property_type": "Shared room in home",
  "person_capacity": 1,
  "bedrooms": null,
  "beds": 1,
  "bathrooms": 3,
  "overview": ["1 double bed", "3 shared bathrooms"],
  "description": "Welcome World Travelers! Convenience & Pleasure ...",
  "rating": 4.62,
  "reviews_count": 34,
  "category_ratings": {
    "cleanliness": 4.2,
    "accuracy": 4.7,
    "check_in": 4.6,
    "communication": 4.6,
    "location": 4.5,
    "value": 4.5
  },
  "is_guest_favorite": false,
  "is_new_listing": false,
  "is_available": true,
  "price": {
    "amount": 153,
    "currency": "USD",
    "qualifier": "for 3 nights",
    "original_amount": null,
    "breakdown": [
      { "description": "3 nights x $50.78", "amount": 152.35 }
    ]
  },
  "cancellation_policy": null,
  "location": {
    "name": "Oakland, California, United States",
    "address": null,
    "latitude": 37.80345,
    "longitude": -122.29667
  },
  "host": {
    "id": "195751579",
    "name": "FacesOasis",
    "is_superhost": false,
    "is_verified": true,
    "rating": 4.6,
    "reviews_count": 693,
    "years_hosting": 6,
    "response_rate": 100,
    "response_time": "within an hour",
    "cohosts": []
  },
  "amenities": [
    {
      "group": "Bathroom",
      "items": [
        { "title": "Bathtub", "is_available": true },
        { "title": "Hair dryer", "is_available": true }
      ]
    }
  ],
  "sleeping_arrangement": [
    { "title": "Bedroom", "subtitle": "1 double bed" }
  ],
  "house_rules": [
    {
      "section": "Checking in and out",
      "items": ["Check-in: 4:00 PM - 10:00 PM", "Checkout before 12:00 PM", "Self check-in with keypad"]
    }
  ],
  "safety_and_property": ["Carbon monoxide alarm", "Smoke alarm"],
  "images": [
    { "link": "https://a0.muscache.com/im/pictures/hosting/Hosting-42433166/original/78a823f8-8129-4e65-b3ee-39ad22040fb5.jpeg", "caption": "1453 living rm a" }
  ]
}
```

</details>

---

### Supported Domains

Language and currency follow the `domain` you pass. 67 Airbnb country sites are supported:

`airbnb.com`, `airbnb.co.uk`, `airbnb.ca`, `airbnb.com.au`, `airbnb.co.nz`, `airbnb.ie`, `airbnb.co.in`, `airbnb.com.sg`, `airbnb.com.my`, `airbnb.com.ph`, `airbnb.co.id`, `airbnb.com.hk`, `airbnb.com.tw`, `airbnb.co.kr`, `airbnb.jp`, `airbnb.cn`, `airbnb.com.vn`, `airbnb.fr`, `airbnb.be`, `airbnb.lu`, `airbnb.de`, `airbnb.at`, `airbnb.ch`, `airbnb.nl`, `airbnb.it`, `airbnb.es`, `airbnb.pt`, `airbnb.gr`, `airbnb.pl`, `airbnb.cz`, `airbnb.hu`, `airbnb.dk`, `airbnb.se`, `airbnb.no`, `airbnb.fi`, `airbnb.is`, `airbnb.ru`, `airbnb.com.tr`, `airbnb.com.ua`, `airbnb.lv`, `airbnb.lt`, `airbnb.si`, `airbnb.rs`, `airbnb.al`, `airbnb.ba`, `airbnb.me`, `airbnb.am`, `airbnb.az`, `airbnb.com.mt`, `airbnb.mx`, `airbnb.com.br`, `airbnb.com.ar`, `airbnb.cl`, `airbnb.com.co`, `airbnb.com.pe`, `airbnb.com.ec`, `airbnb.com.bo`, `airbnb.com.py`, `airbnb.com.sv`, `airbnb.com.hn`, `airbnb.com.ni`, `airbnb.com.gt`, `airbnb.co.cr`, `airbnb.co.ve`, `airbnb.com.pa`, `airbnb.co.za`, `airbnb.ae`

## Pricing

| Plan | Price | Requests/Month |
|------|-------|----------------|
| Free | $0 | 200 |
| Starter | $16 | 20,000 |
| Grow | $48 | 100,000 |
| Scale | $148 | 400,000 |

1 API call = 1 request

Free Plan Available — [create your API key →](https://www.omkar.cloud/auth/sign-up?redirect=/api-key&utm_source=github&utm_medium=cpc&utm_content=pricing-signup). No credit card for the free tier.

## FAQs

### Can I try the API before signing up?

Yes. The playground runs live requests in your browser — free, no account, no API key. [Try it in the Playground →](https://www.omkar.cloud/tools/airbnb-scraper-api/playground?utm_source=github&utm_medium=cpc&utm_content=faq)

### How do I search Airbnb listings for a location?

Call Rooms Autocomplete with a place name (`GET /airbnb/rooms/autocomplete?query=new+york`) to get the location's `full_name` and `google_place_id`, then pass both into Rooms Search (`GET /airbnb/rooms/search?query=...&place_id=...`). Search returns 18 homes per page with live nightly prices, and a `next` link walks you through all ~15 pages Airbnb serves.

### Do I get live prices and availability?

Yes. Prices come back numeric with a full breakdown (base rate, discounts, fees) and the check-in/check-out they were computed for. On Rooms Details, pass `checkin` and `checkout` to get `price` and `is_available` for those exact dates — perfect for rate monitoring and availability tracking. If the room isn't bookable for those dates, `price` will be absent. Omit the dates and a representative upcoming stay is used automatically.

### Does it work for non-US Airbnb regions?

Yes. Pass the `domain` parameter — `airbnb.co.uk`, `airbnb.fr`, `airbnb.de`, `airbnb.co.in`, `airbnb.com.au`, `airbnb.jp`, and 61 more country domains are supported. You'll get results in that site's language and prices in its currency.

### How fresh is the data?

Data is pulled from Airbnb in real time. Every API call fetches live data — not cached or stale results. Prices, availability, ratings, and review counts reflect what's on Airbnb right now.

### Will I get blocked or need proxies?

No. We handle the scraping infrastructure — you call a normal REST API and never touch Airbnb directly, so there are no proxies, headless browsers, or CAPTCHAs on your side.

### Can I pass a room URL instead of an id?

Yes. Rooms Details accepts either a bare room id (`42433166`) or the full Airbnb link (`https://www.airbnb.com/rooms/42433166`). Use whichever you have.

## More Travel & Data Scrapers: TripAdvisor & Google Maps

- **[TripAdvisor Scraper API (200+ GitHub Stars)](https://github.com/omkarcloud/tripadvisor-scraper)** — the same clean JSON for TripAdvisor: hotels, restaurants, attractions, and cruises with reviews, ratings, rankings, pricing, and award badges. Cross-reference an Airbnb location against nearby hotels and things to do, across 45+ locales.

- **[Google Maps Scraper (3,100+ GitHub Stars)](https://github.com/omkarcloud/google-maps-scraper)** — need tens of thousands of leads? Type a niche and a city ("dentists in New York") and get every matching business as a ready-to-call lead list — name, address, phone, website, emails, rating, and reviews. The free tier alone pulls up to 100K leads a month.

- **[Website Email Contact Scraper](https://github.com/omkarcloud/website-email-contact-scraper)** — **Free and open source.** Point it at any website and get every email, phone number, and social profile on it, each with source pages and an official/unofficial flag.

## Support

Built by developers, for developers — when you reach out, you talk to the engineers who built the API, not a support script. Message us anytime and we'll solve your query within 1 working day.


[![Contact Us on WhatsApp about Airbnb Scraper](https://raw.githubusercontent.com/omkarcloud/assets/master/images/whatsapp-us.png)](https://api.whatsapp.com/send?phone=918178804274&text=I%20have%20a%20question%20about%20the%20Airbnb%20Scraper%20API.)

Email: [happy.to.help@omkar.cloud](mailto:happy.to.help@omkar.cloud?subject=Airbnb%20Scraper%20API%20Question)

[![Email Us about Airbnb Scraper](https://raw.githubusercontent.com/omkarcloud/assets/master/images/ask-on-email.png)](mailto:happy.to.help@omkar.cloud?subject=Airbnb%20Scraper%20API%20Question)

## Love It? Star It! ⭐

From one developer to another: If the Airbnb Scraper API saved you time, please [star the repo](https://github.com/omkarcloud/airbnb-scraper).

Here's why it matters: most developers judge a scraper by its stars before trying it. Your star helps the next developer — someone deciding whether the Airbnb data here is real and reliable — try it with confidence.

It takes only 1 second, and means the world to me.
