# Documentation Evolution: From Afterthought to Definition of Done

## Early approach

Important decisions often lived in chat, and documentation was updated after implementation—if it was updated at all.

## What failed

The code could be correct while the repository still described an older design. New conversations and new models then began from stale or incomplete guidance.

## What changed

Documentation became part of normal implementation and review. Depending on the change, the Builder considers updates to:

- architecture and design documents;
- decision records;
- runbooks;
- data dictionaries;
- examples and templates;
- session notes;
- document indexes or registries.

The Reviewer verifies documentation impact. The Architecture Steward checks long-term consistency when work changes shared systems or architectural principles.

There is not a separate recurring prompt to “do documentation.” Documentation is part of the Builder's core responsibility and part of the review and architecture gates.

## Why this is better

The repository remains usable as institutional memory. Work can continue across devices, models, and contributors without reconstructing the project from old conversations.

## Reusable takeaway

**If it is necessary to understand, operate, or safely extend the system, it belongs with the system.**