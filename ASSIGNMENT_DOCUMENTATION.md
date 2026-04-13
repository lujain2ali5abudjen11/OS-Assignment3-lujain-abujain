# Assignment 3 - Complete Documentation

**Student Name**: [LUJAIN ALI ABUDJIN]  
**Student ID**: [445051961]  
**Date Submitted**: [2026-04-13]

---

## 🎥 VIDEO DEMONSTRATION LINK (REQUIRED)

> **⚠️ IMPORTANT: This section is REQUIRED for grading!**
> 
> Upload your 3-5 minute video to your **PERSONAL Gmail Google Drive** (NOT university email).
> Set sharing to "Anyone with the link can view".
> Test the link in incognito/private mode before submitting.

**Video Link**: [\[Paste your personal Gmail Google Drive link here\]](https://drive.google.com/file/d/13c4QeVcyzEYmbuLHLdiARlJunn_fwJZn/view?usp=drivesdk)

**Video filename**: `[445051961]_Assignment3_Synchronization.mp4`

**Verification**:
- [ ] Link is accessible (tested in incognito mode)
- [ ] Video is 3-5 minutes long
- [ ] Video shows code walkthrough and commits
- [ ] Video has clear audio
- [ ] Uploaded to PERSONAL Gmail (not @std.psau.edu.sa)

---

## Part 1: Development Log (1 mark)

Document your development process with **minimum 3 entries** showing progression:

### Entry 1 - 2026-04-13, 6:00 PM
**What I implemented**: Added ReentrantLock to protect shared counters (contextSwitchCount, completedProcessCount, totalWaitingTime)

**Challenges encountered**: Understanding where to place lock() and unlock()

**How I solved it**: Used try-finally to ensure the lock is always released

**Testing approach**: Ran the program multiple times to check values

**Time spent**: 20 minutes

---

### Entry 2 - 2026-04-13, 6:30 PM
**What I implemented**: Added ReentrantLock to protect executionLog

**Challenges encountered**: Preventing ConcurrentModificationException

**How I solved it**: Wrapped executionLog.add() inside lock

**Testing approach**: Verified no crash during execution

**Time spent**: 15 minutes

---

### Entry 3 - 2026-04-13, 7:00 PM
**What I implemented**: Added Semaphore to control CPU access

**Challenges encountered**: Where to place acquire() and release()

**How I solved it**: Used acquire() before execution and release() inside finally

**Testing approach**: Checked only one process runs at a time

**Time spent**: 20 minutes

---

### Entry 4 - 2026-04-13, 7:30 PM
**What I implemented**: Fixed synchronization issues in methods

**Challenges encountered**: Some code didn't work correctly

**How I solved it**: Reviewed and corrected method placement

**Testing approach**: Debugged and tested again

**Time spent**: 15 minutes

---

### Entry 5 - 2026-04-13, 8:00 PM
**What I implemented**: Final testing and verification

**Challenges encountered**: Ensuring everything runs correctly

**How I solved it**: Re-tested all parts

**Testing approach**: Multiple runs

**Time spent**: 20 minutes

---

## Part 2: Technical Questions (1 mark)

### Question 1: Race Conditions

Race conditions occur when multiple threads access shared data at the same time. One example is contextSwitchCount where threads increment it simultaneously, causing incorrect values. Another example is executionLog where multiple threads add data, which may lead to errors or inconsistent output. Concurrent access is a problem because updates can overlap. This may result in lost updates or corrupted data. Synchronization prevents these issues.

---

### Question 2: Locks vs Semaphores

ReentrantLock is used to protect critical sections so only one thread accesses shared data. Semaphore is used to limit the number of threads accessing a resource. I used ReentrantLock for counters and executionLog to prevent race conditions. I used Semaphore to control CPU execution so only one process runs at a time.

---

### Question 3: Deadlock Prevention

Deadlock happens when threads wait for each other indefinitely. One prevention method is using try-finally to always release locks. Another method is avoiding nested locks. In my code, I used try-finally to ensure locks and semaphores are released.

---

### Question 4: Lock Granularity Design Decision 

I used one lock for all three counters (coarse-grained). This simplifies the design and reduces complexity. However, it limits concurrency because only one thread can access any counter at a time. Fine-grained locking allows better performance but is more complex. Since the counters are independent, fine-grained locking provides better concurrency. But I chose coarse-grained for simplicity and safety.

---

## Part 3: Synchronization Analysis (1 mark)

### Critical Section #1: Counter Variables

**Which variables**: contextSwitchCount, completedProcessCount, totalWaitingTime  

**Why they need protection**: Multiple threads modify them causing incorrect results  

**Synchronization mechanism used**: ReentrantLock  

**Code snippet**:
```java
lock.lock();
try {
    contextSwitchCount++;
} finally {
    lock.unlock();
}
Justification: Prevents race conditions and ensures accurate updates

Critical Section #2: Execution Log

What resource: executionLog

Why it needs protection: Multiple threads write simultaneously

Synchronization mechanism used: ReentrantLock

Code snippet:

lock.lock();
try {
    executionLog.add(message);
} finally {
    lock.unlock();
}

Justification: Prevents ConcurrentModificationException

Critical Section #3: CPU Semaphore

Purpose of semaphore: Control number of running processes

Number of permits and why: 1 to allow one process at a time

Where implemented: Inside run() method

Code snippet:

cpuSemaphore.acquire();
try {
    // execution
} finally {
    cpuSemaphore.release();
}

Effect on program behavior: Ensures controlled execution

Part 4: Testing and Verification (2 marks)
Test 1: Consistency Check

Testing procedure:

Run the program multiple times

Results: Output was consistent

Why synchronization is necessary: Without it, shared variables may give incorrect results

Conclusion: Synchronization works correctly

Test 2: Exception Testing

Testing procedure: Checked executionLog

Results: No exception occurred

What this proves: Proper synchronization

Test 3: Correctness Verification

Expected values: Correct totals

Actual values: Matched expected

Analysis: No errors

Test 4: Different Scenarios

Scenario tested: Different process values

Purpose: Check stability

Results: Program worked correctly

What I learned: Synchronization improves reliability

Part 5: Reflection and Learning
What I learned about synchronization:

I learned how synchronization works in multithreading. I understood race conditions and how they affect programs. I used locks and semaphores to fix these problems. It was difficult at first but became easier. I learned the importance of protecting shared resources. Synchronization helps avoid errors and improve program reliability.

Real-world applications:

Example 1: Banking systems
Example 2: Operating systems scheduling

How I would explain synchronization to others:

Synchronization is like taking turns. Only one thread uses a resource at a time to avoid problems.

Part 6: GitHub Repository Information

Repository URL: [PUT YOUR LINK HERE]

Number of commits: 3

Commit messages:

Initial commit
Added synchronization
Final submission
Documentation update
Summary

Total time spent on assignment: 5 hours

Key takeaways:
Learned locks
Learned semaphores
Avoid race conditions

Most challenging aspect: Understanding synchronization

What I'm most proud of: Completing all tasks correctly
---

**End of Documentation**
