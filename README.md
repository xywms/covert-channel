自己做了一些代码调试，增加了计算slice号的函数
以下是0x161e-swei/covert-channel-101的README.md内容
# Implementation of a LLC Prime+Probe and a Flush+Reload covert-channels

This is one possible Implementation of LLC Prime+Probe and Flush+Reload
covert-channels.

This implementation is tested and currently works on
- an aws i3-metal machine
- an aws m4.xlarge dedicated instance
- a local i7 Haswell (4c/8t) desktop

## To compile the code run  
`make clean; make`


## Configuring the covert-channel
This implementation supports configuring the channel through command line
options.  
For both prime+probe and flush+reload use  
`-i` to specify a time interval for each bit transmitted.  
`-r` to specify a cache set to communicate on.  
`-a` to specify cycles spent for sender to access the cache.

For prime+probe use:
`-p` to specify cycles spent for receiver to prime the cache.  
`-b` to compute the channel bandwidth given one configuration.

For flush+reload use:
`-f` to specify a shared file to use (should not be an empty file).

## Running the covert-channel
To run, first setup pre-allocated huge pages
and (recommended) disable hyper-threading by running:  
`./setup.sh`

To run sender and receiver in a chat mode:
```sh
taskset -c X ./sender
taskset -c X ./receiver
```
where `X` is supposed to limit sender and receiver onto the same socket.

To evaluate channel bandwidth with different configurations run:
```sh
./benchmark.py
```

## Acknowledgement
This implementation merges efforts from [a shared-memory, Flush+Reload Covert
Channel](https://github.com/moehajj/Flush-Reload) by Mohamad Hajj. And it's all
developed from on [this github repo](https://github.com/ricpacca/deaddrop) (or
tracked in branch `fork_base`).

