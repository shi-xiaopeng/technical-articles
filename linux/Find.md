```
find [-H] [-L] [-P] [-D debugopts] [-Olevel] [starting-point...] [expression]

find /path option filename
# find by name
find / -name linux.odt
    name - case sensitive
find / -iname linux.odt
    iname - case insensitive

# find by type
    f - regular file
    d - directory
    l - symbolic link
    c - character devices
    b - block devices
find / -type c

find / -type f -name "*.conf"

# Outputting results to a file
find /etc -type f -name “*.conf” > conf_search

# Finding files by size
    c - bytes
    k - Kilobytes
    M - Megabytes
    G - Gigabytes
    b - 512-byte blocks
find / -size +1000MB

```
