# PayHub Workflows

This document describes the complete step-by-step logic the agent must follow for every major action.

## 1. Create Task

**Trigger phrases:**  
`create task:`, `new task:`, `post task:`, `add task:`

**Steps:**
1. Parse the task description and reward amount.
2. Check if `/payhub/config.json` exists. If not, guide the user to configure the payment token first.
3. Validate the reward against `minReward` and `maxReward` in config.
4. Generate the next sequential Task ID (start from 1001 if no tasks exist).
5. Create a new task object with:
   - status: `"open"`
   - client: current user
   - worker: null
   - proof: null
   - createdAt and updatedAt timestamps
6. Append the task to `/payhub/tasks.json`.
7. Reply with a clear confirmation including the Task ID and reward.

## 2. List Tasks

**Trigger phrases:**  
`list tasks`, `show open tasks`, `available work`, `what tasks are available`

**Steps:**
1. Load `/payhub/tasks.json`.
2. Filter tasks with status `"open"` (by default).
3. Display in a clean table format:
   - Task ID
   - Short description (truncated if too long)
   - Reward
   - Client
4. If no open tasks exist, say so clearly.

## 3. Claim Task

**Trigger phrases:**  
`claim task #ID`, `take task #ID`, `I'll do task #ID`

**Steps:**
1. Find the task by ID.
2. Verify status is `"open"`.
3. Set `worker` to the current user.
4. Change status to `"claimed"`.
5. Update `updatedAt`.
6. Save the file.
7. Confirm the claim and remind the user how to submit proof.

## 4. Submit Proof

**Trigger phrases:**  
`submit task #ID:`, `submit proof for #ID:`, `done task #ID:`

**Steps:**
1. Find the task by ID.
2. Verify the current user is the assigned worker.
3. Verify status is `"claimed"`.
4. Save the proof content.
5. Change status to `"submitted"`.
6. Update `updatedAt`.
7. Inform the user that the task is now waiting for approval.

## 5. Approve Task (Payment)

**Trigger phrases:**  
`approve task #ID`, `accept task #ID`, `pay task #ID`

**Steps:**
1. Verify the current user is the skill owner (or has approval permission).
2. Find the task and confirm status is `"submitted"`.
3. Resolve the worker’s wallet address (from Bankr identity if possible).
4. Confirm the amount and recipient with the user before sending.
5. Execute the token transfer using the configured payment token.
6. On success:
   - Change status to `"completed"`
   - Save transaction hash if available
   - Notify both client and worker
7. On failure: report the error clearly and do not change status.

## 6. Reject Task

**Trigger phrases:**  
`reject task #ID`, `deny task #ID`

**Steps:**
1. Only owner/admin can reject.
2. Change status to `"rejected"`.
3. Optionally clear the worker so the task can be re-opened later.
4. Save the reason if provided.

## 7. Cancel / Abandon Task

- **Cancel** (by client): status → `"cancelled"`
- **Abandon** (by worker): status → `"open"` and clear worker

Always confirm the action before applying.
