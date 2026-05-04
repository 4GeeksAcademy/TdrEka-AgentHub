# AgentHub Admin Panel — Specification Document

## 1. Product Description

AgentHub is a SaaS platform where companies can rent pre-configured AI agents and equip them with modular capabilities called **skills**. Each agent can be assigned skills such as web browsing, document reading, or calendar management, and deployed for specific business tasks on behalf of client companies.

The **admin user** is the AgentHub platform operator — an internal team member responsible for overseeing the entire platform. They monitor revenue and agent health, manage registered users and agents, configure agent behavior, review rental contracts, and investigate execution errors.

---

## 2. Tech Stack & Constraints

- **Markup:** HTML5 with semantic tags (`nav`, `header`, `main`, `section`, `table`, `article`, etc.)
- **Styling:** Tailwind CSS loaded via CDN only. No custom CSS files. No inline `style` attributes.
- **Interactivity:** Vanilla JavaScript only. No frameworks (React, Vue, Angular), no jQuery, no build tools.
- **Data:** All data is hardcoded. No API calls, no backend, no localStorage persistence required.
- **Dark mode:** Implemented using Tailwind's `dark:` utility classes, toggled by adding/removing the `dark` class on the `<html>` element.
- **Delivery:** A single `index.html` file (or multiple linked HTML files, one per section).

---

## 3. Section Specifications

### 3.1 Dashboard

1. **Metric Cards Grid:** Four metric cards arranged in a responsive 2×2 grid (`grid-cols-2`). Each card displays: a relevant icon (SVG or emoji), a short label, and a hardcoded value. The four metrics are: *Total Revenue This Month* ($48,320), *Discount & Coupon Losses* ($3,140), *Active Agents* (87), and *Failing Agents* (5).
2. **Card Styling:** Each card uses a distinct accent color (e.g. green for revenue, red for losses, blue for active agents, orange for failing agents), a subtle shadow (`shadow-md`), rounded corners, and sufficient internal padding. In dark mode, card backgrounds and text adapt using `dark:` variants.
3. **Weekly Activity Chart Placeholder:** A full-width `div` below the metric cards with a dashed border, a minimum height of 200px, and a centered label reading "Weekly Activity Chart — Coming Soon". It serves as a visual placeholder for a future chart component.

---

### 3.2 User Management

1. **Users Table:** A `<table>` with columns: Name, Email, Plan, Status, and Actions. Contains at least 5 hardcoded user rows. The Status column displays a colored badge: green for *Active*, red for *Suspended*, yellow for *Trial*.
2. **Action Dropdown:** Each row has a ⋮ button that opens a small dropdown menu with two options: "View detail" and "Delete". Only one dropdown can be open at a time. Clicking outside any open dropdown closes it.
3. **View Detail Modal:** Selecting "View detail" opens a modal overlay displaying the full user record (name, email, plan, status, join date, and any other relevant fields). The modal includes a visible close (✕) button in the top-right corner and closes both via that button and by clicking the semi-transparent dark backdrop behind it.

---

### 3.3 Agent Management

1. **Agent Listing:** At least 4 agent entries displayed as cards or list rows. Each entry shows: agent name, owner (referencing a user from the User Management section), a status badge (Active = green, Inactive = gray, Failing = red), and a collapsed skill list hidden by default. The four agents are: **Atlas** (owner: Marta López, Active), **Nexus** (owner: Carlos Ruiz, Failing), **Prism** (owner: Marta López, Inactive), **Echo** (owner: James O'Brien, Active).
2. **Collapsible Skill List:** Each agent has a chevron/arrow expand control. Clicking it reveals the agent's associated skills using a smooth CSS `max-height` transition (toggled via a Tailwind class). Clicking again collapses the list. The skill list is collapsed by default on page load.
3. **Action Dropdown:** Each agent has a ⋮ dropdown with two options: "Configure" and "Delete". Selecting "Configure" opens a modal containing the agent's system prompt displayed inside an editable `<textarea>`. The modal closes via a close button and via backdrop click.

---

### 3.4 Skills

1. **Contextual Explanation:** A brief paragraph at the top of the section explains what a skill is in the AgentHub context: *"Skills are modular capabilities that can be attached to agents, extending what they can do — such as browsing the web, reading documents, or managing calendars."*
2. **Skills Catalog:** At least 4 skill entries displayed as cards or a styled list. Each entry shows: skill name, a short description, and a badge indicating how many agents currently have it enabled. Skills: *Web Browsing* (23 agents), *Document Reader* (41 agents), *Calendar Manager* (17 agents), *Email Composer* (29 agents).
3. **Action Dropdown:** Each skill has a ⋮ dropdown with "View detail" (opens a modal with the full skill description and usage stats) and "Delete". Dropdowns follow the same open/close behavior as in other sections.

---

### 3.5 Agent Contracts

1. **Contracts Table:** A `<table>` with columns: Client, Agent, Skills, Start Date, End Date, Amount Paid, and Actions. Contains at least 4 hardcoded contracts. Agent names must match those defined in Agent Management (Atlas, Nexus, Prism, Echo) to ensure data consistency.
2. **Action Dropdown:** Each row has a ⋮ dropdown. The only required option is "View detail", which opens a modal with the full contract breakdown.
3. **Contract Detail Modal:** The modal displays all contract fields plus an itemized table of contracted skills with their individual prices, summing to the total amount paid. The modal closes via a close button and via backdrop click.

---

### 3.6 Error Log

1. **Error Entries:** At least 6 hardcoded error entries displayed in a table or card list. Each entry shows: timestamp, agent name (must match Atlas, Nexus, or Echo from Agent Management), error type badge, and a short description. Error types and their badge colors: *Runtime Error* (red), *Timeout* (orange), *Auth Failure* (yellow), *Config Error* (purple).
2. **Color-Coded Badges:** Each error type uses a distinct Tailwind background and text color combination for its badge, making error severity scannable at a glance. Badge styles are consistent across the entire panel.
3. **Action Dropdown:** Each entry has a ⋮ dropdown with two options: "View detail" (opens a modal showing the full error trace in a monospace `<pre>` or `<code>` block) and "Mark as resolved" (visually marks the row as resolved, e.g. dimmed opacity or strikethrough text, without removing it from the list).

---

## 4. Component Inventory

| Component | Description |
|---|---|
| **Sidebar** | Persistent left-side navigation with links to all 6 sections. Highlights the active section. |
| **Top Bar** | Fixed header containing the app name/logo and the dark mode toggle button. |
| **Metric Card** | Reusable card with icon, label, hardcoded value, accent color, and shadow. Used in Dashboard. |
| **Action Dropdown** | A ⋮ trigger button that reveals a small positioned menu with 2–3 options. Used in all sections. Closes on outside click. |
| **Modal Overlay** | A full-screen semi-transparent backdrop with a centered content panel. Includes a close button. Closes on backdrop click. |
| **Status Badge** | A small pill/chip component with background color and text indicating a status or category (Active, Failing, error types, etc.). |
| **Collapsible Skill List** | A toggleable list of skills inside an agent entry, hidden by default, revealed with a max-height CSS transition. |
| **Dark Mode Toggle** | A button in the top bar that adds/removes the `dark` class on `<html>`, switching the full panel color scheme. |

---

## 5. Acceptance Criteria

1. `SPECS.md` is committed to the repository in a separate Git commit before any HTML file.
2. All six sections (Dashboard, User Management, Agent Management, Skills, Agent Contracts, Error Log) are accessible from the sidebar navigation.
3. Only one section is visible at a time; clicking a sidebar link shows the corresponding section and hides all others.
4. The active sidebar link has a distinct visual indicator (e.g. background highlight or accent color).
5. The dark/light mode toggle switches the entire panel color scheme; dark mode is implemented using Tailwind's `dark:` utilities applied via the `dark` class on `<html>`.
6. The chosen dark/light mode is maintained when navigating between sections.
7. All ⋮ action dropdowns open on click and close when clicking outside the menu area.
8. Only one dropdown is open at a time — opening a new one closes the previous.
9. "View detail" opens a modal in at least four different sections (User Management, Agent Management, Skills, Agent Contracts, Error Log).
10. All modals close via the close (✕) button.
11. All modals close via clicking the semi-transparent backdrop.
12. Agent skill lists are collapsed by default on page load.
13. Clicking the expand control on an agent entry reveals its skill list with a visible smooth transition; clicking again collapses it.
14. The "Configure" option in Agent Management opens a modal with the agent's system prompt in an editable `<textarea>`.
15. "Mark as resolved" in the Error Log visually alters the affected row (dimmed, strikethrough, or similar) without removing it.
16. Hardcoded data is consistent: the agent names Atlas, Nexus, Prism, and Echo appear across Agent Management, Agent Contracts, and Error Log.
17. The same user names (e.g. Marta López, Carlos Ruiz, James O'Brien) appear as agent owners in Agent Management and as clients or references elsewhere.
18. Semantic HTML tags are used correctly throughout (`<nav>`, `<header>`, `<main>`, `<section>`, `<table>`, `<article>`).
19. No custom CSS files, no inline `style` attributes, and no JavaScript frameworks are used anywhere.
20. The layout is usable and readable on both desktop and tablet viewports.