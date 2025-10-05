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
```

---

## 🧠 How It Works

- **Schemas** define scalar traits (0–1 floats), tags (binary), and categoricals (multi-select).  
- **Weights** express importance for each scalar.  
- **Filters** (tags + categoricals) narrow the search space.  
- **Scores** are calculated via the chosen `engine.scoring` method — by default `"manhattan-lite"`.  
- **Bundles** are self-contained, portable, and editable in any text editor.

---

## ⚙️ Run It

### Locally
```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

### GitHub Pages
This repo is already configured for GitHub Pages:  
👉 **https://andrew-t-fielden.github.io/affinari_lite/**

You can also specify a bundle directly:

```
https://andrew-t-fielden.github.io/affinari_lite/?bundle=/bundles/duck_test_v0-bundle.json
```

---

## 🪄 Create Your Own Bundle (via ChatGPT)

[![Open in ChatGPT](https://img.shields.io/badge/Open_in_ChatGPT-00a37f?logo=openai&logoColor=white&style=for-the-badge)](https://chat.openai.com/?q=You%20are%20ChatGPT%20(GPT-5)%20Help%20me%20create%20a%20single-file%20Affinari%20Lite%20bundle%20for%20my%20domain%2C%20following%20the%20JSON%20structure%20in%20the%20reference%20export%20(bundle_version%2C%20created_at%2C%20schema%2Fengine%2Ftraits%2Fdefaults%2C%20items%2C%20profiles).%20Use%20my%20repo%20for%20conventions%3A%20https%3A%2F%2Fgithub.com%2FAndrew-T-Fielden%2Faffinari_lite.%20Tasks%3A%201)%20Propose%20traits.%202)%20Produce%20a%20single%20JSON%20%3Cdomain%3E_v0-bundle.json.%203)%20Include%205%E2%80%9310%20items.%204)%20Scoring%3A%20method%3Dmanhattan-lite%2C%20normalization%3Dweights_sum%2C%20missing_scalar%3Dignore.%205)%20Return%20the%20bundle%20and%20a%20short%20README.%20)

This button opens ChatGPT with an instruction that will:
1. Generate 3–7 scalar traits, tags, and categoricals for your chosen domain.  
2. Build a valid `*_v0-bundle.json` following the Affinari schema.  
3. Provide 5–10 example items.  
4. Return both the bundle and a short README snippet describing where to place it (`/bundles/`).  

---

## 📂 Repository Layout

```
affinari_lite/
├─ index.html               # Core HTML app (loads any bundle)
├─ bundles/
│  ├─ duck_test_v0-bundle.json
│  └─ ...other bundles...
├─ assets/
│  └─ styles.css            # optional external stylesheet
└─ README.md
```

---

## 🧩 Extending It

- Create new bundles for different domains (`/bundles/<domain>_v0-bundle.json`).  
- Update the query string `?bundle=…` to switch between them.  
- Adapt the UI for extra scalar visualisations, graphs, or cosine-based “doppelganger” views.

---

## 🔗 Related Projects
- **Parent Project:** [Affinari](https://github.com/Andrew-T-Fielden/affinari)  
- **Affinari Lite Demo Page:** [GitHub Pages Deployment](https://andrew-t-fielden.github.io/affinari_lite/)

---

© 2025 Andrew T. Fielden — Open source for demonstration and educational use under the MIT License.
