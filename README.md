pcm.sh
======

`pcm.sh` simply set up a PCM device on stdout and forwards stdin to stdout
by calling `cat`. If stdout is not a PCM device it still forwards the data.

The following example outputs input_file to PCM device Card 0 Device 0:

	cat input_file | pcm.sh > /dev/snd/pcmC0D0

The default parameters are 16-bit sample resolution, 2 samples per frame
(i.e. channels), 44100 frames per second (i.e. rate).

ioctl
=====

There is no standard method for calling ioctl() system call from a shell
script. `ioctl.c` is essentially a wrapper for the system call.

Compile it using:

	gcc -Wall -o ioctl ioctl.c

It should not display any warnings or errors.

For how to use ioctl, see `ioctl.c`. It's very small.

Notes of the implementation:

When read flag is defined after size parameter, the buffer is written to
stderr after being processed by ioctl regardless of the return value. The
buffer is the same filled with data from stdin if write flag is set.

If `ioctl()` fails its error number (errno) is returned as the exit status
of the program. If ioctl return positive value, there is no straightforward
way to know whether the return value corresponds to an error.
