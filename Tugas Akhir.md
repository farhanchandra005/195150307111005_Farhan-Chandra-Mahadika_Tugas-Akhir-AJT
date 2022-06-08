### Farhan Chandra Mahadika
### 195150307111005
### Tugas Akhir Arsitektur Jaringan Terkini
### -
#### Tugas 1
##### Pada tugas pertama akan dibuat sebuah Virtual Machine dengan konfigurasi sesuai pada petunjuk. Berikut konfigurasi pada VM yang dibuat sebagai berikut
![tugas 1-1](https://user-images.githubusercontent.com/106865290/172580358-cde2a940-be05-49c1-98b0-f12b3fed2209.png)

OS yang digunakan adalah Ubuntu Server 22.04 LTS 64 bit

![tugas 1-2](https://user-images.githubusercontent.com/106865290/172580563-cde6f628-432d-4061-a41e-c9d6e97da3fc.png)

Instance yang digunakan adalah t2.medium dengan key pair "vockey"

![tugas 1-3](https://user-images.githubusercontent.com/106865290/172580739-25820f5d-0ea2-4d16-aaa9-bb560b26e789.png)

![tugas 1-4](https://user-images.githubusercontent.com/106865290/172598018-5ac81635-3a85-43a4-8d80-e27734ce41a0.png)

![tugas 1-5](https://user-images.githubusercontent.com/106865290/172598032-37fcddbf-572a-459f-af7e-da7936cd49ce.png)

![tugas 1-6](https://user-images.githubusercontent.com/106865290/172598042-89aafc29-7c94-4ef8-8860-30120ed33e07.png)

![tugas 1-7](https://user-images.githubusercontent.com/106865290/172598046-cb0f1912-14cb-4fb7-8ac6-fc1dc38986ed.png)

![tugas 1-8](https://user-images.githubusercontent.com/106865290/172598064-565d692d-92c3-482d-abc2-ca621f1a215e.png)

Network setting berupa Allow SSH, HTTP, HTTPS, TCP dengan port 8080, dan TCP dengan port 8081

![tugas 1-9](https://user-images.githubusercontent.com/106865290/172598232-47282100-0571-42ae-8607-cb60496364c8.png)

Konfigurasi storage berupa 30 GiB dengan volume gp3

Setelah VM dibuat akan ada akses key dengan link connect, lalu dimasukkan key ke vocareum labs dengan command "ssh -i .ssh/labsuser (key VM)". Setelah dijalankan akan ditanyakan untuk menambahkan VM baru dan mengetik "yes". Setelah itu akan memasuki VM tersebut

![tugas 1-10](https://user-images.githubusercontent.com/106865290/172598735-77f0fc4e-dc70-4981-aaeb-57be34bf6d71.png)

Lakukan software update pada ubuntu ke versi terbaru, akan diperingatkan untuk restart VM

![tugas 1-11](https://user-images.githubusercontent.com/106865290/172599447-f3cd30da-511b-432f-8694-197914a1de80.png)

![tugas 1-12](https://user-images.githubusercontent.com/106865290/172599566-a52c5d89-77e2-4802-ad9f-45cd962fedf2.png)

![tugas 1-13](https://user-images.githubusercontent.com/106865290/172599572-edaab4e1-a88f-4f3c-90b3-1a5c32d58932.png)

Penginstalan Mininet

![tugas 1-14](https://user-images.githubusercontent.com/106865290/172599725-759c252e-e89e-43a2-b360-7667df6e25bc.png)

Penginstalan Ryu

![tugas 1-15](https://user-images.githubusercontent.com/106865290/172599749-9e1a2fe1-749f-42ca-9d56-17db59b75cd6.png)

Penginstalan Flowmanager

### -

#### Tugas 2
##### Pada tugas 2 akan dibuat custom topology mininet dengan contoh 2 switch dan 2 host, tugas yang akan dibuat berupa 3 switch dan 6 host

```
from mininet.topo import Topo
from mininet.log import setLogLevel, info

class MyTopo( Topo ):

    def addSwitch(self, name, **opts ):
        kwargs = { 'protocols' : 'OpenFlow13'}
        kwargs.update( opts )
        return super(MyTopo, self).addSwitch( name, **kwargs )

    def __init__( self ):
        "Create MyTopo topology..."
        
        # Inisialisasi Topology
        Topo.__init__( self )

        # Tambahkan node, switch, dan host
        info( '*** Add switches\n')
        s1 = self.addSwitch('s1')
        s2 = self.addSwitch('s2')

        info( '*** Add hosts\n')
        h1 = self.addHost('h1', ip='10.1.0.1/24')
        h2 = self.addHost('h2', ip='10.1.0.2/24')
     
        info( '*** Add links\n')
        self.addLink(s1, h1, port1=1, port2=1)
        self.addLink(s1, s2, port1=2, port2=1)
        self.addLink(s2, h2, port1=2, port2=1)

topos = { 'mytopo': ( lambda: MyTopo() ) }
```

Contoh custom topology 2 host 2 switch

![tugas 2-1](https://user-images.githubusercontent.com/106865290/172601427-77ffd2cd-7a70-4ebc-a8f0-fd520e7f7df6.png)

Bagan untuk tugas topology 3 switch, 6 host

```
from mininet.topo import Topo
from mininet.log import setLogLevel, info

class MyTopo( Topo ):
    "Simple topology example."

    def addSwitch(self, name, **opts ):
        kwargs = { 'protocols' : 'OpenFlow13'}
        kwargs.update( opts )
        return super(MyTopo, self).addSwitch( name, **kwargs )

    def __init__(self):
        Topo.__init__(self)
        "Create custom topo."

        # Add hosts and switches
        h1 = self.addHost( 'h1', ip = '10.1.0.1/24' )
        h2 = self.addHost( 'h2', ip = '10.1.0.2/24' )
        h3 = self.addHost( 'h3', ip = '10.1.0.3/24' )
        h4 = self.addHost( 'h4', ip = '10.1.0.4/24' )
        h5 = self.addHost( 'h5', ip = '10.1.0.5/24' )
        h6 = self.addHost( 'h6', ip = '10.1.0.6/24' )
        s1 = self.addSwitch( 's1' )
        s2 = self.addSwitch( 's2' )
        s3 = self.addSwitch( 's3' )

        # Add links
        self.addLink(s1, s2, port1=4, port2=2)
        self.addLink(s1, s3, port1=1, port2=3)
        self.addLink(s2, s3, port1=1, port2=4)
        self.addLink(s1, h1, port1=2, port2=1)
        self.addLink(s1, h2, port1=3, port2=1)
        self.addLink(s2, h3, port1=3, port2=1)
        self.addLink(s2, h4, port1=4, port2=1)
        self.addLink(s3, h5, port1=2, port2=1)
        self.addlInk(s3, h6, port1=1, port2=1)


topos = { 'mytopo': ( lambda: MyTopo() ) }
```

Code untuk custom topology 3 switch, 6 host

Jika dijalankan "sudo mn --controller=none, --custom test.py" maka akaan dibuat host dan switch yang sesuai di kode dan akan membuka terminal mininet

![tugas 2-5](https://user-images.githubusercontent.com/106865290/172602271-1d6a89f5-e428-4bbe-be77-dd89fa0d6e90.png)

Untuk menghubung dari host ke host melalui switch tertentu dimasukkan kode pada terminal mininet sebagai berikut

![tugas 2-3](https://user-images.githubusercontent.com/106865290/172602434-c28e023e-9883-4a34-ba80-bb1f80f50126.png)

jika menjalankan ping diantara host akan menghasilkan sebagai berikut

![tugas 2-4](https://user-images.githubusercontent.com/106865290/172602550-19262cb4-c912-479e-a69b-ea6fc5099edc.png)

### -

#### Tugas 3
##### Pada tugas 3 akan dibuat load balancer. Load balancer dibuat untuk membagi beban traffic dalam suatu server sehingga akan tidak membebankan ke beberapa jalur koneksi, mempercepat respon dari server dan menghindari terjadinya overload. Dari pengamatan tugas akan menghasilkan sebagai berikut

![laporan-tugas3-1](https://user-images.githubusercontent.com/106865290/172603303-e804ab26-b4fd-4619-96a4-4f1c490e1f30.png)

![laporan-tugas3-2](https://user-images.githubusercontent.com/106865290/172603310-37e521f5-b0a5-4748-86a4-0d2096c9b203.png)

![laporan-tugas3-3](https://user-images.githubusercontent.com/106865290/172603316-750217b0-cae3-449f-a1a5-ee8a50217682.png)

### -

#### Tugas 4
##### Pada tugas 4 akan menggunakan SPF Routing, merupakan pengaplikasian untuk menghitung jalur terpendek antara node menggunakan metode Open Shortest Path First.

Dari tugas ditunjuk melalui 2 temrminal. Terminal 1 untuk pemantauan, dan terminal 2 untuk eksekusi mininet

![tugas 4-1](https://user-images.githubusercontent.com/106865290/172604245-8fc54eb5-fee1-40ea-b662-dae9fd8abb61.png)

![tugas 4-2](https://user-images.githubusercontent.com/106865290/172604266-0f57c573-cfdd-44e0-b3b2-9502f1964410.png)

Ryu manager akan memantau aktivitas link dari mininet pada terminal 1

![tugas 4-3](https://user-images.githubusercontent.com/106865290/172604278-8468d8ed-0659-4b62-87db-48f7cbbc18dd.png)

Setelah membuka mininet, terminal 1 mulai membaca dan merekam aktivitas pada terminal 2

![tugas 4-4](https://user-images.githubusercontent.com/106865290/172604285-7a04245a-30b8-4c20-893e-349cc1daf29e.png)

Terminal 1 akan merekam ping dari eksekusi mininet di terminal 2 yang menjalankan "h1 ping -c 4 h4"

![tugas 4-5](https://user-images.githubusercontent.com/106865290/172604293-c1535043-93e3-4366-ae2d-1e487d639f4d.png)

Terminal 2 setelah menjalankan ping "h1 ping -c 4 h4"

![tugas 4-6](https://user-images.githubusercontent.com/106865290/172604303-2fef5b3a-3aa1-438e-ba2d-fb5043e88cfa.png)

Seperti diatas teriminal 1 merekam ping dari eksekusi mininet di terminal 2 yang menjalankan "h5 ping -c 4 h6"

![tugas 4-7](https://user-images.githubusercontent.com/106865290/172604306-ca21c2a9-5056-4feb-8ebc-9afc15e1db71.png)

Terminal 2 setelah menjalankan ping "h5 ping -c 4 h6"





