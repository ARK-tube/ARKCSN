# ARK Content Suggestion System

A local, open-source live-TV layer for home media servers.

Adaptive Live TV turns a personal media library into a dynamic broadcast experience. Instead of stopping playback to browse a large catalog, the system can promote relevant movies, shows, episodes, trailers, and other content from the same library while the viewer is watching.

The central idea is simple:

```text
Watch content
     ↓
Understand context
     ↓
Find relevant content
     ↓
Rank candidates
     ↓
Promote one at the right moment
     ↓
Observe interaction
     ↓
Improve future recommendations
```

## Why

A large home media library can have more content than a viewer can reasonably discover.

Traditional media servers are excellent at storing and browsing content, but discovery usually requires the viewer to leave playback and manually search through the catalog.

Adaptive Live TV treats the library more like a personalized television network.

The viewer watches.

The system handles contextual discovery.

## What Makes It Different

This is not intended to be a conventional advertising platform.

The promoted content comes from the user's own library.

For example:

```text
Currently watching:
    Blade Runner 2049

Context:
    Sci-Fi
    Thriller
    Artificial Intelligence
    Denis Villeneuve
    Dystopian

Possible promotion:
    Ex Machina

Creative:
    Trailer / poster / banner / "Coming Up Next"
```

The same mechanism can promote unfinished content, related episodes, collections, franchises, documentaries, or less obvious discoveries.

## Contextual Signals

The recommendation engine can use media metadata and playback behavior.

Content signals can include:

- Genre
- Keywords
- Cast
- Director
- Studio
- Franchise
- Collection
- Language
- Release period
- Runtime
- Semantic embeddings

Playback signals can include:

- Play
- Pause
- Resume
- Seek
- Rewind
- Fast-forward
- Skip
- Replay
- Completion
- Subtitle changes
- Audio-track changes
- Volume changes
- Mute/unmute

These signals are treated as probabilistic evidence rather than absolute interpretations.

For example, a volume increase during an intense scene may indicate attention, but volume changes can also have completely mundane causes. The system should combine signals instead of pretending one knob on a remote contains the secrets of the universe.

## Adaptive Engagement

The player can provide implicit feedback without requiring explicit ratings.

A possible future model could combine:

```text
engagement(t) =

    volume response
  + uninterrupted playback
  + rewind behavior
  + interaction patterns
  + scene context
  + completion probability
```

The exact weighting can eventually be learned from observed behavior.

This allows the recommendation system to learn not only what content is related, but how the viewer interacts with it.

## Architecture

The intended architecture separates media playback from recommendation.

```text
                 HOME SERVER

┌───────────────────────────────────────┐
│                                       │
│        Media Server / Player          │
│                 │                     │
│                 ▼                     │
│          Playback Events              │
│                 │                     │
│                 ▼                     │
│          Context Builder              │
│                 │                     │
│        ┌────────┴────────┐            │
│        │                 │            │
│     Metadata        Embeddings        │
│        │                 │            │
│        └────────┬────────┘            │
│                 ▼                     │
│       Candidate Retrieval             │
│                 │                     │
│                 ▼                     │
│          Ranking Engine               │
│                 │                     │
│                 ▼                     │
│        Promotion Engine               │
│                 │                     │
│                 ▼                     │
│          Player / UI                  │
│                                       │
└───────────────────────────────────────┘
```

The recommendation system should remain independent from any particular media server wherever practical.

## Local First

The project is intended to work entirely on the home server.

The default architecture should not require:

- Cloud recommendation services
- External advertising networks
- Third-party behavioral tracking
- Centralized user profiles
- Google advertising infrastructure

Media metadata, playback telemetry, recommendation state, and learned user preferences can remain local.

## Recommendation Pipeline

The system can eventually use a two-stage recommendation pipeline.

### Candidate Retrieval

Retrieve a relatively small set of potentially relevant content using:

- Metadata relationships
- Content similarity
- Embeddings
- User history
- Unfinished content
- Collections
- Recent additions
- Exploration candidates

### Ranking

Rank those candidates using:

- Current playback context
- User affinity
- Semantic similarity
- Engagement predictions
- Novelty
- Recent exposure
- Frequency limits
- Historical promotion response

This keeps expensive ranking work away from the entire media catalog.

## Promotion Timing

A good recommendation shown at a terrible moment is still a bad experience.

Potential promotion points include:

- Chapter boundaries
- Scene transitions
- Episode endings
- Movie endings
- Pause events
- Existing break markers
- User-configured intervals
- Other low-disruption moments

The system should treat timing as part of the recommendation problem.

## Promotion Formats

Possible formats include:

- Trailers
- Posters
- Banners
- "Coming Up Next"
- Contextual recommendations
- Continue Watching
- Collection promotions
- Franchise promotions
- Discovery recommendations

The presentation layer should be independent from the ranking engine.

## Open Source Direction

The project is intended to build on existing open-source media and recommendation technology rather than depending on a proprietary advertising ecosystem.

Potential integrations may include:

- Jellyfin or another open media server
- FFmpeg
- Local databases
- Vector indexes
- Open-source recommendation/ranking frameworks
- Local ML inference runtimes
- WebSocket or equivalent playback event interfaces

Specific technologies can change as the implementation develops.

## Development Strategy

The first version should avoid unnecessary machine-learning complexity.

### MVP

Start with:

1. Media metadata ingestion
2. Playback event collection
3. Content similarity
4. Candidate retrieval
5. Deterministic ranking
6. Poster/banner promotions
7. Basic timing rules
8. Local recommendation history

Then introduce:

```text
embeddings
    ↓
behavioral signals
    ↓
learned ranking
    ↓
engagement prediction
    ↓
exploration / exploitation
```

The boring deterministic version should work before the clever probabilistic version gets invited to the party.

## Repository

The repository separates the high-level concept from implementation details.

```text
/
├── README.md
└── idea.md
```

`README.md` is the project overview.

`idea.md` contains the broader product and architecture concept, including the reasoning behind adaptive promotion, engagement signals, ranking, timing, privacy, and future directions.

As implementation begins, additional components can be introduced without turning the root README into a 900-line archaeological site.

## Project Status

Concept / early architecture.

The project is currently focused on defining the system model and identifying the right interfaces between media playback, contextual understanding, recommendation, ranking, and promotion.

## Core Principle

The system should make a large personal media library feel less like a database of files and more like a continuously curated television channel.

The viewer already owns the content.

The system's job is to help them discover it.
