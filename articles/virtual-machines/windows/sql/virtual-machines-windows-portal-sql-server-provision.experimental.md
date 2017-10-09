---
title: een virtuele Machine van SQL Server aaaProvision | Microsoft Docs
description: Maken en koppelen tooa SQL Server-virtuele machine in Azure met behulp van Hallo Portal. Deze zelfstudie wordt de modus Resource Manager Hallo.
services: virtual-machines-windows
documentationcenter: na
author: rothja
editor: 
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: jroth
experimental_id: a641df96-f27d-40
ms.openlocfilehash: aaad422d6ed47f5ca00b1ef484ac270a58e24f99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-in-hello-azure-portal"></a>Een SQL Server-machine inrichten in hello Azure Portal
> [!div class="op_single_selector"]
> * [Portal](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
> 
> 

Deze end-to-end zelfstudie ziet u hoe toouse hello Azure Portal tooprovision een virtuele machine met SQL Server.

Hello Azure virtuele machine (VM) galerie bevat diverse installatiekopieën met Microsoft SQL Server. U kunt met een paar klikken een Hallo die SQL VM van van Hallo galerie afbeeldingen selecteren en inrichten in uw Azure-omgeving.

In deze zelfstudie leert u het volgende:

* [Een SQL-VM-installatiekopie in Hallo galerie selecteren](#select-a-sql-vm-image-from-the-gallery)
* [Configureren en Hallo VM maken](#configure-the-vm)
* [Hallo-VM met extern bureaublad openen](#open-the-vm-with-remote-desktop)
* [TooSQL Server op afstand verbinding maken](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-hello-gallery"></a>Een SQL-VM-installatiekopie in Hallo galerie selecteren
1. Meld u bij toohello [Azure-portal](https://portal.azure.com) met uw account.

   > [!NOTE]
   > Als u geen Azure-account hebt, gaat u naar [Azure, gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).

2. Klik op Hallo Azure-portal, **nieuw**. Hallo wordt geopend Hallo **nieuw** blade. Hallo SQL Server VM bronnen bevinden zich in Hallo **Compute** groep Hallo Marketplace.
3. In Hallo **nieuw** blade, klikt u op **Compute** en klik vervolgens op **alle**.
4. In Hallo **Filter** tekstvak type SQL Server in en druk op ENTER-toets Hallo.

   ![Blade Virtuele machines in Azure](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. Bekijk de beschikbare SQL Server-installatiekopieën Hallo. Elke installatiekopie correspondeert met een bepaalde SQL Server-versie en een bepaald besturingssysteem. 
6. Selecteer Hallo-afbeelding voor SQL Server 2016 SP1 Developer op Windows Server 2016.

   > [!TIP]
   > Hallo ontwikkelaarsversie wordt gebruikt in deze zelfstudie, omdat het een complete-editie van SQL Server die is gratis voor testdoeleinden-ontwikkeling. U betaalt alleen voor Hallo kosten van het uitvoeren van Hallo VM.

   > [!NOTE]
   > SQL-VM-installatiekopieën bevatten Hallo licentiekosten voor SQL Server in Hallo per minuut prijzen Hallo VM die u (met uitzondering van Hallo ontwikkelaars en Express-edities maakt). SQL Server Developer is gratis voor ontwikkeling/testen (niet voor productiedoeleinden) en SQL Express is gratis voor lichte werkbelasting (minder dan 1 GB geheugen, minder dan 10 GB opslagruimte).
   > Er is een andere optie toobring-your-eigenaar-license (BYOL) en betaalt alleen Hallo VM. De namen van de installatiekopieën worden voorafgegaan door {BYOL}. Zie [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Prijsrichtlijnen voor SQL Server Azure VM's) voor meer informatie over deze opties.

7. Controleer onder **Een implementatiemodel selecteren** of **Resource Manager** is geselecteerd. Resource Manager is Hallo aanbevolen implementatiemodel voor nieuwe virtuele machines. Klik op **Create**.

    ![Virtuele SQL-machines maken met Resource Manager](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-hello-vm"></a>Hallo VM configureren
Er zijn vijf blades voor het configureren van een virtuele SQL Server-machine.

| Stap | Beschrijving |
| --- | --- |
| **Basisinstellingen** |[Basisinstellingen configureren](#1-configure-basic-settings) |
| **Grootte** |[De grootte van de virtuele machine kiezen](#2-choose-virtual-machine-size) |
| **Instellingen** |[Optionele kenmerken configureren](#3-configure-optional-features) |
| **SQL Server-instellingen** |[SQL Server-instellingen configureren](#4-configure-sql-server-settings) |
| **Samenvatting** |[Bekijk Hallo samenvatting](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a>1. Basisinstellingen configureren
Op Hallo **basisbeginselen** blade bieden Hallo volgende informatie:

* Voer een unieke **naam** in voor de virtuele machine.
* Geef een **gebruikersnaam** voor Hallo lokale beheerdersaccount op Hallo VM. Dit account wordt ook toegevoegd aan SQL Server toohello **sysadmin** vaste serverrol.
* Geef een sterk **wachtwoord** op.
* Als u meerdere abonnementen, controleert u of Hallo abonnement klopt voor Hallo nieuwe virtuele machine.
* In Hallo **resourcegroep** typt u een naam voor een nieuwe resourcegroep. U kunt ook toouse een bestaande resourcegroep op **gebruik bestaande**. Een resourcegroep is een verzameling verwante resources in Azure (virtuele machines, opslagaccounts, virtuele netwerken enz.).
  
  > [!NOTE]
  > Het is een goed idee om een nieuwe resourcegroep te maken als u het gebruik van SQL Server in Azure alleen wilt testen of hier meer over te weten wilt komen. Nadat u klaar met testen bent, Hallo resource groep tooautomatically verwijderen Hallo VM en alle resources die zijn gekoppeld aan deze resourcegroep verwijderd. Zie voor meer informatie over resourcegroepen [Overzicht van Azure Resource Manager](../../../azure-resource-manager/resource-group-overview.md).
  > 
  > 
* Selecteer een **locatie** voor uw implementatie.
* Klik op **OK** toosave Hallo instellingen.
  
    ![Blade SQL-basisbeginselen](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a>2. De grootte van de virtuele machine kiezen
Op Hallo **grootte** stap, kies de grootte van een virtuele machine in Hallo **een grootte kiezen** blade. Hallo-blade geeft in eerste instantie aanbevolen machine grootten op basis van de geselecteerde installatiekopie Hallo.

> [!IMPORTANT]
> Hallo Geschatte maandelijkse kosten weergegeven op Hallo **een grootte kiezen** blade niet SQL Server-licentiekosten omvat. Bij deze geschatte maandelijkse kosten zijn Hallo kosten van Hallo alleen VM. Voor Hallo Express en Developer-edities van SQL Server is dit Hallo totale geschatte kosten. Zie voor andere edities Hallo [pagina met prijzen virtuele Windows-Machines](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) en selecteer de doeleditie van SQL Server. Zie ook Hallo [richtlijnen voor Azure VM's van SQL Server-prijzen](virtual-machines-windows-sql-server-pricing-guidance.md).

![Opties voor de grootte van uw virtuele SQL-machine](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

Voor productieworkloads raden we u aan voor de virtuele machine een grootte te selecteren die ondersteuning biedt voor [Premium Storage](../../../storage/storage-premium-storage.md). Als u niet nodig dat niveau van de prestaties van hebt, gebruikt u Hallo **weergeven van alle** knop waarin alle opties voor machinegrootte. Voor een ontwikkelings- of testomgeving kunt u bijvoorbeeld een kleinere machinegrootte gebruiken.

> [!NOTE]
> Zie [Grootten van virtuele machines](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor meer informatie over de grootten van virtuele machines. Zie voor overwegingen met betrekking tot de grootte van een virtuele SQL Server-machine [Aanbevolen procedures voor prestaties voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).

Kies de grootte van uw machine en klik vervolgens op **Selecteren**.

## <a name="3-configure-optional-features"></a>3. Optionele kenmerken configureren
Op Hallo **instellingen** blade Azure-opslag, netwerken en -bewaking voor Hallo virtuele machine te configureren.

* Geef onder **Opslag** het **Schijftype** op (Standard of Premium (SSD)). Voor productieworkloads wordt Premium Storage aanbevolen.

> [!NOTE]
> Als u Premium (SSD) selecteert voor een machinegrootte die geen ondersteuning biedt voor Premium Storage, wordt de grootte van uw machine automatisch gewijzigd.  
> 
> 

* Onder **opslagaccount**, kunt u Hallo automatisch ingerichte opslagaccountnaam accepteren. U kunt ook klikken op **opslagaccount** toochoose een bestaande account en configureer Hallo opslagaccounttype. Azure maakt standaard een nieuw opslagaccount met lokaal redundante opslag. Zie voor meer informatie over opslagopties [Azure Storage-replicatie](../../../storage/storage-redundancy.md).
* Onder **netwerk**, kunt u automatisch ingevuld Hallo waarden accepteren. U kunt ook klikken op elke functie toomanually configureren Hallo **virtueel netwerk**, **Subnet**, **openbaar IP-adres**, en **Netwerkbeveiligingsgroep**. Houd voor Hallo doel van deze zelfstudie, Hallo standaardwaarden.
* Azure maakt **bewaking** met hetzelfde opslagaccount voor Hallo VM aangewezen Hallo standaard. U kunt deze instellingen hier wijzigen.
* Geef onder **Beschikbaarheidsset** een beschikbaarheidsset op. Hallo-doel van deze zelfstudie, kunt u selecteren **geen**. Als u van plan tooset van SQL AlwaysOn-beschikbaarheidsgroepen bent, Hallo beschikbaarheid tooavoid opnieuw maken van Hallo virtuele machine configureren.  Zie voor meer informatie [beheren Hallo beschikbaarheid van virtuele Machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Klik op **OK** wanneer u klaar bent met het configureren van deze instellingen.

## <a name="4-configure-sql-server-settings"></a>4. SQL Server-instellingen configureren
Op Hallo **SQL Server-instellingen** blade specifieke instellingen en optimalisaties voor SQL Server configureren. Hallo-instellingen die u voor SQL Server configureren kunt omvatten Hallo instellingen te volgen.

| Instelling |
| --- |
| [Connectiviteit](#connectivity) |
| [Verificatie](#authentication) |
| [Opslagconfiguratie](#storage-configuration) |
| [Automatisch patch toepassen](#automated-patching) |
| [Automatische back-up](#automated-backup) |
| [Integratie van Azure Key Vault](#azure-key-vault-integration) |
| [R Services](#r-services) |

### <a name="connectivity"></a>Connectiviteit
Onder **SQL-connectiviteit**, geef Hallo type toegang dat u wilt dat SQL Server-exemplaar toohello op deze virtuele machine. Selecteer voor Hallo doel van deze zelfstudie, **openbaar (internet)** tooallow verbindingen tooSQL Server vanaf machines of services op internet Hallo. Met deze optie selecteert, configureert Azure automatisch Hallo firewall en Hallo beveiliging groep tooallow netwerkverkeer op poort 1433.  

![SQL-connectiviteitsopties](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

tooconnect tooSQL Server via Hallo internet, ook moet u inschakelen SQL Server-verificatie, die wordt beschreven in de volgende sectie Hallo.

> [!NOTE]
> Het is mogelijk tooadd meer beperkingen voor Hallo netwerk communicatie tooyour SQL Server-VM. U kunt meer beperkingen door bewerken Hallo Netwerkbeveiligingsgroep toevoegen nadat Hallo VM is gemaakt. Zie voor meer informatie [Wat is een netwerkbeveiligingsgroep (NSG)?](../../../virtual-network/virtual-networks-nsg.md)
> 
> 

Als u liever toonot inschakelen verbindingen toohello Database-Engine via internet Hallo, kies een van de Hallo volgende opties:

* **Lokaal (alleen binnen VM)** tooallow verbindingen tooSQL Server alleen uit binnen Hallo VM.
* **Privé (binnen virtueel netwerk)** tooallow verbindingen tooSQL Server vanaf machines of services in Hallo hetzelfde virtuele netwerk.

> [!NOTE]
> installatiekopie van de virtuele machine Hallo voor SQL Server Express edition kunnen niet automatisch Hallo TCP/IP-protocol. Dit geldt ook voor openbare en particuliere connectiviteit Hallo opties. Voor de Express-editie, moet u SQL Server Configuration Manager te gebruiken[handmatig inschakelen Hallo TCP/IP-protocol](#configure-sql-server-to-listen-on-the-tcp-protocol) Hallo na het maken van VM.
> 
> 

In het algemeen moet de beveiliging verbeteren door te kiezen Hallo meest beperkende connectiviteit die voor uw scenario mogelijk is. Maar alle Hallo opties worden beveiligd via regels van de Netwerkbeveiligingsgroep en SQL/Windows-verificatie.

**Poort** too1433 standaardwaarden. U kunt een ander poortnummer opgeven.
Zie voor meer informatie [verbinding tooa SQL Server-VM (Resource Manager) | Microsoft Azure](virtual-machines-windows-sql-connect.md).

### <a name="authentication"></a>Authentication
Als u SQL Server-verificatie vereist, klikt u onder **SQL-verificatie** op **Inschakelen**.

![SQL Server-verificatie](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> Als u SQL Server tooaccess via Hallo internet (dat wil zeggen, Hallo openbare verbinding), moet u hier SQL-verificatie inschakelen. Openbare toegang toohello SQL Server vereist Hallo gebruik van SQL-verificatie.
> 
> 

Als u SQL Server-verificatie inschakelt, geeft u een **Aanmeldingsnaam** en een **Wachtwoord** op. Deze gebruikersnaam is geconfigureerd als een aanmelding voor SQL Server-verificatie en lid zijn van Hallo **sysadmin** vaste serverrol. Zie [Een verificatiemodus kiezen](http://msdn.microsoft.com/library/ms144284.aspx) voor meer informatie over de verificatiemodi.

Als u SQL Server-verificatie niet inschakelt, kunt u de lokale Administrator-account Hallo op Hallo VM tooconnect toohello SQL Server-exemplaar gebruiken.

### <a name="storage-configuration"></a>Opslagconfiguratie
Klik op **opslagconfiguratie** toospecify Hallo opslagvereisten.

![SQL-opslagconfiguratie](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> Als u Standaardopslag selecteert, is deze optie niet beschikbaar. Automatische opslagoptimalisatie is alleen beschikbaar voor Premium Storage.
> 
> 

U kunt vereisten opgeven als i/o-bewerkingen per seconde (IOP's), als doorvoer in MB/s en als totale grootte van de opslagruimte. Deze waarden configureren met behulp van de schuifregelaar Hallo. Hallo portal berekent automatisch Hallo aantal schijven op basis van deze vereisten.

Standaard wordt Azure Hallo opslag geoptimaliseerd voor 5000 IOP's, 200 MB en 1 TB aan opslagruimte. U kunt deze opslaginstellingen wijzigen op basis van de workload. Onder **opslag geoptimaliseerd voor**, selecteer een van de Hallo volgende opties:

* **Algemene** is de standaardinstelling Hallo en ondersteunt de meeste workloads.
* **Transactionele** verwerking wordt hello opslag voor OLTP-workloads van traditionele databases geoptimaliseerd.
* **Gegevensopslag** optimaliseert de hello opslag voor analyse- en rapportageworkloads.

> [!NOTE]
> Hallo bovenste limieten op Hallo schuifregelaars variëren, afhankelijk van de grootte van de geselecteerde virtuele machine.
> 
> 

### <a name="automated-patching"></a>Automatisch patchen
**Automatisch patchen** is standaard ingeschakeld. Automatisch patchen kan Azure tooautomatically patch voor SQL Server en Hallo-besturingssysteem. Geef een dag van week hello, tijd en duur van een onderhoudsvenster. Azure voert de patch uit tijdens deze onderhoudssessie. Hallo onderhoudsschema gebruikt Hallo VM landinstellingen voor de tijd. Als u niet dat Azure tooautomatically patch voor SQL Server en Hallo-besturingssysteem wilt, klikt u op **uitschakelen**.  

![Automatisch patchen van SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

Zie voor meer informatie [Automatisch patchen voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-patching.md).

### <a name="automated-backup"></a>Automatische back-up
Schakel automatische databaseback-ups in voor alle databases onder **Automatische back-up**. Automatische back-up is standaard uitgeschakeld.

Wanneer u automatische back-up van SQL inschakelt, kunt u Hallo volgende instellingen configureren:

* De retentieperiode (dagen) voor back-ups
* Storage-account toouse voor back-ups
* Versleutelingsoptie en wachtwoord voor back-ups
* Back-up maken van systeemdatabases
* Back-upschema configureren

back-up, klik op tooencrypt hello **inschakelen**. Geef vervolgens Hallo **wachtwoord**. Azure maakt een certificaat tooencrypt Hallo back-ups en maakt gebruik van Hallo opgegeven wachtwoord tooprotect dat certificaat.

![Automatische back-up van SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 Zie voor meer informatie [Automatische back-up voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).

### <a name="azure-key-vault-integration"></a>Integratie van Azure Sleutelkluis
toostore beveiligingsgeheimen in Azure voor versleuteling, klikt u op **integratie van Azure sleutelkluis** en klik op **inschakelen**.

![Integratie van Azure Sleutelkluis in SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

Hallo bevat volgende tabel Hallo parameters vereist tooconfigure Azure Sleutelkluis-integratie.

| PARAMETER | BESCHRIJVING | VOORBEELD |
| --- | --- | --- |
| **Key Vault-URL** |Hallo-locatie van de sleutelkluis Hallo. |https://contosokeyvault.vault.azure.net/ |
| **Principal-naam** |Principal-naam voor de Azure Active Directory-service. Deze naam is ook bedoeld tooas Hallo Client-ID. |fde2b411-33d5-4e11-af04eb07b669ccf2 |
| **Principal-geheim** |Principal-geheim voor de Azure Active Directory-service. Dit geheim is ook bedoeld tooas hello Clientgeheim. |9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM= |
| **Referentienaam** |**Referentienaam**: Azure Sleutelkluis-integratie maakt u een referentie binnen SQL Server, zodat Hallo VM toohave toegang toohello sleutelkluis. Kies een naam voor deze referentie. |mycred1 |

Zie voor meer informatie [Integratie van Azure Sleutelkluis configureren voor SQL Server op Azure-VM's](virtual-machines-windows-ps-sql-keyvault.md).

Wanneer u klaar bent met het configureren van de SQL Server-instellingen, klikt u op **OK**.

### <a name="r-services"></a>R services
U kunt [SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx) inschakelen. SQL Server-R-Services kunt u toouse geavanceerde analyses met SQL Server 2016. Klik op **inschakelen** op Hallo **SQL Server-instellingen** blade.

![SQL Server R Services inschakelen](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)


## <a name="5-review-hello-summary"></a>5. Bekijk Hallo samenvatting
Op Hallo **samenvatting** blade revisie Hallo samenvatting en klik op **OK** toocreate SQL Server, de resourcegroep en de resources die zijn opgegeven voor deze virtuele machine.

U kunt Hallo-implementatie van hello azure-portal bewaken. Hallo **meldingen** knop Hallo boven aan het welkomstscherm algemene status van implementatie Hallo weergegeven.

> [!NOTE]
> tooprovide u een idee op implementatie verbindingsaccounts ik een regio SQL VM toohello VS-Oost geïmplementeerd met standaardinstellingen. Deze testimplementatie nam in totaal 26 minuten toocomplete. Afhankelijk van uw regio en de geselecteerde instellingen bent u mogelijk meer of minder tijd kwijt aan de implementatie.
> 
> 

## <a name="open-hello-vm-with-remote-desktop"></a>Hallo-VM met extern bureaublad openen
Volgende stappen tooconnect toohello virtuele machine via Extern bureaublad hello gebruiken:

1. Na hello die Azure VM is gebouwd, Hallo pictogram voor Hallo weergegeven VM op uw Azure-dashboard. U kunt de virtuele machine ook vinden door te bladeren door uw bestaande virtuele machines. Klik op de nieuwe virtuele SQL-machine. De blade **Virtuele machine** wordt weergegeven. Hierop ziet u de details van uw virtuele machine.
2. Hallo boven aan het Hallo **virtuele machine** blade, klikt u op **Connect**.
3. Hallo browser downloadt een RDP-bestand voor Hallo VM. Open Hallo RDP-bestand.
    ![Extern bureaublad tooSQL VM](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-remote-desktop.png)
4. Hallo verbinding met extern bureaublad meldt dat Hallo uitgever van deze externe verbinding kan niet worden vastgesteld. Klik op **Connect** toocontinue.
5. In Hallo **Windows-beveiliging** dialoogvenster, klikt u op **gebruik een ander account**.
6. Voor **gebruikersnaam** type  **\<gebruikersnaam >**, waarbij <user name> Hallo-gebruikersnaam die u hebt opgegeven bij het instellen van Hallo VM is. U hebt een backslash vóór de naam van de Hallo tooadd.
7. Type Hallo **wachtwoord** die u eerder hebt geconfigureerd voor deze virtuele machine en klik vervolgens op **OK** tooconnect.
8. Als er een andere **verbinding met extern bureaublad** dialoogvenster wordt u gevraagd of tooconnect, klikt u op **Ja**.

Nadat u toohello SQL Server-virtuele machine verbinding maakt, kunt u SQL Server Management Studio starten en verbinding maken met Windows-verificatie met uw lokale beheerdersreferenties. Als u SQL Server-verificatie hebt ingeschakeld, kunt u ook verbinding maken met SQL-verificatie met behulp van Hallo SQL-aanmeldingsnaam en wachtwoord die u hebt geconfigureerd tijdens het inrichten.

Toegang toohello machine kunt u toodirectly wijziging machine en de SQL Server-instellingen op basis van uw vereisten. U kunt bijvoorbeeld Hallo firewallinstellingen configureren of SQL Server-configuratie-instellingen wijzigen.

## <a name="connect-toosql-server-remotely"></a>TooSQL Server op afstand verbinding maken
In deze zelfstudie wordt geselecteerd **openbare** toegang voor Hallo virtuele machine en **SQL Server-verificatie**. Deze instellingen automatisch geconfigureerde Hallo virtuele machine tooallow SQL Server-verbindingen vanaf elke client via Hallo internet (ervan uitgaande dat ze de juiste SQL-aanmelding Hallo hebben).

> [!NOTE]
> Als u niet openbaar hebt geselecteerd tijdens het inrichten, en vervolgens extra stappen zijn vereist tooaccess uw exemplaar van SQL Server op Hallo internet. Zie voor meer informatie [verbinding maken met virtuele Machine van SQL Server tooa](virtual-machines-windows-sql-connect.md).
> 
> 

Hallo uit te voeren laten zien hoe tooconnect tooyour SQL Server-exemplaar op de virtuele machine vanaf een andere computer via internet Hallo.

> [!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]
> 
> 

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het gebruik van SQL Server in Azure, [SQL Server op Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md) en Hallo [Frequently Asked Questions](virtual-machines-windows-sql-server-iaas-faq.md).

Bekijk voor een video-overzicht van SQL Server op Azure Virtual Machines [Azure VM is de beste platform voor SQL Server 2016 Hallo](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016).

[Hallo Leertraject verkennen](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) voor SQL Server op Azure virtuele machines.

