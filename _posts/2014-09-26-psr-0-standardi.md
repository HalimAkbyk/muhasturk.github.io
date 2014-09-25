---
layout: post
title: "PSR-0 Standardı"
modified:
categories: 
excerpt: "'PHP Framework Interop Group' tarafından oluşturalan 'PSR-0' standartları ve örnek uygulamalar."
tags: [php-fig, standard, psr, autoloading, php, code]
image:
  feature:
date: 2014-09-26T01:46:10+03:00
---


## Otomatik Yükleme Standardı
Aşağıdaki tanımlamalar, otomatik yükleyici birlikte çalışabilirliği için yapışık olması gereken zorunlu gereksinimleri
tanımlar.

## Zorunlu Kurallar
* Tam nitelikli bir isim alanı ve sınıfın sahip olması gereken yapı
 `\<Sağlayıcı İsmi>\(<İsim Alanı>\)*<Sınıf İsmi>`
* Her isim alanı üst seviye bir isim alanına sahip olmak zorundadır.
* Her isim alanı arzu ettiği kadar alt isim alanlarına sahip olabilir.
* Her isim alanı ayırıcısı dosya sistemi tarafından yüklenirken `KLASÖR_AYRACINA` dönüştürülür.
* Sınıf ismindeki her `_` karakteri `KLASÖR_AYRACINA` dönüştürülür. İsim alanındaki `_` karakterinin özel bir anlamı
yoktur.
* Tam nitelikli isim alanı ve sınıflar dosya sisteminden yüklendiğinde sonuna `.php` eklenir.
* Sağlayıcı isimleri, isim alanları ve sınıf isimlerindeki alfabetik karakterler büyük veya küçük harfların herhangi bir
 kombinasyonundan oluşaiblir.
 
#### Örnekler 
* `\Doctrine\Common\IsolatedClassLoader` => `/path/to/project/lib/vendor/Doctrine/Common/IsolatedClassLoader.php`
* `\Symfony\Core\Request` => `/path/to/project/lib/vendor/Symfony/Core/Request.php`
* `\Zend\Acl` => `/path/to/project/lib/vendor/Zend/Acl.php`
* `\Zend\Mail\Message` => `/path/to/project/lib/vendor/Zend/Mail/Message.php`

#### İsim Alanı ve Sınıf İsmindeki Alt Çizgi
* `\namespace\package\Class_Name` => `/path/to/project/lib/vendor/namespace/package/Class/Name.php`
* `\namespace\package_name\Class_Name` => `/path/to/project/lib/vendor/namespace/package_name/Class/Name.php`

Burada ayarladığımız standartlar, oto-yükleyici birlikte çalışabilirliği için en küçük ortak payda olmalı.

Otomatik yükleyicilerin rahat birlikte çalışabilmesi için burada ayarladığımız standartlar en küçük ortak payda olmalı.
Bu standartları takip ettiğinizi, PHP 5.3 sınıflarını yükleyebilen örnek SplClassLoader gerçeklemesinden yararlanarak test edebilirsiniz.

The standards we set here should be the lowest common denominator for
painless autoloader interoperability. You can test that you are
following these standards by utilizing this sample SplClassLoader
implementation which is able to load PHP 5.3 classes.


#### Örnek Uygulama

Aşağıdaki örnek fonksiyon, üstte önerilen standartların nasıl otomatik yüklendiğini basitçe gösterir.

```php
<?php

function autoload($className)
{
    $className = ltrim($className, '\\');
    $fileName  = '';
    $namespace = '';
    if ($lastNsPos = strrpos($className, '\\')) {
        $namespace = substr($className, 0, $lastNsPos);
        $className = substr($className, $lastNsPos + 1);
        $fileName  = str_replace('\\', DIRECTORY_SEPARATOR, $namespace) . DIRECTORY_SEPARATOR;
    }
    $fileName .= str_replace('_', DIRECTORY_SEPARATOR, $className) . '.php';

    require $fileName;
}
```

#### SplClassLoader Uygulaması

The following gist is a sample SplClassLoader implementation that can
load your classes if you follow the autoloader interoperability
standards proposed above. It is the current recommended way to load PHP
5.3 classes that follow these standards.

* [http://gist.github.com/221634](http://gist.github.com/221634)

**Terimler ve Çevrisi**  
vendor: sağlayıcı  
namespace: isim alanı  
class: sınıf  



