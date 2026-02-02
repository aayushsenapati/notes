### 1. The Basics

- **The Von Neumann Model:** At a basic level, a running program does one thing: it fetches an instruction from memory, decodes it, and executes it. It repeats this cycle until completion.
    
- **The Operating System (OS):** A body of software responsible for making it easy to run programs, allowing programs to share memory, interacting with devices, and ensuring the system operates correctly.
    
- **Key Definitions:**
    
    - **Virtual Machine:** The OS takes a physical resource (CPU, disk, memory) and transforms it into a more general, powerful, virtual form.
        
    - **Standard Library:** The OS provides standard interfaces (APIs/System Calls) to applications.
        
    - **Resource Manager:** The OS manages the CPU, memory, and disk to allow many programs to share them efficiently and fairly.
        

### 2. Virtualizing the CPU

- **The Concept:** The OS creates the illusion that the system has an infinite number of CPUs, allowing many programs to run "simultaneously" on a single physical processor.
    
- **Mechanism:** **Time Sharing**.
    
    - The OS runs one program for a short time, stops it, runs another, and so on.
        
    - This happens so fast that it creates the illusion of concurrency.
        
- **Policy:** The OS must decide which program to run next.
    

### 3. Virtualizing Memory

- **The Model:** Physical memory is an array of bytes.
    
- **The Illusion:** Each process behaves as if it has its own private physical memory (its own **Address Space**).
    
- **Reality:**
    
    - The OS maps virtual addresses (seen by the program) to physical addresses (actual hardware).
        
    - A write to address 0x200000 in Program A does not affect data at 0x200000 in Program B.
        
- **Goal:** **Isolation** and protection. One program cannot corrupt the memory of another.
    

### 4. Concurrency

- **The Problem:** Issues arising when working on many things at once (multi-threaded programs).
    
- **Example:** Two threads trying to increment a shared counter (counter = counter + 1).
    
    - Instruction breakdown: Load value, Increment value, Store value.
        
    - If the OS switches threads mid-sequence (non-atomic execution), data is lost/corrupted.
        
- **Requirement:** The OS must provide primitives and hardware mechanisms to build correct concurrent programs.
    

### 5. Persistence

- **The Problem:** DRAM (Memory) is volatile; data is lost on crash/power loss.
    
- **The Solution:** **File System** (software) + **I/O Devices** (Hardware: Disk/SSD).
    
- **Mechanism:**
    
    - System calls (open(), write(), close()) allow users to create and manage persistent data.
        
    - The OS handles the details of writing to the physical disk (tracks, sectors, etc.).
        
    - **Journaling/Copy-on-Write:** Protocols used to prevent data corruption during system crashes.
        

### 6. OS Design Goals

1. **Abstraction:** Making the system easy to use (e.g., Files, Processes).
    
2. **Performance:** Minimizing OS overhead (time and space).
    
3. **Protection:** Isolation between applications and the OS (malicious code shouldn't crash the system).
    
4. **Reliability:** The OS must run non-stop without failing.
    
5. **Other goals:** Energy efficiency, security, mobility.
    

### 7. History of OS Development

- **Libraries:** Early OSes were just helper functions.
    
- **Batch Processing:** Human operators loaded jobs sequentially.
    
- **Multiprogramming:** Minicomputers allowed multiple jobs to reside in memory; switch to another job when one blocks on I/O.
    
- **System Calls:** Separation of **User Mode** (restricted) and **Kernel Mode** (privileged). Hardware instructions (Traps) transition between them.
    
- **UNIX:** Pioneered small, powerful tools (pipes, shell) and portability.
    
- **The PC:** Early PCs (DOS, MacOS v9) regressed (no memory protection, cooperative scheduling).
    
- **Modern Era:** Modern OSes (Windows NT, MacOS X, Linux) brought minicomputer features (protection, preemption) back to desktops and mobile devices.
    

---

## A Dialogue on Virtualization

- **Analogy:** Imagine a single physical peach (resource) but many hungry eaters (programs).
    
- **Virtualization:** Creating the illusion of a peach for every eater.
    
- **How:** When an eater is napping, you take the peach and give it to someone else.
    
- **Takeaway:** The OS turns one physical CPU into many virtual CPUs through illusions, specifically time sharing.