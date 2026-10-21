# SPSC IT & Robotics Club Application CV Generator

A minimal, modern, responsive, and privacy-first web application designed for students of **St. Philip's High School & College (SPSC)** to fill out the **SPSC IT & Robotics Club Member & Executive Application CV** directly in their browser and generate a professionally formatted, print-ready PDF document.

> **Live Preview & Static Hosting:** Fully compatible with GitHub Pages. Zero dependencies, zero build steps, and zero server backends required.

---

## Table of Contents

1. [Key Features](#key-features)
2. [Privacy & Security Architecture](#privacy--security-architecture)
3. [Language & Bengali Script Support](#language--bengali-script-support)
4. [Project Structure](#project-structure)
5. [Local Testing Instructions](#local-testing-instructions)
6. [GitHub Pages Deployment Guide](#github-pages-deployment-guide)
7. [Troubleshooting & Font/CDN Failures](#troubleshooting--fontcdn-failures)
8. [Browser Compatibility & Known Limitations](#browser-compatibility--known-limitations)
9. [Updating the Application](#updating-the-application)
10. [Copyright & Ownership](#copyright--ownership)

---

## 1. Key Features

- **Multi-Step Guided Workflow:** Breaks down the comprehensive application into 12 intuitive, numbered sections with real-time progress indicators, desktop & mobile section switchers, and bidirectional navigation.
- **Dynamic Repeatable Fields:** Allows students to add and remove technical skills (with proficiency levels), projects (with roles, durations, and links), achievements/awards, and extracurricular experiences on the fly.
- **Interactive 1–10 Soft Skills Assessment:** Easy-to-use, responsive rating pills for all 15 required soft skills with visible value tracking.
- **Embedded Transparent Official Club Logo:** Displays the authentic SPSC IT & Robotics Club emblem with full background transparency across both the responsive website header and generated PDF document headers.
- **Dual Final Action Buttons:** The final review screen (Section 14) provides two distinct, visible, independent action buttons on desktop, laptop, tablet, and mobile:
  - **Preview PDF:** Validates answers, generates the latest multi-page document, and opens the high-fidelity PDF preview modal for inspection.
  - **Download PDF:** Validates answers, generates the PDF directly from current form values with instant browser download, without requiring a prior preview.
- **Dynamic PDF Filename Generation:** Automatically sanitizes student inputs and names files in the exact club format:
  ```
  SPSC_ITRC_CV_FullName_Class_Roll.pdf
  ```
  *(Example: `SPSC_ITRC_CV_Mahir_Ahmed_11_25.pdf`)*
- **High-DPI PDF Generation:** Utilizes client-side rendering with automatic page-break avoidance (`break-inside: avoid;`) to prevent cut-off text, orphaned headers, or broken cards.
- **Embedded In-Browser PDF Preview:** Inspect the actual generated PDF document in a multi-page preview viewer before downloading.
- **Print / Save via Browser Fallback:** Built-in secondary print button formatted specifically for browser print-to-PDF dialogs.

---

## 2. Privacy & Security Architecture

This application was engineered with strict client-side data sovereignty:

- **100% Local Browser Execution:** No student information is ever transmitted to a server, database, cloud API, or third party.
- **Zero Local/Session Storage:** Student data is kept in JavaScript memory only during the active session. If the page is refreshed or closed, all data is immediately discarded. Each visit begins with a blank form.
- **No Analytics or Telemetry:** No Google Analytics, Meta Pixel, tracking beacons, or third-party monitoring scripts are present.
- **Strict DOM Text Escaping:** All user-supplied inputs (including long statements and links) are sanitized and escaped before rendering to prevent Cross-Site Scripting (XSS).
- **Safe Reset Action:** The "Reset Form" button asks for confirmation before clearing entered fields to prevent accidental loss.

---

## 3. Language & Bengali Script Support

The application user interface and section headers are in English, but students are explicitly welcome to write their answers in **Bengali** or **English**.

- **Bengali Unicode Rendering:** The PDF engine natively supports complex Bengali typography, including যুক্তাক্ষর (conjuncts such as `বিজ্ঞান`, `রক্ত`, `সৃষ্টি`, `পরীক্ষা`, `বিশ্ববিদ্যালয়`), কার, ফলা, হসন্ত (virama), and standard Bengali punctuation.
- **Embedded Web Typography:** Loads Google's `Noto Sans Bengali` alongside `Inter`, with robust fallbacks (`Hind Siliguri`, `Kalpurush`, `SolaimanLipi`, system fonts) to guarantee proper text shaping.

---

## 4. Project Structure

The entire application follows a strict single-file website architecture:

```
├── index.html     # Self-contained website (HTML5, CSS3, Vanilla JS, PDF engine)
└── README.md      # Documentation and deployment manual
```

No Node.js runtime, Webpack, Vite, npm packages, or external server configurations are needed to run or deploy the site.

---

## 5. Local Testing Instructions

You can run and test the website locally using any standard static file server or by opening the HTML file directly in your browser.

### Option A: Using Python (Recommended)
Open a terminal in the project directory and run:
```bash
python -m http.server 8000
```
Then navigate to: `http://localhost:8000/`

### Option B: Using Node.js
If you have Node.js installed:
```bash
npx serve .
```
Or with Node 20+:
```bash
node -e "const http=require('http'),fs=require('fs');http.createServer((q,s)=>fs.createReadStream('index.html').pipe(s)).listen(8000,()=>console.log('Listening on http://localhost:8000'))"
```

### Option C: Direct File Opening
Double-click `index.html` or drag it into Google Chrome, Microsoft Edge, Mozilla Firefox, or Safari.

---

## 6. GitHub Pages Deployment Guide

Hosting this website on GitHub Pages is free and takes less than two minutes:

### Step 1: Create a GitHub Repository
1. Log into your account at [github.com](https://github.com/).
2. Click the **+** (New repository) button in the upper right.
3. Name your repository (e.g. `spsc-itrc-cv-generator`).
4. Set the visibility to **Public**.
5. Do not initialize with a `.gitignore` or license. Click **Create repository**.

### Step 2: Upload Files
1. On the empty repository page, click **Upload an existing file**.
2. Drag and drop both `index.html` and `README.md` into the file upload box.
3. Type a commit message (e.g., `Initial release of SPSC ITRC CV Generator`) and click **Commit changes**.

*Alternative via Git command line:*
```bash
git init
git add index.html README.md
git commit -m "Initial release of SPSC ITRC CV Generator"
git branch -M main
git remote add origin https://github.com/<your-username>/spsc-itrc-cv-generator.git
git push -u origin main
```

### Step 3: Enable GitHub Pages
1. Go to your repository's **Settings** tab.
2. In the left navigation menu, click **Pages** (under the "Code and automation" section).
3. Under **Build and deployment** > **Source**, select **Deploy from a branch**.
4. Under **Branch**, select `main` and leave the folder set to `/ (root)`.
5. Click **Save**.

### Step 4: Access Your Live Website
- Within 1–2 minutes, GitHub will publish your static website.
- Refresh the **Pages** settings screen. You will see a green banner:
  > *"Your site is live at `https://<your-username>.github.io/spsc-itrc-cv-generator/`"*
- Click the URL to open your live application.

---

## 7. Troubleshooting & Font/CDN Failures

### What if a CDN is blocked or fails to load?
- The application includes an automated **CDN fallback** in `index.html`: if `cdnjs.cloudflare.com` fails to deliver `html2pdf.js`, the script dynamically loads the bundle from `jsdelivr.net`.
- In the unlikely event that external JavaScript CDNs are completely blocked on a student's network, the application displays a friendly notification and offers the **"Print / Save via Browser"** button, which formats the document directly for the browser's native print-to-PDF utility without requiring external PDF libraries.

### What if Bengali text appears in system default font?
- If Google Fonts (`fonts.googleapis.com`) is blocked or unreachable, the CSS incorporates system font fallbacks (`Hind Siliguri`, `Kalpurush`, `SolaimanLipi`, `Vrinda`). On modern Windows, macOS, iOS, and Android devices, system Bengali Unicode fonts automatically provide correct glyph shaping.

---

## 8. Browser Compatibility & Known Limitations

### Supported Browsers
- **Google Chrome & Chromium-based browsers:** Version 90+ (Windows, macOS, Android, Linux).
- **Microsoft Edge:** Version 90+ (Windows, macOS).
- **Mozilla Firefox:** Version 88+ (Desktop & Mobile).
- **Apple Safari:** Version 14+ (macOS & iOS/iPadOS).

### Known Limitations
- **Data Persistence:** Because the form deliberately operates without cookies or browser storage for maximum student privacy, refreshing the browser tab will reset entered answers. Students should complete their answers in one sitting or draft long answers in a text editor beforehand.
- **Mobile PDF Preview Restrictions:** On certain iOS Safari and mobile Chrome versions, embedded `<iframe>` PDF preview displays a scrollable preview or fallback prompt due to mobile OS sandboxing. The **Download PDF** and **Print / Save via Browser** actions work reliably across all mobile devices.

---

## 9. Updating the Application

To make changes to questions, styling, or instructions:
1. Edit `index.html` locally and verify in your browser.
2. Commit and push the updated `index.html` to your `main` branch on GitHub:
   ```bash
   git add index.html
   git commit -m "Update application questions"
   git push origin main
   ```
3. GitHub Pages automatically rebuilds and deploys the update within 60 seconds.

---

## 10. Copyright & Ownership

- **Website & Software Copyright:** © 2026 Mahir Ahmed. All rights reserved.
- **Club Ownership & Trademark:** SPSC IT & Robotics Club, St. Philip's High School & College.
