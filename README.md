> **Public Actor:** [Run the invoice generator on Apify](https://apify.com/kamerozkan/peppol-ubl-invoice-generator). Publication checked September 30, 2026.

# Peppol UBL Invoice Generator: Samples

Peppol UBL invoice generator for structured JSON inputs. Generate BIS Billing invoice XML and check it against the bundled EN 16931 and Peppol rule profiles before file delivery. Inspect pinned rule versions for your workflow; Peppol network transport is not included.

[Run Peppol UBL Invoice Generator on Apify](https://apify.com/kamerozkan/peppol-ubl-invoice-generator)

![Listing](https://img.shields.io/badge/Apify-public-00c7b7)
![Examples](https://img.shields.io/badge/examples-3%20paired%20local%20runs-2f855a)
![Schema](https://img.shields.io/badge/schema-Actor%20dataset-4c1)
![License](https://img.shields.io/badge/license-MIT-blue)

Generate Peppol BIS Billing 3.0.20 UBL XML from structured JSON and run pinned UBL, EN 16931, and Peppol rule checks.

This flat sample repository contains three paired JSON inputs and outputs,
the October 4 input schema snapshot verified against public release 1.0.3,
the existing Actor dataset schema snapshot, and a standard JSON Schema for one
dataset row. The examples were generated and technically evaluated by
the local release engine. They are not copied from a live Apify run.

Search topics: Peppol invoice generator, JSON to UBL XML, Peppol BIS Billing API, Peppol BIS 3.0, UBL 2.1, EN 16931.

## What the generator does

1. Accepts one `invoice` object or an `invoices` batch of up to 100.
2. Parses monetary values from decimal strings, never binary JSON floats.
3. Calculates line, tax, and payable totals with decimal arithmetic.
4. Generates a Peppol BIS Billing 3.0.20 UBL invoice XML.
5. Runs UBL 2.1 XML Schema plus the pinned CEN EN 16931 and Peppol BIS Billing 3.0.20 Schematron stylesheets.
6. Delivers only an artifact accepted by the complete pinned local preflight.
7. Returns SHA-256, byte count, versions, findings, and explicit scope limits.

## Three paired examples

| # | Scenario | Input JSON | Output JSON | Generated artifact SHA-256 |
|---:|---|---|---|---|
| 1 | Standard consulting service invoice | [input](01_standard_service_input.json) | [output](01_standard_service_output.json) | `0b178b21996f9ceaec8a603e3d5d361f71c75499c8ae723c330a9cc1c31a9d4b` |
| 2 | Multi-line professional services invoice | [input](02_multi_line_input.json) | [output](02_multi_line_output.json) | `cd13a994924797ffe17042516628d4269e0be0a1e4080172abb492a614009934` |
| 3 | Recurring service invoice | [input](03_recurring_service_input.json) | [output](03_recurring_service_output.json) | `4ad8402e6ee2edef85131b128cc36479f65dccb2e9fd1c1d7500dbfa92a19c19` |

Every output is a schema-valid production-row projection created from a real
local `GenerationResult`. The added `sampleProvenance` object is a repository
annotation. It makes explicit that no Apify run, Store publication, or customer
charge occurred.

## Input contract

- Use exactly one of `invoice` or `invoices`.
- Supply quantities, prices, and tax rates as JSON strings such as `"19.00"`.
- Use ISO `YYYY-MM-DD` dates, ISO 4217 currency codes, ISO country codes, and
  UNECE unit codes.
- Each seller and buyer needs a tax, VAT, or registration identifier.
- The complete snapshot is [`actor_input_schema.json`](actor_input_schema.json).

## Input storage maintenance on October 4, 2026

The input schema snapshot now marks the JSON `invoice` object and `invoices`
array as `isSecret: true`. Public `latest` build `1.0.3` and all deployed source
hashes were verified on October 4. The schema hash is recorded in the
maintenance evidence below.

In supported Apify input storage, these flags encrypt the marked values before
storing the run's `INPUT`. The Actor keeps Python `apify==4.0.0` and reads input
with `Actor.get_input()`, which supports automatic decoding of secret objects
and arrays. See the [Apify secret input documentation](https://docs.apify.com/actors/development/actor-definition/input-schema/secret-input).
Existing stored inputs were not audited or migrated by this maintenance.

This change keeps the runtime, dependencies, prices, dataset contract, and
recorded output files unchanged. The input snapshot also synchronizes fields
already present in the current Actor source; those pre-existing differences
from the historical repository schema are separate from the two new privacy
flags. Generated documents, dataset rows, and downloads are not encrypted by
these flags. Manage their access and retention separately.

Local checks validated the known single and batch schema-prefill inputs. No new
encrypted end-to-end Actor run was performed. Historical July 30 examples retain
their original provenance and are not output from this release. Read the
[maintenance evidence](INPUT_PRIVACY_MAINTENANCE_2026-10-04.json) for the exact scope and schema hash.

## Dataset output contract

The production result row separates processing from technical conformance:

| `processingStatus` | `conformanceStatus` | Meaning |
|---|---|---|
| `SUCCEEDED` | `ACCEPTED` | Generation and every pinned local technical layer passed |
| `SUCCEEDED` | `REJECTED` | Generation completed but at least one required technical rule failed |
| `FAILED` | `NOT_EVALUATED` | Input, engine, storage, budget, or runtime failure prevented a decision |

Schema files:

- [`actor_dataset_schema.json`](actor_dataset_schema.json) is the complete Apify
  Actor dataset schema snapshot.
- [`dataset_record.schema.json`](dataset_record.schema.json) is the Actor
  schema's `fields` contract as standalone JSON Schema.
- [`VALIDATION_REPORT.json`](VALIDATION_REPORT.json) records local generation,
  JSON parsing, input-schema, dataset-schema, and artifact-hash checks.

## Pay-per-event contract

See the live [Store pricing](https://apify.com/kamerozkan/peppol-ubl-invoice-generator) for the current `invoice-generated` event price and spending limits.
One event applies only after one invoice passes the pinned validation stack and
its artifact and evidence have been delivered. Invalid input, rejected
artifacts, storage failure, and budget refusal are not intended to charge that
event.

The Actor is publicly listed as of September 30, 2026. These committed examples retain their original local test provenance; listing visibility does not turn them into cloud-run evidence.

## Evidence boundaries

`ACCEPTED` means pinned offline technical preflight only. It does not mean:

- transmitted to Peppol, KSeF, SdI, a tax authority, or a recipient;
- accepted, registered, cleared, or assigned an official network identifier;
- digitally signed, archived, paid, booked, or legally approved;
- semantically identical to source data outside the supported input contract.

The output keeps these boundaries explicit with `transmitted: false`,
`acceptedByNetwork: null`, `networkIdentifier: null`, `signed: false`, and
`archived: false`.

## E-invoice generator family

All five repositories use one normalized invoice-intent model and product-specific
serializers and validators. The sibling products and sample repositories below are public as of September 30, 2026. Check each live listing for current pricing and input limits.

| Generator | GitHub sample repository | Apify Store URL |
|---|---|---|
| XRechnung Invoice Generator | [sample repository](https://github.com/kamerozkan/xrechnung-invoice-generator-sample) | [public Actor](https://apify.com/kamerozkan/xrechnung-invoice-generator) |
| Peppol UBL Invoice Generator | [sample repository](https://github.com/kamerozkan/peppol-ubl-invoice-generator-sample) | [public Actor](https://apify.com/kamerozkan/peppol-ubl-invoice-generator) |
| ZUGFeRD and Factur-X PDF Generator | [sample repository](https://github.com/kamerozkan/zugferd-facturx-pdf-generator-sample) | [public Actor](https://apify.com/kamerozkan/zugferd-facturx-pdf-generator) |
| FatturaPA Invoice Generator | [sample repository](https://github.com/kamerozkan/fatturapa-invoice-generator-sample) | [public Actor](https://apify.com/kamerozkan/fatturapa-invoice-generator) |
| KSeF FA(3) Invoice Generator | [sample repository](https://github.com/kamerozkan/ksef-fa-invoice-generator-sample) | [public Actor](https://apify.com/kamerozkan/ksef-fa-invoice-generator) |

## Data and license

Read [`DATA_NOTICE.md`](DATA_NOTICE.md) before using the fixtures. All invoice
values are synthetic. The MIT License covers this repository's original
documentation, JSON fixtures, and schema packaging. It does not relicense
standards, validator software, specifications, names, marks, or third-party
rulesets.

Standard: `Peppol BIS Billing` `3.0.20`  
Historical sample ruleset: `Peppol BIS Billing 3.0.20`; check the live bundled profiles for current technical scope.
