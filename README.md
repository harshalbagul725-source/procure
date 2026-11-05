<p align="center">
  <img src="public/procure-logo-new.png" alt="Procure logo" width="160" />
</p>

<h1 align="center">Procure</h1>

<p align="center">
  <strong>Turn procurement requirements into structured standards and supplier insights.</strong>
</p>

<p align="center">
  An AI-assisted procurement and Indian Standards intelligence prototype.
</p>

<p align="center">
  <a href="https://procure2-delta.vercel.app/">Open the demo</a>
</p>

<p align="center">
  <img alt="Next.js 16" src="https://img.shields.io/badge/Next.js-16-000000?logo=nextdotjs" />
  <img alt="React 19" src="https://img.shields.io/badge/React-19-149ECA?logo=react" />
  <img alt="TypeScript" src="https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript" />
  <img alt="Tailwind CSS 4" src="https://img.shields.io/badge/Tailwind_CSS-4-06B6D4?logo=tailwindcss" />
  <img alt="Prisma" src="https://img.shields.io/badge/Prisma-SQLite-2D3748?logo=prisma" />
  <img alt="Google Gemini optional" src="https://img.shields.io/badge/Gemini-optional-8E75B2?logo=googlegemini" />
</p>

## Overview

Procure is a prototype for exploring how procurement teams can turn a plain-language requirement into a structured analysis. The application extracts product and specification details, searches a bundled Indian Standards knowledge set, and ranks matching sample suppliers. Users can save suppliers and exchange messages and quotes in the demo workflow.

The project is designed for demonstration and experimentation, not as an authoritative source for tender or compliance decisions. The bundled standards and supplier records are limited sample data, and all standards and regulatory requirements should be checked against current official sources before use.

## Key features

- **Requirement analysis:** Enter a procurement need as text and extract fields such as product, quantity, intended use, and technical requirements.
- **Standards matching:** Search and rank records from the standards data bundled with the project. Gemini-based ranking is optional; deterministic keyword matching is available as a fallback.
- **Research and clarification:** Show additional research, questions, and procurement checklist items. AI-researched standards are marked as requiring verification.
- **Supplier recommendations:** Match sample suppliers to a requirement and rank them using product, standards, compliance, document, certification, and trust signals.
- **Supplier follow-up:** Save supplier favorites, start a conversation, and submit a quote through the demo interface.
- **Voice input:** Use browser speech recognition where supported.

> **Prototype limitations:** The dashboard includes a file picker, but selected files are not uploaded or parsed; the analyzer receives the text in the input field. The sign-in, OTP, and verification screens are a demo UI, not production authentication. AI results and bundled supplier and standards data require independent verification.

## Technology stack

| Area | Technologies |
| --- | --- |
| Web application | Next.js 16 App Router, React 19 |
| Language | TypeScript |
| Styling | Tailwind CSS 4 |
| Data layer | Prisma schema for SQLite; local JSON fallback in the demo |
| AI integration | Google Generative AI SDK (Gemini, optional) |
| UI and motion | Radix UI, Phosphor Icons, Lucide, Framer Motion, GSAP |

## Screenshots

No application screenshots are currently committed. The deployed demo is available at [procure2-delta.vercel.app](https://procure2-delta.vercel.app/).

## Workflow and architecture

1. A user enters a procurement requirement in the dashboard.
2. The Next.js API creates a requirement and runs structured extraction and research. Gemini is used when `GEMINI_API_KEY` is configured; deterministic local logic is used otherwise or when a Gemini request fails.
3. The application searches and ranks the bundled standards records, then displays the analysis and any verification caveats.
4. Matching supplier records are ranked against the requirement. Users can save a supplier, open a conversation, and submit a quote.

The main implementation areas are the App Router pages and API handlers in `src/app/`, AI and data helpers in `src/lib/`, and the Prisma data model in `prisma/schema.prisma`. Supplier and standards reference data are bundled in `src/lib/standards/data/`.

## Installation

### Prerequisites

- Node.js and npm
- A Google Gemini API key only if you want to enable Gemini-backed analysis

### Setup

```bash
git clone https://github.com/harshalbagul725-source/procure.git
cd procure
npm install
```

Copy the example environment file:

```powershell
Copy-Item .env.example .env
```

On macOS or Linux, use `cp .env.example .env` instead. The example file sets the SQLite `DATABASE_URL`; add a Gemini key if desired:

```dotenv
DATABASE_URL="file:./dev.db"
GEMINI_API_KEY="your_google_ai_studio_key"
```

`GEMINI_API_KEY` is optional. Without it, the application uses its deterministic local extraction and ranking paths.

The repository does not include Prisma migrations or a Prisma CLI configuration, so it does not define a Prisma database-bootstrap command. The Prisma schema, runtime storage code, and demo JSON fallback are in `prisma/` and `src/lib/db.ts`.

## Run the project

Start the development server:

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying) for more details.
