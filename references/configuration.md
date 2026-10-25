# PayHub Configuration

## First-Time Setup

When `/payhub/config.json` does not exist, the agent should:

1. Inform the user that PayHub needs initial configuration.
2. Ask for the following information:
   - Token contract address
   - Token symbol
   - Chain (default: `base`)
3. Set the current user as `owner`.
4. Create the config file with sensible defaults:
   - `minReward`: 10
   - `maxReward`: 10000
   - `requireOwnerApproval`: true

## Updating Configuration

Only the owner can update the configuration.

Supported commands:
- `set payhub token to 0x... with symbol PAY on base`
- `set payhub min reward to 50`
- `set payhub max reward to 5000`
- `payhub config` → show current settings

## Recommended Defaults

| Field | Recommended Value |
|-------|-------------------|
| tokenChain | base |
| minReward | 10 |
| maxReward | 10000 |
| requireOwnerApproval | true |
