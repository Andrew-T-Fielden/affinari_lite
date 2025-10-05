# 🪶 Affinari Lite

**Affinari Lite** is a lightweight, bundle-based implementation of the [Affinari](https://github.com/Andrew-T-Fielden/affinari) engine.  
It demonstrates *transparent matching and discovery* using simple mathematics — not opaque machine learning.

Affinari Lite runs entirely in the browser.  
All data is local, schema-driven, and instantly editable.

---

## ✨ Core Idea

Affinari Lite uses **weighted Manhattan distance** for alignment —  
`alignment = 1 − (Σ wᵢ · |uᵢ − vᵢ|) / Σ wᵢ` —  
and optional **cosine similarity** for doppelganger comparisons.  

Every domain (restaurants, hotels, medical conditions, finance, etc.) can be described as a **bundle**:  
a single JSON file containing its schema, items, and optional profiles.

---

## 📦 Bundle Format

Each bundle (e.g. `duck_test_v0-bundle.json`) contains:

```jsonc
{
  "bundle_version": "0.1.0",
  "created_at": "2025-10-05T00:00:00.000Z",
  "schema": {
    "id": "my_domain_v0",
    "name": "My Domain",
    "engine": {
      "scoring": {
        "method": "manhattan-lite",
        "normalization": "weights_sum",
        "ties": [],
        "missing_scalar": "ignore"
      }
    },
    "traits": {
      "scalars": [{ "id": "trait_a", "name": "Trait A", "default": 0.5, "weight": 1 }],
      "tags": [{ "id": "feature_x", "name": "Feature X" }],
      "categoricals": [{
        "id": "category_y",
        "name": "Category Y",
        "options": [{ "id": "y1", "label": "Y1" }]
      }]
    },
    "defaults": {
      "weights": { "trait_a": 1 },
      "required_tags": [],
      "excluded_tags": [],
      "categorical_filters": {}
    }
  },
  "items": {
    "domain_schema_id": "my_domain_v0",
    "items": [
      {
        "id": "item_1",
        "name": "Example Item 1",
        "traits": {
          "scalars": { "trait_a": 0.7 },
          "tags": { "feature_x": true },
          "categoricals": { "category_y": ["y1"] }
        }
      }
    ]
  },
  "profiles": []
}
