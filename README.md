# devirtz-kernel

Linux KVM/AMD SVM research modifications for studying the CPU behavior visible to a Windows guest under QEMU/KVM.

This repository contains an imported Linux kernel tree and subsequent changes to KVM. It is a full source snapshot, not a standalone kernel written from scratch.

## Version and history

- The root `Makefile` identifies Linux **7.0.3**.
- Imported base: [`3067a3c`](https://github.com/meowdiocre/devirtz-kernel/commit/3067a3cf541fb387a7007a034a5ab628580f2d5e), titled `Linux 7.0.3`, May 2, 2026.
- Last functional source change in this snapshot: [`7729c6b`](https://github.com/meowdiocre/devirtz-kernel/commit/7729c6b909e501e7f7fbb5843a0212f07981a8d3), May 4, 2026.
- [Changes after the imported base](https://github.com/meowdiocre/devirtz-kernel/compare/3067a3cf541fb387a7007a034a5ab628580f2d5e...7729c6b909e501e7f7fbb5843a0212f07981a8d3).

The imported commit is the baseline recorded here. An exact match to an upstream signed release has not been established in these notes.

## Research changes

The post-import source commits touch these areas:

| File | Area |
|---|---|
| `arch/x86/kvm/cpuid.c` | Guest CPUID policy |
| `arch/x86/kvm/svm/svm.c` | AMD instruction and MSR intercept handling |
| `arch/x86/kvm/x86.c` | MSR, P-state/CPPC, and hypercall behavior |
| `arch/x86/kvm/mtrr.c` | MTRR validation |

Several commits revise earlier behavior. Use the final tree and comparison above when assessing the changes, rather than treating every historical commit message as current behavior.

## Build notes

Build on a Linux host with the toolchain and dependencies described in [the kernel build requirements](Documentation/process/changes.rst). Start with a configuration appropriate to your host. For example, from the repository root with an existing `.config`:

```sh
make olddefconfig
make -j"$(nproc)"
```

AMD SVM/KVM support must be enabled in that configuration. Installation and bootloader steps depend on the host distribution. Keep a known-working kernel available for recovery when testing this research tree.

No new build or runtime validation is claimed by these notes.

## Recorded results and limits

The repository includes historical screenshots labeled VMAware and VGK. The accompanying host CPU, distribution, QEMU/firmware versions, guest Windows build, and detector versions were not recorded in the original README. Treat them as examples from a particular setup, not a general compatibility or detection guarantee.

![Historical VMAware result](image.png)
![Historical VGK result](image-1.png)

Before comparing new results, record the exact source revision, kernel configuration, host CPU, virtualization stack, guest build, and detector version. Changes to guest-visible CPU behavior may affect guest correctness and compatibility.

## Related work

[vmw](https://github.com/meowdiocre/vmw) contains broader KVM/Windows workspace automation and separate patch sets. The repositories overlap in research area; this README does not claim that vmw contains every change from this snapshot.

## Attribution and license

The Linux kernel is the upstream foundation. Preserve its authorship and licensing information in [COPYING](COPYING), [CREDITS](CREDITS), and [LICENSES](LICENSES/), together with per-file SPDX identifiers.
