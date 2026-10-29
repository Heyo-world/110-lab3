# Lemon Clicker Bug Report

**Name: Tia Lim**
**Tickets solved: 2** <!-- e.g. 1, 2, 3, 5, 6 (at least five) -->

Copy the template below once for each ticket you solved. 

---

## Ticket <number>: <ticket title>

### Actual cause

<!-- Which file and function was the bug in, and what was wrong with the code?
     Explain why that code produced the behavior described in the ticket. -->

**File / function:**

**What was wrong:**

### Fix

<!-- What did you change, and why does that change fix the problem? -->

### How did you find it?

#### Hypothesis testing

**What hypothesis ultimately led you to identify the buggy code, and why?**

#### Backward tracing

<!-- Start from the symptom you saw and work backwards, one step at a time,
     until you reach the buggy line. For each step, note where you looked
     and what you saw there. Add steps as needed. -->

1. **Symptom:** <!-- what you saw, e.g. text on screen, console error -->
2. **Traced back to:** <!-- where that came from, e.g. a function, a request in the Network tab, a server log -->
3. **Traced back to:**
4. **Buggy code:** <!-- the file, function and line where the trace ended -->

<!-- It is okay to use your judgement here in limiting the number of traceback steps. We want to understand your 
    reasoning for how you discovered where the bug was -->

### Confirming the fix

<!-- How did you confirm the problem is gone? -->

---

## Ticket <number>: 1 Fixed Lemon Random Position Generation

### Actual cause

<!-- Which file and function was the bug in, and what was wrong with the code?
     Explain why that code produced the behavior described in the ticket. -->

**File / function:** GameScreenView.ts, randomizeLemonPosition()

**What was wrong:** Lemon was only moved to very few positions, usually the corner of the screen due to Math.round(Math.random())

### Fix

<!-- What did you change, and why does that change fix the problem? -->
Math.round() limiting the result of randomX and randomY to only a few values

### How did you find it?

#### Hypothesis testing

**What hypothesis ultimately led you to identify the buggy code, and why?**
Since it was related to the lemon's position, I hypothesized it was caused by randomizeLemonPosition()

#### Backward tracing

<!-- Start from the symptom you saw and work backwards, one step at a time,
     until you reach the buggy line. For each step, note where you looked
     and what you saw there. Add steps as needed. -->

1. **Symptom:** Lemon only moved to the corners of the screen and sometimes were randomly generated in the same position multiple times in a row<!-- what you saw, e.g. text on screen, console error -->
2. **Traced back to:** GameScreenView.ts<!-- where that came from, e.g. a function, a request in the Network tab, a server log -->
3. **Traced back to:** Function randomizeLemonPosition()
4. **Buggy code:** Lines 85 and 86<!-- the file, function and line where the trace ended -->

<!-- It is okay to use your judgement here in limiting the number of traceback steps. We want to understand your 
    reasoning for how you discovered where the bug was -->

### Confirming the fix

<!-- How did you confirm the problem is gone? -->
I added console.log("X: ", randomX, "  Y: ", randomY); and confirmed more random positions are generated.

---

## Ticket <number>: 2 Fixed Repeated Calls of submitScoreToServer()

### Actual cause

<!-- Which file and function was the bug in, and what was wrong with the code?
     Explain why that code produced the behavior described in the ticket. -->

**File / function:** GameScreenController.ts, endGame()

**What was wrong:** Line 88 had this.stopTimer; instead of this.stopTimer();

### Fix

<!-- What did you change, and why does that change fix the problem? -->
Replaced this.stopTimer; with this.stopTimer();

### How did you find it?

#### Hypothesis testing

**What hypothesis ultimately led you to identify the buggy code, and why?**
The gameOverSound kept playing and the program reverts to the Game Over screen when the Play Again button is pressed, which led me to think submitScoreToServer(). After adding console.log() in multiple calls and backtracing, I found the buggy code.

#### Backward tracing

<!-- Start from the symptom you saw and work backwards, one step at a time,
     until you reach the buggy line. For each step, note where you looked
     and what you saw there. Add steps as needed. -->

1. **Symptom:** Lemon only moved to the corners of the screen and sometimes were randomly generated in the same position multiple times in a row<!-- what you saw, e.g. text on screen, console error -->
2. **Traced back to:** ResultScreenController.ts, submitScoreToServer()<!-- where that came from, e.g. a function, a request in the Network tab, a server log -->
3. **Traced back to:** ResultScreenController.ts, showResultsFromServer()
4. **Traced back to:** main.ts, switchToScreen()
5. **Traced back to:** GameScreenController.ts, endGame()
6. **Buggy code:** Line 88 in GameScreenController.ts<!-- the file, function and line where the trace ended -->

<!-- It is okay to use your judgement here in limiting the number of traceback steps. We want to understand your 
    reasoning for how you discovered where the bug was -->

### Confirming the fix

<!-- How did you confirm the problem is gone? -->
The console.log()s aren't repeatedly appearing in the web console, and the result screen and game over sound isn't repeating anymore.

---

## Ticket <number>: 3 Fixed fetching api/stats

### Actual cause

<!-- Which file and function was the bug in, and what was wrong with the code?
     Explain why that code produced the behavior described in the ticket. -->

**File / function:** MenuScreenController.ts, loadStatsFromServer()

**What was wrong:** Line 51 mispelled api/stats as api/stat

### Fix

<!-- What did you change, and why does that change fix the problem? -->
Replaced api/stat with api/stats;

### How did you find it?

#### Hypothesis testing

**What hypothesis ultimately led you to identify the buggy code, and why?**
The web console showed a thrown error that "/api/stat" cannot be found. It led me to check fetch("/api/stat"); and index.ts

#### Backward tracing

<!-- Start from the symptom you saw and work backwards, one step at a time,
     until you reach the buggy line. For each step, note where you looked
     and what you saw there. Add steps as needed. -->

1. **Symptom:** The web console showed a thrown error that "/api/stat" cannot be found<!-- what you saw, e.g. text on screen, console error -->
2. **Traced back to:** MenuScreenController.ts, loadStatsFromServer()<!-- where that came from, e.g. a function, a request in the Network tab, a server log -->
3. **Traced back to:** index.ts, app.get("/api/stats")
4. **Buggy code:** Line 51 in MenuScreenController.ts<!-- the file, function and line where the trace ended -->

<!-- It is okay to use your judgement here in limiting the number of traceback steps. We want to understand your 
    reasoning for how you discovered where the bug was -->

### Confirming the fix

<!-- How did you confirm the problem is gone? -->
The same error is no longer thrown, and the Best, Average, and Scores Saved are now properly shown on the starting screen