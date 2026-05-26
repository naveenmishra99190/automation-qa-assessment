# Automation & QA Developer Assessment
### Naveen Mishra | May 2026

---

## 📋 Overview

This repository contains my submission for the **Automation & QA Developer Take-Home Skills Assessment**. The assessment tests web application debugging & QA, API integration, and n8n workflow design skills.

---

## 📁 Repository Structure

```
automation-qa-assessment/
│
├── Task1_QA_Report_NaveenMishra.docx       # Bug report with 8 issues found
├── Task2_README_NaveenMishra.docx          # n8n workflow documentation
├── HackerNews Morning Digest.json          # Exported n8n workflow file
└── README.md                               # This file
```

---

## ✅ Task 1 — Web App QA & Debug Report

### App Tested
**Angular RealWorld Example App (Conduit)** — a blogging platform  
**URL:** http://localhost:4200 (run locally)  
**Repo:** https://github.com/gothinkster/angular-realworld-example-app

### Testing Approach
I set up the app locally using Node.js, fixed a build error (missing CSS package), and manually tested all major user flows:
- User Registration & Login
- Article Create, Edit, Delete
- Comments
- Profile Page
- Settings & Logout

### Bugs Found — Summary

| # | Bug | Severity |
|---|-----|----------|
| 1 | Complete CSS Styling Missing — App Appears Unstyled | 🔴 Critical |
| 2 | Logo Image Broken on All Pages | 🟠 High |
| 3 | User Profile Avatar Not Loading | 🟠 High |
| 4 | Weak Password Accepted Without Validation | 🟠 High |
| 5 | Article Description Not Displayed on Article Page | 🟡 Medium |
| 6 | Validation Error Messages Appear Unstyled | 🟡 Medium |
| 7 | Comment Section Avatar Image Broken | 🟢 Low |
| 8 | Logout Button Completely Unstyled | 🟢 Low |

### Root Cause Analysis
**Bug #1 (Critical)** was selected for detailed RCA.  
The `angular.json` file referenced a CSS package path `realworld/assets/theme/styles.css` that didn't exist in `node_modules`. This caused the Angular bundler to skip all styling, making the entire app render without any visual design. This bug was also the **root cause of Bugs #2, #6, #7, and #8**.

📄 Full report: `Task1_QA_Report_NaveenMishra.docx`

---

## ⚙️ Task 2 — n8n API Integration Workflow

### Workflow Name
**HackerNews Morning Digest**

### What It Does
An automated workflow that fetches top HackerNews stories every hour, enriches the data, and sends a digest email to Gmail.

### Workflow Structure

```
[Schedule Trigger - Every 1 Hour]
           ↓
[HTTP Request 1 - HackerNews Top Stories API]
   Fetches 500 top story IDs
           ↓
[Code Node - JavaScript Transformation]
   Filters to top 5 story IDs
           ↓
[HTTP Request 2 - HackerNews Item API]
   Fetches full details for each story
   (title, score, author, URL, comments)
           ↓
[IF Node - Score > 100?]
       ↓ YES              ↓ NO
[Gmail - Hot Stories]  [Gmail - Regular Stories]
🔥 Score > 100         📰 Score ≤ 100

[Error Trigger] → [Gmail - Error Alert Email]
⚠️ Fires if any node fails
```

### APIs Used

| API | Endpoint | Purpose |
|-----|----------|---------|
| HackerNews Firebase API | `/v0/topstories.json` | Fetch top 500 story IDs |
| HackerNews Item API | `/v0/item/{id}.json` | Fetch full story details |

Both APIs are **free and require no authentication**.

### Key Features
- ✅ **Schedule Trigger** — runs every 1 hour automatically
- ✅ **Data Transformation** — filters 500 stories down to top 5
- ✅ **Second API Call** — enriches each story with full details
- ✅ **IF Condition** — separates hot stories (score > 100) from regular
- ✅ **Gmail Output** — sends formatted HTML digest emails
- ✅ **Error Handling** — Error Trigger sends alert email on failure
- ✅ **Credentials** — Gmail connected via OAuth2 (no hardcoded secrets)

### n8n Cloud
Workflow is live and published on n8n Cloud.

📄 Full documentation: `Task2_README_NaveenMishra.docx`  
📦 Workflow JSON: `HackerNews Morning Digest.json`

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| Angular | Frontend app tested in Task 1 |
| Node.js v24 | Running the app locally |
| n8n Cloud | Workflow automation platform |
| HackerNews API | Public data source |
| Gmail OAuth2 | Email output |

---

## 👨‍💻 Author

**Naveen Mishra**  
GitHub: [@naveenmishra99190](https://github.com/naveenmishra99190)  
Email: naveenmishra99190@gmail.com
