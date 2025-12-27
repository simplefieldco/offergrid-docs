# OfferGrid Documentation - CLAUDE.md

## What is This Repo?

This is the **documentation repository** for OfferGrid, containing user-facing documentation, API references, guides, and tutorials. The documentation is built with **Mintlify** and deployed automatically.

**Related Repositories:**

- **Main Application**: [offergrid](https://github.com/simplefieldco/offergrid) - Monorepo with API and web app
- **Docs Site**: This repo - Public-facing documentation

## What is OfferGrid?

OfferGrid is a **B2B marketplace platform** that connects service providers with reseller partners to streamline the distribution and sale of essential services like internet, TV, security, energy, and insurance.

### Quick Summary

**For Providers:**

- Publish service offerings with pricing and availability
- Define order fulfillment workflows
- Manage reseller partnerships
- Track orders across channels

**For Resellers:**

- Search and compare services by location
- Place orders on behalf of customers
- Track order fulfillment
- Earn commissions on referrals

See the [main repo CLAUDE.md](https://github.com/simplefieldco/offergrid/blob/main/CLAUDE.md) for complete technical details.

## Technology Stack

### Documentation Platform

- **Mintlify** - Documentation platform
- **MDX** - Markdown with React components
- **OpenAPI** - API reference auto-generated from spec

### Source of Truth

- **API Spec**: Generated from main repo at `/docs/openapi.json`
- **Updates**: API reference updates automatically when spec is regenerated

## Documentation Structure

docs-repo/
├── introduction.mdx # Getting started
├── quickstart.mdx # Quick setup guide
├── api-reference/ # API documentation
│ ├── introduction.mdx # API overview
│ ├── authentication.mdx # Auth guide
│ └── openapi.json # OpenAPI spec (copied from main repo)
├── guides/ # User guides
│ ├── providers/ # Provider documentation
│ └── resellers/ # Reseller documentation
├── integrations/ # Integration guides
├── mint.json # Mintlify configuration
└── CLAUDE.md # This file

## Common Workflows

### 1. Update API Reference

When the API changes in the main repo:

````bash
# 1. In the main offergrid repo, generate new OpenAPI spec
cd /path/to/offergrid
pnpm --filter=api generate:openapi

# 2. Copy the spec to this docs repo
cp docs/openapi.json /path/to/docs-repo/api-reference/openapi.json

# 3. Commit and push
cd /path/to/docs-repo
git add api-reference/openapi.json
git commit -m "Update API reference from main repo"
git push

Important: Always use the generated spec from the main repo. Never manually edit openapi.json.

2. Add New Documentation Page

# Create new MDX file in appropriate directory
# guides/providers/managing-offers.mdx

---
title: 'Managing Service Offers'
description: 'Learn how to create, update, and manage your service offerings'
---

# Managing Service Offers

Content here...

## Creating an Offer

<Steps>
  <Step title="Navigate to Offers">
    Click on **Offers** in the sidebar
  </Step>

  <Step title="Fill in Details">
    Enter offer name, pricing, and availability
  </Step>
</Steps>

Then update mint.json to add to navigation:

{
  "navigation": [
    {
      "group": "Provider Guides",
      "pages": [
        "guides/providers/getting-started",
        "guides/providers/managing-offers"
      ]
    }
  ]
}

3. Add Code Examples

Use code blocks with language syntax:

## Example: Create an Offer

<CodeGroup>
```typescript
const offer = await fetch('https://offergrid-api.onrender.com/offers', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'x-stack-team-api-key': 'your-api-key'
  },
  body: JSON.stringify({
    name: 'High-Speed Internet 1000 Mbps',
    category: 'internet',
    monthlyPrice: 59.99
  })
});

import requests

response = requests.post(
  'https://offergrid-api.onrender.com/offers',
  headers={
    'Content-Type': 'application/json',
    'x-stack-team-api-key': 'your-api-key'
  },
  json={
    'name': 'High-Speed Internet 1000 Mbps',
    'category': 'internet',
    'monthlyPrice': 59.99
  }
)
4. Preview Documentation Locally

# Install Mintlify CLI
npm i -g mintlify

# Start dev server
mintlify dev

# Open http://localhost:3000

5. Deploy Documentation

Documentation deploys automatically when you push to main:

git add .
git commit -m "docs: add provider guide for managing offers"
git push

Mintlify will automatically build and deploy.

Documentation Best Practices

Content Guidelines

1. Be concise - Get to the point quickly
2. Use examples - Show real code and API calls
3. Add visuals - Screenshots, diagrams, videos when helpful
4. Link liberally - Reference related docs and API endpoints
5. Keep it current - Update when features change

Writing Style

- Use second person ("you can", not "users can")
- Use active voice ("Click Submit" not "Submit should be clicked")
- Use present tense ("returns" not "will return")
- Be specific - Exact button names, field labels, error messages
- Test examples - All code snippets should actually work

MDX Components

Mintlify provides useful components:

<Note>
  Important information users should know
</Note>

<Warning>
  Critical warnings about breaking changes or security
</Warning>

<Tip>
  Helpful tips and best practices
</Tip>

<Card title="Quick Start" icon="rocket" href="/quickstart">
  Get started in 5 minutes
</Card>

<Accordion title="Advanced Options">
  Collapsible content for advanced features
</Accordion>

API Reference Maintenance

Automatic Updates

The API reference is auto-generated from the OpenAPI spec. When you update openapi.json, Mintlify automatically:
- Generates endpoint documentation
- Creates request/response schemas
- Adds authentication requirements
- Includes example requests

Manual Overrides

Add custom descriptions in api-reference/ MDX files:

---
title: 'Create Offer'
openapi: 'POST /offers'
---

## Overview

This endpoint creates a new service offering for your provider team.

## Common Use Cases

- Adding a new internet speed tier
- Launching a promotional offer
- Expanding service availability to new regions

<Note>
  The `providerTeamId` is automatically set from your API key
</Note>

Environment-Specific Docs

Staging vs Production

If you have staging and production APIs, document both:

## API Base URLs

<Tabs>
  <Tab title="Production">
    ```
    https://offergrid-api.onrender.com
    ```
  </Tab>

  <Tab title="Staging">
    ```
    https://offergrid-api-staging.onrender.com
    ```
  </Tab>
</Tabs>

Common Tasks

Updating Authentication Docs

When auth changes, update api-reference/authentication.mdx:

---
title: 'Authentication'
---

# Authentication

OfferGrid uses **Stack Auth Team API Keys** for authentication.

## Getting Your API Key

1. Log into the OfferGrid dashboard
2. Navigate to **Settings** → **API Keys**
3. Click **Generate New Key**
4. Copy the key (you won't see it again!)

## Making Authenticated Requests

Include these headers in every request:

```bash
curl https://offergrid-api.onrender.com/offers \
  -H "x-stack-team-api-key: your-api-key-here"

### Adding Changelog/Release Notes

Create `changelog.mdx`:

```mdx
---
title: 'Changelog'
---

# Changelog

## January 2025

### New Features ✨

- **Offer Categories**: Now support 6 service categories
- **Bulk Import**: Upload multiple offers via CSV

### Improvements 🚀

- Faster offer search with new indexing
- Better error messages in API responses

### Breaking Changes ⚠️

- `status` field now required when creating offers
- Deprecated `submissionUrl` in favor of `submissionConfig`

Troubleshooting

Common Issues

OpenAPI spec not updating
- Verify you copied the latest spec from main repo
- Check Mintlify dashboard for build errors
- Clear Mintlify cache: delete .mintlify folder

Local preview not working
- Reinstall Mintlify CLI: npm i -g mintlify@latest
- Check mint.json for syntax errors
- Ensure all referenced files exist

Navigation not showing
- Verify page paths in mint.json match file structure
- Check for typos in file paths
- Ensure MDX files have proper frontmatter

Key Files

- mint.json - Mintlify configuration (navigation, branding, settings)
- api-reference/openapi.json - API spec (copied from main repo)
- introduction.mdx - Landing page
- quickstart.mdx - Getting started guide

Deployment

Platform: Mintlify Cloud
URL: https://docs.offergrid.io (or your configured domain)
Auto-deploy: Enabled on push to main
Build time: ~30 seconds

Related Documentation

- https://github.com/simplefieldco/offergrid/blob/main/CLAUDE.md
- https://mintlify.com/docs
- https://mdxjs.com/

Quick Commands

# Preview locally
mintlify dev

# Update API reference
cp ../offergrid/docs/openapi.json ./api-reference/openapi.json

# Deploy (automatic on push)
git push origin main

# Check Mintlify version
mintlify --version

Content Sync Process

To keep docs in sync with the main codebase:

1. Weekly: Review main repo for API changes
2. On release: Update changelog and version numbers
3. When API changes: Regenerate and copy OpenAPI spec
4. When features ship: Update relevant guides and examples

Getting Help

- Main repo issues: File in main offergrid repo
- Mintlify issues: Check https://mintlify.com/docs or support
- Content questions: Review existing docs for patterns and style

This CLAUDE.md is tailored for a docs repo that:
- Uses Mintlify for documentation
- Syncs API reference from your main repo's OpenAPI spec
- Has separate guides for providers and resellers
- Auto-deploys on push
- Follows documentation best practices
````
