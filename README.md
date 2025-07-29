# Wikipedia Alt Checker 🖼️

Python script to list all pages in a given Wikipedia category and check whether image links include alternative text (`alt`) in the wikitext.

---

## 📦 Overview

- Retrieves all pages from a specified Wikipedia category.  
- Extracts the raw wikitext for each page using the MediaWiki API.  
- Identifies image links (e.g., `[[File:...]]`, `[[Image:...]]`, `[[Ficheiro:...]]`) in the wikitext.  
- Verifies whether each image includes the `alt=` parameter or numbered variants (`alt1`, `alt2`, ...).  
- Outputs a summary for each page showing:
  - total number of images;
  - number of images with `alt`;
  - number of images without `alt`.

---

## 🚀 Features

- Language support: accepts `--lang pt`, `--lang en`, etc. Automatically handles the correct category namespace (`Categoria:` or `Category:`).
- Normalizes titles by replacing spaces with underscores and handling accented characters.
- Optional page limit for testing purposes (`--limit`).
- Prints page-by-page report and a final global summary.

---

## 🛠️ Setup

### Requirements

- Python 3.7+
- `requests` library:
  ```bash
  pip install requests
  ```

### Usage

Download or clone this repository and run:
```bash
python wikipedia_alt_checker.py --category "CATEGORY NAME" --lang LANGUAGE
```

Examples:
```bash
python wikipedia_alt_checker.py --category "Animais do Brasil" --lang pt
python wikipedia_alt_checker.py --category "Animals by continent" --lang en
```

Limit the number of pages for testing:
```bash
python wikipedia_alt_checker.py --category "Animais do Brasil" --lang pt --limit 5
```

---

## 📄 Sample Output

Example output for the category `"Animais do Brasil"`:

```
Page: Jaguar (Panthera onca)
‑ Total images: 3 | With alt: 2 | Without alt: 1

Page: Arara‑azul (Anodorhynchus hyacinthinus)
‑ Total images: 2 | With alt: 2 | Without alt: 0

Global summary:
‑ Pages processed: 10
‑ Images found: 20
‑ With alt: 15
‑ Without alt: 5
```

---

## 🧠 Code Structure

- `normalize_title(title, lang)`: normalizes titles for API queries.
- `get_category_members(category_title, lang, limit=None)`: gets page titles in a category.
- `get_wikitext(page_title, lang)`: retrieves wikitext via API.
- `find_image_links(wikitext)`: extracts image links from wikitext.
- `has_alt_param(link)`: detects presence of `alt=`.
- `main()`: coordinates workflow and prints report.

---

## 📝 Technical Notes

- Uses the public MediaWiki API (no authentication required).
- Follows Wikimedia's [User-Agent Policy](https://meta.wikimedia.org/wiki/User-Agent_policy).
- Supports UTF-8 titles and resolves spaces/accents for accurate querying.
- Handles edge cases: pages with no images, API errors, empty content.

---

## ♿ Accessibility Context

Alternative text (`alt`) improves accessibility by describing image content to screen readers. This script helps identify articles where `alt=` should be added for inclusivity and compliance with accessibility standards.

---

## 🧪 Testing

Run with various categories and parameters:
```bash
python wikipedia_alt_checker.py --category "Brazilian flags" --lang en --limit 3
python wikipedia_alt_checker.py --category "Ocean animals" --lang en
```

---

## 💡 Future Improvements

- Export results to JSON or CSV.
- Add web interface or HTML reporting.
- Expand support to other Wikimedia projects and language-specific image prefixes.
- Parallelize API calls for large categories.

---

## 🧾 License

Distributed under the **MIT License** — feel free to use, modify, and contribute!
