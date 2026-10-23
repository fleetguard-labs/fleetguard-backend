# Testnet evidence

The dedicated faucet-funded pilot uploaded a reference manager and v1/v2 Wasms, deployed three instances sharing manager/tag stable, proposed v2, waited through the four-ledger delay and executed one reference update. All three returned version 2 and preserved values 100, 101 and 102. No real assets or production account keys are involved.

Manager: `CCFUY4ANTFFX4V2EXIIJCOETT5YXTMUIFDYKVRKYFLEZEHGX6B66DAL3`

Instances:
- `CBOGFA56BYJU7TNLY7AAN6EMDQFDJWO4JKU5TWEWYLTZF26DVTFQB7XJ`
- `CDYVEH2FSMTVIA2DEGI6UN76TQ3BUPFTBGNVXJR4FBMWDRAONUWQDSGH`
- `CALHSM64OGCTOSCKEGJD5QQJFEF3VMABLU7Z3MNGUEUHYF6QVZLEQO27`

Transactions:
- v1 upload: `56213406cd1f23145dc1d056943815d50ad892b542697f21747e362b18ff14f8` (ledger 5348262)
- v2 upload: `15c8d79d88b3c77676d4c3ff1578013fce290c55510f16183f8f374eb72534d9` (ledger 5348263)
- manager upload: `a82479671a9ec5ea330b2af019baba47a24fcca248789af099c8faa2d572b932` (ledger 5348265)
- manager deploy: `0b14d6dee913531b503b71ffe4324d18d84a1912482ec173d09fe0f1c96bda67` (ledger 5348266)
- publish v1: `4672cde2f11a62cc5eaaec5c7583fbeff22f64e302d31a77df8362ac518d88b8` (ledger 5348268)
- spawn 1: `35d7b71d15e7bbbb98e93ff52d89551084b41478b2d600f446f9d86432546a07` (ledger 5348275)
- spawn 2: `b27e3b97ad140c762eb76f39788818b72d209b18c512def8fe8a2764ea62bff4` (ledger 5348277)
- spawn 3: `76f44cf1602ac95f95bae05e479f94fae127fd57ad3e8cb379b29cc57cef47c8` (ledger 5348278)
- propose v2: `eab634cf013312b35c1602fd207bc325f9d7f07958eeffd4748d4abb098e4571` (ledger 5348282)
- execute v2: `2a522db1fa9e74ecb1bd71e96ca75587ab4f5c5d3c92a6dd7e1747650cf26e4f` (ledger 5348287)

## Replay and verification

```sh
npm ci
node replay-testnet.mjs
node verify-testnet.mjs
```

Replay checks saved success results, transaction hashes and before/after assertions offline. Live verification re-fetches transaction receipts and current owner/tag resolution from fixed testnet RPC. RPC retention expiry and testnet resets may make live verification unavailable. Saved simulations are not submitted transactions or independent proofs; the receipts demonstrate actual deployment and upgrade execution.

## Fresh pilot

Build all Wasms in sibling fleetguard-contracts using sh ./build.sh, then run node pilot-testnet.mjs here. This explicitly creates a dedicated testnet identity in ignored .private/, obtains faucet funds, signs and submits only the pilot's testnet operations, and overwrites the local public testnet-evidence.json. It is separate from the web/API app, which cannot sign or submit. Never use a production identity. Do not commit .private/.

## Limits

No automated semantic/storage compatibility proof, global dependent inventory, rollback guarantee or production audit. Host tests additionally verify timelock rejection, admin authorization, stale expected hashes and unchanged state under the supplied fixtures. The actual pilot used one admin-controlled reference manager; it does not establish safety for arbitrary managers.
