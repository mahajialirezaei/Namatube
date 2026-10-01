# 🎬 NamaFront – System Analysis & Design for a Video Sharing Platform

> **Course Project: System Analysis & Design**  
> **No server-side implementation – purely analysis, design, and documentation**

---

## 📌 Project Overview

**NamaFront** is an interactive, responsive user interface built using HTML5, CSS3, and Vanilla JavaScript. Key characteristics include: Comprehensive UI, Educational Elements, Dynamic Integration

**Key decisions:**
- We chose **traditional document-based requirements** (Word/PDF) over Jira to keep the SRS self-contained and version-controlled.
- The project is **analysis and design only** – no backend code.

- **Topic:** Video sharing platform  
- **Approach:** Microservices architecture, cloud deployment, REST API  
- **Deliverables:**  
  - Functional Requirements document (Word/PDF)  
  - Non-Functional Requirements document (Word/PDF)  
  - System Architecture Document (Word/PDF) with all diagrams  
  - Interactive HTML/CSS/JS prototype (no backend)  
- **Team:**  
  - **Farazin Farahmand** – Requirements documentation (functional & non-functional)  
  - **Mohammad Amin Haji Alirezaei** – HTML/CSS prototype, architecture diagrams, final PDF formatting

---

## 🗂 Repository Structure

```
sad-project/
├── README.md
├── .gitignore
│
├── docs/                              # Final documentation (Word & PDF)
│   ├── Functional.docx
│   ├── Functional.pdf
│   ├── Non-Functional.docx
│   ├── Non-Functional.pdf
│   ├── System-Architecture-Document.docx
│   ├── System-Architecture-Document.pdf
│   └── figures/                       # Diagram images
│       ├── Architecture-Diagram.png
│       ├── Components-Diagram.png
│       ├── Data-Flow-Diagram.png
│       └── Deployment-Diagram.png
│
└── prototype/                         # Static HTML/CSS/JS prototype
├── index.html
├── watch.html
├── upload.html
├── login.html
├── channel.html
├── admin.html
├── history.html
├── trending.html
├── subscriptions.html
├── library.html
├── css/
│   ├── style.css
│   ├── admin.css
│   ├── channel.css
│   ├── login.css
│   ├── upload.css
│   ├── watch.css
│   └── library.css
├── js/
│   ├── sidebar.js
│   ├── click-send-video.js
│   ├── recieve-video.js
│   ├── video-click-channel.js
│   ├── list-video.js
│   ├── history.js
│   ├── library.js
│   ├── trending.js
│   ├── login.js
│   ├── upload.js
│   └── channel.js
└── assets/
└── images/                     # Thumbnails and icons
├── containers-vms.png
├── K8s-orchestrasation.jpg
├── micro-service.png
├── modern-ui.png
├── private-public-ipv4.png
├── restful-api.png
├── Subnetting.jpg
└── two-factor.jpg
```

---

## 📄 Documentation

All requirements and design documents are stored in the `docs/` folder:

- **Functional Requirements** (`Functional.pdf`) – detailed list of features with priorities (High/Medium/Low), revision history, and use cases.
- **Non-Functional Requirements** (`Non-Functional.pdf`) – quality attributes, architecture, security, scalability, network simulation, etc.
- **System Architecture Document** (`System-Architecture-Document.pdf`) – includes four diagrams:
  - Architecture Diagram (microservices, API Gateway, data layer)
  - Component Diagram (internal structure of each service)
  - Deployment Diagram (Kubernetes, Docker, cloud infrastructure)
  - Data Flow Diagram (Level 0 & 1)

> The documents follow a traditional SRS format with version history and have been exported to PDF for easy viewing.

---

## 🎨 Static Prototype

The `prototype/` folder contains a fully interactive front-end prototype (no backend). It includes all major pages:

- **Home** – video grid, sidebar, search bar
- **Watch** – video player with blurred thumbnail, comments, recommendations
- **Upload** – form for video title, description, category, privacy, file selection
- **Login / Signup** – tabs with 2FA option (only in signup) and social login placeholders
- **Channel** – channel banner, avatar, tabs (Videos, Playlists, About) with playlist alerts
- **Admin Panel** – stats, network simulation (subnetting, NAT, DHCP, IPv4), user management table, reports
- **History, Trending, Subscriptions, Library** – additional content pages

**Interactive behaviors (static, alert-based):**
- Clicking any video card navigates to `watch.html` and passes video data (title, channel, views, date, thumbnail) via URL parameters.
- Sidebar navigation works and highlights the current page.
- Buttons (like, subscribe, clear history, download reports, playlist items, etc.) display demo alerts.

**How to run the prototype:**  
Open the `prototype/` folder and double-click `index.html` (or use a local web server like Live Server in VS Code).

---

## 🛠 Tools & Technologies

| Area | Tools |
|------|-------|
| Documentation | Microsoft Word, Adobe Acrobat (PDF) |
| Diagrams | Mermaid (exported to PNG) |
| Prototype | HTML5, CSS3, Vanilla JavaScript |
| Version control | Git + GitHub |
| Local development | VS Code, Live Server |

---

## 👥 Team Roles

- **Farazin Farahmand**  
  - Writing Functional and Non-Functional requirements documents  
  - Defining priorities and acceptance criteria  
  - Maintaining revision history and document consistency  

- **Mohammad Amin Haji Alirezaei**  
  - Designing and implementing the static HTML/CSS/JS prototype  
  - Creating architecture, component, deployment, and DFD diagrams  
  - Formatting the final System Architecture Document

---

## 📌 Important Notes for Submission

- The prototype is **completely static** – no backend or database is used.
- All requirements documents include a **revision history** table and **priority** columns.
- The diagrams are embedded as images in the System Architecture Document and also available in `docs/figures/`.
- The project name **Namatube** and producer names appear in the footer of every HTML page.
- This is a **pure analysis & design** project – implementation is not part of the scope.

---

## 📬 Contact

For any questions or feedback, please use the GitHub repository or contact the team.

- **Mohammad Amin Haji Alirezaei** – m.a.hajialirezaei05@gmail.com  

---

**Last Updated:** 2025-05-21  
**README Version:** 1.0
