---
title:  Jak si zahrát Dobyvatele v moderním Firefoxu, který už nepodporuje Flash?
date:   2018-10-17 01:41 +0200
tags:   [dobyvatel, flash, firefox]
---
Nad _Flashem_ se stahují mračna. Jeho podpora z aktuálních verzí webových prohlížečů mizí -
v tento okamžik už dávno nenajdete na [addons.firefox.com](https://addons.mozilla.org)
žádné _Flash player_ rozšíření pro Firefox a pokud vím, podobná situace je i u ostatních
prohlížečů (např. Chrome). Co když ale nutně _Flash_ plugin v prohlížeči potřebujeme
(např. proto, že si chceme zahrát [Dobyvatele][1]), ale nechce se nám stahovat a instalovat
nějaký starodávný prohlížeč? Naštěstí stále existuje způsob, jak manuálně Flash plugin do
prohlížeče dostat.

V tomto článku vám předvedu, jak nainstalovat nejnovější verzi Flashe do
_Firefoxu 62.0b16 (64-bit)_ ([release notes][2]), což je v okamžik psaní článku jedna z nejnovějších
verzí Firefoxu, a to v _Linuxu_ (konkrétně v operačním systému _Debian 9_).

## 1) Stáhnout nejnovější _Flash_ z oficiálních stránek a rozbalte archiv

* [Stáhnout _Adobe Flash Player_ z oficiálních webových stránek][3]

Na uvedený odkaz klikněte a rozklikněte rozbalovací menu _"Select version to download..."_.
Z nabízených možností vyberte _".tar.gz for Linux"_. Potom klikněte vpravo na tlačítko _"Download now"_.

Stažený archiv rozbalte. Pro nás jsou teď zajímavé pouze tyto věci:

* Složka `usr`
* Soubor `libflashplayer.so`

## 2) Zkopírujte `libflashplayer.so` do adresáře Firefoxu pro pluginy

Nyní musíte samotný plugin - v podobě knihovny `libflashplayer.so` - nakopírovat na to správné místo,
tj. do složky Firefoxu, která je určená pro pluginy a kde si Firefox pluginu všimne
a načte jej.

Konkrétně se jedná o složku: `/usr/lib/firefox/browser/plugins`. Pokud náhodou složka `plugins`, případně
`browser` neexistuje, tak je nejprve zkusíme vytvořit. Je tedy potřeba spustit tyto dva příkazy:

```sh
sudo mkdir -p /usr/lib/firefox/browser/plugins
sudo cp libflashplayer.so /usr/lib/firefox/browser/plugins/
```

## 3) Nakopírujte obsah složky `usr` do kořenového adresáře systému `/usr`

Po nainstalování `libflashplayer.so` už nás dělí jen poslední krok od cíle. Musíme spustit příkaz:

```sh
sudo cp -r usr/* /usr
```

Tento příkaz rekurzivně nakopíruje obsah složky `usr` pluginu do kořenového adresáře `/usr`

## 4) Restartujte / spusťte Firefox a vyzkoušejte, zda _Flash_ plugin funguje

Pokud jste vše udělali podle tohoto návodu, nyní by vám měl Flash ve Firefoxu fungovat.
Takže si například můžete zase zahrát na počítači [Dobyvatele][1]!

[1]: https://dobyvatel.nova.cz
[2]: https://www.mozilla.org/en-US/firefox/62.0/releasenotes
[3]: https://get.adobe.com/flashplayer/
