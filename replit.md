# glowifyme - Psychology-Based Weight Loss Application

## Overview

glowifyme is a psychology-based weight loss and wellness application that helps users change their relationship with food through science-backed behavioral psychology techniques. The platform offers personalized coaching, daily lessons based on cognitive behavioral therapy, meal tracking, and progress monitoring. Key features include an onboarding quiz that assesses eating patterns and emotional triggers, subscription-based pricing tiers, recipe browsing, and coach consultations.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter (lightweight alternative to React Router)
- **State Management**: TanStack React Query for server state
- **Styling**: Tailwind CSS v4 with custom theme configuration
- **UI Components**: shadcn/ui component library (new-york style) built on Radix UI primitives
- **Animations**: Framer Motion for page transitions and micro-interactions
- **Typography**: Outfit font for headings, DM Sans for body text
- **Color Theme**: Warm brown palette (primary: HSL 27 65% 42%) — replaced original yellow/amber theme
- **Logo**: `attached_assets/glowy-logo_1776174729960.jpg` used in Navbar, ProductsPage, EvaluationQuizPage, DownloadAppPage

### Backend Architecture
- **Runtime**: Node.js with Express.js
- **Language**: TypeScript with ESM modules
- **Build Tool**: esbuild for server bundling, Vite for client
- **API Design**: RESTful endpoints under `/api/*` prefix

### Data Storage
- **Database**: PostgreSQL via Drizzle ORM
- **Schema Location**: `shared/schema.ts` with models in `shared/models/`
- **Session Storage**: PostgreSQL-backed sessions using connect-pg-simple
- **Key Tables**: users, sessions, quiz_responses, subscriptions, progress_entries, coach_messages, appointments

### Authentication
- **Provider**: Replit Auth (OpenID Connect)
- **Session Management**: Express sessions with PostgreSQL store
- **Auth Flow**: OAuth2/OIDC via Passport.js strategy
- **Protected Routes**: Middleware-based route protection with `isAuthenticated`

### Project Structure
```
├── client/           # React frontend
│   ├── src/
│   │   ├── components/  # UI components (layout, ui/)
│   │   ├── contexts/    # React contexts (LanguageContext)
│   │   ├── hooks/       # Custom hooks (use-auth, use-toast)
│   │   ├── lib/         # Utilities and query client
│   │   └── pages/       # Route pages
├── server/           # Express backend
│   ├── replit_integrations/  # Auth integration
│   ├── routes.ts     # API route definitions
│   └── storage.ts    # Database operations
├── shared/           # Shared types and schemas
│   ├── schema.ts     # Drizzle schema definitions
│   └── models/       # Data models
└── migrations/       # Database migrations
```

### Key Design Patterns
- **Shared Schema Validation**: Drizzle-zod generates Zod schemas from database tables for consistent validation
- **Storage Interface Pattern**: `IStorage` interface abstracts database operations
- **Path Aliases**: `@/` for client source, `@shared/` for shared code
- **Internationalization**: Language context with translation system (`useLanguage` hook)

## External Dependencies

### Database
- **PostgreSQL**: Primary database (requires `DATABASE_URL` environment variable)
- **Drizzle ORM**: Type-safe database queries and migrations
- **drizzle-kit**: Database migration tooling

### Authentication
- **Replit Auth**: OpenID Connect authentication provider
- **passport**: Authentication middleware
- **openid-client**: OIDC client implementation
- **express-session**: Session management

### Third-Party Services
- **Google Fonts**: Outfit and DM Sans typefaces loaded via CDN

### Key NPM Packages
- **@tanstack/react-query**: Server state management
- **recharts**: Charts for progress visualization
- **react-day-picker**: Calendar component for appointments
- **zod**: Runtime type validation
- **zod-validation-error**: Human-readable validation errors

### Environment Variables Required
- `DATABASE_URL`: PostgreSQL connection string
- `SESSION_SECRET`: Session encryption key
- `ISSUER_URL`: Replit OIDC issuer (defaults to https://replit.com/oidc)
- `REPL_ID`: Replit environment identifier