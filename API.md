# Local API

GET /api/health, /api/sample, /api/evidence, /api/runs, /api/runs/:id.
POST /api/capture accepts {"instanceIds":["C..."]}; fixed testnet RPC only, maximum 20 unique IDs.
POST /api/review accepts the complete analyzer sample shape {snapshot,proposal,beforeInterface,afterInterface}; maximum JSON body 1 MiB. Analyzer bounds are 20 manager/tag references, 100 instances and 100 declared functions per version.

POST review validates before persistence. Reports preserve the submitted input and a SHA-256 snapshot digest. The digest is an integrity identifier, not an on-chain attestation. Invalid input returns 422; missing token 401; foreign Host/Origin 403. No signing, execution or submission API exists.
