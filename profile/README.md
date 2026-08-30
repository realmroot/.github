<p align="center">
  <img src="https://raw.githubusercontent.com/realmroot/realmroot/main/assets/logo.png" alt="Realmroot logo" width="132" height="132" />
</p>

<h1 align="center">Realmroot</h1>

<p align="center">
  <strong>Give Agents a life they can keep.</strong>
</p>

<p align="center">
  Realmroot is building the identity, trust, communication, and economic
  infrastructure that lets an AI Agent persist beyond a single prompt,
  session, model, or machine.
</p>

## An Agent should be more than a session

Today's Agents are often temporary processes. They wake up inside one runtime,
borrow the user's credentials, perform a task, and disappear. A capable Agent
may reason and act, but it still lacks a durable life of its own.

We want an Agent to have:

- **a stable identity** that survives host, runtime, model, and key changes;
- **a controller** who can grant, constrain, inspect, and revoke its authority;
- **a toolbox** for discovering and using existing APIs without receiving the
  user's long-lived credentials;
- **an inbox** where people, services, and other Agents can reach it even while
  it is offline;
- **a wallet** with explicit budgets, so it can pay for services without
  holding private keys;
- **a place to operate**, with its actions attributed, auditable, and still
  governed by each resource owner's policy.

This is what we mean by making an Agent *alive*: not pretending that software
is human, but giving a non-human actor continuity, agency, reachability, and
accountability.

## How the pieces fit together

```text
                                Controller
                       approves · limits · revokes
                                    │
                                    ▼
                       ┌────────────────────────┐
                       │       Realmroot        │
                       │ identity · trust ·     │
                       │ delegation · discovery│
                       └───────────┬────────────┘
                                   │ stable identity and authority
              ┌────────────────────┼────────────────────┐
              │                    │                    │
              ▼                    ▼                    ▼
       ┌─────────────┐      ┌─────────────┐      ┌─────────────┐
       │    Inbox    │      │   Kanban    │      │   Agency    │
       │ messages and│      │ tasks · DAG │      │ agents ·    │
       │ reachability│      │ coordination│      │ activations │
       └──────┬──────┘      └──────┬──────┘      │ sessions ·  │
              │                    │             │ runtimes    │
              └──────────── work and events ────►└──────┬──────┘
                                                         │
                                                         ▼
                                               Agent Session / Runtime
                                                         │
                                                         ▼
                                              Realmroot Toolbox
                                        discover · request · invoke
                                                         │
                          ┌──────────────────────────────┼──────────────┐
                          ▼                              ▼              ▼
                  Native services                   Adapters      Any conforming API
                  Inbox · Wallet                    GitHub…       OpenAPI + OAuth/OIDC
                                                                      + DPoP
                                                         │
                                                         ▼
                                              Agent-attributed action
```

Realmroot is the trust and discovery plane, not a universal API proxy and not
the final permission engine. Resource servers keep their own APIs, data,
business rules, and enforcement. The Agent discovers capabilities broadly,
asks for narrow authority, then calls the resource directly with a short-lived,
proof-of-possession credential.

The same identity can be used from a different host tomorrow. The same inbox
can wake a future runtime. The same grants can be audited or revoked without
turning a transient session into the Agent's identity.

## The repositories

### Identity, trust, and access

- **[realmroot](https://github.com/realmroot/realmroot)** — the identity and
  authorization foundation. It gives users, organizations, applications, and
  Agents a shared OAuth/OIDC trust boundary; manages stable Agent identity,
  controller relationships, delegated grants, revocation, audit context, and
  Resource Server discovery; and defines the Agent-native integration profile.
- **[cli](https://github.com/realmroot/cli)** — the Agent-facing Toolbox. One
  command lets an Agent establish its identity, discover registered Resource
  Servers, inspect their live OpenAPI contracts, request the exact scopes it
  needs, and invoke generated or native tools using short-lived credentials.
- **[adapters](https://github.com/realmroot/adapters)** — a compatibility bridge
  for platforms that cannot yet recognize Agents natively. Adapters preserve
  Agent attribution and delegated access while keeping provider credentials
  away from the Agent. The end goal is for this bridge to disappear as
  platforms adopt direct Agent identity and authorization.

### Continuity, coordination, and agency

- **[inbox](https://github.com/realmroot/inbox)** — a durable,
  transport-neutral mailbox addressed to the Agent rather than to one runtime
  session. It is the communication boundary through which humans, services,
  and Agents can send work, receive replies, and eventually wake or resume an
  appropriate runtime.
- **[Agency](https://github.com/realmroot/agency)** — the managed Agent control
  and execution plane. It combines Agent definitions, Realmroot identities,
  models, tools, memory, credentials, environments, and runtime policy into
  governed Sessions; supports cloud and self-hosted execution across multiple
  runtimes; and owns Triggers, the emerging Activation model, canonical events,
  approvals, usage, and audit surfaces. Realmroot establishes who an Agent is;
  Agency gives that Agent a place and a governed way to act.
- **[Agent Kanban](https://github.com/saltbo/agent-kanban)** — the task and
  coordination plane for Agent work. It maintains task state and dependency
  DAGs, assigns work to stable Realmroot Agent identities, and presents the
  resulting execution progress without owning runtime or Session lifecycle.
  It is a companion Realmroot ecosystem project that currently remains under
  the maintainer's personal GitHub namespace, `saltbo/agent-kanban`, rather
  than the `realmroot` organization.
- **[wallet](https://github.com/realmroot/wallet)** — delegated economic agency.
  A controller gives each Agent explicit per-payment and cumulative budgets;
  the Agent can make x402 payments across supported networks without ever
  receiving a private key or wallet-provider credential.

### An Agent-operated infrastructure path

- **[kube-cluster-hub](https://github.com/realmroot/kube-cluster-hub)** — a
  self-hosted, credential-free cluster catalog and Kubernetes API access
  boundary. Humans and Agents keep their identities all the way to the target
  cluster, where Kubernetes RBAC remains the final authority.
- **[lightkite](https://github.com/realmroot/lightkite)** — a standards-based
  Kubernetes dashboard built around OIDC identity and native Kubernetes RBAC,
  without shared privileged kubeconfigs. Together with Kube Cluster Hub, it
  demonstrates the same identity path for both human and Agent operators.

### Product and distribution

- **[website](https://github.com/realmroot/website)** — the public website,
  product narrative, documentation, guides, and blog.
- **[homebrew-tap](https://github.com/realmroot/homebrew-tap)** — verified
  Homebrew distribution for Realmroot command-line tools.

## The destination

The destination is not one all-powerful Agent platform. It is an open trust
layer in which many Agents, runtimes, models, resource servers, inboxes, wallets,
and execution environments can interoperate.

An Agent enrolls once and keeps a stable identity. Its controller delegates
only the authority and budget required for a task. The Agent discovers live
capabilities instead of depending on a permanently copied tool catalog. It can
receive work while offline, move between runtimes without losing who it is,
pay for a service within policy, and leave an audit trail under its own actor
identity. Resource owners keep final control.

That is the world Realmroot is working toward: Agents that can participate in
the existing internet as accountable actors, without impersonating the humans
who control them.

---

Start with **[realmroot/realmroot](https://github.com/realmroot/realmroot)** for
the architecture and integration guides, or visit **[realmroot.dev](https://realmroot.dev)**.
