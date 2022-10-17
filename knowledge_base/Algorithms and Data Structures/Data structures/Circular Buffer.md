## Getting started
A circular buffer is a data structure that uses a single fixed size [[buffer]] as if it were connected end-to-end. this buffer lends itself easily to buffering [[data streams]]. 
![[Circular_buffer.svg.png]]
## Overview
a circular buffer starts out empty and has a set length. assuming that an element is written inside the buffer (location of the first element is irrelevant) then the write pointer advances in the buffer. 
reading from the buffer retrieves the oldest elements written and advances the read pointer.
when the pointers reach the end of the buffer, they loop back to the beginning
assuming that a write operation is done onto a full buffer, then the oldest data is overwritten (dropped data).
alternatively, an exception can be raised instead of overwriting the data.
writing onto a full buffer will push back the read pointer to the next elements in the buffer instead of the old elements that were removed.
## when to use
- circular buffers are perfect for a [[FIFO]] data structure. specially since handling the elements doesn't need a [[mutex]] and/or shuffling elements around.
- when the [[queue]] size is predefined, it is better to use a circular buffer. when not knowing the size, a [[Linked List]] is the better approach
- when handling multimedia and large data, overwriting circular data is the best way of doing things since after a timeout old data is no longer needed so it can be discarded.
## How to implement
A circular buffer can be implemented using two [[pointers]] and two integers
- buffer start in memory
- buffer capacity (length)
- write to buffer index (end)
- read from buffer index (start)
a partially full buffer will look like this, with the write buffer (end) is equal to the read buffer (start) + the number of elements in the array
![[standard_partially_full_buffer.png]]
a full buffer will look like this, with the write buffer (end) is one element before the read buffer(start), additional writes will cause overwrite or exception.
![[standard_circular_buffer_full.png]]
- in case of data overwrite, additional writes when a buffer is full will result in the read pointer (start) being pushed back alongside the write pointer
### example c implementation 

```
#define BUFLEN 3

int buf[BUFLEN];   /* array to be treated as circular buffer of BUFLEN integers */
int end = 0;       /* write index */
int start = 0;     /* read index */

void put(int item)
{
    buf[end++] = item;
    end %= BUFLEN;
}

int get()
{
    int item = buf[start++];
    start %= BUFLEN;
    return item;
}
```
## optimization
the implementation can be optimized by mapping the underlying buffer to two contiguous regions of virtual memory, reading from and writing to the circular buffer may then be carried out with greater efficiency by means of direct memory access. the region of memory should have a length equal to some multiple of the system's page size. when falling beyond the first virtual memory region, the access will wrap around to the beginning of the underlying buffer. when the read offset is advanced into the second virtual region, the write is called for the entire memory block, and then both offsets are decremented by the length of the underlying buffer.
the number and size of the virtual memory slots can vary based on the needs of the program.
## concrete examples of circular buffers
- multimedia players usually use circular buffers since the data compression is lossless, time critical, and doesn't NEED sanity check.
- IO operations (keyboards, hardware input/ouput, ethernet adapters, usb) all can use circular buffering, since getting the input (writing to the buffer) is very time critical, but the handling of this info (reading) can lag for a bit 