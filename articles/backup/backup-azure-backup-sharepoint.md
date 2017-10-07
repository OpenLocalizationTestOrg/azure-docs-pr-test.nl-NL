---
title: beveiliging voor de server van aaaDPM/Azure back-up van een SharePoint-farm tooAzure | Microsoft Docs
description: In dit artikel biedt een overzicht van de beveiliging van DPM/Azure Backup-server van een SharePoint-farm tooAzure
services: backup
documentationcenter: 
author: adigan
manager: Nkolli1
editor: 
ms.assetid: e0c0c252-dc1d-4072-b777-7222c13950b0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: adigan;giridham;jimpark;trinadhk;markgal
ms.openlocfilehash: 726d59320b8d9f14b38e0f041308019eebcfb77b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-sharepoint-farm-tooazure"></a>Back-up van een SharePoint-farm tooAzure
U back-up van een SharePoint-farm tooMicrosoft Azure met behulp van System Center Data Protection Manager (DPM) in veel Hallo dezelfde manier als u back-up van andere gegevensbronnen. Azure Backup biedt flexibiliteit in Hallo back-upschema toocreate dagelijkse, wekelijkse, maandelijkse of jaarlijkse back-uppunten en geeft u de bewaarperiode beleidsopties voor verschillende back-uppunten. DPM biedt Hallo mogelijkheid toostore lokale schijf kopieën voor snelle doelstellingen voor hersteltijd (RTO) en toostore kopieert tooAzure voor het bewaren van voordelige, op lange termijn.

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a>SharePoint ondersteunde versies en gerelateerde beveiligingsscenario 's
Azure Backup voor DPM ondersteunt Hallo volgen scenario's:

| Workload | Versie | SharePoint-implementatie | Type DPM-implementatie | DPM - System Center 2012 R2 | Beveiliging en herstel |
| --- | --- | --- | --- | --- | --- |
| SharePoint |SharePoint 2013, SharePoint 2010, SharePoint 2007 SharePoint 3.0 |SharePoint geïmplementeerd als een fysieke server of Hyper-V/VMware virtuele machine <br> -------------- <br> De Sqlalwayson |Fysieke server of on-premises Hyper-V virtuele machine |Ondersteunt back-tooAzure vanaf updatepakket 5 |Opties voor herstel van SharePoint-Farm beveiligen: herstelfarm, database en bestand of lijstitem vanaf schijfherstelpunten.  Herstel van Azure herstelpunten farm en de database. |

## <a name="before-you-start"></a>Voordat u begint
Er zijn een aantal dingen die u moet tooconfirm voordat u back-up van een tooAzure van SharePoint-farm.

### <a name="prerequisites"></a>Vereisten
Voordat u verdergaat, controleert u of u alle Hallo hebt voldaan [vereisten voor het gebruik van Microsoft Azure Backup](backup-azure-dpm-introduction.md#prerequisites) tooprotect werkbelastingen. Sommige taken voor vereiste onderdelen bevatten: een back-upkluis maken, kluisreferenties downloaden, Azure Backup Agent installeren en DPM/Azure Backup-Server op Hallo kluis registreren.

### <a name="dpm-agent"></a>DPM-agent
Hallo DPM-agent moet worden geïnstalleerd op het Hallo-server waarop SharePoint wordt uitgevoerd, Hallo-servers waarop SQL Server en alle andere servers die deel van de SharePoint-farm Hallo uitmaken. Voor meer informatie over het tooset up Hallo beveiligingsagent, Zie [Setup beveiligingsagent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).  Hallo een uitzondering is dat u Hallo-agent op een enkel web-front-end (WFE)-server installeren. DPM moet Hallo-agent op één WFE-server alleen tooserve als toegangspunt Hallo voor beveiliging.

### <a name="sharepoint-farm"></a>SharePoint-farm
Voor elke 10 miljoen items in Hallo-farm, moet er ten minste 2 GB ruimte op volume Hallo waar Hallo DPM map zich bevindt. Deze ruimte is vereist voor het genereren van de catalogus. Genereren van de catalogus gemaakt voor DPM toorecover specifieke items (siteverzamelingen, sites, lijsten, documentbibliotheken, mappen, individuele documenten en lijstitems), een lijst met Hallo-URL's die zijn opgenomen in elke inhoudsdatabase. U kunt Hallo lijst met URL's weergeven in Hallo herstelbaar item deelvenster in Hallo **herstel** taakgebied van de DPM Administrator-Console.

### <a name="sql-server"></a>SQL Server
DPM wordt uitgevoerd als lokale systeemaccount. tooback van SQL Server-databases DPM moet een sysadmin-machtigingen op dat account voor Hallo-server die SQL Server wordt uitgevoerd. NT AUTHORITY\SYSTEM te ingesteld*sysadmin* op Hallo-server die SQL Server wordt uitgevoerd voordat u een back-up.

Als de SharePoint-farm Hallo SQL Server-databases die zijn geconfigureerd met SQL Server-aliassen, installeert u Hallo SQL Server-clientonderdelen op Hallo front-endwebserver die DPM wilt beveiligen.

### <a name="sharepoint-server"></a>SharePoint Server
Terwijl de prestaties zijn afhankelijk van veel factoren zoals de grootte van de SharePoint-farm, algemene richtlijnen kunt één DPM-server beveiligen een SharePoint-farm 25 TB.

### <a name="dpm-update-rollup-5"></a>DPM-updatepakket 5
toobegin beveiliging van een tooAzure van SharePoint-farm, moet u tooinstall DPM Update Rollup 5 of hoger. Updatepakket 5 biedt Hallo mogelijkheid tooprotect een tooAzure van SharePoint-farm als Hallo-farm met behulp van SQL AlwaysOn is geconfigureerd.
Zie voor meer informatie Hallo blogbericht die introduceert [DPM Update Rollup 5](http://blogs.technet.com/b/dpm/archive/2015/02/11/update-rollup-5-for-system-center-2012-r2-data-protection-manager-is-now-available.aspx)

### <a name="whats-not-supported"></a>Wat wordt er niet ondersteund
* DPM die een SharePoint-farm beveiligt biedt geen bescherming zoekindexen of toepassing-servicedatabases. U moet tooconfigure Hallo beveiliging van deze databases afzonderlijk.
* DPM biedt geen back-up van de SharePoint SQL Server-databases die worden gehost op Servershares van scale-out bestandsserver (SOFS).

## <a name="configure-sharepoint-protection"></a>SharePoint-beveiliging configureren
Voordat u DPM tooprotect SharePoint gebruiken kunt, moet u Hallo SharePoint VSS Writer-service (WSS Writer-service) configureren met behulp van **ConfigureSharePoint.exe**.

U vindt **ConfigureSharePoint.exe** in Hallo [DPM-installatiepad] \bin map op de front-endwebserver Hallo. Dit hulpprogramma biedt Hallo beveiligingsagent met Hallo referenties voor Hallo SharePoint-farm. U uitvoeren deze op één WFE-server. Als u meerdere WFE-servers hebt, selecteert u slechts één wanneer u een beveiligingsgroep configureert.

### <a name="tooconfigure-hello-sharepoint-vss-writer-service"></a>tooconfigure hello SharePoint VSS Writer-service
1. Ga te op Hallo WFE-server bij een opdrachtprompt \bin\ [DPM-installatielocatie]
2. Voer ConfigureSharePoint - EnableSharePointProtection.
3. Geef beheerdersreferenties Hallo-farm. Deze account moet lid zijn van Hallo lokale groep Administrators op Hallo WFE-server. Als de farmbeheerder Hallo niet een lokale beheerder grant Hallo volgende machtigingen op Hallo WFE-server:
   * Verleen Hallo WSS_Admin_WPG-groep volledige controle toohello DPM map (% Program Files%\Microsoft Data Protection Manager\DPM).
   * Verleen Hallo WSS_Admin_WPG-groep leestoegang toohello DPM registersleutel (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).

> [!NOTE]
> U moet toorerun ConfigureSharePoint.exe wanneer er een wijziging in de beheerdersreferenties van Hallo SharePoint-farm.
> 
> 

## <a name="back-up-a-sharepoint-farm-by-using-dpm"></a>Back-up van een SharePoint-farm met behulp van DPM
Nadat u hebt DPM en Hallo SharePoint-farm zoals hierboven is geconfigureerd, kunt u SharePoint beveiligd door DPM.

### <a name="tooprotect-a-sharepoint-farm"></a>tooprotect een SharePoint-farm
1. Van Hallo **beveiliging** tabblad Hallo DPM Administrator-Console klikt u op **nieuw**.
    ![Tabblad voor nieuwe beveiliging](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)
2. Op Hallo **Type beveiligingsgroep selecteren** pagina Hallo **nieuwe beveiligingsgroep maken** wizard, selecteer **Servers**, en klik vervolgens op **volgende** .
   
    ![Type beveiligingsgroep selecteren](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. Op Hallo **groepsleden selecteren** scherm, het selectievakje selecteert Hallo voor Hallo SharePoint server tooprotect en klik op **volgende**.
   
    ![Groepsleden selecteren](./media/backup-azure-backup-sharepoint/select-group-members2.png)
   
   > [!NOTE]
   > Met de Hallo DPM-agent is geïnstalleerd, kunt u Hallo-server in de wizard Hallo zien. DPM bevat ook de structuur. Omdat u ConfigureSharePoint.exe hebt uitgevoerd, DPM communiceert met Hallo SharePoint VSS Writer-service en de bijbehorende SQL Server-databases en herkent Hallo SharePoint-farmstructuur, Hallo inhoudsdatabases, en alle bijbehorende items die zijn gekoppeld.
   > 
   > 
4. Op Hallo **methode voor gegevensbeveiliging selecteren** pagina, voer de naam Hallo Hallo **beveiligingsgroep**, en selecteer de gewenste *beveiligingsmethode*. Klik op **Volgende**.
   
    ![Methode voor gegevensbeveiliging selecteren](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)
   
   > [!NOTE]
   > Hallo schijf beveiligingsmethode helpt toomeet korte hersteltijd doelstellingen. Azure is een voordelige, op lange termijn bescherming doel vergeleken tootapes. Zie voor meer informatie [gebruik Azure Backup tooreplace uw tape-infrastructuur](https://azure.microsoft.com/documentation/articles/backup-azure-backup-cloud-as-tape/)
   > 
   > 
5. Op Hallo **Kortetermijndoelen opgeven** pagina, selecteer de gewenste **bewaartermijn** en als u wilt dat back-ups toooccur te identificeren.
   
    ![Korte-termijndoelstellingen opgeven](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)
   
   > [!NOTE]
   > Omdat het herstel meestal nodig is voor gegevens die minder dan vijf dagen oud, we een bewaartermijn van vijf dagen op schijf geselecteerd en gewaarborgd dat Hallo back-up wordt uitgevoerd tijdens de niet-productieve uren, in dit voorbeeld.
   > 
   > 
6. Hallo opslaggroepschijfruimte die voor het Hallo-beveiligingsgroep is toegewezen bekijken en klik vervolgens op **volgende**.
7. Voor elke beveiligingsgroep DPM schijfruimte toostore toewijst en replica's te beheren. DPM moet op dit punt wordt een kopie van Hallo geselecteerd gegevens maken. Selecteer hoe en wanneer u wilt dat Hallo replica is gemaakt en klik op **volgende**.
   
    ![Methode voor het maken van replica selecteren](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)
   
   > [!NOTE]
   > toomake ervoor dat verkeer niet plaatsvindt, selecteer een tijdstip buiten productie-uren.
   > 
   > 
8. DPM wordt de gegevensintegriteit gewaarborgd door het uitvoeren van consistentiecontroles uit op Hallo replica. Er zijn twee opties beschikbaar. U kunt definiëren een planning toorun consistentie te controleren of DPM consistentiecontroles uit op Hallo replica automatisch kan worden uitgevoerd wanneer het inconsistent wordt. Selecteer de gewenste optie en klik vervolgens op **volgende**.
   
    ![Consistentiecontrole](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. Op Hallo **gegevens voor Online beveiliging opgeven** pagina, selecteert u Hallo SharePoint-farm wilt tooprotect en klik vervolgens op **volgende**.
   
    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. Op Hallo **Online back-upschema opgeven** pagina, selecteer uw voorkeursplanning en klik vervolgens op **volgende**.
    
    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)
    
    > [!NOTE]
    > DPM biedt een maximum van twee tooAzure voor dagelijkse back-ups op verschillende tijdstippen. Azure Backup kunt ook bepalen Hallo hoeveelheid WAN-bandbreedte die kan worden gebruikt voor back-ups in piek- en daluren met behulp van [Azure back-up netwerkbeperking](https://azure.microsoft.com/en-in/documentation/articles/backup-configure-vault/#enable-network-throttling).
    > 
    > 
11. Afhankelijk van de back-upschema Hallo die u hebt geselecteerd, op Hallo **Online bewaarbeleid opgeven** pagina, selecteer Hallo bewaarbeleid voor dagelijkse, wekelijkse, maandelijkse en jaarlijkse back-uppunten.
    
    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)
    
    > [!NOTE]
    > DPM maakt gebruik van een opa-vader-zoon bewaarschema waarin een andere bewaarbeleid kan worden gekozen voor verschillende back-uppunten.
    > 
    > 
12. Vergelijkbare toodisk een eerste verwijzing punt replica moet toobe gemaakt in Azure. Selecteer uw voorkeursoptie toocreate een tooAzure eerste back-up en klik vervolgens op **volgende**.
    
    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. Controleer de geselecteerde instellingen op Hallo **samenvatting** pagina en klik vervolgens op **groep maken**. U ziet een bericht nadat Hallo-beveiligingsgroep is gemaakt.
    
    ![Samenvatting](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-dpm"></a>Herstellen van een SharePoint-item van de schijf met behulp van DPM
Hallo in Hallo voorbeeld te volgen, *herstellen van SharePoint-item* per ongeluk is verwijderd en moet toobe hersteld.
![DPM SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)

1. Open Hallo **DPM Administrator-Console**. Alle SharePoint-farms die zijn beveiligd door DPM worden weergegeven in Hallo **beveiliging** tabblad.
   
    ![DPM SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. Selecteer Hallo-toobegin toorecover Hallo item **herstel** tabblad.
   
    ![DPM SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. U kunt zoeken in SharePoint voor *herstellen van SharePoint-item* verwijzen met behulp van een zoekopdracht op basis van een jokerteken binnen een herstelbewerking bereik.
   
    ![DPM SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. Selecteer de juiste herstelpunt Hallo in zoekresultaten Hallo, met de rechtermuisknop op het Hallo-item en selecteer **herstellen**.
5. U kunt ook door verschillende herstelpunten bladeren en selecteren van een database of item toorecover. Selecteer **datum > hersteltijd**, en selecteer vervolgens de juiste Hallo **Database > SharePoint-farm > herstelpunt > Item**.
   
    ![DPM SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. Hallo-item met de rechtermuisknop en selecteer vervolgens **herstellen** tooopen hello **Herstelwizard**. Klik op **Volgende**.
   
    ![Selectie voor herstel controleren](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. Selecteer Hallo type herstel dat u tooperform wilt en klik vervolgens op **volgende**.
   
    ![Hersteltype](./media/backup-azure-backup-sharepoint/select-recovery-type.png)
   
   > [!NOTE]
   > selectie van Hallo **toooriginal herstellen** in Hallo voorbeeld Hallo item toohello oorspronkelijke SharePoint-site herstelt.
   > 
   > 
8. Selecteer Hallo **herstelproces** dat u wilt dat toouse.
   
   * Selecteer **herstellen zonder herstelfarm** als Hallo SharePoint-farm is niet gewijzigd en Hallo dezelfde zijn als Hallo herstel die wijst wordt hersteld.
   * Selecteer **herstellen met behulp van een herstelfarm** als Hallo SharePoint-farm is gewijzigd sinds Hallo herstelpunt is gemaakt.
     
     ![Herstelproces](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. Een SQL Server-exemplaar locatie toorecover Hallo faseringsdatabase tijdelijk, en bieden een tijdelijke bestandsshare op Hallo DPM-server en Hallo-server waarop SharePoint toorecover Hallo-item wordt uitgevoerd.
   
    ![Fasering Location1](./media/backup-azure-backup-sharepoint/staging-location1.png)
   
    DPM voegt Hallo inhoudsdatabase die als host voor Hallo SharePoint-item toohello tijdelijke SQL Server-exemplaar fungeert. Hallo inhoudsdatabase Hallo DPM-server Hallo item herstelt en plaatst deze op Hallo tijdelijke bestandslocatie op Hallo DPM-server. Hallo moet herstelde item dat zich op een tijdelijke locatie van de DPM-server Hallo nu Hallo toobe geëxporteerd toohello tijdelijke locatie op Hallo SharePoint-farm.
   
    ![Fasering Location2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. Selecteer **herstelopties opgeven**, en toepassen van beveiliging instellingen toohello SharePoint-farm of toepassen van beveiligingsinstellingen Hallo Hallo herstelpunt werd gemaakt. Klik op **Volgende**.
    
    ![Opties voor herstel](./media/backup-azure-backup-sharepoint/recovery-options.png)
    
    > [!NOTE]
    > U kunt toothrottle Hallo netwerkbandbreedte gebruikt. Hierdoor minimaliseert impact toohello productieserver tijdens de productie-uren.
    > 
    > 
11. Hallo samenvattingsinformatie controleren en klik vervolgens op **herstellen** toobegin herstellen van Hallo-bestand.
    
    ![Samenvatting van herstel](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. Nu selecteren Hallo **bewaking** tabblad in Hallo **DPM Administrator-Console** tooview hello **Status** Hallo herstel.
    
    ![Herstelstatus](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)
    
    > [!NOTE]
    > Hallo-bestand is nu hersteld. U kunt Hallo SharePoint-site toocheck Hallo hersteld bestand vernieuwen.
    > 
    > 

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a>Een SharePoint-database herstellen van Azure met DPM
1. een SharePoint-inhoudsdatabase toorecover bladeren door verschillende herstelpunten (zoals eerder is weergegeven) en selecteer Hallo herstelpunt dat u wilt dat toorestore.
   
    ![DPM SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. Dubbelklik op Hallo SharePoint punt tooshow Hallo beschikbaar SharePoint-catalogus herstelgegevens.
   
   > [!NOTE]
   > Omdat de SharePoint-farm Hallo voor lange bewaartermijn in Azure wordt beveiligd, is er is geen catalogusinformatie (metagegevens) beschikbaar op Hallo DPM-server. Als gevolg hiervan als een SharePoint-inhoudsdatabase punt in tijd toobe hersteld moet, moet u toocatalog Hallo SharePoint-farm opnieuw.
   > 
   > 
3. Klik op **opnieuw catalogiseren**.
   
    ![DPM SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)
   
    Hallo **Cloud opnieuw catalogiseren** statusvenster wordt geopend.
   
    ![DPM SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)
   
    Nadat catalogiseren is voltooid, Hallo status verandert te*geslaagd*. Klik op **Sluiten**.
   
    ![DPM SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. Klik op Hallo SharePoint-object wordt weergegeven in DPM Hallo **herstel** tabblad tooget Hallo inhoudsdatabase structuur. Met de rechtermuisknop op het Hallo-item en klik vervolgens op **herstellen**.
   
    ![DPM SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. Op dit moment volgen Hallo [herstel stappen eerder in dit artikel](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover een SharePoint-inhoudsdatabase van de schijf.

## <a name="faqs"></a>Veelgestelde vragen
V: welke versies van DPM ondersteuning voor SQL Server 2014 en SQL 2012 (SP2)?<br>
A: DPM 2012 R2 met updatepakket 4 ondersteunt zowel.

V: kan ik een SharePoint-item toohello oorspronkelijke locatie herstellen als SharePoint is geconfigureerd met behulp van SQL AlwaysOn (met beveiliging op schijf)?<br>
A: Hallo-item kan Ja, de herstelde toohello oorspronkelijke SharePoint-site zijn.

V: kan ik een SharePoint-database toohello oorspronkelijke locatie herstellen als SharePoint met behulp van SQL AlwaysOn is geconfigureerd?<br>
A: omdat SharePoint-databases zijn geconfigureerd in de SQL AlwaysOn, kan deze niet worden gewijzigd als Hallo beschikbaarheidsgroep wordt verwijderd. Hierdoor kan DPM niet een database toohello oorspronkelijke locatie herstellen. U kunt een SQL Server-exemplaar van SQL Server-database tooanother herstellen.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over DPM-beveiliging van SharePoint - Zie [Video Series - DPM-beveiliging van SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)
* Bekijk [releaseopmerkingen voor System Center 2012 - Data Protection Manager](https://technet.microsoft.com/library/jj860415.aspx)
* Bekijk [releaseopmerkingen voor Data Protection Manager in System Center 2012 SP1](https://technet.microsoft.com/library/jj860394.aspx)

