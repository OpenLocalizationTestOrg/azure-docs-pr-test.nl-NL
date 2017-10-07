---
title: een virtuele Machine van SQL Server aaaProvision | Microsoft Docs
description: Maken en koppelen tooa SQL Server-virtuele machine in Azure met behulp van Hallo-portal. Deze zelfstudie wordt de modus Resource Manager Hallo.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: acb52b180103d83715b51b46e2519211c8f0e362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-in-hello-azure-portal"></a>Een SQL Server-machine inrichten in hello Azure-portal
> [!div class="op_single_selector"]
> * [Portal](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
> 
> 

Deze end-to-end zelfstudie ziet u hoe toouse hello Azure portal tooprovision een virtuele machine met SQL Server.

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

2. Klik op Hallo Azure-portal, **nieuw**. Hallo wordt geopend Hallo **nieuw** venster.

3. In Hallo **nieuw** venster, klikt u op **Compute** en klik vervolgens op **alle**.

   ![Het venster Nieuwe berekening](./media/virtual-machines-windows-portal-sql-server-provision/azure-new-compute-blade.png)

4. Typ in het veld voor het zoeken van Hallo **SQL Server**, en druk op ENTER.

5. Klik vervolgens op Hallo **Filter** pictogram en selecteer **Microsoft** voor Hallo publisher. Klik op **gedaan** op Hallo venster toofilter Hallo filterresultaten gepubliceerd tooMicrosoft SQL Server-installatiekopieën.

   ![Het venster Virtuele machines in Azure](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. Bekijk de beschikbare SQL Server-installatiekopieën Hallo. Elke installatiekopie correspondeert met een bepaalde SQL Server-versie en een bepaald besturingssysteem.

6. Selecteer Hallo installatiekopie met de naam **gratis licentie: SQL Server 2016 SP1 Developer op Windows Server 2016**.

   > [!TIP]
   > Hallo ontwikkelaarsversie wordt gebruikt in deze zelfstudie, omdat het een complete-editie van SQL Server die is gratis voor testdoeleinden-ontwikkeling. U betaalt alleen voor Hallo kosten van het uitvoeren van Hallo VM. U hoeft zich echter gratis toochoose van Hallo installatiekopieën toouse in deze zelfstudie.

   > [!TIP]
   > SQL-VM-installatiekopieën bevatten Hallo licentiekosten voor SQL Server in Hallo per minuut prijzen Hallo VM die u (met uitzondering van Hallo ontwikkelaars en Express-edities maakt). SQL Server Developer is gratis voor ontwikkeling/testen (niet voor productiedoeleinden) en SQL Express is gratis voor lichte werkbelasting (minder dan 1 GB geheugen, minder dan 10 GB opslagruimte). Er is een andere optie toobring-your-eigenaar-license (BYOL) en betaalt alleen Hallo VM. De namen van de installatiekopieën worden voorafgegaan door {BYOL}. 
   >
   > Zie [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Prijsrichtlijnen voor SQL Server Azure VM's) voor meer informatie over deze opties.

7. Controleer onder **Een implementatiemodel selecteren** of **Resource Manager** is geselecteerd. Resource Manager is Hallo aanbevolen implementatiemodel voor nieuwe virtuele machines. 

8. Klik op **Create**.

    ![Virtuele SQL-machines maken met Resource Manager](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-hello-vm"></a>Hallo VM configureren
Er zijn vijf vensters voor het configureren van een virtuele SQL Server-machine.

| Stap | Beschrijving |
| --- | --- |
| **Basisinstellingen** |[Basisinstellingen configureren](#1-configure-basic-settings) |
| **Grootte** |[De grootte van de virtuele machine kiezen](#2-choose-virtual-machine-size) |
| **Instellingen** |[Optionele kenmerken configureren](#3-configure-optional-features) |
| **SQL Server-instellingen** |[SQL Server-instellingen configureren](#4-configure-sql-server-settings) |
| **Samenvatting** |[Bekijk Hallo samenvatting](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a>1. Basisinstellingen configureren

Op Hallo **basisbeginselen** venster bieden Hallo volgende informatie:

* Voer een unieke **naam** in voor de virtuele machine.

* Selecteer **SSD** als schijftype voor de virtuele machine voor optimale prestaties.

* Geef een **gebruikersnaam** voor Hallo lokale beheerdersaccount op Hallo VM. Dit account wordt ook toegevoegd aan SQL Server toohello **sysadmin** vaste serverrol.

* Geef een sterk **wachtwoord** op.

* Als u meerdere abonnementen, controleert u of Hallo abonnement klopt voor Hallo nieuwe virtuele machine.

* In Hallo **resourcegroep** typt u een naam voor een nieuwe resourcegroep. U kunt ook toouse een bestaande resourcegroep op **gebruik bestaande**. Een resourcegroep is een verzameling verwante resources in Azure (virtuele machines, opslagaccounts, virtuele netwerken enz.).

  > [!NOTE]
  > Het is een goed idee om een nieuwe resourcegroep te maken als u het gebruik van SQL Server in Azure alleen wilt testen of hier meer over te weten wilt komen. Nadat u klaar met testen bent, Hallo resource groep tooautomatically verwijderen Hallo VM en alle resources die zijn gekoppeld aan deze resourcegroep verwijderd. Zie voor meer informatie over resourcegroepen [Overzicht van Azure Resource Manager](../../../azure-resource-manager/resource-group-overview.md).

* Selecteer een **locatie** voor hello Azure-regio die als voor deze implementatie host fungeert.

* Klik op **OK** toosave Hallo instellingen.

    ![Venster SQL-basisbeginselen](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a>2. De grootte van de virtuele machine kiezen

Op Hallo **grootte** stap, kies de grootte van een virtuele machine in Hallo **een grootte kiezen** venster. Hallo-venster wordt in eerste instantie aanbevolen machine grootten op basis van de geselecteerde installatiekopie Hallo.

> [!IMPORTANT]
> Hallo Geschatte maandelijkse kosten weergegeven op Hallo **een grootte kiezen** venster bevat geen SQL Server-licentiekosten. Dit zijn de kosten Hallo Hallo alleen VM. Voor Hallo Express en Developer-edities van SQL Server is dit Hallo totale geschatte kosten. Zie voor andere edities Hallo [pagina met prijzen virtuele Windows-Machines](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) en selecteer de doeleditie van SQL Server. Zie ook Hallo [richtlijnen voor Azure VM's van SQL Server-prijzen](virtual-machines-windows-sql-server-pricing-guidance.md).

![Opties voor de grootte van uw virtuele SQL-machine](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

Zie voor productieworkloads Hallo aanbevolen grootten van de machine en de configuratie in [best practices prestaties for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md). Als u de grootte van een machine die niet wordt vermeld moet, klikt u op Hallo **weergeven van alle** knop.

> [!NOTE]
> Zie voor meer informatie over grootten voor virtuele machines [Grootten voor virtuele machines](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Kies de grootte van uw machine en klik vervolgens op **Selecteren**.

## <a name="3-configure-optional-features"></a>3. Optionele kenmerken configureren

Op Hallo **instellingen** venster Azure-opslag, netwerken en -bewaking voor Hallo virtuele machine te configureren.

* Onder **Opslag** selecteert u **Ja** onder **Managed Disks**.

   > [!NOTE]
   > Microsoft raadt Managed Disks aan voor SQL Server. Schijven ingangen opslag achter de schermen Hallo beheerd. Bovendien wanneer virtuele machines met beheerd schijven zich in Hallo dezelfde beschikbaarheidsset, Azure distribueert Hallo opslag resources tooprovide juiste redundantie. Zie [Azure Managed Disks overview](../../../storage/storage-managed-disks-overview.md) (Overzicht van Azure Managed Disks) voor meer informatie. Zie [Managed Disks gebruiken schijven voor virtuele machines in een beschikbaarheidsset](../manage-availability.md) voor meer informatie over Managed Disks in een beschikbaarheidsset.

* Onder **netwerk**, kunt u automatisch ingevuld Hallo waarden accepteren. U kunt ook klikken op elke functie toomanually configureren Hallo **virtueel netwerk**, **Subnet**, **openbaar IP-adres**, en **Netwerkbeveiligingsgroep**. Houd voor Hallo doel van deze zelfstudie, Hallo standaardwaarden.

* Azure maakt **bewaking** met hetzelfde opslagaccount voor Hallo VM aangewezen Hallo standaard. U kunt deze instellingen hier wijzigen.

* Onder **beschikbaarheidsset**, kunt u de standaardwaarde van Hallo laten **geen** voor deze zelfstudie. Als u van plan tooset van SQL AlwaysOn-beschikbaarheidsgroepen bent, Hallo beschikbaarheid tooavoid opnieuw maken van Hallo virtuele machine configureren.  Zie voor meer informatie [beheren Hallo beschikbaarheid van virtuele Machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Klik op **OK** wanneer u klaar bent met het configureren van deze instellingen.

## <a name="4-configure-sql-server-settings"></a>4. SQL Server-instellingen configureren
Op Hallo **SQL Server-instellingen** venster specifieke instellingen en optimalisaties voor SQL Server configureren. Hallo-instellingen die u voor SQL Server configureren kunt omvatten Hallo volgende.

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

> [!TIP]
> Standaard gebruikt SQL Server een bekende poort, namelijk **1433**. Voor een betere beveiliging Hallo-poort in het vorige dialoogvenster toolisten Hallo op een niet-standaard-poort, zoals 1401 te wijzigen. Als u dit doet, moet u deze poort gebruiken om verbinding te maken vanaf elk clienthulpprogramma, zoals SSMS.

tooconnect tooSQL Server via Hallo internet, ook moet u inschakelen SQL Server-verificatie, die wordt beschreven in de volgende sectie Hallo.

Als u liever toonot inschakelen verbindingen toohello Database-Engine via internet Hallo, kies een van de Hallo volgende opties:

* **Lokaal (alleen binnen VM)** tooallow verbindingen tooSQL Server alleen uit binnen Hallo VM.
* **Privé (binnen virtueel netwerk)** tooallow verbindingen tooSQL Server vanaf machines of services in Hallo hetzelfde virtuele netwerk.

In het algemeen moet de beveiliging verbeteren door te kiezen Hallo meest beperkende connectiviteit die voor uw scenario mogelijk is. Maar alle Hallo opties worden beveiligd via regels van de Netwerkbeveiligingsgroep en SQL/Windows-verificatie. U kunt de Netwerkbeveiligingsgroep bewerken na Hallo die virtuele machine wordt gemaakt. Zie [Veiligheidsoverwegingen voor SQL Server in virtuele Azure-machines](virtual-machines-windows-sql-security.md) voor meer informatie.

> [!NOTE]
> installatiekopie van de virtuele machine Hallo voor SQL Server Express edition kunnen niet automatisch Hallo TCP/IP-protocol. Dit geldt ook voor openbare en particuliere connectiviteit Hallo opties. Voor de Express-editie, moet u SQL Server Configuration Manager te gebruiken[handmatig inschakelen Hallo TCP/IP-protocol](#configure-sql-server-to-listen-on-the-tcp-protocol) Hallo na het maken van VM.

### <a name="authentication"></a>Authentication

Als u SQL Server-verificatie vereist, klikt u onder **SQL-verificatie** op **Inschakelen**.

![SQL Server-verificatie](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> Als u SQL Server tooaccess via Hallo internet (dat wil zeggen Hallo openbare verbinding), moet u hier SQL-verificatie inschakelen. Openbare toegang toohello SQL Server vereist Hallo gebruik van SQL-verificatie.
> 
> 

Als u SQL Server-verificatie inschakelt, geeft u een **Aanmeldingsnaam** en een **Wachtwoord** op. Deze gebruikersnaam is geconfigureerd als een aanmelding voor SQL Server-verificatie en lid zijn van Hallo **sysadmin** vaste serverrol. Zie [Een verificatiemodus kiezen](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode) voor meer informatie over de verificatiemodi.

Als u SQL Server-verificatie niet inschakelt, kunt u de lokale Administrator-account Hallo op Hallo VM tooconnect toohello SQL Server-exemplaar gebruiken.

### <a name="storage-configuration"></a>Opslagconfiguratie

Klik op **opslagconfiguratie** toospecify Hallo opslagvereisten.

![SQL-opslagconfiguratie](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> Als u handmatig de VM toouse standard-opslag hebt geconfigureerd, is deze optie niet beschikbaar. Automatische opslagoptimalisatie is alleen beschikbaar voor Premium Storage.

> [!TIP]
> Hallo aantal stopt en Hallo bovengrenzen van de schuifregelaar is afhankelijk van het Hallo-grootte van virtuele machine die u hebt geselecteerd. Een virtuele machine groter en krachtiger is kunnen tooscale meer.

U kunt vereisten opgeven als i/o-bewerkingen per seconde (IOP's), als doorvoer in MB/s en als totale grootte van de opslagruimte. Deze waarden configureren met behulp van de schuifregelaar Hallo. U kunt deze opslaginstellingen wijzigen op basis van de workload. Hallo portal berekent automatisch het aantal schijven tooattach Hallo en configureren op basis van deze vereisten.

Onder **opslag geoptimaliseerd voor**, selecteer een van de Hallo volgende opties:

* **Algemene** is de standaardinstelling Hallo en ondersteunt de meeste workloads.
* **Transactionele** verwerking wordt hello opslag voor OLTP-workloads van traditionele databases geoptimaliseerd.
* **Gegevensopslag** optimaliseert de hello opslag voor analyse- en rapportageworkloads.

### <a name="automated-patching"></a>Automatisch patchen

**Automatisch patchen** is standaard ingeschakeld. Automatisch patchen kan Azure tooautomatically patch voor SQL Server en Hallo-besturingssysteem. Geef een dag van week hello, tijd en duur van een onderhoudsvenster. Azure voert de patch uit tijdens deze onderhoudssessie. Hallo onderhoudsschema gebruikt Hallo VM landinstellingen voor de tijd. Als u niet dat Azure tooautomatically patch voor SQL Server en Hallo-besturingssysteem wilt, klikt u op **uitschakelen**.  

![Automatisch patchen van SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

Zie voor meer informatie [Automatisch patchen voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-patching.md).

### <a name="automated-backup"></a>Automatische back-up

Schakel automatische databaseback-ups in voor alle databases onder **Automatische back-up**. Automatische back-up is standaard uitgeschakeld.

Wanneer u automatische back-up van SQL inschakelt, kunt u Hallo volgende configureren:

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

### <a name="r-services"></a>R services

U hebt Hallo optie tooenable [SQL Server-Services R](https://msdn.microsoft.com/library/mt604845.aspx). Hiermee kunt u toouse geavanceerde analyses met SQL Server 2016. Klik op **inschakelen** op Hallo **SQL Server-instellingen** venster.

> [!NOTE]
> Deze optie is niet correct voor SQL Server 2016 Developer Edition uitgeschakeld door Hallo-portal. Voor de Developer Edition moet u R Services handmatig inschakelen nadat u uw virtuele machine hebt gemaakt.

![SQL Server R Services inschakelen](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)

Wanneer u klaar bent met het configureren van de SQL Server-instellingen, klikt u op **OK**.

## <a name="5-review-hello-summary"></a>5. Bekijk Hallo samenvatting

Op Hallo **samenvatting** venster revisie Hallo samenvatting en klik op **aankoop** toocreate SQL Server, de resourcegroep en de resources die zijn opgegeven voor deze virtuele machine.

U kunt Hallo-implementatie van hello Azure-portal bewaken. Hallo **meldingen** knop Hallo boven aan het welkomstscherm algemene status van implementatie Hallo weergegeven.

> [!NOTE]
> tooprovide u een idee op implementatie verbindingsaccounts ik een regio SQL VM toohello VS-Oost geïmplementeerd met standaardinstellingen. Deze testimplementatie nam in totaal 26 minuten toocomplete. Afhankelijk van uw regio en de geselecteerde instellingen bent u mogelijk meer of minder tijd kwijt aan de implementatie.

## <a name="open-hello-vm-with-remote-desktop"></a>Hallo-VM met extern bureaublad openen

Volgende stappen tooconnect toohello SQL Server-VM met extern bureaublad hello gebruiken:

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

Nadat u toohello SQL Server-virtuele machine verbinding maakt, kunt u SQL Server Management Studio starten en verbinding maken met Windows-verificatie met uw lokale beheerdersreferenties. Als u SQL Server-verificatie hebt ingeschakeld, kunt u ook verbinding maken met SQL-verificatie met behulp van Hallo SQL-aanmeldingsnaam en wachtwoord die u hebt geconfigureerd tijdens het inrichten.

Toegang toohello machine kunt u toodirectly wijziging machine en de SQL Server-instellingen op basis van uw vereisten. U kunt bijvoorbeeld Hallo firewallinstellingen configureren of SQL Server-configuratie-instellingen wijzigen.

## <a name="enable-tcpip-for-developer-and-express-editions"></a>TCP/IP inschakelen voor Developer- en Express-edities

Bij het inrichten van een nieuwe SQL Server-VM wordt Azure niet automatisch ingeschakeld Hallo TCP/IP-protocol voor SQL Server-ontwikkelaars en Express-edities. Hallo hieronder wordt uitgelegd hoe toomanually TCP/IP inschakelen zodat u kunt op afstand verbinding maken via IP-adres.

Hallo na gebruik van de stappen **SQL Server Configuration Manager** tooenable Hallo TCP/IP-protocol voor SQL Server-ontwikkelaars en Express-edities.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-toosql-server-remotely"></a>TooSQL Server op afstand verbinding maken

In deze zelfstudie wordt geselecteerd **openbare** toegang voor Hallo virtuele machine en **SQL Server-verificatie**. Deze instellingen automatisch geconfigureerde Hallo virtuele machine tooallow SQL Server-verbindingen vanaf elke client via Hallo internet (ervan uitgaande dat ze de juiste SQL-aanmelding Hallo hebben).

> [!NOTE]
> Als u tijdens het inrichten niet openbaar hebt geselecteerd, kunt u uw SQL-connectiviteit-instellingen via de portal Hallo wijzigen na het inrichten. Zie [Change your SQL connectivity settings](virtual-machines-windows-sql-connect.md#change) (SQL-verbindingsinstellingen wijzigen) voor meer informatie.

Hallo uit te voeren laten zien hoe tooconnect tooyour SQL Server-exemplaar op de virtuele machine vanaf een andere computer via internet Hallo.

> [!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over het gebruik van SQL Server in Azure, [SQL Server op Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md) en Hallo [Frequently Asked Questions](virtual-machines-windows-sql-server-iaas-faq.md).
