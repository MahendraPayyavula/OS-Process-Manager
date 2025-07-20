💻 OS Process Management Simulation
This project is a C++ console application that simulates fundamental operating system process management concepts. It allows you to create and terminate processes, manage their state transitions (Ready to I/O and vice-versa), and visualize the process hierarchy and execution stacks.

✨ Features
Process Creation: Create new processes, optionally specifying a parent process to build a hierarchical tree.

Process States: Simulate processes moving between a Ready Queue (processes ready to run) and an I/O Queue (processes waiting for I/O completion).

Function Call Stack: Each process maintains its own call stack to simulate function execution within that process.

Process Termination: Terminate processes, which also removes them from any queues and updates the process hierarchy.

Process Hierarchy Display: Visualize the parent-child relationships between processes in a tree-like structure.

State Overview: Get a snapshot of the current state of the Ready Queue, I/O Queue, and the Process Tree.

🛠️ How to Compile and Run
Prerequisites
A C++ compiler (e.g., GCC, Clang) that supports C++11 or later.

Compilation
Save the provided code as a .cpp file (e.g., process_manager.cpp).

Open a terminal or command prompt.

Navigate to the directory where you saved the file.

Compile the code using your C++ compiler. For GCC, you would use:

Bash

g++ process_manager.cpp -o process_manager -std=c++11
g++: The GNU C++ compiler.

process_manager.cpp: Your source code file.

-o process_manager: Specifies the output executable name.

-std=c++11: Ensures compilation with C++11 features (for unique_ptr, make_unique, etc.).

Running the Application
After successful compilation, run the executable:

Bash

./process_manager
The application will present a menu of options in the console, allowing you to interact with the process manager.

🚀 Usage
Upon running, you'll see a menu like this:

--- OS Process Manager (Console) ---
1. Create Process
2. Call Function
3. Request I/O
4. Complete I/O
5. Terminate Process
6. Show State
0. Exit
Enter choice:
Follow the prompts to perform actions:

1. Create Process: Enter a name for the new process and an optional parent PID. If no parent (enter -1), it tries to become the root process.

2. Call Function: Specify a PID and a function name to push onto that process's call stack.

3. Request I/O: Move a process from the Ready Queue to the I/O Queue.

4. Complete I/O: Move a process from the I/O Queue back to the Ready Queue.

5. Terminate Process: Remove a process from the system. This handles its removal from queues and its parent's children list.

6. Show State: Displays the current contents of the Ready Queue, I/O Queue, and the process hierarchy.

0. Exit: Quits the application.

⚙️ Design Choices
Process Class: Represents an individual process with a PID, name, parent pointer, children list, and a call stack.

ProcessManager Class: Manages all processes in the system.

pidCounter: Simple counter for unique Process IDs.

root: Pointer to the root of the process hierarchy.

processMap: std::map<int, unique_ptr<Process>> stores all active processes, mapping PIDs to unique_ptrs. unique_ptr is used for automatic memory management and clear ownership.

readyQueue & ioQueue: std::queue<Process*> to simulate different process states. Note that these queues store raw pointers to Process objects, with ownership residing in processMap.

Memory Management: std::unique_ptr is used in processMap to ensure that process objects are automatically deallocated when they are no longer needed (e.g., when a process is terminated or the ProcessManager goes out of scope).

Queue Management: Helper functions removeFromQueue are used to manage process transitions between the ready and I/O queues.

Hierarchy Management: When a process is created, it's linked to its parent. When terminated, it's removed from its parent's children list.
