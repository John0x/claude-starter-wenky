# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

- `npm run dev` - Start development server on http://localhost:3000
- `npm run build` - Build production application
- `npm run start` - Start production server
- `npm run lint` - Run ESLint
- `npm run typecheck` - Run TypeScript type checking
- `npm run test` - Run Playwright end-to-end tests

## Framework and Library Recommendations

For this web application project, use the following technologies:

- **Next.js** - React framework with App Router
- **Tailwind CSS** - Utility-first styling framework
- **shadcn/ui** - Component library (using shadcn@latest CLI)
- **Supabase** - Backend and authentication
- **Zod** - Input validation
- **React Hook Form** - Form handling
- **React Query** - Data fetching and caching
- **polar.sh** - Payment processing (see https://docs.polar.sh/integrate/sdk/adapters/nextjs for setup)
- **Playwright** - End-to-end testing

**ALWAYS** use TypeScript with strict type checking over JavaScript.
**NEVER** create projects from scratch - always use framework CLIs to scaffold projects.

## Architecture

This is a Next.js 15 application using the App Router with:

- **Framework**: Next.js 15 with React 19
- **Styling**: Tailwind CSS 4 with custom CSS variables
- **UI Components**: shadcn/ui components in "new-york" style with Radix primitives
- **Testing**: Playwright for end-to-end testing
- **Fonts**: Geist Sans and Geist Mono from Google Fonts
- **Charts**: Recharts for data visualization
- **Theme**: next-themes for dark/light mode support
- **Notifications**: Sonner for toast notifications
- **Backend**: Supabase integration configured
- **Forms**: React Hook Form with Zod validation
- **Additional Libraries**: Embla Carousel, Command Menu (cmdk), Date handling (date-fns)

### Project Structure

- `app/` - Next.js App Router pages and layouts
- `components/ui/` - Complete shadcn/ui component library including accordion, alert-dialog, avatar, badge, breadcrumb, button, calendar, card, carousel, checkbox, collapsible, command, context-menu, dialog, drawer, dropdown-menu, form, hover-card, input, input-otp, label, menubar, navigation-menu, pagination, popover, progress, radio-group, resizable, scroll-area, select, separator, sheet, sidebar, skeleton, slider, sonner, switch, table, tabs, textarea, toggle, tooltip, and more
- `hooks/` - Custom React hooks (e.g., `use-mobile.ts` for responsive design)
- `lib/utils.ts` - Utility functions including Tailwind class merging
- `supabase/` - Supabase configuration and setup
- `tests/` - Playwright test files
- `public/` - Static assets

### shadcn/ui Configuration

Components are configured with:
- Style: "new-york"
- Base color: neutral
- CSS variables enabled
- Icon library: lucide-react
- Path aliases: `@/components`, `@/lib/utils`, etc.

### Playwright Configuration
- Tests run against all major browsers (Chrome, Firefox, Safari)
- Base URL: http://localhost:3000
- Auto-starts dev server if not running, reuses existing server if available
- 2-minute timeout for server startup

## Validation Strategy

**ALWAYS** work iteratively and validate your work after finishing each task by following these steps in order:

### Quick Validation Steps (run for each task)
1. **Linting**: `npm run lint` - Check for syntax and style issues
2. **Specific tests**: Run only relevant Playwright tests for changed functionality
3. **Type checking**: `npm run typecheck` - Ensure TypeScript correctness

### Complete Validation (run only after all tasks are complete)
4. **Build**: `npm run build` - Full production build verification
5. **Complete test suite**: `npm run test` - All Playwright end-to-end tests

### Testing Guidelines
- **ALWAYS** write tests for new functionality - this is required for validation
- Write realistic e2e tests from a user perspective focusing on actual interactions
- **NEVER** write trivial tests that only assert component visibility
- Focus on meaningful user workflows and business logic
- If existing tests fail that are not part of the current task, **STOP** and ask for guidance
- Do NOT auto-fix unrelated test failures