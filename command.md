# SNMPツール

## 参考
https://github.com/etingof/pysnmp
https://github.com/etingof/snmpsim


## install
~~~ shell
python -m pip install pysnmp
python -m pip install snmpclitools
python -m pip install snmpsim
~~~ 

## SNMP Simulator (Server側)

~~~ log
> python .\snmpsimd.py --help
> python .\snmpsimd.py --agent-udpv4-endpoint=127.0.0.1:8080 --data-dir=./data --v2c-arch
~~~ 

### 設定ファイル

- ./data/public.snmprec
~~~ log
1.3.6.1.2.1.1.1.0|4|Linux 2.6.25.5-smp SMP Tue Jun 19 14:58:11 CDT 2007 i686
1.3.6.1.2.1.1.2.0|6|1.3.6.1.4.1.8072.3.2.10
1.3.6.1.2.1.1.3.0|67|233425120
1.3.6.1.2.1.1.4.0|2|100
1.3.6.1.2.1.2.2.1.6.2|4x|00127962f940
1.3.6.1.2.1.4.22.1.3.2.192.21.54.7|64x|c3dafe61
~~~ 

| code | データ型          | 備考 |
| ---: | ----------------- | ---- |
|   01 | boolean           |      |
|   02 | integer           |      |
|   03 | bit string        |      |
|   04 | octet string      |      |
|   05 | null              |      |
|   06 | object identifier |      |
|   40 | IP address        |      |
|   41 | counter           |      |


## snmp tools  (client側)

### SNMPv2 get

~~~ log
> python .\snmpget.py -v2c -c public -On 127.0.0.1:8080 1.3.6.1.2.1.1.1.0
1.3.6.1.2.1.1.1.0 = DisplayString: Linux 2.6.25.5-smp SMP Tue Jun 19 14:58:11 CDT 2007 i686 
~~~

~~~ log
> python .\snmpget.py -v2c -c public -On 127.0.0.1:8080 1.3.6.1.2.1.4.22.1.3.2.192.21.54.7
1.3.6.1.2.1.4.22.1.3.2.192.21.54.7 = IpAddress: 195.218.254.97
~~~

### SNMPv2 walk


~~~ log
> python .\snmpwalk.py -v2c -c public -On 127.0.0.1:8080 1.3.6.1.2
1.3.6.1.2.1.1.1.0 = DisplayString: Linux 2.6.25.5-smp SMP Tue Jun 19 14:58:11 CDT 2007 i686 
1.3.6.1.2.1.1.2.0 = ObjectIdentifier: iso.org.dod.internet.private.enterprises.8072.3.2.10 
1.3.6.1.2.1.1.3.0 = TimeTicks: 27 days 0:24:11.20
1.3.6.1.2.1.2.2.1.6.2 = OctetString: 0x00127962f940
1.3.6.1.2.1.4.22.1.3.2.192.21.54.7 = IpAddress: 195.218.254.97
1.3.6.1.2.1.4.22.1.3.2.192.21.54.7 = No more variables left in this MIB View
~~~ 


### SNMPv2 set

~~~ log
> python .\snmpset.py -v2c -c public -On 127.0.0.1:8080 1.3.6.1.2.1.1.1.0 s Test01
1.3.6.1.2.1.1.1.0 = No Such Instance currently exists at this OID
~~~

