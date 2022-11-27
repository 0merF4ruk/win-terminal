![terminal-logos](https://user-images.githubusercontent.com/48369326/115790869-4c852b00-a37c-11eb-97f1-f61972c7800c.png)

# Windows Terminal, Konsol ve Komut Satırı deposuna hoş geldiniz.

Bu depo aşağıdakiler için kaynak kodu içerir:

* [Windows Terminal](https://aka.ms/terminal)
* [Windows Terminal Preview](https://aka.ms/terminal-preview)
* Windows konsolu ana bilgisayarı (`conhost.exe`)
* İki proje arasında paylaşılan bileşenler
* [ColorTool](https://github.com/microsoft/terminal/tree/main/src/tools/ColorTool)
* [Örnek projeler](https://github.com/microsoft/terminal/tree/main/samples)
  Windows Console API'lerinin nasıl kullanılacağını gösterir.

İlgili depolar şunlardır:

* [Windows Terminal Dokümantasyonu](https://docs.microsoft.com/windows/terminal)
  ([Repo: Belgelere katkıda bulunun](https://github.com/MicrosoftDocs/terminal))
* [Konsol API Dokümantasyonu](https://github.com/MicrosoftDocs/Console-Docs)
* [Cascadia Kod Fontu](https://github.com/Microsoft/Cascadia-Code)

## Windows Terminal'i yükleme ve çalıştırma

> **Note**: Windows Terminal için Windows 10 2004 (19041 derlemesi) veya üstü gerekir

### Microsoft Store [Önerilen]

[Microsoft Store'dan Windows Terminali][store-install-link] yükleyin.
Bu, yeni derlemeler yayınladığımızda her zaman en son sürümde olmanızı sağlar otomatik yükseltmelerle.

Bu bizim tercih ettiğimiz yöntemdir.

### Diğer yükleme yöntemleri

#### GitHub aracılığıyla

Windows Terminal'i Microsoft Store'dan yükleyemeyen kullanıcılar için, 
yayınlanan derlemeler bu deponun [Sürümler sayfası](https://github.com/microsoft/terminal/releases) 
adresinden manuel olarak indirilebilir.


`Microsoft.WindowsTerminal_<versionNumber>.msixbundle` dosyasını şu adresten indirin **Assets** bölümünden ulaşabilirsiniz. 
Uygulamayı yüklemek için `.msixbundle` dosyasını yüklediğinizde uygulama yükleyicinin otomatik olarak çalışması gerekir.
Eğer bu herhangi bir nedenle başarısız olursa, PowerShell komut isteminde aşağıdaki komutu deneyebilirsiniz:

```powershell
# NOTE: PowerShell 7+ kullanıyorsanız, lütfen
# Import-Module Appx -UseWindowsPowerShell
# Add-AppxPackage kullanmadan önce.

Add-AppxPackage Microsoft.WindowsTerminal_<versionNumber>.msixbundle
```

> **Note**: Terminal'i manuel olarak yüklerseniz:
>
> * [VC++ v14 Desktop Framework Package](https://docs.microsoft.com/troubleshoot/cpp/c-runtime-packages-desktop-bridge#how-to-install-and-update-desktop-framework-packages) yüklemeniz gerekebilir.  
>   Bu yalnızca Windows 10'un eski sürümlerinde ve yalnızca eksik çerçeve paketleriyle ilgili bir hata alırsanız gerekli olmalıdır.
* Terminal, yeni yapılar yayınlandığında otomatik olarak güncellenmeyecektir, bu nedenle
> en son Terminal sürümünü düzenli olarak yüklemek için
> düzeltmeler ve iyileştirmeler!

#### Windows Paket Yöneticisi CLI (diğer adıyla winget) aracılığıyla


[winget](https://github.com/microsoft/winget-cli) kullanıcıları indirebilir ve yükleyebilir
`Microsoft.WindowsTerminal` dosyasını yükleyerek en son Terminal sürümünü
Paket:
```powershell
winget install --id Microsoft.WindowsTerminal -e
```

#### Chocolatey aracılığıyla (resmi olmayan)

[Chocolatey](https://chocolatey.org) kullanıcıları en son sürümü indirip yükleyebilir
`microsoft-windows-terminal` paketini yükleyerek Terminal sürümü:

```powershell
choco install microsoft-windows-terminal
```

Chocolatey kullanarak Windows Terminal'i yükseltmek için aşağıdakileri çalıştırın:

```powershell
choco upgrade microsoft-windows-terminal
```

Paketi yüklerken/yükseltirken herhangi bir sorun yaşarsanız lütfen
[Windows Terminal paket sayfası](https://chocolatey.org/packages/microsoft-windows-terminal) ve
[Chocolatey triyaj süreci](https://chocolatey.org/docs/package-triage-process).

#### Scoop aracılığıyla (resmi olmayan)

[Scoop](https://scoop.sh) kullanıcıları en son Terminal'i
indirip yükleyebilirler `windows-terminal` paketini yükleyerek yayınlayın:

```powershell
scoop bucket add extras
scoop install windows-terminal
```

Scoop kullanarak Windows Terminal'i güncellemek için aşağıdakileri çalıştırın:

```powershell
scoop update windows-terminal
```

Paketi yüklerken/güncellerken herhangi bir sorunla karşılaşırsanız,
lütfen Scoop Extras bucket'in [sorunlar sayfasında](https://github.com/lukesampson/scoop-extras/issues) 
aynı sorunu arayın veya bildirin Depo.

---

## Windows Terminal Yol Haritası

Windows Terminali için plan [burada açıklanmıştır](/doc/roadmap-2022.md) 
ve proje ilerledikçe güncellenecektir.

## Proje Yapı Durumu

Proje|Yapı Durumu
---|---
Terminal|[![Terminal Yapı Durumu](https://dev.azure.com/ms/terminal/_apis/build/status/terminal%20CI?branchName=main)](https://dev.azure.com/ms/terminal/_build?definitionId=136)
ColorTool|![Colortool Yapı Durumu](https://microsoft.visualstudio.com/_apis/public/build/definitions/c93e867a-8815-43c1-92c4-e7dd5404f1e1/17023/badge)

---

## Terminal & Konsola Genel Bakış

Lütfen aşağıdaki genel bakışı incelemek için birkaç dakikanızı ayırın. Kod:

### Windows Terminal

Windows Terminal, komut satırı kullanıcıları için yeni, modern, zengin özelliklere sahip, üretken bir terminal uygulamasıdır.
Windows komut satırı topluluğu tarafından en sık talep edilen sekme desteği, zengin metin, küreselleştirme, yapılandırılabilirlik, 
temalandırma ve stil oluşturma ve daha birçok özelliği içerir.

Terminalin aynı zamanda hedeflerimizi ve tedbirlerimizi karşılaması gerekecektir. 
Hızlı ve verimlidir ve büyük miktarda bellek veya güç tüketmez.

### Windows Konsol Ana Bilgisayarı

Windows Console host, `conhost.exe`, Windows'un orijinal komut satırı kullanıcı deneyimidir. 
Aynı zamanda Windows'un komut satırı altyapısını ve Windows Konsol API sunucusu, girdi motoru, işleme motoru, 
kullanıcı tercihleri vb. Kullanıcı tercihleri Bu depodaki konsol ana bilgisayar kodu, 
konsol ana bilgisayarının Windows'un kendisinde `conhost.exe` oluşturulmuştur.


Ekip, 2014 yılında Windows komut satırının sahipliğini aldığından beri Konsola arka plan şeffaflığı, 
satır tabanlı seçim, [ANSI / Sanal Terminal dizileri](https://en.wikipedia.org/wiki/ANSI_escape_code) 
desteği, [24-bit color](https://devblogs.microsoft.com/commandline/24-bit-color-in-the-windows-console/), 
bir [Pseudoconsole
("ConPTY")](https://devblogs.microsoft.com/commandline/windows-command-line-introducing-the-windows-pseudo-console-conpty/) 
ve daha fazlası.

Ancak, Windows Console'un birincil amacı geriye dönük uyumluluğu nedeniyle, topluluk tarafından talep edilen birçok özelliği ekleyemedik.
(ve ekibin) son birkaç yıldır sekmeler de dahil olmak üzere istedikleri, unicode metin ve emoji.

Bu sınırlamalar bizi yeni Windows Terminalini yaratmaya yöneltti.

> Genel olarak komut satırının evrimi hakkında daha fazla bilgi edinebilir ve
> Windows komut satırı özellikle [bu blog serisine eşlik eden
> posts](https://devblogs.microsoft.com/commandline/windows-command-line-backgrounder/)
> Command-Line ekibinin blogunda.

### Paylaşılan Bileşenler

Windows Console'u elden geçirirken, kod tabanını önemli ölçüde modernize ettik,
mantıksal varlıkları modüllere ve sınıflara temiz bir şekilde ayırdık, bazı önemli genişletilebilirlik noktaları ekledik, birkaç eski, 
evde yetiştirilen koleksiyonu ve daha güvenli, daha verimli [STL] ile konteynerler containers](https://docs.microsoft.com/en-us/cpp/standard-library/stl-containers?view=vs-2022) ve Microsoft'un [Windows Implementation Libraries - WIL](https://github.com/Microsoft/wil) 
kullanarak kodu daha basit ve güvenli hale getirmiştir.

Bu revizyon, Console'un temel bileşenlerinden birkaçının 
Windows'taki herhangi bir terminal uygulamasında yeniden kullanılabilmesiyle sonuçlandı. 
Bu bileşenler şunları içerir
yeni DirectWrite tabanlı metin düzeni ve işleme motoru,
aşağıdakileri yapabilen bir metin tamponu hem UTF-16 hem de UTF-8 depolamak, 
bir VT ayrıştırıcı / verici ve daha fazlası.

### Yeni Windows Terminali Oluşturma

Yeni Windows Terminal uygulamasını planlamaya başladığımızda, aşağıdakileri araştırdık ve 
çeşitli yaklaşımları ve teknoloji yığınlarını değerlendirdik. Sonunda şuna karar verdik
hedeflerimize en iyi şekilde C++ kod tabanımıza yatırım yapmaya devam ederek ulaşabileceğimizi düşünüyoruz, 
Bu da bize yukarıda bahsedilen modernize edilmiş bileşenlerini hem mevcut Konsolda hem de yeni Terminalde kullanıyoruz. 
Ayrıca, biz bu sayede Terminalin çekirdeğinin büyük bir kısmını kendimiz inşa edebileceğimizi fark ettik. 
Başkalarının kendi uygulamalarına dahil edebileceği yeniden kullanılabilir bir UI kontrolü.

Bu çalışmanın sonucu bu repoda yer almakta ve Microsoft Store'dan veya  indirebileceğiniz Windows Terminal uygulaması olarak sunulmaktadır.
[doğrudan bu reponun sürümlerinden](https://github.com/microsoft/terminal/releases).

---

## Kaynaklar

Windows Terminal hakkında daha fazla bilgi için bu kaynaklardan bazılarını yararlı ve ilginç bulabilirsiniz:

* [Komut Satırı Blogu](https://devblogs.microsoft.com/commandline)
* [Komut Satırı Arka Plan Bilgisi Blog Serisi.](https://devblogs.microsoft.com/commandline/windows-command-line-backgrounder/)
* Windows Terminal Başlatma: [Terminal "Sizzle Video"](https://www.youtube.com/watch?v=8gw0rXPMMPE&list=PLEHMQNlPj-Jzh9DkNpqipDGCZZuOwrQwR&index=2&t=0s)
* Windows Terminal Başlatma: [Build 2019
  Session](https://www.youtube.com/watch?v=KMudkRcwjCw)
* Radyo Olarak Çalıştır: [Show 645 - Windows Terminal with Richard
  Turner](https://www.runasradio.com/Shows/Show/645)
* Azure Devops Podcast: [Bölüm 54 - Kayla Cinnamon ve Rich Turner Windows Terminalinde DevOps üzerine](http://azuredevopspodcast.clear-measure.com/kayla-cinnamon-and-rich-turner-on-devops-on-the-windows-terminal-team-episode-54)
* Microsoft Ignite 2019 Session: [Modern Windows Komut Satırı: Windows Terminal - BRK3321](https://myignite.techcommunity.microsoft.com/sessions/81329?source=sessions)

---

## SSS

### Yeni Terminali kurdum ve çalıştırdım, ancak tıpkı eski konsol gibi görünüyor.

Nedeni: Visual Studio'da yanlış çözümü başlatıyorsunuz.

Çözüm: `CascadiaPackage` projesini oluşturduğunuzdan ve dağıttığınızdan emin olun. Visual Studio.

> **Not**: `OpenConsole.exe` sadece yerel olarak oluşturulmuş bir `conhost.exe`dir, klasik
> Windows'un komut satırı altyapısını barındıran Windows Konsolu. OpenConsole
> Windows Terminal tarafından komut satırına bağlanmak ve komut satırıyla iletişim kurmak için kullanılır
> uygulamalar (aracılığıyla
> [ConPty](https://devblogs.microsoft.com/commandline/windows-command-line-introducing-the-windows-pseudo-console-conpty/)).

---

## Dokümantasyon

Tüm proje belgeleri [aka.ms/terminal-docs](https://aka.ms/terminal-docs) adresinde yer almaktadır.
Eğer isterseniz belgelere katkıda bulunmak için lütfen [Windows Terminal Dokümantasyon deposu](https://github.com/MicrosoftDocs/terminal).

---

## Katkıda Bulunmak

Sizlerle, muhteşem topluluğumuzla birlikte çalışmaktan heyecan duyuyoruz. Windows Terminal\'i geliştirin!

***Bir özellik/düzeltme üzerinde çalışmaya başlamadan ÖNCE***, lütfen okuyun ve [Katılımcının
Kılavuz](https://github.com/microsoft/terminal/blob/main/CONTRIBUTING.md) adresine boşa harcanan 
veya mükerrer çabaları önlemeye yardımcı olur.

## Ekiple İletişim Kurmak

Ekip ile iletişim kurmanın en kolay yolu GitHub sorunlarıdır.

Lütfen yeni sorunları, özellik isteklerini ve önerileri dosyalayın, 
ancak **DO Yeni bir sorun oluşturmadan önce önceden var olan benzer açık/kapalı sorunlar.**

Eğer bir sorunu gerektirmediğini düşündüğünüz bir soru sormak isterseniz (henüz), 
lütfen bize Twitter üzerinden ulaşın:

* Kayla Cinnamon, Program Yöneticisi:
  [@cinnamon\_msft](https://twitter.com/cinnamon_msft)
* Dustin Howett, Mühendislik Lideri: [@dhowett](https://twitter.com/DHowett)
* Mike Griese, Kıdemli Geliştirici: [@zadjii](https://twitter.com/zadjii)
* Carlos Zamora, Geliştirici: [@cazamor_msft](https://twitter.com/cazamor_msft)
* Pankaj Bhojwani, Geliştirici
* Leonard Hecker, Geliştirici: [@LeonardHecker](https://twitter.com/LeonardHecker)

## Geliştirici Rehberliği

## Ön Koşullar

* Çalıştırmak için Windows 10 2004 (yapı >= 10.0.19041.0) veya üstünü çalıştırıyor olmanız gerekir
  Windows Terminali
* Windows Ayarları'nda Geliştirici Modu'nu etkinleştirmelisiniz
  app](https://docs.microsoft.com/en-us/windows/uwp/get-started/enable-your-device-for-development)
  Windows Terminal'i yerel olarak yüklemek ve çalıştırmak için
* PowerShell 7 veya üstü](https://github.com/PowerShell/PowerShell/releases/latest) yüklü olmalıdır
* [Windows 11 (10.0.22621.0)] SDK'sına sahip olmalısınız
  SDK](https://developer.microsoft.com/en-us/windows/downloads/windows-sdk/)
  kurulu
* En az [VS
  2022](https://visualstudio.microsoft.com/downloads/) yüklü
* Aşağıdaki İş Yüklerini VS Installer aracılığıyla yüklemeniz gerekir. Not: Açılış
  VS 2022'deki çözüm [eksik bileşenleri yüklemenizi isteyecektir
  otomatik olarak](https://devblogs.microsoft.com/setup/configure-visual-studio-across-your-organization-with-vsconfig/):
  * C++ ile Masaüstü Geliştirme
  * Evrensel Windows Platformu Geliştirme
  * **Aşağıdaki Bireysel Bileşenler**
    * C++ (v143) Evrensel Windows Platform Araçları
* Test projeleri oluşturmak için [.NET Framework Targeting Pack](https://docs.microsoft.com/dotnet/framework/install/guide-for-developers#to-install-the-net-framework-developer-pack-or-targeting-pack) yüklemeniz gerekir.

## Kod Oluşturma.

Bu depo [git alt modülleri](https://git-scm.com/book/en/v2/Git-Tools-Submodules) için bağımlılıklar. 
Alt modüllerin geri yüklendiğinden veya güncellendiğinden emin olmak için inşaattan önce aşağıdakileri yapın:

```shell
git submodule update --init --recursive
```

OpenConsole.sln, Visual Studio içinden veya komut satırından oluşturulabilir
dizinindeki bir dizi kullanışlı komut dosyası ve araç kullanarak:

### PowerShell ile Oluşturma

```powershell
Import-Module .\tools\OpenConsole.psm1
Set-MsBuildDevEnvironment
Invoke-OpenConsoleBuild
```

### Cmd'de Oluşturma

```shell
.\tools\razzle.cmd
bcz
```

## Çalıştırma & Hata Ayıklama

VS'de Windows Terminalinde hata ayıklamak için `CascadiaPackage` üzerine sağ tıklayın (VS'de
Solution Explorer) ve özelliklere gidin. Hata Ayıklama menüsünde, "Uygulama
süreci" ve "Arka plan görev süreci" öğelerini "Yalnızca Yerel" olarak değiştirin.

Daha sonra Terminal projesini derleyebilmeli ve hata ayıklayabilmelisiniz
<kbd>F5</kbd>. "x64" veya "x86" platformlarından birini seçtiğinizden emin olun - x64
Terminal "Any Cpu" için oluşturulmaz (çünkü Terminal bir C++ uygulamasıdır,
bir C# değil).

> 👉 Terminal'i aşağıdaki komutu çalıştırarak doğrudan başlatamazsınız
> WindowsTerminal.exe. Nedeniyle ilgili daha fazla ayrıntı için bakınız.
> [#926](https://github.com/microsoft/terminal/issues/926),
> [#4043](https://github.com/microsoft/terminal/issues/4043)

### Kodlama Rehberliği

Lütfen kodlama uygulamalarımız hakkında aşağıdaki kısa dokümanları inceleyin.

> 👉 Bu dokümanlarda eksik bir şey bulursanız, katkıda bulunmaktan çekinmeyin
> deponun herhangi bir yerindeki dokümantasyon dosyalarımızdan herhangi biri (veya yeni
> olanlar!)

This is a work in progress as we learn what we'll need to provide people in
order to be effective contributors to our project.

* [Kodlama Stili](https://github.com/microsoft/terminal/blob/main/doc/STYLE.md)
* [Kod Organizasyonu](https://github.com/microsoft/terminal/blob/main/doc/ORGANIZATION.md)
* [Eski kod tabanımızdaki istisnalar](https://github.com/microsoft/terminal/blob/main/doc/EXCEPTIONS.md)
* [WIL'de Windows ile arayüz oluşturmak için faydalı akıllı işaretçiler ve makrolar](https://github.com/microsoft/terminal/blob/main/doc/WIL.md)

---

## Davranış Kuralları

Bu proje, [Microsoft Açık Kaynak Kodunu] benimsemiştir.
Davranış][conduct-code]. Daha fazla bilgi için [Davranış Kuralları
SSS][conduct-FAQ] veya [opencode@microsoft.com][conduct-email] ile iletişime geçin.
ek sorular veya yorumlar.

[conduct-code]: https://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: https://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com
[store-install-link]: https://aka.ms/terminal
