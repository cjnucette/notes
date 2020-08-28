# tcpdump

tcpdump is packet capture tool used to troubleshoot network connectivity issues.

## Find network interfaces
`tcpdump -D`: lists all available interfaces.

## Specify which interface to listen on
`tcpdump -i <interface>`: starts to listen on the given <interface> until an interrupt signal is given via `ctrl-c`.
### Use the `-c` option to limit the number of packets to be captured.
`tcpdump -i any -c 3`: listens to all the interfaces and captures only 3 packets.
### Use the `-nn` option to disable name and port resolution.
`tcpdump -i any -c 3 -nn`: Shows host and port numbers instead of their names.

## Pre-capture filters
### Filter by ip
`tcpdump host x.x.x.x`: Shows packets from and to the specified ip address.

### Filter by <interface>
`tcpdump eth0`: Shows packets from and to the specified interface.

### Filter by source
`tcpdump src x.x.x.x`: Shows packets from the specified the ip address.

### Filter by destination
`tcpdump dst x.x.x.x`: Shows packets to the specified the ip address.

### Filter by <protocol>
`tcpdump icmp`: Shows packets using the specified <protocol>.

## Writing captures to a file (pcap)
`tcpdump` has an output file format that captures all of the data we see. This format is called a _packet capture file_, aka PCAP, and is used across various utilities, including network analyzers and `tcpdump`.
### To write a pcap file using option `-w <filename>`.
`tcpdump -i enp0s8 -c100 -nn -w output_file`: writes a pcap file to output_file.
### To read from a pcap file using option `-r <filename>`.
`tcpdump -r output_file`: reads the given file.
### To write to a .txt file
`tcpdump -i enp0s8 -c100 -nn > output.txt`: write output to a text file.
