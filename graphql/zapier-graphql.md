# Zapier GraphQL Schema

## Overview

Zapier is an integration automation platform connecting 8,000+ apps through a workflow engine built around Zaps — automated workflows that watch for triggers in one app and execute actions in others. Zapier exposes a REST-based Partner API and CLI-driven Developer Platform; it does not publish a native GraphQL endpoint.

This conceptual GraphQL schema represents the full domain model of the Zapier platform: workflow automation objects (Zap, ZapStep, Trigger, Action, Search, Filter, Formatter, Webhook), app catalog structures (App, AppVersion, AppCategory, Integration, IntegrationVersion), authentication mechanisms (OAuth2, APIKeyAuth, SessionAuth, BasicAuth, DigestAuth), field definitions (Field, FieldType, InputField, OutputField), hook infrastructure (Hook, Middleware, HookSubscribe, HookUnsubscribe, TriggerHook, PollTrigger, RestHookTrigger, InstantTrigger), account and team management (User, Account, Team, Workspace, Invite, Transfer), operational data (ZapHistory, ZapRun, RunResult, Error, ThrottleConfig, Quota, Usage), and commercial constructs (Billing, Plan, AppDirectory).

## Source

Schema derived from:

- Zapier Platform documentation: https://platform.zapier.com/reference
- Zapier Platform SDK schema: https://zapier.github.io/zapier-platform-schema/build/schema.html
- Zapier Partner API OpenAPI: https://api.zapier.com/schema
- GitHub: https://github.com/zapier/zapier-platform

## Types

### Workflow Objects

| Type | Description |
|---|---|
| Zap | A complete automated workflow connecting a trigger to one or more actions |
| ZapStep | An individual step within a Zap (trigger, action, filter, path, etc.) |
| Trigger | A step that watches for events in a connected app |
| Action | A step that performs an operation in a connected app |
| Search | A step that looks up existing data in a connected app |
| Filter | A conditional step that halts a Zap run when criteria are not met |
| Formatter | A built-in Zapier step that transforms text, dates, or numbers |
| Webhook | A URL-based event notification endpoint used by REST Hook triggers |

### App Catalog

| Type | Description |
|---|---|
| App | A Zapier-connected application available in the app directory |
| AppVersion | A versioned release of an App integration |
| AppCategory | A classification grouping similar Apps |
| Integration | A developer-built Zapier integration definition |
| IntegrationVersion | A versioned snapshot of an Integration |
| AppDirectory | A paginated listing of available Apps for embedding in partner products |

### Authentication

| Type | Description |
|---|---|
| Credential | Stored authentication credentials linking a user to an App |
| Authentication | Abstract base for all authentication schemes |
| OAuth2 | OAuth 2.0 authorization code flow authentication |
| APIKeyAuth | Simple API key authentication |
| SessionAuth | Session token-based authentication |
| BasicAuth | HTTP Basic username/password authentication |
| DigestAuth | HTTP Digest authentication |

### Fields

| Type | Description |
|---|---|
| Field | Abstract field definition used in triggers, actions, and searches |
| FieldType | Enumeration of allowed field data types |
| InputField | A field capturing user-provided configuration for a step |
| OutputField | A field describing data returned by a step for use downstream |
| Line | A key-value pair rendered as a line item in Zapier's UI |

### Hook Infrastructure

| Type | Description |
|---|---|
| Hook | A lifecycle callback invoked at specific points during Zap execution |
| Middleware | Request/response transformers applied to API calls in an integration |
| HookSubscribe | A REST Hook subscription registration payload |
| HookUnsubscribe | A REST Hook subscription removal payload |
| TriggerHook | A hook type bound to trigger events |
| PollTrigger | A trigger polling an API endpoint on an interval |
| RestHookTrigger | A trigger receiving real-time payloads via webhook subscription |
| InstantTrigger | An alias for RestHookTrigger emphasizing real-time delivery |

### Account and Team

| Type | Description |
|---|---|
| User | An authenticated Zapier user |
| Account | A Zapier account, which may contain multiple users |
| Team | A group of users within an Account with shared Zap access |
| Workspace | An organizational container scoping Zaps, credentials, and members |
| Invite | A pending invitation for a user to join a Team or Workspace |
| Transfer | A transfer of Zap ownership between users or teams |

### Operational Data

| Type | Description |
|---|---|
| ZapHistory | A paginated log of Zap activity for a given Zap |
| ZapRun | A single execution instance of a Zap |
| RunResult | The output produced by a ZapStep during a ZapRun |
| Error | A structured error record from a failed ZapRun or ZapStep |
| ThrottleConfig | Rate limiting configuration applied to an integration's API calls |
| Quota | Task or API call limits attached to a Plan |
| Usage | Aggregated task consumption metrics for an Account |

### Commercial

| Type | Description |
|---|---|
| Billing | Payment and subscription information for an Account |
| Plan | A Zapier subscription tier defining feature access and quotas |

## Queries

- `zap(id: ID!)` — fetch a single Zap by ID
- `zaps(workspaceId: ID, status: ZapStatus, first: Int, after: String)` — paginated Zap listing
- `zapRuns(zapId: ID!, first: Int, after: String)` — execution history for a Zap
- `app(id: ID!)` — fetch an App from the directory
- `apps(categoryId: ID, search: String, first: Int, after: String)` — search the App directory
- `integration(id: ID!)` — fetch an Integration by ID
- `me` — current authenticated User
- `account(id: ID!)` — fetch an Account
- `team(id: ID!)` — fetch a Team
- `workspace(id: ID!)` — fetch a Workspace
- `usage(accountId: ID!, period: String)` — task usage for a billing period
- `plan(id: ID!)` — fetch a Plan

## Mutations

- `createZap(input: CreateZapInput!)` — create a new Zap
- `updateZap(id: ID!, input: UpdateZapInput!)` — update Zap configuration
- `enableZap(id: ID!)` — turn a Zap on
- `disableZap(id: ID!)` — turn a Zap off
- `deleteZap(id: ID!)` — permanently remove a Zap
- `createCredential(input: CreateCredentialInput!)` — store new authentication credentials
- `deleteCredential(id: ID!)` — remove stored credentials
- `inviteUser(input: InviteInput!)` — invite a user to a Team or Workspace
- `transferZap(input: TransferInput!)` — transfer Zap ownership
- `subscribeHook(input: HookSubscribeInput!)` — register a REST Hook subscription
- `unsubscribeHook(input: HookUnsubscribeInput!)` — remove a REST Hook subscription

## Subscriptions

- `zapRunStarted(zapId: ID!)` — fires when a Zap run begins
- `zapRunCompleted(zapId: ID!)` — fires when a Zap run finishes
- `zapRunErrored(zapId: ID!)` — fires when a Zap run encounters an error

## Schema File

See `zapier-schema.graphql` in this directory for the full type definitions.
