⚠️ **API UNDER MAINTENANCE**  

# R6Data API Documentation

Comprehensive API for accessing Rainbow Six Siege game data, player statistics, and service information. Get operators, weapons, maps, ranks, and player stats.

**Stats:**
- **11** Endpoints
- **100%** Uptime
- **Free** To Use

---

## Getting Started

### Introduction

The R6 API provides access to Rainbow Six Siege game data including operators, weapons, maps, player statistics, and more. All endpoints return JSON data and support various query parameters for filtering results.

### Base URL

```
https://r6-api.vercel.app
```

---

## Game Data

### Operators

Get information about Rainbow Six Siege operators including their stats, biographical data, and abilities.

**Endpoint:** `GET /api/operators`

#### Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `name` | string | Filter by operator name |
| `realname` | string | Filter by real name |
| `birthplace` | string | Filter by birthplace |
| `roles` | string | Filter by role (Attacker/Defender) |
| `side` | string | Filter by side |
| `health` | number | Filter by minimum health |

#### Example Request

```javascript
fetch('https://r6-api.vercel.app/api/operators?name=ash&roles=attacker')
  .then(response => response.json())
  .then(data => console.log(data));
```

#### Example Response

```json
[
  {
    "name": "Ash",
    "safename": "ash",
    "realname": "Eliza Cohen",
    "birthplace": "Jerusalem, Israel",
    "age": "33",
    "date_of_birth": "December 24, 1983",
    "season_introduced": "Release",
    "health": 100,
    "speed": "3",
    "unit": "FBI SWAT",
    "country_code": "us",
    "roles": "Attacker",
    "side": "ATK",
    "icon_url": "https://example.com/ash.png"
  }
]
```

---

### Weapons

Access information about weapons available in Rainbow Six Siege.

**Endpoint:** `GET /api/weapons`

#### Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `name` | string | Filter by weapon name |

#### Example Request

```javascript
fetch('https://r6-api.vercel.app/api/weapons?name=R4-C')
  .then(response => response.json())
  .then(data => console.log(data));
```

---

### Maps

Get information about Rainbow Six Siege maps including location, release date, and available playlists.

**Endpoint:** `GET /api/maps`

#### Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `name` | string | Filter by map name |
| `location` | string | Filter by location |
| `playlists` | string | Filter by available playlists |
| `releaseDate` | string | Filter by release date |

#### Example Response

```json
[
  {
    "name": "Oregon",
    "location": "Oregon, USA",
    "releaseDate": "2015-12-01",
    "playlists": "Ranked, Casual, Unranked",
    "mapReworked": "Y5S3"
  }
]
```

---

### Seasons

Information about Rainbow Six Siege seasons including operators, maps, and release dates.

**Endpoint:** `GET /api/seasons`

#### Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `name` | string | Filter by season name |
| `code` | string | Filter by season code (e.g., Y8S4) |
| `map` | string | Filter by season map |
| `operators` | string | Filter by operators introduced |

---

### Ranks

Get ranking system information for different seasons of Rainbow Six Siege.

**Endpoint:** `GET /api/ranks`

#### Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `version` | string | **Required:** Rank version (v1, v2, v3, v4, v5, v6) |
| `name` | string | Filter by rank name |
| `min_mmr` | number | Filter by minimum MMR |
| `max_mmr` | number | Filter by maximum MMR |

#### Example Request

```javascript
fetch('https://r6-api.vercel.app/api/ranks?version=v6&name=diamond')
  .then(response => response.json())
  .then(data => console.log(data));
```

---

### Game Stats

Get real-time player count statistics across all platforms including Steam, Ubisoft Connect, PlayStation, Xbox, and total player counts.

**Endpoint:** `GET /api/stats?type=gameStats`

No additional parameters required. Returns current player statistics for all platforms.

#### Example Request

```javascript
fetch('https://r6-api.vercel.app/api/stats?type=gameStats')
  .then(response => response.json())
  .then(data => console.log(data));
```

#### Example Response

```json
{
  "steam": {
    "concurrent": 33631,
    "estimate": 33631
  },
  "crossPlatform": {
    "totalRegistered": 85000000,
    "monthlyActive": 15300000,
    "trendsEstimate": 175666,
    "platforms": {
      "pc": 6885000,
      "playstation": 5355000,
      "xbox": 3060000
    }
  },
  "ubisoft": {
    "onlineEstimate": 127739
  },
  "lastUpdated": "2025-10-15T22:39:38.636Z"
}
```

---

## Cosmetics

### Universal Skins

Access universal weapon skins available in Rainbow Six Siege.

**Endpoint:** `GET /api/universalSkins`

#### Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `name` | string | Filter by skin name |

---

### Charms

Get information about weapon charms in Rainbow Six Siege.

**Endpoint:** `GET /api/charms`

#### Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `name` | string | Filter by charm name |
| `collection` | string | Filter by collection |
| `rarity` | string | Filter by rarity |
| `availability` | string | Filter by availability |
| `season` | string | Filter by season |

---

### Attachments

Access weapon attachment information including styles and availability.

**Endpoint:** `GET /api/attachment`

#### Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `name` | string | Filter by attachment name |
| `style` | string | Filter by style |
| `rarity` | string | Filter by rarity |

---

## Player Data

### Player Stats

Get player statistics and account information from Ubisoft's Rainbow Six Siege API.

**Endpoint:** `GET /api/stats`

#### Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `type` | string | **Required:** "accountInfo" or "stats" |
| `nameOnPlatform` | string | **Required:** Player username |
| `platformType` | string | **Required:** Platform (uplay, psn, xbl) |
| `platform_families` | string | Required for stats: Platform family (pc, console) |

#### Example Request - Account Info

```javascript
fetch('https://r6-api.vercel.app/api/stats?type=accountInfo&nameOnPlatform=PlayerName&platformType=uplay')
  .then(response => response.json())
  .then(data => console.log(data));
```

#### Example Request - Player Stats

```javascript
fetch('https://r6-api.vercel.app/api/stats?type=stats&nameOnPlatform=PlayerName&platformType=uplay&platform_families=pc')
  .then(response => response.json())
  .then(data => console.log(data));
```

---

### Seasonal Stats

Get detailed rank points history and seasonal progression for a specific player in the current season. Includes timestamp, rank information, RP values, and rank images.

**Endpoint:** `GET /api/stats?type=seasonalStats`

#### Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `type` | string | **Required:** "seasonalStats" |
| `nameOnPlatform` | string | **Required:** Player username |
| `platformType` | string | **Required:** Platform (uplay, psn, xbl, steam) |

#### Example Request

```javascript
fetch('https://r6-api.vercel.app/api/stats?type=seasonalStats&nameOnPlatform=PlayerName&platformType=uplay')
  .then(response => response.json())
  .then(data => console.log(data));
```

#### Example Response

```json
{
  "data": {
    "history": {
      "metadata": {
        "key": "RankPoints",
        "name": "Rank Points",
        "description": null
      },
      "data": [
        [
          "2025-10-14T21:43:27.315+00:00",
          {
            "displayName": "Rank Points",
            "metadata": {
              "rank": "PLATINUM II",
              "imageUrl": "https://r6data.eu/assets/img/r6_ranks_img/platinum-2.webp",
              "color": "#44ccc2"
            },
            "value": 3300,
            "displayValue": "3,300",
            "displayType": "Number"
          }
        ],
        [
          "2025-10-14T21:12:55.821+00:00",
          {
            "displayName": "Rank Points",
            "metadata": {
              "rank": "PLATINUM II",
              "imageUrl": "https://r6data.eu/assets/img/r6_ranks_img/platinum-2.webp",
              "color": "#44ccc2"
            },
            "value": 3302,
            "displayValue": "3,302",
            "displayType": "Number"
          }
        ]
      ]
    },
    "leaderboard": null,
    "expiryDate": "0001-01-01T00:00:00+00:00",
    "bestMatches": null
  }
}
```

#### Response Details

- **history.data**: Array of rank point entries, each containing a timestamp and stats object
- **value**: Current MMR/rank points for that match
- **metadata.rank**: Rank name at that point in time
- **metadata.imageUrl**: Direct link to rank badge image (from R6Data CDN)
- **metadata.color**: Hex color code for the rank tier

---

## Utilities

### Global Search

Search across all game data with a single query.

**Endpoint:** `GET /api/searchAll`

#### Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `q` | string | **Required:** Search query |

#### Example Request

```javascript
fetch('https://r6-api.vercel.app/api/searchAll?q=ash')
  .then(response => response.json())
  .then(data => console.log(data));
```

#### Example Response

```json
{
  "query": "ash",
  "summary": {
    "total": 2,
    "operators": 1,
    "weapons": 1,
    "maps": 0,
    "seasons": 0,
    "charms": 0,
    "attachments": 0
  },
  "results": {
    "operators": [...],
    "weapons": [...],
    "maps": [],
    "seasons": [],
    "charms": [],
    "attachments": []
  }
}
```

---

### Service Status

Get real-time Rainbow Six Siege server status information.

**Endpoint:** `GET /api/servicestatus`

No parameters required. Returns current server status for all platforms.

#### Example Response

```json
[
  {
    "name": "PC",
    "status": "Online",
    "services": [
      "Game Services: Online",
      "Online Features: Online"
    ]
  },
  {
    "name": "PlayStation",
    "status": "Online",
    "services": [
      "Game Services: Online",
      "Online Features: Online"
    ]
  }
]
```

---

**Documentation by R6Data Team**

