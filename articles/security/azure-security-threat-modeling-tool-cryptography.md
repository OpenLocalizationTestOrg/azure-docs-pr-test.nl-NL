---
title: -Microsoft Threat Modeling Tool - aaaCryptography Azure | Microsoft Docs
description: oplossingen voor bedreigingen die worden weergegeven in Hallo Threat Modeling hulpprogramma
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: cab981bf116a0e76bbf44fe0f0a1a3650e4ab0f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-cryptography--mitigations"></a>Beveiliging Frame: Cryptografie | Oplossingen 
| Product/Service | Artikel |
| --------------- | ------- |
| **Webtoepassing** | <ul><li>[Gebruik alleen goedgekeurde symmetrische blokcodering en sleutellengten](#cipher-length)</li><li>[Gebruik goedgekeurde blok cipher modi en initialisatie vectoren voor symmetrische codering](#vector-ciphers)</li><li>[Goedgekeurde asymmetrische algoritmen, sleutellengten en opvulling gebruiken](#padding)</li><li>[Gebruik goedgekeurde genereren van willekeurige nummer](#numgen)</li><li>[Gebruik geen symmetrische stroom coderingen](#stream-ciphers)</li><li>[Goedgekeurde MAC, HMAC/sleutelhash hash-algoritmen gebruiken](#mac-hash)</li><li>[Gebruik alleen goedgekeurde cryptografische hash-functies](#hash-functions)</li></ul> |
| **Database** | <ul><li>[Sterke versleuteling algoritmen tooencrypt gegevens in het Hallo-database gebruiken](#strong-db)</li><li>[SSIS-pakketten moeten worden versleuteld en digitaal zijn ondertekend](#ssis-signed)</li><li>[Digitale handtekening toocritical database securables toevoegen](#securables-db)</li><li>[Versleutelingssleutels voor SQL server EKM tooprotect gebruiken](#ekm-keys)</li><li>[AlwaysEncrypted-functie te gebruiken als de versleutelingssleutels mag geen weergegeven tooDatabase-engine](#keys-engine)</li></ul> |
| **IoT-apparaat** | <ul><li>[Cryptografische sleutels veilig opslaan op IoT-apparaat](#keys-iot)</li></ul> | 
| **IoT-Cloudgateway** | <ul><li>[Een willekeurige symmetrische sleutel lang genoeg zijn voor verificatie tooIoT Hub genereren](#random-hub)</li></ul> | 
| **Mobiele Dynamics CRM-Client** | <ul><li>[Zorg ervoor dat een apparaat management-beleid is geïmplementeerd waarmee een gebruik PINCODE vereist is en extern wissen](#pin-remote)</li></ul> | 
| **Dynamics CRM Outlook-Client** | <ul><li>[Zorg ervoor dat een apparaat management-beleid is geïmplementeerd die vereist dat een PINCODE of wachtwoord/automatisch vergrendelen en versleutelt alle gegevens (bijvoorbeeld Bitlocker)](#bitlocker)</li></ul> | 
| **Identiteitsserver** | <ul><li>[Zorg ervoor dat de handtekeningsleutels zijn overgeschakeld bij gebruik van Identiteitsserver](#rolled-server)</li><li>[Zorg ervoor dat cryptografisch sterke client-ID clientgeheim zijn gebruikt in Identiteitsserver](#client-server)</li></ul> | 

## <a id="cipher-length"></a>Gebruik alleen goedgekeurde symmetrische blokcodering en sleutellengten

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>Producten moeten alleen de symmetrische blokcodering en de bijbehorende sleutellengte die expliciet zijn goedgekeurd door Hallo Crypto Advisor in uw organisatie gebruiken. Goedgekeurde symmetrische algoritmen bij Microsoft omvatten hello blokcodering volgende:</p><ul><li>Voor nieuwe code AES-128, AES-192 en AES-256 worden geaccepteerd</li><li>Voor achterwaartse compatibiliteit met bestaande code wordt 3DES drie-sleutel geaccepteerd</li><li>Voor producten met symmetrische blokcodering:<ul><li>Geavanceerde Encryption Standard (AES) is vereist voor nieuwe code</li><li>Drie sleutel triple Data Encryption Standard (3DES) is toegestaan in de bestaande code voor achterwaartse compatibiliteit</li><li>Alle andere blokcodering, met inbegrip van RC2, DES, 2 sleutel 3DES, DESX en gestreepte, kunnen alleen worden gebruikt voor het ontsleutelen van oude gegevens en moeten worden vervangen als gebruikt voor versleuteling</li></ul></li><li>Voor symmetrische blok versleutelingsalgoritmen is een minimum sleutellengte van 128 bits vereist. Hallo alleen blok versleutelingsalgoritme aanbevolen voor nieuwe code AES is (AES-128, AES-192 en AES-256 zijn allemaal geaccepteerd)</li><li>Drie sleutel 3DES is momenteel acceptabel als deze al in gebruik in de bestaande code. overgang tooAES wordt aanbevolen. DES, DESX RC2 en gestreepte worden niet langer als veilig beschouwd. Deze algoritmen kunnen alleen worden gebruikt voor het ontsleutelen van bestaande gegevens voor Hallo verjaardagen achterwaartse compatibiliteit en gegevens opnieuw moet worden versleuteld met een aanbevolen blokcodering</li></ul><p>Houd er rekening mee dat alle symmetrische blokcodering moeten worden gebruikt met een goedgekeurde versleutelingsmodus waarvoor gebruik van een juiste initialisatievector (IV). Een juiste IV is doorgaans een willekeurig getal en nooit een constante waarde</p><p>Hallo gebruik van verouderde of anderszins niet-goedgekeurde cryptografische algoritmen en sleutellengten kleinere voor het lezen van bestaande gegevens (als de nieuwe gegevens tegengestelde toowriting) kan worden toegestaan nadat Crypto het mededelingenbord van uw organisatie. U moet echter bestand voor een uitzondering op deze vereiste. Bovendien in bedrijfsimplementaties overwegen producten waarschuwing beheerders als zwakke crypto gebruikte tooread gegevens. Deze waarschuwingen moeten verklarende en actie worden uitgevoerd. In sommige gevallen kan het juiste toohave Groepsbeleid besturingselement Hallo gebruik van zwakke crypto mogelijk</p><p>.NET-algoritmen voor beheerde crypto flexibiliteit toegestaan (in volgorde van voorkeur)</p><ul><li>AesCng (FIPS-compatibel)</li><li>AuthenticatedAesCng (FIPS-compatibel)</li><li>AESCryptoServiceProvider (FIPS-compatibel)</li><li>AESManaged (niet-FIPS-compatibel)</li></ul><p>Houd er rekening mee dat geen van deze algoritmen kan worden opgegeven via Hallo `SymmetricAlgorithm.Create` of `CryptoConfig.CreateFromName` methoden zonder dat wijzigingen toohello machine.config-bestand. Let ook op AES in versies van .NET voorafgaande too.NET 3.5 heet `RijndaelManaged`, en `AesCng` en `AuthenticatedAesCng` zijn > beschikbaar via CodePlex en CNG in onderliggende OS Hallo nodig</p>

## <a id="vector-ciphers"></a>Gebruik goedgekeurde blok cipher modi en initialisatie vectoren voor symmetrische codering

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Alle symmetrische blokcodering moeten worden gebruikt met een goedgekeurde symmetrische versleutelingsmodus. Hallo alleen goedgekeurde modi zijn CBC en CTS. In het bijzonder moet Hallo elektronische code adresboek (ECB) modus worden vermeden; gebruik van ECB moet uw organisatie Crypto mededelingenbord. Alle informatie over het gebruik van de OFB, CFB, CTR, CCM, en GCM of andere versleuteling-modus moet worden gecontroleerd door de Crypto-mededelingenbord van uw organisatie. Hergebruik van dezelfde Hallo initialisatievector (IV) met blokcodering in 'streaming coderingen modi,' zoals CTR, kan ertoe leiden dat versleutelde gegevens toobe getoond. Alle symmetrische blokcodering moeten ook worden gebruikt met een juiste initialisatievector (IV). Een juiste IV is een cryptografisch sterk, willekeurig getal en nooit een constante waarde. |

## <a id="padding"></a>Goedgekeurde asymmetrische algoritmen, sleutellengten en opvulling gebruiken

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>Hallo gebruik van cryptografische algoritmen verboden introduceert aanzienlijke risico tooproduct beveiliging en moet worden vermeden. Producten moeten alleen de cryptografische algoritmen en sleutellengten en opvulling die expliciet zijn goedgekeurd door uw organisatie Crypto Board die is gekoppeld.</p><ul><li>**RSA -** kunnen worden gebruikt voor versleuteling, sleuteluitwisseling en handtekening. RSA-versleuteling moet alleen Hallo OAEP of RSA KEM opvulling modi gebruiken. Bestaande code kunt PKCS #1 v1.5 opvulling van de modus alleen voor compatibiliteit. Gebruik van null opvulling is expliciet verboden. Sleutels > = 2048 bits voor nieuwe code is vereist. Bestaande code ondersteunen mogelijk sleutels < 2048 bits zijn alleen voor achterwaartse compatibiliteit na een controle door de Crypto-mededelingenbord van uw organisatie. Sleutels < 1024 bits mag alleen worden gebruikt voor de oude gegevens decoderen/controleren, en moet worden vervangen als gebruikt voor versleuteling of ondertekening</li><li>**ECDSA -** voor handtekening alleen kan worden gebruikt. ECDSA met > = 256 bitssleutels is vereist voor nieuwe code. Handtekeningen op basis van ECDSA moeten een van de Hallo drie NIST goedgekeurd curven gebruiken (P-256, p-384 of P521). Curven die grondig is geanalyseerd, kunnen alleen na een overzicht met Crypto het mededelingenbord van uw organisatie worden gebruikt.</li><li>**ECDH -** voor sleuteluitwisseling alleen kan worden gebruikt. ECDH met > = 256 bitssleutels is vereist voor nieuwe code. Op basis van ECDH sleuteluitwisseling moet een van de Hallo drie NIST goedgekeurd curven gebruiken (P-256, p-384 of P521). Curven die grondig is geanalyseerd, kunnen alleen na een overzicht met Crypto het mededelingenbord van uw organisatie worden gebruikt.</li><li>**DSA -** mogelijk acceptabele na beoordeling en goedkeuring van uw organisatie Crypto mededelingenbord. Neem contact op met uw beveiliging advisor tooschedule mededelingenbord Crypto-revisie van uw organisatie. Als uw gebruik van DSA wordt goedgekeurd, houd er rekening mee dat u tooprohibit gebruik van sleutels minder dan 2048 bits lang moet. CNG ondersteunt 2048-bits en groter sleutellengten vanaf Windows 8.</li><li>**Diffie-Hellman -** voor sessie Sleutelbeheer alleen kan worden gebruikt. Sleutellengte > = 2048 bits voor nieuwe code is vereist. Bestaande code kan ondersteunen sleutellengten < 2048 bits zijn alleen voor achterwaartse compatibiliteit na een controle door de Crypto-mededelingenbord van uw organisatie. Sleutels < 1024 bits kan niet worden gebruikt.</li><ul>

## <a id="numgen"></a>Gebruik goedgekeurde genereren van willekeurige nummer

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>Producten moeten goedgekeurde genereren van willekeurige nummer gebruiken. Pseudo-willekeurige functies zoals Hallo C runtime functie RNG, Hallo .NET Framework-klasse System.Random of systeemfuncties zoals GetTickCount moeten daarom nooit worden gebruikt in deze code toebehoort. Gebruik van Hallo dual elliptische algoritme willekeurige getallen generator (DUAL_EC_DRBG) is niet toegestaan</p><ul><li>**CNG -** BCryptGenRandom (gebruik van Hallo BCRYPT_USE_SYSTEM_PREFERRED_RNG vlag aanbevolen, tenzij Hallo aanroeper mogelijk worden uitgevoerd op een groter dan 0 [dat wil zeggen, PASSIVE_LEVEL] IRQL)</li><li>**CAPI -** cryptGenRandom</li><li>**Win32/64-** RtlGenRandom (nieuwe implementaties moeten gebruiken BCryptGenRandom of CryptGenRandom) * rand_s * SystemPrng (voor kernelmodus)</li><li>**. NET -** RNGCryptoServiceProvider of RNGCng</li><li>**Windows Store-Apps -** Windows.Security.Cryptography.CryptographicBuffer.GenerateRandom of. GenerateRandomNumber</li><li>**Apple OS X (10.7+)/iOS(2.0+) -** int SecRandomCopyBytes (willekeurige SecRandomRef size_t telling, uint8_t *bytes)</li><li>**Apple OS X (< 10.7)-** gebruik / dev/willekeurige tooretrieve willekeurige getallen</li><li>**Java(including Google Android Java code) -** java.security.SecureRandom-klasse. Voor Android 4.3 (geleiproducten Bean) ontwikkelaars moeten Hallo Android oplossing aanbevolen te volgen en bijwerken van hun toepassingen tooexplicitly hello PRNG met entropie van /dev/urandom of /dev/random initialiseren</li></ul>|

## <a id="stream-ciphers"></a>Gebruik geen symmetrische stroom coderingen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Symmetrische stroom coderingen toe, zoals RC4, mogen niet worden gebruikt. Producten moeten een blokcodering, speciaal AES met een sleutellengte van ten minste 128 bits gebruiken in plaats van de symmetrische stream-codering. |

## <a id="mac-hash"></a>Goedgekeurde MAC, HMAC/sleutelhash hash-algoritmen gebruiken

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>Producten moeten alleen goedgekeurde message authentication code (MAC) of op basis van het hash-code (HMAC) algoritmen voor berichtauthenticatie gebruiken.</p><p>Een message authentication code (MAC) is een stukje informatie gekoppelde tooa bericht waarmee de ontvanger tooverify zowel Hallo Hallo afzender en Hallo integriteit van een geheime sleutel met het Hallo-bericht. gebruik van beide een hash gebaseerde MAC Hallo ([HMAC](http://csrc.nist.gov/publications/nistpubs/800-107-rev1/sp800-107-rev1.pdf)) of [cipher-op basis van blokken MAC](http://csrc.nist.gov/publications/nistpubs/800-38B/SP_800-38B.pdf) is toegestaan, zolang alle onderliggende hash of symmetrische versleutelingsalgoritmen ook zijn goedgekeurd voor gebruik; momenteel dit bevat Hallo HMAC SHA2 functies (HMAC SHA256, HMAC SHA384 en HMAC SHA512) en Hallo CMAC/OMAC1 en OMAC2 blokkeren op basis van cipher MACs (deze zijn gebaseerd op AES).</p><p>Gebruik van HMAC-SHA1 mogelijk toegestane voor compatibiliteit tussen platforms, maar u wordt vereist toofile een uitzondering toothis procedure en ondergaan Crypto revisie van uw organisatie. Het afkappen van HMAC's tooless dan 128 bits is niet toegestaan. Met behulp van de klant methoden toohash een sleutel en gegevens die niet is goedgekeurd en van uw organisatie Crypto mededelingenbord Bekijk eerdere toouse moet ondergaan.</p>|

## <a id="hash-functions"></a>Gebruik alleen goedgekeurde cryptografische hash-functies

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>Producten moeten Hallo SHA-2-familie van hash-algoritmen (SHA256, SHA384 en SHA512) gebruiken. Als een kortere hash is vereist, zoals een lengte van 128-bits-uitvoer in volgorde toofit een gegevensstructuur die is ontworpen met een kortere MD5-hash Hallo in acht nemen, kunnen een Hallo SHA2 hashes (meestal SHA256) door productteams afkappen. Houd er rekening mee dat SHA384 een afgekapte versie van SHA512 gebruikt is. Het afkappen van cryptografische hashes voor beveiliging doeleinden tooless dan 128 bits is niet toegestaan. Nieuwe code geen Hallo MD2, MD4, MD5, SHA-0, SHA-1 of RIPEMD hash-algoritmen gebruiken. Hash-conflicten rekenkundig uitvoerbaar zijn worden voor deze algoritmen die ze effectief wordt verbroken.</p><p>.NET-hash-algoritmen voor beheerde crypto flexibiliteit toegestaan (in volgorde van voorkeur):</p><ul><li>SHA512Cng (FIPS-compatibel)</li><li>SHA384Cng (FIPS-compatibel)</li><li>SHA256Cng (FIPS-compatibel)</li><li>SHA512Managed (niet-FIPS-compatibele) (gebruik SHA512 gebruikt als de naam van algoritme in aanroepen tooHashAlgorithm.Create of CryptoConfig.CreateFromName)</li><li>SHA384Managed (niet-FIPS-compatibele) (gebruik SHA384 als naam van algoritme in aanroepen tooHashAlgorithm.Create of CryptoConfig.CreateFromName)</li><li>SHA256Managed (niet-FIPS-compatibele) (gebruik SHA256 als naam van algoritme in aanroepen tooHashAlgorithm.Create of CryptoConfig.CreateFromName)</li><li>SHA512CryptoServiceProvider (FIPS-compatibel)</li><li>SHA256CryptoServiceProvider (FIPS-compatibel)</li><li>SHA384CryptoServiceProvider (FIPS-compatibel)</li></ul>| 

## <a id="strong-db"></a>Sterke versleuteling algoritmen tooencrypt gegevens in het Hallo-database gebruiken

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Een algoritme kiezen](https://technet.microsoft.com/library/ms345262(v=sql.130).aspx) |
| **Stappen** | Versleutelingsalgoritmen definiëren gegevenstransformaties die gemakkelijk kunnen niet worden teruggedraaid door onbevoegde gebruikers. SQL Server kunnen beheerders en ontwikkelaars toochoose uit verschillende algoritmen, zoals DES, Triple DES, TRIPLE_DES_3KEY, RC2, RC4, 128-bits RC4, DESX, AES 128-bits, 192 bits AES en AES 256-bits |

## <a id="ssis-signed"></a>SSIS-pakketten moeten worden versleuteld en digitaal zijn ondertekend

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Hallo bron van pakketten met digitale handtekeningen identificeren](https://msdn.microsoft.com/library/ms141174.aspx), [dreiging en beveiligingslek risicobeperking (Integration Services)](https://msdn.microsoft.com/library/bb522559.aspx) |
| **Stappen** | Hallo-bron van een pakket is Hallo afzonderlijke of organisatie die Hallo pakket gemaakt. Een pakket uitgevoerd van een onbekende of niet-vertrouwde bron mogelijk riskant. tooprevent unauthorized knoeien met SSIS-pakketten digitale handtekeningen moeten worden gebruikt. Tooensure hello vertrouwelijkheid van hello-pakketten tijdens opslag/doorvoer, SSIS-pakketten moeten ook toobe versleuteld |

## <a id="securables-db"></a>Digitale handtekening toocritical database securables toevoegen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [HANDTEKENING toevoegen (Transact-SQL)](https://msdn.microsoft.com/library/ms181700) |
| **Stappen** | In gevallen waarin Hallo integriteit van een beveiligbaar kritieke database toobe geverifieerd heeft moeten digitale handtekeningen worden gebruikt. Database-securables zoals een opgeslagen procedure, functie, assembly of trigger kunnen digitaal worden ondertekend. Hieronder volgt een voorbeeld van wanneer dit kan handig zijn: we spreken ondersteuning tooa software geleverd tooone van klanten is opgegeven door een ISV (onafhankelijke softwareleverancier). Hallo ISV zou tooensure dat een database kunnen worden beveiligd in Hallo software niet is geknoeid per ongeluk of door een kwaadwillende poging willen voordat het bieden van ondersteuning. Hallo beveiligbare digitaal is ondertekend, kunt Hallo ISV controleren of de digitale handtekening als de integriteit te valideren.| 

## <a id="ekm-keys"></a>Versleutelingssleutels voor SQL server EKM tooprotect gebruiken

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [SQL Server Extensible Key Management (EKM)](https://msdn.microsoft.com/library/bb895340), [Extensible Key Management met behulp van Azure Sleutelkluis (SQL Server)](https://msdn.microsoft.com/library/dn198405) |
| **Stappen** | SQL Server Extensible Key Management kunt Hallo-versleutelingssleutels die Hallo database bestanden toobe opgeslagen in een uitgeschakeld selectievakje apparaat zoals een smartcard, USB-apparaat of EKM/HSM-module beveiligen. Hierdoor kunnen ook gegevensbeveiliging van databasebeheerders (met uitzondering van de leden van Hallo sysadmin-groep). Gegevens kunnen worden versleuteld met behulp van coderingssleutels dat hello databasegebruiker alleen toegang tooon Hallo externe EKM/HSM-module heeft. |

## <a id="keys-engine"></a>AlwaysEncrypted-functie te gebruiken als de versleutelingssleutels mag geen weergegeven tooDatabase-engine

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | SQL Azure, OnPrem |
| **Kenmerken**              | SQL-versie - V12, MsSQL2016 |
| **Verwijzingen**              | [Altijd versleuteld (Database-Engine)](https://msdn.microsoft.com/library/mt163865) |
| **Stappen** | Versleutelde is altijd een voorziening waarmee tooprotect gevoelige gegevens, zoals creditcardnummers of nationale ID-nummers (bijvoorbeeld Amerikaans sofi-nummer), opgeslagen in Azure SQL Database of SQL Server-databases. Altijd versleutelde kan clients tooencrypt gevoelige gegevens binnen clienttoepassingen en nooit onthullen Hallo versleuteling sleutels toohello Database-Engine (SQL-Database of SQL Server). Als gevolg hiervan altijd versleuteld biedt een scheiding tussen degenen die eigenaar zijn van Hallo gegevens (en het kunnen bekijken) en degenen die Hallo gegevens beheren (maar moet hebben geen toegang) |

## <a id="keys-iot"></a>Cryptografische sleutels veilig opslaan op IoT-apparaat

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | IoT-apparaat | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | Besturingssysteem van het apparaat - Windows-IoT-Core, connectiviteit van apparaten - SDK's Azure IoT-apparaat |
| **Verwijzingen**              | [TPM op Windows IoT Core](https://developer.microsoft.com/windows/iot/docs/tpm), [TPM op Windows IoT Core instellen](https://developer.microsoft.com/windows/iot/win10/setuptpm), [TPM Azure IoT-apparaat-SDK](https://github.com/Azure/azure-iot-hub-vs-cs/wiki/Device-Provisioning-with-TPM) |
| **Stappen** | Symmetric of persoonlijke sleutels veilig in een hardware beveiligde opslag zoals chips TPM of een smartcard. Windows 10 IoT Core ondersteunt Hallo gebruiker van een TPM en er zijn verschillende compatibele TPM's die kunnen worden gebruikt: https://developer.microsoft.com/windows/iot/win10/tpm. Het is aanbevolen toouse een Firmware of Discrete TPM. Een TPM Software moet alleen worden gebruikt voor ontwikkeling en voor testdoeleinden. Zodra een TPM beschikbaar is en Hallo sleutels in deze zijn ingericht, worden Hallo-code die gegenereerd Hallo-token geschreven zonder vaste gevoelige informatie in deze codering. | 

### <a name="example"></a>Voorbeeld
```
TpmDevice myDevice = new TpmDevice(0);
// Use logical device 0 on hello TPM 
string hubUri = myDevice.GetHostName(); 
string deviceId = myDevice.GetDeviceId(); 
string sasToken = myDevice.GetSASToken(); 

var deviceClient = DeviceClient.Create( hubUri, AuthenticationMethodFactory. CreateAuthenticationWithToken(deviceId, sasToken), TransportType.Amqp); 
```
Zoals u kunt zien, is Hallo apparaat primaire sleutel niet aanwezig in Hallo-code. In plaats daarvan wordt opgeslagen in Hallo TPM op sleuf 0. TPM-apparaat genereert een tijdelijke SAS-token wordt vervolgens gebruikt tooconnect toohello IoT Hub. 

## <a id="random-hub"></a>Een willekeurige symmetrische sleutel lang genoeg zijn voor verificatie tooIoT Hub genereren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | IoT-Cloudgateway | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | Keuze van de gateway - Azure IoT Hub |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | IoT Hub bevat een apparaat-id-register en tijdens het inrichten van een apparaat genereert automatisch een willekeurige symmetrische sleutel. Het verdient aanbeveling toouse deze functie van hello Azure IoT Hub identiteit toogenerate Hallo registersleutel voor verificatie gebruikt. IoT-Hub kunt ook een belangrijke toobe opgegeven tijdens het Hallo-apparaat te maken. Als een sleutel is buiten de IoT Hub gegenereerd tijdens het inrichten van apparaten, is het aanbevolen toocreate een willekeurige symmetrische sleutel of ten minste 256 bits. |

## <a id="pin-remote"></a>Zorg ervoor dat een apparaat management-beleid is geïmplementeerd waarmee een gebruik PINCODE vereist is en extern wissen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Mobiele Dynamics CRM-Client | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Zorg ervoor dat een apparaat management-beleid is geïmplementeerd waarmee een gebruik PINCODE vereist is en extern wissen |

## <a id="bitlocker"></a>Zorg ervoor dat een apparaat management-beleid is geïmplementeerd die vereist dat een PINCODE of wachtwoord/automatisch vergrendelen en versleutelt alle gegevens (bijvoorbeeld Bitlocker)

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Dynamics CRM Outlook-Client | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Zorg ervoor dat een apparaat management-beleid is geïmplementeerd die vereist dat een PINCODE of wachtwoord/automatisch vergrendelen en versleutelt alle gegevens (bijvoorbeeld Bitlocker) |

## <a id="rolled-server"></a>Zorg ervoor dat de handtekeningsleutels zijn overgeschakeld bij gebruik van Identiteitsserver

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Identiteitsserver | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Van Identiteitsserver - sleutels, handtekeningen en cryptografie](https://identityserver.github.io/Documentation/docsv2/configuration/crypto.html) |
| **Stappen** | Zorg ervoor dat ondertekeningssleutels zijn overgeschakeld wanneer Identity-Server. Hallo-koppeling in de sectie Verwijzingen hello wordt uitgelegd hoe dit moet worden gepland zonder dat de uitval tooapplications vertrouwen op de Server van de identiteit. |

## <a id="client-server"></a>Zorg ervoor dat cryptografisch sterke client-ID clientgeheim zijn gebruikt in Identiteitsserver

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Identiteitsserver | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>Zorg ervoor dat cryptografisch sterke client-ID clientgeheim in Identiteitsserver gebruikt. Hallo richtlijnen moet worden gebruikt tijdens het genereren van een client-ID en geheim:</p><ul><li>Genereren van een willekeurige GUID als Hallo client-ID</li><li>Genereren van een cryptografisch willekeurige 256-bits sleutel als Hallo geheim</li></ul>|
