# Awesome-Realtime-Messaging-Websockets

## Top Realtime Messaging & WebSockets Tools Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Bidirectional Pub/Sub, Connection Recovery & Self-Hosted WebSocket Servers*  
**Last updated: March 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **Realtime Messaging & WebSockets**. These tools push data to connected clients instantly — enabling live chat, collaborative editing, real-time dashboards, notifications, and multiplayer experiences — without polling.

**Examples** include Socket.IO, Pusher, Ably, PubNub, Supabase Realtime, Centrifugo, Soketi, Mercure, deepstream.io, and Firebase (the category leaders).

**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, Pusher-protocol compatibility, and transparent WebSocket infrastructure — ideal for developers prioritizing data sovereignty, avoiding per-message SaaS costs, and maintaining control over real-time transport.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[Pusher Channels](https://pusher.com/)**  
  **The reference hosted pub/sub service** with a massive SDK ecosystem and the Pusher protocol that many open-source tools implement. **Sandbox free tier: 200,000 messages/day, 100 concurrent connections** [citation:2]. **When limits are exceeded, new connections are blocked and server-side publishes return 403 errors** [citation:2]. Paid Startup tier at $49/month. **Best for teams wanting the least infrastructure work** and straightforward real-time transport.

- **[Ably](https://ably.com/)**  
  **The reliability-focused realtime platform** with a **99.999% uptime SLA** and seven-year history of 100% uptime. **Free plan: 6,000,000 messages/month, 200 concurrent connections, 200 concurrent channels, 500 messages/second** [citation:7][citation:16]. **No daily message cap** — the monthly framing means a heavy testing day does not zero out the week's remaining budget [citation:2]. **Consumption-based pricing** ($2.50/million messages, scaling down to $0.50 with volume) can be complex for startups [citation:2]. **Best for teams wanting the most generous free message headroom** before paying.

- **[PubNub](https://www.pubnub.com/)**  
  Multi-purpose realtime platform combining messaging, push notifications, and serverless functions. **Free account covers up to 200 monthly active users (MAUs) or 1 million transactions, whichever limit is reached first** [citation:3][citation:17]. **Free plan keysets are limited to Testing keysets** and are not suitable for live traffic [citation:3][citation:12]. **The 200 MAU cap is low for user-facing apps** — the breadth of channels (push + functions) is the free-tier advantage.

- **[Supabase Realtime](https://supabase.com/)**  
  **Globally distributed Elixir/Phoenix cluster** providing **Broadcast, Presence, and Postgres Changes** via WebSockets. **Benchmarked at 224,000 messages/second with 32,000 concurrent users** (median latency 6ms) on a 2-6 node cluster. **Free tier: 200 concurrent clients, 100 messages/second** [citation:9]. Pro tier at **$25/month** raises limits to 500 concurrent clients and 500 messages/second [citation:9]. Postgres Changes streams WAL via logical replication slots with automatic reconnection.

- **[Firebase Realtime Database](https://firebase.google.com/)**  
  Google's NoSQL realtime database with client SDKs that sync state across devices automatically. Deep integration with Firebase Authentication and Cloud Functions.

- **[AWS AppSync](https://aws.amazon.com/appsync/)**  
  Managed GraphQL service with real-time subscriptions over WebSockets, integrated with DynamoDB, Lambda, and Cognito.

## Open-Source GitHub Projects

- **[Socket.IO](https://github.com/socketio/socket.io)**  
  **The most widely used realtime application framework** — MIT licensed, **61,000+ GitHub stars** . **Not a plain WebSocket implementation** — it adds an additional protocol layer over WebSocket (and HTTP long-polling fallback) with metadata per packet [citation:1][citation:6]. **Features that plain WebSockets lack**: **HTTP long-polling fallback** for misconfigured proxies, **automatic reconnection** with exponential backoff, **packet buffering** during disconnection, **acknowledgements** for request-response patterns, **broadcasting to rooms**, and **namespaces** for multiplexing application logic over one connection [citation:1]. **Scale-out via Redis adapter** for multi-node deployments [citation:1]. **Trade-offs**: Protocol overhead adds a few bytes per message (`42["hello","world"]`); at-most-once delivery by default (fire-and-forget) unless using acknowledgements; **not meant for background mobile apps** due to battery drain from persistent TCP [citation:1][citation:6]. **Best for web applications wanting battle-tested realtime primitives** without building reconnection and room logic from scratch.

- **[Centrifugo](https://github.com/centrifugal/centrifugo)**  
  **The most feature-complete self-hosted realtime messaging server** — Apache 2.0 licensed, **10,800+ GitHub stars** . **Language-agnostic** with official SDKs for JavaScript, Swift, Java/Android, C#, Dart/Flutter, Python, and Go . **Transport flexibility**: WebSocket, HTTP-streaming, Server-Sent Events (SSE), gRPC, and WebTransport [citation:9]. **Built-in scalability** with Redis (or Redis Cluster, Valkey, KeyDB, DragonflyDB) or Nats . **Channel history with automatic recovery on reconnect**, delta compression, presence with join/leave, and **asynchronous PostgreSQL/Kafka consumers** for outbox and CDC patterns . **HTTP and gRPC server API** for backend integration, JWT or proxy authentication, and a beautiful embedded admin UI with Prometheus metrics . **Base product is free and open source**; **Centrifugo PRO** adds analytics with ClickHouse, real-time tracing, push notification API, and SSO [citation:19]. **Best for teams wanting a production-grade, self-hosted PubNub/Pusher/Ably alternative** without vendor lock-in.

- **[Soketi](https://github.com/soketi/soketi)**  
  **The Pusher-protocol-compatible self-hosted server** — AGPL-3.0 licensed, **5,600+ GitHub stars** . **Drop-in replacement for Pusher Channels** — existing Pusher SDKs and applications work without code changes [citation:14]. **Written in Node.js/TypeScript** with a Rust adapter for performance. **Supports horizontal scaling via Redis adapter**, HTTP API, and multiple apps [citation:14]. **No hosted cloud option** — self-hosting overhead is the trade-off [citation:14]. **Best for teams already using Pusher SDKs** who want to migrate to self-hosting without rewriting client code.

- **[Mercure](https://github.com/dunglas/mercure)**  
  **The standards-based SSE pub/sub hub** — AGPL-3.0 licensed, **5,000+ GitHub stars** . **Hub-based publish/subscribe protocol over HTTP and Server-Sent Events (SSE)** — designed for server-to-client real-time updates . **Spec stabilized for 1.0** with **OAuth 2.0 Rich Authorization Requests** and **WHATWG URL Pattern** . **SSE-native** — the same transport used by OpenAI, Anthropic, and MCP for token streaming — with authorization, multiplexing, discovery, and reconnection that ad-hoc SSE lacks . **First-class integration in Symfony, API Platform, Laravel, and FrankenPHP** . **Best for PHP/Symfony ecosystems** and applications where SSE is preferred over WebSockets.

- **[deepstream.io](https://github.com/deepstreamIO/deepstream.io)**  
  **The realtime server with records, events, and RPC** — MIT licensed, **7,100+ GitHub stars** . **Three core primitives**: schema-less persistent documents (records) that sync across clients, topic-based events for many-to-many messaging, and remote procedure calls with load-balancing and failover . **Valve permission language** for fine-grained authorization . **Connectors for PostgreSQL, MongoDB, Redis, and Memcached** . **Best for applications needing realtime data sync plus RPC** in one server.

### Additional Strong Open-Source Options

- **ws** — Fast and tested plain WebSocket client and server library for Node.js. Use this when you want raw WebSocket without Socket.IO's protocol layer [citation:1][citation:13].
- **µWebSockets** — High-performance WebSocket server and client library in C++ with pub/sub engine, designed for millions of connections [citation:13].
- **Centrifuge** — The Go library powering Centrifugo. Embed realtime WebSocket support directly in Go applications .
- **SocketCluster** — Highly scalable realtime pub/sub and RPC framework for Node.js [citation:13].
- **Primus** — Abstraction layer that lets you switch between realtime transport engines without rewriting application logic [citation:13].
- **Mercure.rocks Hub** — Managed high-scalability Mercure hub for teams wanting the protocol without self-hosting .

**Frameworks for building custom systems**: Combine **Socket.IO** for battle-tested web realtime with rooms, reconnection, and fallback, **Centrifugo** for a full-featured self-hosted pub/sub server with multi-transport support and Redis clustering, **Soketi** for drop-in Pusher compatibility without rewriting SDK code, **Supabase Realtime** for Postgres-native CDC and Broadcast at scale, **Mercure** for standards-based SSE where WebSockets aren't required, and **deepstream.io** for realtime records plus RPC — to build a realtime messaging layer tailored to your transport preferences, existing SDK ecosystem, and infrastructure constraints.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- Realtime messaging tools differ significantly in transport support, free-tier limits, and operational complexity. **Socket.IO is not a plain WebSocket implementation** — a WebSocket client cannot connect to a Socket.IO server and vice versa [citation:1]. **Pusher's free tier offers 200K messages/day** but blocks new connections and returns 403 on publish when the daily cap is hit [citation:2]. **Ably's free tier offers 6M messages/month with no daily cap** — the most generous headroom before paying [citation:2][citation:7]. **PubNub's free tier caps at 200 MAU**, which is restrictive for user-facing apps [citation:3]. **Centrifugo is the most feature-complete self-hosted option** with multi-transport support, Redis clustering, and CDC consumers . **Soketi is the drop-in Pusher replacement** but has no hosted cloud option [citation:14]. **Mercure's SSE approach is standards-based** and aligns with AI streaming patterns, but SSE is one-way server-to-client . **Supabase Realtime's free tier is 200 concurrent clients and 100 messages/second** — Pro at $25/month raises to 500/500 [citation:9].
- Self-hosted open-source solutions require proper Redis/Nats configuration for horizontal scaling, WebSocket-aware load balancers, and monitoring of connection counts and message throughput.

---

**Made for developers, platform engineers, and teams building real-time collaborative and live-update applications.**
Let's make realtime messaging and WebSockets more open, self-hostable, and transport-flexible.
