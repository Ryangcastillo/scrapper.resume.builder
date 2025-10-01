# Tasks Master Plan: Testing, Performance, Email, and Deployment

This document breaks down the requested initiatives into Epics and Tickets with clear next actions. Each ticket ends with a short progress note placeholder.

---

## Epic 9: Testing Framework Enablement

### 🎯 Goal
Implement a comprehensive testing strategy that covers unit, integration, and end-to-end (E2E) scenarios for the CiVi platform.

### Tickets
- **9.1 Establish Testing Toolchain**  
  - Decide on Jest + React Testing Library for unit tests, MSW for API mocking, Playwright for E2E.  
  - Add `npm` scripts (e.g., `test`, `test:watch`, `test:e2e`).  
  - Configure base Jest setup (`jest.config.js`, `setupTests.js`).  
  - Progress: _Not started_

- **9.2 Unit Test Coverage for Critical Components**  
  - Identify top-priority components (e.g., `JobCard`, `CVEditor`, `Heatmap`).  
  - Write unit tests covering render states, props interactions, and error handling.  
  - Target 80% coverage for selected components.  
  - Progress: _Not started_

- **9.3 Integration Tests for API Routes**  
  - Use `supertest` (or Playwright API) to validate `/api/scrape`, `/api/parse-cv`, `/api/match`, `/api/export-cv`.  
  - Mock Oracle DB layer via dependency injection or MSW server.  
  - Ensure responses conform to expected schema and handle failure paths.  
  - Progress: _Not started_

- **9.4 E2E Flow Automation**  
  - Script Playwright journeys for: upload CV → parse → match results → export CV.  
  - Include login/auth placeholder if required.  
  - Capture screenshots and artifacts for CI.  
  - Progress: _Not started_

---

## Epic 10: Performance Optimization

### 🎯 Goal
Improve perceived and actual performance of the Next.js application through caching, lazy loading, and PWA capabilities.

### Tickets
- **10.1 Implement API Response Caching**  
  - Cache scraped job results using Redis or Vercel KV.  
  - Apply SWR caching on the client for frequently accessed data.  
  - Document cache invalidation (cron job or webhook).  
  - Progress: _Not started_

- **10.2 Lazy Load Heavy Components**  
  - Convert non-critical components (heatmaps, AI suggestions) to dynamic imports with suspense/loading states.  
  - Audit bundle using `next build --analyze`.  
  - Progress: _Not started_

- **10.3 PWA Enhancements**  
  - Integrate `next-pwa` for service worker, offline caching, and install prompts.  
  - Provide manifest with NZ-centric branding.  
  - Test Lighthouse PWA score ≥ 80.  
  - Progress: _Not started_

---

## Epic 11: Email Integration for RSVP & Notifications

### 🎯 Goal
Deliver reliable email workflows for interview RSVPs and status notifications to candidates and hiring partners.

### Tickets
- **11.1 Choose Email Provider & Configure Env**  
  - Evaluate providers (SendGrid, Postmark, AWS SES).  
  - Add environment variables to `.env.example`.  
  - Create helper in `lib/email.js` to send templated emails.  
  - Progress: _Not started_

- **11.2 RSVP Confirmation Flow**  
  - API route `/api/rsvp` validates payload, stores RSVP status, triggers confirmation email.  
  - Email template: includes job title, interview slot, reschedule link.  
  - Add unit tests for RSVP handler + email send stub.  
  - Progress: _Not started_

- **11.3 Notification Preferences**  
  - Extend user profile schema with notification toggles (match updates, interview reminders).  
  - Build UI in settings page to manage preferences.  
  - Send digest emails using cron or serverless scheduled functions.  
  - Progress: _Not started_

---

## Epic 12: Deployment Pipeline with Vercel CI/CD

### 🎯 Goal
Automate build, testing, and deployment using Vercel with performance optimizations baked into the pipeline.

### Tickets
- **12.1 Configure GitHub → Vercel Integration**  
  - Set up preview deployments per PR.  
  - Protect `main` branch with required checks (tests, lint, build).  
  - Document environment variable setup on Vercel.  
  - Progress: _Not started_

- **12.2 Add CI Workflow**  
  - Create `.github/workflows/ci.yml` running install, lint, unit/integration/E2E tests.  
  - Cache `node_modules` and Playwright browsers for faster builds.  
  - Upload Playwright traces on failure.  
  - Progress: _Not started_

- **12.3 Performance Budgets in Pipeline**  
  - Add Lighthouse CI or Vercel analytics step enforcing performance budgets (TTI, LCP).  
  - Block deploy if thresholds exceeded.  
  - Progress: _Not started_

---

### Next Steps
1. Confirm priorities with product owner to sequence Epics 9–12 alongside existing roadmap.  
2. Assign owners and deadlines for each ticket.  
3. Begin with Epic 9.1 (testing toolchain) to unblock the rest of the work.

