# Cisco RIP(Routing Information Protocol)  Routing

Routing Information Protocol (RIP), iki farklı versiyona sahip bir yönlendirme bilgisi protokolüdür. Biz burada versiyon 2'yi kullanmayı tercih edeceğiz. Genellikle küçük ağlarda kullanılan bu protokol, yakınlık vektörüne dayanır. Yani veri paketleri, hedef ağa ulaşırken en yakın yolu seçmeye çalışır, bu da demek oluyor ki verilerin istenen hedefe ulaşma süresi en kısa olan yol üzerinden yönlendirilir.

Ancak, RIP'in bazı dezavantajları vardır. En belirgin dezavantajı, en kısa yolun her zaman en doğru yol olmamasıdır. RIP, maksimum olarak 15 sıçramayı destekler, 16 sıçramadan sonrasında çalışmaz. Ayrıca, yönlendirme güncellemeleri her 30 saniyede bir yapılır, bu da ağ üzerinde gereksiz bir bilgi trafiğine neden olabilir.

Dolayısıyla, RIP, küçük ağlarda kullanılabilir ancak büyük ve karmaşık ağlar için uygun bir seçenek değildir. Yönlendirme bilgisi protokollerinin seçiminde, ağın büyüklüğü ve karmaşıklığı gibi faktörler göz önünde bulundurulmalıdır.




