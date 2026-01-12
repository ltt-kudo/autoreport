# Smart Reports

## Overview

Smart Reports is an AI-powered report generation application that allows users to create, edit, and export data-driven reports. The application features a markdown-based editor with live preview, AI content generation using Google's Gemini models, file attachments, multiple visual themes, and chart rendering capabilities. Users can create visually appealing reports with embedded data visualizations and export them for sharing.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React with TypeScript, using Vite as the build tool
- **Routing**: Wouter for lightweight client-side routing
- **State Management**: TanStack React Query for server state management and caching
- **UI Components**: shadcn/ui component library built on Radix UI primitives
- **Styling**: Tailwind CSS with custom CSS variables for theming
- **Animations**: Framer Motion for transitions and micro-interactions
- **Charts**: Recharts for data visualization (bar charts, pie charts)
- **Markdown**: react-markdown for rendering report content
- **Layout**: react-resizable-panels for split-screen editor interface

### Backend Architecture
- **Runtime**: Node.js with Express.js
- **Language**: TypeScript compiled with tsx for development, esbuild for production
- **API Structure**: RESTful endpoints defined in `shared/routes.ts` with Zod validation
- **File Uploads**: Multer middleware handling file storage to `uploads/` directory

### Data Storage
- **Database**: PostgreSQL with Drizzle ORM
- **Schema Location**: `shared/schema.ts` defines all database tables
- **Migrations**: Drizzle Kit for schema migrations (`drizzle-kit push`)
- **Core Tables**:
  - `reports`: Stores report metadata (title, markdown content, theme, attachments)
  - `conversations` and `messages`: Chat history for AI interactions

### AI Integration
- **Provider**: Google Gemini via Replit AI Integrations
- **Models Used**:
  - `gemini-2.5-flash`: Fast text generation
  - `gemini-2.5-pro`: Advanced reasoning
  - `gemini-2.5-flash-image`: Image generation
- **Configuration**: Uses Replit-provided environment variables (`AI_INTEGRATIONS_GEMINI_API_KEY`, `AI_INTEGRATIONS_GEMINI_BASE_URL`)
- **Features**: Batch processing with rate limiting, streaming responses, image generation

### Key Design Patterns
- **Shared Types**: Schema and route definitions in `shared/` directory used by both client and server
- **Storage Interface**: `IStorage` interface in `server/storage.ts` abstracts database operations
- **Custom Hooks**: React hooks in `client/src/hooks/` encapsulate data fetching logic
- **Component Library**: Pre-built UI components in `client/src/components/ui/`

## External Dependencies

### Database
- **PostgreSQL**: Primary database, connection via `DATABASE_URL` environment variable
- **connect-pg-simple**: Session storage in PostgreSQL

### AI Services
- **Replit AI Integrations**: Provides Gemini API access without requiring separate API keys
- **Environment Variables Required**:
  - `AI_INTEGRATIONS_GEMINI_API_KEY`
  - `AI_INTEGRATIONS_GEMINI_BASE_URL`

### Third-Party Libraries
- **@google/genai**: Google Generative AI client library
- **multer**: File upload handling
- **date-fns**: Date formatting utilities
- **zod**: Runtime type validation for API requests/responses
- **drizzle-orm / drizzle-zod**: Database ORM and schema validation

### Development Tools
- **Vite**: Development server with HMR
- **Replit Plugins**: `@replit/vite-plugin-runtime-error-modal`, `@replit/vite-plugin-cartographer` for enhanced development experience