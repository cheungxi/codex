## Sandbox & approvals

For information about Codex sandboxing and approvals, see [this documentation](https://developers.openai.com/codex/security).

## Architecture-specific limitations

### LoongArch64

On LoongArch64 Linux systems, there are some temporary limitations due to the current state of the seccomp ecosystem:

- **Network sandboxing**: The seccomp-based network filtering is not yet available on LoongArch64 because the `seccompiler` crate (v0.5.0) does not support this architecture. Network sandboxing relies on Landlock for filesystem restrictions, which is available, but the network-level filtering via seccomp is currently disabled.
- **Impact**: When running sandboxed commands on LoongArch64, network access restrictions may not be fully enforced at the syscall level. Users should be aware of this limitation when running untrusted code.
- **Future**: This limitation will be resolved when the `seccompiler` crate adds LoongArch64 support or when an alternative implementation is provided.

### Other architectures

All other supported architectures (x86_64, aarch64, riscv64) have full sandbox support including both filesystem (Landlock) and network (seccomp) restrictions.
