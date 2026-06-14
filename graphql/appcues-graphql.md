# Appcues GraphQL Schema

## Overview

This conceptual GraphQL schema represents the Appcues platform — a product-led growth and in-app onboarding tool. Appcues enables teams to build flows, checklists, pins, NPS surveys, and launchpad experiences that guide users through product adoption without requiring engineering resources.

The schema covers the core Appcues Public API surface (US and EU regions: `https://api.appcues.com`) including flows, steps, audiences, segments, users, companies, events, properties, analytics, and account management.

## Schema Source

Conceptual schema derived from:
- Appcues Public API: https://api.appcues.com/
- Developer documentation: https://docs.appcues.com/dev-docs
- Developer overview: https://docs.appcues.com/dev-overview/

## Types

### Experience Types
- `Flow` — Core in-app experience (tour, announcement, survey, etc.)
- `FlowDetails` — Full flow record with content, targeting, and analytics
- `FlowType` — Enum: TOUR, MODAL, SLIDEOUT, TOOLTIP, BANNER, HOTSPOT, NPS
- `FlowStatus` — Enum: DRAFT, PUBLISHED, PAUSED, ARCHIVED
- `FlowTrigger` — Conditions that launch a flow (page, event, manual)
- `FlowAudience` — Audience targeting rules applied to a flow
- `FlowGoal` — Conversion goal attached to a flow
- `FlowContent` — Serialized content payload for a flow

### Step Types
- `Step` — Individual step within a flow
- `StepDetails` — Full step record with content, layout, and targeting
- `StepType` — Enum: MODAL, TOOLTIP, HOTSPOT, BANNER, FORM, NUDGE, SLIDEOUT
- `StepContent` — Rich content blocks within a step
- `FormStep` — Step subtype with form fields and submission handling
- `TooltipStep` — Step subtype anchored to a DOM element
- `ModalStep` — Step subtype rendered as a centered modal
- `HotspotStep` — Step subtype rendered as a pulsing beacon
- `BannerStep` — Step subtype rendered as a top/bottom banner
- `NudgeStep` — Step subtype for subtle in-app nudges

### Audience and Segmentation Types
- `Audience` — Reusable audience definition
- `AudienceDetails` — Full audience record with conditions
- `SegmentCondition` — Condition based on a named segment
- `PropertyCondition` — Condition comparing a user or company property
- `EventCondition` — Condition based on event occurrence or count
- `PageCondition` — Condition based on current page URL or pattern
- `CompanyCondition` — Condition based on company-level properties

### Checklist Types
- `Checklist` — In-app onboarding checklist experience
- `ChecklistDetails` — Full checklist record with items and targeting
- `ChecklistItem` — Individual task within a checklist
- `ChecklistItemStatus` — Enum: INCOMPLETE, COMPLETE, SKIPPED

### Pin Types
- `Pin` — Persistent anchored tooltip or callout
- `PinDetails` — Full pin record with content and targeting
- `PinContent` — Rich content payload for a pin

### NPS and Survey Types
- `NPS` — NPS survey configuration
- `NPSSurvey` — Full NPS survey record including follow-up questions
- `NPSResponse` — Individual user response to an NPS survey

### User and Company Types
- `User` — Appcues user identity record
- `UserProfile` — Extended user properties and attributes
- `UserActivity` — User engagement and interaction history
- `Company` — Company (account) record for B2B use cases
- `CompanyDetails` — Full company record with properties and members

### Event and Property Types
- `Event` — User or company event tracked by Appcues
- `EventDetails` — Full event record with properties and metadata
- `EventProperty` — Key-value property attached to an event
- `Property` — User or company attribute definition
- `PropertyDefinition` — Metadata about a tracked property (type, source)

### Installation and SDK Types
- `Installation` — Appcues SDK installation record for an account
- `InstallationDetails` — Full installation record with configuration
- `APIKey` — API key for authenticating with the Appcues Public API
- `Token` — Short-lived authentication token
- `Webhook` — Webhook subscription for Appcues events

### Analytics Types
- `FlowAnalytics` — Aggregate analytics for a flow (views, completions, dropoff)
- `GoalConversion` — Goal conversion event tied to a flow
- `FlowView` — Individual flow view event
- `FlowComplete` — Individual flow completion event

### Content and Navigation Types
- `Experience` — Top-level wrapper for any Appcues experience type
- `ContentPage` — Paginated content listing
- `LaunchpadItem` — Item within an in-app launchpad widget

## Queries

- `flow(accountId, flowId)` — Fetch a single flow by ID
- `flows(accountId, filter, page, limit)` — List flows with filtering
- `step(accountId, flowId, stepId)` — Fetch a single step
- `audience(accountId, audienceId)` — Fetch a single audience
- `audiences(accountId)` — List all audiences
- `checklist(accountId, checklistId)` — Fetch a checklist
- `checklists(accountId)` — List all checklists
- `pin(accountId, pinId)` — Fetch a pin
- `pins(accountId)` — List all pins
- `nps(accountId, npsId)` — Fetch an NPS survey
- `user(accountId, userId)` — Fetch a user profile
- `users(accountId, filter, page, limit)` — List users
- `company(accountId, companyId)` — Fetch a company
- `companies(accountId, filter)` — List companies
- `event(accountId, eventId)` — Fetch an event definition
- `events(accountId)` — List tracked events
- `flowAnalytics(accountId, flowId, dateRange)` — Fetch flow analytics
- `installation(accountId)` — Fetch installation details
- `webhooks(accountId)` — List webhook subscriptions

## Mutations

- `createFlow(accountId, input)` — Create a new flow
- `updateFlow(accountId, flowId, input)` — Update flow content or settings
- `publishFlow(accountId, flowId)` — Publish a draft flow
- `pauseFlow(accountId, flowId)` — Pause a live flow
- `archiveFlow(accountId, flowId)` — Archive a flow
- `createAudience(accountId, input)` — Create a reusable audience
- `updateAudience(accountId, audienceId, input)` — Update audience conditions
- `createChecklist(accountId, input)` — Create a checklist
- `updateChecklist(accountId, checklistId, input)` — Update a checklist
- `createPin(accountId, input)` — Create a pin
- `updatePin(accountId, pinId, input)` — Update a pin
- `identifyUser(accountId, userId, properties)` — Upsert a user with properties
- `trackEvent(accountId, userId, eventName, properties)` — Track a custom event
- `identifyCompany(accountId, companyId, properties)` — Upsert a company
- `createWebhook(accountId, input)` — Register a webhook
- `deleteWebhook(accountId, webhookId)` — Remove a webhook
- `rotateAPIKey(accountId, keyId)` — Rotate an API key
