# Indian States and Districts JSON Dataset (Latest, Official Source)

![Data Source](https://img.shields.io/badge/source-Official%20Government%20Site-blue)
![Format](https://img.shields.io/badge/format-JSON-green)
![Updated](https://img.shields.io/badge/status-Latest%20Data-success)
![Includes](https://img.shields.io/badge/includes-Scraper%20%2B%20Data-orange)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

This repository provides the **latest Indian states and districts JSON dataset**, along with the **browser-based scraper code** used to generate it.
The data is sourced directly from an **official Indian government website** and includes **both the generated JSON file and the scraper code**.

Source website:
[https://igod.gov.in/sg/district/states](https://igod.gov.in/sg/district/states)

---

## Why This Repository Exists

Developers commonly search for:

* Indian states and districts JSON
* District list of India in JSON format
* India state district dropdown data
* Indian address data for forms and APIs

Most available datasets are outdated, incomplete, or not traceable to an official source.
This repository solves that by enabling **direct, reproducible extraction from a government portal**.

---

## What This Repository Contains

### 1. Ready-to-Use JSON File

* Latest available states and districts
* Clean, minimal structure
* Suitable for frontend, backend, APIs, and databases

### 2. Browser-Based Scraper Code

* Runs directly in the browser console
* No Node.js or dependencies
* No CORS issues
* Can be re-run anytime to refresh data

---

## Data Source

All data is extracted from the official Indian government portal:

[https://igod.gov.in/sg/district/states](https://igod.gov.in/sg/district/states)

This ensures:

* Authentic data
* Verifiable source
* Transparency
* Long-term reliability

---

## JSON Structure

```json
[
  {
    "state": "West Bengal",
    "districts": [
      "Kolkata",
      "Howrah",
      "Darjeeling"
    ]
  },
  {
    "state": "Maharashtra",
    "districts": [
      "Mumbai",
      "Pune",
      "Nagpur"
    ]
  }
]
```

### Structure Rationale

* Flat and predictable
* Easy to map to dropdowns
* Simple to extend with codes or metadata
* Language-agnostic

---

## How to Generate the Latest Dataset

### Step 1: Open the Official Website

Navigate to:

```
https://igod.gov.in/sg/district/states
```

---

### Step 2: Open Developer Tools

* Windows / Linux: `F12` or `Ctrl + Shift + I`
* macOS: `Cmd + Option + I`

Switch to the **Console** tab.

---

## Running the Scraper

### Option A: Paste Directly in Console (Default)

Paste the script below into the browser console and press Enter.

```js
(async () => {
  const stateLinks = Array.from(
    document.querySelectorAll(".state li a")
  ).map(a => ({
    state: a.innerText.trim(),
    url: a.href
  }));

  const result = [];

  for (const item of stateLinks) {
    const response = await fetch(item.url);
    const html = await response.text();

    const parser = new DOMParser();
    const doc = parser.parseFromString(html, "text/html");

    const districts = Array.from(
      doc.querySelectorAll(".search-row .search-title")
    ).map(el => el.innerText.trim());

    result.push({
      state: item.state,
      districts
    });
  }

  const json = JSON.stringify(result, null, 2);
  const blob = new Blob([json], { type: "application/json" });
  const url = URL.createObjectURL(blob);

  const a = document.createElement("a");
  a.href = url;
  a.download = "india-states-districts-latest.json";
  a.click();

  URL.revokeObjectURL(url);
})();
```

---

### Option B: If Pasting Is Disabled in the Console

Some environments (managed browsers, enterprise devices, hardened profiles) **disable paste in DevTools**.

In that case:

1. Type this manually in the console:

   ```js
   allow pasting
   ```

   Press Enter.

2. Paste the script again.

This is a built-in Chrome / Edge safety prompt and is expected behavior.

---

### Option C: Manual Injection (No Paste at All)

If paste is completely blocked:

1. Create a new **Snippet** in DevTools:

   * DevTools → Sources → Snippets → New Snippet
2. Paste the code there
3. Right-click → Run

This works even in restricted environments.

---

## Output

The browser will automatically download:

```
india-states-districts-latest.json
```

This file reflects the **current data at the time of execution**.

---

## Use Cases

* Indian address forms
* State and district dropdowns
* Government and civic applications
* College and university projects
* Location-based filtering
* APIs and microservices
* Data analysis and research

---

## Keeping the Data Updated

Districts and administrative boundaries may change.

To update:

1. Visit the source website again
2. Re-run the scraper
3. Replace the JSON file in the repository

This approach ensures freshness without relying on third parties.

---

## Accuracy and Responsibility

* Data comes directly from a public government source
* No automated crawling or abuse
* Fully transparent extraction logic
* Users should validate data for mission-critical use

---

## License

MIT License.
Free to use, modify, and distribute.

---

## Maintainer

Maintained by **Somen Das**.

---

## SEO Target Keywords

Indian states districts JSON
India district list JSON
Indian address dataset
State district dropdown India
Indian geography data
Government district data India
igod.gov.in districts

