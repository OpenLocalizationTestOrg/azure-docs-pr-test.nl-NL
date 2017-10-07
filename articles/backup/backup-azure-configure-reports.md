---
title: aaaConfigure rapporten voor Azure Backup
description: In dit artikel wordt gesproken over het configureren van Power BI-rapporten voor Azure Backup aan de hand van de Recovery Services-kluis.
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 86e465f1-8996-4a40-b582-ccf75c58ab87
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 503a240b36ea999e0fea434b6a50d26ddf7677bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-backup-reports"></a>Azure Backup-rapporten configureren
In dit artikel wordt gesproken over stappen tooconfigure rapporten voor Azure Backup Recovery Services-kluis en tooaccess met deze rapporten via Power BI. Na deze stappen uitvoert, kunt u rechtstreeks tooPower BI tooview gaan alle Hallo rapporten, aanpassen en rapporten maken. 

## <a name="supported-scenarios"></a>Ondersteunde scenario 's
1. Azure Backup-rapporten worden ondersteund voor virtuele machine van Azure back-up en het bestand/map back-toocloud met behulp van de Azure Recovery Services Agent.
2. Rapporten voor Azure SQL, DPM en Azure Backup-Server worden niet ondersteund op dit moment.
3. U kunt rapporten weergeven tussen kluizen en abonnementen, als hetzelfde opslagaccount is geconfigureerd voor elk Hallo kluizen. Geselecteerde opslagaccount moet Hallo dezelfde regio bevinden als de recovery services-kluis.
4. Hallo frequentie van geplande vernieuwing voor Hallo rapporten is 24 uur in Power BI. U kunt ook een ad-hoc vernieuwing van Hallo rapporten in Power BI, waarin de meest recente gegevens van de case in klant storage-account wordt gebruikt voor het weergeven van rapporten uitvoeren. 

## <a name="prerequisites"></a>Vereisten
1. Maak een [Azure storage-account](../storage/common/storage-create-storage-account.md#create-a-storage-account) tooconfigure voor rapporten. Dit opslagaccount wordt gebruikt voor het opslaan van de bijbehorende gegevens van rapporten.
2. [Een Power BI-account maken](https://powerbi.microsoft.com/landing/signin/) tooview, aanpassen en uw eigen rapporten maken met Power BI-portal.
3. Hallo registerbronprovider **Microsoft.insights** als niet al is geregistreerd, met Hallo-abonnement van de storage-account en met Hallo-abonnement van de Recovery Services-kluis tooenable reporting gegevens tooflow toohello Storage-account. toodo Hallo dezelfde, moet u tooAzure portal gaan > abonnement > resourceproviders en controleer of deze provider tooregister deze. 

## <a name="configure-storage-account-for-reports"></a>Opslagaccount voor rapporten configureren
Gebruik hello tooconfigure Hallo storage-account voor de recovery services-kluis met Azure portal stappen te volgen. Dit is een eenmalige configuratie en zodra storage-account is geconfigureerd, kunt u tooPower BI gaan direct tooview inhoudspakket en gebruik de rapporten.
1. Als u al een Recovery Services-kluis openen, gaat u verder toonext stap. Als u geen een Recovery Services-kluis is geopend hebt, maar in hello Azure-portal op Hallo Hub-menu zijn, klikt u op **Bladeren**.

   * Typ in de lijst met resources Hallo **Recovery Services**.
   * Als u te typen begint, Hallo lijstfilters op basis van uw invoer. Wanneer **Recovery Services-kluizen** wordt weergegeven, klikt u erop.

      ![Een Recovery Services-kluis maken, stap 1](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     Hallo-lijst met Recovery Services-kluizen wordt weergegeven. Selecteer in Hallo lijst met Recovery Services-kluizen een kluis.

     Hallo geselecteerde kluisdashboard wordt geopend.
2. Uit Hallo lijst met items die onder de kluis wordt weergegeven, klikt u op **back-up rapporten** onder bewaking en rapporten sectie tooconfigure Hallo storage-account voor rapporten.

      ![Selecteer back-up rapporten menu-item stap 2](./media/backup-azure-configure-reports/backup-reports-settings.PNG)
3. Klik op de blade back-up rapporten Hallo **configureren** knop. Hiermee opent u hello Azure Application Insights blade die wordt gebruikt voor het pushen van gegevens toocustomer storage-account.

      ![Storage-account-stap 3 configureren](./media/backup-azure-configure-reports/configure-storage-account.PNG)
4. Hallo Status wisselknop te ingesteld**op** en selecteer **tooa Opslagaccount archiveren** inschakelen, zodat reporting gegevens kunt beginnen met het stromende in toohello storage-account.

      ![Stap 4 van diagnostische gegevens inschakelen](./media/backup-azure-configure-reports/set-status-on.png)
5. Klik op Opslagaccount kiezen en selecteer Hallo storage-account in de lijst Hallo voor het opslaan van gegevens en klik op **OK**.

      ![Selecteer de storage-account-stap 5](./media/backup-azure-configure-reports/select-storage-account.png)
6. Selecteer **AzureBackupReport** selectievakje en ook verplaatsen Hallo schuifregelaar tooselect bewaarperiode voor dit rapportgegevens. Rapportgegevens in Hallo storage-account wordt voor Hallo periode met behulp van deze schuifregelaar opgeslagen.

      ![Selecteer de storage-account-stap 6](./media/backup-azure-configure-reports/save-configuration.png)
7. Controleer alle Hallo wijzigingen en klik op **opslaan** knop bovenaan, zoals wordt weergegeven in de bovenstaande Hallo-afbeelding. Deze actie zorgt ervoor dat al uw wijzigingen zijn opgeslagen en storage-account is nu geconfigureerd voor het opslaan van rapportgegevens.

> [!NOTE]
> Wanneer u rapporten door op te slaan storage-account configureert, moet u **24 uur wachten** voor initiële gegevens push toocomplete. Azure Backup in Power BI-inhoudspakket importeert u alleen na dit tijdstip. Raadpleeg [sectie Veelgestelde vragen over](#frequently-asked-questions) voor meer informatie. 
>
>

## <a name="view-reports-in-power-bi"></a>Rapporten weergeven in Power BI 
Het duurt ongeveer 24 uur voor het melden van gegevens toostart stromende nadat het opslagaccount voor het configureren van rapporten met behulp van de recovery services-kluis. Gebruik Hallo volgende stappen na 24 uur voor het instellen van opslagaccount tooview rapporten in Power BI:
1. [Meld u aan](https://powerbi.microsoft.com/landing/signin/) tooPower BI.
2. Klik op **gegevens ophalen** en klik op Get onder **Services** in de Inhoudsbibliotheek Pack. Gebruik de stappen die worden vermeld in [Power BI-documentatie tooaccess inhoud pack](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-packs-services/).

     ![Het inhoudspakket importeren](./media/backup-azure-configure-reports/content-pack-import.png)
3. Type **Azure Backup** in de zoekbalk en op **nu downloaden**.

      ![Inhoudspakket ophalen](./media/backup-azure-configure-reports/content-pack-get.png)
4. Voer Hallo opslagaccountnaam in stap 5 hierboven hebt geconfigureerd en klik op **volgende** knop.

    ![Voer opslagaccountnaam in](./media/backup-azure-configure-reports/content-pack-storage-account-name.png)    
5. Voer de opslagaccountsleutel Hallo voor dit opslagaccount. U kunt [bekijken en kopiëren van de toegangssleutels voor opslag](../storage/common/storage-create-storage-account.md#manage-your-storage-account) door te navigeren tooyour storage-account in Azure-portal. 

     ![Voer het opslagaccount](./media/backup-azure-configure-reports/content-pack-storage-account-key.png) <br/>
     
6. Klik op **aanmelden** knop. Nadat de aanmelding is geslaagd, u krijgt **importeren van gegevens** melding.

    ![Inhoudspakket importeren](./media/backup-azure-configure-reports/content-pack-importing-data.png) <br/>
    
    Na enige tijd krijgt u **geslaagd** melding nadat Hallo importeren voltooid is. Weinig langer tooimport Hallo-inhoudspakket kan duren als er een grote hoeveelheid gegevens in Hallo storage-account.
    
    ![Geslaagd-inhoudspakket importeren](./media/backup-azure-configure-reports/content-pack-import-success.png) <br/>
    
7. Wanneer u gegevens importeert **Azure Backup** inhoudspakket is zichtbaar in **Apps** in het navigatiedeelvenster Hallo. Hallo-lijst bevat nu Azure Backup-dashboard en rapporten, gegevensset met een gele ster zojuist geïmporteerde rapporten die aangeeft. 

     ![Azure Backup-inhoudspakket](./media/backup-azure-configure-reports/content-pack-azure-backup.png) <br/>
     
8. Klik op **Azure Backup** onder Dashboards, waarmee een reeks vastgezette belangrijkste rapporten wordt weergegeven.

      ![Azure Backup-dashboard](./media/backup-azure-configure-reports/azure-backup-dashboard.png) <br/>
9. tooview hello volledige set van rapporten, klikt u op een rapport in Hallo-dashboard.

      ![Status van de taak Azure back-up](./media/backup-azure-configure-reports/azure-backup-job-health.png) <br/>
10. Klik op elk tabblad in Hallo rapporten tooview rapporten in het desbetreffende gebied.

      ![Tabbladen met Azure Backup-rapporten](./media/backup-azure-configure-reports/reports-tab-view.png)


## <a name="frequently-asked-questions"></a>Veelgestelde vragen
1. **Hoe kan ik controleren als rapportagegegevens in toostorage-account dat is gestart?**
    
    U kunt gaan toohello opslag containers geconfigureerde en selecteert u een account. Als Hallo container een vermelding voor insights-logboeken-azurebackupreport heeft, betekent dit dat rapportagegegevens is gestart stromende.

2. **Wat is Hallo frequentie van toostorage account voor push-gegevens en Azure Backup-inhoudspakket in Power BI?**

   Voor gebruikers van Day 0 zou zij rekening ongeveer 24 uur toopush gegevens toostorage. Zodra deze initiële push compelete is, kunnen gegevens worden vernieuwd met de volgende frequentie wordt weergegeven in onderstaande afbeelding ziet Hallo Hallo. 
      * Gegevens gerelateerd te**taken, waarschuwingen, back-Upitems, kluizen, beveiligde Servers en -beleid** wordt doorgeschoven toocustomer storage-account als en wanneer deze fout wordt vastgelegd.
      * Gegevens gerelateerd te**opslag** gepusht toocustomer storage-account om de 24 uur.
   
    ![Azure Backup-rapporten gegevens push frequentie](./media/backup-azure-configure-reports/reports-data-refresh-cycle.png)

  Power BI heeft een [geplande vernieuwing eenmaal per dag](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/#what-can-be-refreshed). U kunt handmatig vernieuwen van het Hallo-gegevens in Power BI uitvoeren voor Hallo-inhoudspakket.

3. **Hoe lang kan ik Hallo rapporten behouden?** 

   Tijdens het configureren van storage-account, kunt u de bewaarperiode van rapportagegegevens in Hallo storage-account (met stap 6 in de storage-account configureren voor rapporten sectie hierboven) selecteren. Behalve dat u kunt [rapporten analyseren in excel](https://powerbi.microsoft.com/documentation/powerbi-service-analyze-in-excel/) en deze wilt opslaan voor een langere bewaartermijn volgens uw behoeften. 

4. **Ziet ik mijn gegevens in rapporten na het configureren van Hallo storage-account?**

   Alle gegevens die zijn gegenereerd na Hallo **'storage-account configureren'** wordt gepusht toohello storage-account en is beschikbaar in rapporten. Echter, **In voortgang taken niet worden gepusht** voor rapportage. Zodra het Hallo-taak is voltooid of mislukt, wordt het tooreports verzonden.

5. **Als ik account Hallo-tooview opslagrapporten al hebt geconfigureerd, kan ik wijzigen Hallo configuratie toouse een ander opslagaccount?** 

   Ja, kunt u Hallo configuratie toopoint tooa ander opslagaccount. Hallo zojuist geconfigureerd storage-account moet u gebruiken bij het verbinden van tooAzure back-up-inhoudspakket. Zodra een ander opslagaccount is geconfigureerd, zou ook nieuwe gegevens in dit opslagaccount stromen. Maar oudere gegevens (vóór het Hallo-configuratie wijzigen) nog steeds in Hallo oudere storage-account.

6. **Kan ik rapporten bekijken tussen kluizen en abonnementen?** 

   Ja, kunt u Hallo hetzelfde opslagaccount via verschillende kluizen tooview cross-kluis rapporten. Bovendien kunt u hetzelfde opslagaccount voor kluizen Hallo voor abonnementen. U kunt dit opslagaccount vervolgens gebruiken bij het verbinden van tooAzure back-up-inhoudspakket in Power BI tooview Hallo-rapporten. Hallo geselecteerde opslagaccount moet echter in Hallo dezelfde regio bevinden als de recovery services-kluis.
   
## <a name="next-steps"></a>Volgende stappen
Nu u hebt geconfigureerd Hallo storage-account en geïmporteerde inhoudspakket van Azure Backup, de volgende stap Hallo is toocustomize deze rapporten en gebruik reporting data model toocreate rapporten. Raadpleeg Hallo volgende artikelen voor meer informatie.

* [Met behulp van Azure Backup-gegevensmodel rapportage](backup-azure-reports-data-model.md)
* [Filteren van rapporten in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-about-filters-and-highlighting-in-reports/)
* [Maken van rapporten in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)

