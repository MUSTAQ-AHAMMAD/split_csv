# CSV Splitter — Split by Customer

A fully self-contained, single-page web application that splits a CSV file into separate files — one per customer — entirely in your browser. No server required. No data ever leaves your device.

---

## 🚀 Live Demo / Usage

1. Open `index.html` in any modern browser (Chrome, Edge, Firefox, Safari).
2. Drag & drop your CSV file onto the upload zone, or click **Browse**.
3. Configure the **Sales Order column**, **Date column**, and **separator character** (default `/`).
4. Choose **CSV** or **Excel (.xlsx)** output format.
5. Click **⚡ Split CSV**.
6. Download individual files with the **⬇ Download** button per row, or grab everything as a **ZIP archive**.

---

## ✨ Features

### 📤 Upload
- Drag & drop zone with animated border on hover
- Click-to-browse fallback
- Shows file name, size, row count, and column count after loading
- Clear/reset button to start over
- Supports `.csv` files — UTF-8 and UTF-8 BOM

### ⚙️ Configuration
- **Sales Order Column** — dropdown auto-populated from CSV headers; auto-selects the column matching "sales order" (case-insensitive)
- **Date Column** — dropdown auto-populated; auto-selects the column matching "date"
- **Separator character** — configurable text input (default `/`)
- **Output format** — CSV or Excel (.xlsx) toggle
- **Include Summary Sheet** — when Excel mode is selected, optionally add a "Summary" sheet listing all customers, row counts, date ranges, and unique transaction counts

### ⚡ Split & Results
- Animated progress bar while processing
- Results table with columns: #, Customer, File Name, Rows, Date Range, Unique Transactions, Download
- Per-row **⬇ Download** button
- **Download All as ZIP** button (top right of results)
- **Export Summary as CSV** button — one row per customer with stats
- Row hover highlight

### 🔍 Search & Filter
- Live search bar above the results table to filter by customer name instantly

### 👁 Customer Preview Modal
- Click any customer pill to open a modal showing the first 5 rows for that customer

### 📊 Statistics Bar
- Total rows processed
- Total customers found
- Date range of the entire file
- Total unique transaction numbers
- Animated count-up numbers

### 🌍 Encoding
- All output CSV files include a **UTF-8 BOM** prefix so Arabic and other non-ASCII text opens correctly in Excel
- File names are sanitized (no invalid characters)

### 💡 UX Polish
- Toast notifications (success, error, info) — slide in from the bottom-right corner
- Skeleton loader while parsing large files
- Smooth scroll to results after split
- Empty state message when no file is loaded

### 🎨 Design
- Deep navy dark-mode UI (`#0a0f1e` background)
- Glassmorphism cards with `backdrop-filter: blur`
- Animated gradient header title
- Subtle dot-grid CSS background pattern
- Fully responsive — works on mobile and desktop
- Google Font **Inter**

---

## 🏗 Tech Stack (CDN, no install needed)

| Library      | Version | Purpose           |
|--------------|---------|-------------------|
| PapaParse    | 5.4.1   | CSV parsing       |
| JSZip        | 3.10.1  | ZIP bundling      |
| SheetJS xlsx | 0.18.5  | Excel export      |
| Inter font   | —       | Typography        |

---

## 📁 File Structure

```
index.html   ← complete self-contained app (open directly in browser)
README.md    ← this file
```

---

## 🔑 How the Split Works

The app extracts the **customer name prefix** from the Sales Order Number column by splitting on the configured separator character (default `/`):

```
SALAMJED/73395          →  customer = SALAMJED
JOHNCO/12345            →  customer = JOHNCO
ACME/73322استرداد الأموال →  customer = ACME
```

All rows sharing the same prefix are grouped into a single output file named `<CUSTOMER>.csv` (or `.xlsx`).
