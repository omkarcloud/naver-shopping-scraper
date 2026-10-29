# 🛍️ Naver Shopping Scraper

Naver Shopping Scraper is a **free and open-source** scraper that gets you **unlimited** detailed Naver Shopping data for free.

## ✨ What Can I Get?

- 🛍️ **Full details on millions of products** — price & discounts, every option with stock, add-ons, description, specs, review stats & seller
- 🔍 **96 products per search** — price, category, delivery & brand-store filters, plus the live match count (5M+ for "necklace" alone)
- ⭐ **Every review & every store** — 20 reviews per page with photos and star breakdown, store profiles, best-sellers & popular products
- 📈 **Top 500 trending keywords per category** — Naver DataLab click trends since 2017, by day, week or month, split by device, gender & age

## 💎 Example: A Full Naver Shopping Product

```json
{
  "id": "8087042745",
  "name": "14k 여자목걸이 금 여성 하트 선물",
  "link": "https://smartstore.naver.com/dailyromantic/products/8087042745",
  "catalog_id": "85631543068",
  "status": "SALE",
  "pricing": { "sale_price": 298100, "discounted_price": 227100, "discount_ratio": 23, "seller_discount": 71000, "currency": "KRW" },
  "stock_quantity": 25408,
  "images": ["https://shop-phinf.pstatic.net/20260620_6/1781935858848eGfQY_PNG/24011891765105689_1221774915.png"],
  "category": { "id": "50004168", "name": "14K목걸이", "path": ["패션잡화", "주얼리", "목걸이", "14K목걸이"] },
  "brand": "데일리로맨틱",
  "tags": ["20대여자생일선물", "여자친구목걸이", "14k목걸이선물"],
  "reviews": {
    "count": 2508,
    "average_score": 4.86,
    "score_counts": { "1": 5, "2": 9, "3": 52, "4": 199, "5": 2243 },
    "photo_count": 1292,
    "recent": { "count": 209, "average_score": 4.79 }
  },
  "variants": [
    { "id": "37158451756", "name": "하트 목걸이+ 곰인형 + 쇼핑백 / 골드 / 14k 목걸이", "extra_price": 0, "stock_quantity": 490 },
    { "id": "37158451757", "name": "하트 목걸이+ 곰인형 + 쇼핑백 / 골드 / 18k 목걸이", "extra_price": 69000, "stock_quantity": 683 }
  ],
  "delivery": { "fee_type": "FREE", "is_free": true, "company": "CJ대한통운" },
  "store": { "id": "500278691", "name": "데일리로맨틱", "link": "https://smartstore.naver.com/dailyromantic", "type": "smart_store", "grade": "FIRST" }
}
```

*Trimmed for readability.*

## 🚀 Unlimited Free Naver Shopping Data — Get It in 60 Seconds

1️⃣ Clone and install:
```bash
git clone https://github.com/omkarcloud/naver-shopping-scraper
cd naver-shopping-scraper
python -m pip install -r requirements.txt
```

2️⃣ Start the API:
```bash
python run.py
```

3️⃣ Get your first data:
```bash
curl "http://localhost:8000/products/details?product=https://smartstore.naver.com/dailyromantic/products/8087042745"
```

```json
{
  "id": "8087042745",
  "name": "14k 여자목걸이 금 여성 하트 선물",
  "link": "https://smartstore.naver.com/dailyromantic/products/8087042745",
  "status": "SALE",
  "pricing": { "sale_price": 298100, "discounted_price": 227100, "discount_ratio": 23, "currency": "KRW" },
  "stock_quantity": 25408,
  "category": { "id": "50004168", "name": "14K목걸이", "path": ["패션잡화", "주얼리", "목걸이", "14K목걸이"] },
  "reviews": { "count": 2508, "average_score": 4.86, "photo_count": 1292 },
  "option_groups": [
    { "id": "8011013232", "name": "목걸이 종류(품질 보증서 有)", "type": "COMBINATION" },
    { "id": "7671263787", "name": "색상", "type": "COMBINATION" }
  ],
  "variants": [
    { "id": "37158451758", "name": "하트 목걸이+ 곰인형 + 쇼핑백 / 핑크골드 / 14k 목걸이", "extra_price": 10000, "stock_quantity": 538 }
  ],
  "store": { "name": "데일리로맨틱", "link": "https://smartstore.naver.com/dailyromantic", "grade": "FIRST", "sale_count": 540 }
}
```

All 11 endpoints are now live at `http://localhost:8000`.

Search, counts, store profiles and the DataLab insights run as plain HTTP. Product details, reviews, store product lists and catalog reviews are answered by Naver only inside a real browser page, so they need **Google Chrome** installed: on the first such call Chrome opens once (about 10 seconds), then stays open, so every call after that takes a second or two.

Naver answers most connections directly. If it ever starts refusing yours (HTTP 418 or 429 errors), restart with a proxy:

```bash
NAVER_SHOPPING_PROXY="http://user:pass@host:port" python run.py
```

## 📚 Endpoints

11 endpoints cover everything you need.

| Endpoint | Path | Returns |
|---|---|---|
| Product Details | `/products/details` | Price, every option with stock, description, specs & review stats in one call |
| Search Products | `/products/search` | Up to 96 products per keyword, with price, category & delivery filters |
| Count Products | `/products/count` | The exact number of products matching a keyword and filters |
| Product Reviews | `/products/reviews` | 20 reviews per page: score, text, photos, option bought & star breakdown |
| Store Details | `/stores/details` | Grade, sales count, business info, social links & category tree |
| Store Products | `/stores/products` | A store's 20 popular products or 30 best-sellers by period |
| Catalog Reviews | `/catalogs/reviews` | Naver's review sample for any price-comparison catalog |
| Top Keywords | `/keywords/rank` | The top 500 trending keywords of any category, 20 per page |
| Keyword Trend | `/keywords/trend` | A keyword's click trend by day, week or month since 2017 |
| Category Trend | `/categories/trend` | A category's click trend plus device, gender & age split |
| Categories | `/categories/list` | The category tree with the IDs every insight endpoint takes |

Every `product`, `store` and `catalog` param takes an ID or any Naver link. Product names, store names and keywords come back in Korean, exactly as on Naver.

## 🔍 Exploring Parameters

The same API is published on RapidAPI, and its playground is the easiest place to try parameters and see raw responses. Once a request looks right, run it locally for **unlimited free** data.

1. [Subscribe to the free plan](https://rapidapi.com/OmkarCloud/api/best-naver-shopping-scraper-free-1000-calls/pricing) — 1,000 calls/month, no credit card.
2. [Try the endpoints in the playground](https://rapidapi.com/OmkarCloud/api/best-naver-shopping-scraper-free-1000-calls/playground) — every param is pre-filled, so you see real data in one click.
3. Copy the generated code and replace `https://best-naver-shopping-scraper-free-1000-calls.p.rapidapi.com` with `http://localhost:8000`. It will now run against your local API.

```python
import requests

# generated by the playground, host swapped for the local API
response = requests.get(
    "http://localhost:8000/products/search",
    params={"query": "raspberry pi", "max_price": 100000},
)
print(response.json())
```

## 💬 Have Questions? We Have Answers.

You're a developer — we know how hard completing a project can be. So we offer full support: just message us and we'll reply ✅ with a solution within 1 working day.

[![Message Us on WhatsApp about Naver Shopping Scraper](https://raw.githubusercontent.com/omkarcloud/assets/master/images/whatsapp-us.png)](https://api.whatsapp.com/send?phone=918178804274&text=I%20need%20help%20using%20the%20Naver%20Shopping%20Scraper%20API.)

[![Ask Us by Email about Naver Shopping Scraper](https://raw.githubusercontent.com/omkarcloud/assets/master/images/ask-on-email.png)](mailto:happy.to.help@omkar.cloud?subject=Help%20with%20Naver%20Shopping%20Scraper%20API&body=I%20need%20help%20using%20the%20Naver%20Shopping%20Scraper%20API.)

## ⚡ Popular Scrapers by Omkar Cloud

- [**Google Maps Scraper (3,100+ GitHub Stars)**](https://github.com/omkarcloud/google-maps-scraper) — type "dentists in New York", get every business as a ready-to-call lead list: phones, emails, websites & reviews. Up to 100K free leads/month.
- [**G2 Scraper**](https://www.omkar.cloud/tools/g2-scraper) — G2 product details, ratings & AI-found contacts
- [**Website Email Contact Scraper**](https://www.omkar.cloud/tools/website-email-contact-scraper) — emails, phones & socials from any website
- [**AliExpress Scraper**](https://www.omkar.cloud/tools/aliexpress-scraper-api) — live product details, SKU variants, stock & shipping
- [**Booking Scraper**](https://www.omkar.cloud/tools/booking-scraper) — Booking.com hotels: prices, ratings, rooms & amenities
- [**Etsy Scraper**](https://www.omkar.cloud/tools/etsy-scraper) — Etsy products: prices, discounts, shops & variations

## ⭐ Love It? [Star It ⭐!](https://github.com/omkarcloud/naver-shopping-scraper)

Star the repo ⭐ and become my star hero!

It's just 1 click, but it means the world to me.

[![Star us on GitHub](https://raw.githubusercontent.com/omkarcloud/google-maps-scraper/master/screenshots/star-us.png)](https://github.com/omkarcloud/naver-shopping-scraper)
