# Decentralized Communication platform 

cíle: 
- vyrobit tak moc decentralizovanou komunikační platformu, aby nás nemohl ohrozit chat control

jak na to: 
- nejspíš pouźijeme sftp na samotné zprávy ve smyslu, že každý chat je soubor a nové zprávy appendují
- veškerá komunikace je na bázi peer2peer, tedy nejprve musí být navázáno spojení
- spojení se navazuje tak, že musí dva lidi znát svou aktuální IP adresu
- postupně se začnou lidičky seskupovat do houfů, hives
- každé zařízení si udržuje databázi se seznamem známých zařízení - uživatel se identifikuje svým veřejným ssh klíčem, má nějakou IP adresu
- tady je schovaná síla a zároveň slabina: pokud se nějaký uživatel odpojí z internetu a po nějaké době se opět připojí s jinou IP adresou, pošle informaci se svou IP adresou všem svým *kontaktům* dokud je alespoň jeden z nich stále přítomný na stejné IP adrese, odpoví a spojí se. náš znovu připojený uživatel se začne ptát všech se kterými se mu podařilo spojit, na aktuální IP adresy těch, se kterými se mu spojit nepodařilo, dokud neobnoví všechny
- pokud se mu nepodaří s nikým spojit, musí znovu zjistit aktuální IP adresu některého kamaráda a připojit se napřímo. automaticky pak proběhne reconnect všech známých, popsán v předchozím bodě
- nechceme, aby se sítí libovolně šířily IP adresy uživatelů, proto se posílají pouze v navázaném spojení a pouze ty kdy tazatel zná veřejný klíč toho, s kým chce navázat komunikaci
- čim více lidí ve skupince, tím spíš bude reconnect úspěšný - lze přidat pasivního uživatele, server, který bude sloužit pouze jako broker IP adres ve skupince
- zlí útočníci mohou tvrdit, že jsou někdo jiný a tuto informaci rozesílat do světa. na validaci uživatelů slouží jejich private/public keypair.

tedy shrnutí: kompletně decentralizovaná komunikační platforma nevyžadující existenci serveru (ale umožňuje vytvořit lokální, pro potřeby konkrétní skupinky). Spojení jsou navazována na přímo pomocí IP adres. Síť předpokládá, že alespoň jednomu zařízení ze skupiny se nezmění IP adresa dost dlouho na to, aby mohl proběhnout úspěšný reconnect. Takže benefitují velké skupiny.

Hádám, že přidáme možnosti sdílení kontaktů ostatním - manuální - pro navazování nových spojení (musíš mít kamarády, abys mohl mít další).
Taky asi přijdou skupinové chaty, což bude synchronizační výzva sama o sobě.

Něco jsem zapomněl, nebo napsal špatně? Opravte mě!

potenciální obtíže: 
NAT

existující řešení:
- https://briarproject.org/
  Používá TOR, konkrétně Onion Address Service. Tím taky obchází nutnost znát IP adresy ostatních, nebo mít server, který je zná. Za cenu pomalejší služby (prostě tor routing) je to tak moc anonymizovaná síť, jak jen to jde. Jo a zprávy se posílají jen pokud jsou oba sender i receiver online, ledaže by si založili lokální mailbox. Android/F-Droid. Stále se vyvíjí.
- https://tox.chat/
  Připojení přes IP, existují veřejné uzly, kde se ukládá kdo je aktuálně kde připojen (pokud se připojí do uzlu, stávají se viditelní), aby zjistili IP kamaráda a mohli mu/jí psát. Podobný IP systém, jako jsme chtěli my - akorát mají tyhle uzly navíc (ale to by šlo hostovat lokálně). Umí srandičky (videohovory apod), ale dají se stopovat metadata a vytvářet sociální graf (bigtech/nations are capable of that). Není ve vývoji, hotovo. Má různý klienty (asi si můžeme napsat svýho klidně), pro všechny main OS kromě iPhone.
- https://cwtch.im/
  Taky používá tor. Má ofiko aplikace pro normální OS kromě iPhone. Nevím, jak moc aktivní je vývoj (5-months last commit). Vypadá v pohodě, ale ničím nezaujalo (kromě hezkýho videa vysvětlující proč).
- https://tryquiet.org/
  Zatím pouze Alfa release, ale vypadá krásně. Používá Tor, funguje jako discord/slack. Ještě není stable, tak chybí základní věci (např. join multiple communities, DMs). Podporuje všechny standardní OS (díky electronu), plánují přidat i TorBrowser a následně všechny browsery. Aktivní vývoj.
- https://scuttlebot.io/more/protocols/secure-scuttlebutt.html
  Pěknej protokol, mají tam víc různých klientů na tom samym protokolu. Nepoužívá TOR, ale je hodně podobná našemu návrhu, respektive ne tomu finálnímu - mají "bot servery", který mají *veřejnou IP* (proto jsme to zavrhli) a předávají zprávy těm, co jsou právě offline. Taky mají navíc oproti nám rozesílání zašifrovaných zpráv i přes kamarády, my to měli jen jako P2P. Vývoj závisí na klientech, stejně tak podpora OS - ale viděl jsem tam asi všechny.
- https://retroshare.cc/
  Fakt retro. Vypadá jako kombinace toru a serverů na navázání komunikace - jak si uživatel vybere. Je to starý, staře vypadající a spíš se to nevyvíjí?

