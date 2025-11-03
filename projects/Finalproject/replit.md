# UDP Network Simulator

## Overview

The UDP Network Simulator is an educational web application designed to visualize and teach UDP network protocols through interactive simulation. The application combines two primary features:

1. **Network Protocol Simulation**: A real-time visualization of UDP packet transmission using the Stop-and-Wait protocol, featuring packet loss, checksums, ACK/NACK handling, and timeout detection. Includes real-time event logging with JSON export capability.

2. **Matrix Operations**: A computational tool supporting matrix operations (addition, subtraction, multiplication, transpose, inverse, determinant) on matrices up to 700×700 dimensions. Supports CSV file upload for matrix input and provides real-time performance profiling charts showing execution time across different matrix sizes.

The project serves as a technical educational tool with emphasis on information clarity, immediate visual feedback, and protocol understanding.

## Recent Enhancements (November 2025)

1. **CSV Upload Feature**: Users can upload CSV files for matrix input with comprehensive validation, error handling, and support for repeated uploads of the same file.

2. **Event Log Export**: Network event logs can be exported as timestamped JSON files for offline analysis.

3. **Performance Profiling Charts**: Interactive recharts visualization showing matrix operation execution times across different sizes, with multi-operation comparison and summary statistics.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Technology Stack**:
- **Framework**: React with TypeScript
- **Build Tool**: Vite for development and production builds
- **UI Library**: Shadcn/ui components built on Radix UI primitives
- **Styling**: Tailwind CSS with custom design tokens
- **State Management**: React hooks with TanStack Query for server state
- **Routing**: Wouter (lightweight client-side routing)

**Design System**:
- Material Design principles adapted for technical/educational content
- Dual theme support (light/dark mode) with CSS variables
- Typography hierarchy using Inter/Roboto for UI and JetBrains Mono for technical data
- Consistent spacing system based on Tailwind's 2/4/8/12/16 unit scale
- Custom color tokens for semantic UI elements (primary, secondary, destructive, muted, accent)

**Component Architecture**:
- Separation of concerns: UI components (`/components/ui`), feature components (`/components`), and page-level components (`/pages`)
- Real-time visualization using HTML Canvas for network topology rendering
- Event-driven architecture for simulation controls and packet animation

**Path Aliases**:
- `@/*` → `client/src/*`
- `@shared/*` → `shared/*`
- `@assets/*` → `attached_assets/*`

### Backend Architecture

**Technology Stack**:
- **Runtime**: Node.js with TypeScript (ESM modules)
- **Server Framework**: Express.js
- **Real-time Communication**: WebSocket (ws library) for bidirectional simulation control
- **Build Tool**: esbuild for production bundling

**API Structure**:
- REST endpoints for matrix operations (`/api/matrix/*`)
- WebSocket endpoint (`/ws`) for real-time simulation state synchronization
- Middleware for request logging and JSON parsing with raw body capture

**Simulation Engine**:
- Server-side simulation loop (`UDPSimulation` class) managing packet lifecycle
- Stop-and-Wait protocol implementation with configurable parameters
- Event logging system tracking all network events
- Statistics aggregation (packets sent/received/dropped, retransmissions, timeouts, checksum errors)

**Matrix Operations**:
- Pure computational logic in `MatrixOperations` class
- Support for matrices up to 700×700 elements
- Operations: add, subtract, multiply, transpose, inverse, determinant, scalar multiplication

**Development Features**:
- Vite middleware integration for HMR in development
- Replit-specific plugins (runtime error overlay, cartographer, dev banner) conditionally loaded
- Static file serving in production mode

### Data Storage Solutions

**Current Implementation**:
- **In-Memory Storage**: `MemStorage` class provides runtime state management for users
- No persistent database currently active despite Drizzle ORM configuration

**Configured but Unused**:
- **Drizzle ORM**: PostgreSQL schema defined in `shared/schema.ts`
- **Neon Database**: Serverless Postgres adapter included (`@neondatabase/serverless`)
- **Schema Tables**: 
  - `users` (authentication placeholder)
  - `matrixOperations` (operation history tracking)
  - `networkEvents` (event log persistence)
  - `simulationSessions` (simulation state snapshots)

**Rationale**: The application currently operates entirely in-memory for simplicity and educational focus. Database infrastructure is scaffolded for future enhancement when persistence becomes necessary.

### Authentication and Authorization

**Current State**: Minimal authentication infrastructure
- User schema defined but not enforced
- Session management configured (`connect-pg-simple`) but not actively used
- No login/registration UI implemented

**Rationale**: As an educational tool focused on network simulation, authentication is not core to the application's primary value. Infrastructure exists for future multi-user features.

## External Dependencies

### UI Component Library
- **Radix UI**: Unstyled, accessible component primitives (@radix-ui/react-*)
- **Shadcn/ui**: Pre-styled component layer built on Radix UI with Tailwind CSS
- **Lucide React**: Icon library for consistent iconography

### Data Visualization
- **Recharts**: Charting library for performance metrics visualization (execution time vs matrix size)
- **HTML Canvas API**: Custom network topology and packet animation rendering

### Utilities
- **Zod**: Runtime type validation and schema parsing
- **clsx/tailwind-merge**: Dynamic className composition
- **date-fns**: Date formatting for timestamps in event logs
- **class-variance-authority**: Type-safe component variant API

### Development Tools
- **TypeScript**: Static type checking across client/server/shared code
- **Vite**: Fast development server with HMR
- **esbuild**: Production build optimization
- **tsx**: TypeScript execution for server runtime
- **Replit Plugins**: Development environment enhancements (error overlay, cartographer, dev banner)

### Network Communication
- **ws (WebSocket)**: Bidirectional real-time communication for simulation state
- **TanStack Query**: Server state management with caching and synchronization

### Potential Database (Configured)
- **PostgreSQL**: Via Neon serverless driver
- **Drizzle ORM**: Type-safe database toolkit with migration support
- **connect-pg-simple**: PostgreSQL session store for Express

### Build and Deployment
- **PostCSS**: CSS processing with Tailwind and Autoprefixer
- **cross-env**: Environment variable management across platforms