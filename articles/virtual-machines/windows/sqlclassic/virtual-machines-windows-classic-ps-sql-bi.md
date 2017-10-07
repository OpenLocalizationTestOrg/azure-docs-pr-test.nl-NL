---
title: aaaSQL Server Business Intelligence | Microsoft Docs
description: Dit onderwerp maakt gebruik van resources die zijn gemaakt met het klassieke implementatiemodel Hallo en beschrijft Hallo Business Intelligence (BI)-functies die beschikbaar zijn voor SQL Server op Azure Virtual Machines (VM's) wordt uitgevoerd.
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: c681e7a7-eeda-48aa-bc35-6277f4828244
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/30/2017
ms.author: asaxton
ms.openlocfilehash: e3288f0835d6c4a19baeeea5f6b65fec16cd751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-business-intelligence-in-azure-virtual-machines"></a>SQL Server Business Intelligence in Virtual Machines van Azure
> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

Hallo virtuele Machine in Microsoft Azure-galerie bevat afbeeldingen met SQL Server-installaties. Hallo SQL Server-edities worden ondersteund in Hallo-afbeeldingen zijn Hallo dezelfde bestanden voor installatie, kunt u virtuele machines en tooon lokale computers installeren. In dit onderwerp bevat een overzicht van SQL Server Business Intelligence (BI) Hallo functies die zijn geïnstalleerd op het Hallo-installatiekopieën en configuratiestappen vereist nadat een virtuele machine is ingericht. Dit onderwerp beschrijft ook ondersteunde implementatietopologieën voor BI-functies en best practices.

## <a name="license-considerations"></a>Licentie-overwegingen
Er zijn twee manieren toolicense SQL Server in Microsoft Azure Virtual Machines:

1. License mobility voordelen die deel van de Software Assurance uitmaken. Zie voor meer informatie [License Mobility through Software Assurance in Azure](https://azure.microsoft.com/pricing/license-mobility/).
2. Betalen verwerkingssnelheid per uur van Azure Virtual Machines waarop SQL Server is geïnstalleerd. Zie de sectie 'SQL Server' in Hallo [prijzen van virtuele Machines](https://azure.microsoft.com/pricing/details/virtual-machines/#Sql).

Zie voor meer informatie over licentieverlening en huidige tarieven [virtuele Machines Veelgestelde vragen over licenties](https://azure.microsoft.com/pricing/licensing-faq/%20/).

## <a name="sql-server-images-available-in-azure-virtual-machine-gallery"></a>SQL Server-installatiekopieën beschikbaar in Azure virtuele Machine-galerie
Hallo virtuele Machine in Microsoft Azure-galerie bevat diverse installatiekopieën met Microsoft SQL Server. Hallo-software geïnstalleerd op de installatiekopieën van virtuele machines Hallo varieert op basis van het Hallo-versie van besturingssysteem Hallo en Hallo versie van SQL Server. Hallo-lijst met afbeeldingen die beschikbaar zijn in de virtuele machine van Azure-galerie Hallo vaak wordt gewijzigd.

<!--![SQL image in azure VM gallery](./media/virtual-machines-windows-classic-ps-sql-bi/IC741367.png)-->
![SQL-installatiekopie in de galerie van Azure VM](./media/virtual-machines-windows-classic-ps-sql-bi/vm-sql-images.png)

![PowerShell](./media/virtual-machines-windows-classic-ps-sql-bi/IC660119.gif) Hallo retourneert volgende PowerShell-script Hallo-lijst van installatiekopieën van Azure die 'SQL-Server' in hello ImageName bevatten:

    # assumes you have already uploaded a management certificate tooyour Microsoft Azure Subscription. View hello thumbprint value from hello "Subscriptions" menu in Azure portal.

    $subscriptionID = ""    # REQUIRED: Provide your subscription ID.
    $subscriptionName = "" # REQUIRED: Provide your subscription name.
    $thumbPrint = "" # REQUIRED: Provide your certificate thumbprint.
    $certificate = Get-Item cert:\currentuser\my\$thumbPrint # REQUIRED: If your certificate is in a different store, provide it here.-Ser  store is hello one specified with hello -ss parameter on MakeCert

    Set-AzureSubscription -SubscriptionName $subscriptionName -Certificate $certificate -SubscriptionID $subscriptionID

    Write-Host -foregroundcolor green "List of available gallery images where imagename contains 2016"
    Write-Host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
    get-azurevmimage | where {$_.ImageName -Like "*SQL-Server-2016*"} | select imagename,category, location, label, description

    Write-Host -foregroundcolor green "List of available gallery images where imagename contains 2014"
    Write-Host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
    get-azurevmimage | where {$_.ImageName -Like "*SQL-Server-2014*"} | select imagename,category, location, label, description

Zie voor meer informatie over edities en functies die worden ondersteund door SQL Server Hallo volgende:

* [SQL Server-edities](https://www.microsoft.com/server-cloud/products/sql-server-editions/#fbid=Zae0-E6r5oh)
* [Ondersteunde functies door Hallo-edities van SQL Server 2016](https://msdn.microsoft.com/library/cc645993.aspx)

### <a name="bi-features-installed-on-hello-sql-server-virtual-machine-gallery-images"></a>BI-onderdelen op Hallo installatiekopieën voor virtuele Machine galerie van SQL Server geïnstalleerd
Hallo volgende tabel ziet u Hallo geïnstalleerd op Hallo algemene Microsoft Azure Virtual Machine-afbeeldingen voor SQL Server Business Intelligence-functies:

* SQL Server 2016 SP1 Enterprise
* SQL Server 2016 SP1 Standard
* SQL Server 2014 SP2 Enterprise
* SQL Server 2014 SP2 Standard
* SQL Server 2012 SP3 Enterprise
* SQL Server 2012 SP3 Standard

| SQL Server BI functie | Geïnstalleerd op Hallo afbeelding | Opmerkingen |
| --- | --- | --- |
| **Native modus van Reporting Services** |Ja |Geïnstalleerd, maar moet worden geconfigureerd, inclusief Hallo report manager-URL. Zie de sectie Hallo [Reporting Services configureren](#configure-reporting-services). |
| **Reporting Services-modus SharePoint wordt uitgevoerd** |Nee |Hallo Microsoft Azure Virtual Machine galerie installatiekopie bevat geen SharePoint- of SharePoint bestanden voor installatie. <sup>1</sup> |
| **Analysis Services multidimensionale en Data mining (OLAP)** |Ja |Hallo geïnstalleerd en geconfigureerd als standaard Analysis Services-exemplaar |
| **Analyseservices in tabelvorm** |Nee |Ondersteund in SQL Server 2012, is 2014 en 2016 afbeeldingen, maar het niet standaard geïnstalleerd. Een ander exemplaar van Analysis Services installeren. Zie de sectie Hallo andere SQL Server-Services en functies in dit onderwerp installeren. |
| **Analysis Services Power Pivot voor SharePoint** |Nee |Hallo Microsoft Azure Virtual Machine galerie installatiekopie bevat geen SharePoint- of SharePoint bestanden voor installatie. <sup>1</sup> |

<sup>1</sup> Zie voor meer informatie over SharePoint en virtuele machines in Azure [Microsoft Azure architecturen voor SharePoint 2013](https://technet.microsoft.com/library/dn635309.aspx) en [SharePoint-implementatie in Microsoft Azure Virtual Machines](https://www.microsoft.com/download/details.aspx?id=34598).

![PowerShell](./media/virtual-machines-windows-classic-ps-sql-bi/IC660119.gif) Hallo PowerShell-opdracht tooget na een lijst met geïnstalleerde services die 'SQL' bevatten in Hallo servicenaam uitgevoerd.

    get-service | Where-Object{ $_.DisplayName -like '*SQL*' } | Select DisplayName, status, servicetype, dependentservices | format-Table -AutoSize

## <a name="general-recommendations-and-best-practices"></a>Algemene aanbevelingen en Best Practices
* Hallo minimale aanbevolen grootte voor een virtuele machine is **A3** bij gebruik van SQL Server Enterprise Edition. Hallo **A4** grootte van virtuele machine wordt aanbevolen voor implementaties van SQL Server BI van Analysis Services en Reporting Services.
  
    Zie voor informatie over de huidige VM-grootten hello, [grootten van virtuele machines voor Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Is een best practice voor Schijfbeheer toostore gegevens, het logboek en back-upbestanden op stations dan **C**: en **D**:. Maak bijvoorbeeld gegevensschijven **E**: en **F**:.
  
  * Hallo station cachebeleid voor Hallo standaardstation **C**: is niet optimaal voor het werken met gegevens.
  * Hallo **D**: station is een tijdelijke station dat hoofdzakelijk voor het wisselbestand Hallo gebruikt wordt. Hallo **D**: station is niet persistent en wordt niet opgeslagen in blob-opslag. Beheertaken, zoals een wijziging van grootte door toohello virtuele machine opnieuw Hallo **D**: station. Het is raadzaam te**niet** hello gebruiken **D**: station voor databasebestanden, met inbegrip van tempdb.
    
    Zie voor meer informatie over het maken en koppelen van schijven [hoe tooAttach een gegevensschijf tooa virtuele Machine](../classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* Stop of services die u niet van plan bent toouse verwijderen. Voor bijvoorbeeld als Hallo virtuele machine alleen wordt gebruikt voor Reporting Services stoppen of verwijderen van Analysis Services en SQL Server Integration Services. Hallo is volgende afbeelding een voorbeeld van Hallo-services die standaard worden gestart.
  
    ![SQL Server-services](./media/virtual-machines-windows-classic-ps-sql-bi/IC650107.gif)
  
  > [!NOTE]
  > Hallo SQL Server database-engine is vereist in Hallo ondersteund BI-scenario's. Hallo database-engine is in een VM-topologie van één server vereist waarop toobe Hallo dezelfde virtuele machine.
  
    Zie voor meer informatie de volgende Hallo: [Reporting Services verwijderen](https://msdn.microsoft.com/library/hh479745.aspx) en [verwijderen van een exemplaar van Analysis Services](https://msdn.microsoft.com/library/ms143687.aspx).
* Controleer **Windows Update** voor nieuwe 'belangrijke updates'. Hallo Microsoft Azure Virtual Machine-installatiekopieën worden regelmatig vernieuwd; echter belangrijke updates, worden mogelijk beschikbaar is via **Windows Update** nadat Hallo VM-installatiekopie voor het laatst is vernieuwd.

## <a name="example-deployment-topologies"></a>Voorbeeld van de implementatietopologieën
Hallo hieronder vindt u Voorbeeldimplementaties die gebruikmaken van Microsoft Azure Virtual Machines. Hallo-topologieën in deze diagrammen zijn slechts enkele mogelijke Hallo-topologieën die kunt u met SQL Server BI functies en Microsoft Azure Virtual Machines.

### <a name="single-virtual-machine"></a>Eén virtuele Machine
Analysis Services, Reporting Services, SQL Server Database Engine en gegevensbronnen op een enkele virtuele machine.

![BI Standards-scenario met 1 virtuele machine](./media/virtual-machines-windows-classic-ps-sql-bi/IC650108.gif)

### <a name="two-virtual-machines"></a>Twee virtuele Machines
* Analyseservices, Reporting Services en SQL Server Database Engine Hallo op een enkele virtuele machine. Deze implementatie omvat het Hallo report server-databases.
* Gegevensbronnen op een tweede virtuele machine. Hallo bevat tweede VM Database-Engine van SQL Server als een gegevensbron.

![BI iaas-scenario met 2 virtuele machines](./media/virtual-machines-windows-classic-ps-sql-bi/IC650109.gif)

### <a name="mixed-azure--data-on-azure-sql-database"></a>Gemengde Azure-gegevens op Azure SQL-database
* Analyseservices, Reporting Services en SQL Server Database Engine Hallo op een enkele virtuele machine. Deze implementatie omvat het Hallo report server-databases.
* Gegevensbron is Azure SQL-database.

![virtuele machine BI iaas-scenario's en AzureSQL als gegevensbron](./media/virtual-machines-windows-classic-ps-sql-bi/IC650110.gif)

### <a name="hybrid-data-on-premises"></a>Hybride: gegevens die lokaal
* In deze voorbeeldimplementatie Analysis Services, Reporting Services en SQL Server Database Engine Hallo uitgevoerd op een enkele virtuele machine. hosts voor virtuele machines Hallo Hallo report server-databases. Hallo virtuele machine is gekoppeld tooan lokaal domein via Azure virtuele netwerken of enige andere VPN-tunneling oplossing.
* Gegevensbron is lokaal.

![BI iaas-scenario's voor vm- en on-premises gegevensbronnen](./media/virtual-machines-windows-classic-ps-sql-bi/IC654384.gif)

## <a name="reporting-services-native-mode-configuration"></a>Configuratie van de Native modus Reporting Services
Hallo virtuele machine afbeelding voor SQL Server bevat Reporting Services Native modus geïnstalleerd, maar Hallo rapportserver is niet geconfigureerd. Hallo stappen in deze sectie configureren Hallo Reporting Services report server. Zie voor meer informatie over het configureren van Reporting Services Native modus, [installeren Reporting Services Native modus Report Server (SSRS)](https://msdn.microsoft.com/library/ms143711.aspx).

> [!NOTE]
> Zie voor vergelijkbare inhoud die gebruikmaakt van Windows PowerShell-scripts tooconfigure Hallo-rapportserver [tooCreate Gebruik PowerShell een Azure VM met een Native modus Report Server](../classic/ps-sql-report.md).

### <a name="connect-toohello-virtual-machine-and-start-hello-reporting-services-configuration-manager"></a>Verbinding maken met virtuele Machine toohello en Hallo Reporting Services Configuration Manager te starten
Er zijn twee algemene werkstromen voor het verbinden van tooan Azure virtuele Machine:

* tooconnect in hello, Hallo-naam van Hallo virtuele machine op en klik op **Connect**. Een verbinding met extern bureaublad wordt geopend en Hallo computernaam wordt automatisch ingevuld.
  
    ![verbinding maken met tooazure virtuele machine](./media/virtual-machines-windows-classic-ps-sql-bi/IC650112.gif)
* Verbinding maken met toohello virtuele machine Windows verbinding met extern bureaublad. In de gebruikersinterface van de extern bureaublad Hallo Hallo:
  
  1. Type Hallo **cloudservicenaam** als Hallo-computernaam.
  2. Typ dubbele punt (:) en Hallo openbare-poortnummer dat is geconfigureerd voor Hallo TCP extern bureaublad-eindpunt.
     
      Myservice.cloudapp.NET:63133
     
      Zie voor meer informatie [wat is een cloudservice?](https://azure.microsoft.com/manage/services/cloud-services/what-is-a-cloud-service/).


**Start u Reporting Services Configuration Manager**

In **Windows Server 2012-2016**:

1. Van Hallo **Start** Typ **Reporting Services** toosee een lijst met Apps.
2. Met de rechtermuisknop op **Reporting Services Configuration Manager** en klik op **als Administrator uitvoeren**.

In **Windows Server 2008 R2**:

1. Klik op **Start**, en klik vervolgens op **alle programma's**.
2. Klik op **Microsoft SQL Server 2016**.
3. Klik op **configuratiehulpprogramma's**.
4. Met de rechtermuisknop op **Reporting Services Configuration Manager** en klik op **als Administrator uitvoeren**.

Of:

1. Klik op **Start**.
2. In Hallo **programma's en bestanden zoeken** type dialoogvenster **reporting services**. Als Hallo VM wordt uitgevoerd op Windows Server 2012, typt u **reporting services** op Windows Server 2012 Start welkomstscherm.
3. Met de rechtermuisknop op **Reporting Services Configuration Manager** en klik op **als Administrator uitvoeren**.
   
    ![zoeken naar ssrs configuration manager](./media/virtual-machines-windows-classic-ps-sql-bi/IC650113.gif)

### <a name="configure-reporting-services"></a>Reporting Services configureren
**Service-account en webservice-URL:**

1. Controleer of Hallo **servernaam** is de naam van de lokale server Hallo en klikt u op **Connect**.
2. Opmerking Hallo leeg **Report Server-databasenaam**. Hallo-database wordt gemaakt wanneer het Hallo-configuratie is voltooid.
3. Controleer of Hallo **Rapportserverstatus** is **gestart**. Als u tooverify Hallo service in Windows Server Manager wilt, Hallo-service is Hallo **SQL Server Reporting Services** Windows-Service.
4. Klik op **serviceaccount** en Hallo account indien nodig wijzigen. Als Hallo virtuele machine wordt gebruikt in een niet-gekoppelde domeinomgeving, Hallo ingebouwde **ReportServer** account voldoende is. Zie voor meer informatie over Hallo-serviceaccount [serviceaccount](https://msdn.microsoft.com/library/ms189964.aspx).
5. Klik op **URL van webservice** in het linkerdeelvenster Hallo.
6. Klik op **toepassen** tooconfigure Hallo standaardwaarden.
7. Opmerking Hallo **Report Server webservice-URL's**. Houd er rekening mee Hallo standaard TCP-poort 80 en maakt deel uit van Hallo-URL. In een latere stap maakt u een Microsoft Azure Virtual Machine-eindpunt voor Hallo-poort.
8. In Hallo **resultaten** deelvenster controleren Hallo acties met succes is voltooid.

**Database:**

1. Klik op **Database** in het linkerdeelvenster Hallo.
2. Klik op **Database wijzigen**.
3. Controleer of **maken van een nieuw report server-database** is geselecteerd en klik op volgende.
4. Controleer of **servernaam** en klik op **testverbinding**.
5. Als resultaat Hallo **verbinding testen is voltooid**, klikt u op **OK** en klik vervolgens op **volgende**.
6. Opmerking Hallo databasenaam is **ReportServer** en Hallo **Report Server-modus** is **systeemeigen** klikt u vervolgens op **volgende**.
7. Klik op **volgende** op Hallo **referenties** pagina.
8. Klik op **volgende** op Hallo **samenvatting** pagina.
9. Klik op **volgende** op Hallo **navigatie- en eindtijd** pagina.

**Web-Portal-URL of URL van Report Manager voor 2012 en 2014:**

1. Klik op **Portal-URL voor webinhoud**, of **URL van Report Manager** voor 2014 en 2012 in het linkerdeelvenster Hallo.
2. Klik op **Toepassen**.
3. In Hallo **resultaten** deelvenster controleren Hallo acties met succes is voltooid.
4. Klik op **afsluiten**.

Zie voor informatie over report servermachtigingen [machtigingen verlenen voor een Native modus rapportserver](https://msdn.microsoft.com/library/ms156014.aspx).

### <a name="browse-toohello-local-report-manager"></a>Blader toohello lokale Report Manager
tooverify hello configuratie bladeren tooreport manager op Hallo VM.

1. Start Internet Explorer op Hallo VM, met administrator-bevoegdheden.
2. Blader toohttp://localhost/reports op Hallo VM.

### <a name="tooconnect-tooremote-web-portal-or-report-manager-for-2014-and-2012"></a>tooConnect tooRemote-webportal of van Report Manager for 2014 en 2012
Als u tooconnect toohello-webportal of Rapportbeheer voor 2014 en 2012 op Hallo virtuele machine vanaf een externe computer wilt maken van een nieuwe virtuele machine TCP-eindpunt. Standaard Hallo rapportserver luistert naar HTTP-aanvragen op **poort 80**. Als u Hallo report server-URL's toouse een andere poort configureren, moet u dat poortnummer opgeven in Hallo instructies te volgen.

1. Een eindpunt voor de virtuele Machine van de TCP-poort 80 Hallo maken. Zie voor meer informatie, Hallo [eindpunten van de virtuele Machine en Firewall-poorten](#virtual-machine-endpoints-and-firewall-ports) sectie in dit document.
2. Open poort 80 in de firewall Hallo virtuele machine.
3. Blader toohello-webportal of Rapportbeheer, met behulp van de virtuele Machine van Azure **DNS-naam** als Hallo-servernaam in Hallo-URL. Bijvoorbeeld:
   
    **Rapportserver**: http://uebi.cloudapp.net/reportserver **webportal**: http://uebi.cloudapp.net/reports
   
    [Een Firewall configureren voor toegang tot de Server van rapporten](https://msdn.microsoft.com/library/bb934283.aspx)

### <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a>tooCreate en rapporten publiceren toohello Azure virtuele Machine
Hallo volgende tabel ziet u enkele Hallo opties beschikbaar toopublish bestaande rapporten uit een on-premises computer toohello rapportserver gehost op Hallo van Microsoft Azure Virtual Machine:

* **Report Builder**: Hallo virtuele machine bevat Hallo Klik-eenmaal versie van Microsoft SQL Server Report Builder voor SQL 2014 en 2012. toostart Report builder Hallo eerst op Hallo virtuele machine met SQL 2016:
  
  1. Start uw browser met beheerdersbevoegdheden.
  2. Toohello-webportal op Hallo virtuele machine bladeren en selecteer Hallo **downloaden** pictogram in de rechterbovenhoek Hallo.
  3. Selecteer **Report Builder**.
     
     Zie voor meer informatie [Start Report Builder](https://msdn.microsoft.com/library/ms159221.aspx).
* **SQL Server Data Tools**: VM: SQL Server Data Tools op Hallo virtuele machine is geïnstalleerd en kan worden gebruikt toocreate **Report Server-projecten** en rapporten op Hallo virtuele machine. SQL Server Data Tools kunt publiceren Hallo rapporten toohello-rapportserver op Hallo virtuele machine.
* **SQL Server Data Tools: Extern**: op uw lokale computer, kunt u een Reporting Services-project maken in SQL Server Data Tools met Reporting Services-rapporten. Hallo project tooconnect toohello URL van webservice configureren.
  
    ![de Projecteigenschappen SSDT voor SQL Server Reporting Services-project](./media/virtual-machines-windows-classic-ps-sql-bi/IC650114.gif)
* Maak een. Harde schijf VHD die rapporten bevat en vervolgens uploaden en het Hallo-station koppelen.
  
  1. Maak een. VHD harde schijf op de lokale computer die uw rapporten bevat.
  2. Maak en installeer een beheercertificaat.
  3. Hallo VHD-bestand tooAzure met de cmdlet Add-AzureVHD Hallo uploaden [maken en uploaden van een Windows Server-VHD tooAzure](../classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
  4. Koppel Hallo schijf toohello virtuele machine.

## <a name="install-other-sql-server-services-and-features"></a>Andere SQL Server-Services en onderdelen installeren
tooinstall aanvullende SQL Server-services, zoals Analysis Services in de modus tabellair uitvoeren Hallo SQL server setup wizard. Hallo setup-bestanden zijn op de lokale schijf Hallo virtuele machine.

1. Klik op **Start** en klik vervolgens op **alle programma's**.
2. Klik op **Microsoft SQL Server 2016**, **Microsoft SQL Server 2014** of **Microsoft SQL Server 2012** en klik vervolgens op **configuratiehulpprogramma's**.
3. Klik op **Installatiecentrum van SQL Server**.

C:\SQLServer_13.0_full\setup.exe, C:\SQLServer_12.0_full\setup.exe of C:\SQLServer_11.0_full\setup.exe of starten

> [!NOTE]
> Hallo eerste keer dat u de installatie van SQL Server meer setup-bestanden kunnen worden gedownload en vereisen Hallo virtuele machine opnieuw worden opgestart en het opnieuw opstarten van SQL Server setup uitvoert.
> 
> Als u toorepeatedly moet aanpassen Hallo-installatiekopie in Hallo Microsoft Azure virtuele Machine hebt geselecteerd, kunt u uw eigen SQL Server-installatiekopie. Analysis Services SysPrep-functionaliteit is ingeschakeld met SQL Server 2012 SP1 CU2. Zie voor meer informatie [overwegingen voor het installeren van SQL Server met behulp van SysPrep](https://msdn.microsoft.com/library/ee210754.aspx) en [Sysprep-ondersteuning voor serverrollen](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).
> 
> 

### <a name="tooinstall-analysis-services-tabular-mode"></a>tooInstall Tabellaire modus van Analysis Services
Hallo stappen in deze sectie **samenvatten** Hallo installatie van de modus tabellair Analysis Services. Zie voor meer informatie de volgende Hallo:

* [Analyseservices in de modus Tabellair installeren](https://msdn.microsoft.com/library/hh231722.aspx)
* [Tabellaire model (Adventure Works zelfstudie)](https://msdn.microsoft.com/library/140d0b43-9455-4907-9827-16564a904268)

**tooInstall Tabellaire modus van Analysis Services:**

1. Klik in de installatiewizard voor Hallo SQL Server op **installatie** in Hallo linker deelvenster en klik vervolgens op **zelfstandige installatie van nieuwe SQL server of bestaande installatie van functies tooan toevoegen**.
   
   * Als u Hallo ziet **map**, tooc:\SQLServer_13.0_full, c:\SQLServer_12.0_full of c:\SQLServer_11.0_full bladeren en klik vervolgens op **Ok**.
2. Klik op **volgende** op Hallo updates productpagina.
3. Op Hallo **installatietype** pagina **voert u een nieuwe installatie van SQL Server** en klik op **volgende**.
4. Op Hallo **Setup-rol** pagina, klikt u op **installatie van SQL Server-functies**.
5. Op Hallo **Functieselectie** pagina, klikt u op **Analysis Services**.
6. Op Hallo **Exemplaarconfiguratie** pagina, typ een beschrijvende naam, zoals **tabelvorm** in **exemplaar met de naam** en **exemplaar-Id** tekst vakken.
7. Op Hallo **configuratie van Analysis Services** pagina **Tabellair**. Hallo huidige gebruiker toohello beheerdersmachtigingen lijst toevoegen.
8. Voltooien en Hallo SQL Server-installatiewizard te sluiten.

## <a name="analysis-services-configuration"></a>Configuratie van Analysis Services
### <a name="remote-access-tooanalysis-services-server"></a>Externe toegang tooAnalysis Services-Server
Analysis Services-server ondersteunt alleen windows-verificatie. tooaccess Analysis Services op afstand van clienttoepassingen, zoals SQL Server Management Studio of SQL Server Data Tools Hallo virtuele machine moet toobe gekoppelde tooyour lokale domein, met behulp van virtuele netwerken van Azure. Zie voor meer informatie, [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md).

Een **standaardexemplaar** luistert op TCP-poort van Analysis Services **2383**. Hallo-poort in Hallo virtuele machines firewall openen. Een geclusterde benoemd exemplaar van Analysis Services ook luistert op poort **2383**.

Voor een **benoemd exemplaar** van Analysis Services Hallo SQL Server Browser-service is vereist toomanage poort toegang. standaardconfiguratie voor SQL Server Browser Hallo is poort **2382**.

In de firewall van de virtuele machines hello, open poort **2382** en maak een statische Analysis Services met de naam exemplaar poort.

1. tooverify-poorten die al in gebruik op Hallo VM en welke proces Hallo poorten gebruikt, voert u Hallo opdracht met beheerdersbevoegdheden te volgen:
   
        netstat /ao
2. Gebruik SQL Server Management Studio toocreate een statische Analysis Services met de naam exemplaar poort door bij te werken, 'Poort' waarde in tabelvorm AS algemene eigenschappen-instantie. Zie voor meer informatie 'Een vaste poort gebruiken voor een standaard of benoemd exemplaar' Hallo [Hallo Windows Firewall tooAllow Analysis Services Access configureren](https://msdn.microsoft.com/library/ms174937.aspx#bkmk_fixed).
3. Hallo in tabelvorm exemplaar Hallo Analysis Services-service opnieuw starten.

Zie voor meer informatie, Hallo **eindpunten van de virtuele Machine en Firewall-poorten** sectie in dit document.

## <a name="virtual-machine-endpoints-and-firewall-ports"></a>Eindpunten van de virtuele Machine en Firewall-poorten
Deze sectie bevat een overzicht van Microsoft Azure virtuele Machine eindpunten toocreate en poorten tooopen in Hallo virtuele machine firewalls. Hallo volgende tabel ziet u Hallo **TCP** toocreate eindpunten voor en Hallo poorten tooopen in Hallo virtuele machines firewall-poorten.

* Als u van één VM gebruikmaakt en hello volgende twee vereisten voldaan is, hoeft u geen toocreate VM eindpunten en hoeft u geen tooopen Hallo poorten in de firewall Hallo op Hallo VM.
  
  * U bent niet extern verbinding maken toohello SQL Server-functies op Hallo VM. Tot stand brengen van een verbinding met extern bureaublad-toohello VM en toegang tot de SQL Server-functies Hallo lokaal op Hallo VM wordt niet beschouwd als een externe verbinding toohello SQL Server-onderdelen.
  * U bent geen lid worden Hallo VM tooan lokaal domein via Azure virtuele netwerken of een andere VPN-tunneling oplossing.
* Als Hallo virtuele machine is geen gekoppelde tooa domein, maar u wilt verbinden tooremotely toohello SQL Server-functies op virtuele machine:
  
  * Hallo poorten openen in Hallo-firewall op Hallo VM.
  * Maken van virtuele machine eindpunten voor Hallo poorten (*) hebt genoteerd.
* Hallo-eindpunten zijn niet vereist als Hallo virtuele machine gekoppelde tooa domein met een VPN-tunnel zoals Azure virtuele netwerken. Echter Hallo poorten openen in de firewall Hallo op Hallo VM.
  
  | Poort | Type | Beschrijving |
  | --- | --- | --- |
  | **80** |TCP |Rapportserver externe toegang (*). |
  | **1433** |TCP |SQL Server Management Studio (*). |
  | **1434** |UDP |SQL Serverbrowser. Dit is nodig wanneer Hallo VM in het domein gekoppelde tooa. |
  | **2382** |TCP |SQL Serverbrowser. |
  | **2383** |TCP |Standaardexemplaar van SQL Server Analysis Services en geclusterde benoemde exemplaren. |
  | **De gebruiker gedefinieerde** |TCP |Maak een statische Analysis Services met de naam exemplaar poort van een poortnummer dat die u kiest en vervolgens deblokkeren Hallo poortnummer in Hallo firewall. |

Zie voor meer informatie over het maken van eindpunten Hallo volgende:

* Eindpunten maken:[hoe tooSet Up eindpunten tooa virtuele Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* SQL Server: Zie Hallo 'Volledige configuratie stappen tooconnect toohello virtuele machine met SQL Server Management Studio' sectie [inrichten van een virtuele Machine van SQL Server op Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).

Hallo volgende diagram illustreert Hallo poorten tooopen in Hallo VM firewall tooallow RAS toofeatures en -onderdelen op Hallo VM.

![poorten tooopen voor bi toepassingen in Azure Virtual machines](./media/virtual-machines-windows-classic-ps-sql-bi/IC654385.gif)

## <a name="resources"></a>Resources
* Bekijk Hallo ondersteuningsbeleid voor Microsoft-serversoftware gebruikt in een omgeving met hello Azure virtuele machines. Hallo Volgend onderwerp bevat een overzicht van ondersteuning voor functies zoals BitLocker Failover Clustering en netwerktaakverdeling. [Microsoft server softwareondersteuning voor Azure Virtual Machines](http://support.microsoft.com/kb/2721672).
* [SQL Server op Azure Virtual Machines-overzicht](../sql/virtual-machines-windows-sql-server-iaas-overview.md)
* [Virtuele machines](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Inrichting van een virtuele Machine van SQL Server op Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md)
* [Hoe tooAttach een gegevensschijf tooa virtuele Machine](../classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Migreren van een Database tooSQL Server op een Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)
* [Hallo modus van een exemplaar van Analysis Services Server bepalen](https://msdn.microsoft.com/library/gg471594.aspx)
* [Multidimensionale model (Adventure Works zelfstudie)](https://technet.microsoft.com/library/ms170208.aspx)
* [Documentatiecentrum van Azure](https://azure.microsoft.com/documentation/)
* [Gebruik van Power BI in een hybride omgeving](https://msdn.microsoft.com/library/dn798994.aspx)

> [!NOTE]
> [Feedback en contactgegevens via het Microsoft SQL Server-verbinding verzenden](https://connect.microsoft.com/SQLServer/Feedback)

### <a name="community-content"></a>Inhoud van de community
* [Azure SQL Database-beheer met PowerShell](http://blogs.msdn.com/b/windowsazure/archive/2013/02/07/windows-azure-sql-database-management-with-powershell.aspx)

