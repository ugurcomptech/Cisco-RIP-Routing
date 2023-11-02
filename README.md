# Cisco RIP(Routing Information Protocol)  Routing

Routing Information Protocol (RIP), iki farklı versiyona sahip bir yönlendirme bilgisi protokolüdür. Biz burada versiyon 2'yi kullanmayı tercih edeceğiz. Genellikle küçük ağlarda kullanılan bu protokol, yakınlık vektörüne dayanır. Yani veri paketleri, hedef ağa ulaşırken en yakın yolu seçmeye çalışır, bu da demek oluyor ki verilerin istenen hedefe ulaşma süresi en kısa olan yol üzerinden yönlendirilir.

Ancak, RIP'in bazı dezavantajları vardır. En belirgin dezavantajı, en kısa yolun her zaman en doğru yol olmamasıdır. RIP, maksimum olarak 15 sıçramayı destekler, 16 sıçramadan sonrasında çalışmaz. Ayrıca, yönlendirme güncellemeleri her 30 saniyede bir yapılır, bu da ağ üzerinde gereksiz bir bilgi trafiğine neden olabilir.

Şimdi yapılandırmalarımıza başlayalım:

# Network Yapılandırmaları

## PC Yapılandırmaları

- **Ankara Network:**
  - **Ip Adres:** 192.168.10.10
  - **Ağ Maskesi:** 255.255.255.0
  - **Ağ Geçidi:** 192.168.10.1


- **İstanbul Network:**
  - **Ip Adres:** 192.168.20.10
  - **Ağ Maskesi:** 255.255.255.0
  - **Ağ Geçidi:** 192.168.20.1


- **İzmir Network:**
  - **Ip Adres:** 192.168.30.10
  - **Ağ Maskesi:** 255.255.255.0
  - **Ağ Geçidi:** 192.168.30.1


## Router İç ve Dış Network Yapılandırmaları


### Ankara Router

```
Router>en
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#interface fastEthernet 0/0
Router(config-if)#ip address 192.168.10.1 255.255.255.0 // iç network yapılandırması
Router(config-if)#no shutdown 
Router(config-if)# exit
Router(config)#interface serial 2/0
Router(config-if)#ip address 10.1.1.1 255.0.0.0 // İstanbul ile iletişimde olan dış network yapılandırması
Router(config-if)#no shutdown 
```

### İstanbul Router

```
Router>en
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#interface fastEthernet 0/0
Router(config-if)#ip address 192.168.20.1 255.255.255.0 // iç network yapılandırması
Router(config-if)#no shutdown 
Router(config-if)# exit
Router(config)#interface serial 2/0
Router(config-if)#ip address 10.1.1.2 255.0.0.0 // Ankara ile iletişimde olan dış network yapılandırması
Router(config-if)#no shutdown
Router(config-if)# exit
Router(config)#interface serial 3/0
Router(config-if)#ip address 30.1.1.1 255.0.0.0 // İzmir ile iletişimde olan dış network yapılandırması
Router(config-if)#no shutdown 
```

### İzmir Router

```
Router>en
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#interface fastEthernet 0/0
Router(config-if)#ip address 192.168.30.1 255.255.255.0 // iç network yapılandırması
Router(config-if)#no shutdown 
Router(config-if)# exit
Router(config)#interface serial 3/0
Router(config-if)#ip address 30.1.1.2 255.0.0.0 // İstanbul ile iletişimde olan dış network yapılandırması
Router(config-if)#no shutdown 
```


Şimdi RIP yapılandırmalarını yapalım:


## RIP

### Ankara Router

```
Router(config)#router rip
Router(config-router)#version 2
Router(config-router)#network 192.168.10.0
Router(config-router)#network 10.1.1.0
Router(config-router)#no auto-summary 
Router(config-router)#passive-interface fastEthernet 0/0
```


### İstanbul Router

```
Router(config)#router rip
Router(config-router)#version 2
Router(config-router)#network 192.168.20.0
Router(config-router)#network 10.1.1.0
Router(config-router)#network 30.1.1.0
Router(config-router)#no auto-summary 
Router(config-router)#passive-interface fastEthernet 0/0
```



### İzmir Router

```
Router(config)#router rip
Router(config-router)#version 2
Router(config-router)#network 192.168.30.0
Router(config-router)#network 30.1.1.0
Router(config-router)#no auto-summary 
Router(config-router)#passive-interface fastEthernet 0/0
```

**BİLGİLENDİRME:** "no auto-summary" komutu, RIP'in ağ sınırları arasındaki alt ağları özetlemeyi kapatır ve daha ayrıntılı yönlendirme bilgilerinin kullanılmasına izin verir. "passive-interface" komutu ise belirli bir ağ arabiriminin RIP iletişimine katılmamasını sağlar, bu da iç ağ trafiğini dışarıya sızdırmadan korur ve ağ güvenliğini artırır. Bu komutlar, yönlendirme davranışını özelleştirmek ve ağ güvenliğini sağlamak için kullanılır.


