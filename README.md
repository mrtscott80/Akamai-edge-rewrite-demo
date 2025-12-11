# Akamai-edge-rewrite-demo
This project demonstrates an Edge logic configuration to handle routing vanity URLs.
# Akamai Edge: Transparent Path Rewrite

## Project Overview
This project demonstrates an Edge logic configuration to handle vanity URLs for marketing campaigns without triggering a client-side redirect (301/302).

**Scenario:**
Marketing wants to use `example.com/promo` for print ads, but the actual content lives on the CMS at `/landing-pages/2024-sale.html`.

**Constraint:**
The URL in the user's browser must remain `example.com/promo` for branding consistency.

## The Architecture
The following sequence diagram illustrates the `Modify Incoming Request Path` behavior:

```mermaid
sequenceDiagram
    participant User as Browser
    participant Edge as Akamai Edge
    participant Origin as Origin Server (CMS)

    User->>Edge: GET /promo
    Note over Edge: Rule Match: Path == /promo
    Note over Edge: Behavior: Rewrite path to /landing-pages/2024-sale.html
    Edge->>Origin: GET /landing-pages/2024-sale.html
    Origin-->>Edge: Returns 200 OK (Content)
    Edge-->>User: Returns 200 OK (Content)
    Note over User: URL Bar stays: /promo
