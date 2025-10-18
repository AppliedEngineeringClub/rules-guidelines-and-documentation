# **Professional and Safe Coding Style Guidelines**

This document defines consistent, safe, and maintainable coding practices suitable for general software projects and safety-critical systems.

---

## **1. File Headers**
Each source file must begin with a standardized comment block containing:

- **Filename**  
- **Author(s)**  
- **Date created / modified**  
- **Module or project name**  
- **Brief summary** of purpose and contents  
- **Dependencies** or related modules  

---

## **2. Function Headers**
Every function or method should include a short comment block describing:

- **Name and purpose**  
- **Inputs:** name, type, purpose, and range  
- **Outputs / return value**  
- **Side effects:** modifies global state, writes to file, etc.  
- **Assumptions or preconditions**

---

## **3. Naming Conventions**
- Use **descriptive, readable names** for all identifiers. Avoid unclear abbreviations.  
- Use **camelCase** for variables and functions; **PascalCase** for classes or data types.  
- Constants should use **UPPER_SNAKE_CASE**.  
- Prefix **member variables** with `m_` and **global variables** with `g_` when appropriate.  
- Function names should be **verbs** that describe behavior (e.g., `readFile()`, `computeSum()`).  

---

## **4. Formatting and Whitespace**
- Use **tabs** for indentation — one tab per level.  
- Opening braces `{` go on a **new line**, aligned with the controlling statement.  
- Closing braces `}` align with their opening braces.  
- Place **spaces around operators** (`x = y + z;`).  
- Keep lines under **100 characters**.  
- Use **blank lines** to separate logical blocks.  
- **Same-line comments** are allowed and encouraged when they describe that line clearly.  

Example:
```cpp
total = value1 + value2;    // Add both values for the total
```

---

## **5. Function Design**
- Keep functions **short and focused** — one clear purpose each.  
- **Avoid recursion.** Use iterative or explicit stack solutions instead.  
- Limit **nesting depth** (3–4 levels maximum).  
- Each function should have **a single, clear exit point** when possible.  
- Include braces `{}` for all `if`, `else`, `for`, and `while` statements — even one-liners.  
- **Indent consistently** using tabs for all inner blocks.  

---

## **6. Variable Declarations**
- Every variable must be **explicitly initialized** before use.  
- **Group related variables** on the same line when they share a purpose:  
  ```cpp
  int width, height, depth;    // Dimensions in pixels
  ```
- Otherwise, declare variables **individually** for clarity:  
  ```cpp
  double temperature;          // Celsius
  double pressure;             // Pascals
  ```
- Avoid reusing variable names in nested scopes.  

---

## **7. Control Flow**
- Avoid `goto`, `continue`, and `break` (except in `switch` statements).  
- Each loop must have a **definite termination condition**.  
- No unbounded loops (e.g., `while(true)` without a guaranteed exit).  
- Avoid **side effects in conditions**:  
  ```cpp
  if ((x = getValue()) > 0)    // ❌ Avoid assignment in condition
  ```

---

## **8. Memory and Resource Management**
- No **recursion** or **dynamic memory allocation** in safety-critical code.  
- Use **static** or **stack allocation** instead.  
- Free or release all resources **deterministically**.  
- Avoid **shared mutable global data** — use encapsulation or parameters.  
- Always check for **allocation failures** and **invalid pointers**.  

---

## **9. Comments**
- Comments should describe **intent and reasoning**, not restate the code.  
- **Same-line comments** are acceptable for short notes.  
- Multi-line explanations go **above** the relevant section.  

Example:
```cpp
// Calculate final velocity using v = u + at
velocity = initialVelocity + acceleration * time;    // basic kinematic formula
```

---

## **10. Error Handling**
- Always **check function return codes** or exceptions.  
- Never ignore potential errors from I/O, conversions, or system calls.  
- Prefer **graceful fallback** or **error propagation** instead of silent failure.  

---

## **11. Testing and Verification**
- Code must be **deterministic** — same inputs yield the same outputs.  
- Avoid reliance on **undefined or platform-specific behavior**.  
- Test all **branches, limits, and failure paths**.  
- Run **static analysis tools** regularly — no unhandled warnings.  

---

## **12. NASA/JPL Safety Rules Summary**

| Rule | Description |
|------|--------------|
| 🚫 **No recursion** | Prevents stack overflows and unpredictable timing. |
| 🚫 **No dynamic memory allocation** | Must use static or stack memory. |
| ✅ **Single return per function** | Increases traceability and readability. |
| ✅ **All variables initialized** | Prevents undefined behavior. |
| ✅ **All errors handled** | Never ignore failures. |
| ✅ **No global mutable state** | Reduces coupling and race conditions. |
| ✅ **Deterministic execution** | Predictable and testable behavior. |

---

## **13. Example Layout**

```cpp
//=============================================================
// Filename:    SensorReader.cpp
// Author:      Justin Pemberton
// Date:        2025-10-18
// Description: Reads and averages sensor data safely.
//=============================================================

double computeAverage(double a, double b, double c)    // Compute average of three values
{
	// Validate inputs
	if (a < 0 || b < 0 || c < 0)
	{
		return -1.0;    // Invalid input
	}

	double sum = a + b + c;    // Total of all readings
	double avg = sum / 3.0;    // Compute mean
	return avg;                // Return average value
}    // end computeAverage
```
