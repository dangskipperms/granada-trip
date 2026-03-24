# Where to get real photos of a specific place

## What works

### 1. pyWikiCommons (Python package)
- pip install pyWikiCommons
- Downloads from Wikimedia Commons using the proper API
- The 403 errors we got were because of missing/wrong User-Agent headers
- Fix: set User-Agent to "AppName/1.0 (https://yoursite.org; email@example.org)"
- This is the Wikimedia-approved way to download
- Source: https://github.com/amckenna41/pyWikiCommons

### 2. Wikimedia REST API with proper User-Agent
- The API itself works fine (we confirmed this — search returns results, metadata works)
- The image CDN blocks requests without a proper User-Agent that follows their policy
- Policy: https://meta.wikimedia.org/wiki/User-Agent_policy
- Must include: app name, version, URL, and contact email
- Source: https://api.wikimedia.org/wiki/Reusing_free_images_and_media_files_with_Python

### 3. Flickr API
- Free API key required (easy to get)
- flickr.photos.search with bounding box (lat/lon) returns geotagged photos
- flickr.photos.geo.photosForLocation for specific coordinates
- Can filter by license (Creative Commons)
- Can filter by tags ("Ronda", "Puente Nuevo", etc.)
- Actual photos taken by real people at real places
- Source: https://www.flickr.com/services/api/flickr.photos.search.html

### 4. Google Places Photos API
- Requires Google Cloud API key
- Free tier: up to 25,000 requests/month
- Returns actual photos from Google Maps (user-submitted, real)
- Search by place name, get photo references, download
- Source: https://developers.google.com/maps/documentation/places/web-service/place-photos

### 5. Unsplash API
- Free, no auth needed for low volume
- Better than Pexels for location-specific (has location metadata)
- But still generic stock — not guaranteed to be the actual place
- Source: https://unsplash.com/developers

## What does NOT work

### Pexels
- Returns random stock photos that match keywords loosely
- A search for "Marbella" returns flowers, random women, Moroccan riads
- Useless for location-specific imagery

### Direct Wikimedia curl without User-Agent
- Returns HTML redirect pages or 403 errors
- The CDN blocks anonymous/bot-like requests

### AI-generated images (kie.ai, DALL-E, etc.)
- Generates fake photos that look plausible but are not real
- Costs money
- Dishonest to present as real place photos

## Recommendation

Try pyWikiCommons first — it handles the User-Agent and API dance properly.
If that fails, use Flickr API with a free key.
As last resort, use remote Wikimedia URLs directly in HTML (browsers load them fine).
