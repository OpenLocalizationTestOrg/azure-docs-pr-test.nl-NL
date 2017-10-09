---
title: de installatiekopie van een virtuele machine voor hello Azure Marketplace aaaCreating | Microsoft Docs
description: Gedetailleerde instructies over hoe een virtuele machine toocreate voor beelden hello Azure Marketplace voor anderen toopurchase.
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5c937b8e-e28d-4007-9fef-624046bca2ae
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio; v-divte
ms.openlocfilehash: 65e1c0530bb050fb379a52544e36c55faacd84df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-virtual-machine-image-for-hello-azure-marketplace"></a>Handleiding toocreate de installatiekopie van een virtuele machine voor hello Azure Marketplace
In dit artikel **stap 2**, begeleidt u bij het voorbereiden van Hallo virtuele harde schijven (VHD's) dat u Azure Marketplace toohello gaat implementeren. Uw VHD's zijn Hallo foundation van uw SKU. Hallo-proces is afhankelijk van of u een SKU op basis van Linux of op basis van Windows biedt. In dit artikel komen beide scenario's. Dit proces kan worden uitgevoerd in combinatie met [accountaanmaking en registratie][link-acct-creation].

## <a name="1-define-offers-and-skus"></a>1. Definieer aanbiedingen en SKU 's
In deze sectie leert u toodefine Hallo aanbiedingen en hun bijbehorende SKU's.

Een aanbieding is een tooall 'parent' van de SKU's. U kunt meerdere aanbiedingen hebben. Hoe u toostructure beslist is uw aanbiedingen tooyou. Wanneer een aanbieding wordt doorgegeven toostaging, wordt deze doorgegeven met alle van de SKU's. De SKU-id's, moet u zorgvuldig overwegen omdat ze zichtbaar in Hallo URL:

* Azure.com: http://azure.microsoft.com/marketplace/partners/ {PartnerNamespace} / {OfferIdentifier}-{SKUidentifier}
* Azure preview-portal: https://portal.azure.com/#gallery/ {PublisherNamespace}. {OfferIdentifier} {SKUIDdentifier}  

Een SKU is Hallo commerciële naam voor een VM-installatiekopie. Een VM-installatiekopie bevat de schijf van een besturingssysteem en nul of meer gegevensschijven. Het is in wezen Hallo volledige opslagprofiel voor een virtuele machine. Een VHD is per schijf nodig. Zelfs leeg gegevensschijven vereisen een VHD-toobe gemaakt.

Ongeacht welk besturingssysteem u gebruikt, alleen Hallo minimum aantal gegevensschijven dat nodig is voor de SKU Hallo toevoegen Klanten schijven die deel van een installatiekopie op Hallo moment van implementatie uitmaken kunnen niet worden verwijderd, maar kunnen altijd schijven toevoegen tijdens of na de implementatie als ze deze nodig.

> [!IMPORTANT]
> **Het aantal schijven in een nieuwe Afbeeldingversie niet wijzigen.** Als u gegevensschijven in Hallo installatiekopie configureren moet, definieert u een nieuwe SKU. Publiceren van een nieuwe Afbeeldingversie met een andere schijf aantallen hebben Hallo potentieel van nieuwe implementatie op basis van de nieuwe installatiekopie versie Hallo in geval van automatisch schalen, automatische implementaties van oplossingen op basis van ARM-sjablonen en andere scenario's op te splitsen.
>
>

### <a name="11-add-an-offer"></a>1.1 een aanbieding toevoegen
1. Meld u aan toohello [Publishing Portal] [ link-pubportal] met behulp van uw verkopersaccount.
2. Selecteer Hallo **virtuele Machines** tabblad Hallo Publishing Portal. Voer de aanbiedingsnaam van uw in Hallo vraag vermelding veld. Hallo wordt aanbieding doorgaans Hallo naam van het Hallo-producten of services dat u van plan toosell in hello Azure Marketplace bent.
3. Selecteer **Maken**.

### <a name="12-define-a-sku"></a>1.2 een SKU definiëren
Wanneer u een aanbieding hebt toegevoegd, u moet toodefine en uw SKU's identificeren. U kunt meerdere aanbiedingen hebben kan, en elke aanbieding meerdere SKU's onder deze. Wanneer een aanbieding wordt doorgegeven toostaging, wordt deze doorgegeven met alle van de SKU's.

1. **Voeg een SKU.** Hallo SKU moet een id die wordt gebruikt in Hallo-URL. Hallo-id moet uniek zijn binnen uw publicatieprofiel, maar er is geen risico bestaat dat ID conflicten met andere uitgevers.

   > [!NOTE]
   > Hallo aanbieding en SKU-id's worden weergegeven in Hallo aanbieding URL op Hallo Marketplace.
   >
   >
2. **Voeg een beknopte beschrijving voor de SKU.** Samenvatting beschrijvingen zijn zichtbaar toocustomers, dus moet u ze gemakkelijk leesbare. Deze informatie heeft geen toobe geblokkeerd tot Hallo 'Push tooStaging' fase nodig. Tot u gratis tooedit zijn deze.
3. Als u op basis van een Windows SKU's gebruikt, volgt u de voorgestelde koppelingen Hallo tooacquire Hallo goedgekeurd versies van Windows Server.

## <a name="2-create-an-azure-compatible-vhd-linux-based"></a>2. Maken van een Azure-compatibele VHD (op basis van Linux)
Deze sectie richt zich op de aanbevolen procedures voor het maken van een installatiekopie op basis van Linux-VM voor hello Azure Marketplace. Raadpleeg voor een stapsgewijze toohello volgende documentatie: [maakt en uploadt u een virtuele harde schijf met Hallo Linux-besturingssysteem](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="3-create-an-azure-compatible-vhd-windows-based"></a>3. Maken van een Azure-compatibele VHD (gebaseerd op Windows)
Deze sectie richt zich op Hallo stappen toocreate een SKU op basis van Windows Server voor hello Azure Marketplace.

### <a name="31-ensure-that-you-are-using-hello-correct-base-vhds"></a>3.1 Zorg ervoor dat u gebruikmaakt van Hallo corrigeren base VHD 's
Hallo besturingssysteem-VHD voor VM-installatiekopie moet worden gebaseerd op een Azure-goedgekeurde basisinstallatiekopie met Windows Server of SQL Server.

toobegin, een virtuele machine maken van een van de volgende afbeeldingen, zich bevindt op Hallo Hallo [Microsoft Azure-portal][link-azure-portal]:

* WindowsServer ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1][link-datactr-2008-r2])
* SQL Server 2014 ([Enterprise][link-sql-2014-ent], [standaard][link-sql-2014-std], [Web][link-sql-2014-web])
* SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent], [standaard][link-sql-2012-std], [Web][link-sql-2012-web])

Deze koppelingen kunnen worden gevonden in Hallo Publishing Portal onder Hallo SKU pagina.

> [!TIP]
> Als u van Hallo huidige Azure-portal of PowerShell gebruikmaakt, zijn installatiekopieën van Windows Server gepubliceerde op 8 September 2014 of hoger goedgekeurd.
>
>

### <a name="32-create-your-windows-based-vm"></a>3.2 maken van de VM op basis van Windows
U kunt uw virtuele machine op basis van een goedgekeurde basisinstallatiekopie in een paar eenvoudige stappen maken vanuit Hallo Microsoft Azure-portal. Hallo hieronder vindt u een overzicht van Hallo proces:

1. Selecteer Hallo basisinstallatiekopie pagina **virtuele Machine maken** toobe omgeleid toohello nieuwe [Microsoft Azure-portal][link-azure-portal].

    ![tekenen][img-acom-1]
2. Meld u aan de portal toohello Hello Microsoft-account en het wachtwoord voor hello Azure-abonnement u wilt dat toouse.
3. Ga als volgt Hallo prompts toocreate een virtuele machine met behulp van de basisinstallatiekopie Hallo die u hebt geselecteerd. Tooprovide moet u een hostnaam (naam van de computer Hallo), de gebruikersnaam (geregistreerd als een beheerder) en het wachtwoord voor Hallo VM.

    ![tekenen][img-portal-vm-create]
4. Hallo-grootte van Hallo VM toodeploy selecteren:

    a.    Als u van plan toodevelop Hallo VHD lokale bent, is de grootte van de Hallo niet van belang. Overweeg het gebruik van een van de Hallo kleinere virtuele machines.

    b.    Als u van plan toodevelop Hallo installatiekopie in Azure bent, kunt u met behulp van een Hallo VM-grootten voor de geselecteerde installatiekopie Hallo aanbevolen.

    c.    Raadpleeg voor informatie over prijzen, toohello **aanbevolen Prijscategorieën** selector op Hallo portal weergegeven. Het biedt Hallo drie aanbevolen grootten worden verstrekt door Hallo uitgever. (In dit geval is Hallo publisher Microsoft.)

    ![tekenen][img-portal-vm-size]
5. Eigenschappen instellen:

    a.    Voor snelle implementatie kunt u Hallo standaardwaarden voor Hallo onder laten **optionele configuratie** en **resourcegroep**.

    b.    Onder **Opslagaccount**, kunt u eventueel selecteren Hallo storage-account op welke Hallo besturingssysteem VHD worden opgeslagen.

    c.    Onder **resourcegroep**, kunt u eventueel Hallo logische groep in welke tooplace Hallo VM selecteren.
6. Selecteer Hallo **locatie** voor implementatie:

    a.    Als u van plan toodevelop Hallo VHD lokale bent, Hallo locatie niet van belang omdat Hallo installatiekopie tooAzure later gaat uploaden.

    b.    Als u van plan toodevelop Hallo installatiekopie in Azure bent, kunt u een van de Microsoft Azure VS gebaseerde regio's Hallo Hallo vanaf. Dit versnelt Hallo VHD kopiëren die Microsoft namens jou worden uitgevoerd als u uw afbeelding voor de certificeringsinstantie indienen.

    ![tekenen][img-portal-vm-location]
7. Klik op **Create**. Hallo VM start toodeploy. Binnen enkele minuten, wordt de implementatie en kunt beginnen met toocreate Hallo afbeelding voor de SKU.

### <a name="33-develop-your-vhd-in-hello-cloud"></a>3.3 uw VHD in de cloud Hallo ontwikkelen
Het is raadzaam dat u uw VHD in de cloud Hallo ontwikkelen met behulp van Remote Desktop Protocol (RDP). U verbinden tooRDP met Hallo-gebruikersnaam en wachtwoord die zijn opgegeven tijdens het inrichten.

> [!IMPORTANT]
> Als u uw VHD ontwikkelt op locatie (dit wordt niet aanbevolen), Zie [maken van de installatiekopie van een virtuele machine op de lokale](marketplace-publishing-vm-image-creation-on-premise.md). Downloaden van de VHD is niet nodig als u in de cloud Hallo ontwikkelt.
>
>

**Verbinden via RDP met Hallo [Microsoft Azure-portal][link-azure-portal]**

1. Selecteer **Bladeren** > **VMs**.
2. Hallo virtuele machines blade wordt geopend. Zorg ervoor dat Hallo VM die u wilt dat tooconnect met wordt uitgevoerd en selecteert u deze in Hallo lijst met geïmplementeerde VM's.
3. Een blade geopend die worden beschreven Hallo geselecteerd VM. Klik aan de bovenkant Hallo **Connect**.
4. U bent na vragen aan gebruiker tooenter Hallo-gebruikersnaam en wachtwoord die u hebt opgegeven tijdens het inrichten.

**Verbinden via RDP met behulp van PowerShell**

een extern bureaublad bestand tooa lokale machine toodownload gebruiken Hallo [cmdlet Get-AzureRemoteDesktopFile][link-technet-2]. In volgorde toouse deze cmdlet, moet u tooknow Hallo-naam van Hallo-service en de naam van Hallo VM. Als u Hallo VM vanuit Hallo gemaakt [Microsoft Azure-portal][link-azure-portal], u vindt deze informatie onder VM-eigenschappen:

1. Selecteer in de Microsoft Azure-portal hello, **Bladeren** > **VMs**.
2. Hallo virtuele machines blade wordt geopend. Selecteer Hallo VM die u hebt geïmplementeerd.
3. Een blade geopend die worden beschreven Hallo geselecteerd VM.
4. Klik op **Eigenschappen**.
5. het eerste deel van de domeinnaam Hallo Hallo is Hallo servicenaam. Hallo-hostnaam is Hallo VM-naam.

    ![tekenen][img-portal-vm-rdp]
6. Hallo cmdlet toodownload Hallo RDP-bestand voor de lokale bureaublad Hallo gemaakt VM toohello van beheerder is als volgt.

        Get‐AzureRemoteDesktopFile ‐ServiceName “baseimagevm‐6820cq00” ‐Name “BaseImageVM” –LocalPath “C:\Users\Administrator\Desktop\BaseImageVM.rdp”

Meer informatie over RDP vindt u op MSDN in Hallo artikel [tooan Azure VM verbinding met RDP of SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx).

**Een virtuele machine te configureren en uw SKU maken**

Na het Hallo-besturingssysteem die VHD wordt gedownload, gebruik van Hyper-v en configureren van een VM-toobegin maken van uw SKU. Gedetailleerde stappen kunnen u vinden op TechNet koppeling Hallo: [Hyper-v installeren en configureren van een virtuele machine](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="34-choose-hello-correct-vhd-size"></a>3.4 Hallo juist VHD grootte kiezen
Hallo Windows-besturingssysteem VHD in uw VM-installatiekopie moet worden gemaakt als een vaste indeling 128 GB VHD.  

Als Hallo fysieke grootte minder dan 128 GB is, moet VHD Hallo sparse zijn. Hallo Windows en SQL Server basisinstallatiekopieën opgegeven al aan deze vereisten voldoet, dus Hallo-indeling of Hallo grootte van Hallo verkregen van de VHD niet wijzigen.  

Gegevensschijven mag even groot zijn als 1 TB. Bij het kiezen van de schijfgrootte hello, houd er rekening mee dat klanten VHD's binnen een afbeelding kunnen niet op Hallo moment van implementatie aangepast. Gegevens schijf VHD's moeten worden gemaakt als een vaste indeling VHD. Ze moeten ook worden verspreid. Gegevensschijven kunnen leeg zijn of gegevens bevatten.

### <a name="35-install-hello-latest-windows-patches"></a>3.5 installeren de nieuwste Windows patches Hallo
Hallo basisinstallatiekopieën bevatten de meest recente patches Hallo up tootheir gepubliceerde datum. Zorg ervoor dat Windows Update is uitgevoerd en dat alle nieuwste kritiek Hallo en belangrijke updates zijn geïnstalleerd voordat het publiceren van het besturingssysteem Hallo VHD die u hebt gemaakt.

### <a name="36-perform-additional-configuration-and-schedule-tasks-as-necessary"></a>3.6 uitvoeren van extra taken voor de configuratie en planning indien nodig
Wanneer u aanvullende configuratie nodig hebt, overweeg het gebruik van een geplande taak die wordt uitgevoerd op opstarten toomake een definitieve wijzigingen toohello VM nadat deze is geïmplementeerd:

* Het is een best practice toohave Hallo taak zelf verwijderen na voltooiing van uitvoering.
* Er is geen configuratie verstandig stations dan stations C of D, omdat dit zijn slechts twee Hallo-stations die zijn altijd tooexist gegarandeerd. Station C is besturingssysteemschijf hello en station D is Hallo tijdelijke lokale schijf.

### <a name="37-generalize-hello-image"></a>3.7 generaliseer Hallo installatiekopie
Alle installatiekopieën in hello Azure Marketplace moet herbruikbare op algemene wijze. Met andere woorden, moet het besturingssysteem Hallo VHD worden gegeneraliseerd:

* Hallo-installatiekopie moet voor Windows, 'Sysprep voorbereide' en geen configuraties worden uitgevoerd die geen ondersteuning voor Hallo bieden **sysprep** opdracht.
* U kunt de volgende opdracht uit Hallo directory % windir%\System32\Sysprep Hallo uitvoeren.

        sysprep.exe /generalize /oobe /shutdown

  Hulp bij hoe toosysprep Hallo-besturingssysteem is opgegeven in stap van de volgende MSDN-artikel Hallo: [maken en uploaden van een Windows Server-VHD tooAzure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="4-deploy-a-vm-from-your-vhds"></a>4. Geen VM implementeren vanaf uw VHD 's
Nadat u uw VHD's (Hallo gegeneraliseerd besturingssysteem-VHD en nul of meer gegevens schijf VHD's) hebt geüpload tooan Azure storage-account, kunt u ze registreren als een installatiekopie van een virtuele machine. Vervolgens kunt u die afbeelding testen. Houd er rekening mee dat omdat uw besturingssysteem-VHD is gegeneraliseerd, u niet rechtstreeks Hallo VM implementeren doordat Hallo VHD URL.

toolearn meer informatie over de VM-installatiekopieën revisie Hallo blogberichten te volgen:

* [VM-installatiekopie](https://azure.microsoft.com/blog/vm-image-blog-post/)
* [VM Image PowerShell hoe](https://azure.microsoft.com/blog/vm-image-powershell-how-to-blog-post/)
* [Over de installatiekopieën van de virtuele machine in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)

### <a name="set-up-hello-necessary-tools-powershell-and-azure-cli"></a>Hallo vereiste hulpprogramma's, PowerShell en Azure CLI instellen
* [Hoe toosetup PowerShell](/powershell/azure/overview)
* [Hoe toosetup Azure CLI](../cli-install-nodejs.md)

### <a name="41-create-a-user-vm-image"></a>4.1 een installatiekopie van een virtuele machine maken
#### <a name="capture-vm"></a>Vastleggen van VM
Lees Hallo koppelingen hieronder voor hulp bij het vastleggen van Hallo VM die gebruikmaakt van PowerShell-API/Azure CLI.

* [API](https://msdn.microsoft.com/library/mt163560.aspx)
* [PowerShell](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Azure-CLI](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="generalize-image"></a>Generaliseer installatiekopie
Lees Hallo koppelingen hieronder voor hulp bij het vastleggen van Hallo VM die gebruikmaakt van PowerShell-API/Azure CLI.

* [API](https://msdn.microsoft.com/library/mt269439.aspx)
* [PowerShell](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Azure-CLI](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="42-deploy-a-vm-from-a-user-vm-image"></a>4.2 geen VM implementeren vanaf een installatiekopie van een virtuele machine
toodeploy een virtuele machine van een installatiekopie van een virtuele machine, kunt u de huidige Hallo [Azure-portal](https://manage.windowsazure.com) of PowerShell.

**Geen VM implementeren vanaf Hallo huidige Azure-portal**

1. Ga te**nieuw** > **Compute** > **virtuele machine** > **vanuit galerie**.

    ![tekenen][img-manage-vm-new]
2. Ga te**Mijn afbeeldingen**, en vervolgens selecteert Hallo VM-installatiekopie uit welke toodeploy een virtuele machine:

   1. Betalen aandacht toowhich-installatiekopie die u selecteert, omdat Hallo **Mijn afbeeldingen** weergave bevat zowel installatiekopieën van besturingssystemen en VM-installatiekopieën.
   2. Bekijkt hello aantal schijven kunt u bepalen welk type installatiekopie die u implementeert, omdat er meer dan één schijf Hallo meerderheid van de VM-installatiekopieën. Het is echter nog steeds mogelijk toohave een VM-afbeelding met slechts één besturingssysteemschijf, die vervolgens **aantal schijven** too1 ingesteld.

      ![tekenen][img-manage-vm-select]
3. Voer de wizard voor het maken van VM Hallo en Hallo VM-naam, VM-grootte, locatie, gebruikersnaam en wachtwoord opgeven.

**Een virtuele machine vanuit PowerShell implementeren**

toodeploy die een grote virtuele machine uit Hallo gegeneraliseerd VM-installatiekopie zojuist hebt gemaakt, kunt u Hallo cmdlets volgen.

    $img = Get-AzureVMImage -ImageName "myVMImage"
    $user = "user123"
    $pass = "adminPassword123"
    $myVM = New-AzureVMConfig -Name "VMImageVM" -InstanceSize "Large" -ImageName $img.ImageName | Add-AzureProvisioningConfig -Windows -AdminUsername $user -Password $pass
    New-AzureVM -ServiceName "VMImageCloudService" -VMs $myVM -Location "West US" -WaitForBoot

> [!IMPORTANT]
> Zie [probleemoplossing problemen aangetroffen tijdens het maken van de VHD] voor assistentie.
>
>

## <a name="5-obtain-certification-for-your-vm-image"></a>5. Certificeringsinstantie voor uw VM-installatiekopie verkrijgen
volgende stap bij het voorbereiden van uw VM-installatiekopie op Hallo Azure Marketplace Hallo is toohave die het gecertificeerd.

Dit proces omvat een hulpprogramma voor speciale certificering, Hallo verificatie resultaten toohello uploaden Azure container waarin uw VHD's zich bevinden, toe te voegen een aanbieding voor het definiëren van uw SKU en verzenden van uw virtuele machine image voor certificering.

### <a name="51-download-and-run-hello-certification-test-tool-for-azure-certified"></a>5.1 downloaden en uitvoeren van Hallo certificeringsinstantie Test hulpprogramma voor Azure gecertificeerd
Hallo certificeringsinstantie hulpprogramma wordt uitgevoerd op een actieve virtuele machine van de VM-installatiekopie van de gebruiker is ingericht, tooensure die Hallo VM-installatiekopie is compatibel met Microsoft Azure. Het controleren of Hallo richtlijnen en over het voorbereiden van uw VHD-vereisten is voldaan. Hallo-uitvoer van Hallo hulpprogramma is een compatibiliteitsrapport die moet worden geüpload op Hallo Publishing Portal tijdens aanvragende certificeringsinstantie.

Hallo certificeringsinstantie hulpprogramma kan worden gebruikt met Windows- en Linux-machines. Deze tooWindows-VM's via PowerShell verbinding maakt en verbindt tooLinux VM's via SSH.Net:

1. Eerst download Hallo certificeringsinstantie hulpprogramma op Hallo [Microsoft-website][link-msft-download].
2. Hallo certificeringsinstantie hulpprogramma openen en klik vervolgens op Hallo **nieuwe Test Start** knop.
3. Van Hallo **informatie testen** scherm, voer een naam voor het Hallo-test uitvoeren.
4. Bepaal of uw VM op Linux of op Windows draait. Afhankelijk van die u kiest, selecteert u de volgende opties Hallo.

### <a name="connect-hello-certification-tool-tooa-linux-vm-image"></a>**Verbinding maken met de Hallo certificeringsinstantie hulpprogramma tooa Linux VM-installatiekopie**
1. Selecteer Hallo SSH-verificatiemodus: wachtwoord of sleutel bestand.
2. Als verificatie op basis van wachtwoorden, Voer Hallo Domain Name System (DNS) naam, gebruikersnaam en wachtwoord.
3. Als de verificatie-sleutelbestand, Voer Hallo DNS-naam, gebruikersnaam en locatie van de persoonlijke sleutel.

   ![Wachtwoordverificatie van Linux VM-installatiekopie][img-cert-vm-pswd-lnx]

   ![Sleutelbestand verificatie van Linux VM-installatiekopie][img-cert-vm-key-lnx]

### <a name="connect-hello-certification-tool-tooa-windows-based-vm-image"></a>**Verbinding maken met de Hallo certificeringsinstantie hulpprogramma tooa VM op basis van Windows-installatiekopie**
1. Voer Hallo volledig gekwalificeerd VM DNS-naam (bijvoorbeeld MyVMName.Cloudapp.net).
2. Hallo-gebruikersnaam en wachtwoord invoeren.

   ![Wachtwoordverificatie van Windows VM-installatiekopie][img-cert-vm-pswd-win]

Nadat u de juiste opties Hallo voor uw Linux- of virtuele machine op basis van Windows-installatiekopie hebt geselecteerd, selecteert u **testverbinding** tooensure dat SSH.Net of PowerShell een geldige verbinding is voor testdoeleinden. Nadat een verbinding tot stand is gebracht, selecteert u **volgende** toostart Hallo test.

Wanneer het Hallo-test is voltooid, ontvangt u Hallo resultaten (mislukken-Pass/waarschuwing) voor elk element in de test.

![Testscenario's voor Linux VM-installatiekopie][img-cert-vm-test-lnx]

![Testscenario's voor VM-installatiekopie voor Windows][img-cert-vm-test-win]

Als een van de tests Hallo mislukt, wordt de afbeelding niet gecertificeerd. Als dit gebeurt, Hallo vereisten doornemen en breng de gewenste wijzigingen.

Nadat Hallo geautomatiseerd test, kunt u extra invoer tooprovide op uw VM-installatiekopie via een scherm vragenlijst wordt gevraagd.  Hallo vragen voltooien en selecteer vervolgens **volgende**.

![Certificeringsinstantie hulpprogramma vragenlijst][img-cert-vm-questionnaire]

![Certificeringsinstantie hulpprogramma vragenlijst][img-cert-vm-questionnaire-2]

Nadat u Hallo vragenlijst hebt voltooid, kunt u aanvullende informatie zoals SSH toegang tot gegevens van Hallo Linux VM-installatiekopie en een uitleg voor elke mislukte beoordelingen bieden. U kunt de resultaten bekijkt hello downloaden en logboekbestanden voor testcases Hallo uitgevoerd in toevoeging tooyour antwoorden toohello vragenlijst. Hallo resultaten opslaan in Hallo dezelfde container als uw virtuele harde schijven.

![Certificeringsinstantie testresultaten opslaan][img-cert-vm-results]

### <a name="52-get-hello-shared-access-signature-uri-for-your-vm-images"></a>5.2 Hallo shared access signature voor URI voor uw VM-installatiekopieën ophalen
Tijdens het Hallo publicatieproces, moet u Hallo uniform resource-id's (URI's) die leiden tooeach Hallo VHD's die u hebt gemaakt voor de SKU opgeven. Microsoft moet toegang toothese VHD's tijdens het Hallo-certificeringsproces. Daarom moet u een shared access signature URI toocreate voor elke VHD. Dit is Hallo URI die moet worden ingevoerd in de **installatiekopieën** tabblad in Hallo Publishing Portal.

Hallo shared access signature voor URI gemaakt moet toohello volgens de vereisten voldoen:

* Bij het genereren van shared access signature voor URI's voor uw virtuele harde schijven, zijn machtigingen lijst en lezen voldoende. Verleen geen toegang voor schrijven ('Write') of verwijderen ('Delete').
* Hallo duur om toegang te krijgen moet minimaal drie (3) de weken van bij Hallo shared access signature voor URI wordt gemaakt.
* toosafeguard voor UTC-tijd Selecteer Hallo dag vóór Hallo huidige datum. Selecteer bijvoorbeeld als Hallo de huidige datum 6 oktober 2014 valt, 5-10-2014.

SAS-URL kan worden gegenereerd in meerdere manieren tooshare uw VHD voor Azure Marketplace.
Hieronder worden Hallo 3 aanbevolen hulpprogramma's:

1.  Azure Opslagverkenner
2.  Microsoft Opslagverkenner
3.  Azure CLI

**Azure Opslagverkenner (aanbevolen voor Windows-gebruikers)**

Hieronder vindt u Hallo stappen voor het genereren van SAS-URL met behulp van Azure Storage Explorer

1. Download [Azure Storage Explorer 6 Preview 3](https://azurestorageexplorer.codeplex.com/) van CodePlex. Ga te[Azure Storage Explorer 6 Preview](https://azurestorageexplorer.codeplex.com/) en klik op **'Downloads'**.

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_01.png)

2. Download [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) en na deze ritsen installeren.

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_02.png)

3. Nadat deze is geïnstalleerd, opent u Hallo-toepassing.
4. Klik op **Account toevoegen**.

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_03.png)

5. De opslagaccountnaam hello, opslagaccountsleutel en opslag eindpunten domein opgeven. Dit is Hallo storage-account in uw Azure-abonnement waar u uw VHD hebt opgeslagen in de Azure-portal.

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_04.png)

6. Zodra het is verbonden met Azure Storage Explorer tooyour specifieke storage-account, wordt deze gestart waarin alle Hallo binnen Hallo-opslagaccount bevat. Selecteer waar u Hallo besturingssysteem schijf VHD-bestand (ook gegevensschijven als ze van toepassing zijn voor uw scenario) gekopieerd Hallo-container.

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_05.png)

7. Azure Storage Explorer start na het selecteren van de blob-container Hallo met Hallo bestanden binnen Hallo container. Selecteer Hallo installatiekopiebestand (VHD) die toobe verzonden behoeften.

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_06.png)

8.  Na het selecteren van Hallo .vhd-bestand in container hello, klikt u op Hallo **beveiliging** tabblad.

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_07.png)

9.  In Hallo **Blob-Container beveiliging** laat Hallo standaardwaarden op Hallo van het dialoogvenster **toegangsniveau** tabblad en klik vervolgens op **Shared Access Signatures** tabblad.

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_08.png)

10. Voer onderstaande toogenerate een shared access signature URI voor de VHD-installatiekopie Hallo Hallo stappen:

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_09.png)

    a. **Toegang van toegestaan:** toosafeguard voor UTC-tijd Selecteer Hallo dag vóór Hallo huidige datum. Selecteer bijvoorbeeld als Hallo de huidige datum 6 oktober 2014 valt, 5-10-2014.

    b. **Toegang is toegestaan voor:** selecteert u een datum die ten minste drie weken na Hallo **toegang toegestaan van** datum.

    c. **Acties die zijn toegestaan:** Selecteer Hallo **lijst** en **lezen** machtigingen.

    d. Als u uw VHD-bestand juist hebt geselecteerd, wordt het bestand wordt weergegeven in **Blob-naam tooaccess** met extensie VHD.

    e. Klik op **Signature genereren**.

    f. In **gegenereerd Shared Access Signature URI van deze container**, controleren op Hallo als gemarkeerde hierboven te volgen:

       - Zorg ervoor dat uw installatiekopie bestandsnaam en **".vhd"** in Hallo URI zijn.
       - Aan het einde van de Hallo Hallo handtekening, Controleer of **"rl ="** wordt weergegeven. Dit toont aan dat toegang voor lezen en de lijst met succes is opgegeven.
       - Controleer in het midden van de handtekening Hallo **' sr c = "** wordt weergegeven. Dit toont aan dat er toegangsniveau van de container

11. tooensure die Hallo gegenereerd shared access signature URI gebruikt, klikt u op **testen in de Browser**. Hallo downloadproces moet worden gestart.

12. Kopieer Hallo shared access signature voor URI. Dit is Hallo URI toopaste in Hallo Publishing Portal.

13. Herhaal stap 6-10 voor elke VHD in Hallo SKU.

**Microsoft Azure Opslagverkenner (Windows of MAC/Linux)**

Hieronder vindt u Hallo stappen voor het genereren van SAS-URL met behulp van Microsoft Azure Storage Explorer

1.  Downloaden van Microsoft Azure Storage Explorer formulier [http://storageexplorer.com/](http://storageexplorer.com/) website. Ga te[Microsoft Azure Storage Explorer](http://storageexplorer.com/releasenotes.html) en klik op **'Downloaden voor Windows'**.

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_10.png)

2.  Nadat deze is geïnstalleerd, opent u Hallo-toepassing.

3.  Klik op **Account toevoegen**.

4.  Microsoft Azure Storage Explorer tooyour abonnement aanmelden tooyour account configureren

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_11.png)

5.  Ga toostorage account en Hallo Container selecteren

6.  Selecteer **'Share Access Signature ophalen'...** met behulp van de rechtermuisknop te klikken op Hallo **container**

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_12.png)

7.  Begintijd van de update, verlooptijd en machtigingen volgens de volgende

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_13.png)

    a.  **Begintijd:** toosafeguard voor UTC-tijd Selecteer Hallo dag vóór Hallo huidige datum. Selecteer bijvoorbeeld als Hallo de huidige datum 6 oktober 2014 valt, 5-10-2014.

    b.  **Verlooptijd:** selecteert u een datum die ten minste drie weken na Hallo **begintijd** datum.

    c.  **Machtigingen:** Selecteer Hallo **lijst** en **lezen** machtigingen

8.  Shared access signature voor containers URI kopiëren

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_14.png)

    Gegenereerde SAS-URL is voor container niveau en er moet nu tooadd VHD-naam in het.

    Indeling van de Container niveau SAS-URL:`https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    De naam van de VHD invoegen na Hallo containernaam in SAS-URL zoals hieronder`https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    Voorbeeld:

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_15.png)

    TestRGVM201631920152.vhd is Hallo naam VHD wordt VHD SAS-URL`https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    - Zorg ervoor dat uw installatiekopie bestandsnaam en **".vhd"** in Hallo URI zijn.
    - Controleer in het midden van de handtekening Hallo **"sp rl ="** wordt weergegeven. Dit toont aan dat toegang voor lezen en de lijst met succes is opgegeven.
    - Controleer in het midden van de handtekening Hallo **' sr c = "** wordt weergegeven. Dit toont aan dat er toegangsniveau van de container

9.  tooensure die Hallo gegenereerde shared access signature URI werkt in de browser testen. Hallo downloadproces moet worden gestart

10. Kopieer Hallo shared access signature voor URI. Dit is Hallo URI toopaste in Hallo Publishing Portal.

11. Herhaal deze stappen voor elke VHD in Hallo SKU.

**Azure CLI (aanbevolen voor niet-Windows & continue integratie)**

Hieronder vindt u Hallo stappen voor het genereren van SAS-URL met Azure CLI

1.  Downloaden van Microsoft Azure CLI van [hier](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/). Ook vindt u koppelingen naar de andere  **[Windows](http://aka.ms/webpi-azure-cli)**  en  **[MAC OS](http://aka.ms/mac-azure-cli)**.

2.  Zodra deze is gedownload, installeer

3.  Een PowerShell-bestand met de volgende code maken en opslaan in de lokale

          $conn="DefaultEndpointsProtocol=https;AccountName=<StorageAccountName>;AccountKey=<Storage Account Key>"
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl <Permission End Date> -c $conn --start <Permission Start Date>  

    Bijwerken van de volgende Hallo in bovenstaande parameters

    a. **`<StorageAccountName>`**: Geef de naam van uw opslagaccount

    b. **`<Storage Account Key>`**: Geef de sleutel van uw opslagaccount

    c. **`<Permission Start Date>`**: toosafeguard voor UTC-tijd Selecteer Hallo dag vóór Hallo huidige datum. Bijvoorbeeld, als hello huidige datum 26 oktober 2016 wordt de waarde moet 25-10-2016

    d. **`<Permission End Date>`**: Selecteer een datum die ten minste drie weken na Hallo **begindatum**. Waarde moet **02-11-2016**.

    Hieronder volgt de voorbeeldcode Hallo na het bijwerken van de juiste parameters

          $conn="DefaultEndpointsProtocol=https;AccountName=st20151;AccountKey=TIQE5QWMKHpT5q2VnF1bb+NUV7NVMY2xmzVx1rdgIVsw7h0pcI5nMM6+DVFO65i4bQevx21dmrflA91r0Vh2Yw=="
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl 11/02/2016 -c $conn --start 10/25/2016  

4.  Powershell-editor te openen met 'Als Administrator uitvoeren'-modus en open bestand in stap #3.

5.  Voer Hallo script en bieden dat u hello SAS-URL voor het toegangsniveau van de container

    Hieronder worden Hallo-uitvoer van Hallo SAS handtekening en kopieer Hallo gemarkeerd onderdeel in een Kladblok

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_16.png)

6.  Nu krijgt u container niveau SAS-URL en moet u de naam van de VHD tooadd in deze.

    Container niveau SAS-URL #

    `https://st20151.blob.core.windows.net/vhds?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

7.  De naam van de VHD invoegen na Hallo containernaam in SAS-URL, zoals hieronder wordt weergegeven`https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    Voorbeeld:

    TestRGVM201631920152.vhd is Hallo naam VHD wordt VHD SAS-URL

    `https://st20151.blob.core.windows.net/vhds/ TestRGVM201631920152.vhd?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    - Zorg ervoor dat uw afbeeldingsbestandsnaam en ".vhd" in hello URI zijn.
    -   Controleer in het midden van de handtekening Hallo 'sp rl =' wordt weergegeven. Dit toont aan dat toegang voor lezen en de lijst met succes is opgegeven.
    -   Controleer in het midden van de handtekening Hallo ' sr = c ' wordt weergegeven. Dit toont aan dat er toegangsniveau van de container

8.  tooensure die Hallo gegenereerde shared access signature URI werkt in de browser testen. Hallo downloadproces moet worden gestart

9.  Kopieer Hallo shared access signature voor URI. Dit is Hallo URI toopaste in Hallo Publishing Portal.

10. Herhaal deze stappen voor elke VHD in Hallo SKU.


### <a name="53-provide-information-about-hello-vm-image-and-request-certification-in-hello-publishing-portal"></a>5.3 bieden informatie over de VM-installatiekopie Hallo en certificering in Hallo Publishing Portal aanvragen
Nadat u uw aanbieding en SKU hebt gemaakt, moet u Hallo installatiekopie gegevens die zijn gekoppeld aan deze SKU invoeren:

1. Ga toohello [Publishing Portal][link-pubportal], en meld u aan met uw verkopersaccount.
2. Selecteer Hallo **VM-installatiekopieën** tabblad.
3. Hallo-id weergegeven bovenaan Hallo Hallo pagina is daadwerkelijk Hallo aanbieding-id en geen Hallo-SKU-id.
4. Hallo eigenschappen onder Hallo invullen **SKU's** sectie.
5. Onder **besturingssysteemgroep**, klikt u op Hallo besturingssysteem dat is gekoppeld aan Hallo besturingssysteem-VHD.
6. In Hallo **besturingssysteem** vak, beschrijven Hallo-besturingssysteem. U kunt een notatie zoals-besturingssystemen, type, versie en updates. Een voorbeeld is 'Windows Server Datacenter 2014 R2'.
7. Selecteer toosix aanbevolen grootten van virtuele machines. Dit zijn de aanbevelingen die weergegeven toohello klant Hallo prijzen laag blade in Azure Portal Hallo krijgen wanneer ze toopurchase bepalen en implementeren van uw installatiekopie. **Dit zijn alleen aanbevelingen. Hallo klant is kunnen tooselect elke VM-grootte die geschikt is voor Hallo schijven die zijn opgegeven in uw installatiekopie.**
8. Hallo-versie in te voeren. Hallo Versieveld ingekapseld een semantische versie tooidentify Hallo product en de updates:
   * Versies moet Hallo vorm X.Y.Z, waarbij X, Y en Z gehele getallen zijn.
   * Afbeeldingen in verschillende SKU's kunnen verschillende primaire en secundaire versies hebben.
   * Versies binnen een SKU moet alleen incrementele wijzigingen, die versie van de patch hello (Z van X.Y.Z) te verhogen.
9. In Hallo **OS VHD URL** Voer Hallo shared access signature voor URI voor het besturingssysteem Hallo VHD gemaakt.
10. Als er gegevensschijven gekoppeld aan deze SKU, selecteert u Hallo logische eenheid number (LUN) toowhich die u deze gegevens schijf toobe gekoppeld bij de implementatie dat wilt.
11. In Hallo **LUN X VHD URL** Voer Hallo shared access signature voor URI voor Hallo eerste gegevens VHD gemaakt.

    ![tekenen](media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-3.png)


## <a name="common-sas-url-issues--fixes"></a>Algemene SAS-URL problemen en oplossingen

|Probleem|Foutbericht|Oplossen|Koppeling van documentatie|
|---|---|---|---|
|Fout bij het kopiëren van afbeeldingen - '? ' is niet gevonden in het SAS-url|Fout: Afbeeldingen kopiëren. Er kan geen toodownload met behulp van blob SAS-Uri opgegeven.|Bijwerken Hallo SAS-Url met aanbevolen hulpprogramma 's|[https://Azure.Microsoft.com/en-us/Documentation/articles/Storage-DotNet-Shared-Access-Signature-Part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Fout bij het kopiëren van afbeeldingen - parameters voor 'st' en 'se' niet in het SAS-url|Fout: Afbeeldingen kopiëren. Er kan geen toodownload met behulp van blob SAS-Uri opgegeven.|Hallo SAS-Url met de begin- en einddatums erop bijwerken|[https://Azure.Microsoft.com/en-us/Documentation/articles/Storage-DotNet-Shared-Access-Signature-Part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Fout bij het kopiëren van afbeeldingen - 'sp = rl' niet in het SAS-url|Fout: Afbeeldingen kopiëren. Er kan geen toodownload met behulp van blob SAS-Uri opgegeven|Hallo SAS-Url met machtigingen zijn ingesteld als 'Lezen' en 'lijst bijwerken|[https://Azure.Microsoft.com/en-us/Documentation/articles/Storage-DotNet-Shared-Access-Signature-Part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Fout bij het kopiëren van afbeeldingen - SAS-url spaties hebben in de naam van de vhd|Fout: Afbeeldingen kopiëren. Er kan geen toodownload met behulp van blob SAS-Uri opgegeven.|Hallo SAS-Url zonder spaties bijwerken|[https://Azure.Microsoft.com/en-us/Documentation/articles/Storage-DotNet-Shared-Access-Signature-Part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Fout bij het kopiëren van afbeeldingen – SAS-Url-autorisatie-fout|Fout: Afbeeldingen kopiëren. Er kan geen toodownload blob vanwege fout tooauthorization|Opnieuw genereren Hallo SAS-Url|[https://Azure.Microsoft.com/en-us/Documentation/articles/Storage-DotNet-Shared-Access-Signature-Part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|


## <a name="next-step"></a>Volgende stap
Nadat u klaar bent met Hallo SKU details, kunt u doorsturen toohello [Azure Marketplace marketing inhoud handleiding][link-pushstaging]. In deze stap Hallo publicatieproces u Hallo marketing inhoud, prijzen en andere benodigde vóór de informatie te bieden**stap 3: uw virtuele machine testen bieden in fasering**, waarin u verschillende scenario's voor use case testen voordat u implementeert Hallo aanbieding toohello Azure Marketplace voor openbare zichtbaarheid en inkoop.  

## <a name="see-also"></a>Zie ook
* [Aan de slag: hoe toopublish een aanbieding toohello Azure Marketplace](marketplace-publishing-getting-started.md)

[img-acom-1]:media/marketplace-publishing-vm-image-creation/vm-image-acom-datacenter.png
[img-portal-vm-size]:media/marketplace-publishing-vm-image-creation/vm-image-portal-size.png
[img-portal-vm-create]:media/marketplace-publishing-vm-image-creation/vm-image-portal-create-vm.png
[img-portal-vm-location]:media/marketplace-publishing-vm-image-creation/vm-image-portal-location.png
[img-portal-vm-rdp]:media/marketplace-publishing-vm-image-creation/vm-image-portal-rdp.png
[img-azstg-add]:media/marketplace-publishing-vm-image-creation/vm-image-storage-add.png
[img-manage-vm-new]:media/marketplace-publishing-vm-image-creation/vm-image-manage-new.png
[img-manage-vm-select]:media/marketplace-publishing-vm-image-creation/vm-image-manage-select.png
[img-cert-vm-key-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-keyfile-linux.png
[img-cert-vm-pswd-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-linux.png
[img-cert-vm-pswd-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-win.png
[img-cert-vm-test-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-linux.png
[img-cert-vm-test-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-win.png
[img-cert-vm-results]:media/marketplace-publishing-vm-image-creation/vm-image-certification-results.png
[img-cert-vm-questionnaire]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire.png
[img-cert-vm-questionnaire-2]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire-2.png
[img-pubportal-vm-skus]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus.png
[img-pubportal-vm-skus-2]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-2.png

[link-pushstaging]:marketplace-publishing-push-to-staging.md
[link-github-waagent]:https://github.com/Azure/WALinuxAgent
[link-azure-codeplex]:https://azurestorageexplorer.codeplex.com/
[link-azure-2]:../storage/blobs/storage-dotnet-shared-access-signature-part-2.md
[link-azure-1]:../storage/common/storage-dotnet-shared-access-signature-part-1.md
[link-msft-download]:http://www.microsoft.com/download/details.aspx?id=44299
[link-technet-3]:https://technet.microsoft.com/library/hh846766.aspx
[link-technet-2]:https://msdn.microsoft.com/library/dn495261.aspx
[link-azure-portal]:https://portal.azure.com
[link-pubportal]:https://publish.windowsazure.com
[link-sql-2014-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014enterprisewindowsserver2012r2/
[link-sql-2014-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014standardwindowsserver2012r2/
[link-sql-2014-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014webwindowsserver2012r2/
[link-sql-2012-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2enterprisewindowsserver2012/
[link-sql-2012-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2standardwindowsserver2012/
[link-sql-2012-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2webwindowsserver2012/
[link-datactr-2012-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012r2datacenter/
[link-datactr-2012]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012datacenter/
[link-datactr-2008-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2008r2sp1/
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-technet-1]:https://technet.microsoft.com/library/hh848454.aspx
[link-azure-vm-2]:./virtual-machines-linux-agent-user-guide/
[link-openssl]:https://www.openssl.org/
[link-intsvc]:http://www.microsoft.com/download/details.aspx?id=41554
[link-python]:https://www.python.org/
