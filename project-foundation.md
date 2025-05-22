
# 🧱 Project Foundation & Structure Guidelines

This document outlines best practices and setup recommendations to establish a **scalable**, **team-friendly**, and **maintainable** foundation for modern web applications.

---

## ⚙️ 1. Framework & Tooling Options

### Frontend Framework
- ✅ **React** (default choice)
- ⚡️ **Vite** over CRA (faster dev build, smaller bundles, better DX)

### Language Choices
- **Option 1: React + Vite (JavaScript)**
  - Fast prototyping
  - Good for MVPs or solo devs
- **Option 2: React + Vite + TypeScript**
  - Recommended for mid- to long-term projects
  - Strong typing = fewer bugs, better IntelliSense
  - Ideal for team collaboration

---

## 🗂 2. Project Structure

```
src/
│
├── app/                  # App root (entry point, routes)
├── components/           # Shared UI components (buttons, modals)
├── features/             # Domain-based features (auth, drops, profile)
│   ├── auth/
│   │   ├── components/
│   │   ├── context/
│   │   ├── hooks/
│   │   ├── pages/
│   │   └── index.ts      # Barrel export
│   └── ...
├── hooks/                # Reusable logic/hooks (not domain-specific)
├── layouts/              # Global layout components
├── lib/                  # Utility functions, helpers
├── pages/                # Route-level pages (optional if using `app/`)
├── services/             # External integrations (e.g., Supabase, Stripe)
├── styles/               # Global styles or Tailwind config
└── types/                # Global TypeScript types
```

> ✅ **Tip:** Prefer a *feature-first* folder structure over type-based (e.g., `auth/` over `components/auth/`).

---

## 🔐 3. Authentication (Recommended Setup)

- Use **Context API** + custom hooks:
  - `AuthProvider.tsx`
  - `useAuthContext.ts`
  - `useAuthState.ts`
  - `useAuthInitialization.ts`
- Handle logic in `contexts/auth/` or `features/auth/context/`
- UI wrappers like `<ProtectedRoute />` live in `features/auth/components/`

---

## 📦 4. Package/Library Suggestions

| Concern            | Package / Tool             |
|--------------------|----------------------------|
| Build tool         | `vite`                     |
| Styling            | `tailwindcss`              |
| Routing            | `react-router-dom`         |
| State (optional)   | `zustand`, `jotai`, or Context API |
| Auth               | `supabase`, `auth.js`, or `firebase` |
| Forms              | `react-hook-form`          |
| Validation         | `zod` or `yup`             |
| Linting            | `eslint`, `prettier`       |
| Type-checking      | `typescript`               |

---

## 🧪 5. Testing Setup (Optional)

- Unit Testing: `vitest` or `jest`
- Component Testing: `@testing-library/react`
- E2E: `cypress` or `playwright`

---

## 🔁 6. Import & Barrel Patterns

Use `index.ts` files for every `context/`, `hooks/`, and `components/` folder:

```ts
// features/auth/context/index.ts
export * from './AuthContext';
export * from './useAuthContext';
```

This allows cleaner imports:

```ts
import { useAuthContext } from '@/features/auth/context';
```

---

## 📘 7. README or Docs Notes

Make sure to include:
- Project structure overview
- Setup instructions
- Development workflow (`npm run dev`)
- Environment variable naming conventions (`.env.local`)
