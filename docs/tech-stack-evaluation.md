# Tech Stack Evaluation

## Project
Campus Event Registration System

## Requirements that drive the decision
List 3 to 5 requirements from your own docs/requirements.md. Include at
least 2 non-functional requirements.
- FR1: The system shall allow users to search, filter, and view upcoming campus events by category, date, and venue
- NFR1: The system shall deliver confirmation emails with QR codes within 5 seconds of form submission
- NFR2: The system shall support a minimum of 500 concurrent active users during peak registration windows without downtime.

## Options
- Option A: Static website on GitHub Pages
- Option B: Python web app with a database on a cloud host
- Option C: Low-code tool

## Decision matrix
Weight: how important the criterion is for YOUR project (1 = low, 5 = high).
Score: how well each option does (1 = poor, 5 = excellent).
Weighted score = weight x score. Add them up for each option.

| Criterion                          | Weight | A score | B score | C score |
|------------------------------------|--------|---------|---------|---------|
| Fits my requirements               |    5   |    3    |    5    |    2    |
| Skills I already have              |    4   |    5    |    3    |    4    |
| Time to build before my deadline   |    4   |    5    |    3    |    4    |
| Free hosting and tools             |    3   |    5    |    3    |    2    |
| Performance and security needs     |    4   |    3    |    3    |    2    |
| Room to grow later                 |    2   |    2    |    4    |    1    |
| **Total (weighted)**               |        |   86    |   78    |   58    |

## Decision record
- **Context:** We need to build a Campus Event Registration System within a tight semester deadline with zero budget for paid hosting. While the team has strong foundational skills in HTML, CSS, and basic web development, setting up and deploying a full Python cloud server from scratch introduces steeper learning curves and potential hosting limits.

- **Decision:** We chose **Option A: Static website on GitHub Pages** (enhanced with client-side JavaScript and lightweight external API services for form handling and email delivery).

- **Reasons:** 
1. **Highest Overall Score (86 vs. 78 and 58):** Option A scored highest in *Skills I already have* (5) and *Time to build before my deadline* (5), ensuring we can deliver a working prototype on time.
2. **Zero Cost & High Availability (NFR2):** GitHub Pages provides 100% free, reliable CDN-backed static hosting that easily handles 500+ concurrent users browsing the event catalog without server crashes.
3. **Fast Frontend Filtering (FR1):** Client-side JavaScript allows instant searching and filtering of campus events by category, date, and venue without page reloads.

- **Consequences:** 
- *What becomes easy:* Rapid UI development, instant deployment via Git push, zero server maintenance, and fast page load speeds for students.
- *What becomes hard:* Handling persistent backend state (like preventing duplicate registrations in FR2 and automated server-side QR code emailing in NFR1) requires integrating third-party serverless APIs (such as Firebase, Supabase, or EmailJS) rather than a traditional unified backend.

- **Risks and next review:** 
- *Risks:* Client-side logic can expose API keys if not properly secured, and complex multi-step Agentic AI workflows or strict database concurrency locks (preventing overbooking) are harder to enforce without a dedicated backend.
- *Next review:* We will review this architecture after **Sprint 1 (Prototype Testing)**. If third-party APIs cannot reliably meet the 5-second QR email delivery (NFR1) or duplicate-prevention rules (FR2), we will migrate the backend logic to **Option B (Python FastAPI/Flask)** while keeping the frontend on GitHub Pages.
