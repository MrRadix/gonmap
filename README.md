<!-- Code generated by gomarkdoc. DO NOT EDIT -->

# gonmap

```go
import "github.com/MrRadix/gonmap"
```

### Package gonmap provides an efficient API to interface go programs with nmap binary

For every scan it's necessary define a scan with:

```
scan := NewInitScan()
```

and populate it with related functions or directly with:

```
scan, err := NewScan([]string{"host1", "host2", ...}, []int{port1, port2, ...}, performance, vesionScan)
```

A simple main example:

```
package main

import (
	"log"
	"fmt"

	gonmap "github.com/MrRadix/gonmap"
)

func main() {
	scan := gonmap.NewInitScan()

	if err := scan.AddHost("github.com"); err != nil {
		log.Fatal(err)
	}

	if err := scan.AddPort(80); err != nil {
		log.Fatal(err)
	}

	ret, err := scan.TCPScan()
	if err != nil {
		log.Fatal(err)
	}

	fmt.Println(ret)
}
```

## Index

- [func IsHost(h string) bool](<#func-ishost>)
- [type Address](<#type-address>)
- [type Host](<#type-host>)
- [type HostStatus](<#type-hoststatus>)
- [type NmapRun](<#type-nmaprun>)
- [type OsInfo](<#type-osinfo>)
- [type OsMatch](<#type-osmatch>)
- [type Port](<#type-port>)
- [type PortInfo](<#type-portinfo>)
- [type PortState](<#type-portstate>)
- [type Scan](<#type-scan>)
  - [func NewInitScan() Scan](<#func-newinitscan>)
  - [func NewScan(hosts []string, ports []int, performance int, versionScan bool, osDetection bool) (Scan, error)](<#func-newscan>)
  - [func (s Scan) ACKScan() (NmapRun, error)](<#func-scan-ackscan>)
  - [func (s *Scan) AddHost(h string) error](<#func-scan-addhost>)
  - [func (s *Scan) AddHosts(hosts []string) error](<#func-scan-addhosts>)
  - [func (s *Scan) AddPort(p int) error](<#func-scan-addport>)
  - [func (s *Scan) AddPortRange(min int, max int) error](<#func-scan-addportrange>)
  - [func (s *Scan) AddPorts(ports []int) error](<#func-scan-addports>)
  - [func (s Scan) FINScan() (NmapRun, error)](<#func-scan-finscan>)
  - [func (s Scan) GetHosts() []string](<#func-scan-gethosts>)
  - [func (s *Scan) GetOsDetection() bool](<#func-scan-getosdetection>)
  - [func (s Scan) GetPerformance() int](<#func-scan-getperformance>)
  - [func (s Scan) GetPorts() []int](<#func-scan-getports>)
  - [func (s Scan) HasHost(h string) bool](<#func-scan-hashost>)
  - [func (s Scan) HasPort(p int) bool](<#func-scan-hasport>)
  - [func (s Scan) IDLEScan(zombie string) (NmapRun, error)](<#func-scan-idlescan>)
  - [func (s Scan) IsEqual(s1 Scan) bool](<#func-scan-isequal>)
  - [func (s Scan) MaimonScan() (NmapRun, error)](<#func-scan-maimonscan>)
  - [func (s Scan) NULLScan() (NmapRun, error)](<#func-scan-nullscan>)
  - [func (s Scan) SYNScan() (NmapRun, error)](<#func-scan-synscan>)
  - [func (s *Scan) SetOsDetection(choise bool)](<#func-scan-setosdetection>)
  - [func (s *Scan) SetPerformance(performance int) error](<#func-scan-setperformance>)
  - [func (s *Scan) SetVersionScan(choise bool)](<#func-scan-setversionscan>)
  - [func (s Scan) String() string](<#func-scan-string>)
  - [func (s Scan) TCPScan() (NmapRun, error)](<#func-scan-tcpscan>)
  - [func (s Scan) UDPScan() (NmapRun, error)](<#func-scan-udpscan>)
  - [func (s Scan) WindowScan() (NmapRun, error)](<#func-scan-windowscan>)
  - [func (s Scan) XmasScan() (NmapRun, error)](<#func-scan-xmasscan>)
- [type ScanInfo](<#type-scaninfo>)
- [type Service](<#type-service>)


## func [IsHost](<https://github.com/MrRadix/gonmap/blob/master/aux.go#L10>)

```go
func IsHost(h string) bool
```

IsHost gets a string and returns true if string represents a host false otherwise

## type [Address](<https://github.com/MrRadix/gonmap/blob/master/parser.go#L34-L37>)

Address contains info about address \(ipv4\, ipv6\)

```go
type Address struct {
    Addr string `xml:"addr,attr" json:"addr"`
    Type string `xml:"addrtype,attr" json:"type"`
}
```

## type [Host](<https://github.com/MrRadix/gonmap/blob/master/parser.go#L20-L25>)

Host contains all info about a specific host

```go
type Host struct {
    Status   HostStatus `xml:"status" json:"status"`
    Address  Address    `xml:"address" json:"address"`
    PortList Port       `xml:"ports" json:"ports"`
    OsInfo   OsInfo     `xml:"os" json:"osinfo"`
}
```

## type [HostStatus](<https://github.com/MrRadix/gonmap/blob/master/parser.go#L28-L31>)

HostStatus contains status of specific host

```go
type HostStatus struct {
    State  string `xml:"state,attr" json:"state"`
    Reason string `xml:"reason,attr" json:"reason"`
}
```

## type [NmapRun](<https://github.com/MrRadix/gonmap/blob/master/parser.go#L8-L11>)

NmapRun is the root of every scan result

```go
type NmapRun struct {
    Info  ScanInfo `xml:"scaninfo" json:"scaninfo"`
    Hosts []Host   `xml:"host" json:"hosts"`
}
```

## type [OsInfo](<https://github.com/MrRadix/gonmap/blob/master/parser.go#L65-L67>)

OsInfo contains all os detection matches

```go
type OsInfo struct {
    OsMatch []OsMatch `xml:"osmatch" json:"osmatch"`
}
```

## type [OsMatch](<https://github.com/MrRadix/gonmap/blob/master/parser.go#L70-L73>)

OsMatch contains info about an os detection match

```go
type OsMatch struct {
    Name     string `xml:"name,attr" json:"name"`
    Accuracy string `xml:"accuracy,attr" json:"accuracy"`
}
```

## type [Port](<https://github.com/MrRadix/gonmap/blob/master/parser.go#L40-L42>)

Port contains all port checked in scan

```go
type Port struct {
    Port []PortInfo `xml:"port" json:"ports"`
}
```

## type [PortInfo](<https://github.com/MrRadix/gonmap/blob/master/parser.go#L45-L50>)

PortInfo contains info about a specific port

```go
type PortInfo struct {
    ID       int       `xml:"portid,attr" json:"id"`
    Protocol string    `xml:"protocol,attr" json:"protocol"`
    Status   PortState `xml:"state" json:"status"`
    Service  Service   `xml:"service" json:"service"`
}
```

## type [PortState](<https://github.com/MrRadix/gonmap/blob/master/parser.go#L53-L56>)

PortState contains status of specific port

```go
type PortState struct {
    State  string `xml:"state,attr" json:"state"`
    Reason string `xml:"reason,attr" json:"reason"`
}
```

## type [Scan](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L12-L18>)

Scan contains basic scan information like hosts\, ports\, performance of scan and a flag for service version scan\. Is the base for every scan type

```go
type Scan struct {
    // contains filtered or unexported fields
}
```

### func [NewInitScan](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L21>)

```go
func NewInitScan() Scan
```

NewInitScan returns a new Scan with default values

### func [NewScan](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L33>)

```go
func NewScan(hosts []string, ports []int, performance int, versionScan bool, osDetection bool) (Scan, error)
```

NewScan return a new Scan with given settings if they are valid and returns error otherwise

### func \(Scan\) [ACKScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L174>)

```go
func (s Scan) ACKScan() (NmapRun, error)
```

ACKScan are used to determine whether a particular port is filtered or not\. Flag: \-sA

### func \(\*Scan\) [AddHost](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L105>)

```go
func (s *Scan) AddHost(h string) error
```

AddHost adds host h to Scan s if it's a valid host and returns error otherwise

### func \(\*Scan\) [AddHosts](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L125>)

```go
func (s *Scan) AddHosts(hosts []string) error
```

AddHosts adds hosts slice to Scan if all hosts are valid and returns error otherwise

### func \(\*Scan\) [AddPort](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L148>)

```go
func (s *Scan) AddPort(p int) error
```

AddPort adds port p to Scan s if p is a valid port and returns error otherwise

### func \(\*Scan\) [AddPortRange](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L162>)

```go
func (s *Scan) AddPortRange(min int, max int) error
```

AddPortRange adds ports from min to max if min and max are valid bounds and returns error otherwise

### func \(\*Scan\) [AddPorts](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L187>)

```go
func (s *Scan) AddPorts(ports []int) error
```

AddPorts adds ports in ports slice to Scan s if all ports are valid and returns error otherwise

### func \(Scan\) [FINScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L188>)

```go
func (s Scan) FINScan() (NmapRun, error)
```

FINScan is like SYN scan\, but sends a TCP FIN packet instead\. Flag: \-sF

### func \(Scan\) [GetHosts](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L229>)

```go
func (s Scan) GetHosts() []string
```

GetHosts returns hosts set

### func \(\*Scan\) [GetOsDetection](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L250>)

```go
func (s *Scan) GetOsDetection() bool
```

GetOsDetection returns os detection choise

### func \(Scan\) [GetPerformance](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L245>)

```go
func (s Scan) GetPerformance() int
```

GetPerformance returns performance

### func \(Scan\) [GetPorts](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L237>)

```go
func (s Scan) GetPorts() []int
```

GetPorts returns ports set

### func \(Scan\) [HasHost](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L88>)

```go
func (s Scan) HasHost(h string) bool
```

HasHost checks if Scan s has host h

### func \(Scan\) [HasPort](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L77>)

```go
func (s Scan) HasPort(p int) bool
```

HasPort checks if Scan s has port p

### func \(Scan\) [IDLEScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L263>)

```go
func (s Scan) IDLEScan(zombie string) (NmapRun, error)
```

IDLEScan is the stealthiest of all scans as the packets are bounced off an external host\. Flag: \-sI

### func \(Scan\) [IsEqual](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L259>)

```go
func (s Scan) IsEqual(s1 Scan) bool
```

IsEqual cheks if two scans are equal

### func \(Scan\) [MaimonScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L248>)

```go
func (s Scan) MaimonScan() (NmapRun, error)
```

MaimonScan is exactly the same as NULL\, FIN\, and Xmas scan\, except that the probe is FIN/ACK\. Flag: \-sM

### func \(Scan\) [NULLScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L203>)

```go
func (s Scan) NULLScan() (NmapRun, error)
```

NULLScan are extremely stealthy scan and what they do is as the name suggests — they set all the header fields to null\. Flag: \-sN

### func \(Scan\) [SYNScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L159>)

```go
func (s Scan) SYNScan() (NmapRun, error)
```

SYNScan is another form of TCP scan\. The difference is unlike a normal TCP scan\, nmap itself crafts a syn packet\, which is the first packet that is sent to establish a TCP connection\. Flag: \-sS

### func \(\*Scan\) [SetOsDetection](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L224>)

```go
func (s *Scan) SetOsDetection(choise bool)
```

SetOsDetection sets operative system detection flag if choise is true\. Nmap flag: \-O

### func \(\*Scan\) [SetPerformance](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L209>)

```go
func (s *Scan) SetPerformance(performance int) error
```

SetPerformance sets scan performance if performance parameter is an integer between 0 and 5

### func \(\*Scan\) [SetVersionScan](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L219>)

```go
func (s *Scan) SetVersionScan(choise bool)
```

SetVersionScan sets service version scan\. Nmap flag: \-sV

### func \(Scan\) [String](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L254>)

```go
func (s Scan) String() string
```

### func \(Scan\) [TCPScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L128>)

```go
func (s Scan) TCPScan() (NmapRun, error)
```

TCPScan is generally used to check and complete a three\-way handshake between you and a chosen target system\. Flag: \-sT

### func \(Scan\) [UDPScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L144>)

```go
func (s Scan) UDPScan() (NmapRun, error)
```

UDPScan are used to check whether there is any UDP port up and listening for incoming requests on the target machine\. Flag: \-sU

### func \(Scan\) [WindowScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L233>)

```go
func (s Scan) WindowScan() (NmapRun, error)
```

WindowScan is exactly the same as ACK scan except that it exploits an implementation detail of certain systems to differentiate open ports from closed ones\, rather than always printing unfiltered when a RST is returned\. Flag: \-sW

### func \(Scan\) [XmasScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L217>)

```go
func (s Scan) XmasScan() (NmapRun, error)
```

XmasScan is just like null scans\, these are also stealthy in nature\. Flag \-sX

## type [ScanInfo](<https://github.com/MrRadix/gonmap/blob/master/parser.go#L14-L17>)

ScanInfo contains info about the scan

```go
type ScanInfo struct {
    Type     string `xml:"type,attr" json:"type"`
    Protocol string `xml:"protocol,attr" json:"protocol"`
}
```

## type [Service](<https://github.com/MrRadix/gonmap/blob/master/parser.go#L59-L62>)

Service contains info about service served in a specific port

```go
type Service struct {
    Name    string `xml:"name,attr" json:"name"`
    Version string `xml:"product,attr" json:"version"`
}
```



Generated by [gomarkdoc](<https://github.com/princjef/gomarkdoc>)
