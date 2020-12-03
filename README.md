# İşletim Sistemleri Projesi
# 21. Unixte kabuk programlama (shell scripting) dilinin temel örneklerle anlatımı

## Shell (Kabuk) nedir?

Basitçe tanımlamak gerekirse komutları klavyeden alan işletim sistemiyle haberleşmemizi sağlayan bir programdır. Eskiden bilgisayarlar etkileşime girmek için şimdiki gibi grafik kullanıcı arayüzleri (graphical user interface GUI) olmayıp shell gibi komut satırı arayüzleri (command line interface CLI) kullanılıyordu. Hala pek çok işletim sisteminde en etkin şekilde kullanmak için kabukla etkileşmek gereklidir. Hatta bu verimi fark eden Microsoft firması da işletim sisteminde yakın zamanda PowerShell kabuğu geliştirmiştir.

Pek çok Linux çekirdeği kullanan işletim sistemlerinde Steve Bourne tarafından yazılmış olan bash programını shell olarak kullanır. Bu program aslında Unix sistemindeki sh shell programının geliştirilmiş halidir.

## Test komutu

    test expr

expr şart ifadesini değerlendirip 0 (Doğru) veya 1 Yanlış durumu döndürür. 

Eğer [ biçimi kullanılacaksa son arguman ] olmalıdır.


## Kabuk Programları
Kabuk programı aslında bir veya daha fazla komutu barındıran çalışabilir metin bazlı dosyalardır. Bir dosyanın çalışabilir yapılması için

    $ chmod +x dosya_ismi

Dosyayı çalıştırmak içinse

    $ ./dosya_ismi

### Yorum satırları
Kabuk programlarına yorum eklenmek istenirse # kullanılır. İlgili satırda # simgeden sonra gelen komutlar yorum olarak değerlendirilir ve göz ardı edilirler.

Pek çok kabuk programı olduğundan yazdığınız kabuk programını belirtmeniz gerebilir. Bunun için Shebang olarak ifade edilen #! karaterlerinden sonra kullanılacak kabuk programının yolu vermek gereklidir. 

    which bash

komutu ile işletim sisteminide bash programının tam yolunu öğrenip Shebang i doğru şekilde yazabilirsiniz. Genellikle aşağıdaki 

    #!/bin/bash

yazarak bash kabuğunu kullandığımızı belirtebiliriz. Eğer unutulursa da belki programını çalışabilir. Herhangi bir hatayı en aza ingirdegemek için yazılması gereklidir.

## Değişkenler

Belli bir değeri hafıza tutup ona bir isimle ulaşmak için değişkenler kullanırız.

    degisken1=3; degisken2="Deneme" #aynı satırda iki komutu birbirinden ayırabilmek için ; kullanılır.

Atama işlemi için kullanılan = operatörünü kullanırken boşluk kullanmamalısınız.

    degisken3=degisken1 #Doğru kullanım
    degsiken4 = degisken3 #Yanlış kullanım

Pek çok programlama dilinde olduğu gibi değişkenleri isimlendirirken aşağıdaki kurallara dikkat edilmelidir.

- Değişken isimleri rakamla başlayamaz.
- Değişken ismi içerisinde _ dışında karakter bulunamaz.
  
Değişkenlere erişebilmek için $ işareti kullanılır.

Bir değişkenin değeri ise echo komutu ile ekrana yazdırılır.

    echo Yukarıda değişkenlere atanan değerler $degisken1 ve $degisken2 dir.
    Yukarıda değişkenlere atanan değerler 3 ve Deneme dir.

### Aritmetik işlemler

Aritmetik işlemler için eval veya let komutu kullanılır.

    $let "carpim=2*7"
    $echo $carpim
    14

    typeset -i sonuc #sonuc isimli tam sayı değişkeni tanımlandı.
    a=100; b=56 #aynı satırda iki komutu birbirinden ayırabilmek için ; kullanılır.
    sonuc = a*b
    echo $sonuc

### Mantıksal Operatörler

#### Aritmetik Karşılaştırma
|Operatör|Anlamı     |Örneği    |Açıklaması|
|:------:|:----------|:--------:|:--------:|
|-gt     |büyük      | $a -gt $b| a > b    |
|-lt     |küçük      | $a -lt $b| a < b    |
|-ge     |büyük eşit | $a -ge $b| a >= b   |
|-le     |küçük eşit | $a -le $b| a <= b   |
|-eq     |eşit       | $a -eq $b| a == b   |
|-ne     |eşit değil | $a -ne $b| a != b   |
 
#### Dizi (String) Karşılaştırma
|Operatör|Anlamı        |Örneği    |Açıklaması|
|:------:|:-------------|:--------:|:--------:|
|-z      |boş dizi      | -z Metin | Metin dizisinin uzunluğu sıfır ise    |
|-n      |tanımlı dizi  | -n Metin | Metin dizisinin uzunluğu sıfır değilse|
|=       |eşit diziler  | Metin1 = Metin2 | Metin1 dizisi Metin2 dizisine eşitse   |
|!=      |farklı diziler| Metin1 != Metin2 | Metin1 dizisi Metin2 dizisine eşit değilse |

#### Dosya Karşılaştırma
|Operatör|Anlamı        |Örneği    |Açıklaması|
|:------:|:-------------|:--------:|:--------:|
|-a      |dosya var      | $a -gt $b| a > b    |
|-e      |dosya var      | $a -gt $b| a > b    |
|-f      |dosya var      | $a -gt $b| a > b    |
|-s      |dosya boş değil  | $a -lt $b| a < b    |
|-r      |dosya okunabilir  | $a -ge $b| a >= b   |
|-w      |dosya yazılabilir| $a -le $b| a <= b   |
|-x      |çalıştırabilir dosya| $a -le $b| a <= b   |
|-h      |sembolik bağlantı| $a -le $b| a <= b   |
|-c      |karakter aygıt| $a -le $b| a <= b   |
|-b      |blok aygıt| $a -le $b| a <= b   |
|-nt     |Yeni(değiştirilme tarihi) dosya| Dosya1 -nt Dosya2 | Dosya1 Dosya2'den daha yeni
 
 ## Akış kontrolü

 ### if-else-elif

    if [ şart ]
    then
        komut 1
        komut 2
    elif [ şart ]
    then 
        komut 3
        komut 4
    else
        komut 5
        komut 6
    fi

