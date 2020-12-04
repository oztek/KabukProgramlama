# İşletim Sistemleri Projesi HAKAN ÖMER ÖZTEK 2190656006

[Bu belgeye ve videoya ulaşabileceğiniz adres] (https://github.com/oztek/KabukProgramlama)


![Erişim Yolu](images/Yol.png) 

- [İşletim Sistemleri Projesi HAKAN ÖMER ÖZTEK 2190656006](#i̇şletim-sistemleri-projesi-hakan-ömer-öztek-2190656006)
- [21. Unixte kabuk programlama (shell scripting) dilinin temel örneklerle anlatımı](#21-unixte-kabuk-programlama-shell-scripting-dilinin-temel-örneklerle-anlatımı)
  - [Shell (Kabuk) nedir?](#shell-kabuk-nedir)
  - [Kabuk Programları](#kabuk-programları)
    - [Çalıştırılabilir dosya](#çalıştırılabilir-dosya)
    - [Shebang satırı](#shebang-satırı)
    - [Yorum satırları](#yorum-satırları)
  - [Değişkenler](#değişkenler)
  - [Parametreler](#parametreler)
    - [Argüman Parametresi](#argüman-parametresi)
    - [Özel Karakter Parametresi](#özel-karakter-parametresi)
    - [Aritmetik işlemler](#aritmetik-işlemler)
    - [$( ) ve <() Operatörleri](#--ve--operatörleri)
    - [Mantıksal Operatörler](#mantıksal-operatörler)
    - [Aritmetik Karşılaştırma](#aritmetik-karşılaştırma)
    - [Dizi (String) Karşılaştırma](#dizi-string-karşılaştırma)
    - [Dosya Karşılaştırma](#dosya-karşılaştırma)
  - [Akış kontrolü](#akış-kontrolü)
    - [if-else-elif](#if-else-elif)
    - [case](#case)
    - [while-do Döngüsü](#while-do-döngüsü)
    - [until-do Döngüsü](#until-do-döngüsü)
  - [Fonksiyonlar](#fonksiyonlar)
    - [Değişlenleri Geçerlilikleri](#değişlenleri-geçerlilikleri)
    - [Geri Dönüş Değeri](#geri-dönüş-değeri)
    - [Argüman Göndermek](#argüman-göndermek)
  - [Ekler](#ekler)
    - [date komutu](#date-komutu)
    - [declare komutu](#declare-komutu)
    - [echo komutu](#echo-komutu)
    - [let komutu](#let-komutu)
    - [man komutu](#man-komutu)
    - [printf komutu](#printf-komutu)
    - [read komutu](#read-komutu)
    - [test komutu](#test-komutu)
  

# 21. Unixte kabuk programlama (shell scripting) dilinin temel örneklerle anlatımı

## Shell (Kabuk) nedir?

Basitçe tanımlamak gerekirse komutları klavyeden alan işletim sistemiyle haberleşmemizi sağlayan bir programdır. Eskiden bilgisayarlarla etkileşime girmek için şimdiki gibi grafik kullanıcı arayüzleri (graphical user interface GUI) olmadığından shell gibi komut satırı arayüzleri (command line interface CLI) kullanılıyordu. Hala pek çok işletim sistemini en etkin şekilde kullanmak için kabukla etkileşmek gereklidir. Hatta bu verimi fark eden Microsoft firması da işletim sisteminde yakın zamanda PowerShell kabuğunu geliştirmiştir.

Pek çok Linux çekirdeği kullanan işletim sistemlerinde Steve Bourne tarafından yazılmış olan bash (Bourne Again SHell) programı shell olarak kullanır. Bu program aslında Unix sistemindeki sh shell programının geliştirilmiş halidir.

Script bir dosya içindeki sıralı komutlara denir.

## Kabuk Programları
Kabuk programı aslında bir veya daha fazla komutu barındıran çalışabilir metin bazlı dosyalardır. Herhangi bir zorunluluk olmamasına karşılık sh uzantılı olması adettendir. 

### Çalıştırılabilir dosya
Bir dosyanın çalışabilir yapılması için

```bash
$ chmod +x dosya_ismi
```
Dosyayı çalıştırmak içinse
```bash
$ ./dosya_ismi
```
### Shebang satırı
Pek çok kabuk programı olduğundan yazdığınız kabuk programını belirtmeniz gerebilir. Bunun için Shebang olarak ifade edilen #! karaterlerinden sonra kullanılacak kabuk programının yolu vermek gereklidir.

```bash
which bash
$ /bin/bash
```
komutu ile işletim sisteminide bash programının tam yolunu öğrenip Shebang i doğru şekilde yazabilirsiniz. Genellikle aşağıdaki 
```bash
#!/bin/bash
```
yazarak bash kabuğunu kullandığımızı belirtebiliriz. Eğer unutulursa da belki programını çalışabilir. Herhangi bir hatayı en aza ingirdegemek için yazılması gereklidir.

### Yorum satırları
Kabuk programlarına yorum eklenmek istenirse # kullanılır. İlgili satırda # simgeden sonra gelen komutlar yorum olarak değerlendirilir ve göz ardı edilirler.

## Değişkenler

Belli bir değeri hafıza tutup ona bir isimle ulaşmak için değişkenler kullanırız.
```bash
degisken1=3; degisken2="Deneme" #aynı satırda iki komutu birbirinden ayırabilmek için ; kullanılır.
```
Atama işlemi için kullanılan = operatörünü kullanırken boşluk kullanmamalısınız.
```bash
degisken3=degisken1 # Doğru kullanım
degsiken4 = degisken3 # Yanlış kullanım
```
Pek çok programlama dilinde olduğu gibi değişkenleri isimlendirirken aşağıdaki kurallara dikkat edilmelidir.

- Değişken isimleri rakamla başlayamaz.
- Değişken ismi içerisinde _ dışında karakter bulunamaz.
  
Değişkenlere erişebilmek için **$** işareti kullanılır.

Bir değişkenin değeri ise **echo** veya **printf** komutu ile ekrana yazdırılır.
```bash
$ echo Yukarıda değişkenlere atanan değerler $degisken1 ve $degisken2 dir.
Yukarıda değişkenlere atanan değerler 3 ve Deneme dir.
```

## Parametreler
### Argüman Parametresi
Komut satırındaki argümanlar numaralandırılırlar. İlk arguman $1 ikincisi $2 diye devam eder.

merhaba.sh 
```bash
printf "Merhaba, %s\n" "$1"
```
Bu programı çalıştırdığımızda 

```bash
$ ./merhaba.sh Hakan
Merhaba, Hakan
$ ./merhaba.sh Ömer
Merhaba, Ömer
```

### Özel Karakter Parametresi
$* ve $@ tüm argümanları gösterirken, $$ programın proses ID sini (PID) ve $?  son çalışan programın çıkış değerini gösterir.

### Aritmetik işlemler

Aritmetik işlemler için eval veya let komutu kullanılır.
```bash
$ let "carpim=2*7"
$ echo $carpim
14
```
```bash
$ declare -i sonuc # sonuc isimli tam sayı değişkeni tanımlandı.
$ a=100; b=56 # aynı satırda iki komutu birbirinden ayırabilmek için ; kullanılır.
$ sonuc = a*b
$ echo $sonuc
5600
```
### $( ) ve <() Operatörleri

Bir komutun çıktısını kullanmak için **$( )** size yardımcı olacaktır.
```bash
$ echo "Bugün'ün tarihi $(date) dir."
Bugün'ün tarihi Thu 03 Dec 2020 03:24:44 AM +03 dir.
```
Bir komutun çıktısını geçiçi bir dosya yazıp bunu girdi olarak bir programa verme için **<( )** kullanılır.

```bash
$ more <(ls ~/)
```
Çıktısı

    dosya1
    dosya2
    dosya3

Burada **more** komutu bir çıktının sayfa sayfa gösterilmesini sağlar. **~** kullanıcı dizinini ifade eder. **ls** komutu ise ilgili dizindeki dosyaları listeler.


### Mantıksal Operatörler

|Operatör|Anlamı     |Örneği    |
|:------:|:----------|:--------:|
|-a     |ve      | şart1 -a şart2 |
|-o     |veya      | şart1 -o şart2|
|!     |değil | ! şart| 

### Aritmetik Karşılaştırma
|Operatör|Anlamı     |Örneği    |Açıklaması|
|:------:|:----------|:--------:|:--------:|
|-gt     |büyük      | $a -gt $b| a > b    |
|-lt     |küçük      | $a -lt $b| a < b    |
|-ge     |büyük eşit | $a -ge $b| a >= b   |
|-le     |küçük eşit | $a -le $b| a <= b   |
|-eq     |eşit       | $a -eq $b| a == b   |
|-ne     |eşit değil | $a -ne $b| a != b   |
 
### Dizi (String) Karşılaştırma
|Operatör|Anlamı        |Örneği    |Açıklaması|
|:------:|:-------------|:--------:|:--------|
|-z      |boş dizi      | -z Metin | Metin dizisinin uzunluğu sıfır ise    |
|-n      |tanımlı dizi  | -n Metin | Metin dizisinin uzunluğu sıfır değilse|
|=       |eşit diziler  | Metin1 = Metin2 | Metin1 dizisi Metin2 dizisine eşitse   |
|!=      |farklı diziler| Metin1 != Metin2 | Metin1 dizisi Metin2 dizisine eşit değilse |

### Dosya Karşılaştırma
|Operatör|Anlamı        |Örneği    |
|:------:|:-------------|:--------:|
|-a      |dosya var      | -a dosyaadı |
|-e      |dosya var      | -e dosyaadı |
|-f      |dosya var      | -f dosyaadı |
|-s      |dosya boş değil  | -s dosyaadı | 
|-r      |dosya okunabilir  | -r dosyaadı |
|-w      |dosya yazılabilir|  -w dosyaadı |
|-x      |çalıştırabilir dosya| -x dosyaadı | 
|-h      |sembolik bağlantı| -h dosyaadı | 
|-c      |karakter aygıt| -c dosyaadı | 
|-b      |blok aygıt|  -b dosyaadı | 
|-nt     |Yeni(değiştirilme tarihi) dosya| Dosya1 -nt Dosya2 |
 
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

```bash
read sayi
if [ sayi -lt 100 ]
then 
    echo "Girilen sayi 100 den küçüktür."
elif [ sayi -lt 0 ]
    echo "Girilen sayı negatiftir."
else
    echo "Girilen sayı 100 den büyüktür."
fi
```
### case 

    case anahtar in 
        secenek1)
                komutlar;;
        secenek2)
                komutlar;;
        *)
                komutlar;;
    esac
```bash
echo -n "Bir ders ismi giriniz:"
read DERS
echo -n "$DERS isimli ders "
case $DERS in 
    fizik | matematik | kimya) echo -n "dört";;
    programlama | veritabanı) echo -n "beş";;
    *) echo -n " bilmediğim ";;
esac
echo " ders saatindedir."
```
### while-do Döngüsü

```bash
while [ şart ]
do
    komutlar
done
```

```bash
sayi=1
while [ $sayi -le 5 ]
do
    echo "$sayi. sayi"
    let sayi=sayi+1
done

### for-do Döngüsü

```bash
for deger in liste
do
    komutlar
done
```
ve C diline benzer şekilde

```bash
#for (( altsınır; şart; artım ))
for (( n=1; n<=5; ++n ))
do
    komutlar
done
```
### until-do Döngüsü

```bash
until [ şart ]
do
    komutlar
done
```

## Fonksiyonlar

Fonksiyonlar, büyük bir programın alt parçaları olarak düşünülebilir.

```bash
fonksiyon_ismi(){
    komutlar
}
```

### Değişlenleri Geçerlilikleri

```bash
degisken1=1
degisken2=2
fonksiyon () {
    local degisken1=5
    degisken2=6
    echo "Fonksiyon içindeki degisken1: $degisken1, degisken2: $degisken2"
}

echo "Fonksiyon çağrılmadan önceki degisken1: $degisken1, degisken2: $degisken2"

fonksiyon
echo "Fonksiyon çağrıldıktan sonraki degisken1: $degisken1, degisken2: $degisken2"
```

### Geri Dönüş Değeri
```bash
fonksiyon () {
    return 10
}

fonksiyon
echo $?
```
veya

```bash
fonksiyon () {
    sonuclar="1 2 3 4"
}
fonksiyon
echo $sonuclar
```
Çıktısı

    1 2 3 4

### Argüman Göndermek

Fonksiyon isminden sonra gelen argümanlar için sırasıyla $1, $2, ... , $(10), ... $n

$# kaç tana argüman gönderildiğinin sayısını göstermektedir.

```bash
selam () {
    echo "Merhaba $1"
}

selam "Hakan"
```

Çıktısı

    Merhaba Hakan

## Ekler

### date komutu

Tarih ve saati gösteren ve ayarlamanıza yarayan komuttur.
```bash
$ date
Thu 03 Dec 2020 03:24:44 AM +03
```
### declare komutu

Değişkenlerin değer ve özelliklerinin tanımlanması için kullanılır. typeset komutu declare komutunun takma adıdır.
```bash
declare -i degisken
degisken = "3**3"
echo $degisken
```
### echo komutu

Argumanlarını standart çıkışa yazan bir programıdır.
```bash
$ echo Merhaba 
```

### let komutu
Matematiksel ifadelerin hesaplanması için kullanılır. Bash küsüratlı sayıları desteklemediğin sadece tam sayılarla işlemler yapılır.
```bash
$ let "carpim=2*7"
$ echo $carpim
14
```

### man komutu

Belkide en çok kullanacağız komut olan **man** manual pages (kullanım sayflarına) ulaşmanızı sağlayan komuttur.
```bash
$ man echo
```
Çıkmak için **q** tuşuna basmayı unutmayın.

### printf komutu

C'deki kullanıma oldukça benzeyen biçimli çıktı komutudur.
```bash
print format [argumanlar ...]
```
Bir diziyi (string) yazdırmak için
```bash
$ printf "%s\n" hello
hello
```

### read komutu

Klavyeden bir giriş yapmak için kullanılır.
```bash
$ read DENEME
Ali
$ echo Merhaba $DENEME
Merhaba Ali
```

### test komutu
Bir şartı hesaplar. Eğer şart doğruya 0 diğer durumlarda ise 1 döndürür.
```bash
$ test 5 -lt 3
$ echo $?
1
$ test 5 -lt 3 && echo "Hayır 5 3den küçük değil" || echo "Evet 5 3den küçük"
Hayır 5 3de küçük
```
