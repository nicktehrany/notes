# My 5.19 Kernel configs

Just copy these configs to the kernel root dir as `.config` and modify as needed `make menuconfig`.

**ALWAYS COPY THE FILES. DO NOT DIRECTLY MODIFY THEM PLEASE**

- .config-f2fs_multi_stream - debug config with all debug symbols (kasan, lock tracer, etc.) only for debuggin
- .config-default - clean config for installing kernels
- .config-default_with_debug - default config with some debugging support (lock profiling stats in /proc/lock_stat)

If there are compile issues about certificates, run these commands, which disable the options and on compile hit enter to select the default when prompted again for these options:

```bash
scripts/config --disable SYSTEM_TRUSTED_KEYS
scripts/config --disable SYSTEM_REVOCATION_KEYS
```

## Building Kernel and Installing

Build:

```bash
make -j4 bindeb-pkg LOCALVERSION=-stosys
```

Copy to a VM or wherever you want to install and remove the `-dbg` image, if there is one.

```bash
scp -P 8888 *.deb user@localhost:~/src/f2fs-build-debs/
rm  linux-image-5.19.0-f2fs-multi-stream-dbg_5.19.0-f2fs-multi-stream-185_amd64.deb
sudo dpkg -i *.deb
```
