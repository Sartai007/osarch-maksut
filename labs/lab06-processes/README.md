# Lab 06 — Processes and Memory

## Objective

The objective of this lab was to investigate how operating systems manage processes and memory, compare process-monitoring tools, observe memory pressure in Linux, and examine operating-system logs.

## Task 1 — Process Investigation

### Windows 11: Task Manager and Process Explorer

The process `explorer.exe` (PID 5324) was investigated using both Task Manager and Process Explorer inside the Windows 11 virtual machine.

**Task Manager:**
- Process: `explorer.exe`
- PID: 5324
- Working Set (memory): 483,240 KB
- Commit size: 137,260 KB
- Handles: 4,542

Evidence:
- `evidence/task-manager-explorer.png`
- `evidence/task-manager-parent.png`

The parent process ID was 5268.

**Process Explorer:**
- Process: `explorer.exe`
- PID: 5324
- Working Set Size: 460,524 KB
- Private Bytes: 135,196 KB
- Virtual Size: 2,152,566,148 KB
- WS Shareable: 343,460 KB

Evidence:
- `evidence/process-explorer.png`
- `evidence/process-explorer-properties.png`

### Linux: htop

The Ubuntu virtual machine was investigated using `htop`. The selected process was the SSH daemon (`sshd`).

- PID: 1635
- Parent PID: 1
- User: root
- State: S
- VIRT: 10,744 KB
- RES: 7,784 KB
- SHR: 6,616 KB

The process command was `/usr/sbin/sshd -D [listener]`.

Its open file descriptors were also inspected using `/proc/1635/fd`. They included `/dev/null` and socket descriptors.

Evidence:
- `evidence/htop1.png`
- `evidence/htop2.png`

**Note:** Task Manager and Process Explorer examined the same Windows process instance. htop examined a Linux process in a separate Ubuntu virtual machine; therefore, it was not the same process instance.

## Task 2 — Differences Between Monitoring Tools

Task Manager and Process Explorer use different labels and may show slightly different values for memory usage.

For example:
- Task Manager reports a Working Set of 483,240 KB.
- Process Explorer reports a Working Set Size of 460,524 KB.
- Task Manager reports a Commit size of 137,260 KB.
- Process Explorer reports Private Bytes of 135,196 KB.

These values are close but not identical. The tools expose different memory metrics and may capture values at slightly different moments.

Linux htop uses:
- VIRT: virtual memory size.
- RES: resident memory in physical RAM.
- SHR: shared resident memory.

The metrics should not be treated as directly interchangeable without considering their definitions.

## Task 3 — Memory Pressure Experiment

Before the experiment, the Ubuntu VM had approximately:
- Total RAM: 3.3 GiB
- Available memory: 2.7 GiB
- Swap used: 0 B
- Swap total: 3.8 GiB

A Python script was used to allocate memory in repeated 100 MB blocks. During the experiment, available RAM decreased and swapping activity was observed.

The allocation reached approximately 7,000 MB. The Linux kernel eventually terminated the Python process because the system ran out of memory.

The process was killed:
- Process: `python3`
- PID: 3489

After the experiment, the system recovered most of its available memory. Approximately 50 MiB of swap remained in use.

Evidence:
- `evidence/memory-pressure.txt`
- `evidence/memory-pressure-after.png`

## Task 4 — Linux Kernel Response

The kernel log was inspected using:

```bash
journalctl -k | grep -iE 'out of memory|oom|killed process'
```

The log recorded that the Python process invoked the OOM killer and was terminated.

The kernel reported:

`Out of memory: Killed process 3489 (python3)`

This confirms that the Linux kernel responded to memory exhaustion by terminating the memory-consuming process.

Evidence:
- `evidence/kernel-log-extract.txt`

## Task 5 — Windows Event Log

The Windows System log was checked using the Event ID 2004 query from the lecture.

One event was returned, but it came from `Microsoft-Windows-Setup` and reported successful OS information logging. It was not a memory-exhaustion event.

An additional check for events from `Microsoft-Windows-Resource-Exhaustion-Detector` returned no matching events.

Therefore, no corresponding Windows memory-exhaustion event was found in the available System log.

Evidence:
- `evidence/windows-event-log.png`
- `evidence/windows-no-memory-event.png`
- `evidence/windows-memory-log.txt`

## Conclusion

This lab demonstrated how processes can be investigated using different operating-system tools and how their memory metrics differ. The Linux memory-pressure experiment showed that when memory resources become exhausted, the kernel can invoke the OOM killer to terminate a process and protect system stability. The Windows investigation showed that no corresponding memory-exhaustion event was recorded in the available System log.


