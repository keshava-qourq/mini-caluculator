<!-- sdlc:auto:start adr -->
# ADR-0004: Use AWS for Cloud

Status: Accepted  
Date: 2026-11-17

## Context and Problem Statement

Which Cloud technology does the project use? Decided in architecture v1.

## Considered Options

- AWS
- Netlify
- Cloudflare Pages

## Decision Outcome

Chosen option: AWS, because AWS hosts the responsive single page cheaply and serves it globally via CloudFront to anonymous visitors on desktop and mobile, satisfying the compatibility and immediate-use needs. It is the platform default.

## Consequences

A specialized static host could be marginally simpler, but AWS keeps the whole stack on one approved cloud and the footprint stays very small with no accounts or stored data.
<!-- sdlc:auto:end adr -->