## Ceph performance
# demystified
Benchmarks, Tools, and the Metrics That Matter

Note: I don't know about you. But whenever *I* deploy a Ceph cluster,
I'm like ...


<!-- .slide: data-background="https://farm4.staticflickr.com/3113/3117146807_578f059d67_b_d.jpg" -->
`ceph -s`
# HEALTH_OK
Note: this guy.

And then I wonder:

- Credit: [Aidan Jones](https://www.flickr.com/photos/aidan_jones/), CC-BY-SA
- Source: https://flic.kr/p/5Ksc9t


How does it
# perform?

Note: Now "performance" are really at least three different things
when it comes to I/O, it's about...


# Latency

Note: ... latency, which is normally defined as the amount of time it
takes us to make the smallest possible write to the device; it's about...


# Throughput

Note: ... throughput, which is the amount of data we can write per
unit time; and it's about ...


# IOPS

Note: ... IOPS, which is the number of I/O operations per second.

Now, with Ceph what makes performance tuning even more challenging is
the fact that we might be needing to look at multiple dimensions
depending on our use case, such as:


# RADOS

Note: ... what's the performance of my RADOS object store, and ...


# RBD

Note: ... what's the performance of my RBD devices, and ...


# radosgw

Note: ... what is the performance of my radosgw instances, and perhaps
even ...


# CephFS

Note: ... what's the filesystem performance of my CephFS. And to make
matters even worse, Ceph throughput *and* latency *and* IOPS are
strongly determined by ...


# Block

Note: ... the performance of the block devices underpinning our OSDs,
and ...


# Network

Note: ... the performance of our storage and replication networks
(*public* and *cluster* networks in Ceph parlance).
