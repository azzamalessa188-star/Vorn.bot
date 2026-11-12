# Vorn.bot

> **A persistent cloud workspace for autonomous AI bots.**

Vorn.bot is a cloud-based workspace where users create and manage personalized AI bots, give them tasks, and observe their work through a persistent remote environment. Each bot has its own identity, avatar, conversation, and execution context, while the user retains the ability to inspect the environment and take control whenever needed.

---

## Project at a Glance

| Item | Description |
|---|---|
| Product | Vorn.bot |
| Category | Cloud workspace for AI bots |
| Primary audience | Individual developers, makers, and independent users |
| Runtime environment | Persistent Linux cloud environment |
| AI integration | Direct OpenAI Platform integration |
| Interface foundation | [fortun8te/hydo](https://github.com/fortun8te/hydo) |
| Visual identity | Teal bot mark and Vorn.bot wordmark |
| Themes | Dark mode and light mode |
| Subscription plans | Starter (BYOK) and Pro (Hosted AI) |

## Contents

- [What is Vorn.bot?](#what-is-vornbot)
- [Product Principles](#product-principles)
- [Core Capabilities](#core-capabilities)
- [User Interface](#user-interface)
- [Bot Identity and Avatar System](#bot-identity-and-avatar-system)
- [How Vorn.bot Works](#how-vornbot-works)
- [Cloud Workspace](#cloud-workspace)
- [AI Integration](#ai-integration)
- [Subscriptions and Pricing](#subscriptions-and-pricing)
- [Technical Architecture](#technical-architecture)
- [Security and Isolation](#security-and-isolation)
- [Product Requirements](#product-requirements)
- [Development Roadmap](#development-roadmap)
- [Project Status and Documentation Policy](#project-status-and-documentation-policy)

---

## What is Vorn.bot?

Vorn.bot is a platform for creating and operating AI bots inside persistent cloud workspaces.

Rather than treating an AI bot as only a chat window, Vorn.bot gives it access to a dedicated working environment. Depending on permissions and available integrations, a bot can interact with a browser, execute terminal commands, work with files, and carry out multi-step tasks.

The user can follow the bot's activity, communicate with it, inspect its workspace, and interrupt execution to take manual control.

Vorn.bot combines four central concepts:

1. **Bot identity:** Each bot has a name, description, avatar, color, and conversation.
2. **AI interaction:** Users communicate with bots and delegate tasks.
3. **Cloud execution:** Tasks run in a persistent Linux environment rather than depending on the user's computer staying online.
4. **Human supervision:** Users can observe activity and take control when necessary.

## Product Principles

### Simple by design

The primary experience should remain focused: a bot list, a conversation area, and clear access to the bot's working environment. Advanced infrastructure should not overwhelm the interface.

### Persistent cloud execution

The cloud workspace should preserve its files and relevant session state across reconnects and user sessions. Runtime persistence, process supervision, and recovery must be implemented deliberately; a persistent disk alone does not guarantee that every process survives a restart.

### Human control

Automation must not remove user oversight. Users should be able to pause or stop work, inspect actions, and take control of the remote environment.

### User choice for AI providers

The Starter plan uses the user's own API credentials (BYOK). The Pro plan includes hosted AI access under explicit usage and cost limits.

### Honest product behavior

The interface and documentation must distinguish between completed functionality, partially implemented functionality, and planned capabilities. A UI control must not imply that an operation succeeded before the backend confirms it.

---

## Core Capabilities

### 1. Bot Management

- Create multiple bots.
- Give each bot a custom name.
- Add a short description defining its role or purpose.
- Select an avatar shape, color, and visual identity.
- Generate a random avatar configuration.
- Browse the available avatar collection.
- Open an individual bot's conversation.
- Edit bot details and appearance.
- Delete a bot with an explicit confirmation step.

### 2. Conversational Workspace

- Dedicated conversation for each bot.
- Message composition and submission.
- Streaming responses where supported by the selected AI integration.
- Clear message status and execution status.
- Task progress and tool activity presented separately from ordinary chat text.
- Error reporting with actionable details.
- Conversation history associated with the relevant bot.

### 3. Autonomous Task Execution

A bot may plan and execute multi-step tasks using the tools made available to it. Depending on configuration, these may include:

- Browser interaction.
- Terminal command execution.
- File creation, reading, and editing.
- Installing project dependencies.
- Running development servers and scripts.
- Inspecting command output and application errors.
- Returning task results to the conversation.

Tool availability must be permission-controlled. The AI model must not be treated as having access to a capability unless that capability is actually connected and authorized.

### 4. Live Cloud Environment

- Remote browser access.
- Linux terminal.
- Cloud file storage.
- Live view of the remote desktop when a graphical session is enabled.
- Human takeover and return-to-agent controls.
- Reconnection to an existing workspace.

### 5. Bot Activity States

The avatar and status presentation should reflect the bot's actual execution state. The intended state vocabulary includes:

| State | Meaning |
|---|---|
| Idle | Waiting for a task or user message |
| Thinking | Processing information or deciding what to do |
| Planning | Preparing an execution plan |
| Working | Performing an active task |
| Running | Executing a process or command |
| Browsing | Interacting with a browser |
| Waiting | Waiting for an external result or user input |
| Needs Attention | Blocked or requires user intervention |
| Paused | Execution has been paused |
| Completed | The current task has completed |
| Error | An operation failed |

These are product-level states. The backend must define the exact state transitions and report them to the interface; animations must not independently determine execution status.

---

## User Interface

### Interface Foundation

The project adopts [fortun8te/hydo](https://github.com/fortun8te/hydo) as the reference and starting foundation for its interface.

The goal is to preserve the simple bot-oriented interaction model while adapting the product to Vorn.bot's branding, cloud workspace, subscription system, and technical requirements.

This is an adoption of the interface foundation, not a claim that every capability of Vorn.bot already exists in the upstream project. Before integrating or distributing code, review the upstream repository's license, dependencies, architecture, and attribution requirements.

### Main Layout

The primary workspace consists of two main areas:

#### A. Fixed Sidebar

The sidebar provides navigation between bots and access to the main workspace controls.

It contains:

- Vorn.bot logo and brand identity.
- A button to create a new bot.
- A list of the user's bots.
- Each bot's avatar and name.
- A visual indication of the selected bot.
- Activity indicators based on the bot's actual state.
- Access to account and settings controls.
- Theme switching between dark and light modes.

The sidebar should remain fixed while the main conversation area changes. On smaller screens, it may collapse into a navigation drawer without changing the underlying navigation model.

#### B. Main Conversation Area

The main area displays the selected bot's conversation and activity.

It contains:

- Selected bot identity.
- Conversation history.
- User messages and bot responses.
- Streaming response presentation.
- Task and tool activity indicators.
- Error and attention notifications.
- Message input field.
- Send and stop controls.
- Access to the bot's cloud environment.

Code and execution output should be presented in appropriate structured panels rather than being indiscriminately mixed into ordinary conversational text.

### Create Bot Window

Selecting the new-bot button opens a centered creation window.

The window contains:

1. **Avatar preview:** A live preview of the selected bot.
2. **Bot name:** A text field for the bot's name.
3. **Short description:** A concise description of the bot's role.
4. **Avatar shapes:** A gallery of available avatar shapes.
5. **Avatar colors:** A palette of supported colors.
6. **Randomize:** Generates a random combination of supported avatar properties.
7. **Avatar gallery:** Allows the user to browse all available avatar configurations.
8. **Animation preview:** Allows the user to preview available avatar animations.
9. **Create button:** Creates the bot after validating the required fields.
10. **Cancel button:** Closes the window without creating a bot.

The creation process should validate the name, preserve the selected avatar configuration, and show a clear error if creation fails.

### Interaction Rules

| Control | Expected behavior |
|---|---|
| New Bot (+) | Opens the bot creation window |
| Bot item | Selects that bot and loads its conversation |
| Avatar selector | Changes the preview and selected avatar |
| Color selector | Applies the selected color |
| Randomize | Generates a valid random avatar configuration |
| Name field | Updates the bot name value |
| Description field | Updates the bot description value |
| Create | Submits bot creation and closes the window only after success |
| Cancel | Closes the creation window without saving |
| Message input | Accepts the user's message |
| Send | Submits the message to the selected bot |
| Stop | Requests cancellation of the active operation |
| Take Control | Transfers interaction to the user when the remote environment is available |
| Resume Agent | Returns control to the agent after the user relinquishes manual control |
| Theme switch | Changes the interface theme |
| Settings | Opens account and application settings |

All controls must have loading, disabled, success, and error behavior appropriate to their operation. Destructive actions require confirmation.

---

## Bot Identity and Avatar System

### Visual Identity

Vorn.bot uses a custom bot character as a central part of its brand identity.

The approved wordmark combines the bot character with the word Vorn and the `.bot` suffix. The bot mark uses the Teal accent:

- **Primary Teal:** `#38C6AA`
- **Brand name:** `Vorn.bot`
- **Theme variants:** Light and dark logo assets.

The supplied logo artwork is the visual source of truth. The implementation should use the actual approved assets rather than approximating the mark with an unrelated icon or font glyph.

### Avatar Customization

Each bot should have a persistent avatar configuration containing:

- Shape identifier.
- Color identifier.
- Expression or eye configuration, where supported.
- Animation state, derived from runtime status.

The avatar gallery should expose all configurations supported by the adopted avatar implementation. The product must not advertise a fixed number of shapes, colors, expressions, or animations until the integrated source has been inspected and verified.

### Animation Behavior

Animations communicate activity and personality:

- **Idle:** Gentle breathing or subtle movement.
- **Thinking:** Focused eye movement or a restrained thinking animation.
- **Planning:** A distinct planning animation.
- **Working:** Active movement indicating execution.
- **Browsing:** A state suitable for browser activity.
- **Needs Attention:** A noticeable but restrained attention animation.
- **Completed:** A brief completion animation.
- **Error:** A clear error expression or status treatment.

Animation should be lightweight and suitable for a sidebar containing multiple bots. Prefer vector-based rendering and efficient transitions. Respect reduced-motion preferences and avoid unnecessary continuous animation when a bot is not visible.

### Technical Reference

The project may use the avatar and animation implementation available through the adopted Hydo codebase or another compatible, reviewed implementation. The exact source files, APIs, license, and available states must be verified during integration.

---

## How Vorn.bot Works

### 1. Account and Subscription

A user creates an account, selects a subscription plan, and enters the application.

The backend verifies the subscription and provisions the workspace resources associated with that plan.

### 2. Bot Creation

The user opens the creation window, enters a name and description, selects or randomizes an avatar, and creates the bot.

The backend stores the bot configuration and associates it with the authenticated user.

### 3. Task Submission

The user selects a bot, enters a message, and submits it.

The backend:

1. Authenticates the user.
2. Verifies subscription status and usage limits.
3. Loads the bot's configuration and conversation context.
4. Resolves the configured AI provider.
5. Sends the request to the AI integration.
6. Receives the response and any requested tool calls.
7. Validates tool permissions.
8. Executes authorized operations in the bot's cloud workspace.
9. Returns progress and results to the interface.
10. Persists the conversation and relevant task state.

### 4. Tool Execution

When the model requests a tool, the orchestration layer validates the request before execution.

For example, a browser task may require the browser service, while a command-line task requires the terminal execution service.

The system records the operation, its status, and its result. Failed operations should return structured diagnostics rather than silently disappearing.

### 5. Human Intervention

When a user chooses to take control, the system must safely coordinate access to the remote environment.

The agent should pause or relinquish conflicting actions before manual control is granted. When the user resumes the agent, the orchestration layer should restore the appropriate execution state and provide the agent with updated context.

### 6. Completion and Persistence

The bot reports the result, updates the task status, and preserves relevant workspace data.

Users should be able to reconnect and continue working without losing persistent files or conversation history.

---

## Cloud Workspace

Each user receives cloud workspace resources according to the active subscription.

### Intended Environment

- Linux-based environment, using Debian as the target base.
- Browser access through Google Chrome.
- Terminal access.
- Persistent file storage.
- Remote graphical desktop when required.
- A controlled execution interface for agent tools.

### Resource Allocation

Both subscription plans use the following target allocation:

| Resource | Allocation |
|---|---:|
| CPU | 1 vCPU |
| Memory | 2 GB RAM |
| Storage | 40 GB |

These are product allocation targets. Actual infrastructure limits, storage quotas, and availability must be enforced by the provisioning layer.

### Remote Desktop and Streaming

The remote desktop should be accessible through a secure browser-based streaming mechanism.

The architecture may use a remote desktop server with noVNC and WebSockets, or a suitable WebRTC-based implementation where required by latency and deployment constraints.

The final transport must be selected and tested against the actual hosting environment. The interface should not expose a fake live view or report a connection as active until the streaming service confirms it.

### Persistence and Lifecycle

The platform should separate:

- Persistent user files.
- Bot configuration and conversation data.
- Runtime processes.
- Temporary execution artifacts.
- Remote desktop session state.

The system must define behavior for workspace shutdown, restart, disconnection, subscription expiration, and resource recovery.

---

## AI Integration

### Provider

The Hosted AI plan is intended to use a direct integration with **OpenAI Platform**.

The integration must use the supported OpenAI API and authentication mechanism for the selected model. Model identifiers and API capabilities must be verified against the actual OpenAI Platform account and current API documentation before deployment.

The platform must not route this integration through OpenRouter.

### BYOK

The Starter plan allows users to supply their own supported API credentials.

Credentials must be stored securely and never exposed in browser code, client-side logs, or ordinary application responses.

### Hosted AI

The Pro plan includes platform-managed AI usage subject to the monthly allowance, daily limit, and financial cost caps described below.

### AI Request Lifecycle

- Resolve the selected provider and model.
- Retrieve credentials securely on the server.
- Validate the user's plan and remaining allowance.
- Apply rate and cost controls.
- Submit the request.
- Process streaming output and tool calls when supported.
- Validate and execute authorized tools.
- Record usage and cost information.
- Return the result and updated usage state.

### Usage Accounting

Usage accounting must be server-side and auditable.

The system should track:

- User and subscription.
- Request identifier.
- Provider and model identifier.
- Input and output usage where available.
- Total billable usage.
- Estimated and reconciled provider cost.
- Request timestamp.
- Daily and monthly usage totals.
- Whether a request was rejected by a limit.

Do not rely exclusively on client-reported token counts or client-side cost calculations.

---

## Subscriptions and Pricing

Vorn.bot has exactly two individual subscription plans.

There is no Enterprise plan, team/company subscription tier, or agent skills marketplace in this product specification.

### Starter — BYOK

**Price: $9.99 per month**

For developers and independent users who bring their own AI API credentials.

Included:

- Persistent cloud workspace.
- 1 vCPU.
- 2 GB RAM.
- 40 GB storage.
- Google Chrome access.
- Linux terminal.
- Cloud file storage.
- Remote desktop access where enabled.
- Human takeover and agent resume controls.
- Bot creation and customization.
- User-provided AI API credentials.

The user pays their AI provider directly for API usage. Vorn.bot's subscription does not include a hosted AI token allowance.

### Pro — Hosted AI

**Price: $19.99 per month**

For users who want an integrated AI experience without configuring their own provider credentials for normal usage.

Included:

- All Starter workspace capabilities.
- 1 vCPU.
- 2 GB RAM.
- 40 GB storage.
- Hosted AI integration through OpenAI Platform.
- 30,000,000 tokens per subscription month.
- Daily usage limit of 1,000,000 tokens.
- Daily financial cost cap of $0.17.
- Monthly financial cost cap of $5.00.
- Option to enter a temporary BYOK key when the hosted allowance or cost limit is reached.

The hosted AI allowance is subject to all applicable usage and financial limits. The first applicable limit reached governs whether additional hosted requests are accepted.

### Pricing Comparison

| Feature | Starter — BYOK | Pro — Hosted AI |
|---|---:|---:|
| Monthly price | $9.99 | $19.99 |
| Automatic monthly renewal | $9.99 | $19.99 |
| Cloud workspace | Included | Included |
| CPU | 1 vCPU | 1 vCPU |
| RAM | 2 GB | 2 GB |
| Storage | 40 GB | 40 GB |
| Browser and terminal | Included | Included |
| Persistent file storage | Included | Included |
| Human takeover | Included | Included |
| AI provider | User's own key | OpenAI Platform |
| Monthly hosted token allowance | Not included | 30,000,000 |
| Daily token limit | Provider-dependent | 1,000,000 |
| Daily hosted AI cost cap | Not applicable | $0.17 |
| Monthly hosted AI cost cap | Not applicable | $5.00 |
| Temporary BYOK fallback | User's own key | Available |

### Renewal and Limit Behavior

- Both plans renew monthly at their listed prices unless cancelled.
- The Pro token allowance resets with the subscription billing cycle.
- Daily limits reset according to a clearly defined server-side billing timezone.
- The daily and monthly financial caps must be enforced server-side.
- When a hosted AI limit is reached, further hosted requests are rejected until the applicable limit resets or the billing cycle changes.
- A Pro user may configure a temporary BYOK key as an alternative.
- BYOK requests must be accounted for separately from hosted AI usage.
- Workspace access, data retention, and cancellation behavior must be defined in the billing lifecycle.

### Financial Safeguards

The Pro plan must enforce both daily and monthly cost limits.

The effective hosted AI spending allowance is the lowest remaining applicable limit. The system should reserve estimated cost before or during execution, reconcile actual provider usage afterward, and prevent concurrent requests from overspending the configured caps.

The $0.17 daily and $5.00 monthly limits are product-level limits, not a guarantee that every possible request can complete within a fixed token allowance. Actual cost depends on the provider's pricing and the selected model.

---

## Technical Architecture

The following is the intended logical architecture. It describes the target system and does not assert that every component is already implemented in the repository.

### Main Components

| Component | Responsibility |
|---|---|
| Web Frontend | Bot list, conversations, avatar customization, themes, and workspace controls |
| Authentication | User identity and session management |
| API Backend | Application APIs, authorization, and request validation |
| Bot Service | Bot profiles, settings, and lifecycle |
| Conversation Service | Message history and conversation state |
| Agent Orchestrator | Planning, model requests, tool routing, and execution coordination |
| AI Provider Adapter | OpenAI Platform and BYOK provider integration |
| Tool Execution Layer | Controlled browser, terminal, and file operations |
| Workspace Manager | Provisioning and lifecycle management for cloud workspaces |
| Remote Desktop Service | Secure remote graphical access and streaming |
| Storage Layer | Persistent files and application data |
| Billing and Usage Service | Subscriptions, renewals, quotas, and cost enforcement |
| Observability | Logs, metrics, tracing, and operational alerts |

### Logical Request Flow

```text
User
 |
 v
Vorn.bot Web Interface
 |
 v
Application API
 |
 +------ Authentication and Authorization
 |
 +------ Subscription and Usage Validation
 |
 v
Bot and Conversation Services
 |
 v
Agent Orchestrator
 |
 +------ OpenAI Platform / BYOK
 |
 +------ Browser Tools
 |
 +------ Terminal Tools
 |
 +------ File Tools
 |
 v
Cloud Workspace
 |
 +------ Linux Environment
 +------ Chrome
 +------ Terminal
 +------ Persistent Storage
 +------ Remote Desktop
 |
 v
Task Results and Activity Events
 |
 v
Vorn.bot Web Interface
```

### Data Model

The backend should support entities equivalent to:

- **Users:** Account identity and authentication metadata.
- **Subscriptions:** Plan, billing status, renewal period, and provider references.
- **Bots:** Owner, name, description, avatar configuration, and settings.
- **Conversations:** Bot association and conversation metadata.
- **Messages:** Role, content, timestamps, and relevant tool-call references.
- **Tasks:** Execution state, progress, and result metadata.
- **Workspaces:** Environment allocation, lifecycle, and storage association.
- **Credentials:** Encrypted provider credentials and access metadata.
- **Usage Records:** Provider usage, token counts, and cost accounting.
- **Audit Events:** Security-sensitive actions and administrative events.

These are logical data entities; the final database schema and relationships must be established during implementation.

### Realtime Events

The frontend should receive server-authoritative events for:

- New messages.
- Streaming response chunks.
- Bot state changes.
- Task progress.
- Tool execution start and completion.
- Workspace connection state.
- Human takeover and resume.
- Usage limit notifications.
- Errors and attention requests.

WebSockets or another suitable realtime transport may be used. Reconnection must recover the latest authoritative state rather than assuming no events were missed.

---

## Security and Isolation

Cloud execution requires strict security boundaries.

### Workspace Isolation

- Each user's workspace must be isolated from other users' workspaces.
- Container or VM boundaries must be enforced by infrastructure, not only by application conventions.
- Workspace processes must not receive unrestricted host access.
- Resource limits must be applied to CPU, memory, storage, and process usage.
- Network access should be restricted according to the platform's security policy.
- Workspace lifecycle operations must be authenticated and authorized.

### Credential Protection

- Store provider credentials encrypted at rest.
- Keep secret decryption and provider calls on the server.
- Never place API keys in frontend bundles.
- Avoid logging secrets, authorization headers, or raw credential values.
- Provide a way to replace or revoke credentials.
- Restrict credential access to the services that need it.

### Tool Permissions

- Validate tool calls on the server.
- Apply per-user and per-workspace authorization.
- Use explicit policies for sensitive operations.
- Record important actions in audit logs.
- Require confirmation for operations designated as destructive or high impact.
- Provide a reliable stop mechanism for active work.

### Billing Protection

- Enforce subscription state and usage limits on the backend.
- Make cost reservations safe under concurrent requests.
- Reconcile provider usage against recorded estimates.
- Reject requests when the applicable limit has been reached.
- Keep BYOK usage separate from platform-funded hosted usage.

### Operational Security

- Use HTTPS for all public application traffic.
- Protect remote desktop sessions with authenticated, short-lived access.
- Apply rate limits to authentication and application endpoints.
- Maintain backups and define restoration procedures.
- Monitor unusual resource consumption and repeated failures.

---

## Product Requirements

The following requirements define expected product behavior.

### Reliability

- A failed AI request must not corrupt conversation history.
- A disconnected browser must not automatically destroy persistent user files.
- Reconnecting must restore the latest available workspace and task state.
- A stopped task must not continue indefinitely in the background.
- A workspace restart must have a defined recovery procedure.

### Accessibility and Interface Quality

- Support dark and light themes.
- Use the approved Vorn.bot brand assets in both themes.
- Keep keyboard navigation and focus behavior usable.
- Provide readable status indicators that do not depend on color alone.
- Respect reduced-motion preferences.
- Keep avatar animations efficient when many bots are listed.

### Product Scope Constraints

The product specification intentionally excludes:

- Enterprise or company subscription plans.
- Team-based subscription tiers.
- An agent skills marketplace.
- Arbitrary feature branding that prefixes every feature name with Vorn.bot.

Feature labels should remain direct and functional, such as **Stream**, **Terminal**, and **Storage**.

---

## Development Roadmap

The roadmap below is a suggested implementation sequence, not a claim of completed work.

### Phase 1 — Repository and Foundation

- Inspect the selected Hydo source and its license.
- Establish the Vorn.bot repository structure.
- Integrate the approved light and dark brand assets.
- Adapt the base interface to Vorn.bot.
- Implement authentication and account boundaries.

### Phase 2 — Bot Experience

- Implement bot creation and editing.
- Implement avatar selection and randomization.
- Integrate supported avatar animations.
- Implement bot list and conversation navigation.
- Persist bot profiles and conversation history.

### Phase 3 — AI and Orchestration

- Integrate OpenAI Platform.
- Implement BYOK credential management.
- Implement conversation streaming.
- Implement the agent orchestration layer.
- Add permission-checked tool execution.
- Implement authoritative bot and task states.

### Phase 4 — Cloud Workspace

- Provision isolated Linux workspaces.
- Integrate Chrome and terminal access.
- Implement persistent storage.
- Add remote desktop streaming.
- Implement human takeover and agent resume.
- Add workspace recovery and lifecycle controls.

### Phase 5 — Billing and Limits

- Implement Starter and Pro subscriptions.
- Integrate subscription renewal and cancellation.
- Implement token usage accounting.
- Enforce daily and monthly financial limits.
- Add temporary BYOK fallback for Pro.
- Test concurrency and cost-limit enforcement.

### Phase 6 — Hardening and Release

- Run security and isolation tests.
- Test workspace lifecycle and recovery.
- Test AI failures and provider limits.
- Test light and dark themes.
- Test responsive behavior and accessibility.
- Add monitoring, backups, and operational alerts.
- Publish deployment and user documentation.

---

## Project Status and Documentation Policy

This repository's README is the central product and architecture reference. It describes the approved product direction and target behavior.

**A documented requirement is not automatically an implemented feature.** Implementation status must be verified against source code, tests, and deployed behavior.

When reporting progress, classify functionality as:

- **Implemented and verified**
- **Implemented, not yet fully verified**
- **Partially implemented**
- **Planned**
- **Blocked**
- **Unknown**

Do not claim that a workspace is persistent, isolated, live-streaming, or production-ready without corresponding implementation and verification evidence.

Keep pricing, brand identity, provider integration, and product scope consistent across future documentation and implementation.

---

## Brand and Reference Links

- **Project repository:** https://github.com/azzamalessa188-star/Vorn.bot
- **Interface foundation:** https://github.com/fortun8te/hydo
- **OpenAI Platform:** https://platform.openai.com/
- **OpenAI API documentation:** https://platform.openai.com/docs

---

## License

The license for Vorn.bot must be explicitly selected and added to the repository before the project is distributed.

The license of the adopted Hydo codebase and any other third-party dependencies must be reviewed independently. Do not assume that the upstream project's license automatically applies to Vorn.bot or permits every intended form of reuse.

---

**Vorn.bot — Your bots. Your workspace. Always within reach.**
