# BitnationShares Token Verification

Byte-for-byte bytecode verification for the BitnationShares (XBN) token deployed by Alex Van de Sande (avsa).

| Field | Value |
|---|---|
| Contract | `0xedb37809291efbc00cca24b630c3f18c2a98f144` |
| Network | Ethereum Mainnet |
| Block | 1,019,907 |
| Deployed | Feb 17, 2016 |
| Deployer | `0xd1220a0cf47c7b9be7a2e6ba89f429762e7b9adb` (alex.vandesande.eth) |
| Compiler | soljson v0.2.2+commit.ef92f566 |
| Optimizer | ON |
| Runtime match | ✅ EXACT (1,416 bytes) |

## Verification

```bash
node verify.js
```

## What this contract does

AVSA's token tutorial variant implementing `BitnationShares` (XBN) for Bitnation's migration to Ethereum (Feb 2016). Includes:

- `spentAllowance` mapping tracking total allowance already spent, enabling secure `transferFrom` without resetting the full allowance
- `approve` calls back the spender via the `tokenRecipient` interface (`sendApproval`), an early callback pattern predating ERC-677
- `transferFrom` emits `Transfer(msg.sender, _to, _value)` — a historical bug where `msg.sender` was used instead of `_from`

Source corresponds to avsa's Token Standard gist with the `sendApproval` callback interface, deployed the same day as the Foundation Tip Jar (0x5aae, block 1,019,844).

## Source recovery notes

- Multiple soljson versions (v0.2.1 and v0.2.2) produce identical output; v0.2.2 listed as the canonical match
- Contract name in source is `BitnationShares` (not `token` or `MyToken`)
- The `tokenRecipient` helper contract is included in the same source file
