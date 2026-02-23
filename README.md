![Airbnb Scraper Featured Image](https://raw.githubusercontent.com/omkarcloud/airbnb-scraper/master/airbnb-scraper-featured-image.png)

# Airbnb Scraper API

Scrape Airbnb listings, prices, host profiles, and ratings for any destination worldwide via a simple REST API. 5,000 free requests/month.

## Key Features

- Search Airbnb listings by destination, travel dates, and guest count
- Get 30+ data points per listing (pricing, ratings, host info, photos, amenities)
- Full property details with rating breakdown by category
- Host profiles with verification status, ratings, and years hosting
- Date-aware pricing with itemized cost breakdowns
- **5,000 requests/month on free tier**
- Example Response:
```json
{
    "listing_id": "1447073736891652317",
    "title": "Skytree within walking distance! Kinshicho Station is right nearby | For couples and families",
    "property_type": "Private room in rental unit",
    "listing_url": "https://www.airbnb.com/rooms/1447073736891652317",
    "city": "Sumida City",
    "full_address": "Sumida City, Tokyo, Japan",
    "latitude": 35.69477,
    "longitude": 139.81317,
    "bedroom_count": 1,
    "bathroom_count": 1,
    "bed_count": 2,
    "guest_capacity": 2,
    "is_superhost": false,
    "overall_rating": 4.92,
    "review_count": 13,
    "pricing": {
        "nightly_rate": 331,
        "currency": "USD",
        "cost_breakdown": [
            { "label": "4 nights x $90.36", "amount": 361.43 },
            { "label": "Early bird discount", "amount": 30.46 }
        ]
    },
    "cancellation_policy": "better_strict_with_grace_period"
}
```

## Get API Key

Create an account at [omkar.cloud](https://www.omkar.cloud/auth/sign-up?redirect=/api-key) to get your API key.

It takes just 2 minutes to sign up. You get 5,000 free requests every month for detailed Airbnb data — more than enough for most users to get their job done without paying a dime.

This is a well built product, and your search for the best Airbnb Scraper API ends right here.


## Quick Start

```bash
curl -X GET "https://airbnb-scraper-api.omkar.cloud/airbnb/listings/search?destination_query=Tokyo&arrival_date=2026-07-01&departure_date=2026-07-05&adult_guests=2" \
  -H "API-Key: YOUR_API_KEY"
```

```json
{
    "total_results": 40,
    "listings": [
        {
            "listing_id": "1447073736891652317",
            "title": "Skytree within walking distance! Kinshicho Station is right nearby | For couples and families",
            "property_type": "Private room in rental unit",
            "listing_url": "https://www.airbnb.com/rooms/1447073736891652317",
            "city": "Sumida City",
            "full_address": "Sumida City, Tokyo, Japan",
            "overall_rating": 4.92,
            "review_count": 13,
            "pricing": {
                "nightly_rate": 331,
                "currency": "USD"
            },
            "is_superhost": false
        }
    ]
}
```

## Quick Start (Python)

```bash
pip install requests
```

```python
import requests

# Search listings in Tokyo
response = requests.get(
    "https://airbnb-scraper-api.omkar.cloud/airbnb/listings/search",
    params={
        "destination_query": "Tokyo",
        "arrival_date": "2026-07-01",
        "departure_date": "2026-07-05",
        "adult_guests": 2,
    },
    headers={"API-Key": "YOUR_API_KEY"}
)

print(response.json())
```


## API Reference

### Search Listings

```
GET https://airbnb-scraper-api.omkar.cloud/airbnb/listings/search
```

#### Parameters

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `destination_query` | Yes | — | City, neighborhood, landmark, or region. |
| `arrival_date` | No | — | Check-in date in `YYYY-MM-DD` format. |
| `departure_date` | No | — | Check-out date in `YYYY-MM-DD` format. |
| `adult_guests` | No | — | Number of adult travelers (age 13+). |
| `page_number` | No | `1` | Results page number. |

#### Example

```python
import requests

response = requests.get(
    "https://airbnb-scraper-api.omkar.cloud/airbnb/listings/search",
    params={
        "destination_query": "Tokyo",
        "arrival_date": "2026-07-01",
        "departure_date": "2026-07-05",
        "adult_guests": 2,
    },
    headers={"API-Key": "YOUR_API_KEY"}
)

print(response.json())
```

#### Response

<details>
<summary>Sample Response (click to expand)</summary>

```json
{
    "total_results": 40,
    "listings": [
        {
            "listing_id": "1447073736891652317",
            "title": "Skytree within walking distance! Kinshicho Station is right nearby | For couples and families",
            "property_type": "Private room in rental unit",
            "listing_url": "https://www.airbnb.com/rooms/1447073736891652317",
            "booking_url": "https://www.airbnb.com/rooms/1447073736891652317?check_in=2026-07-01&check_out=2026-07-05&adults=2",
            "photos": [
                "https://a0.muscache.com/im/pictures/hosting/Hosting-1447073736891652317/original/600480dc-f4a2-4ab2-919b-76aede4010bc.png?im_w=720",
                "https://a0.muscache.com/im/pictures/hosting/Hosting-1447073736891652317/original/71e76dc9-3bde-432b-8b05-be81adb05ca0.png?im_w=720"
            ],
            "city": "Sumida City",
            "full_address": "Sumida City, Tokyo, Japan",
            "latitude": 35.69477,
            "longitude": 139.81317,
            "bedroom_count": 1,
            "bathroom_count": 1,
            "bed_count": 2,
            "guest_capacity": 2,
            "amenity_ids": [1, 35, 4, 5, 39, 167, 40, 104, 41, 73, 137, 107, 44, 45, 77, 79, 657, 51, 53, 85, 663, 89, 91, 30],
            "host_id": 451581302,
            "host_avatar": "https://a0.muscache.com/im/pictures/user/User/original/758f5808-ab3e-41f7-9f72-1735a7466dfc.jpeg?aki_policy=profile_x_medium",
            "is_superhost": false,
            "overall_rating": 4.92,
            "review_count": 13,
            "pricing": {
                "nightly_rate": 331,
                "currency": "USD",
                "total_cost": null,
                "cost_breakdown": [
                    { "label": "4 nights x $90.36", "amount": 361.43 },
                    { "label": "Early bird discount", "amount": 30.46 }
                ]
            },
            "cancellation_policy": "better_strict_with_grace_period",
            "is_rare_find": false,
            "rank": 1
        }
    ]
}
```

</details>

---

### Listing Details

```
GET https://airbnb-scraper-api.omkar.cloud/airbnb/listings/details
```

#### Parameters

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `stay_id` | Yes | — | Airbnb listing ID. |
| `arrival_date` | No | — | Check-in date in `YYYY-MM-DD` format for date-aware pricing. |
| `departure_date` | No | — | Check-out date in `YYYY-MM-DD` format for date-aware pricing. |
| `adult_guests` | No | — | Number of adult travelers (age 13+). |
| `currency_code` | No | `USD` | Currency code for prices. |

#### Example

```python
import requests

response = requests.get(
    "https://airbnb-scraper-api.omkar.cloud/airbnb/listings/details",
    params={
        "stay_id": "1447073736891652317",
        "arrival_date": "2026-07-01",
        "departure_date": "2026-07-05",
        "adult_guests": 2,
        "currency_code": "USD",
    },
    headers={"API-Key": "YOUR_API_KEY"}
)

print(response.json())
```

#### Response Fields

Returns 30+ fields including title, tagline, property type, all photos, property highlights, full location with coordinates, host profile (name, verification, rating, review count, years hosting), overall rating, review count, guest favorite status, rating breakdown by category, full pricing with itemized costs, cancellation terms, and availability status.

<details>
<summary>Sample Response (click to expand)</summary>

```json
{
    "listing_id": "1447073736891652317",
    "title": "Skytree within walking distance! Kinshicho Station is right nearby | For couples and families",
    "tagline": "Room in Sumida-ku, Japan",
    "property_type": "Private room in rental unit",
    "listing_url": "https://www.airbnb.com/rooms/1447073736891652317",
    "photos": [
        "https://a0.muscache.com/im/pictures/hosting/Hosting-1447073736891652317/original/71e76dc9-3bde-432b-8b05-be81adb05ca0.png",
        "https://a0.muscache.com/im/pictures/hosting/Hosting-1447073736891652317/original/600480dc-f4a2-4ab2-919b-76aede4010bc.png"
    ],
    "highlights": ["2 beds", "Private attached bathroom"],
    "location": "Sumida-ku, Tokyo Prefecture, Japan",
    "latitude": 35.6948,
    "longitude": 139.8132,
    "guest_capacity": 2,
    "amenity_ids": [],
    "host_name": "Eichi",
    "host_id": "451581302",
    "is_superhost": false,
    "is_verified": true,
    "host_rating": 4.62,
    "host_review_count": 1050,
    "years_hosting": 3,
    "overall_rating": 4.92,
    "review_count": 13,
    "is_guest_favorite": true,
    "rating_categories": [
        { "category": "Cleanliness", "score": "5.0" },
        { "category": "Accuracy", "score": "5.0" },
        { "category": "Check-in", "score": "5.0" },
        { "category": "Communication", "score": "5.0" },
        { "category": "Location", "score": "4.8" },
        { "category": "Value", "score": "5.0" }
    ],
    "pricing": {
        "rate": 340,
        "qualifier": "For 4 nights",
        "currency": "USD",
        "total": 339.3,
        "priceItems": [
            { "title": "4 nights x $92.44", "amount": 369.76 },
            { "title": "Early bird discount", "amount": 30.46 }
        ]
    },
    "cancellation_terms": [
        "Free cancellation before June 1. Cancel before June 24 for a partial refund."
    ],
    "is_available": true,
    "unavailability_reason": null
}
```

</details>

## Error Handling

```python
response = requests.get(
    "https://airbnb-scraper-api.omkar.cloud/airbnb/listings/search",
    params={"destination_query": "Tokyo"},
    headers={"API-Key": "YOUR_API_KEY"}
)

if response.status_code == 200:
    data = response.json()
elif response.status_code == 401:
    # Invalid API key
    pass
elif response.status_code == 429:
    # Rate limit exceeded
    pass
```

## FAQs

### What data does the API return?

**Search Listings** returns title, property type, listing URL, booking URL, photos, city, full address, coordinates, bedroom/bathroom/bed count, guest capacity, amenity IDs, host ID, host avatar, superhost status, overall rating, review count, pricing with cost breakdown, cancellation policy, and rare find flag.

**Listing Details** returns 30+ fields — title, tagline, property type, all photos, property highlights, full location with coordinates, host name, verification status, host rating, host review count, years hosting, overall rating, review count, guest favorite status, rating breakdown by category (cleanliness, accuracy, check-in, communication, location, value), full pricing with itemized costs, cancellation terms, and availability status.

All in structured JSON. Ready to use in your app.

### How accurate is the data?

Data is pulled from Airbnb in real time. Every API call fetches live data — not cached or stale results. Prices, availability, ratings, and host info reflect what's on Airbnb right now.

### Can I search any destination worldwide?

Yes. Pass any city, neighborhood, or landmark as `destination_query`. Tokyo, Paris, New York, Bali, a specific neighborhood like "Shibuya" — it all works. The API returns listings exactly as Airbnb shows them for that destination.

### Do I need check-in / check-out dates?

No. Dates are optional. Without dates, you get listings with base pricing. With dates, you get date-aware pricing including nightly rates, discounts, and total cost for your exact stay.

### What's the difference between Search Listings and Listing Details?

**Search Listings** finds available properties matching a destination and travel dates — like typing a city into the Airbnb search bar. You get pricing, photos, location, and key stats for each result.

**Listing Details** gives you the deep dive on a single property — host profile, rating breakdown by category, cancellation terms, availability, guest favorite status, and more.

Use Search to discover listings. Use Details to get the full picture on one.

## Rate Limits

| Plan | Price | Requests/Month |
|------|-------|----------------|
| Free | $0 | 5,000 |
| Starter | $25 | 100,000 |
| Grow | $75 | 1,000,000 |
| Scale | $150 | 10,000,000 |

## Questions? We have answers.

Reach out anytime. We will solve your query within 1 working day.

[![Contact Us on WhatsApp about Airbnb Scraper](https://raw.githubusercontent.com/omkarcloud/assets/master/images/whatsapp-us.png)](https://api.whatsapp.com/send?phone=918178804274&text=I%20have%20a%20question%20about%20the%20Airbnb%20Scraper%20API.)

[![Contact Us on Email about Airbnb Scraper](https://raw.githubusercontent.com/omkarcloud/assets/master/images/ask-on-email.png)](mailto:happy.to.help@omkar.cloud?subject=Airbnb%20Scraper%20API%20Question)
