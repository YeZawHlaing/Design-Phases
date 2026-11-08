# Style OS: Interactive Trend Discovery & Body-Matching Platform (Myanmar MVP)

> **Replace passive scrolling with active style decisions.** Style OS is a demand-first, community-driven social commerce platform tailored for Gen Z and Millennials in Myanmar. It pairs a gamified daily "Fit Check or Skip" voting game with hyper-local context discovery ("Places") and physical fit predictions powered by personal body metrics and digital closets.

---

##  Table of Contents

- [Key Features](#-key-features)
- [System Architecture](#-system-architecture)
- [Database Schema (ERD Entities)](#-database-schema-erd-entities)
- [Algorithm & Personalization Engine](#-algorithm--personalization-engine)
- [Getting Started](#-getting-started)
- [Project Structure](#-project-structure)
- [Growth & Virality Strategy](#-growth--virality-strategy)
- [License & Contribution](#-license--contribution)

---

##  Key Features

### 1.  "Places" Contextual Outfit Discovery
Solves the daily dilemma: *"What should I wear to [Place] today?"* 
Users select from 10 hyper-local venues (Coffee Shops, Pagodas/Temples, Corporate Offices, Universities, Parks, Bars/Night Out, Malls, Travel Getaways, Weddings, Gyms) to discover top-trending outfits validated by people with their exact body type.

### 2.  "Fit Check or Skip" Daily Voting Game
An interactive 10-card daily check-in stack (or visual grid loop). Users swipe **FIT** or **SKIP** on real creator outfits and cosmetic combos. Completing the daily game yields real-time community consensus stats (`"84% voted FIT like you"`) and unlocks daily venue recommendations.

### 3.  Smart Closet & Beauty Cabinet
Users log personal body metrics (Height, Weight, Shoulder Width, Foot Size, Skin Tone/Undertone, Skin Type) alongside physical items they own. The system generates a real-time **Fit Match Confidence Score (%)** on creator posts to ensure clothes look good *and* physically fit.

### 4.  Creator Vlogs & Style Mindset Reviews
Micro-creators and community users post short cosmetic application vlogs, 15-second wear tests, and budget fashion reviews (e.g., `#ThriftVsBrand`), tagging exact items and cosmetics.

### 5.  Seller Boutique Profiles (Sub-Feature)
Local fashion boutiques and online shops create lightweight profiles linked directly to tagged products in trending vlogs, converting community hype into organic sales without disruptive ads.

---

## System Architecture

The system operates on a **Decoupled Client-Server Architecture** optimized for high-volume swipe telemetry and dynamic vector filtering.

```
       +-------------------------------------------------+
       |           Mobile App / Web Frontend             |
       |  (UI Widgets, Swipe Gesture Deck, Places Grid)   |
       +------------------------+------------------------+
                                |
                        REST / GraphQL API
                                |
       +------------------------v------------------------+
       |             Backend API Service                 |
       |  (Auth, Body Matcher, Velocity Engine, Feeds)    |
       +------------------------+------------------------+
                                |
        +-----------------------+-----------------------+
        |                                               |
+-------v-------+                               +-------v-------+
| Relational DB |                               | Analytics /   |
| (MySQL/Postgre|                               | Vector Engine |
| Users, Posts, |                               | (Clustering & |
| Places, Logs) |                               | Trend Scoring)|
+---------------+                               +---------------+
```

---

##  Database Schema (ERD Entities)

The data model connects user body profiles, swipe behavior, item logs, and venues across 15 core entities:

1. **`users`**: Auth credentials, profile metadata, location.
2. **`user_body_metrics`**: Height, weight, shoulder width, foot size, skin tone, undertone, skin type.
3. **`user_preferences`**: Aesthetic tag subscriptions (#Streetwear, #CleanGirl, etc.).
4. **`places`**: The 10 core context venues (Coffee Shop, Temple, Office, etc.).
5. **`posts`**: Creator and user content (images, video reels, captions).
6. **`post_items`**: Individual tagged apparel and cosmetics within a post.
7. **`post_places`**: Junction table mapping posts to target venue contexts.
8. **`hashtags`**: 6-tier taxonomy tags for categorization.
9. **`post_hashtags`**: Junction table mapping posts to hashtags.
10. **`votes`**: Telemetry log of every FIT/SKIP swipe per user per post.
11. **`closet_items`**: User-owned wardrobe inventory.
12. **`beauty_cabinet_items`**: User-owned cosmetic/skincare inventory with shade codes.
13. **`user_streaks`**: Daily voting game streak tracking (` Day Count`).
14. **`seller_profiles`**: Merchant storefront profiles.
15. **`seller_products`**: Product catalog linked to seller profiles and tagged post items.

---

##  Algorithm & Personalization Engine

For every post or 2D/3D card shown in the app, the engine computes a **Personalized Fit Match Score ($S$)**:

$$S = (W_1 \times \text{TVI}) + (W_2 \times \text{TasteVector}) + (W_3 \times \text{BodySimilarity}) + (W_4 \times \text{ClosetMatch})$$

Where:
* **Trend Velocity Index (TVI):** $\frac{\text{Fit Swipes (Last 24h)}}{\text{Total Views}} \times \text{Creator Weight}$
* **TasteVector:** Alignment between past "FIT" swipes and post hashtags.
* **BodySimilarity:** Clustering match across height, weight, shoulder width, and skin undertone.
* **ClosetMatch:** Synergy between tagged outfit pieces and items in the user's Smart Closet.

---

##  Growth & Virality Strategy

* **Watermarked "Style Match" Share Cards:** Auto-generated visual cards summarizing a user's daily fit twin match percentage, watermarked for instant posting to Facebook Stories & TikTok.
* **30-Day Micro-Creator Seeding:** Onboarding 30–50 local Myanmar creators (5k–30k followers) to seed high-quality content across all 10 Places.
* **#MMFitBattle Challenges:** Weekly gamified voting competitions rewarding high-ranking community stylists with local brand vouchers and verification badges.

---


##  License

This project is proprietary and confidential. All rights reserved.
