# h4 - NFC ja RFID

## a) Tarkastele käytössäsi olevia RFID tuotteita,

Lähdin selvittämään, mitä omia tuotteitani hyödyntää RFID- tai NFC-teknologiaa. Löysin ainakin seuraavat tuotteet:

- Maksukortti
- Passi
- Apple Watch
- iPhone 17
- RFID-suojattu lompakko

Maksukorttini, iPhoneni ja Apple Watchini käyttävät lähimaksamiseen NFC-teknologiaa. NFC on RFID-teknologiaan läheisesti liittyvä lyhyen kantaman langaton tiedonsiirtotekniikka, joka toimii 13,56 MHz:n taajuudella (NFC Forum s.a.).

Myös Suomen passeissa on langattomasti luettava mikrosiru. Sirulle tallennetaan passinhaltijan henkilötiedot, kasvokuva ja sormenjäljet. Sormenjäljet eivät näy passin tietosivulla, vaan ne ovat tallennettuina ainoastaan sirulle (Poliisi s.a.).

Tutkin myös sitä, miten nämä tuotteet ovat suojautuneet mahdolliselta RFID-urkinnalta.

Maksukorttini osalta käytän RFID-suojattua lompakkoa, jonka tarkoituksena on estää kortin tietojen lukeminen ilman lupaa. En kuitenkaan ole itse testannut, kuinka tehokas lompakon suojaus todellisuudessa on.

Passin sirun suojaamiseen käytetään erilaisia käyttöoikeuksien tarkistamiseen liittyviä menetelmiä. Yksi näistä on PACE-protokolla (Password Authenticated Connection Establishment). Sen avulla passin sirun ja lukijalaitteen välille muodostetaan suojattu yhteys. Tämä vaikeuttaa sirun tietojen luvatonta lukemista ja tiedonsiirron salakuuntelua (ICAO 2021).

Applen laitteissa maksamiseen liittyviä tietoja käsitellään Secure Element -turvaelementissä. Se on erillinen suojattu siru, jossa säilytetään maksamiseen liittyviä arkaluontoisia tietoja. Maksutapahtumat vaativat myös käyttäjän tunnistautumisen. iPhonessa tämä tapahtuu esimerkiksi Face ID:llä tai pääsykoodilla. Apple Watchissa maksu vahvistetaan avaamalla kello ja painamalla sivupainiketta kaksi kertaa (Apple s.a.).

Näiden tietojen perusteella omissa laitteissani on käytössä useita erilaisia suojausmenetelmiä. Maksukortin kohdalla luotan RFID-suojattuun lompakkoon, kun taas passissa ja Applen laitteissa suojaus perustuu niiden omiin teknisiin ratkaisuihin.

Sanoisin, että olen suojautunut RFID-urkinnalta ihan kohtuullisesti. En kuitenkaan pysty varmistamaan kaikkien suojausmenetelmien todellista tehokkuutta. Lisäksi on hyvä muistaa, että RFID- ja NFC-teknologian turvallisuus riippuu myös käytetystä toteutuksesta eikä pelkästään itse teknologiasta.

## b) Tutustu APDU-komentojen rakenteeseen

Tutustuin APDU-komentojen rakenteeseen ChatGPT:n avulla.

APDU (Application Protocol Data Unit) on komentorakenne, jota käytetään älykorttien ja niitä lukevien laitteiden välisessä tiedonsiirrossa. Sitä käytetään esimerkiksi maksukorteissa, passeissa ja SIM-korteissa.

Käytännössä lukijalaite lähettää APDU-komennon kortille, joka käsittelee pyynnön ja palauttaa siihen vastauksen (ETSI 2026).

APDU-komennon perusrakenne sisältää neljä pakollista kenttää:

```text
CLA, INS, P1 ja P2
```

Näiden lisäksi komennossa voi olla kolme muuta kenttää:

```text
Lc, Data ja Le
```

Kenttien tarkoitukset ovat seuraavat:

- **CLA** – Määrittelee komennon luokan.
- **INS** – Määrittelee suoritettavan toiminnon.
- **P1** – Komennon ensimmäinen parametri.
- **P2** – Komennon toinen parametri.
- **Lc** – Ilmoittaa lähetettävän datan pituuden tavuina.
- **Data** – Sisältää kortille lähetettävän tiedon.
- **Le** – Ilmoittaa, kuinka paljon dataa lukijalaite odottaa saavansa enintään vastauksena.

Kaikkia kenttiä ei käytetä jokaisessa komennossa, vaan rakenne riippuu siitä, mitä kortilta halutaan pyytää. APDU-komennosta on olemassa neljä erilaista perusrakennetta sen mukaan, sisältääkö komento lähetettävää dataa tai odotetaanko kortilta vastausdataa (ETSI 2026).

Kortin lähettämä vastaus sisältää mahdollisesti pyydettyä dataa sekä kaksi tilakoodia, SW1 ja SW2. Näiden avulla lukijalaite saa tiedon siitä, miten komennon suorittaminen onnistui.

Esimerkiksi tilakoodi **90 00** tarkoittaa onnistunutta suoritusta. Tilakoodi **6A 82** puolestaan tarkoittaa, ettei pyydettyä tiedostoa tai sovellusta löytynyt (Euroopan komissio 2002).

Yksi esimerkki APDU-komennosta on SELECT FILE. Sen avulla voidaan valita kortilta tietty sovellus tai tiedosto, jonka kanssa halutaan jatkaa kommunikointia. Komennon INS-kentän arvo on A4 (ETSI 2026).

APDU-komentojen avulla eri valmistajien älykortit ja lukijalaitteet pystyvät kommunikoimaan yhteisen rakenteen mukaisesti.

**ChatGPT:n käyttö ja käytetyt kehotteet**

Käytin ChatGPT:tä APDU-komentojen rakenteen selvittämiseen ja eri kenttien tarkoituksen ymmärtämiseen. Alla on esimerkkejä aiheeseen liittyvistä kehotteista. Ne on kirjoitettu tiivistettyinä, eivätkä ne ole sanatarkkoja lainauksia alkuperäisestä keskustelusta.

1. Mikä on APDU-komento ja missä sitä käytetään?
2. Selitä APDU-komennon rakenne ja sen eri kenttien tarkoitukset.
3. Mitä eroa on komento-APDU:lla ja vastaus-APDU:lla?
4. Mitä SW1- ja SW2-tilakoodit tarkoittavat? Anna esimerkkejä yleisistä koodeista.
5. Selitä SELECT FILE -komennon käyttötarkoitus käytännön esimerkillä.

Näiden kysymysten avulla sain paremman käsityksen APDU-komentojen rakenteesta ja niiden käyttötarkoituksesta.

## c) Tutki ja kerro minkä mielenkiintoisen RFID hakkerointi uutiset löysit.

Löysin RFID Journal -sivustolta 26.8.2024 julkaistun uutisen, joka käsitteli RFID-kulkukorttien tietoturvaongelmia. Uutisessa kerrottiin Quarkslab-tietoturvatutkijoiden löytämästä haavoittuvuudesta tietyissä MIFARE Classic -yhteensopivissa älykorteissa (Hickey 2024).

Tutkimuksessa keskityttiin erityisesti Shanghai Fudan Microelectronics Groupin valmistamiin FM11RF08- ja FM11RF08S-kortteihin. Kyseisiä kortteja käytetään esimerkiksi hotellien lukitusjärjestelmissä ja kulunvalvonnassa.

Tutkijat löysivät korteista laitteistotason takaoven, jonka avulla oli mahdollista päästä käsiksi korttien salausavaimiin. Tämän seurauksena korttien tietoturva oli huomattavasti heikompi kuin niiden perusteella olisi voinut olettaa (Teuwen 2024).

Hyökkäyksen erikoisuutena oli se, ettei tutkijoiden tarvinnut päästä käsiksi itse kortinlukijaan tai kulunvalvontajärjestelmään. Hyökkäys kohdistui suoraan korttiin. Tutkijat pystyivät hyödyntämään löytämäänsä takaovea ja selvittämään korttien käyttämiä salausavaimia.

Korttiin piti kuitenkin päästä fyysisesti käsiksi muutamaksi minuutiksi. Tämän jälkeen sen käyttämiä salausavaimia voitiin selvittää ja kortin tietoturvaa murtaa. Menetelmä mahdollisti myös korttien kopioinnin (Teuwen 2024).

Tutkimuksen mukaan ongelma ei rajoittunut ainoastaan yhteen korttimalliin. Tutkijat löysivät samanlaisen takaoven myös vanhemmasta FM11RF08-mallista. Lisäksi kortteja oli löytynyt käytöstä esimerkiksi hotelleissa Yhdysvalloissa, Euroopassa ja Intiassa (Teuwen 2024; Hickey 2024).

Pidin tätä uutista mielenkiintoisena erityisesti siksi, että hyökkäys kohdistui suoraan itse RFID-korttiin eikä sen käyttämään lukijalaitteeseen. Kortti voi näyttää täysin tavalliselta kulkukortilta, vaikka sen sisäisessä toteutuksessa olisi vakavia tietoturvaongelmia.

Tapaus sai myös miettimään RFID-korttien turvallisuutta yleisemmin. Pelkkä RFID-teknologian käyttäminen ei vielä tarkoita, että järjestelmä olisi turvallinen. Myös kortin valmistus, salaus ja tunnistautumisen toteutus vaikuttavat siihen, kuinka helposti järjestelmää voidaan väärinkäyttää.

## Lähteet

Apple s.a. Apple Pay component security. Luettavissa: https://support.apple.com/en-gb/guide/security/sec2561eb018/web. Luettu: 15.11.2026.

ETSI 2026. ETSI TS 102 221 V18.4.0. Smart Cards; UICC-Terminal interface; Physical and logical characteristics. Luettavissa: https://www.etsi.org/deliver/etsi_ts/102200_102299/102221/18.04.00_60/ts_102221v180400p.pdf. Luettu: 15.11.2026.

Euroopan komissio 2002. Komission asetus (EY) N:o 1360/2002. Luettavissa: https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX:32002R1360. Luettu: 15.11.2026.

Hickey, J. 2024. RFID Smart Access Cards Allow Instant Cloning Due to Backdoor: Report. RFID Journal. 26.8.2024. Luettavissa: https://www.rfidjournal.com/news/rfid-smart-access-cards-allow-instant-cloning-due-to-backdoor-report/221564/. Luettu: 15.11.2026.

ICAO 2021. Doc 9303. Machine Readable Travel Documents. Part 11: Security Mechanisms for MRTDs. Eighth Edition. Muutettu 14.6.2024. Luettavissa: https://www.icao.int/publications/documents/9303_p11_cons_en.pdf. Luettu: 15.11.2026.

NFC Forum s.a. NFC Technology. Technical Overview. Luettavissa: https://nfc-forum.org/learn/NFC-technology/. Luettu: 15.11.2026.

Poliisi s.a. Näin käytät passia – passiin liittyvät käytännön asiat. Luettavissa: https://poliisi.fi/nain-kaytat-passia. Luettu: 15.11.2026.

Teuwen, P. 2024. MIFARE Classic: exposing the static encrypted nonce variant... and a few hardware backdoors. Quarkslab. 20.8.2024, päivitetty 6.9.2024. Luettavissa: https://blog.quarkslab.com/mifare-classic-static-encrypted-nonce-and-backdoors.html. Luettu: 15.11.2026.
