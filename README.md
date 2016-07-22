# RamMonitor
Dynamic Memory Monitor for Teensy 3.x by Adrian Hunt

Teensy 3.x RAM Monitor
 copyright by Adrian Hunt (c) 2015 - 2016

 simplifies memory monitoring;  providing both "raw"
 memory information  and with frequent  calls to the
 run() function, adjusted information with simulated
 stack allocations. memory is also monitored for low
 memory state and stack and heap crashes.

 raw memory information methods:

     int32_t unallocated() const;
   calculates space between  heap and current stack.
   will return negitive if heap and stack currently
   overlap, corruption is very likely.

     uint32_t stack_used() const;
   calculates the current stack size.

     uint32_t heap_total() const;
   return the heap size.

     uint32_t heap_used() const;
   returns allocated heap.

     uint32_t heap_free() const;
   returns unused heap.

     int32_t free() const;
   calculates total free ram; unallocated and unused
   heap. note that this uses the current stack size.

     uint32_t total() const;
   returns total physical ram.

 extended memory information.  These methods require
 the  RamMonitor  object to  be initialized  and the
 run() method called regularly.

     uint32_t stack_total() const;
   returns the  memory required for  the stack. this
   is determind by historical stack usage.

     int32_t stack_free() const;
   returns stack  space that can be used  before the
   stack grows and total size is increased.

     int32_t adj_unallocd() const;
   calculates  unallocated  memory,  reserving space
   for the stack.

     int32_t adj_free() const;
   calculates  total  free  ram  by  using  adjusted
   unallocated and unused heap.

     bool warning_lowmem() const;
     bool warning_crash() const;
   return warning states: low memory is flagged when
   adjusted unallocated memory is below a set value.
   crash is flagged when  reserved stack space over-
   laps heap and there is a danger of corruption.

     void initialize();
   initializes the RamMonitor  object enabling stack
   monitoring and the extended information methods.

     void run();
   detects stack growth and updates memory warnings.
   this function must be called regulary.

 when using the extended memory information methods,
 a single  RamMonitor  object  should be  create  at
 global level.  two static  constants define  values
 that control stack allocation step size and the low
 memory  warning level.  these values  are in bytes.
 the stack allocation step must be divisable by 4.

     static const uint16_t STACKALLOCATION;
     static const uint16_t LOWMEM;

