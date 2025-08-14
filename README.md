# ClauseCraft

**Dynamic Risk-Adaptive Contract Generator for Legal Teams**  
ClauseCraft lets you instantly rewrite entire contracts to match your risk appetite. Slide from Conservative (maximum protection) to Aggressive (speed and flexibility), and watch each clause expand, shrink, or swap with AI-powered precision. See side-by-side diffs, get plain-language rationales, and export Word/PDF drafts—making negotiations faster, safer, and fully transparent.

---

## Table of Contents

1. [Overview](#overview)
2. [Stack Overview](#stack-overview)
3. [Features](#features)  
4. [Roadmap](#roadmap)  
5. [Getting Started](#getting-started)  
6. [Contributing](#contributing)  
7. [License](#license)  

---

## Overview

ClauseCraft transforms static contract templates into interactive, AI-driven agreements. Users adjust a single **Risk Slider** (0–100) to automatically:
- Expand protections (longer indemnity, stricter penalties)  
- Shrink hurdles (shorter notice periods, faster terminations)  
- Swap jurisdictions or payment terms  
- Receive clear, clause-by-clause explanations  
- Compare drafts with track-changes–style diffs  
- Export polished Word or PDF documents  

Designed for legal teams and business users, ClauseCraft cuts drafting time, reduces errors, and aligns every clause with your business goals.

---

## Stack Overview

- **Frontend:** Next.js (React) + Tailwind CSS  
- **Backend:** Node.js + Express (or Next.js API routes)  
- **AI Integration:** OpenAI GPT-4 for clause generation and rationale  
- **Database:** MongoDB Atlas (M0 free cluster)  
- **Caching (Optional):** Upstash Redis free tier  
- **Document Export:** js-docx, PDFKit  
- **Deployment:** Vercel (frontend + serverless functions), Railway (backend)  
- **CI/CD:** GitHub Actions  
- **Monitoring:** Sentry (errors), Vercel Logs

---

## Features

- **Risk Slider Control**: One slider to govern the entire contract’s risk profile.  
- **AI-Generated Clauses**: GPT-4 templates for indemnity, confidentiality, termination, and more.  
- **Diff Viewer**: Side-by-side before vs. after with highlights.  
- **Clause Rationale**: Plain-English explanations for every change.  
- **Version History**: Save, restore, and share past drafts.  
- **Export & Review**: Download Word/PDF and generate secure review links.  

---

## Roadmap

### 1. Project Initialization

1.1 **GitHub Organization & Repository**  
- Create a GitHub organization and add all team members.  
- Create the `clausecraft` repo with a README, MIT license, and Node.js `.gitignore`.  
- Protect `main` branch: require pull requests and at least one review before merging.  
- Add project issues and labels (feature, bug, docs).

---

### 2. Development Environment Setup

2.1 **Local Environment**  
- Install Node.js v18+, npm or Yarn, Git, Docker (optional).  
- Configure VSCode with ESLint, Prettier, and Tailwind CSS IntelliSense.

2.2 **Frontend Scaffold**  
- `npx create-next-app clausecraft-frontend --typescript`  
- Install Tailwind CSS and initialize with `npx tailwindcss init -p`.

2.3 **Backend Setup**  
- In `clausecraft-backend` or Next.js API routes, install Express (or use Next.js API), dotenv, mongoose.

2.4 **Version Control Workflow**  
- Create `develop` and feature branches (`feature/xxx`).  
- Enforce pull requests and code reviews.

---

### 3. Core Features & Component Buildout

#### 3.1 Frontend Core

1. **Layout & Routing**  
   - Build a `<Layout>` component with header, sidebar, and footer.  
   - Pages: `/`, `/editor`, `/history`, `/settings`, `/login`.

2. **Risk Slider**  
   - Create `<RiskSlider>` emitting values 0–100 with “Conservative”/“Aggressive” labels.

3. **Clause Editor**  
   - Use a `<textarea>` or `contentEditable` `<div>` for the contract draft.

4. **Diff Viewer**  
   - Integrate `js-diff` to compute changes.  
   - Render side-by-side before vs. after with highlights.

5. **Rationale Panel**  
   - Collapsible list of GPT-4 explanations for each clause change.

6. **Version History**  
   - List saved drafts with date, risk level, and restore/share actions.

7. **Export Buttons**  
   - “Download DOCX” and “Download PDF” trigger backend export endpoints.

#### 3.2 State Management

- Use React Context or Redux Toolkit for global state:  
  - `riskLevel`, `currentDraft`, `diffData`, `rationaleList`.  
- Create custom hooks (e.g., `useContract`).

#### 3.3 Backend Core

1. **Authentication**  
   - JWT-based login/sign-up or API key for hackathon.

2. **API Endpoints**  
   - `POST /generate`: `{ riskLevel, section }` → `updatedText`.  
   - `POST /diff`: `{ before, after }` → diff data.  
   - `POST /explain`: `{ changes }` → rationales.  
   - `GET|POST /history`: fetch and save drafts.  
   - `POST /export`: return DOCX/PDF blob.

3. **Data Store**  
   - MongoDB Atlas for templates, sessions, and history.

4. **AI Integration**  
   - Use OpenAI GPT-4 with prompt templates keyed by risk level.  
   - Cache common prompts in Redis or in-memory.

#### 3.4 Integration Workflow

1. User moves slider → Frontend `POST /generate`.  
2. Backend returns new draft → update state.  
3. Frontend computes diff and calls `/explain`.  
4. Render diff viewer and rationale panel.  
5. Save versions or export as needed.

---

## Getting Started

1. **Clone the repo**  
(https://github.com/your-org/clausecraft.git)

2. **Frontend setup**  
cd clausecraft/frontend
npm install
npm run dev

3. **Backend setup**  
cd clausecraft/backend
npm install
npm run dev

4. **Environment variables**  
- Create `.env` files in frontend and backend with:  
  ```
  NEXT_PUBLIC_API_URL=http://localhost:3000/api
  OPENAI_API_KEY=your_openai_key
  MONGODB_URI=your_mongo_uri
  JWT_SECRET=your_jwt_secret
  ```

5. **Access the app**  
- Frontend: http://localhost:3000  
- Backend API: http://localhost:3000/api

---

## Contributing

- Fork the repo and create feature branches: `git checkout -b feature/your-feature`.  
- Submit pull requests to `develop` branch.  
- Ensure linting and tests pass before requesting review.  
- Refer to [CONTRIBUTING.md](/CONTRIBUTING.md) for detailed guidelines.

---

## License

MIT © 2025 ClauseCraft Team  



