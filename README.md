# Enhanced-XV6


This project involves modifying XV6, a simple Unix-like OS, to implement new system calls and alternative scheduling algorithms.
## System Calls

    getSysCount  – Tracks how many times a specific system call is invoked by a process and its children, using a bitmask to select the syscall.
    sigalarm & sigreturn  – Implements a periodic user-level interrupt:
        sigalarm(n, fn): Calls fn after every n CPU ticks.
        sigreturn(): Resumes process execution after fn completes.

## Scheduling Policies 

    Lottery-Based Scheduling 
        Each process has tickets determining its chance of execution.
        The more tickets, the higher the probability of being scheduled.
        If multiple processes have the same tickets, the earliest arrival wins.
        settickets(n): Sets process ticket count (inherits from parent).

    Multi-Level Feedback Queue (MLFQ)
        4 priority queues (0 = highest, 3 = lowest).
        Processes move down if they exceed their time slice.
        Time slices: 1, 4, 8, and 16 ticks.
        Round-robin scheduling in the lowest queue.
        Priority Boosting: Every 48 ticks, all processes move to queue 0 to prevent starvation.
