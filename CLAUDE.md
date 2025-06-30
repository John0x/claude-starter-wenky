# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Workflow

**MANDATORY: Follow this iterative development process for ALL tasks (including UI-only changes):**

### Pre-Development Setup
- Verify current tests pass: `npm run test` (dev server will start automatically if needed)

### For Each Feature/Change (Iterate):

1. **Plan the feature** 
   - Break down into smallest testable unit
   - Consider happy path, error cases, edge cases, and accessibility

2. **Implement the feature**
   - Write production-ready code following existing patterns
   - Include proper error handling and validation

3. **Immediate code quality checks**
   - Run linting: `npm run lint`
   - Fix any linting issues immediately
   - Verify TypeScript compilation (if build fails, feature is incomplete)

4. **Write comprehensive test**
   - Create specific Playwright test for the feature
   - Include happy path, error cases, and edge cases
   - Add accessibility checks where relevant
   - Use descriptive test names and organize in logical test files
   - Never assert styling like classes. Focus on interactions and behavior
   - Never assert visibility unless it is to make sure that a component is rendered when testing interactions
   - **IMPORTANT**: UI-only changes still require tests, if the parts are not covered by other tests

5. **Validate implementation**
   - Run the relevant tests only: `npm run test -- --grep "specific-test-name"`
   - Fix any issues before proceeding

6. **Clean up test state**
   - Ensure tests don't leave persistent state that affects other tests
   - Use proper test cleanup and data isolation

### Post-Development Validation

7. **Full integration validation**
   - Run complete test suite: `npm run test`
   - Run production build: `npm run build`
   - Fix any regressions or build failures
   - All tests must pass before task is considered complete

### Test Organization Guidelines
- Group related tests in `test.describe()` blocks
- Use page object patterns for complex UI interactions
- Create reusable test utilities in `tests/utils/`
- Name test files descriptively (e.g., `auth-flow.spec.ts`, `dashboard-navigation.spec.ts`)

## Development Commands

- `npm run dev` - Start development server on http://localhost:3000
- `npm run build` - Build production application
- `npm run start` - Start production server
- `npm run lint` - Run ESLint
- `npm run test` - Run Playwright end-to-end tests

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