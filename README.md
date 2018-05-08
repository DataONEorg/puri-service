# puri-service

The DataONE service for resolving PURIs to resources like datasets, people, and organizations.

## Summary

The core idea is to provide the following things to DataONE:

- Platform service version independent URIs for resources that existed either literally (Objects, Nodes, Accounts) or virtually (Datasets, People, Organizations)
- Stable & resolvable Linked Open Data URIs for use in Linked Open Data contexsts such as RDF and JSON-LD
- Provide HTTP Content Negotiation for clients

### High level overview

```text
┌──────────────┐                 ┌──────────────┐               ┌──────────────┐
│    Client    │─────makes ─────▶│ PURI Service │───redirects ─▶│ DataONE API  │
└──────────────┘   request to    └──────────────┘       to      └──────────────┘
        ▲                                                               │
        │                           responds                            │
        └──────────────────────────────to───────────────────────────────┘
```

### Example requests

```text
             .───────────.
    ┌──────▶(   Client    )
    │        `───────────'
    │              │
    │            makes             makes
    │           request┬──────────request─────────────────────┐
    │                  │                                      │
    │                  ▼                                      ▼
    │    ┌──────────────────────────┐         ┌───────────────────────────────┐
    │    │GET /dataset/X            │         │GET /dataset/X                 │
    │    │Accept: text/html         │         │Accept: application/ld+json    │
    │    └──────────────────────────┘         └───────────────────────────────┘
    │                  │                                      │
    │              is  │                                      │is
returns        redirected                                  redirected
response           to                                          to
    │              ▼                                           ▼
    │            ┌────────────────────────────────────────────────────────────┐
    │            │                        PURI Service                        │
    │            └────────────────────────────────────────────────────────────┘
    │               │                                          │
    │              is                                         is
    │          redirected                                 redirected
    │              to │                                       to
    │                 │                                        │
    │                 ▼                                        ▼
    │ ┌──────────────────────────────┐    ┌───────────────────────────────────┐
    │ │search.dataone.org/#view/X    │    │LOD Service                        │
    │ │Content-Type: text/html       │    │Content-Type: application/json+ld  │
    │ └──────────────────────────────┘    └───────────────────────────────────┘
    │                 │                                     │
    │                 │                                     │
    └─────────────────◀─────────────────────────────────────┘
```

## Installation

TODO

## Development

TODO

## Contributing

Please report any bugs or feature requests as Issues on this repository. Pull Requests welcome.
