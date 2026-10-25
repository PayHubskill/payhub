<p align="center">
  <img src="https://avatars.githubusercontent.com/u/347955301?s=200&v=4" width="120" alt="PayHub Logo" />
</p>

<h1 align="center">PayHub</h1>

<p align="center">
  <strong>Your friendly onchain work marketplace.</strong>
</p>

<p align="center">
  Create tasks • Claim work • Get paid in your own token<br>
  Fully chat-based. No website needed.
</p>

<p align="center">
  <a href="https://x.com/Onchain_Based">
    <img src="https://img.shields.io/badge/Built%20by-%40Onchain__Based-black?logo=x&logoColor=white" alt="Built by @Onchain_Based" />
  </a>
  <a href="https://github.com/PayHubskill/payhub">
    <img src="https://img.shields.io/badge/Bankr-Skill-blue" alt="Bankr Skill" />
  </a>
</p>

---

### What is PayHub?

PayHub is a **Bankr skill** that turns ordinary chat into a fully functional onchain task marketplace.  

Users can:
- Create tasks and set rewards in your token
- Claim available work
- Submit proof of completion
- Get paid directly in the configured ERC-20 token

Everything happens through natural language — on Bankr Terminal, Telegram, or X.

---

### Features

- Fully chat-based experience
- Create, claim, submit, approve, and pay tasks
- Payments using your own token
- Persistent storage via Bankr file system
- Clean task status flow
- Owner-controlled approval system
- Simple and transparent

---

### Installation

Tell your Bankr agent:

```bash
install the payhub skill from https://github.com/PayHubskill/payhub
```

---

### Quick Start

1. Install the skill
2. Configure your payment token:
   ```bash
   set payhub token to 0xYourTokenAddress with symbol PAY on base
   ```
3. Create your first task:
   ```bash
   create task: Write a short thread about PayHub | reward: 300 PAY
   ```

---

### Main Commands

| Command | Description |
|---------|-------------|
| `list tasks` | Show all open tasks |
| `create task: [description] \| reward: [amount] TOKEN` | Create a new task |
| `claim task #ID` | Claim a task |
| `submit task #ID: [proof]` | Submit proof of work |
| `approve task #ID` | Approve and send payment |
| `reject task #ID` | Reject a submission |
| `my tasks` | Show your tasks |
| `view task #ID` | View full task details |

---

### How It Works

1. Someone creates a task and sets a reward
2. A worker claims the task
3. The worker submits proof
4. The owner reviews and approves
5. Payment is sent to the worker in the configured token

All data is stored under `/payhub/` in the agent's persistent file storage.

---

### Links

- Builder: [@_Onchain_Based](https://x.com/Onchain_Based)
- Repository: [github.com/PayHubskill/payhub](https://github.com/PayHubskill/payhub)

---

### License

MIT
```
