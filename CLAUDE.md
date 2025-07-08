# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

### Root Level Commands
- `npm run backend:dev` - Start backend development server with hot reload
- `npm run frontend:dev` - Start frontend development server with hot reload
- `npm run backend` - Start backend in production mode
- `npm run frontend` - Build frontend for production

### Testing
- `npm run test:api` - Run backend tests
- `npm run test:client` - Run frontend tests
- `npm run e2e` - Run end-to-end tests (requires local config)
- `npm run e2e:headed` - Run E2E tests with browser UI

### Building
- `npm run build:data-provider` - Build shared data provider package
- `npm run build:api` - Build API package
- `npm run build:data-schemas` - Build data schemas package
- `npm run frontend` - Build complete frontend (includes all packages)

### Linting & Formatting
- `npm run lint` - Run ESLint on all files
- `npm run lint:fix` - Auto-fix ESLint issues
- `npm run format` - Format code with Prettier

### User Management
- `npm run create-user` - Create new user account
- `npm run ban-user` - Ban user account
- `npm run delete-user` - Delete user account
- `npm run reset-password` - Reset user password

## Project Architecture

### Monorepo Structure
LibreChat is a monorepo with workspaces:
- `api/` - Backend Express.js server
- `client/` - Frontend React application
- `packages/` - Shared packages (data-provider, data-schemas, api)
- `config/` - Configuration scripts and utilities
- `e2e/` - End-to-end test suite

### Backend (`api/`)
The backend follows a layered architecture:
- **Controllers** (`server/controllers/`) - Request handlers for different features
- **Routes** (`server/routes/`) - API endpoint definitions
- **Services** (`server/services/`) - Business logic layer
- **Models** (`models/`) - Database models using Mongoose
- **Middleware** (`server/middleware/`) - Request processing (auth, validation, rate limiting)
- **AI Clients** (`app/clients/`) - Integrations with various AI providers

### Frontend (`client/`)
React application with modern tooling:
- **Components** (`src/components/`) - Feature-organized UI components
- **Hooks** (`src/hooks/`) - Custom React hooks for business logic
- **Store** (`src/store/`) - Recoil state management
- **Data Provider** (`src/data-provider/`) - API integration layer
- **Routes** (`src/routes/`) - React Router configuration

### Database Models
Key models in `api/models/`:
- **User** - User accounts and authentication
- **Conversation** - Chat conversations with metadata
- **Message** - Individual chat messages
- **File** - File uploads and attachments
- **Preset** - Saved conversation configurations
- **Agent** - AI agent configurations
- **Assistant** - Assistant definitions

### Authentication
Multi-strategy authentication system:
- JWT tokens for stateless authentication
- OAuth providers (Google, GitHub, Discord, etc.)
- LDAP integration for enterprise
- Local username/password
- Two-factor authentication (2FA)

### AI Provider Integration
The system supports multiple AI providers through a unified client interface:
- OpenAI (GPT models)
- Anthropic (Claude models)
- Google (Gemini/PaLM models)
- Azure OpenAI
- AWS Bedrock
- Custom endpoints for local models

### File Management
File handling with multiple storage strategies:
- Local filesystem storage
- AWS S3 integration
- Firebase storage
- Azure Blob storage

## Development Workflow

### Setting Up Development Environment
1. Install dependencies: `npm install` (installs all workspaces)
2. Set up environment variables (copy from `.env.example`)
3. Start MongoDB (local or Docker)
4. Start backend: `npm run backend:dev`
5. Start frontend: `npm run frontend:dev`

### Making Changes
1. Backend changes: Work in `api/` directory
2. Frontend changes: Work in `client/` directory
3. Shared utilities: Work in `packages/` directory
4. Run tests before committing: `npm run test:api` and `npm run test:client`
5. Format code: `npm run format`
6. Fix linting: `npm run lint:fix`

### API Development
- Controllers handle request/response logic
- Services contain business logic
- Models define data structure and validation
- Middleware handles cross-cutting concerns
- Follow RESTful conventions for endpoints

### Frontend Development
- Use TypeScript for type safety
- Components should be feature-organized
- Custom hooks for reusable logic
- Recoil for local state, React Query for server state
- Tailwind CSS for styling
- Follow accessibility best practices

### Testing
- Unit tests with Jest
- E2E tests with Playwright
- API tests using supertest
- Test files should be co-located with source code

## Configuration

### Main Configuration
- `librechat.example.yaml` - Main application configuration template
- Environment variables for sensitive data
- Docker compose for containerized deployment

### AI Provider Configuration
Each AI provider requires specific configuration:
- API keys and endpoints
- Model specifications
- Rate limiting settings
- Custom parameters

### Database Configuration
- MongoDB connection strings
- Index optimization
- TTL settings for data retention

## Key Directories to Understand

### Backend Key Files
- `api/server/index.js` - Main server entry point
- `api/app/clients/` - AI provider implementations
- `api/models/` - Database schema definitions
- `api/server/routes/` - API endpoint definitions
- `api/server/services/` - Business logic layer

### Frontend Key Files
- `client/src/App.jsx` - Main React application
- `client/src/components/` - UI component library
- `client/src/hooks/` - Custom React hooks
- `client/src/store/` - State management
- `client/src/data-provider/` - API integration

### Shared Packages
- `packages/data-provider/` - API client library
- `packages/data-schemas/` - Database schema definitions
- `packages/api/` - Shared API utilities

## Deployment

### Docker Deployment
- `docker-compose.yml` - Development environment
- `deploy-compose.yml` - Production deployment
- Kubernetes Helm charts in `helm/` directory

### Environment Variables
Key environment variables to configure:
- Database connection strings
- AI provider API keys
- Authentication secrets
- File storage configuration
- Redis configuration for caching

## Common Development Tasks

### Adding New AI Provider
1. Create client in `api/app/clients/`
2. Add configuration in `api/server/services/Config/`
3. Update frontend provider selection
4. Add provider-specific UI components

### Adding New API Endpoint
1. Create route in `api/server/routes/`
2. Add controller in `api/server/controllers/`
3. Implement service logic
4. Add middleware as needed
5. Update frontend data provider

### Adding New UI Component
1. Create component in appropriate `client/src/components/` subdirectory
2. Add to `index.ts` exports
3. Create custom hooks if needed
4. Add to Storybook if applicable

### Database Schema Changes
1. Update model in `api/models/`
2. Update data schemas in `packages/data-schemas/`
3. Create migration script if needed
4. Update related services and controllers