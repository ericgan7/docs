vessellookup.repy is designed to give repy programmers an easy way to look up various resources that a vessel/VM has.  These resources include but are not limited to max CPU percentage, max memory usage, allowed ports, etc.



## API
All functions in this module take a single vessellocation as an argument.  A vessellocation is a string that describes where a VM can be found.  It is in the form of ip:port:VMname. Example: 123.45.67.89:1224:v4.  The resources file is retrieved the first time a lookup is performed on a VM.  The data from this initial retrieval is cached so that subsequent calls to are fast.

### lookup_cpu()
Returns the CPU percentage given to the VM, as a float.

### lookup_disk()
Returns the number of bytes of disk space allocated to the VM, as an int.

### lookup_memory()
Returns the number of bytes of memory allocated to the VM, as an int.

### lookup_ports()
Returns the list of ports that this VM is allowed to listen on, as a list of ints.

## Usage Example
First, you need to generate a list of vessellocations through seash and upload this file to the VMs.
```sh
username@ !> on %all show vessellocation to vessellocations.txt
username@ !> on %all upload vessellocations.txt
```

And then in your program file, you can pass the nodelocations in the file to the lookup functions:
```repy
vessel_comm_port = {}
vessel_result_port = {}

max_disk_space = 2 ** 32 # Assume 4GB, actual allowed disk space is less
vessellocations = open('vessellocations.txt', 'r').read()

for vessel in vessellocations:
  # This is the first time we contacted this vessel/VM, so the results will be
  # cached for future usage.
  vessel_comm_port[vessel] = lookup_ports(vessel)[0]
  # We already have this information so this takes no time at all
  vessel_result_port[vessel] = lookup_ports(vessel)[1]
  if lookup_disk(vessel) < max_disk_space:
    max_disk_space = lookup_disk(vessel)

```