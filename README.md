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
- https://tox.chat/
- https://docs.cwtch.im/
- https://scuttlebot.io/more/protocols/secure-scuttlebutt.html
- https://retroshare.cc/

