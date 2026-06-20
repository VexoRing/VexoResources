# Users

There are two personas, each with a private vs. exposed mode. That gives four user types in practice. The whole taxonomy comes down to two questions:

- Consumer or developer?
- Whose data do they touch: only their own, or other people's?

## The 2x2

| | Own data only | Other people's data |
|---|---|---|
| **Consumer** | Type 1 (app-only) and Type 2 (app + own agent) | (none) |
| **Developer** | Type 3 (local self-dev) | Type 4 (marketplace) |

## The four types

1. **Wearer (local).** Stays strictly on the app. On-device only, no export. This is the default state for every user.
2. **Wearer (connected).** Same person as Type 1, after granting an MCP scope to their own AI agent (Claude, ChatGPT, Gemini, etc.). Data crosses only for the granted slice.
3. **Builder (self).** A developer building against their own ring data locally. Same SDK and MCP interface as Type 4, but only ever touches their own data.
4. **Builder (marketplace).** A developer shipping apps that other users grant scoped access to. The only persona that touches other people's data.

## Things to be deliberate about

### Types 1 and 2 are one user in two consent states

A Type 1 user becomes Type 2 the moment they grant an MCP scope, and drops back to Type 1 the moment they revoke it. This is not two account types, it is one consumer persona with a revocable consent toggle. Build one onboarding flow, not two.

### Type 3 is the on-ramp to Type 4

A marketplace developer almost always starts by building against their own data (Type 3), then publishes for everyone (Type 4). Same SDK, same MCP interface. The only thing that changes at the 3 to 4 boundary is whose data flows through their code. The product decision is how frictionless that promotion is.

### Type 4 is the only real security boundary

Types 1, 2, and 3 only ever touch the user's own data. Type 4 is the only persona that touches other people's data, and only ever through a per-user consented MCP grant. That single line is the entire security surface: per-user data isolation, scoped and revocable grants, developers never receiving data except through a permission the user gave, and only the slice it covers.

## Type 4 runtime model: data never leaves the device

For the marketplace builder, the third-party app's code runs where the data is (on the phone, inside the user's trust boundary, against a local MCP endpoint). The developer's servers never receive raw context.

Consequences:

- **The unit shipped to the marketplace is code/logic, not an API integration.** A marketplace app is pulled down and executed against the user's local context server, sandboxed, with the grant defining which tools and scopes it can call. It is not "your context gets sent to the app's backend."
- **Per-user isolation becomes almost free.** Each user runs the app against only their own data, on their own device, in a separate process. The isolation is physical, not a multi-tenant database we have to keep perfectly partitioned. What the architecture must guarantee shrinks to: a sandbox that confines a third-party app to its granted scopes on one device.
- **The output is the only thing that can leave, and only with its own grant.** Distribution (a tweet, a ticket, a changelog) is itself egress. So there are two distinct grant classes:
  - **Input scope:** what context the app may read (HR, transcripts, location, etc.).
  - **Output/action scope:** what external destination the app may write to.
  A user can grant read-without-send.
- **What we give up:** server-side cross-user features (trending across all users, developer-side analytics on raw data, heavy cloud compute the phone cannot do). Anything aggregate must be built from data users separately consented to export, or computed on-device and aggregated only in anonymized/derived form.

This is the strongest reading of the one rule (data never leaves without consent), and it is a genuine differentiator: most context platforms are cloud data brokers. This is the one where the platform never holds the data.
