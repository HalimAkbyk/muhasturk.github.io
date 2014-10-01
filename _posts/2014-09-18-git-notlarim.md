---
layout: post
title: "Git Notlarım"
modified:
categories: 
excerpt: Kaynak kod yönetim aracı olan açık kaynak 'git' ile ilgili notlarımı paylaşıyorum.
tags: [git, scm, open, source, code]
image:
  feature:
date: 2014-09-18T14:47:08+03:00
---


[Linus Torvalds][linus-wikipedia] bize harika bir kaynak kod yönetim aracı olan [git][git]'i sunmuş. Bende [git][git] ile ilgili notlarımı buraya düşeceğim.

### Terimler
**staging area**  
dosyaları commit ile snapshot almadan önce bulunduğu yer, sahne.

**tracked files**
git add ile izlenmeye alınmış dosyalar

**untracked files**
git add ile izlenmeye alınmamış dosyalar

**commit**
depomuzun timeline ındaki snapshotlara commit deniliyor.

**HEAD**
her zaman geçerli branchi gösteren pointer gibidir. Dal üzerindeki son commiti gösterir.

**HEAD^**
geçerli HEAD den bir önceki parent commiti işaret eder

**HEAD~n**
geçerli HEAD den n önceki commiti işaret eder.


### Yardım Alma
    git help
    git help <command>

### Git İnit - Depo Oluşturmak
    git init
lokalde git deposu oluşturmak için.

    git init <directory>
verilen dizinde git deposu oluşturmak için
     
    git clone <repo>
verilen URL deki depoyu locakde çalışılan klasörün içine çeker

    git clone <repo-URLlock> <directory>
verilen URL deki depoyu verilen klasöre çeker.
    
    git status
git çalışma alanındaki durumu görmek için

### Git Add - İzlemeye Başlamak
Çalışma alanındaki izlenmemiş untracked dosyaları izlemesini git e söyleriz. Eklenen dosyalar staging area da olur.

`git add "*.md"` şeklindeki bir kullanım ile tüm projede verilen uzantılı dosyaları izlemeye başlar. 
`git add --all` veya `git add -A` ile silinen veya değiştirilmiş dahil tüm dosyalar staging area ya eklenir.

### Git Commit - Snapshot Almak

Staging area da bulunan izlenen dosyaların snapshot ını almak için kullanıyoruz.

Commit mesajları yazılırken geniş zamanda belirtmek iyi bir alışkanlıktır.

### Git Log - Log Kayıtlarını Görüntülemek
    git log
yapılan commit loglarını görüntülemek için   

    git log -n <limit>
verilen sayı kadar sınırlandırılmış commit log unu gösterir.   

    git log --oneline
commitleri tek satırda gösterir.
   
    git log --stat
standart çıktıdan farklı olarak committen etkilenen dosyaları gösterir.   

    git log -p
ayrıntılı diff dökümanı ile birlikte görüntüler.   

    git log --author="<pattern>"
verilen pattern ile geçerli yazarlardaki commitleri gösterir. Düz metin olabileceği gibi regex de verilebilir.

    git log --grep="<pattern>"
verilen pattern ile commit mesajında eşleşen loglar gösterilir. Düz metin olabileceği gibi regex de verilebilir.

    git log <since>..<until>
verilen iki referans arasındaki logları gösterir.  
 
    git log <file>
verilen dosya ile ilişkili commit logları bastırılır.

    git log --graph
metin tabanlı grafikler ile ayrıntılı log çıktısı verir.

    git log --decorate
commitlerin referans isimleri ile birlikte gösterir.
    
    git log --summary
etkilenen dosyaları log çıktısında gösterir.

    git log --pretty=<command>
ile çıktılara detay verilebilir.

    git log --until=1.minute ago 
    git log --since=2.day ago
ile zaman aralığı vererek çıktıyı daraltabiliriz.

### Git Diff - Farkı Görmek
Bu komut ile commitler, branchler arasında ki farklılıkları görebiliriz.

    git diff HEAD
geçerli durum ile son commit arasındaki farkı gösterir.

    git diff <SHA1>..<SHA2>
hash değeri verilmiş iki commit arasındaki farkı gösterir.

    git diff <branchName> <otherBrachName>
farklı branchler arasındaki farklılığı da görebiliyoruz.

### Git Checkout

Brancler veya çalışma alanı üzerindeki commitler üzerinde hareket etmeyi sağlar.  

**Branch değiştirmek**

    git checkout <existing-branch>
ile varolan dala geçilebilir.

    git checkout -b <new-branch>
verilen dal oluşturulduktan sonra o dala geçiş yapılır.


**Belli bir commite geçmek**

    git checkout <commit>
ile hash değeri veya etiketi verilen commit anına geri dönülür.

**Belli  bir committeki dosyaya geçmek**

    git checkout <commit> <file>
ile hash değeri veya etiketi verilen commit deki dosyanın halini çalışma alanına yükler.



### Git Remote - Remote ile Çalışmak

Remote verilen ad herhangi birşey olabilir ama ana depo için *origin*, veya github hesap adı iyi alışkanlıktır.

**Remote listelemek**
    
    git remote
ile sadece isimleri listelenir iken

    git remote -v
adresleri ile birlikte listeler.         

**Remote eklemek**

    git remote add <RemoteName> <URL>
    
**Remote silmek**

    git remote rm <remoteName>
    
**Remote yeniden adlandırmak**

    git remote rename <oldName> <newName>
    
**Remote ile gösterilen adresi değiştirmek**

    git remote set-url <RemoteName> <URL>
    
### Git Branch - Dallar ile Çalışmak

**Tüm brancleri listelemek**

    git branch -a

**Local brancleri listelemek**
 
    git branch -l
    
**Remote brancleri listelemek**

    git branch 
veya

    git branch -r
        
**Branch eklemek**

    git branch <newBranch>
Bu komut ile oluşturulan dala geçilmez.

    git checkout -b <newBranch>
ile yeni dal oluşturulur ve oluşturulan dala geçilir.    
 
   
**Local branch silmek**

    git branch -d <BranchName>
Güvenli silme modudur. Eğer merge edilmemiş değişiklikler varsa git silme işlemini engeller.

    git branch -D <BranchName>
Merge edilmemiş değişiklikler olsa bile dalı siler. Force modudur.  
  

**Remote branch silmek**

    git push <remoteName> :<RemoteBranch>

**Branch'i yeniden adlandırmak**

    git branch -m <newBranchName>
Geçerli dalın adını değiştirir.

### Git Push - Uzağa gönderme

**Oluşturulan branch'i remote a atmak**
    
    git push <remoteName> <branchName>
ile local ve remote branch isimleri aynı olur ve localdeki branch remote a gönderilmiş olur.

    git push -u <remoteName> <branchName>
*-u* parametresi argümanları hatırlar bir sonraki göndermede branch ve remote adı verilmesine gerek kalmaz.

    git push <remoteName> <localBranchName>:<remoteBranchName>
ile localdeki branch remote a verilen isim ile aktarılır.


    
### Git Config - Yapılandırma 

Git ayar dosyaları sistemde 3 farklı konumda bulunur.  

* <repo>/.git/config – Depoya özel ayar dosyası.
* ~/.gitconfig – Kullanıcı tanımlı ayar dosyası. --global bayrağı ile ayarlanır.
* $(prefix)/etc/gitconfig – Sistem genelindeki ayar dosyası   
    
Eğer bu üç ayar dosyası birbiri ile çakışır ise kullanıcı ayar dosyası sistem genelindekini, depoya özel ayar dosyası da
kullanıcıya özel ayar dosyasını ezer.

##### Bayraklar
**`--local`** ile depoya özgü,  
**`--global`** ile kullanıcıya özgü,  
**`--system`** ile sistem genelindeki ayarı değiştirir.  
  

    git config --global user.name <name>
    git config --global user.email <email>
    git config --global color.ui true

```
git config --system core.editor <editor>
```

ile git komutları tarafından kullanılan metin edötörü belirlenir. Bu editör konsoldan çağrılabilen bir komut olmalıdır.

    git config --global --edit
global ayar dosyasını düzenlemek için açar

```
git config --global alias.<alias-name> <git-command>
```
ile git komutlarına alias atanabilir.

    git config --list
ile tüm ayarlar listelenebilir.


### Git Blame - Suçlamak

Proje genişledikçe kod üzerinde yer alan değişikliği satır satır kimin gerçekleştriğini görebiliyoruz.

    git blame <file>
ile verilen dosyada satır satır değişikliğin kimin yaptığını görüp suçlama yapabiliyoruz.

    git blame <file> --date=short
tarih kısmını biraz daha kısa tutabiliyoruz.

    
### Dışlamak
Proje üzerinde çalıştığımız bazı dosyaların git tarafından izlenmesini hiçbir zaman istemeyiz ve dışlamak isteriz.
Localde bunu yapmak için `.git/info/exclude` dosyasına dışlamak istediğimiz dosya veya dizinleri ekliyoruz.

Dışlamak istediğimiz dosyaların genel geçer olması ve proje üzerinde çalışan herkes için geçerli olmasını istiyor isek
proje ana klasöründe oluşturduğuuz `.gitignore` dosyasına dışlamak istediğimiz dosya veya klasör isimlerini ekleyoruz.


[linus-wikipedia]: http://en.wikipedia.org/wiki/Linus_Torvalds "Linus Torvalds on wikipedia"
[git]: http://git-scm.com/ "git-scm offical website"

#### Kaynaklar
* [Git Real](https://www.codeschool.com/courses/git-real)  
Ücretli bir eğitim serisi ancak çok kaliteli. Bu eğitimin slaytlarına [buradan](https://yadi.sk/i/PIk4gRTnbiDg4)
erişebilirsiniz. Videoları da internette bulabilirsiniz.






























