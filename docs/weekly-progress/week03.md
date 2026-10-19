# Week 3 – Architecture and Technical Design

| Field | Response |
|-------|----------|
| Tasks planned and completed | Requirements-to-design mapping, component responsibilities, architecture and ER diagrams, end-to-end order flow, data dictionary, two ADRs, risks and Week 4 prototype goal. |
| New diagrams / files | `docs/design/architecture.drawio` + `.png`, `docs/design/er-diagram.drawio` + `.png`, `docs/design/design-decisions.md`, `docs/design/component-interfaces.md`, this file. |
| GitHub commits | [0709ff8](https://github.com/hasanackl/croptrader/commit/0709ff8) diagrams, [08c8405](https://github.com/hasanackl/croptrader/commit/08c8405) design docs, [433ef76](https://github.com/hasanackl/croptrader/commit/433ef76) README + progress log (Closes #2), merged via PR #4 |
| Technical problems found | Two orders at the same time could oversell the stock; frontend and API are separate projects and may not connect (CORS, tokens). |
| Solutions considered | Transaction + rowversion concurrency check; building one end-to-end path first in Week 4. |
| References consulted | Microsoft Learn: SPA vs traditional web apps, Choose an ASP.NET Core UI, EF Core SQL Server provider, SQL Server Express LocalDB, EF Core concurrency. |
| Report sections updated | Methodology, Proposed System, System Architecture, Technology Selection, Design Decisions. |
| Week 4 prototype objective | Register/login as a farmer, create a listing, and find it with a consumer search (FR-01, FR-02, FR-03). |
