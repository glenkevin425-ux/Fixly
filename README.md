# Fixly — full frontend milestone (customer, provider & admin)

Covers the whole spec's frontend: **landing → provider discovery → provider profile → 6-step booking flow → customer dashboard → provider dashboard → admin dashboard**, fully interactive on realistic mock data. Only auth (`/login`, `/register`) is left as the styled 404 — everything else routes.

## Design direction

Dark charcoal/lime brand from the brief, executed through a "service ticket" motif: bookings, prices and statuses are treated like work-order stubs — dashed perforations, mono uppercase labels, ticket IDs (`#FX-08234`). Space Grotesk for display type, Inter for body, IBM Plex Mono for tickets/data.

## Run it locally

Requires Node 18.18+.

```bash
npm install
npm run dev
```

Then open http://localhost:3000.

> Built and reviewed without a network connection in the sandbox that generated it, so it has **not** been run through `next build` yet. If `npm run dev` throws anything, it'll most likely be a small import-path or type nit — flag it and I'll patch it immediately.

## What's interactive right now

- **Landing** (`/`) — ticket-styled hero search routes into `/providers` with query params, category grid, featured professionals.
- **`/services`** and **`/services/[slug]`** — category browsing, filtered provider lists per category.
- **`/providers`** — live search, category/distance/price/rating/availability filters, verified-only toggle, sort, mobile filter drawer, empty state.
- **`/providers/[id]`** — full profile: about, services & pricing, portfolio, reviews, availability strip.
- **`/book/[providerId]`** — 6-step booking wizard (service → date/time → location → details → photos → review) with live pricing, photo upload preview, and a confirmation ticket on submit. All state is local — nothing persists.
- **`/dashboard`** — overview with stats, upcoming booking, quick actions.
- **`/dashboard/bookings`** — list/detail view with tabs (Active/Completed/All) and the 6-stage status timeline (Requested → Accepted → Scheduled → Provider arrived → In progress → Completed).
- **`/dashboard/favorites`** — saved providers, removable.
- **`/dashboard/messages`** — thread list + live conversation view, send appends locally.
- **`/dashboard/profile`** — editable form with validation and a save confirmation.
- **`/provider`** — provider overview for John Mwangi: today's schedule, pending requests, earnings chart, recent reviews, availability toggle.
- **`/provider/jobs`** — Today/Upcoming/Completed tabs with the same status timeline.
- **`/provider/requests`** — accept/decline incoming job requests, live-updating list.
- **`/provider/calendar`** — 7-day strip, per-day availability toggle, jobs per day.
- **`/provider/messages`** — customer threads from the provider's side.
- **`/provider/services`** — add/edit/deactivate/remove services and pricing.
- **`/provider/earnings`** — monthly chart and payout history.
- **`/provider/profile`** — editable business profile with validation.
- **`/admin`** — platform stats, revenue/bookings/user-growth charts, popular services, recent activity.
- **`/admin/users`**, **`/admin/bookings`**, **`/admin/reviews`** — searchable, filterable, sortable, paginated tables with status badges; reviews support flag-clearing and removal.
- **`/admin/providers`** — provider table plus an applications tab with approve/reject.
- **`/admin/reports`** — exportable report cards (mock export, no real file).

## Structure

```
app/            routes (App Router)
components/ui   button, input, badge primitives
components/     layout, home, providers, booking sections
data/           mock services.ts, providers.ts, bookings.ts, messages.ts, favorites.ts, provider-portal.ts, provider-messages.ts, admin.ts
types/          shared TS types
lib/utils.ts    cn(), formatKsh(), ticketId()
```

Mock data lives in `data/`, typed via `types/index.ts` — swapping to Supabase later means replacing the functions in `data/*.ts` with queries, not touching the components.

## Next milestones (not built yet)

Auth (`/login`, `/register`) and connecting `data/*.ts` to a real Supabase backend.
