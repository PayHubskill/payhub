# PayHub Payment Rules

This document defines how payments must be handled inside the PayHub skill.

## Core Principles

- All payments must use the token defined in `/payhub/config.json`.
- Payments must never be sent automatically.
- Explicit approval from the skill owner (or authorized admin) is required before any transfer.
- The agent must always resolve and confirm the recipient before sending tokens.
- Safety is more important than speed.

## Payment Flow

Follow these steps strictly when approving a task:

1. **Permission Check**  
   Verify that the current user is allowed to approve payments (normally only the owner).

2. **Task Validation**  
   - Task must exist  
   - Task status must be `"submitted"`  
   - Task must have a valid worker assigned

3. **Resolve Recipient**  
   Convert the worker identity (social handle / username) into a wallet address using Bankr’s resolution tools.

4. **Confirmation**  
   Always show a clear confirmation message before sending, for example:

   ```
   Ready to pay 500 PAY to @worker for Task #1042.
   Recipient: 0xabc...def
   Confirm payment? (yes / no)
   ```

5. **Execute Transfer**  
   Only after the user confirms, execute the token transfer using the configured payment token.

6. **After Successful Payment**
   - Save the transaction hash (`txHash`) if available
   - Update task status to `"completed"`
   - Update the `updatedAt` field
   - Notify the user that payment was successful

7. **On Failure**
   - Do **not** change the task status
   - Report the error clearly to the user
   - Keep the task in `"submitted"` status so it can be retried

## Safety Rules

- Never pay using a different token than the one in `config.json`.
- Never pay if the worker wallet cannot be resolved.
- Never pay if the reward amount is invalid or missing.
- Never skip the confirmation step.
- Prefer using Bankr’s native transfer functionality.
- Double-check the amount and recipient before executing the transfer.

## Example Successful Response

```
Task #1042 has been approved.
Sending 500 PAY to @worker...

Payment successful.
Transaction: 0x1234...abcd
Status updated to completed.
```

## Example Failure Response

```
Failed to send payment for Task #1042.
Reason: Could not resolve worker wallet address.

The task remains in "submitted" status. Please try again later or contact the worker.
```
```
