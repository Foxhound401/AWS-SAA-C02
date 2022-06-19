IOPS measures the number of read and write **operations** persecond, while throughput measures the number of **bits** read or written per second

Although they measure different things, they genearlly follow each other as IO operations have about the same size.

If you have large files, you simply need more IO oeprations to read the entire file. The file size has no effecton the IOPS as it measures the number of clusters read or written, not the number of files.

If you have a small files, there will be more overhead, so while the IOPS and througput look good, you may experience a lower actual performance

https://stackoverflow.com/a/15759907/5934288

This is the analogy I came up with when talking about Throughput and IOPS.

Think of it as:

1. You have 4 buckets (Disk blocks) of the same size tha tyou want to fil or empty with water.
2. You'll be using a jug to transfer the water into the buckets. Now your quesiton will be:
    - At a given time (persecond), how mnay jugs of water can you pour (write) or withdraw (read)? This is IOPS.
    - At a given time (persecond) what's the amount (bit, kb, mb, etc) of water the
   jug can transfer into/out of the bucket continuously? This is througput.

Additionally, there is a delay in the process of you pouring and/or withdrawing the
water. This is latency.
There're 3 things to consider when talking about IOPS and Througput:

- Size (file size/block size)
- Patterns (Random/Sequential)
- Mix (Read/Write) percentage
