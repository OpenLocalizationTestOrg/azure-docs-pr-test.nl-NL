---
title: aaaHow toogenerate en de overdracht met HSM beveiligde sleutels voor Azure Sleutelkluis | Microsoft Docs
description: Gebruik dit artikel toohelp plannen, te genereren en brengt u uw eigen toouse HSM beveiligde sleutels met Azure Sleutelkluis. Ook wel BYOK of breng uw eigen sleutel.
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: ambapat
ms.openlocfilehash: 3bb234bd1c4b81770542ccf7110e256385ca3309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a>Hoe toogenerate en de overdracht met HSM beveiligde sleutels voor Azure Sleutelkluis
## <a name="introduction"></a>Inleiding
Voor de zekerheid wanneer u Azure Sleutelkluis, gebruikt kunt u importeren of genereren van sleutels in hardware security modules (HSM's) die Hallo HSM-grens nooit verlaten. Dit scenario is het vaak waarnaar wordt verwezen tooas *Breng uw eigen sleutel*, of BYOK. Hallo HSM's zijn FIPS 140-2 Level 2-gevalideerde modules. Azure Sleutelkluis gebruikt Thales nShield-familie van HSM's tooprotect uw sleutels.

Gebruik Hallo informatie in dit onderwerp toohelp plannen, te genereren en brengt u uw eigen toouse HSM beveiligde sleutels met Azure Sleutelkluis.

Deze functionaliteit is niet beschikbaar voor Azure China.

> [!NOTE]
> Zie voor meer informatie over Azure Sleutelkluis [wat is Azure Sleutelkluis?](key-vault-whatis.md)  
>
> Zie voor een zelfstudie aan de slag, waaronder het maken van een sleutelkluis voor met HSM beveiligde sleutels, [aan de slag met Azure Key Vault](key-vault-get-started.md).
>
>

Meer informatie over het genereren en overdragen van een HSM beveiligde sleutel via Internet Hallo:

* U Hallo sleutel genereren van een offline werkstation, waardoor de kwetsbaarheid Hallo.
* Hallo-sleutel is versleuteld met een KEK Key Exchange Key (), die versleuteld blijft totdat deze overgedragen toohello Azure Key Vault HSM's is. Alleen Hallo versleutelde versie van uw sleutel verlaat Hallo oorspronkelijke werkstation.
* Hallo toolset stelt de eigenschappen van uw tenantsleutel waaraan uw belangrijkste toohello beveiligingswereld van Azure Sleutelkluis is gebonden. Dus nadat hello Azure Key Vault HSM's ontvangen en uw sleutel ontsleuteld, kunnen deze HSM's gebruiken. Uw sleutel kan niet worden geëxporteerd. Deze binding wordt afgedwongen door Hallo Thales HSM's.
* Hello KEK Key Exchange Key () die is gebruikt tooencrypt uw sleutel wordt gegenereerd binnen hello Azure Key Vault HSM's en kan niet worden geëxporteerd. Hallo HSM's dwingen af dat er geen versie van Hallo KEK buiten Hallo HSM's kunnen worden. Daarnaast bevat de toolset Hallo attest van Thales dat Hallo KEK-sleutel kan niet worden geëxporteerd en is gegenereerd binnen een legitieme door Thales vervaardigde HSM.
* Hallo toolset bevat een attest van Thales dat hello Azure Key Vault beveiligingswereld ook is gegeneerd met een legitieme HSM, door Thales vervaardigde. Deze verklaring bewijst tooyou dat Microsoft legitieme hardware wordt gebruikt.
* Microsoft gebruikt afzonderlijke kek's en afzonderlijke Beveiligingswerelden in elke geografische regio. Deze scheiding zorgt ervoor dat uw sleutel kan alleen worden gebruikt in datacenters in Hallo regio waarin u het versleuteld. Bijvoorbeeld, kan niet een sleutel van een Europese klant worden gebruikt in datacenters in Noord-Amerika of Azië.

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a>Meer informatie over Thales HSM's en Microsoft-services
Thales e-Security is een toonaangevende, wereldwijde leverancier van gegevensversleuteling en cyberbeveiliging beveiliging oplossingen toohello financiële diensten, high tech productie, overheid en technologiesector. Met een 40 jaar bogen van het beveiligen van bedrijfs- en overheidsgegevens worden oplossingen van Thales gebruikt door vier Hallo vijf grootste energie en ruimtevaart bedrijven. Hun oplossingen worden ook gebruikt door 22 NAVO-landen en meer dan 80 procent van de betalingstransacties wereldwijd beveiligen.

Microsoft heeft samengewerkt met Thales tooenhance Hallo status van de illustraties HSM's. Dankzij deze verbeteringen kunt u tooget Hallo gebruikelijke voordelen van gehoste services, zonder verliest controle over uw sleutels. In het bijzonder kan deze uitbreidingen Microsoft hello HSM's beheren, zodat u niet te hoeft. Als een cloud die service, Azure Key Vault op korte termijn toomeet schaalt bereikt gebruik van uw organisatie. AT Hallo dezelfde tijd, uw sleutel beschermd binnen de HSM's van Microsoft: U controle over de levenscyclus van Hallo behouden omdat u Hallo sleutel genereren en tooMicrosoft van HSM's overdragen.

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a>Implementatie van uw eigen BYOK (bring key) voor Azure Sleutelkluis
Gebruik Hallo informatie en procedures te volgen als u uw eigen met HSM beschermde sleutel genereren en vervolgens tooAzure Sleutelkluis overdragen: Hallo brengt uw eigen scenario key (BYOK).

## <a name="prerequisites-for-byok"></a>Vereisten voor BYOK
Zie Hallo volgende tabel voor een lijst met vereisten voor uw eigen BYOK (bring key) voor Azure Sleutelkluis.

| Vereiste | Meer informatie |
| --- | --- |
| Een abonnement tooAzure |een Azure Sleutelkluis toocreate, moet u een Azure-abonnement: [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/) |
| Hello Azure Key Vault Premium service tier toosupport HSM beveiligde sleutels |Zie voor meer informatie over Hallo Servicelagen en mogelijkheden voor Azure Sleutelkluis hello [prijzen van Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/) website. |
| Thales HSM, smartcards en ondersteunende software |U moet hebben toegang tot tooa Thales Hardware Security Module en operationele basiskennis hebben van Thales HSM's. Zie [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) voor Hallo-lijst met compatibele modellen of toopurchase een HSM als u nog geen abonnement hebt. |
| Hallo volgende hardware en software:<ol><li>Een offline x64 werkstation met een besturingssysteem minimaal Windows 7 en Thales nShield-software die ten minste versie 11.50.<br/><br/>Als dit werkstation Windows 7 wordt uitgevoerd, moet u [Installeer Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</li><li>Een werkstation dat is verbonden toohello Internet en een Windows-besturingssysteem minimaal Windows 7 en [Azure PowerShell](/powershell/azure/overview) **minimaal versie 1.1.0** geïnstalleerd.</li><li>Een USB-station of ander draagbaar opslagapparaat met ten minste 16 MB vrije ruimte heeft.</li></ol> |Uit veiligheidsoverwegingen is het raadzaam dat Hallo eerste werkstation is niet verbonden tooa netwerk. Deze aanbeveling is echter niet via een programma afgedwongen.<br/><br/>Houd er rekening mee dat in Hallo instructies wordt dit werkstation waarnaar wordt verwezen tooas Hallo niet verbonden werkstation.</p></blockquote><br/>Bovendien, als uw tenantsleutel bedoeld voor een productienetwerk is, raden wij aan dat u een tweede, afzonderlijk werkstation toodownload Hallo toolset en uploaden Hallo tenantsleutel. Maar voor testdoeleinden kunt u hetzelfde werkstation Hallo als eerste Hallo.<br/><br/>Houd er rekening mee dat in Hallo instructies wordt dit tweede werkstation waarnaar wordt verwezen tooas Hallo met Internet verbonden werkstation.</p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-tooazure-key-vault-hsm"></a>Genereren en overdragen van uw belangrijkste tooAzure Sleutelkluis HSM
U wilt gebruiken Hallo toogenerate van vijf stappen te volgen en dragen uw sleutel tooan Azure Key Vault HSM:

* [Stap 1: Uw met Internet verbonden werkstation voorbereiden](#step-1-prepare-your-internet-connected-workstation)
* [Stap 2: Uw niet-verbonden werkstation voorbereiden](#step-2-prepare-your-disconnected-workstation)
* [Stap 3: Uw sleutel genereren](#step-3-generate-your-key)
* [Stap 4: De sleutel voor de overdracht voorbereiden](#step-4-prepare-your-key-for-transfer)
* [Stap 5: Draag uw belangrijkste tooAzure Sleutelkluis](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a>Stap 1: Uw met Internet verbonden werkstation voorbereiden
Deze eerste stap Hallo procedures te volgen op uw werkstation dat is verbonden toohello Internet.

### <a name="step-11-install-azure-powershell"></a>Stap 1.1: Azure PowerShell installeren
Van Hallo met Internet verbonden werkstation, download en installeer hello Azure PowerShell-module met Hallo cmdlets toomanage Azure Sleutelkluis. Hiervoor moet een minimumversie van 0.8.13.

Zie voor installatie-instructies [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

### <a name="step-12-get-your-azure-subscription-id"></a>Stap 1.2: Uw Azure-abonnement-ID ophalen
Start een Azure PowerShell-sessie en meld u aan tooyour Azure-account met behulp van de volgende opdracht Hallo:

        Add-AzureAccount
In het pop-browservenster hello, Voer uw Azure-account, gebruikersnaam en wachtwoord. Gebruik vervolgens Hallo [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) opdracht:

        Get-AzureSubscription
Zoek van uitvoer Hallo Hallo-ID voor Hallo abonnement die u voor Azure Sleutelkluis gebruiken wilt. U kunt deze abonnement-ID wordt later nodig.

Hello Azure PowerShell-venster niet sluiten.

### <a name="step-13-download-hello-byok-toolset-for-azure-key-vault"></a>Stap 1.3: Download de BYOK-hulpmiddelenset Hallo voor Azure Sleutelkluis
Ga toohello Microsoft Download Center en [download hello Azure Key Vault BYOK-hulpmiddelenset](http://www.microsoft.com/download/details.aspx?id=45345) voor uw geografische regio of het exemplaar van Azure. Gebruik de volgende Hallo informatie tooidentify Hallo pakket naam toodownload en de bijbehorende SHA-256 hash van het pakket:

- - -
**Verenigde Staten:**

KeyVault-BYOK-hulpprogramma's-Verenigd States.zip

760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B

- - -
**Europa:**

KeyVault-BYOK-hulpprogramma's-Europe.zip

7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D

- - -
**Azië:**

KeyVault-BYOK-hulpprogramma's-AsiaPacific.zip

813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8

- - -
**Latijns-Amerika:**

KeyVault-BYOK-hulpprogramma's-LatinAmerica.zip

3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0

- - -
**Japan:**

KeyVault-BYOK-hulpprogramma's-Japan.zip

453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90

- - -
**Korea:**

KeyVault-BYOK-hulpprogramma's-Korea.zip

C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A

- - -
**Australië:**

KeyVault-BYOK-hulpprogramma's-Australia.zip

4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B

- - -
[**Azure Government:**](https://azure.microsoft.com/features/gov/)

KeyVault-BYOK-hulpprogramma's-USGovCloud.zip

3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64

- - -
**Amerikaanse overheid DOD:**

KeyVault-BYOK-hulpprogramma's-USGovernmentDoD.zip

A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D

- - -
**Canada:**

KeyVault-BYOK-hulpprogramma's-Canada.zip

30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7

- - -
**Duitsland:**

KeyVault-BYOK-hulpprogramma's-Germany.zip

5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261

- - -
**India:**

KeyVault-BYOK-hulpprogramma's-India.zip

136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7

- - -
**Verenigd Koninkrijk:**

KeyVault-BYOK-hulpprogramma's-UnitedKingdom.zip

ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268

- - -

toovalidate hello integriteit van de gedownloade BYOK-toolset van uw Azure PowerShell-sessie gebruik Hallo [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.

    Get-FileHash KeyVault-BYOK-Tools-*.zip

Hallo toolset bevat Hallo volgende:

* Een KEK Key Exchange Key ()-pakket met een naam die begint met **BYOK-KEK - pkg-.**
* Een beveiligingswereldpakket met een naam die begint met **BYOK-SecurityWorld - pkg-.**
* Een pythonscript met de naam **verifykeypackage.py.**
* Een uitvoerbaar opdrachtregelbestand met de naam **KeyTransferRemote.exe** en bijbehorende DLL-bestanden.
* Een herdistrueerbare pakket Visual C++, met de naam **vcredist_x64.exe.**

Kopieer Hallo pakket tooa USB-station of ander draagbaar opslagmedium.

## <a name="step-2-prepare-your-disconnected-workstation"></a>Stap 2: Uw niet-verbonden werkstation voorbereiden
Deze tweede stap Hallo procedures te volgen op Hallo werkstation dat geen netwerk verbonden tooa (Hallo Internet of het interne netwerk).

### <a name="step-21-prepare-hello-disconnected-workstation-with-thales-hsm"></a>Stap 2.1: Bereid Hallo verbroken werkstation met Thales HSM
Hallo (Thales) nCipher-ondersteuningssoftware installeren op een Windows-computer, en voeg vervolgens een Thales HSM toothat-computer.

Zorg ervoor dat Hallo Thales-hulpprogramma's zijn in het pad (**%nfast_home%\bin**). Typ bijvoorbeeld de volgende Hallo:

        set PATH=%PATH%;"%nfast_home%\bin"

Zie voor meer informatie Hallo handleiding inbegrepen bij Hallo Thales HSM.

### <a name="step-22-install-hello-byok-toolset-on-hello-disconnected-workstation"></a>Step 2.2: Installatie Hallo BYOK-toolset op Hallo niet verbonden werkstation
Hallo BYOK-toolset pakket van Hallo USB-station of ander draagbaar opslagmedium kopiëren en vervolgens Hallo te volgen:

1. Hallo-bestanden extraheren uit pakket Hallo gedownload naar een map.
2. Voer vcredist_x64.exe uit in die map.
3. Hallo instructies toohello Hallo Visual C++ runtime-onderdelen voor Visual Studio 2013 installeren.

## <a name="step-3-generate-your-key"></a>Stap 3: Uw sleutel genereren
Deze derde stap Hallo procedures te volgen op Hallo niet verbonden werkstation. toocomplete deze stap uw HSM moet in de modus van de initialisatie. 


### <a name="step-31-change-hello-hsm-mode-tooi"></a>Stap 3.1: Wijzig Hallo HSM modus too'I'
Als u van Thales nShield Edge, toochange Hallo modus gebruikmaakt: 1. Hallo modus knop toohighlight Hallo vereist modus gebruiken. 2. Binnen een paar seconden en houdt u knop Hallo-wissen van een paar seconden. Hallo-modus wordt gewijzigd, hello nieuwe modus LED niet meer knippert als blijft branden. Hallo Status LED onregelmatig mogelijk flash een paar seconden en vervolgens knippert regelmatig wanneer Hallo apparaat gereed is. Anders Hallo apparaat blijft in de huidige modus Hallo met relevante Hallo-modus LED branden.

### <a name="step-32-create-a-security-world"></a>Stap 3.2: Maak een beveiligingswereld
Start een opdrachtprompt en Voer Hallo nieuwe-wereld-programma van Thales uit.

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

Dit programma maakt een **Beveiligingswereld** bestand op % NFAST_KMDATA%\local\world, wat overeenkomt met toohello C:\ProgramData\nCipher\Key Management Settings\User map. U kunt andere waarden gebruiken voor Hallo quorum maar in ons voorbeeld u na vragen aan gebruiker tooenter drie lege kaarten en pincodes voor elk criterium. Vervolgens geeft twee kaarten volledige toegang toohello beveiligingswereld. Deze kaarten worden Hallo **Beheerderskaartenset** voor Hallo nieuwe beveiligingswereld.

Vervolgens Hallo na:

* Back-up Hallo wereld-bestand. Secure beveiligen Hallo wereld-bestand, Hallo Beheerderskaarten en de bijbehorende pincodes en zorg ervoor dat iemand toegang toomore dan één kaart heeft.

### <a name="step-33-change-hello-hsm-mode-tooo"></a>Stap 3.3: Wijzig Hallo HSM modus too'O'
Als u van Thales nShield Edge, toochange Hallo modus gebruikmaakt: 1. Hallo modus knop toohighlight Hallo vereist modus gebruiken. 2. Binnen een paar seconden en houdt u knop Hallo-wissen van een paar seconden. Hallo-modus wordt gewijzigd, hello nieuwe modus LED niet meer knippert als blijft branden. Hallo Status LED onregelmatig mogelijk flash een paar seconden en vervolgens knippert regelmatig wanneer Hallo apparaat gereed is. Anders Hallo apparaat blijft in de huidige modus Hallo met relevante Hallo-modus LED branden.


### <a name="step-34-validate-hello-downloaded-package"></a>Stap 3.4: Hallo gedownloade pakket valideren
Deze stap is optioneel maar aanbevolen zodat u kunt de volgende Hallo valideren:

* Hallo-sleutel voor sleuteluitwisseling die is opgenomen in de hulpmiddelenset Hallo is gegenereerd met een legitieme Thales HSM.
* Hallo-hash van het Hallo-Beveiligingswereld die is opgenomen in de hulpmiddelenset Hallo is gegenereerd met een legitieme Thales HSM.
* Hallo-sleutel voor sleuteluitwisseling is niet exporteerbaar.

> [!NOTE]
> Hallo toovalidate pakket hebt gedownload, hello HSM moet worden verbonden, wordt ingeschakeld, en moet een beveiligingswereld (zoals Hallo dat die u zojuist hebt gemaakt).
>
>

toovalidate hello gedownload pakket:

1. Hallo verifykeypackage.py script uitvoeren door een van de volgende hello, afhankelijk van uw geografische regio of het exemplaar van Azure te typen:

   * Voor Noord-Amerika:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * Voor Europa:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * Voor Azië:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * Voor Latijns-Amerika:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * Voor Japan:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * Voor Korea:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * Voor Australië:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * Voor [Azure Government](https://azure.microsoft.com/features/gov/), waarbij Hallo US government-exemplaar van Azure wordt gebruikt:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * Voor de overheid van de VS DOD:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * Voor Canada:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * Voor Duitsland:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * Voor India:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > Hallo Thales-software bevat python in %NFAST_HOME%\python\bin
     >
     >
2. Controleer of u de volgende hello, waarmee wordt aangegeven validatie is geslaagd: **resultaat: geslaagd**

Dit script valideert Hallo ondertekenaarsketen up toohello Thales-hoofdsleutel. Hallo-hash van deze hoofdsleutel is ingesloten in het Hallo-script en de waarde moet **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**. U kunt deze waarde ook afzonderlijk controleren door te bezoeken Hallo [Thales-website](http://www.thalesesec.com/).

U bent nu klaar toocreate een nieuwe sleutel.

### <a name="step-35-create-a-new-key"></a>Stap 3.5: Maak een nieuwe sleutel
Een sleutel genereren met behulp van Hallo Thales **generatekey** programma.

Voer Hallo opdracht toogenerate Hallo sleutel te volgen:

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

Wanneer u deze opdracht uitvoert, gebruikt u deze instructies:

* parameter Hallo *beveiligen* toohello-waarde moet worden ingesteld **module**, zoals wordt weergegeven. Hiermee maakt u een modulair beveiligde sleutel. Hallo BYOK-toolset biedt geen ondersteuning voor OCS beveiligde sleutels.
* Vervang de waarde Hallo van *contosokey* voor Hallo **ident** en **plainname** met een tekenreekswaarde. toominimize administratieve overhead en Hallo risico's te beperken van fouten, wordt aangeraden dezelfde voor beide waarde hello te gebruiken. Hallo **ident** waarde mag alleen cijfers, streepjes en kleine letters bestaan.
* Hallo pubexp is leeg (standaard) in dit voorbeeld, maar u kunt specifieke waarden opgeven. Zie voor meer informatie Hallo Thales-documentatie.

Deze opdracht maakt u een Tokenized sleutelbestand in uw map %NFAST_KMDATA%\local met een naam die begint met **key_simple_**, gevolgd door Hallo **ident** dat is opgegeven in het Hallo-opdracht. Bijvoorbeeld: **key_simple_contosokey**. Dit bestand bevat een versleutelde sleutel.

Back-up van deze Tokenized sleutelbestand op een veilige locatie.

> [!IMPORTANT]
> Wanneer u later uw sleutel tooAzure Sleutelkluis overdraagt, kan Microsoft deze sleutel back tooyou niet exporteren dus is het erg belangrijk back-up van uw sleutel en beveiligingswereld veilig. Neem contact op met Thales voor richtlijnen en aanbevolen procedures voor back-ups van uw sleutel.
>
>

U zijn nu gereed tootransfer uw belangrijkste tooAzure Sleutelkluis.

## <a name="step-4-prepare-your-key-for-transfer"></a>Stap 4: De sleutel voor de overdracht voorbereiden
Deze vierde stap Hallo procedures te volgen op Hallo niet verbonden werkstation.

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a>Stap 4.1: Maak een kopie van uw sleutel met beperkte machtigingen

Open een nieuw opdrachtpromptvenster en wijzig Hallo huidige directory toohello locatie waar u Hallo BYOK zip-bestand hebt uitgepakt. tooreduce hello machtigingen voor de sleutel, vanaf een opdrachtprompt, voer een van de volgende hello, afhankelijk van uw geografische regio of het exemplaar van Azure:

* Voor Noord-Amerika:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* Voor Europa:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* Voor Azië:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* Voor Latijns-Amerika:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* Voor Japan:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* Voor Korea:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* Voor Australië:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* Voor [Azure Government](https://azure.microsoft.com/features/gov/), waarbij Hallo US government-exemplaar van Azure wordt gebruikt:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* Voor de overheid van de VS DOD:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* Voor Canada:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* Voor Duitsland:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* Voor India:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

Wanneer u deze opdracht uitvoert, vervangt *contosokey* Hello dezelfde waarde als u hebt opgegeven in **stap 3.5: Maak een nieuwe sleutel** van Hallo [uw sleutel genereren](#step-3-generate-your-key) stap.

Wordt u gevraagd tooplug in uw security world admin-kaarten.

Wanneer Hallo-opdracht is voltooid, ziet u **resultaat: SUCCES** en Hallo kopie van uw sleutel met beperkte machtigingen zich in Hallo-bestand met de naam key_xferacId_<contosokey>.

U mag inspecteert Hallo ACL's met behulp van volgende opdrachten met Thales-hulpprogramma Hallo:

* aclprint.PY:

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* kmfile-dump.exe:

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  Wanneer u deze opdrachten uitvoert, vervangt u contosokey Hello dezelfde waarde als u hebt opgegeven in **stap 3.5: Maak een nieuwe sleutel** van Hallo [uw sleutel genereren](#step-3-generate-your-key) stap.

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a>Stap 4.2: Versleutel de sleutel met behulp van Microsoft sleutel voor sleuteluitwisseling
Voer een van de volgende opdrachten uit, afhankelijk van uw geografische regio of het exemplaar van Azure Hallo:

* Voor Noord-Amerika:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Voor Europa:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Voor Azië:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Voor Latijns-Amerika:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Voor Japan:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Voor Korea:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Voor Australië:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Voor [Azure Government](https://azure.microsoft.com/features/gov/), waarbij Hallo US government-exemplaar van Azure wordt gebruikt:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Voor de overheid van de VS DOD:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Voor Canada:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Voor Duitsland:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Voor India:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

Wanneer u deze opdracht uitvoert, gebruikt u deze instructies:

* Vervang *contosokey* door Hallo-id die u gebruikt toogenerate Hallo sleutel in **stap 3.5: Maak een nieuwe sleutel** van Hallo [uw sleutel genereren](#step-3-generate-your-key) stap.
* Vervang *SubscriptionID* met de Hallo ID hello Azure-abonnement dat u de sleutelkluis bevat. U hebt deze waarde opgehaald in **stap 1.2: uw Azure-abonnement-ID ophalen** van Hallo [uw met Internet verbonden werkstation voorbereiden](#step-1-prepare-your-internet-connected-workstation) stap.
* Vervang *ContosoFirstHSMKey* met een label dat wordt gebruikt voor naam van uw uitvoerbestand.

Wanneer dit succesvol is voltooid, wordt weergegeven **resultaat: SUCCES** en er is een nieuw bestand in de huidige Hallo-map met Hallo achter naam: KeyTransferPackage -*ContosoFirstHSMkey*.byok

### <a name="step-43-copy-your-key-transfer-package-toohello-internet-connected-workstation"></a>Stap 4.3: Kopieer uw sleuteloverdracht pakket toohello met Internet verbonden werkstation
Gebruik een USB-station of ander draagbaar opslagmedium toocopy Hallo-bestand voor uitvoer van Hallo vorige stap (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour met Internet verbonden werkstation.

## <a name="step-5-transfer-your-key-tooazure-key-vault"></a>Stap 5: Draag uw belangrijkste tooAzure Sleutelkluis
Gebruik voor deze laatste stap op Hallo met Internet verbonden werkstation, Hallo [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet tooupload hello sleuteloverdrachtpakket die u hebt gekopieerd uit Hallo verbroken werkstation toohello Azure Key Vault HSM:

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

Als Hallo uploaden voltooid is, ziet u de eigenschappen weergegeven Hallo van Hallo-sleutel die u zojuist hebt toegevoegd.

## <a name="next-steps"></a>Volgende stappen
U kunt deze met HSM beschermde sleutel nu gebruiken in de sleutelkluis. Zie voor meer informatie, Hallo **als u wilt dat er een hardware security module (HSM) toouse** sectie in Hallo [aan de slag met Azure Key Vault](key-vault-get-started.md) zelfstudie.
