---
title: uw eerste Azure Virtual Network aaaCreate | Microsoft Docs
description: Ontdek hoe toocreate een Azure-netwerk (VNet), verbinding maken met twee virtuele machines (VM) toohello VNet en toohello virtuele machines verbinding maken.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2016
ms.author: jdial
ms.openlocfilehash: 1981524cf706d5ebc83b1ff77735617550ff058a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-virtual-network"></a>Uw eerste virtuele netwerk maken

Meer informatie over hoe toocreate een virtueel netwerk (VNet) met twee subnetten maakt twee virtuele machines (VM) en verbinding maken met elke VM tooone van Hallo subnetten, zoals wordt weergegeven in de volgende afbeelding Hallo:

![Virtueel-netwerkdiagram](./media/virtual-network-get-started-vnet-subnet/vnet-diagram.png)

Een Azure-netwerk (VNet) is een weergave van uw eigen netwerk in Hallo cloud. U kunt uw Azure-netwerkinstellingen beheren en DHCP-adresblokkeringen, DNS-instellingen, beveilingsbeleidsregels en routering definiëren. meer informatie over VNet-concepten, Hallo lezen toolearn [Virtual Network-overzicht](virtual-networks-overview.md) artikel. Volgende stappen toocreate Hallo bronnen weergegeven in afbeelding Hallo Hallo voltooien:

1. [Maak een VNet met twee subnetten](#create-vnet).
2. [Maak twee virtuele machines, elk met één netwerkinterface (NIC)](#create-vms), en een network security group (NSG) tooeach NIC koppelen
3. [Tooand vanaf Hallo virtuele machines verbinding maken](#connect-to-from-vms)
4. [Verwijder alle resources](#delete-resources). U kosten voor een aantal Hallo-resources die zijn gemaakt in deze oefening terwijl deze zijn ingericht. toominimize hello kosten, na het voltooien van Hallo oefening, moet u toocomplete Hallo stappen in deze sectie toodelete Hallo resources u maakt.

Hebt u een basiskennis van hoe u een VNet nadat voltooit Hallo in dit artikel stappen kunt gebruiken. De volgende stappen zijn meegeleverd, dus u kunt meer informatie over het toouse VNets op een dieper niveau.

## <a name="create-vnet"></a>Een virtueel netwerk met twee subnetten maken

toocreate een virtueel netwerk met twee subnetten, volledige Hallo stappen volgen. Verschillende subnetten zijn meestal toocontrol Hallo verkeersstroom tussen subnetten gebruikt.

1. Meld u bij toohello [Azure-portal](<https://portal.azure.com>). Als u nog geen account hebt, kunt u zich registreren voor een [gratis proefversie van één maand](https://azure.microsoft.com/free). 
2. In Hallo **Favorieten** deelvenster van de portal hello, klikt u op **nieuw**.
3. In Hallo **nieuw** blade, klikt u op **Networking**. In Hallo **Networking** blade, klikt u op **virtueel netwerk**, zoals weergegeven in de volgende afbeelding Hallo:

    ![Virtueel-netwerkdiagram](./media/virtual-network-get-started-vnet-subnet/virtual-network.png)

4.  In Hallo **virtueel netwerk** blade laat *Resource Manager* geselecteerd als Hallo-implementatiemodel, en klik op **maken**.
5.  In Hallo **de blade virtueel netwerk maken** dat wordt weergegeven, Voer Hallo volgende waarden en klik op **maken**:

    |**Instelling**|**Waarde**|**Details**|
    |---|---|---|
    |**Naam**|*MyVNet*|Hallo-naam moet uniek zijn binnen het Hallo-resourcegroep.|
    |**Adresruimte**|*10.0.0.0/16*|U kunt elke gewenste adresruimte opgeven in CIDR-notatie.|
    |**Subnetnaam**|*Front-end*|Hallo subnetnaam moet uniek zijn binnen het virtuele netwerk Hallo.|
    |**Subnetadresbereik**|*10.0.0.0/24*| Hallo bereik dat u opgeeft moet bestaan binnen het Hallo-adresruimte die u hebt gedefinieerd voor het virtuele netwerk Hallo.|
    |**Abonnement**|*[Uw abonnement]*|Selecteer een abonnement toocreate hello VNet in. Een VNet bestaat binnen één abonnement.|
    |**Resourcegroep**|**Nieuwe maken:** *MyRG*|Maak een resourcegroep. de naam van resourcegroep Hallo moet uniek zijn binnen het Hallo-abonnement die u hebt geselecteerd. meer informatie over resourcegroepen lezen Hallo toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-groups) overzichtsartikel.|
    |**Locatie**|*VS - west*| Normaal gesproken is Hallo locatie die het dichtst tooyour fysieke locatie ingeschakeld.|

    Hallo VNet duurt een paar seconden toocreate. Nadat deze gemaakt, ziet u hello Azure-portaldashboard.

6. Met de Hallo virtueel netwerk in hello Azure-portal gemaakt **Favorieten** deelvenster, klikt u op **alle resources**. Klik op Hallo **MyVNet** virtuele netwerk in Hallo **alle resources** blade. Als u hebt geselecteerd al Hallo-abonnement verschillende resources heeft, kunt u *MyVNet* in Hallo **filteren op naam...** vak tooeasily toegang hello VNet.
7. Hallo **MyVNet** blade wordt geopend en geeft informatie weer over Hallo VNet, zoals wordt weergegeven in de volgende afbeelding Hallo:

    ![Virtueel-netwerkdiagram](./media/virtual-network-get-started-vnet-subnet/myvnet.png)

8. Zoals u in de vorige afbeelding hello, klikt u op **subnetten** toodisplay een lijst met subnetten in VNet Hallo Hallo. Hallo alleen subnet dat aanwezig is **front-**, Hallo subnet dat u in stap 5 hebt gemaakt.
9. In Hallo MyVNet - blade subnetten klikt u op **+ Subnet** toocreate een subnet met Hallo informatie en klik op volgende **OK** toocreate Hallo subnet:

    |**Instelling**|**Waarde**|**Details**|
    |---|---|---|
    |**Naam**|*Back-end*|Hallo-naam moet uniek zijn binnen het virtuele netwerk Hallo.|
    |**Adresbereik**|*10.0.1.0/24*|Hallo bereik dat u opgeeft moet bestaan binnen het Hallo-adresruimte die u hebt gedefinieerd voor het virtuele netwerk Hallo.|
    |**Netwerkbeveiligingsgroep** en **Routetabel**|*Geen* (standaard)|Netwerkbeveiligingsgroepen (NSG's) worden verderop in dit artikel besproken. meer informatie over de gebruiker gedefinieerde routes, Hallo lezen toolearn [gebruiker gedefinieerde routes](virtual-networks-udr-overview.md) artikel.|

10. Nadat de nieuwe subnet Hallo is toohello VNet toegevoegd, kunt u Hallo sluiten **MyVNet – subnetten** blade en klik op sluiten Hallo **alle resources** blade.

## <a name="create-vms"></a>Virtuele machines maken

Met de Hallo VNet en subnetten gemaakt, kunt u Hallo virtuele machines maken. Voor deze oefening beide VM Hallo Windows Server-besturingssysteem draait, hoewel ze mogen uitvoeren elk besturingssysteem dat wordt ondersteund door Azure, met inbegrip van verschillende verschillende Linux-distributies.

### <a name="create-web-server-vm"></a>Hallo-webserver VM maken

toocreate hello webserver VM, volledige Hallo stappen te volgen:

1. Klik in deelvenster hello Azure portal Favorieten op **nieuw**, **Compute**, klikt u vervolgens **Windows Server 2016 Datacenter**.
2. In Hallo **Windows Server 2016 Datacenter** blade, klikt u op **maken**.
3. In Hallo **basisbeginselen** blade die wordt weergegeven, invoeren of selecteren Hallo volgende waarden en klik op **OK**:

    |**Instelling**| **Waarde**|**Details**|
    |---|---|---|
    |**Naam**|*MyWebServer*|Deze virtuele machine fungeert als een webserver waarmee internetresources verbinding maken.|
    |**Type VM-schijf**|*SSD*|
    |**Gebruikersnaam**|*Uw keuze*|
    |**Wachtwoord en wachtwoord bevestigen**|*Uw keuze*|
    | **Abonnement**|*<Your subscription>*|Hallo-abonnement moet hetzelfde abonnement die u hebt geselecteerd in stap 5 van Hallo Hallo [een virtueel netwerk maken met twee subnetten](#create-vnet) sectie van dit artikel. Hallo VNet dat u verbinding maakt met een VM-toomust aanwezig zijn in Hallo hetzelfde abonnement, zoals Hallo VM.|
    |**Resourcegroep**|**Bestaande gebruiken:** selecteer *MyRG*|Hoewel we maken gebruik van dezelfde resourcegroep als we hebben gedaan voor Hallo VNet, Hallo Hallo resources tooexist geen in Hallo dezelfde resourcegroep.|
    |**Locatie**|*VS - west*|Hallo-locatie moet dezelfde locatie die u hebt opgegeven in stap 5 van Hallo Hallo [een virtueel netwerk maken met twee subnetten](#create-vnet) sectie van dit artikel. Virtuele machines en Hallo VNets ze verbinding maken met toomust aanwezig zijn in Hallo dezelfde locatie.|

4. In Hallo **een grootte kiezen** blade, klikt u op *DS1_V2 standaard*, klikt u vervolgens op **Selecteer**. Lees Hallo [Windows VM-grootten](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel voor een lijst van alle Windows-VM-formaten ondersteund door Azure.
5. In Hallo **instellingen** blade invoeren of selecteren Hallo volgende waarden en klik op **OK**:

    |**Instelling**|**Waarde**|**Details**|
    |---|---|---|
    |**Opslag: beheerde schijven gebruiken**|*Ja*||
    |**Virtueel netwerk**| Selecteer *MyVNet*|Kunt u een VNet dat in Hallo dezelfde bestaat locatie als Hallo VM die u maakt. meer informatie over vnet's en subnetten, Hallo lezen toolearn [virtueel netwerk](virtual-networks-overview.md) artikel.|
    |**Subnet**|Selecteer *Front-end*|U kunt elk subnet selecteert dat binnen Hallo VNet bestaat.|
    |**Openbaar IP-adres**|Accepteer de standaardinstelling Hallo|Een openbaar IP-adres, kunt u tooconnect toohello VM van Hallo Internet. meer informatie over openbare IP-adressen, Hallo lezen toolearn [IP-adressen](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses) artikel.|
    |**Netwerkbeveiligingsgroep (firewall)**|Accepteer de standaardinstelling Hallo|Klik op Hallo **(nieuw) MyWebServer-nsg** standaard NSG Hallo portal gemaakt tooview instellingen ervan. In Hallo **netwerkbeveiligingsgroep maken** blade die wordt geopend, u ziet dat er één binnenkomende regel waarmee TCP/3389 (RDP)-verkeer van een IP-adres.|
    |**Alle andere waarden**|Accepteer de standaardwaarden Hallo|meer informatie over de resterende instellingen lezen Hallo Hallo toolearn [over virtuele machines](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel.|

    Netwerkbeveiligingsgroepen (NSG) kunnen u binnenkomend en uitgaand regels toocreate voor Hallo type netwerkverkeer waarop tooand van Hallo VM kan stromen. Standaard alle binnenkomend verkeer toohello VM is geweigerd. U kunt voor een productiewebserver aanvullende regels voor binnenkomende verbindingen toevoegen voor TCP/80 (HTTP) en TCP/443 (HTTPS). Er is geen regel voor uitgaand verkeer, omdat al het uitgaande verkeer standaard wordt toegestaan. U kunt toevoegen of verwijderen regels toocontrol verkeer per uw beleid. Lees Hallo [Netwerkbeveiligingsgroepen](virtual-networks-nsg.md) artikel toolearn meer informatie over nsg's.

6.  In Hallo **samenvatting** blade Hallo instellingen bekijken en klik op **OK** toocreate Hallo VM. Een tegel status wordt weergegeven op Hallo portaldashboard als Hallo die VM maakt. Het duurt enkele minuten toocreate. U hoeft niet toowait voor toocomplete. De volgende stap toohello tijdens het Hallo-virtuele machine wordt gemaakt, kunt u blijven.

### <a name="create-database-server-vm"></a>Hallo-databaseserver VM maken

toocreate hello databaseserver VM, volledige Hallo stappen te volgen:

1.  Klik in deelvenster Hallo Favorieten op **nieuw**, **Compute**, klikt u vervolgens **Windows Server 2016 Datacenter**.
2.  In Hallo **Windows Server 2016 Datacenter** blade, klikt u op **maken**.
3.  In Hallo **blade grondbeginselen**, invoeren of selecteren Hallo volgende waarden en klik vervolgens op **OK**:

    |**Instelling**|**Waarde**|**Details**|
    |---|---|---|
    |**Naam**|*MyDBServer*|Deze virtuele machine fungeert als een databaseserver dat Hallo webserver maakt verbinding met, maar die Hallo Internet kan geen verbinding met.|
    |**Type VM-schijf**|*SSD*||
    |**Gebruikersnaam**|Uw keuze||
    |**Wachtwoord en wachtwoord bevestigen**|Uw keuze||
    |**Abonnement**|<Your subscription>|Hallo-abonnement moet hetzelfde abonnement dat u hebt geselecteerd in stap 5 van Hallo Hallo [een virtueel netwerk maken met twee subnetten](#create-vnet) sectie van dit artikel.|
    |**Resourcegroep**|**Bestaande gebruiken:** selecteer *MyRG*|Hoewel we maken gebruik van dezelfde resourcegroep als we hebben gedaan voor Hallo VNet, Hallo Hallo resources tooexist geen in Hallo dezelfde resourcegroep.|
    |**Locatie**|*VS - west*|Hallo-locatie moet dezelfde locatie die u hebt opgegeven in stap 5 van Hallo Hallo [een virtueel netwerk maken met twee subnetten](#create-vnet) sectie van dit artikel.|

4.  In Hallo **een grootte kiezen** blade, klikt u op *DS1_V2 standaard*, klikt u vervolgens op **Selecteer**.
5.  In Hallo **instellingen** blade invoeren of selecteren Hallo volgende waarden en klik op **OK**:

    |**Instelling**|**Waarde**|**Details**|
    |----|----|---|
    |**Opslag: beheerde schijven gebruiken**|*Ja*||
    |**Virtueel netwerk**|Selecteer *MyVNet*|Kunt u een VNet dat in Hallo dezelfde bestaat locatie als Hallo VM die u maakt.|
    |**Subnet**|Selecteer *Back-end* door te klikken op Hallo **Subnet** vak te selecteren **Back-end** van Hallo **Kies een subnet** blade|U kunt elk subnet selecteert dat binnen Hallo VNet bestaat.|
    |**Openbaar IP-adres**|Geen – Hallo standaardadres Klik **geen** van Hallo **openbare IP-adres kiezen** blade|Zonder een openbaar IP-adres, u kunt alleen verbinding toohello VM uit een andere virtuele machine verbonden toohello hetzelfde VNet. U kunt tooit kan geen verbinding rechtstreeks vanuit Hallo Internet.|
    |**Netwerkbeveiligingsgroep (firewall)**|Accepteer de standaardinstelling Hallo| Zoals Hallo standaard die NSG voor Hallo MyWebServer VM, deze NSG ook gemaakt Hallo heeft standaard dezelfde regel voor binnenkomende verbindingen. U kunt voor een databaseserver een aanvullende regel voor binnenkomende verbindingen voor TCP/1433 (MS SQL) toevoegen. Er is geen regel voor uitgaand verkeer, omdat al het uitgaande verkeer standaard wordt toegestaan. U kunt toevoegen of verwijderen regels toocontrol verkeer per uw beleid.|
    |**Alle andere waarden**|Accepteer de standaardwaarden Hallo||

6.  In Hallo **samenvatting** blade Hallo instellingen bekijken en klik op **OK** toocreate Hallo VM. Een tegel status wordt weergegeven op Hallo portaldashboard als Hallo die VM maakt. Het duurt enkele minuten toocreate. U hoeft niet toowait voor toocomplete. De volgende stap toohello tijdens het Hallo-virtuele machine wordt gemaakt, kunt u blijven.

## <a name="review"></a>Resources controleren

Hoewel u een VNet en twee virtuele machines, hello Azure-portal enkele aanvullende bronnen voor u gemaakt op Hallo MyRG resourcegroep hebt gemaakt. Bekijkt hello inhoud van Hallo MyRG resourcegroep door Hallo volgende stappen uit te voeren:

1. In Hallo **Favorieten** deelvenster, klikt u op **meer services**.
2. In Hallo **meer services** deelvenster, type *resourcegroepen* in Hallo-vak met Hallo woord *Filter* erin. Klik op **resourcegroepen** wanneer u deze bekijken in Hallo lijst gefilterd.
3. In Hallo **resourcegroepen** deelvenster, klikt u op Hallo *MyRG* resourcegroep. Als u veel bestaande resourcegroepen in uw abonnement hebt, typt u *MyRG* in Hallo vak waarin tekst hello *filteren op naam...* tooquickly toegang Hallo MyRG resourcegroep.
4.  In Hallo **MyRG** blade ziet u die resourcegroep Hallo 12 bronnen bevat, zoals wordt weergegeven in de volgende afbeelding Hallo:

    ![Inhoud resourcegroep](./media/virtual-network-get-started-vnet-subnet/resource-group-contents.png)

meer informatie over virtuele machines, schijven en storage-accounts lezen Hallo toolearn [virtuele machine](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [schijf](../virtual-machines/windows/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-network%2ftoc.json), en [opslagaccount](../storage/common/storage-introduction.md?toc=%2fazure%2fvirtual-network%2ftoc.json) overzicht artikelen. Hallo twee standaard nsg's Hallo-portal voor u gemaakt, kunt u zien. U ziet ook dat Hallo portal twee netwerkbronnen interface (NIC) gemaakt. Een NIC kunt een VM-netwerkbronnen tooconnect tooother via Hallo VNet. Lees Hallo [NIC](virtual-network-network-interface.md) artikel toolearn meer informatie over NIC's. Hallo-portal gemaakt ook een bron van het openbare IP-adres. Openbare IP-adressen zijn één instelling voor een openbare IP-adresresource. meer informatie over openbare IP-adressen, Hallo lezen toolearn [IP-adressen](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses) artikel.

## <a name="connect-to-from-vms"></a>Verbinding maken met virtuele machines toohello

Met uw VNet en twee virtuele machines die zijn gemaakt, kunt u nu toohello VMs verbinden via Hallo stappen in Hallo uit te voeren:

### <a name="connect-from-internet"></a>Webserver toohello VM vanaf Hallo Internet verbinding maken

tooconnect toohello webserver VM van Hallo Internet, volledige Hallo stappen te volgen:

1. In de portal Hallo open Hallo MyRG resourcegroep door te voeren Hallo stappen voor het Hallo [resources bekijken](#review) sectie van dit artikel.
2. In Hallo **MyRG** blade, klikt u op Hallo **MyWebServer** VM.
3. In Hallo **MyWebServer** blade, klikt u op **Connect**, zoals weergegeven in de volgende afbeelding Hallo:

    ![Verbinding maken met server tooweb VM](./media/virtual-network-get-started-vnet-subnet/webserver.png)

4. Uw browser toodownload Hallo toestaan *MyWebServer.rdp* en het bestand vervolgens openen.
5. Als u een dialoogvenster vak geïnformeerd u die Hallo-uitgever van Hallo externe verbinding kan niet worden gecontroleerd krijgt, klikt u op **Connect**.
6. Wanneer u uw referenties invoert, zorg ervoor dat u zich aanmelden met het Hallo-gebruikersnaam en wachtwoord die u hebt opgegeven in stap 3 van Hallo [maken Hallo webserver VM](#create-web-server-vm) sectie van dit artikel. Als hello **Windows-beveiliging** vak dat wordt weergegeven, de juiste referenties Hallo wordt niet weergegeven, moet u mogelijk tooclick **meer opties**, klikt u vervolgens **gebruik een ander account**, zodat u kunt Hallo juiste gebruikersnaam en wachtwoord opgeven). Klik op **OK** tooconnect toohello VM.
7. Als u krijgt een **verbinding met extern bureaublad** vak geïnformeerd dat de identiteit van de externe computer Hallo Hallo kan niet worden gecontroleerd, klikt u op **Ja**.
8. U bent verbonden toohello MyWebServer VM van Hallo Internet. Hallo-verbinding met extern bureaublad openen toocomplete Hallo stappen in de volgende sectie Hallo laat.

Hallo externe verbinding is toohello openbaar IP-adres toegewezen toohello openbare IP-adres resource Hallo portal gemaakt in stap 5 van Hallo [een virtueel netwerk maken met twee subnetten](#create-vnet) sectie van dit artikel. Hallo-verbinding is toegestaan, omdat Hallo standaardregel in Hallo gemaakt **MyWebServer nsg** NSG TCP/3389 (RDP) toegestaan inkomende toohello VM van een IP-adres. Als u tooconnect toohello VM via een andere poort probeert, Hallo verbinding worden gemaakt, tenzij u extra regels voor binnenkomende verbindingen toohello NSG waardoor Hallo extra poorten toevoegen.

>[!NOTE]
>Als u extra regels voor binnenkomende verbindingen toohello NSG toevoegt, zorg ervoor dat Hallo dezelfde poorten zijn geopend op Hallo Windows firewall of Hallo verbinding mislukt.
>

### <a name="connect-to-internet"></a>Verbinding maken met Internet toohello van webserver Hallo VM

tooconnect uitgaande toohello Internet van de webserver Hallo VM, volledige Hallo stappen te volgen:

1. Als u een verbinding met extern toohello MyWebServerVM openen nog geen hebt, een externe verbinding toohello VM maken door de stappen in Hallo Hallo [Connect toohello webserver VM van Hallo Internet](#connect-from-internet) sectie van dit artikel.
2. Open Internet Explorer Hallo Windows-bureaublad. In Hallo **Setup Internet Explorer 11** in het dialoogvenster, klikt u op **geen aanbevolen instellingen gebruiken**, klikt u vervolgens op **OK**. Het is aanbevolen tooaccept Hallo aanbevolen instellingen voor een productieserver.
3. Voer in Internet Explorer adresbalk Hallo [bing.com](http:www.bing.com). Als er een dialoogvenster voor Internet Explorer, klikt u op **toevoegen**, klikt u vervolgens **toevoegen** in Hallo **vertrouwde websites** dialoogvenster en klik op **sluiten**. Herhaal dit proces voor alle andere dialoogvensters van Internet Explorer.
4. Zoeken op Hallo Bing pagina, voert u *whatsmyipaddress*, klikt u op Hallo Vergrootglas knop. Bing retourneert Hallo openbare IP-adres toegewezen toohello openbare IP-adres resource gemaakt door Hallo portal wanneer u Hallo VM gemaakt. Als u instellingen voor Hallo Hallo onderzoeken **MyWebServer-IP-** resource, ziet u Hallo hetzelfde IP-adres toegewezen toohello openbare IP-adres resource, zoals in afbeelding Hallo die volgt. Hallo IP-adres toegewezen tooyour VM verschilt echter.

    ![Verbinding maken met server tooweb VM](./media/virtual-network-get-started-vnet-subnet/webserver-pip.png)

5.  Hallo-verbinding met extern bureaublad openen toocomplete Hallo stappen in de volgende sectie Hallo laat.

U zijn kunt tooconnect toohello Internet van Hallo VM omdat alle uitgaande verbinding van VM Hallo standaard is toegestaan. U kunt uitgaande verbinding beperken door het toevoegen van aanvullende regels toohello NSG toegepast toohello NIC, toohello subnet Hallo NIC is verbonden, of beide.

Als Hallo VM wordt geplaatst Hallo gestopt (toewijzing ongedaan gemaakt) staat met Hallo-portal, Hallo openbaar IP-adres kunt wijzigen. Als u nodig hebt met het openbare IP-adres Hallo adres nooit veranderen, kunt u de statische toewijzingsmethode Hallo voor Hallo IP-adres in plaats van Hallo dynamische toewijzingsmethode (dit is standaard Hallo). Hallo toolearn informatie over de verschillen tussen toewijzingsmethoden, Hallo lezen [IP-adres typen en toewijzingsmethoden](virtual-network-ip-addresses-overview-arm.md) artikel.

### <a name="webserver-to-dbserver"></a>Verbinding maken met databaseserver toohello VM van de webserver Hallo VM

tooconnect toohello databaseserver VM van de webserver Hallo VM, volledige Hallo stappen te volgen:

1. Als u een verbinding met extern toohello MyWebServer VM openen nog geen hebt, een externe verbinding toohello VM maken door de stappen in Hallo Hallo [Connect toohello webserver VM van Hallo Internet](#connect-from-internet) sectie van dit artikel.
2. Klik op de startknop Hallo in Hallo linkerbenedenhoek van het Windows-bureaublad Hallo en vervolgens typt *extern bureaublad*. Als Hallo Start menulijst bevat **verbinding met extern bureaublad**, klik erop.
3. In Hallo **verbinding met extern bureaublad** dialoogvenster Voer *MijnDBServer* voor Hallo computernaam en klik op **Connect**.
4. Hallo-gebruikersnaam en wachtwoorden die u hebt opgegeven in stap 3 van Hallo [maken Hallo databaseserver VM](#create-database-server-vm) sectie van dit artikel, klikt u vervolgens op **OK**.
5. Als u een dialoogvenster vak geïnformeerd u die Hallo-identiteit van de externe computer Hallo kan niet worden gecontroleerd krijgt, klikt u op **Ja**.
6. Laat Hallo verbinding met extern bureaublad openen toocomplete Hallo in de volgende sectie Hallo stappen tooboth-servers.

U zijn kunt toomake Hallo verbinding toohello databaseserver VM van Hallo webserver VM voor Hallo volgende redenen:

- TCP/3389 inkomende verbindingen zijn ingeschakeld voor een bron-IP in Hallo standaard NSG in stap 5 van Hallo gemaakt [maken Hallo databaseserver VM](#create-database-server-vm) sectie van dit artikel.
- Start u de verbinding van de webserver Hallo VM die verbonden toohello is Hallo hetzelfde VNet als databaseserver Hallo VM. tooconnect tooa VM die beschikt niet over een openbare IP-adres toegewezen tooit, moet u verbinding maken vanaf een andere virtuele machine verbonden toohello hetzelfde VNet, zelfs wanneer Hallo VM is verbonden tooa ander subnet.
- Hoewel Hallo VM's verbonden toodifferent subnetten zijn, maakt Azure standaardroutes waarmee de verbinding tussen subnetten. U kunt maken van uw eigen echter Hallo standaardroutes overschrijven. Lees Hallo [gebruiker gedefinieerde routes](virtual-networks-udr-overview.md) artikel toolearn meer informatie over routering in Azure.

Als u een verbinding met extern toohello databaseserver VM vanaf Internet, Hallo tooinitiate probeert net als bij het Hallo [Connect toohello webserver VM van Hallo Internet](#connect-from-internet) sectie van dit artikel ziet u dat Hallo **Connect** optie wordt grijs weergegeven. Verbinding maken is niet beschikbaar omdat er geen openbare IP-adres toegewezen toohello VM, zodat binnenkomende verbindingen tooit van Hallo Internet zijn niet mogelijk.

### <a name="connect-toohello-internet-from-hello-database-server-vm"></a>Hallo-databaseserver VM toohello Internet verbinding

Verbinding met het maken van uitgaande toohello Internet vanaf Hallo databaseserver VM door Hallo volgende stappen uit te voeren:

1. Als u een verbinding met extern toohello MyDBServer VM openen vanuit Hallo MyWebServer VM nog geen hebt voltooid Hallo stappen voor het Hallo [Connect toohello databaseserver VM van de webserver Hallo VM](#webserver-to-dbserver) sectie van dit artikel.
2. Hallo Windows-bureaublad op Hallo MyDBServer VM open Internet Explorer en dialoogvensters toohello reageren, net als bij stap 2 en 3 Hallo [toohello Internet verbinding van de webserver Hallo VM](#connect-to-internet) sectie van dit artikel.
3. Voer in de adresbalk Hallo [bing.com](http:www.bing.com).
4. Klik op **toevoegen** in Hallo Internet Explorer in het dialoogvenster dat wordt weergegeven, klikt u vervolgens **toevoegen**, klikt u vervolgens **sluiten** in Hallo **vertrouwde** dialoogvenster sites. Herhaal deze stappen als er nog andere dialoogvensters worden weergegeven.
5. Zoeken op Hallo Bing pagina, voert u *whatsmyipaddress*, klikt u op Hallo Vergrootglas knop. Bing retourneert Hallo openbare IP-adres is momenteel toegewezen toohello VM door hello Azure-infrastructuur. 6. Hallo extern bureaublad toohello MyDBServer VM van Hallo MyWebServer VM sluiten en sluit vervolgens Hallo verbinding met extern toohello MyWebServer VM.

Hallo uitgaande verbinding toohello Internet is toegestaan omdat het al het uitgaande verkeer is toegestaan standaard zelfs als een openbare IP-adres resource toohello MyDBServer VM niet is toegewezen. Alle virtuele machines, standaard zijn kunnen tooconnect uitgaande toohello Internet, met of zonder een openbare IP-adres toegewezen resource-toohello VM. U bent niet kunnen tooconnect toohello openbare IP-adres van Hallo Internet, zoals u zou kunnen toofor hello MyWebServer VM met een openbare IP-adres resource die is toegewezen.

## <a name="delete-resources"></a>Alle resources verwijderen

toodelete alle resources die worden gemaakt in dit artikel wordt voltooid Hallo stappen te volgen:

1. tooview hello MyRG resourcegroep hebt gemaakt in dit artikel, volledige stappen 1-3 in Hallo [resources bekijken](#review) sectie van dit artikel. Hallo-resources in de resourcegroep Hallo nogmaals controleren. Als u Hallo MyRG resourcegroep, per de vorige stappen gemaakt ziet u Hallo 12 resources die worden weergegeven in afbeelding Hallo in stap 4.
2. Klik op Hallo MyRG blade Hallo **verwijderen** knop.
3. Hallo portal, moet u tootype Hallo-naam van Hallo resource groep tooconfirm dat u wilt dat toodelete deze. Als u resources met andere dan Hallo resources zien in stap 4 van Hallo [resources bekijken](#review) sectie van dit artikel, klikt u op **annuleren**. Als u alleen Hallo 12 resources gemaakt als onderdeel van dit artikel ziet, typt u *MyRG* hello Resourcegroepnaam, vervolgens klikt u op **verwijderen**. Een resourcegroep verwijdert, worden alle bronnen binnen de resourcegroep hello, dus altijd zeker tooconfirm Hallo inhoud van een resourcegroep voordat u het verwijdert. Hallo portal Hiermee verwijdert u alle resources binnen de resourcegroep Hallo vervolgens Hallo resourcegroep zelf verwijdert. Dit proces duurt enkele minuten.

## <a name="next-steps"></a>Volgende stappen

In deze oefening hebt u een VNet en twee virtuele machines gemaakt. U hebt tijdens het maken van deze virtuele machines een aantal aangepaste instellingen opgegeven en verschillende standaardinstellingen geaccepteerd. U wordt aangeraden Hallo artikelen, volgen voordat u implementeert productie vnet's en virtuele machines, tooensure begrijpen van alle beschikbare instellingen te lezen:

- [Virtuele netwerken](virtual-networks-overview.md)
- [Openbare IP-adressen](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses)
- [Netwerkinterfaces](virtual-network-network-interface.md)
- [Netwerkbeveiligingsgroepen](virtual-networks-nsg.md)
- [Virtuele machines](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
