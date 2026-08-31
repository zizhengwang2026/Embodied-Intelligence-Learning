# Lecture 49 · MCP: Giving the LLM Real Control over the Physical World

> **Lecture info**
> - Date: 2026-10-01 (Thu)
> - Lecture #: 49 (Study Plan Day 49, P9)
> - Plan ref: `study-plan-60d.md` → **P9**, episodes **183–186**
> - Goal: Close the biggest gap left on Day 44 — make the LLM not just **talk** but actually **do**. The key is **MCP (Model Context Protocol)**. This is the most important lecture of P9.

---

## 0. One-line summary

> My own understanding: **MCP = the “USB standard” for plugging peripherals into an LLM**: it defines how tools describe themselves, how the model discovers them, how it calls them, and how results come back — so the model can **autonomously choose and invoke tools** to act on the real world. It is not an ordinary API wrapper: with a plain API, *you* decide what to call; with MCP, **the model decides**.

---

## 1. Core concepts (eps 183–186)

### 1.1 183 What MCP is
- **MCP** is an open protocol that exposes **tools / data sources / devices** to an LLM in a uniform way.
- Three roles:
  - **MCP Host**: the program running the LLM (chat client, your robot’s main control program).
  - **MCP Client**: the component inside the host that talks to servers.
  - **MCP Server**: the capability provider (e.g. “arm-control server”, “file-reading server”).
- Three kinds of capability: **Tools** (callable functions), **Resources** (readable data), **Prompts** (preset templates).

### 1.2 184 Client–server interaction flow
Typical loop:
1. **Connect & discover**: the client asks “what tools do you have?” → the server returns a list (name + description + parameter schema).
2. **Model decides**: the tool list goes into context; the user says “pick up the red block” → the model judges whether to call `move_arm` or `grasp`.
3. **Invoke**: the client issues the call with the tool name and arguments chosen by the model.
4. **Return**: the server executes and returns the result; the model turns it into a natural-language reply.

### 1.3 185 Controlling physical devices
- The key shift: **the model’s output changes from “a paragraph” into “a structured tool call”** (tool name + arguments).
- Now speaking and doing are connected: **one user sentence → model picks a tool → real device moves → result returns**.

### 1.4 186 An MCP server driving real hardware
- A typical server wraps hardware ops into tools such as `set_joint_angle`, `open_gripper`, `get_camera_objects`.
- Engineering notes:
  - Write clear tool descriptions (the model decides usage from that text) — **vague descriptions mean the tool never gets used**.
  - **Validate parameter ranges**; never pass a model-produced value straight to hardware.
  - Add **confirmation steps / allow-lists** for dangerous operations.

---

## 2. Principles (grab these)

1. **MCP is a protocol for autonomous tool selection**, not an API wrapper library.
2. **The tool list is documentation written for the model** — clearer text, better calls.
3. **Everything downstream of the model needs validation and guardrails**, especially moving hardware.

## 2.5 补充细节：What MCP is / the three primitives

- MCP = Model Context Protocol, an open protocol for uniformly connecting external tools and data to an LLM, communicating over JSON-RPC underneath.
- Two roles: Host/Client (runs the model, initiates calls) and MCP Server (exposes capability); the Server provides three capability primitives:
- Three primitives: Tools (let the model "do things", callable), Resources (let the model "read data"), Prompts (give the model "prompt templates").
- Value: instead of writing a separate SDK adapter for every tool, everything plugs into one standard protocol; swapping models or tools rarely means rewriting integration code.
- Connecting hardware: the server wraps the arm / gripper / camera as Tools, so the model can "say one sentence" to drive real devices (see the ALOHA demo in the next lecture).

## 3. One diagram: the MCP loop

![MCP interaction loop](assets/mcp_flow.svg)

---

## 4. Today’s steps

1. **Watch 183–186** (1.0–1.5×), focus on 184 (interaction flow) and 186 (how to write tool descriptions).
2. **Draw the interaction flow from memory** — label Host / Client / Server.
3. **Design 3 tools for an imaginary task**: name, description, parameters and valid ranges.
4. **Feel the “model chooses” part**: offer two similar tools (e.g. `move_arm` vs `rotate_wrist`) and see whether it picks correctly.
5. **Design a validation layer**: list which parameters must be range/type checked.
6. **Mirror test (3 min):** *“What MCP is ___; the three roles ___; the essential difference from a plain API wrapper ___; why add validation ___.”*

> **Done today when:** you can draw the MCP flow unaided + explain the difference from plain APIs + mirror test passed.

---

## 5. Common pitfalls

| # | Myth | Truth |
|---|---|---|
| 1 | MCP is just an API wrapper | The essence is **the model chooses the tool**, not hardcoded call logic |
| 2 | Tool descriptions can be sloppy | The model relies entirely on that text to decide usage; vague = never called |
| 3 | Send model output straight to hardware | Validate parameters and confirm dangerous ops — one hallucination is one accident |
| 4 | Small local models select tools reliably | Small models are weak at tool choice: fewer tools, sharper descriptions, stronger guardrails |
| 5 | MCP means “it can do anything” | Its reach equals the tools you expose; the tool set defines its hands and feet |

---

## 6. DEA cross-link (light, not main thread)

- For soft actuators, **MCP guardrails matter even more**: if the model mis-invokes `set_voltage` with an out-of-range value, the membrane can break down — or someone can get hurt. Design tools at the **semantic level** rather than the physical level (e.g. `bulge_slightly` instead of `set_voltage_kv`), keeping physical limits sealed inside the server.
- That’s a paper-worthy opening: **tool abstraction and safety-constraint design for LLM-driven soft actuators** — funnel dangerous high-voltage actions into a few audited tools.

---

## 7. Next / checkpoint

- **Checkpoint passed =** draw the MCP flow unaided + explain the difference from APIs + mirror test.
- **Next (Day 50):** MCP results showcase + Stanford ALOHA intro (187–188) — **entering P10 behavior cloning**.

---

### References (not required today)
- Episodes 183–186 (B站《黑马程序员 · 具身智能》).
- Reuse: Day 44 (the “no tools” gap closed here), Day 47 (structured output helps tool calling).

*This lecture strictly follows 《60-Day Plan》 Day 49 (P9): 183–186. Zero military content.*
