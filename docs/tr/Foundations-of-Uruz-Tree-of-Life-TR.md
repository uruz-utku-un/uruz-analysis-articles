# Uruz Yaşam Ağacının Temelleri
\
**Belgenin Ortaya Çıkış Tarihi:**
2026-08-03
\
**Belge Sürümü:**
V1.0
\
**Belgeyi Oluşturanlar:**
Utku Ün (Uruz)

**Başlıklar:**
- [Genel İlke - 1](#genel-i̇lke---1)
- [Genel İlke - 2](#genel-i̇lke---2)
- [Genel İlke - 3](#genel-i̇lke---3)
- [Tek Bileşen Akışı](#tek-bileşen-akışı)
- [Çoklu Bileşen Akışı](#çoklu-bileşen-akışı)
- [Tersine Bileşen Akışı (Tersine Mühendislik)](#tersine-bileşen-akışı-tersine-mühendislik)
- [Tasarım Felsefesinin Öngürülen Sektörel Yansımaları](#tasarım-felsefesine-öngürülen-sektörel-yansımaları)

> Ayrıntılı düşünce süreci için ilgili deneme yazısına göz atabilirsiniz:
[Programlamanın Özü: Veri ve Düşünce](https://github.com/uruz-utku-un/uruz-thoughts/blob/main/docs/tr/Essence-of-Programming-TR.md)

---

## Genel İlke - 1
Her bileşen **bir girdi alır** ve **bir sonuç üretir.**
\
Bu yaklaşımın amaçları:
- **Bağımsızlık:**
  Bileşenler birbirinden bağımsızdır, yalnızca kendi girdileriyle çalışır.
- **Modülerlik:**
  Her bileşen tek başına test edilebilir ve yeniden kullanılabilir.
- **Kompozisyon:**
  Bir bileşenin çıktısı başka bir bileşenin girdisi olabilir, böylece akış
  zincirleri kurulabilir.
- **Daha Kolay Test Edilebilirlik:**
  Bileşenler küçük ve bağımsız tasarlandığında, her biri ayrı ayrı test
  edilebilir. Bu sayede hataları erken aşamada yakalamak mümkün olur ve 
  sistem güvenilirliği artar. 
- **Daha Kolay Hata Yönetimi**
  Bağımsız bileşenler sayesinde bir hata yalnızca ilgili bileşeni etkiler.
  Bu izolasyon, hatanın kaynağını bulmayı ve çözmeyi kolaylaştırır.
  Böylece sistemin tamamı yerine yalnızca sorunlu parçaya odaklanılır.
- **Bakım Kolaylığı:**
  Modüler yapı, zaman içinde yapılacak güncellemeleri ve iyileştirmeleri
  basitleştirir. Bir bileşen üzerinde değişiklik yapıldığında diğer
  bileşenler etkilenmez. Bu da uzun vadede sürdürülebilir bir geliştirme
  süreci sağlar.

---

## Genel İlke - 2
- Her bileşen **amacına yönelik** tasarlanmalıdır.
- Her bileşen planlanırken **temel işlevsellik** öncelik alınmalıdır.
- Bu yaklaşım, **karmaşıklığı önler** ve **algılamayı kolaylaştırır.**
- Tasarım aşamasında bir bileşenin gereksiz şekilde dallandırılması veya
  odağından sapması, uzun vadede projenin işlevselliğini baltalayan en temel
  sebeplerden biridir.
- Bu ilke, yazılım geliştirmede **basitlik**, **sadelik ve anlaşılabilirlik**
  prensiplerini vurgular. Aynı zamanda **spagetti kodu** engelleyerek
  sürdürülebilir proje yönetimini destekler.

- **Örnek Senaryo:**
  \
  Bir **personel kayıt bileşeni,** yalnızca kayıt ekleme işlevine
  odaklanmalıdır.
  \
  Eğer aynı bileşen aynı anda raporlama, analiz veya e-posta gönderme gibi
  farklı işlevleri üstlenirse, kısa vadede kullanışlı görünse de uzun vadede
  karmaşıklık artar ve bakım zorlaşır.
  \
  Bu nedenle her bileşen tek bir amaca hizmet etmeli, diğer işlevler ayrı
  bileşenlere dağıtılmalıdır.

---

## Genel İlke - 3 
- Bu ilke daha çok **ürün aşamasını** hedefler.
- Bileşenlere bir özellik yalnızca "olsun diye" eklenmemelidir.
  Evet, teknik olarak eklenebilir ve yazpılabilir bir özellik olabilir;
  ancak bu tek başına hiçbir değer taşımaz.
- Bir özelliğin **süslü veya gösterişli olması,** onun kullanışlı ya da
  gerekli olduğu anlamına gelmez. 
- Bu durum hem geliştirici hem de kullanıcı için bir problemdir:
    * **Geliştirici açısından:**
      Gereksiz özellikler bakım kolaylığını, hata yönetimini ve
      anlaşılabilirliği baltalar.
    * **Kullanıcı açısından:**
      Fazlalıklar öğrenme sürecini zorlaştırır, ürünü karmaşık ve erişilmez
      hale getirir. 

- **Örnek Senaryo:**
  \
  Bir **metin işleme bileşeni** düşünelim. Temel amacı metni parçalamak ve
  işlemek olmalıdır.
  \
  Eğer bu bileşene aynı anda görsel efektler, istatiksel analizler veya
  kullanıcı arayüzü öğeleri eklenirse, kısa vadede "zengin" görünse de uzun
  vadede hem bakım zorlaşır hem de kullanıcı için öğrenme süreci karmaşık
  hale gelir.
  \
  Bu nedenle her özellik, yalnızca **gerçek ve temel bir ihtiyacı**
  **karşılıyorsa** eklenmelidir. 

---

## Tek Bileşen Akışı
- Bir bileşen yalnızca girdisini işleyip sonuç üretir.
- Aynı bileşen girdisinin doğru tipte olduğunu kontrol ederek garanti
  eder. Yani **her bileşen giriş ve çıkış sözleşmesini tanımlar.**
- Aynı bileşen **eğer gerek duyuluyorsa** girdiden sonuç üretebildiği gibi
  sonuçtanda girdiyi tekrar üretebilmelidir (**tersine mühendislik**).

```mermaid
flowchart LR
START(Başla)
END(Son)
COMPONENT[Bileşen]

START -->|Girdi| COMPONENT -->|Sonuç| END
```

**Özellikler:**
- İzole çalışma ortamı
- Hata izolasyonu kolaylığı
- Basit test edilebilirlik

---

## Çoklu Bileşen Akışı
- Birden fazla bileşen birbirine bağlanarak daha karmaşık bir akış oluşturur.
- Aynı anda birden fazla bileşen farklı girdiler üzerinde çalışabilir.
```mermaid
flowchart LR
START(Başla)
END(Son)
COMPONENT_X[Bileşen-X]
COMPONENT_Y[Bileşen-Y]
COMPONENT_Z[Bileşen-Z]

START -->|Girdi| COMPONENT_X
COMPONENT_X -->|Sonuç| COMPONENT_Y
COMPONENT_Y -->|Sonuç| COMPONENT_Z
COMPONENT_Z -->|Sonuç| END
```

**Özellikler:**
- Zincirleme veri akışı
- Esnek sistem tasarımı
- Yeniden kullanılabilir modüller 

---

## Tersine Bileşen Akışı (Tersine Mühendislik)
- Eğer gerek duyuluyorsa bir bileşen, **girdiden sonuç üretebildiği gibi**
  sonuçtan da girdiyi yeniden üretebilmelidir. 
- Her bileşen için tersine mühendislik zorunlu değildir. Burada önemli olan,
  **o anki ihtiyaç** veya **uzun vadeli kullanım senaryosu** açısından
  tersine mühendisliğe gerek olup olmadığıdır.
- Bu yaklaşım, özellikle veri kaybı durumlarında veya çıktının doğruluğunu
  sınamak gerektiğinde faydalıdır.

```mermaid
flowchart LR
INPUT(Girdi)
RESULT(Sonuç)
COMPONENT[Bileşen]

INPUT --> COMPONENT --> RESULT
RESULT --> COMPONENT --> INPUT
```

**Özellikler:**
- Çift yönlü akış imkânı sağlar.
- Veri bütünlüğünü test etmeye yardımcı olur.
- Gereksiz karmaşıklığı önlemek için yalnızca ihtiyaç halinde uygulanmalıdır.

**Örnek Senaryo:**
\
Bir **dosya şifreleme bileşeni** düşünelim. Normal akışta girdiyi (metni)
alır ve sonuç (şifrelenmiş metin) üretir.
\
Ancak tersine akışta, şifrelenmiş metinden tekrar orjinal metin elde
edebilmek gerekir.
\
Bu özellik her bileşen için geçerli değildir; fakat güvenlik ve veri
erişilebilirliği açısından bu tür bileşenlerde kritik öneme sahiptir.
 
---

## Tasarım Felsefesinin Öngürülen Sektörel Yansımaları
1. **Avantajlar**
    - Bu tasarım felsefesi sayesinde büyük ekiplerin üstleneceği işler, daha
      küçük ekipler tarafından daha temiz ve verimli şekilde yapılabilir.
    - Küçük ekipler, daha az bütçe ile çalışırken ters orantılı olarak daha
      kaliteli işler ortaya koyabilir. 
    - Geleneksel olarak küçük ekiplerin iş yükü ve maliyet sebebiyle kurumsal
      yapı kazanmaları zorken bu felsefe sayesinde
      **yeni oluşumların artması** ve köklü kuruluşların yanında rekabetçi bir
      ekosistemin gelişmesi öngörülmektedir.
    - Bu felsefenin hedeflerinden biri de, ortaya çıkan ürünlerin
      **anlaşılabilirliğini arttırmak** olduğu için kullanıcıların öğrenme
      sürecini kolaylaştırır. Böylece ürünün ekosistemine dahil olma süreci
      hızlanır ve kullanıcı kitlesi genişleyebilir.

2. **Dezavantajlar**
    - Köklü kuruluşlar için az iş gücüyle aynı veya daha iyi işlerin
      yapılabilmesi, **"az maliyet, çok iş" politikları, artan maliyet baskısı**
      **veya kontrolsüz büyüme gibi sebeplerden dolayı iş gücünde küçülmeye yol**
      **açabilir.** Bu durum çalışanlar açısından olumsuz sonuçlar doğurabilir.
    - **Ancak unutulmamalıdır ki,** bu tasarım felsefesi aynı zamanda
      **tecürbeli bireylerin ve küçük-bağımsız ekiplerin** kendi
      girişimlerini kurmalarına ve daha iyi olanakların kapısını
      aralamalarına da zemin hazırlayabilir.
      Böylece sektörde **yeni rekabet alanları ve daha dinamik bir**
      **ekosistem oluşabilir.**
