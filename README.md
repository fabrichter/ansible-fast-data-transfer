Ansible role to copy files using [FDT](https://fast-data-transfer.github.io)

>FDT is an Application for Efficient Data Transfers which is capable of reading and writing at disk speed over wide area networks (with standard TCP). It is written in Java, runs an all major platforms and it is easy to use. FDT is based on an asynchronous, flexible multithreaded system and is using the capabilities of the Java NIO libraries.

Requires Java (installed by the role). Tested on Ubuntu 18.04.

Data is *not* encrypted, *no* authentification is done (though access is restricted to the IP address of the source machine).


## Usage

```yaml
# From host to target
- hosts: source
  roles:
    - name: fast-data-transfer
      vars:
        fdt_path: /tmp/foobar.txt # must be a single file
        fdt_dest: /tmp
        fdt_target: target

# From source to host
- hosts: target
  roles:
    - name: fast-data-transfer
      vars:
        fdt_path: /tmp/foobar.txt
        fdt_dest: /tmp
        fdt_source: source
```

## Parameters to tweak

Also see the [FDT documentation](https://fast-data-transfer.github.io/doc-fdt-ddcopy.html)

```yaml
fdt_max_transfer_time: 600 # seconds to wait for transfer (uses asynchronous Ansible actions)
fdt_poll_time: 10 # interval to poll for task status
fdt_io_buffer_size: 64M # IO buffer size on server (-bs option for FDT)
fdt_tcp_buffer_size: 1M # TCP send buffer size (-ss option for FDT)
fdt_tcp_streams: 10 # number of parallel TCP connections (-P option for FDT)
```

## Roadmap

Contributions are welcome!

- [ ] Publish to Ansible Galaxy
- [ ] Checksums
- [ ] Authentification
- [ ] Dropping privileges
- [ ] Copying multiple files (via `-fl`option or Ansible using archive/unarchive)
- [ ] Support more platforms
- [ ] Support more FDT features
