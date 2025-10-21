# Contributing to AutoRFP

Thank you for your interest in contributing to AutoRFP! We're excited to have you join our community of contributors working to make RFP response generation faster and smarter.

## 🤝 How to Contribute

### Reporting Issues

Before creating an issue, please:

1. **Search existing issues** to avoid duplicates
2. **Use a clear and descriptive title** that summarizes the problem
3. **Provide detailed information** including:
   - Steps to reproduce the issue
   - Expected vs. actual behavior
   - Environment details (OS, Node version, browser)
   - Screenshots or error messages if applicable
4. **Label appropriately** (bug, enhancement, documentation, etc.)

### Feature Requests

We welcome feature requests! When proposing new features:

1. **Explain the use case** - Why is this feature valuable?
2. **Describe the expected behavior** - How should it work?
3. **Consider the impact** - How does it affect existing functionality?
4. **Propose an implementation** - Share your technical ideas if you have them

### Pull Requests

Ready to contribute code? Follow these steps:

1. **Fork the repository** and create a new branch from `main`
2. **Follow our coding standards** (see below)
3. **Write clear, descriptive commit messages**
4. **Add tests** for new functionality
5. **Update documentation** as needed
6. **Ensure all checks pass** before submitting
7. **Reference related issues** in your PR description

## 🏗 Development Setup

### Prerequisites

Make sure you have these installed:

- **[Node.js](https://nodejs.org/)** v18.x or later
- **[pnpm](https://pnpm.io/)** v8.x or later
- **[Git](https://git-scm.com/)** for version control
- **[PostgreSQL](https://www.postgresql.org/)** database (local or cloud)

You'll also need accounts for:

- **[Supabase](https://supabase.com/)** (for authentication)
- **[OpenAI](https://platform.openai.com/)** (with API credits)
- **[LlamaCloud](https://cloud.llamaindex.ai/)** (optional but recommended)

### Local Development

```bash
# 1. Fork and clone the repository
git clone https://github.com/your-username/tata-rfp.git
cd tata-rfp

# 2. Install dependencies
pnpm install

# 3. Copy environment file and configure
cp .env.example .env.local
# Edit .env.local with your configuration

# 4. Set up the database
psql -c "CREATE DATABASE auto_rfp;"

# 5. Generate Prisma client and run migrations
pnpm prisma generate
pnpm prisma migrate deploy

# 6. Start development server
pnpm dev
```

The application will be available at `http://localhost:3000`

### Environment Configuration

Create a `.env.local` file with the following variables:

```env
# Database
DATABASE_URL="postgresql://username:password@localhost:5432/auto_rfp"
DIRECT_URL="postgresql://username:password@localhost:5432/auto_rfp"

# Supabase Configuration
NEXT_PUBLIC_SUPABASE_URL="your-supabase-project-url"
NEXT_PUBLIC_SUPABASE_ANON_KEY="your-supabase-anon-key"

# OpenAI API
OPENAI_API_KEY="your-openai-api-key"

# LlamaCloud (Optional)
LLAMACLOUD_API_KEY="your-llamacloud-api-key"

# App Configuration
NEXT_PUBLIC_APP_URL="http://localhost:3000"
```

#### Setting Up External Services

**Supabase Setup:**
1. Create a new project at [Supabase](https://supabase.com/)
2. Get your project URL and anon key from Project Settings > API
3. Configure authentication providers in Authentication > Providers
4. Set up email templates for magic link authentication

**OpenAI Setup:**
1. Create an account at [OpenAI Platform](https://platform.openai.com/)
2. Generate an API key from API Keys section
3. Add credits to your account for API usage

**LlamaCloud Setup (Optional):**
1. Create an account at [LlamaCloud](https://cloud.llamaindex.ai/)
2. Create a new project
3. Generate an API key from your project settings

## 📝 Coding Standards

### TypeScript

- **Use TypeScript** for all new code
- **Define proper interfaces** and types for all data structures
- **Avoid using `any`** - use proper typing or `unknown` when type is truly unknown
- **Export types** from dedicated files when shared across components

Example:
```typescript
// Good
interface UserProfile {
  id: string;
  email: string;
  createdAt: Date;
}

// Avoid
const user: any = getData();
```

### React Components

Use functional components with TypeScript:

```typescript
interface MyComponentProps {
  title: string;
  onAction: () => void;
  optional?: boolean;
}

export function MyComponent({ 
  title, 
  onAction, 
  optional = false 
}: MyComponentProps) {
  return (
    <div>
      <h1>{title}</h1>
      {optional && <button onClick={onAction}>Action</button>}
    </div>
  );
}
```

### File Naming Conventions

- **Components**: PascalCase (`OrganizationCard.tsx`)
- **Pages**: kebab-case (`create-organization.tsx`)
- **Utilities**: camelCase (`formatDate.ts`)
- **API routes**: kebab-case (`extract-questions.ts`)
- **Types/Interfaces**: PascalCase (`ProjectTypes.ts`)

### Import Order

Organize imports in this order:

```typescript
// 1. External imports
import React from 'react';
import { NextRequest } from 'next/server';

// 2. Internal components
import { Button } from '@/components/ui/button';
import { ProjectCard } from '@/components/projects/project-card';

// 3. Services and utilities
import { db } from '@/lib/db';
import { formatDate } from '@/lib/utils';

// 4. Types and interfaces
import type { Project } from '@/types/project';

// 5. Styles (if any)
import styles from './component.module.css';
```

### API Routes

Follow this pattern for all API endpoints:

```typescript
import { NextRequest } from 'next/server';
import { apiHandler } from '@/lib/middleware/api-handler';
import { CreateProjectSchema } from '@/lib/validators/project';

export async function POST(request: NextRequest) {
  return apiHandler(async () => {
    const body = await request.json();
    
    // Validate input with Zod
    const validatedData = CreateProjectSchema.parse(body);
    
    // Business logic
    const project = await createProject(validatedData);
    
    // Return response
    return {
      success: true,
      data: project
    };
  });
}
```

### Styling Guidelines

We use **Tailwind CSS** for styling:

- Use Tailwind utility classes for most styling
- Follow mobile-first responsive design principles
- Use the `cn()` utility for conditional classes
- Keep custom CSS minimal and component-scoped

```typescript
import { cn } from '@/lib/utils';

<div className={cn(
  "rounded-lg p-4",
  isActive && "bg-blue-50 border-blue-500",
  isDisabled && "opacity-50 cursor-not-allowed"
)}>
  Content
</div>
```

## 🗂 Project Structure

Understanding the project structure will help you navigate the codebase:

```
auto_rfp/
├── app/                          # Next.js 15 App Router
│   ├── api/                      # API routes
│   │   ├── extract-questions/    # Question extraction
│   │   ├── generate-response/    # AI response generation
│   │   ├── llamacloud/          # LlamaCloud integration
│   │   ├── organizations/       # Organization management
│   │   └── projects/            # Project management
│   ├── auth/                    # Authentication pages
│   ├── login/                   # Login flow
│   ├── organizations/           # Organization pages
│   ├── projects/                # Project pages
│   ├── upload/                  # Document upload
│   └── globals.css              # Global styles
│
├── components/                   # Reusable components
│   ├── ui/                      # Base UI (shadcn/ui)
│   ├── organizations/           # Organization components
│   ├── projects/                # Project components
│   └── upload/                  # Upload components
│
├── lib/                         # Core libraries
│   ├── services/                # Business logic
│   ├── interfaces/              # TypeScript interfaces
│   ├── validators/              # Zod schemas
│   ├── utils/                   # Utility functions
│   ├── errors/                  # Error definitions
│   └── db.ts                    # Database client
│
├── prisma/                      # Database
│   ├── schema.prisma            # Database schema
│   └── migrations/              # Migration files
│
├── types/                       # Type definitions
└── providers/                   # React context providers
```

### Component Organization

- **Single Responsibility**: Each component should have one clear purpose
- **Reusability**: Design components to be reusable across the application
- **Composition**: Prefer composition over large monolithic components
- **Co-location**: Keep related files close (component, styles, tests)

### Service Layer Pattern

Business logic lives in service classes under `lib/services/`:

```typescript
// lib/services/project-service.ts
export class ProjectService {
  async createProject(data: CreateProjectData) {
    // Validation
    // Database operations
    // Return result
  }
  
  async getProjectById(id: string) {
    // Implementation
  }
}
```

## 🧪 Testing

### Running Tests

```bash
# Run all tests
pnpm test

# Run tests in watch mode
pnpm test:watch

# Run with coverage
pnpm test:coverage

# Type checking
pnpm type-check

# Linting
pnpm lint

# Fix linting issues automatically
pnpm lint:fix
```

### Writing Tests

- **Test user behavior**, not implementation details
- **Use descriptive test names** that explain what's being tested
- **Follow the Arrange-Act-Assert (AAA) pattern**
- **Mock external dependencies** (API calls, database, etc.)
- **Test edge cases** and error conditions

Example test:

```typescript
describe('ProjectCard', () => {
  it('should display project name and description', () => {
    const project = {
      name: 'Test Project',
      description: 'Test description'
    };
    
    render(<ProjectCard project={project} />);
    
    expect(screen.getByText('Test Project')).toBeInTheDocument();
    expect(screen.getByText('Test description')).toBeInTheDocument();
  });
});
```

## 🔄 Database Changes

### Making Schema Changes

1. **Update `prisma/schema.prisma`** with your changes
2. **Create a migration**:
   ```bash
   pnpm prisma migrate dev --name descriptive-migration-name
   ```
3. **Test the migration** thoroughly
4. **Update TypeScript types** if needed
5. **Document breaking changes** in your PR

### Migration Best Practices

- **Use descriptive names**: `add-user-preferences` not `update1`
- **Test on sample data**: Ensure migrations work on realistic data
- **Consider backward compatibility**: Will this break existing functionality?
- **Handle data transformation**: If changing data types, provide migration logic
- **Document in PR**: Explain what changed and why

Example schema change:

```prisma
model Project {
  id          String   @id @default(cuid())
  name        String
  description String?
  // New field
  status      String   @default("active")
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
}
```

## 📚 Documentation

### Code Documentation

- **Comment complex logic** with clear explanations
- **Use JSDoc** for public functions and classes
- **Update README** for significant feature additions
- **Document API endpoints** with request/response examples

Example JSDoc:

```typescript
/**
 * Creates a new organization with the specified details
 * 
 * @param name - The organization name (required)
 * @param description - Optional organization description
 * @param userId - ID of the user creating the organization
 * @returns Promise resolving to the created organization
 * @throws {ValidationError} If name is invalid
 * @throws {DatabaseError} If database operation fails
 */
export async function createOrganization(
  name: string,
  description: string | null,
  userId: string
): Promise<Organization> {
  // Implementation
}
```

### API Documentation

Document all API endpoints with:

- **Method and route**
- **Request body/params**
- **Response format**
- **Error responses**
- **Authentication requirements**

## 🚀 Deployment and Release

### Pre-deployment Checklist

Before submitting a PR or deploying:

- [ ] All tests pass locally
- [ ] No TypeScript errors (`pnpm type-check`)
- [ ] No linting errors (`pnpm lint`)
- [ ] Database migrations tested
- [ ] Environment variables documented
- [ ] README/documentation updated
- [ ] Breaking changes documented

### Pull Request Process

1. **Create a feature branch** from `main`:
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make your changes** following all guidelines above

3. **Commit with clear messages**:
   ```bash
   git commit -m "feat: add project export functionality"
   ```

4. **Push to your fork**:
   ```bash
   git push origin feature/your-feature-name
   ```

5. **Create a Pull Request** with:
   - Clear title and description
   - Reference to related issues
   - Screenshots for UI changes
   - List of changes made
   - Testing steps

6. **Address review feedback** promptly

7. **Merge after approval** from maintainers

### Commit Message Convention

We follow conventional commits:

- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation changes
- `style:` Code style changes (formatting)
- `refactor:` Code refactoring
- `test:` Adding or updating tests
- `chore:` Maintenance tasks

## 🎯 Priority Contribution Areas

### High-Impact Areas

These areas would benefit most from contributions:

1. **Testing Coverage**
   - Unit tests for services
   - Integration tests for API routes
   - E2E tests for critical flows

2. **Documentation**
   - Inline code documentation
   - API endpoint documentation
   - User guides and tutorials

3. **Performance Optimization**
   - Database query optimization
   - API response caching
   - Frontend bundle size reduction

4. **Accessibility**
   - ARIA labels and roles
   - Keyboard navigation
   - Screen reader compatibility

5. **Mobile Responsiveness**
   - Touch-friendly interactions
   - Responsive layouts
   - Progressive Web App features

### Feature Ideas

Looking for ideas? Consider these:

- **Export Functionality**: Export RFP responses to various formats (DOCX, PDF, CSV)
- **Template System**: Pre-built templates for common RFP scenarios
- **Analytics Dashboard**: Usage analytics and response metrics
- **Collaboration Tools**: Real-time collaboration features
- **Integration APIs**: Connect with CRM systems (Salesforce, HubSpot)
- **Advanced Search**: Full-text search across all documents
- **Version Control**: Track changes to responses over time
- **Bulk Operations**: Process multiple RFPs simultaneously

## 💬 Getting Help

### Where to Ask Questions

- **GitHub Discussions**: For questions and general discussion
- **GitHub Issues**: For bugs and feature requests
- **Email**: bytebardderia@gmail.com for private inquiries

### Code Review Guidelines

When reviewing code:

- **Be constructive and respectful** in all feedback
- **Explain reasoning** behind suggestions
- **Suggest alternatives** when requesting changes
- **Focus on code quality**, not personal preferences
- **Ask questions** if something is unclear
- **Acknowledge good work** when you see it

When your code is reviewed:

- **Be open to feedback** - it helps improve the code
- **Ask for clarification** if you don't understand
- **Explain your decisions** if questioned
- **Don't take it personally** - it's about the code, not you

## 🐛 Troubleshooting Common Issues

### Database Connection Issues

```bash
# Test database connection
pnpm prisma db pull

# Reset database (WARNING: deletes all data)
pnpm prisma migrate reset
```

### Authentication Issues

- Verify Supabase URL and keys in `.env.local`
- Check redirect URLs in Supabase project settings
- Ensure email templates are configured correctly

### Build Errors

```bash
# Clear Next.js cache
rm -rf .next

# Clear node_modules and reinstall
rm -rf node_modules pnpm-lock.yaml
pnpm install

# Clear Prisma client
pnpm prisma generate
```

### AI Processing Issues

- Verify OpenAI API key has sufficient credits
- Check LlamaCloud API key and project configuration
- Ensure document formats are supported (PDF, DOCX, XLSX, PPTX)

## 📄 License

By contributing to AutoRFP, you agree that your contributions will be licensed under the **MIT License**.

## 🙏 Acknowledgments

Thank you for taking the time to contribute to AutoRFP! Your efforts help make RFP response generation faster and more efficient for everyone.

---

<div align="center">

**Questions?** Reach out to [@RanitDERIA](https://github.com/RanitDERIA](https://github.com/RanitDERIA/tata-rfp/issues))

**Happy Contributing!** 🚀

</div>
