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


[Linus Torvalds][linus-wikipedia] bize harika bir kaynak kod yönetim aracı olan [git'i][git] sunmuş. Bende [git][git] ile ilgili notlarımı buraya düşeceğim.


    git init
lokalde git deposu oluşturmak için.

    git init <directory>
verilen dizinde git deposu oluşturmak için
     
    git clone <repo>
verilen URL deki depoyu locakde çalışılan klasörün içine çeker

    git clone <repo> <directory>
verilen URL deki depoyu verilen klasöre çeker.
    
    git status
git çalışma alanındaki durumu görmek için


### Git Log
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

    git log --graph --decorate
metin tabanlı grafikler ile ayrıntılı log çıktısı verir.

### Git Checkout

Brancler veya çalışma alanı üzerindeki commitler üzerinde hareket etmeyi sağlar.  

**Branch değiştirmek**

    git checkout <branchName>
ile verilen dala geçilebilir.

**Belli bir commite geçmek**

    git checkout <commit>
ile hash değeri veya etiketi verilen commit anına geri dönülür.

**Belli  bir committeki dosyaya geçmek**

    git checkout <commit> <file>
ile hash değeri veya etiketi verilen commit deki dosyanın halini çalışma alanına yükler.





### Remote ile çalışmak

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
    
**Remote da gösterilecek adresi değiştirmek**

    git remote set-url <RemoteName> <URL>
    
### Branch ile çalışmak

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

**Oluşturulan branch'i remote a atmak**
    
    git push <remoteName> <branchName>
ile local ve remote branch isimleri aynı olur.

    git push <remoteName> <localBranchName>:<remoteBranchName>
ile localdeki branch remote a verilen isim ile aktarılır.


    
### Config 

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
    



    



[linus-wikipedia]: http://en.wikipedia.org/wiki/Linus_Torvalds "Linus Torvalds on wikipedia"
[git]: http://git-scm.com/ "git-scm offical website"


