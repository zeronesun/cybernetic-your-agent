# L2/L3 Initialization Output Example

This file demonstrates a typical L2/L3 initialization dialogue. After the user sends an refine command, the Agent generates structured L2 and L3 drafts based on its understanding of the user's history.

> **Note**: The user preferences in this example are fictional and are only used to demonstrate the output format and refinement granularity. Your Agent will generate a version specific to you based on your historical conversations.

---

## Agent's Refinement Output

Based on my current understanding of you, here are the refinement results:

### [L2·User's Underlying Logic]

- **Communication Preferences**: Concise and direct, no pleasantries or padding; clear boundaries, stop when "no" is said
- **Quality Standards**: Code must include verification methods; output must be reusable, not just correct once
- **Decision Making**: Risk-first approach, expose the full problem before discussing solutions; second-order assessment precedes intuition
- **Learning Mode**: Cross-domain theory transfer; unity of knowledge and action, understanding must translate into operation

### [L3·Scenario Core Principles]

- **Short-form Writing**:
  - Emotional tone prioritized over plot development
  - Leave space at the end, no value summary or moral elevation
  - Line drawing to build imagery, not dependent on metaphorical rendering

- **Code Output**:
  - Write tests or verification methods first, then implement
  - Functional completeness prioritized over detailed comments
  - Mark uncertain behavior as "to be verified", don't fabricate

- **Architecture Design**:
  - Define system boundaries and data flow first, then select technology stack
  - Evaluate extensibility and failure modes, not just happy path
  - Output includes risk classification (P0-P3) and mitigation

- **Troubleshooting**:
  - Locate log/runtime scene root cause first, don't guess based on experience
  - Mark uncertain aspects as "to be verified"
  - Provide reusable troubleshooting steps, not just conclusions

---

## User Review Actions

1. **Item-by-item Confirmation**: For each principle, ask yourself—"Is this really my stable preference?"
2. **Correct Deviations**: Directly tell the Agent which point is wrong and what it should be
3. **Supplement Gaps**: If you feel a dimension/scenario is missing key principles, state them directly
4. **Remove Inaccuracies**: If the Agent fabricated it (you don't have this preference), remove it directly

---

## Common Correction Examples

| Agent's Original Refinement | User's Correction | Explanation |
| :----------------- | :--------------------------------------- | :--------------------------------- |
| Communication: Concise and direct | Communication: Concise but must have sufficient context | User discovered they need context, not just brevity |
| Short stories: Leave space at end | Short stories: Leave space at end; but series stories can have gentle closure | User added an exception case |
| Code output: Test-first | Code output: Tests can be added later during rapid prototyping | User distinguished between different standards for prototypes and formal output |

---

## Save Command

After review is approved, send:
> Save the confirmed L2 and L3 above to memory.

The Agent will store them in the memory main area, organized by [L2·User's Underlying Logic] and [L3·Scenario Core Principles] nodes.