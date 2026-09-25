# Applause

A team recognition feed where colleagues publicly thank and praise each other, built with Next.js 15, React 19, TypeScript and Tailwind CSS 4.

[![CI](https://github.com/GersonRocha9/applause-teste/actions/workflows/ci.yml/badge.svg)](https://github.com/GersonRocha9/applause-teste/actions/workflows/ci.yml)
[![Latest release](https://img.shields.io/github/v/release/GersonRocha9/applause-teste)](https://github.com/GersonRocha9/applause-teste/releases)

**Live demo:** https://applause-teste.vercel.app

> The interface copy is in Brazilian Portuguese.

## Features

**Recognition feed**
- Post cards showing author, recipient, recognition type, relative date, message, hashtags and optional image
- Infinite scroll with `IntersectionObserver`, loading 5 posts at a time
- Real-time search by author or recipient name, plus one-tap filters per recognition type
- Live "showing X of Y" counter and a one-click reset for all filters

**Recognition form**
- Participant picker with search, incremental loading (20 at a time) and a chip for the selected person
- Four recognition types: 🙏 Thank you, 🙌 Good job, 😍 Impressive, ✨ Extraordinary
- Message field with a 500-character counter and automatic `#hashtag` extraction
- Image attachment validated for type and a 5 MB size limit
- Form state and validation with React Hook Form, feedback via toast notifications
- New recognitions appear at the top of the feed right after submission

**Responsive layout**
- Desktop (`lg` and up): form and feed side by side
- Mobile: tabbed navigation between the feed and the form

Data comes from local JSON mocks (`participants-mock.json`, `posts-mock.json`) and state lives in memory; there is no backend.

## Tech stack

| Area | Tools |
| --- | --- |
| Framework | Next.js 15 (App Router), React 19 |
| Language | TypeScript (strict mode) |
| Styling | Tailwind CSS 4 |
| State | React Context API with `useReducer` |
| Forms | React Hook Form |
| Notifications | react-hot-toast |
| Testing | Jest 30, React Testing Library, user-event, jsdom |
| Tooling | ESLint 9 (`eslint-config-next`), GitHub Actions, Dependabot |
| Hosting | Vercel |

## Engineering highlights

- **Tests across the whole app.** Every UI primitive (`Avatar`, `Button`, `Input`, `Select`, `Textarea`), every feature component, the `AppContext` provider, the `useToast` hook and the utility functions have a dedicated test suite. Jest enforces a 70% global coverage threshold for branches, functions, lines and statements.
- **Continuous integration.** Every push and pull request to `main`, `develop` and `staging` runs lint, the test suite with coverage, and a production build.
- **Automated releases.** Each push to `main` runs tests and build, bumps the version with `npm version`, tags it and publishes a GitHub Release. Patch is the default; a manual dispatch can cut a minor or major release, and `[skip release]` in the commit message opts out.
- **Dependency hygiene.** Dependabot opens weekly update PRs for npm packages and GitHub Actions. A scheduled workflow runs `npm audit` (failing on high or critical findings), checks for unused and outdated packages, and opens a PR with patch-level updates after the tests pass.
- **Rendering performance.** Feature components are wrapped in `React.memo`, with `useCallback` and `useMemo` keeping props and derived lists stable. Images go through `next/image`.

## Getting started

Requires Node.js 20 (the version used in CI) and npm.

```bash
git clone https://github.com/GersonRocha9/applause-teste.git
cd applause-teste
npm install
npm run dev
```

The app runs at http://localhost:3000.

| Script | Description |
| --- | --- |
| `npm run dev` | Start the development server |
| `npm run build` | Create a production build |
| `npm run start` | Serve the production build |
| `npm run lint` | Run ESLint |

## Running tests

```bash
npm test               # run the suite once
npm run test:watch     # watch mode
npm run test:coverage  # with coverage report
npm run test:ci        # CI mode with coverage
```

## Project structure

```
src/
├── app/            # App Router: layout, page, global styles
├── components/     # Feed, PostCard, RecognitionForm, ParticipantSelector, SearchAndFilters, MobileLayout
│   └── ui/         # Reusable primitives: Avatar, Button, Input, Select, Textarea
├── contexts/       # AppContext: posts, participants, filters and pagination
├── hooks/          # useToast
├── constants/      # Recognition types, page size, toast options
├── types/          # Shared TypeScript types
└── utils/          # Date formatting, hashtag extraction, image validation, debounce
```

Tests live next to the code they cover in `__tests__` folders.

## Author

**Gerson Rocha** — [github.com/GersonRocha9](https://github.com/GersonRocha9)
