# Container Networking

Container networking refers to the ability for containers to connect to and communicate with each other, and with non-Docker network services. 

Docker k ander networking ko samjhney kelye hamey kuxh prerequisite concept ka pata hona zarori hey, nahi to kuxh samjh nahi ayega. 

## Internet Protocol (IP)

Yeah aik unique address hey jo kisi bhi device ko internet per uniquely identify karta hey or har us device k pass hona zrori hey jo inter network communication (communication between two different networks) karna chahati hey.

An example of IP in version 4 (IPV4)

```bash
192.160.1.21
```

Yeah dot seprated decimal values ko ham Octets kehtay heyn or har IP address mey total 4 dot separated Octets hoti heyn. Or har octet ko represent karney kelye 8 bits use hoti heyn, isliye har IP address 32 bits ka hota hey. Har octet 0 - 255 k darmiyan hoti hey because obviously in 8 bits the higher number we can represents is:

$$
2⁸ = 256
$$

```bash
11000000.10100000.00000001.00010101
```

**Fun Fact:** The total number of IP addresses possible with 32 bits are:

$$
2^{32} = 4,294,967,296
$$

And we are already running out of those range of IP addresses and have invented a new version of IP which is IPv6. It provides a lot more IP address then IPv4.

### Parts of IP Address

An IP address has two parts:

1. Network Bits

2. Host Bits

**Network Bits/Octets**

Yeah part hamey batata hey k kitni bits netwrok ko represent kar rahi heyn, ager in bits ya, network Octets ki value ko aik digit bhi increase kiya to network change ho jaye ga.

```bash
192.143.2.3
```

Let say in the above IP we can say the first two Octets reserver for the network, if I change any of them then it's a totaly different network, for example this is a different network.

```bash
193.143.2.3
```

**Host Bits**

Host bits are used to identify the device or host who have this IP allocated in the network. For example I can say the last two Octets in IP given below are for hosts.

```bash
192.143.2.3
```

It's an host, If I want an other IP to allocated to a next device I Increase the host bit by one and assigne to any of my divice on the network

```bash
192.143.3.3
```

## Important:_

Yaha pay slash k bash 16 k mtlb hey k pehli 16 bits network kelye reserve heyn.

```bash
123.131.1.3/16
```

## Subnet Mask

Pixchlay section mey ham ney IP address ko dehka but how the heck computer will know that which part of IP is Network Part and Host Part? Right?

That is where the Subnet Mask will come into picture, yeah aik esi value of hey jiskoe ager ham AND kartey heyn kis IP address k sath to hamey Network Address kit bits mill jati heyn, ya phir network address mill jata hey.

Let say ager subnetmask yeah hey:

```bash
255.255.0.0 // subnet mask
```

To iska mtlb kisi bhi IP jiska subnet mask yeah hoga uski pehli do Octets network Octets hongi ya network kelye use hongi. Let say this IP `192.143.2.3` has the subnet mask of `255.255.0.0`  iska mtlb hey k pehli do octets network octets heyn, unko ham change nahi kar saktey, ager kareyngey to woh network different network hoga

```bash
192.143.2.3
```

**Trick:** Subnet mey jitni Octets ki value 255 hogi utni octets network octets hongi. 

But this for us as human, per computer karta hey AND operation between the IP address and the Subnet Mask after converting them into Binary Formate.

```bash
IP Address:    192.143.2.3
Binary:        11000000.10001111.00000010.00000011

Subnet Mask:   255.255.0.0
Binary:        11111111.11111111.00000000.00000000

AND Operation: --------------------------------
Result:        11000000.10001111.00000000.00000000 => 192.143.0.0
```

So the network address for IP address `192.143.2.3` is `192.143.0.0`

### Are we on the same network?

Subnet mask is help your device know, is the device am I sending the message is on the same network as me or not, but how? It perfroms `AND` operation with your subnet mask on both, the sender and Receiver IP address and if it will end up getting the same network address, that means what, you and sender are on the same fucking network.

## What if we aren't on the same network?

Ager sender ko pata chalta hey k network address to match kar hi nahi raha tho phir message esay case mey default gateway ya phir sirf gateway k IP address ko send kar diya jata hey, or yeah aik router hota hey, 

# Default Gateway

Har PC mey aik extra IP configure hota hey jab koee message network me majood kis node ko nahi send karna hota to woh is default gatway per send kar diya jata hey, or yeah default gateway asal mey Router ka address hota hey. Jo is message ko phir network say bahir lay jata hey

I mean gateway aik router device hoti hey jo responsible hoti hey inter network communication kelye.

## Unusable IP Adresses

Kisi bhi network ander pehla or akhri IP address usable nahi hota qn nahi hota kisi bhi network ka pehla IP address us network ka adress hota hey.

Kisi bhi network ka last adress us network ka broadcast adress hota hey.

**Fun Fact:** Pehlay usable IP aksar router k interface ko allocate kiya jata hey.

## Switch

Switch is a layer two device that mean the Data Link layer where all the comunications happens using MAC Address (Media Access Controle Adress- burned in device and cannot be changed).

Jab bhi koee message firts time kisi port (ethernet port) per ata hey to switch us tarf k PC ka MAC address or switch ki jis ethernet port per woh aya hey switch isay yad kar layta hey. 

Next time jab bhi koee message is learned kiye howay MAC address par ata hey to switch dehkta hey k yeah MAC address meyri kis port k uper tha, us tarf message send kar deyta hey.

**Fun Fact:** is say pehlay Hub (Layer 1 Device) use hoti thi yeah message ko network per majood sabhi computer ko broadcast kar deyti thi. Jisay pacted collision ho jati thi or security risk bhi barh jata tha.

## Broadcast Address

Har network ander last IP address broadcast address hota hey, let say a network with subnet mask given below has the last IP address used as a broadcast address.

It also called an unsuable IP address on the network.

```bash
Last IP: 192.255.255.255
Subnet Mask: 255.0.0.0
```

Jab sab devices ko aik message bhejna hota hey without knowing their IPs then we use this broadcast Network address.

## Broadcast MAC Address

Broadcast a message to all nodes on the network either they in a sub a network without any filter.

```bash
FFFF.FFFF.FFFF.FFFF
```

When a device wants to communicate with IP address 192.168.1.50 (Or IP address comunication hoti kab jab aik pc ko kisi dosray network k pc say baat karni hoti hey), it needs to know the **MAC address** (physical hardware address) to actually send the data at the data link layer.

But here's the catch:

The device doesn't know which MAC address corresponds to 192.168.1.50. Per zrori hi qn hey MAC address jab IP hey to?

Har network say message bahir lay kar janey kelye aik router configure hota hey, yeah router bhi local network mey aik node ki traha hota hey, isay bhi network adresses mey say aik IP address mila hota hey, jo aksar kisi network ka pehlay usable IP ko assigne kar diya jata hey router ko, and isi same address ko as a default gateway k tor per use kia jata hey baki sarey nodes k ander.

Abh local network k ander communication MAC address k base pay hoti chaye woh Wifi Adapter k zariye say ho ya phir ethernet cable use kartey switch k zariye say yeah sabh Layer 2 pay kaam kartey heyn.

Abh ager mujeh aik packet network say bahir send karna hey to mujeh woh router bhajna parey ga router kaha hey meyray local network mey but meyray PC ko uska MAC address to pata hi nahi per mujeh route ka IP zror pata hey (which is setted as gateway in my PC) so what my PC will do it uses the broadcast MAC Adress to send an ARP (Address Resolution Protocol) Packet to everyone one the network.

ARP kehta arey bahi jis bhi device ka IP address 192.168.1.50 woh respond karey k uska MAC address kia hey baki devices jinka IP woh nahi jis device ka hamey MAC address chaye (192.168.1.50) woh is broadcast message ko ignore kar deyn.

To in the same network router ko jab yeah packet milta hey to woh kehta hey han bahi meyra hey yeah IP adress. Ad sender device proper data frame banati hey jismey exact destination MAC address hota hey router ka, or isay cache bhi karliya jata hey ARP table mey takey nextime dobara yeah kaam karna parey.

## Router

Router is a Layer 3 three device (Network Layer) which means the communication happens using IP address. Router is used for internetwork communication yani jab aik network per majood device ko dosray network per majood kisi device ko message send karna hota hey to tabh router yeah communication handle karta hey.

Sabh say pehlay computer check karta hey k receiver same network per hey ya nahi through. Kesay karta hey ham subnet mask walay section mey yeah dehk chukay heyn, ager to Receiver same address per hey to LAN device like swithc ko yeah message diya jata hey network k ander communication kelye

But if Sender or Receiver ka network different hota hey to computer k pass rotuer ka IP address as Default Gateway set hota hey

### DHCP

Stands for Dynamic Host Configuration Protocol, pehlay kia huwa karta tha har computer ko network uper manually network k sath configure karna parhta thaa jo k chotey networks kelye bhi time taking tha per barey networks per har PC k manually bhait IP allocate karna or subnetmask, gateway, or DNS configure karna thora mushkil thaa

Then we've invend this dude DHCP yeah automatically IP allocate kar sari setting configure kar deyta hey, Asal mey jab hamrey kis computer ko internet chaye hota hey ya network k sath connect hona hota hey to woh DHCP server ko request karta hey IP kelye, or DHCP agey say usay sari detail send karta hey jisay hamara computer setup kar layta hey.

Home Router k ander built in DHCP hota hey tabhi ham Wi-Fi network say connect kar patey hey, yeah DHCP server dynamically IPs allocate karta rehta hey.

Barey networks k pass unka apna dedicated DHCP server hota hey.

```bash
Step 1: DISCOVER (Device → Broadcast)
──────────────────────────────────────
Tumhara Device:
"Koi DHCP server hai? Mujhe IP chahiye!"

Frame:
├─ Source MAC: AA:AA:AA:AA:AA:AA (Your device)
├─ Dest MAC: FF:FF:FF:FF:FF:FF (Broadcast)
├─ Source IP: 0.0.0.0 (Abhi koi IP nahi!)
├─ Dest IP: 255.255.255.255 (Broadcast)
└─ Message: "DHCP DISCOVER"


Step 2: OFFER (DHCP Server → Your Device)
──────────────────────────────────────────
DHCP Server (Router):
"Haan main hoon! Yeh lo IP address!"

Frame:
├─ Source MAC: RR:RR:RR:RR:RR:RR (Router)
├─ Dest MAC: AA:AA:AA:AA:AA:AA (Your device)
├─ Offered IP: 192.168.1.105
├─ Subnet: 255.255.255.0
├─ Gateway: 192.168.1.1
├─ DNS: 8.8.8.8
├─ Lease Time: 24 hours
└─ Message: "DHCP OFFER"
```

### DNS

Stands for Domain Name System. The DNS server is like a phone book of internet, 

```bash
Ahmad -> 03106715784 # Your mobile phone
google.com -> 123.432.12.3 # DNS Server
```

Har computer k sath aik DNS server ka IP configure hota hey, jab bhi koee domain name ko request ki jati hey to sabh say pehlay domain resolve kia jata hey aik IP address mey uskey baad is IP address ko request ki jati hey

Yani pehlay request DNS server K IP per ki jati hey k bahi IP bata is domain ka kia hey, ager to yeah domain ham ney pehli dafa DNS server say request ki hoti hey to isay multip level pay cache kar liya jata hey:-

```bash
|- Router
|- OS 
|- Browser
# Next time faster
```

## Network Interface

**Network Interface** Hardware/Software component jo device ko network se connect karta hai aur data send/receive karta hai.

Jo ethernet port apko dhik rahi hey apke laptop mey yeah aik network interface hey, jikey 

**Physical Interface (Hardware)**

```bash
Examples:
├─ Ethernet port
├─ Wi-Fi adapter
```

**Virtual Interface**

Virtual Network Interface (VNI), jise Virtual Network Adapter ya Virtual NIC (VNIC) hi kehte hain, yeh ek software-based ya abstract representation hai jo computer network interface ki tarah kaam karti hai, lekin yeh kisi physical hardware (asal Network Interface Card - NIC) se seedha talluq nahi rakhti.

## Netwok Address Translation

It converts the private IP address into Public and Public into Private. IPv4 limmited heyn is liye ham har device ko public IP nahi dey saktey. To NAT ka feature router k ander hi hota hey jab bhi koee request ati hey to usay public IP k through bahir bheja jata hey.

## Network Namespace

Linux ka aik feature hey k app isolated virtual network namespace bana saktey ho jinkey ander pora aik virtual networking stack hota hey jesay aik physical device k pass hota hey, jesay, network interface `ethernet`, loopback interface, ports, routing table, IP address etc.

### Networking in Containers

Jab bhi koee container banta hey to uski aik apni network namespace hoti hey.

Har Network Namespace k ander pora virtual network stack hota hey, complete with its own set of network devices.

Let's look inside a docker container running a busybox image inside it. Yaha pay mey ager mey yeah command run karta hun

```bash
$ ip addr
```

To mujeh netwrok interfaces of unki configuration ki detail nazar ati hey. 

![](C:\Users\mrasi\AppData\Roaming\marktext\images\2025-11-04-15-35-47-image.png)

**1 LOOPBACK**

Har device k pas aik loopback interface hota hey jisay ham localhost k name say access kar saktey heyn, yeah address itself computer ko refer karta hey

```bash
127.0.0.1/8
```

**2 eth0**

Dosra network interface aik virtual ethernet interface hota hey. Jiska IP address hey:-

```bash
172.18.0.2
```

## Bridge

Jab ham docker install kartey heyn to docker aik virtual network Bridge banata hey, hamarey host machine k uper, if you are on linux you can see it throuhg command:-

```bash
ip addr
```

Docker Bridge Network ek **Virtual Network Switch** aur **Gateway** dono ka kaam karta hai.

### Bridge Working as Switch

Jab do containers jo ek hi  Bridge Network jaise `docker0` by default bridge created by docker, ya koi **User-Defined Bridge** par chal rahe hon, aapas mein baat karna chahte hain, toh **Bridge Network** ek **Layer 2 Switch** (Data Link Layer, Mac Addresses) ki tarah kaam karta hai.

### 🛡️ Yeh Kyun Zaroori Hai? (Fayde)

- **Isolation (Alag-Thalag Rakhna):** Sabse bada fayda yeh hai ki ek container ke network mein ki gayi tabdeeli (change) doosre containers ya Host system par **asar nahi karti**. Agar ek container crash ho jaaye ya usmein security issue ho, to doosre containers **mehfooz** rehte hain.

- **Portability (Harkat-Paziri):** Har container ko lagta hai ki woh ek **clean slate** (khaali) network par chal raha hai. Isse woh har environment mein aasani se deploy ho jaate hain.

- **No Port Conflicts (Ports ka Takrao Nahi):** Aap ek hi Host machine par kayi containers chala sakte hain, aur har container port 80 ya port 22 istemaal kar sakta hai, kyunki woh sab apne **alag-alag Network Namespace** mein maujood hain.

**Misaal:**

Aap isse aise samajh sakte hain jaise **ek building** (Host Machine) hai, aur usmein **bohot saare kamre** (Containers) hain. Har kamra (Network Namespace) ka **apna darwaza** (`eth0`), **apna address** (IP address), aur **apne andar ke rules** (Firewall) hain, bhale hi woh sab ek hi building mein hon.

---

Kya aap **Control Group (Cgroups)** ke baare mein bhi jaanna chahenge, jo **Network Namespace** ki tarah containers ko **CPU aur Memory** bhi alag-alag dete hain?

 apna  **`lo` (loopback)** aur woh **`eth0`** interface (jo veth pair ka ek end hota hai).

**Kaam:** Yeh Bridge (masalan, `br-86069f1b7658` jo aapke output mein tha) container ke **veth interface** se aane waale data packets ko dekhta hai aur unhein usi Bridge par maujood **doosre container** ke `veth` interface ki taraf **forward** kar deta hai.

- **Summary:** **Bridge** hi woh zariya hai jiske through containers aapas mein **private IPs** ka istemaal karte hue **direct baat** karte hain.

Jab container data bhejta hai, toh woh `eth0` se nikal kar veth pair ke zariye **Docker Bridge** tak pahunchta hai.

**Docker Bridge** phir us data ko **Host machine** ke asli **physical network interface** (jaise aapka Wi-Fi ya LAN card) se bahar Internet ya local network par bhej deta hai.
