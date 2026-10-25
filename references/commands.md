# PayHub Command Reference

## General Commands

| Command | Description | Who can use |
|---------|-------------|-------------|
| `list tasks` | Show all open tasks | Everyone |
| `show open tasks` | Alias for list tasks | Everyone |
| `available work` | Alias for list tasks | Everyone |
| `view task #ID` | Show full details of a specific task | Everyone |
| `my tasks` | Show tasks created or claimed by the user | Everyone |
| `help payhub` | Show available commands | Everyone |

## Client Commands (Task Creators)

| Command | Example | Description |
|---------|---------|-------------|
| `create task:` | `create task: Design a logo \| reward: 500 PAY` | Create a new task |
| `cancel task #ID` | `cancel task #1042` | Cancel an open or claimed task |
| `approve task #ID` | `approve task #1042` | Approve work and send payment |
| `reject task #ID` | `reject task #1042 low quality` | Reject a submission |

## Worker Commands

| Command | Example | Description |
|---------|---------|-------------|
| `claim task #ID` | `claim task #1042` | Claim an open task |
| `submit task #ID:` | `submit task #1042: https://...` | Submit proof of work |
| `abandon task #ID` | `abandon task #1042` | Release a claimed task back to open |

## Owner / Admin Commands

| Command | Description |
|---------|-------------|
| `set payhub token to [address] with symbol [SYMBOL] on [chain]` | Configure the payment token |
| `payhub config` | Show current configuration |
| `payhub stats` | Show basic statistics (optional) |
