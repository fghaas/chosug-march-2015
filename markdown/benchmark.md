Ceph cluster
# Benchmarks


<!-- .slide: data-background="images/ceph_benchmarks_bottom_to_top.svg" data-background-size="auto 95%" data-background-color="rgba(255,255,255,0.8)" -->


## Block device benchmarks
(simple)
```sh
dd if=/dev/zero of=/dev/sdh1 bs=1G count=1 oflag=direct

dd if=/dev/zero of=/dev/sdh1 bs=512 count=1000 oflag=direct
```

Note: This is a very simple *destructive* device benchmark to run on
your OSD. Don't do this on a device already in use as an OSD. Top:
throughput test of writing 1GB in `O_DIRECT` mode; bottom, latency
test of writing 1000 sectors in `O_DIRECT` mode.


<iframe src="https://asciinema.org/api/asciicasts/13104?size=medium&amp;theme=solarized-light&amp;speed=3" id="asciicast-iframe-13104" name="asciicast-iframe-13104" scrolling="yes"></iframe>

Note: `dd` throughput and latency tests against journal (`journal`)
and a file in the filestore (`test.bin`).


## Block device benchmarks
(advanced)
```sh
fio --size=100m \
	--ioengine=libaio \
	--invalidate=1 \
	--direct=1 \
	--numjobs=10 \
	--rw=write \
	--name=fiojob \
	--blocksize_range=4K-512k \
	--iodepth=1
```

Note: Here is a more advanced *destructive* device benchmark to run on
your OSD. Don't do this on a device already in use as an OSD. 100MB in
sequential write, with variable block sizes, 10 times in a row.


<iframe src="https://asciinema.org/api/asciicasts/13105?size=medium&amp;theme=solarized-light&amp;speed=3" id="asciicast-iframe-13105" name="asciicast-iframe-13105" scrolling="yes"></iframe>

Note: `fio` throughput tests against journal (`journal`)
and a file in the filestore (`test.bin`).


## Network benchmarks
```sh
netperf -t TCP_STREAM -H <host>
```


## OSD benchmark
```sh
ceph tell osd.X bench
```


<iframe src="https://asciinema.org/api/asciicasts/13106?size=medium&amp;theme=solarized-light&amp;speed=3" id="asciicast-iframe-13106" name="asciicast-iframe-13106" scrolling="yes"></iframe>

Note: `ceph osd tell bench` producing overall write throughput of
approx. 300 MB/s per OSD.


## rados benchmark
```sh
rados bench -p bench 30 write
```
Do this on a throwaway pool!


<iframe src="https://asciinema.org/api/asciicasts/13107?size=medium&amp;theme=solarized-light&amp;speed=3" id="asciicast-iframe-13107" name="asciicast-iframe-13107" scrolling="yes"></iframe>

Note: `rados bench` producing RADOS throughput of about 1 GB/s.


## fio RBD benchmarks
```sh
fio --size=10G \
	--ioengine=rbd \
	--invalidate=0 \
	--direct=1 \
	--numjobs=10 \
	--rw=write \
	--name=fiojob \
	--blocksize_range=4K-512k \
	--iodepth=1 \
	--pool=bench \
	--rbdname=fio-test
```


<iframe src="https://asciinema.org/api/asciicasts/13119?size=medium&amp;theme=solarized-light&amp;speed=2" id="asciicast-iframe-13119" name="asciicast-iframe-13119" scrolling="yes"></iframe>

Note: `fio` producing RBD throughput of about 800 MB/s.


## Mind the cache!


<iframe src="https://asciinema.org/api/asciicasts/13118?size=medium&amp;theme=solarized-light&amp;speed=2" id="asciicast-iframe-13118" name="asciicast-iframe-13118" scrolling="yes"></iframe>

Note: `fio` producing RBD throughput of about 1.1 GB/s with cache (and
flushes enabled).
