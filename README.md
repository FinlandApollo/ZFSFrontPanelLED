# ZFSFrontPanelLED

# -v gives us individual drive statistics, 0.5 gives us 500ms delay in iterations
zpool iostat -v 0.5

# Output form: 

                                   capacity     operations     bandwidth
pool                             alloc   free   read  write   read  write
-------------------------------  -----  -----  -----  -----  -----  -----
ZFSPool                          24.7T  4.29T    260     81  17.2M  2.17M
  raidz2                         24.7T  4.29T    260     81  17.2M  2.16M
    pci-0000:00:11.4-ata-1           -      -     33     10  2.15M   277K
    pci-0000:00:11.4-ata-2           -      -     31      9  2.16M   277K
    pci-0000:00:11.4-ata-3           -      -     34     10  2.15M   277K
    pci-0000:00:11.4-ata-4           -      -     29      9  2.15M   277K
    pci-0000:00:1f.2-ata-1           -      -     35     10  2.15M   277K
    pci-0000:00:1f.2-ata-2           -      -     30     10  2.16M   277K
    pci-0000:00:1f.2-ata-3           -      -     30     10  2.16M   277K
    pci-0000:00:1f.2-ata-4           -      -     35     10  2.15M   277K
-------------------------------  -----  -----  -----  -----  -----  -----


# this removes all the excess data, columns and names
zpool iostat -v 0.5 | awk -F' ' '/-ata-/{ print "Z",$1,$4,$5}'

# Output form from this (it includes only pci-name and operation's read and write:

pci-0000:00:11.4-ata-1 33 10
pci-0000:00:11.4-ata-2 31 9
pci-0000:00:11.4-ata-3 34 10
pci-0000:00:11.4-ata-4 29 9
pci-0000:00:1f.2-ata-1 35 10
pci-0000:00:1f.2-ata-2 30 10
pci-0000:00:1f.2-ata-3 30 10
pci-0000:00:1f.2-ata-4 35 10



