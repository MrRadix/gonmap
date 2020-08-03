<!-- Code generated by gomarkdoc. DO NOT EDIT -->

# gonmap

```go
import "github.com/MrRadix/gonmap"
```

### Package gonmap provides an efficient and simple API for nmap

For every scan it's necessary create a scan with:

```
scan := NewScan()
```

and populate it with related functions\.

A simple main example:

```
package main

import (
	"log"
	"fmt"

	gonmap "github.com/MrRadix/gonmap"
)

func main() {
	scan := gonmap.NewScan()

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

	fmt.Println(out.Hosts[0].PortList.Port[0].ID)
}
```

## Index

- [func IsValidHost(h string) bool](<#func-isvalidhost>)
- [type Address](<#type-address>)
- [type Elem](<#type-elem>)
- [type Host](<#type-host>)
- [type HostDiscovery](<#type-hostdiscovery>)
- [type HostStatus](<#type-hoststatus>)
- [type NmapRun](<#type-nmaprun>)
- [type OsInfo](<#type-osinfo>)
- [type OsMatch](<#type-osmatch>)
- [type Port](<#type-port>)
- [type PortInfo](<#type-portinfo>)
- [type PortState](<#type-portstate>)
- [type Scan](<#type-scan>)
  - [func NewScan() Scan](<#func-newscan>)
  - [func (s Scan) ACKDiscovery() (NmapRun, error)](<#func-scan-ackdiscovery>)
  - [func (s Scan) ACKScan() (NmapRun, error)](<#func-scan-ackscan>)
  - [func (s *Scan) AddHost(h string) error](<#func-scan-addhost>)
  - [func (s *Scan) AddHosts(hosts []string) error](<#func-scan-addhosts>)
  - [func (s *Scan) AddPort(p int) error](<#func-scan-addport>)
  - [func (s *Scan) AddPortRange(min int, max int) error](<#func-scan-addportrange>)
  - [func (s *Scan) AddPorts(ports []int) error](<#func-scan-addports>)
  - [func (s *Scan) AddScript(script string) error](<#func-scan-addscript>)
  - [func (s *Scan) AddScripts(scripts []string) error](<#func-scan-addscripts>)
  - [func (s Scan) AggressiveScan() (NmapRun, error)](<#func-scan-aggressivescan>)
  - [func (s Scan) FINScan() (NmapRun, error)](<#func-scan-finscan>)
  - [func (s Scan) GetHosts() []string](<#func-scan-gethosts>)
  - [func (s Scan) GetOsDetection() bool](<#func-scan-getosdetection>)
  - [func (s Scan) GetPerformance() int](<#func-scan-getperformance>)
  - [func (s Scan) GetPorts() []int](<#func-scan-getports>)
  - [func (s Scan) GetRunScript() bool](<#func-scan-getrunscript>)
  - [func (s Scan) GetScripts() []string](<#func-scan-getscripts>)
  - [func (s Scan) HasHost(h string) bool](<#func-scan-hashost>)
  - [func (s Scan) HasPort(p int) bool](<#func-scan-hasport>)
  - [func (s Scan) HasScript(script string) bool](<#func-scan-hasscript>)
  - [func (s Scan) IDLEScan(zombie string) (NmapRun, error)](<#func-scan-idlescan>)
  - [func (s Scan) IsEqual(s1 Scan) bool](<#func-scan-isequal>)
  - [func (s Scan) MaimonScan() (NmapRun, error)](<#func-scan-maimonscan>)
  - [func (s Scan) NULLScan() (NmapRun, error)](<#func-scan-nullscan>)
  - [func (s *Scan) RunScripts(choise bool)](<#func-scan-runscripts>)
  - [func (s Scan) SCTPDiscovery() (NmapRun, error)](<#func-scan-sctpdiscovery>)
  - [func (s Scan) SYNDiscovery() (NmapRun, error)](<#func-scan-syndiscovery>)
  - [func (s Scan) SYNScan() (NmapRun, error)](<#func-scan-synscan>)
  - [func (s *Scan) SetOsDetection(choise bool)](<#func-scan-setosdetection>)
  - [func (s *Scan) SetPerformance(performance int) error](<#func-scan-setperformance>)
  - [func (s *Scan) SetVersionScan(choise bool)](<#func-scan-setversionscan>)
  - [func (s Scan) String() string](<#func-scan-string>)
  - [func (s Scan) TCPScan() (NmapRun, error)](<#func-scan-tcpscan>)
  - [func (s Scan) UDPDiscovery() (NmapRun, error)](<#func-scan-udpdiscovery>)
  - [func (s Scan) UDPScan() (NmapRun, error)](<#func-scan-udpscan>)
  - [func (s Scan) WindowScan() (NmapRun, error)](<#func-scan-windowscan>)
  - [func (s Scan) XmasScan() (NmapRun, error)](<#func-scan-xmasscan>)
- [type ScanInfo](<#type-scaninfo>)
- [type ScanTecnique](<#type-scantecnique>)
- [type Script](<#type-script>)
- [type Service](<#type-service>)
- [type Table](<#type-table>)


## func [IsValidHost](<https://github.com/MrRadix/gonmap/blob/master/aux.go#L11>)

```go
func IsValidHost(h string) bool
```

IsValidHost gets a string and returns true if string represents a valid host false otherwise\. Examples of valid hosts: 192\.168\.1\.0\, 192\.0\-100\.0\-3\.8\, 192\.168\.1\.0/24\, 192\.0\-100\.0\-3\.8/19\, www\.google\.com\,github\.com/17

## type [Address](<https://github.com/MrRadix/gonmap/blob/master/parser.go#L34-L37>)

Address contains info about address \(ipv4\, ipv6\)

```go
type Address struct {
    Addr string `xml:"addr,attr" json:"addr"`
    Type string `xml:"addrtype,attr" json:"type"`
}
```

## type [Elem](<https://github.com/MrRadix/gonmap/blob/master/parser.go#L91-L94>)

Elem contains a part of script result

```go
type Elem struct {
    Key   string `xml:"key,attr" json:"key"`
    Value string `xml:",chardata" json:"value"`
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

## type [HostDiscovery](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L27-L32>)

HostDiscovery contains all methods that implement an host discovery scan

```go
type HostDiscovery interface {
    SYNDiscovery()
    ACKDiscovery()
    UDPDiscovery()
    SCTPDiscovery()
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

## type [OsInfo](<https://github.com/MrRadix/gonmap/blob/master/parser.go#L66-L68>)

OsInfo contains all os detection matches

```go
type OsInfo struct {
    OsMatch []OsMatch `xml:"osmatch" json:"osmatch"`
}
```

## type [OsMatch](<https://github.com/MrRadix/gonmap/blob/master/parser.go#L71-L74>)

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

## type [PortInfo](<https://github.com/MrRadix/gonmap/blob/master/parser.go#L45-L51>)

PortInfo contains info about a specific port

```go
type PortInfo struct {
    ID       int       `xml:"portid,attr" json:"id"`
    Protocol string    `xml:"protocol,attr" json:"protocol"`
    Status   PortState `xml:"state" json:"status"`
    Service  Service   `xml:"service" json:"service"`
    Scripts  []Script  `xml:"script" json:"scripts"`
}
```

## type [PortState](<https://github.com/MrRadix/gonmap/blob/master/parser.go#L54-L57>)

PortState contains status of specific port

```go
type PortState struct {
    State  string `xml:"state,attr" json:"state"`
    Reason string `xml:"reason,attr" json:"reason"`
}
```

## type [Scan](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L12-L20>)

Scan contains basic scan information like hosts\, ports\, performance of scan and a flag for service version scan\. Is the base for every scan type

```go
type Scan struct {
    // contains filtered or unexported fields
}
```

### func [NewScan](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L23>)

```go
func NewScan() Scan
```

NewScan returns a new Scan with default values

### func \(Scan\) [ACKDiscovery](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L378>)

```go
func (s Scan) ACKDiscovery() (NmapRun, error)
```

ACKDiscovery makes a TCP ACK discovery

### func \(Scan\) [ACKScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L207>)

```go
func (s Scan) ACKScan() (NmapRun, error)
```

ACKScan are used to determine whether a particular port is filtered or not\. Flag: \-sA

### func \(\*Scan\) [AddHost](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L80>)

```go
func (s *Scan) AddHost(h string) error
```

AddHost adds given host to scan if it's a valid host and returns error otherwise

### func \(\*Scan\) [AddHosts](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L100>)

```go
func (s *Scan) AddHosts(hosts []string) error
```

AddHosts adds all given hosts to scan if all hosts are valid and returns error otherwise

### func \(\*Scan\) [AddPort](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L123>)

```go
func (s *Scan) AddPort(p int) error
```

AddPort adds given port to scan if is a valid port and returns error otherwise

### func \(\*Scan\) [AddPortRange](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L137>)

```go
func (s *Scan) AddPortRange(min int, max int) error
```

AddPortRange adds ports from min to max if min and max are valid bounds and returns error otherwise

### func \(\*Scan\) [AddPorts](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L162>)

```go
func (s *Scan) AddPorts(ports []int) error
```

AddPorts adds all given ports to scan if all ports are valid and returns error otherwise

### func \(\*Scan\) [AddScript](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L204>)

```go
func (s *Scan) AddScript(script string) error
```

AddScript adds given script to scan

### func \(\*Scan\) [AddScripts](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L216>)

```go
func (s *Scan) AddScripts(scripts []string) error
```

AddScripts adds all given scripts to scan

### func \(Scan\) [AggressiveScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L352>)

```go
func (s Scan) AggressiveScan() (NmapRun, error)
```

AggressiveScan makes a scan with version scan \(\-sV\)\, os detection \(\-O\)\, script scanning \(\-sC\) and traceroute

### func \(Scan\) [FINScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L221>)

```go
func (s Scan) FINScan() (NmapRun, error)
```

FINScan is like SYN scan\, but sends a TCP FIN packet instead\. Flag: \-sF

### func \(Scan\) [GetHosts](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L242>)

```go
func (s Scan) GetHosts() []string
```

GetHosts returns hosts set

### func \(Scan\) [GetOsDetection](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L271>)

```go
func (s Scan) GetOsDetection() bool
```

GetOsDetection returns os detection choise

### func \(Scan\) [GetPerformance](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L266>)

```go
func (s Scan) GetPerformance() int
```

GetPerformance returns performance

### func \(Scan\) [GetPorts](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L250>)

```go
func (s Scan) GetPorts() []int
```

GetPorts returns ports set

### func \(Scan\) [GetRunScript](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L276>)

```go
func (s Scan) GetRunScript() bool
```

GetRunScript returns script running choise

### func \(Scan\) [GetScripts](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L258>)

```go
func (s Scan) GetScripts() []string
```

GetScripts returns scripts set

### func \(Scan\) [HasHost](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L47>)

```go
func (s Scan) HasHost(h string) bool
```

HasHost checks if scan has given host

### func \(Scan\) [HasPort](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L36>)

```go
func (s Scan) HasPort(p int) bool
```

HasPort checks if scan has given port

### func \(Scan\) [HasScript](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L63>)

```go
func (s Scan) HasScript(script string) bool
```

HasScript checks if scan has given script

### func \(Scan\) [IDLEScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L296>)

```go
func (s Scan) IDLEScan(zombie string) (NmapRun, error)
```

IDLEScan is the stealthiest of all scans as the packets are bounced off an external host\. Flag: \-sI

### func \(Scan\) [IsEqual](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L285>)

```go
func (s Scan) IsEqual(s1 Scan) bool
```

IsEqual cheks if two scans are equal

### func \(Scan\) [MaimonScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L281>)

```go
func (s Scan) MaimonScan() (NmapRun, error)
```

MaimonScan is exactly the same as NULL\, FIN\, and Xmas scan\, except that the probe is FIN/ACK\. Flag: \-sM

### func \(Scan\) [NULLScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L236>)

```go
func (s Scan) NULLScan() (NmapRun, error)
```

NULLScan are extremely stealthy scan and what they do is as the name suggests — they set all the header fields to null\. Flag: \-sN

### func \(\*Scan\) [RunScripts](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L237>)

```go
func (s *Scan) RunScripts(choise bool)
```

RunScripts sets scripts running if choise is true\. Setting this true without adding scripts it's equivalent to a scan with default scripts\. Flag: \-sC

### func \(Scan\) [SCTPDiscovery](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L404>)

```go
func (s Scan) SCTPDiscovery() (NmapRun, error)
```

SCTPDiscovery makes an SCTP discovery

### func \(Scan\) [SYNDiscovery](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L365>)

```go
func (s Scan) SYNDiscovery() (NmapRun, error)
```

SYNDiscovery makes a TCP SYN discovery

### func \(Scan\) [SYNScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L192>)

```go
func (s Scan) SYNScan() (NmapRun, error)
```

SYNScan is another form of TCP scan\. The difference is unlike a normal TCP scan\, nmap itself crafts a syn packet\, which is the first packet that is sent to establish a TCP connection\. Flag: \-sS

### func \(\*Scan\) [SetOsDetection](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L199>)

```go
func (s *Scan) SetOsDetection(choise bool)
```

SetOsDetection sets operative system detection flag if choise is true\. Nmap flag: \-O

### func \(\*Scan\) [SetPerformance](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L184>)

```go
func (s *Scan) SetPerformance(performance int) error
```

SetPerformance sets scan performance if performance parameter is an integer between 0 and 5

### func \(\*Scan\) [SetVersionScan](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L194>)

```go
func (s *Scan) SetVersionScan(choise bool)
```

SetVersionScan sets service version scan\. Nmap flag: \-sV

### func \(Scan\) [String](<https://github.com/MrRadix/gonmap/blob/master/scan.go#L280>)

```go
func (s Scan) String() string
```

### func \(Scan\) [TCPScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L161>)

```go
func (s Scan) TCPScan() (NmapRun, error)
```

TCPScan is generally used to check and complete a three\-way handshake between you and a chosen target system\. Flag: \-sT

### func \(Scan\) [UDPDiscovery](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L391>)

```go
func (s Scan) UDPDiscovery() (NmapRun, error)
```

UDPDiscovery makes an UDP discovery

### func \(Scan\) [UDPScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L177>)

```go
func (s Scan) UDPScan() (NmapRun, error)
```

UDPScan are used to check whether there is any UDP port up and listening for incoming requests on the target machine\. Flag: \-sU

### func \(Scan\) [WindowScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L266>)

```go
func (s Scan) WindowScan() (NmapRun, error)
```

WindowScan is exactly the same as ACK scan except that it exploits an implementation detail of certain systems to differentiate open ports from closed ones\, rather than always printing unfiltered when a RST is returned\. Flag: \-sW

### func \(Scan\) [XmasScan](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L250>)

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

## type [ScanTecnique](<https://github.com/MrRadix/gonmap/blob/master/functions.go#L13-L24>)

ScanTecnique contains all methods that implement a scan tecnique

```go
type ScanTecnique interface {
    TCPScan()
    UDPScan()
    SYNScan()
    ACKScan()
    FINScan()
    NULLScan()
    XmasScan()
    WindowScan()
    MaimonScan()
    IDLEScan()
}
```

## type [Script](<https://github.com/MrRadix/gonmap/blob/master/parser.go#L77-L82>)

Script contains info about a specific script launched against a specific port

```go
type Script struct {
    ID     string  `xml:"id,attr" json:"id"`
    Output string  `xml:"output,attr" json:"output"`
    Elems  []Elem  `xml:"elem" json:"elems"`
    Tables []Table `xml:"table" json:"tables"`
}
```

## type [Service](<https://github.com/MrRadix/gonmap/blob/master/parser.go#L60-L63>)

Service contains info about service served in a specific port

```go
type Service struct {
    Name    string `xml:"name,attr" json:"name"`
    Version string `xml:"product,attr" json:"version"`
}
```

## type [Table](<https://github.com/MrRadix/gonmap/blob/master/parser.go#L85-L88>)

Table contains a group of elems of a specific script

```go
type Table struct {
    Key   string `xml:"key,attr" json:"key"`
    Elems []Elem `xml:"elem" json:"elems"`
}
```



Generated by [gomarkdoc](<https://github.com/princjef/gomarkdoc>)
