# Turbin3 Prerequisite Challenge: Vault Program

This is my solution for the Turbin3 Q4 2026 Builders Cohort prerequisite challenge.

## What it does

The vault program lets a user deposit SOL, withdraw SOL, and close the vault.
I extended the withdraw instruction so that after the transfer, it makes a
Cross Program Invocation (CPI) to the Turbin3 registration program. That call
records my GitHub username (jamesonchain).

## Deployed on devnet

Program ID: 154hqWbHuPGboFu1wBzSTgc2g6aJ17oyMKhexUwNiMV

Withdraw transaction (the one that calls the registration program):
3yP23Z7B6ubjas1fisfCAeo5BaVDEf2Xns891qUUWYWUo9ywHBHBET1dML2SZ9JDYcLvjAhf7vmrG9AfSPSyTZV2

Explorer: https://explorer.solana.com/tx/3yP23Z7B6ubjas1fisfCAeo5BaVDEf2Xns891qUUWYWUo9ywHBHBET1dML2SZ9JDYcLvjAhf7vmrG9AfSPSyTZV2?cluster=devnet

## How the CPI works

1. The user calls withdraw.
2. The vault sends SOL to the user, signed by the vault's own seeds.
3. The vault then calls the registration program's initialize instruction.
4. The registration program writes my GitHub username into my application account.

## Run it yourself

Requirements: Solana CLI 4.3.x, Anchor 1.2.1, pnpm.

pnpm install
anchor build

Note: the registration only works once per wallet, so running the full test
again on devnet with the same wallet will fail at the withdraw step.

## Files

programs/pre-req-vault/src/instructions/withdraw.rs has the CPI.