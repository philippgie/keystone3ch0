# keystone3ch0

This is a PoC demonstrating that size confusion in `copy_to_user` after OCALLs/syscalls can be abused to leak confidential memory. In general, it is sufficient to have an application that reads a large amount of data and echoes information about that data back to the host. While this PoC simply echoes the complete input, in certain applications receiving less information such as single bits might already leak enough information (e.g., leaking configuration flags).

The same idea can be applied to recvfrom() and getsockname() syscalls, altohugh, the attack is more complicated because we do not control the offset. In this case either the expected data size must be greater, or we can reduce the size of UTM. Furthermore, since these are built statically, the binary size increases drastically, increasing the distance between UTM and eapp stack.

## Flow

Follow normal keystone build instruction and run qemu:

```console
insmod keystone-driver.ko
./hello-native.ke
```

## Expected Output

> [...]
> 0xffffff85647fb0: ?@@Super confidential enclave secre
> 0xffffff85647ff0: t!!!h
