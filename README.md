# VERDACCIO Kurulumu
NPM, Node.js için oluşturulmuş bir paket yöneticisi olmakla beraber çeşitli 3. parti kullanımlar için de paket yönetimini sağlamaktadır. Angular Framework de bu paket yöneticisini kullanmaktadır. Bununla beraber, geliştirilen Angular uygulamaları da NPM’de publish edilebilmektedir. Publish edilen kod private olmadığı için kod herkese açık bulunmaktadır. Bunu önlemek için çeşitli seçenekler mevcuttur. Bunlardan ilki NPM’den premium hizmet (kullanıcı başına ayda 7 $) satın almaktır. İkinci seçenek ise, kendi NPM sunucunuzu kurmaktır. Verdaccio bu hizmeti sunan open-source bir NPM server alternatifidir.



## Yerel Makina Kurulumu
Konsoldan: 
```npm install --global verdaccio```


Uygulamayı çalıştırmak içinse, konsoldan verdaccio komutunu çalıştırmak yeterlidir. Default olarak verdaccio 4873 portunda çalışmaktadır. Çalışan uygulamayı görmek için http://localhost:4873 adresine yönlenmek yeterlidir.

Docker Kurulumu
Docker hub üstünden verdaccio kurulumu için

1. Konsoldan:
```
$ docker pull verdaccio/verdaccio
$ docker run -it --rm --name verdaccio -p 4873:4873 verdaccio/verdaccio
```
2. Kitematic üstünden:
![image](https://user-images.githubusercontent.com/261946/75019156-72c1e900-54a1-11ea-8f1d-9722d1180e77.png)

Kurulduktan sonra ilgili porttan giriş yaparak browser üstünden yüklü paketleri görebilirsiniz.
![image](https://user-images.githubusercontent.com/261946/75019228-92591180-54a1-11ea-81ca-75b91dfe3032.png)

![image](https://user-images.githubusercontent.com/261946/75019278-a56be180-54a1-11ea-93bb-ba44f3068c6f.png)



Örnek Paket Yayını
Özetle aşağıdaki komutları çalıştırıyoruz:

Proje klasörü oluştur ve klasöre git
md VerdaccioTest
cd VerdaccioTest 

Node projesi başlat
npm init --scope=@cemt
VS Code ile projeyi açıp index.js dosyasını düzenle
code .
Proje klasöründe konsol üstünden verdaccio üstünde çalışabilecek kullanıcı adı ve şifresini tanımla
npm adduser --registry http://192.168.99.100:4873
Paketi yayınla
npm publish --registry http://192.168.99.100:4873

```
C:\Temp
# md VerdaccioTest
 
C:\Temp
# cd VerdaccioTest
 
C:\Temp\VerdaccioTest
# npm init --scope=@cemt
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.
 
See `npm help json` for definitive documentation on these fields
and exactly what they do.
 
Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.
 
Press ^C at any time to quit.
package name: (@cemt/verdacciotest)
version: (1.0.0)
description: verdaccio için ilk test paketi
entry point: (index.js)
test command:
git repository:
keywords: verdaccio test
author: Cem Topkaya
license: (ISC)
About to write to C:\Temp\VerdaccioTest\package.json:
 
{
  "name": "@cemt/verdacciotest",
  "version": "1.0.0",
  "description": "verdaccio için ilk test paketi",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [
    "verdaccio",
    "test"
  ],
  "author": "Cem Topkaya",
  "license": "ISC"
}
 
 
Is this OK? (yes)
 
C:\Temp\VerdaccioTest
# code .
 
C:\Temp\VerdaccioTest
# npm adduser --registry http://192.168.99.100:4873
Username: cemt
Password:
Email: (this IS public) cem.topkaya@cemtopkaya.com
Logged in as cemt on http://192.168.99.100:4873/.
 
C:\Temp\VerdaccioTest
# npm publish --registry http://192.168.99.100:4873
npm notice
npm notice package: @cemt/verdacciotest@1.0.0
npm notice === Tarball Contents ===
npm notice 72B  index.js
npm notice 306B package.json
npm notice === Tarball Details ===
npm notice name:          @cemt/verdacciotest
npm notice version:       1.0.0
npm notice package size:  387 B
npm notice unpacked size: 378 B
npm notice shasum:        8b575538fafe82624fe45682df74d56897443c16
npm notice integrity:     sha512-L8ud2cecT7e9t[...]4TsIl7hxUcoHg==
npm notice total files:   2
npm notice
+ @cemt/verdacciotest@1.0.0
```

Yukarıdaki işlemlerin sonucunda oluşturduğumuz paketi Verdaccio üstünden yayınlamış olduk.





Paketin Yayından Kaldırılması
npm unpublish --force <paket adı> --registry http://192.168.99.100:4873 Komutu kullanılarak yayındaki paket kaldırılabilir.


C:\Temp\VerdaccioTest
# npm unpublish --force @cemt/verdacciotest@1.0.0 --registry http://192.168.99.100:4873
npm WARN using --force I sure hope you know what you are doing.
- @cemt/verdacciotest@1.0.0


publishConfig İle Registry Ayarı
Komut satırında registry ayarı vermemek için package.json içinde aşağıdaki packageConfig tanımı yapılabilir:

{
  "name": "@cemt/verdacciotest",
  "version": "1.0.0",
  "description": "verdaccio için ilk test paketi",
  "main": "index.js",
 
  "publishConfig": {
    "registry":"http://192.168.99.100:4873"
  },
  ....


Artık komut satırında npm publish yeterli olacaktır.



Referanslar:

https://verdaccio.org/
https://hub.docker.com/r/verdaccio/verdaccio
https://docs.npmjs.com/creating-node-js-modules
https://docs.npmjs.com/cli/publish
