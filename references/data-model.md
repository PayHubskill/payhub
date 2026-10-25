# PayHub Data Model

This document defines the official data structures used by the PayHub skill.

## 1. Configuration File

**Path:** `/payhub/config.json`

```json
{
  "tokenAddress": "0x1234567890abcdef1234567890abcdef12345678",
  "tokenSymbol": "PAY",
  "tokenChain": "base",
  "owner": "@Onchain_Based",
  "minReward": 10,
  "maxReward": 10000,
  "requireOwnerApproval": true,
  "createdAt": "2026-10-26T00:00:00Z",
  "updatedAt": "2026-10-26T00:00:00Z"
}
```

### Field Explanation

| Field | Type | Required | Description |
|-------|------|----------|-----------|
| `tokenAddress` | string | Yes | Contract address of the payment token |
| `tokenSymbol` | string | Yes | Token symbol (e.g. PAY) |
| `tokenChain` | string | Yes | Chain name (usually `base`) |
| `owner` | string | Yes | Skill owner (wallet or social handle) |
| `minReward` | number | No | Minimum allowed reward |
| `maxReward` | number | No | Maximum allowed reward |
| `requireOwnerApproval` | boolean | Yes | If true, only owner can approve payments |
| `createdAt` | string | Yes | ISO timestamp |
| `updatedAt` | string | Yes | ISO timestamp |

---

## 2. Tasks File

**Path:** `/payhub/tasks.json`

This file contains an array of task objects.

```json
[
  {
    "id": 1042,
    "description": "Design a simple logo for PayHub",
    "reward": 500,
    "token": "PAY",
    "status": "open",
    "client": "@Onchain_Based",
    "worker": null,
    "proof": null,
    "txHash": null,
    "deadline": null,
    "createdAt": "2026-10-26T12:00:00Z",
    "updatedAt": "2026-10-26T12:00:00Z"
  }
]
```

### Task Object Fields

| Field | Type | Required | Description |
|-------|------|----------|-----------|
| `id` | number | Yes | Unique sequential task ID |
| `description` | string | Yes | Full task description |
| `reward` | number | Yes | Reward amount |
| `token` | string | Yes | Token symbol used for payment |
| `status` | string | Yes | Current status of the task |
| `client` | string | Yes | Who created the task |
| `worker` | string \| null | Yes | Who claimed the task |
| `proof` | string \| null | Yes | Proof submitted by the worker |
| `txHash` | string \| null | No | Transaction hash after payment |
| `deadline` | string \| null | No | Optional deadline (ISO format) |
| `createdAt` | string | Yes | ISO timestamp |
| `updatedAt` | string | Yes | ISO timestamp |

---

## 3. Allowed Status Values

| Status | Meaning |
|--------|---------|
| `open` | Task is available to be claimed |
| `claimed` | Task has been claimed by a worker |
| `submitted` | Worker has submitted proof |
| `completed` | Task approved and payment sent |
| `rejected` | Submission was rejected |
| `cancelled` | Task cancelled by the client |
| `abandoned` | Task released by the worker |

---

## 4. Rules

- Task IDs must be unique and sequential (recommended to start from 1001).
- Never delete tasks. Only update the `status` field.
- Always update the `updatedAt` field whenever a task changes.
- Keep `tasks.json` reasonably sized (archive very old completed tasks if needed).
- `worker`, `proof`, and `txHash` must be `null` when not applicable.
```
