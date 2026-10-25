---
name: payhub
description: Onchain work marketplace skill for Bankr. Create tasks, claim work, submit proof, and receive payment in a custom token. Fully chat-based. Use this skill when the user wants to post tasks, complete microtasks, manage a task board, earn tokens, or pay workers through natural language.
tags: [marketplace, tasks, work, payments, onchain, bankr, microtask]
version: 1.0.0
metadata:
  clawdbot:
    emoji: "📺"
    homepage: "https://github.com/PayHubskill/payhub"
---

# PayHub

PayHub is a fully chat-based onchain work marketplace that runs as a Bankr skill.  
Users can create tasks, claim them, submit proof of completion, and get paid in a configured ERC-20 token — all through natural language.

No external website is required. All state is stored in the agent's persistent file storage.

## When to Use This Skill

Activate this skill whenever the user:
- Wants to create or manage tasks
- Wants to claim or complete work
- Asks about available tasks / open work
- Wants to pay or get paid for completed work
- Mentions PayHub, task board, microtasks, or onchain work

## Core Concepts

| Term | Meaning |
|------|---------|
| **Task** | A unit of work with description, reward, status, and optional deadline |
| **Client** | The person who creates a task and provides the reward |
| **Worker** | The person who claims and completes a task |
| **Payment Token** | The ERC-20 token used for all rewards (set by the skill owner) |

## Data Storage

Store all PayHub data under the following structure:

```
/payhub/
├── config.json          # Token settings and owner configuration
├── tasks.json           # All active and recent tasks
└── history/             # Optional archive of completed tasks
```

If the `/payhub` folder or required files do not exist, create them automatically on first use.

### config.json structure
```json
{
  "tokenAddress": "0x...",
  "tokenSymbol": "PAY",
  "tokenChain": "base",
  "owner": "@Onchain_Based",
  "minReward": 10,
  "maxReward": 10000,
  "requireOwnerApproval": true
}
```

### tasks.json structure
Each task should contain:
- `id` (number)
- `title` / `description`
- `reward` (number)
- `token` (symbol)
- `status` (`open`, `claimed`, `submitted`, `completed`, `rejected`, `cancelled`, `abandoned`)
- `client` (who created it)
- `worker` (who claimed it, if any)
- `proof` (submission content)
- `createdAt`
- `updatedAt`
- `deadline` (optional)

## Supported Commands

### General
- `list tasks` / `show open tasks` / `available work`
- `view task #ID`
- `my tasks`
- `help payhub`

### Client Commands
- `create task: [description] | reward: [amount] [TOKEN]`
- `cancel task #ID`
- `approve task #ID`
- `reject task #ID [reason]`

### Worker Commands
- `claim task #ID`
- `submit task #ID: [proof]`
- `abandon task #ID`

## Workflow Rules

### Creating a Task
1. Parse the description and reward.
2. Validate against `minReward` and `maxReward`.
3. Assign the next available numeric ID.
4. Set status to `open`.
5. Save to `tasks.json`.
6. Confirm creation to the user with the Task ID.

### Claiming a Task
1. Check that the task exists and status is `open`.
2. Assign the current user as `worker`.
3. Change status to `claimed`.
4. Confirm to the user.

### Submitting Proof
1. Only the assigned worker can submit.
2. Save the proof content.
3. Change status to `submitted`.
4. Notify that the task is waiting for approval.

### Approving a Task
1. Only the skill owner (or designated admin) can approve if `requireOwnerApproval` is true.
2. Verify the worker address/wallet.
3. Execute the token transfer using the configured payment token.
4. Change status to `completed`.
5. Record the transaction hash if available.

### Rejecting / Cancelling / Abandoning
- Update the status accordingly.
- Clear the worker if the task returns to `open`.
- Always confirm the action.

## Payment Rules

- Only use the token defined in `config.json`.
- Never send payment automatically without explicit approval.
- Always resolve the recipient (wallet address, ENS, or social handle) before transferring.
- Confirm the amount and recipient with the user before executing the transfer.
- After successful payment, update the task status to `completed`.

## Response Style

- Be clear and structured.
- Use tables when listing multiple tasks.
- Always show Task ID prominently.
- Keep confirmations short and professional.
- If an action is not allowed for the current user, explain why politely.

## First-Time Setup

When the skill is used for the first time and `config.json` is missing:
1. Inform the user that PayHub needs to be configured.
2. Ask for the payment token address, symbol, and chain (default to Base).
3. Set the current user as the owner.
4. Create the initial config and empty tasks list.

## Important Safety Rules

- Do not invent task data.
- Do not pay from the wrong token.
- Do not allow non-owners to approve payments by default.
- Always double-check wallet addresses before sending tokens.
- Prefer updating existing records over creating duplicates.

---

PayHub turns conversation into productive onchain work.  
Keep the experience simple, transparent, and reliable.
```
