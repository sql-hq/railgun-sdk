# SQL Cash RAILGUN SDK

Typed integration used by SQL Cash for private Ethereum USDC payments. It wraps the official RAILGUN SDK for vault creation, synchronization, shielding, private transfers, normal unshielding and return-to-origin.

Website: https://sql.cash  
GitHub: https://github.com/sql-hq  
X: https://x.com/SQL_Cash  
Support: [support@sql.cash](mailto:support@sql.cash)

## Install the release package

```sh
npm install https://github.com/sql-hq/railgun-sdk/releases/download/v0.1.0/silentquery-railgun-0.1.0.tgz
```

For application dependency policy and the scope of the audit, read [DEPENDENCY_REVIEW.md](DEPENDENCY_REVIEW.md). Consumer projects must apply their own root-level overrides.

The package name is @silentquery/railgun. Availability here is through a GitHub release tarball; no npm-registry publication is claimed.

```ts
import { USDC, MAINNET_CHAIN_ID } from '@silentquery/railgun';
const engine = await import('@silentquery/railgun/engine');
console.log(MAINNET_CHAIN_ID, USDC.decimals);
```

For browser builds, install the globals entry before loading the engine and provide the Node built-in browser aliases used in [the application Vite configuration](https://github.com/sql-hq/sql-cash/blob/main/apps/web/vite.config.ts). The SDK requires a database adapter, configured RPC transport and prover-artifact storage. Use the application as the complete integration example; it is not a hosted signing service.

## Development

Use Node.js 22 or newer.

```sh
pnpm install --frozen-lockfile
npm run typecheck
npm test
npm run build
npm pack
```

The lightweight root export contains network constants, amount helpers and recipient resolution. The engine export loads the RAILGUN wallet integration lazily. See [source](https://github.com/sql-hq/railgun-sdk/tree/main/src) and [integration documentation](https://github.com/sql-hq/sql-docs/blob/main/docs/railgun-integration.md) for the actual API and setup.

## Safety and scope

Only Ethereum mainnet USDC is the active financial asset. The separate $SQL project-token address is informational and does not change USDC or the RAILGUN pool. Signing remains in the caller's wallet. Origin returns must use the SDK-derived original destination, not an arbitrary recipient. No operator key, private backup, funded fixture or test-signing endpoint is distributed.

Controlled mainnet financial tests passed; this is not an independent audit or comprehensive real external-wallet certification. Preserve wallet/session guards, exact approvals, backup requirements and synchronization checks in your integration.

[Releases](https://github.com/sql-hq/railgun-sdk/releases) · [Application](https://github.com/sql-hq/sql-cash) · [Evidence](https://github.com/sql-hq/sql-docs/tree/main/evidence)

MIT licensed; see LICENSE. Support and private vulnerability reports: support@sql.cash.
