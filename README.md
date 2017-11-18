# C-Observatory
C library to observe and record all events that affect a particular process

Provide a library which can allow persistent structured logging of events that happen in the context of a process.
For instance, IPC, interrupts, messaging, file i/o

This can help in reproducing any issue that happens in a large event-driven program

Example:
 A game of chess can be recorded completely using the algebraic notation
 1. e4 e5 
 2. Bc4 Nc6 
 3. Qh5 Nf6 
 4. Qxf7#

The program can define different types of events and register persistent queues that keep track of various events.
This can be useful in providing a replay option as well.

typedef struct persistent_event_data_ {
    time_t timestamp;
    void   *data;
} persistent_event_data;

typedef struct persist_event_ {
    uint32_t                type;
    size_t                  data_unit_size;
    size_t                  data_in_memory_units;
    void                    *reported_to; /* This is the function which was notified of this type of event */
    persistent_event_data  **event_data_list; /* An array of datail */
    File                    *persistent_file;  
};
