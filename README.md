# Web3 Campaign Evidence Registry

**An open-source, evidence-first registry for Web3 campaign claims, source provenance and historical changes.**

> Project status: **alpha scaffold (v0.1.0)**. The included dataset is synthetic test data, not real campaign information.

## Why this exists

Campaign discovery is already served by established crypto research products. This project explores a narrower infrastructure problem: making individual campaign claims traceable to their sources, timestamped, explicitly classified by evidence state, and easy for other developers to consume.

The unit of information is a **claim**, not a campaign listing. A single campaign can have separate claims about its announcement, dates, requirements, reward terms and distribution contract. Each claim can have different supporting evidence and a different verification state.

## What this first release does

- Defines a versioned JSON format for projects, campaigns, evidence and claims.
- Validates schema, identifiers, cross-references and evidence-state requirements.
- Exposes a read-only FastAPI service.
- Provides a CLI command to validate a registry before it is merged or published.
- Includes tests and a synthetic fixture.

## What it deliberately does not do

- No wallet connection, private-key or seed-phrase collection.
- No eligibility checker or reward estimator.
- No automated campaign scraping or AI verification.
- No campaign discovery dashboard or notification system.
- No claim that an official announcement proves individual wallet eligibility.

These exclusions keep the first release auditable. Automated source adapters should only be added after source terms, access rules, rate limits and the value of each integration have been checked.

## Quick start

Requires Python 3.11 or newer.

```bash
python -m venv .venv
```

Activate the environment, then install the project and development tools:

```bash
# macOS / Linux
source .venv/bin/activate

# Windows PowerShell
.venv\Scripts\Activate.ps1

pip install -e ".[dev]"
```

Validate the included synthetic dataset:

```bash
cer validate --data data/registry.json
```

Run the test suite:

```bash
pytest
```

Run the API:

```bash
cer serve --data data/registry.json
```

Open the interactive API documentation at `http://127.0.0.1:8000/docs`.

## API endpoints

| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/health` | Validate the registry and report service health |
| GET | `/v1/projects` | List projects |
| GET | `/v1/campaigns` | List campaigns |
| GET | `/v1/campaigns/{campaign_id}` | Retrieve one campaign |
| GET | `/v1/evidence` | List evidence references |
| GET | `/v1/evidence/{evidence_id}` | Retrieve one evidence record |
| GET | `/v1/claims` | List claims |
| GET | `/v1/claims?verification_state=unverified` | Filter claims by evidence state |

The API is read-only in this release. Changes are made through reviewed dataset updates, not public write endpoints. The dataset is loaded from the JSON file for each request, which keeps this alpha implementation simple but is not intended for high-throughput production use.

## Data model

- **Project:** ecosystem, canonical project name and website.
- **Campaign:** a campaign associated with a project. A non-unknown lifecycle status must reference a claim that supports that exact status.
- **Evidence:** a source pointer, source kind, publisher, retrieval timestamp and optional SHA-256 digest of a captured artifact.
- **Claim:** one atomic assertion, its value, verification state, review timestamp and evidence references.

### Verification states

| State | Meaning |
|---|---|
| `official_statement` | An official project source explicitly states the claim |
| `technical_evidence` | Direct technical evidence supports the claim |
| `independently_corroborated` | Multiple independent publishers support the claim |
| `community_reported` | The claim is supported by a community source only |
| `unverified` | No sufficient supporting evidence has been recorded |
| `contradicted` | Recorded evidence conflicts with the claim |

These are evidence classifications, not probability scores or eligibility decisions. The validator checks structural rules; it cannot decide whether a source is genuinely authoritative or whether two publishers are truly independent. Human review is still required.

A URL is a pointer, not proof of historical page content. A SHA-256 digest is useful only when the corresponding captured artifact is retained and accessible to reviewers. The digest alone does not establish authenticity or authority.

## Contributing data

1. Find a primary source controlled by the project or a relevant technical source.
2. Create a campaign, evidence record and atomic claim in `data/registry.json`.
3. Use an explicit verification state. Do not mark a claim verified merely because a third-party tracker repeats it.
4. Include the retrieval time in UTC and a concise factual note.
5. Run `cer validate --data data/registry.json` and `pytest`.
6. Submit a pull request with source links and a short explanation of the review method.

See [CONTRIBUTING.md](CONTRIBUTING.md), [docs/verification-model.md](docs/verification-model.md), the machine-readable [JSON Schema](schemas/registry.schema.json) and the [public launch checklist](docs/launch-checklist.md).

## Research and limitations

The initial competitive scan found existing campaign trackers and commercial APIs. This repository is not claiming they are inaccurate. The differentiating hypothesis is that a neutral, inspectable claim-and-evidence layer may be useful to researchers and developers. That hypothesis still needs user interviews, independent data review and external API integrations.

See [docs/research-sources.md](docs/research-sources.md) for the initial landscape and primary-source plan.

## Licensing

The MIT license in `LICENSE` applies to the software code in this repository. It does not grant rights to third-party source pages, copied text, images, databases or API output. Dataset licensing is discussed separately in [DATA-LICENSE.md](DATA-LICENSE.md); do not assume that upstream content can be republished.

## Security

Do not submit private keys, seed phrases, wallet credentials, personal data or secrets. See [SECURITY.md](SECURITY.md) for responsible disclosure guidance.# Campaign-Evidence-Registry-CER-
An evidence-first, open-source registry for Web3 campaign claims, source provenance and historical changes.
