### 1. The Definition

- **Process:** A running program.
    
- A program is lifeless (code on disk); a process is active execution.
    

### 2. The Crux: How to provide the illusion of many CPUs?

- **Time Sharing:** Running one process, stopping it, and running another.
    
- **Mechanism vs. Policy:**
    
    - **Mechanism (HOW):** Low-level protocols.
        
        - Example: **Context Switch** (saving/restoring registers to switch processes).
            
    - **Policy (WHICH):** High-level algorithms for decision making.
        
        - Example: **Scheduling** (deciding which process runs next based on history/priority).
            

### 3. Machine State (What comprises a process?)

To summarize a process, you must know its machine state:

1. **Memory (Address Space):**
    
    - **Code:** Instructions.
        
    - **Static Data:** Initialized variables.
        
    - **Heap:** Dynamically allocated memory (malloc).
        
    - **Stack:** Local variables, function parameters, return addresses.
        
2. **Registers:**
    
    - **Program Counter (PC/IP):** Which instruction executes next.
        
    - **Stack Pointer / Frame Pointer:** Manages the function stack.
        
3. **I/O Information:** List of open files (file descriptors).
    

### 4. Process API

A standard OS provides specific interface calls for processes:

- **Create:** Make a new process (e.g., via shell command).
    
- **Destroy:** Halt a runaway process.
    
- **Wait:** Wait for a process to finish.
    
- **Miscellaneous Control:** Suspend/Resume.
    
- **Status:** Get info (how long it has run, etc.).
    

### 5. Process Creation (Loading)

How a program becomes a process:

1. **Load Code/Data:** Read executable bytes from disk into memory (Address Space).
    
    - Note: Modern OSes do this **lazily** (loading pieces only when needed).
        
2. **Allocate Stack:** Set up memory for local variables/params. Initialize argc/argv.
    
3. **Allocate Heap:** Set up area for dynamic memory.
    
4. **I/O Setup:** Establish file descriptors (STDIN, STDOUT, STDERR).
    
5. **Start:** Jump to the entry point (usually main()), transferring control to the CPU.
    

### 6. Process States

A process is generally in one of three states:

1. **Running:** Executing instructions on the CPU.
    
2. **Ready:** Ready to run, but the OS has not scheduled it yet.
    
3. **Blocked:** Waiting for an event (e.g., Disk I/O completion).
    

**State Transitions:**

![[state-transitions.png]]
### 7. Data Structures

The OS tracks processes using specific structures:

- **Process List (Task List):** Keeps track of all ready/running/blocked processes.
    
- **Process Control Block (PCB):** A C-structure containing information about a specific process.
    
    - Includes: Process ID (PID), State (Running/Ready/etc.), Parent process, Context (Saved Registers), Open files.
        
- **The zombie state** is a **temporary, necessary state** for a terminated child process. It exists so the parent can collect the child's exit status. If the parent fails to collect this status using wait(), the zombie can persist and potentially cause problems. Proper process management, especially by the init process for orphaned children, is key to preventing these issues.
