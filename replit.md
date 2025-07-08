# Trading Card Game Application

## Overview

This is a full-stack trading card game application built with React (frontend) and Express.js (backend). The app features card scanning via barcodes, collection management, player battles, and matchmaking functionality. It uses a PostgreSQL database with Drizzle ORM for data persistence and includes a comprehensive UI built with shadcn/ui components.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter for client-side routing
- **State Management**: TanStack Query for server state management
- **Styling**: TailwindCSS with shadcn/ui component library
- **Build Tool**: Vite for development and production builds

### Backend Architecture
- **Framework**: Express.js with TypeScript
- **Database**: PostgreSQL with Drizzle ORM
- **Session Management**: PostgreSQL sessions with connect-pg-simple
- **API Pattern**: RESTful API endpoints under `/api` prefix

### Database Architecture
- **ORM**: Drizzle ORM with PostgreSQL dialect
- **Schema Location**: `shared/schema.ts` for type sharing between frontend and backend
- **Migrations**: Managed through Drizzle Kit

## Key Components

### Database Schema
The application uses four main tables:
- **users**: Player profiles with username, wins, losses, and timestamps
- **cards**: Game cards with barcode, type, stats (attack, defense, energy), and rarity
- **playerCards**: Junction table linking users to their card collections with quantities
- **battles**: Battle sessions with player references, HP tracking, and game state

### Card System
- **Card Types**: Character cards only (C) - simplified system
- **NFC Format**: Structured text containing Character data (Name, HP, ATK, DEF, SPD, Rarity, Version) and Charge data (Name, Effect)
- **Stats**: HP, Attack, Defense, Speed values for gameplay mechanics
- **Rarity System**: Common, Uncommon, Rare, Legendary, Promo classifications with color-coded UI display
- **Upgrade System**: Players can upgrade character stats after battle victories by rewriting NFC data

### Game Features
- **NFC Scanning**: NFC card reading and manual text input for card data
- **Collection Management**: View, search, and organize collected cards
- **Battle System**: Turn-based combat with HP tracking and character abilities
- **Matchmaking**: Player pairing system for battles
- **Card Upgrade System**: Post-battle stat upgrades with NFC data rewriting

## Data Flow

### Card Acquisition Flow
1. Player scans NFC card or enters NFC text data manually
2. NFC data is parsed to extract character stats (Name, HP, ATK, DEF, SPD) and charge info
3. System checks if card exists in database, creates if new
4. Card is added to player's collection or quantity increased

### Card Upgrade Flow
1. Player wins a battle and earns upgrade points
2. Player accesses upgrade system from victory screen or home page
3. Player reads NFC card data to load character for upgrade
4. Player allocates upgrade points to HP, ATK, DEF, or SPD stats
5. Player writes upgraded character data back to NFC card

### Battle Flow
1. Players enter matchmaking queue
2. System pairs players and creates battle record
3. Battle state tracks HP, current turn, and active cards
4. Players select cards and execute moves
5. Battle concludes when a player's HP reaches zero

### Collection Management
1. Players view their collected cards with quantities
2. Search and filter functionality by type, rarity, or name
3. Card details display stats and descriptions

## External Dependencies

### Frontend Dependencies
- **@tanstack/react-query**: Server state management and caching
- **@radix-ui/***: Unstyled UI primitives for accessibility
- **class-variance-authority**: Utility for conditional styling
- **cmdk**: Command menu component
- **date-fns**: Date manipulation utilities
- **wouter**: Lightweight routing library

### Backend Dependencies
- **@neondatabase/serverless**: PostgreSQL database connection
- **drizzle-orm**: Type-safe ORM for database operations
- **express**: Web application framework
- **connect-pg-simple**: PostgreSQL session store
- **tsx**: TypeScript execution for development

### Development Dependencies
- **drizzle-kit**: Database migrations and schema management
- **vite**: Build tool and development server
- **tailwindcss**: Utility-first CSS framework
- **typescript**: Type checking and compilation

## Deployment Strategy

### Build Process
1. Frontend builds to `dist/public` directory via Vite
2. Backend bundles to `dist/index.js` via esbuild
3. Static assets served from backend in production

### Environment Configuration
- **Development**: Uses tsx for hot reloading, Vite dev server for frontend
- **Production**: Serves static files from Express, uses bundled backend

### Database Setup
- Requires `DATABASE_URL` environment variable
- Uses Drizzle migrations in `migrations/` directory
- PostgreSQL connection via @neondatabase/serverless

### Web App Deployment
- **HTTPS Required**: NFC Web APIs require secure context (HTTPS) for writing operations
- **Mobile Optimized**: Best NFC support on Chrome for Android and Samsung Internet
- **PWA Ready**: Can be installed as Progressive Web App for better mobile experience
- **Replit Deployments**: Ready for deployment via Replit's hosting platform

### Replit Integration
- Configured for Replit development environment
- Includes Replit-specific Vite plugins for debugging
- Development banner integration for external access
- Ready for Replit Deployments with automatic HTTPS

## Changelog

```
Changelog:
- July 06, 2025. Initial setup
- July 06, 2025. Updated battle system to turn-based with single characters having 3 assigned moves each
- July 06, 2025. Removed manual barcode input from scanner, keeping only camera scanning
- July 06, 2025. Simplified battle system to use 1 Character, 1 Power, and 1 Special card instead of 3 of each type
- July 06, 2025. Further simplified to use only Character cards for battles, prepared power system for future integration with card assets
- July 06, 2025. Fully deleted power and special cards from system, implemented Tester card with specific abilities: Power (block opponent attack), Special (Armageddon after 5 turns)
- July 07, 2025. Complete migration from barcode to NFC scanning system
- July 07, 2025. Implemented card upgrade system allowing players to enhance character stats after battle victories
- July 07, 2025. Added NFC data structure: Character section (Name, HP, ATK, DEF, SPD) and Charge section (Name, Effect)
- July 07, 2025. Created card upgrade page with NFC read/write functionality for stat enhancement
- July 07, 2025. Removed manual input from NFC scanner, enforcing physical card scanning only
- July 07, 2025. Updated battle system to require physical card scanning, preventing collection-based battles
- July 07, 2025. Fixed NFC browser compatibility detection (reading vs writing support)
- July 07, 2025. Added 5-tier rarity system to NFC cards: Common, Uncommon, Rare, Legendary, Promo
- July 07, 2025. Added Version field to NFC structure for card version identification
- July 07, 2025. Implemented local battle system with two players using same device
- July 07, 2025. Added online battle options (room codes and matchmaking) for future implementation
- July 07, 2025. Restructured battle flow: Local battle for same-device play, Online battle with create/join rooms
- July 07, 2025. Updated entire UI theme to match BEYONDER logo with black, red, and yellow fire gradient colors
- July 07, 2025. Added BEYONDER logo to header and created reusable Header component for consistent branding
```

## User Preferences

```
Preferred communication style: Simple, everyday language.
```