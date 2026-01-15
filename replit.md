# Doviz Exchange Rate Tracker

## Overview

A bilingual (Arabic/English) currency exchange rate tracking application for Syrian Pound (SYP) to USD. The app displays real-time buy/sell rates, provides historical rate archives, includes a currency converter, and features an admin panel for rate management. Built as a full-stack TypeScript application with React frontend and Express backend.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter (lightweight alternative to React Router)
- **State Management**: TanStack React Query for server state caching and synchronization
- **Styling**: Tailwind CSS with shadcn/ui component library (New York style variant)
- **Animations**: Framer Motion for smooth transitions
- **Form Handling**: React Hook Form with Zod validation
- **RTL Support**: Full Arabic language support with RTL layout

### Backend Architecture
- **Runtime**: Node.js with Express
- **Language**: TypeScript with ESM modules
- **Build**: Vite for frontend, esbuild for server bundling
- **API Pattern**: RESTful endpoints defined in shared routes file with Zod schemas for type safety

### Data Layer
- **ORM**: Drizzle ORM with PostgreSQL dialect
- **Schema Location**: `shared/schema.ts` (shared between frontend and backend)
- **Migrations**: Drizzle Kit with `db:push` command
- **Connection**: PostgreSQL via `pg` Pool

### Database Schema
- **exchangeRates**: Historical buy/sell prices with timestamps
- **dailyAverages**: Computed daily average rates
- **appSettings**: Key-value configuration (market status, auto-update settings, admin password)
- **notifications**: Admin-created announcements
- **visitorStats**: Daily visitor count tracking

### Authentication
- Simple token-based admin authentication stored in sessionStorage
- Admin token validated via `x-admin-token` header
- No user registration system (admin-only access)

### Key Design Decisions

1. **Shared Type Definitions**: Schema and route definitions live in `shared/` directory, enabling type-safe API contracts between frontend and backend

2. **Rate Change Logic**: Price decrease = Green (Lira strengthening), Price increase = Red (Lira weakening) - inverted from typical financial displays

3. **Market Status System**: Three states - Open (green), Opening (orange), Closed (red)

4. **Web Scraping**: Rates can be auto-fetched from sp-today.com using Cheerio for HTML parsing

## External Dependencies

### Database
- **PostgreSQL**: Primary data store, connection via `DATABASE_URL` environment variable

### External APIs & Services
- **sp-today.com**: Web scraping source for current exchange rates (via Axios + Cheerio)
- **Google Fonts**: Cairo and Tajawal Arabic fonts, DM Sans, Fira Code, Geist Mono

### Key NPM Packages
- **UI**: Radix UI primitives, Lucide icons, class-variance-authority
- **Data**: Drizzle ORM, Zod validation, date-fns
- **HTTP**: Axios for scraping, Express for server
- **Session**: connect-pg-simple for PostgreSQL session store