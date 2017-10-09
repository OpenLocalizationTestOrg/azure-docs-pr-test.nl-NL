---
title: aaaGet gestart met een Azure-logboekanalyse-werkruimte | Microsoft Docs
description: U kunt binnen enkele minuten aan de slag met een Azure Log Analytics-werkruimte.
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 508716de-72d3-4c06-9218-1ede631f23a6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/08/2017
ms.author: magoedte
ms.openlocfilehash: 442a9258a37ee79e8f0b45759ef24b5e3dae0130
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-a-log-analytics-workspace"></a>Aan de slag met een Log Analytics-werkruimte
U kunt snel aan de slag met Azure Log Analytics. Deze service helpt u bij het evalueren van operationele gegevens die over uw IT-infrastructuur zijn verzameld. Aan de hand van dit artikel kunt u gemakkelijk beginnen met het verkennen, analyseren en benutten van gegevens die u *gratis* verzamelt.

In dit artikel fungeert als een inleiding tooLog Analytics met een korte zelfstudie toowalk u via een minimale implementatie in Azure zodat u kunt nu Hallo-service gebruiken. Hallo logische container waar de gegevens van uw management in Azure worden opgeslagen, wordt een werkruimte genoemd. Nadat u hebt deze informatie bekeken en uw eigen evaluatie voltooid, kunt u Hallo evaluatie werkruimte verwijderen. Omdat dit artikel een zelfstudie betreft, blijven specifieke bedrijfsbehoeften, planningsvereisten en architectuurrichtlijnen buiten beschouwing.

>[!NOTE]
>Als u Microsoft Azure Government Cloud hello, gebruik [Azure Government Monitoring + Management-documentatie](https://docs.microsoft.com/azure/azure-government/documentation-government-services-monitoringandmanagement#log-analytics) in plaats daarvan.

Hier volgt een kort overzicht van Hallo proces gebruikt tooget gestart:

![procesdiagram](./media/log-analytics-get-started/onboard-oms.png)

## <a name="1-create-an-azure-account-and-sign-in"></a>1 Een Azure-account maken en u aanmelden

Als u nog een Azure-account hebt, moet u toocreate één toouse logboekanalyse. U kunt een [gratis account](https://azure.microsoft.com/free/) maken dat 30 dagen geldig is en waarmee u toegang hebt tot alle Azure-services.

### <a name="toocreate-a-free-account-and-sign-in"></a>een gratis account toocreate en u aanmelden
1. Volg de aanwijzingen Hallo op [uw gratis Azure-account maken](https://azure.microsoft.com/free/).
2. Ga toohello [Azure-portal](https://portal.azure.com) en meld u aan.

## <a name="2-create-a-workspace"></a>2 Een werkruimte maken

de volgende stap Hallo is toocreate een werkruimte.

1. Zoek in hello Azure-portal, Hallo lijst met services in Hallo Marketplace voor *logboekanalyse*, en selecteer vervolgens **logboekanalyse**.  
    ![Azure Portal](./media/log-analytics-get-started/log-analytics-portal.png)
2. Klik op **maken**, schakelt u opties voor de volgende items Hallo:
   * **OMS-werkruimte**: geef een naam op voor uw werkruimte.
   * **Abonnement** : als u meerdere abonnementen, kies de gewenste tooassociate met de nieuwe werkruimte Hallo Hallo hebt.
   * **Resourcegroep**
   * **Locatie**
   * **Prijscategorie**  
       ![snel maken](./media/log-analytics-get-started/oms-onboard-quick-create.png)
3. Klik op **OK** toosee een lijst met uw werkruimten.
4. Selecteer een werkruimte toosee de details ervan in hello Azure-portal.       
    ![details van de werkruimte](./media/log-analytics-get-started/oms-onboard-workspace-details.png)         

## <a name="3-upgrade-workspace-toonew-log-search"></a>3 upgrade werkruimte toonew logboek zoeken
Een nieuwe Log Analytics-querytaal is vrijgegeven en in de volgorde tootake profiteren, moet u tooconvert uw werkruimte.  Als het Hallo-regio die wordt gehost door uw werkruimte is bijgewerkt, ziet u een paarse banner aan de bovenkant Hallo van uw werkruimte uitnodiging tooconvert. Hallo-upgrade is geheel vrijwillig en heeft geen gevolgen voor uw ervaring met logboekanalyse en eventuele oplossingen die u toevoegt.  

Zie voor meer informatie toounderstand Hallo voordeel, overwegingen en proces tooupgrade [upgraden Azure Log Analytics toonew logboek zoeken](log-analytics-log-search-upgrade.md).  

## <a name="4-add-solutions-and-solution-offerings"></a>4 Oplossingen en oplossingenpakketten toevoegen

Voeg vervolgens beheeroplossingen en oplossingenpakketten toe. Beheeroplossingen bestaan uit een combinatie van logica, visualisatiemogelijkheden en regels voor gegevensverwerving die metrische gegevens bieden met betrekking tot een specifiek probleemgebied. Een oplossingenpakket is een samenstelling van meerdere beheeroplossingen.

Oplossingen tooyour werkruimte kan logboekanalyse toocollect verschillende soorten gegevens van computers die zijn verbonden tooyour werkruimte op basis van agents. Het onboarden van deze agents komt later aan bod.

### <a name="tooadd-solutions-and-solution-offerings"></a>tooadd oplossingen en oplossingen

1. In Azure-portal klikt u op **nieuw** en klik vervolgens in Hallo **zoeken Hallo marketplace** in het vak **activiteit Log Analytics** en druk op ENTER.
2. Hallo alles in select blade **activiteit Log Analytics** en klik vervolgens op **maken**.  
    ![Activity Log Analytics](./media/log-analytics-get-started/activity-log-analytics.png)  
3. In Hallo *management oplossingsnaam* blade, selecteert u een werkruimte die u tooassociate met Hallo-beheeroplossing wilt.
4. Klik op **Create**.  
    ![werkruimte voor de oplossing](./media/log-analytics-get-started/solution-workspace.png)  
5. Herhaal stap 1-4 tooadd:
    - Hallo **beveiliging en naleving** serviceaanbieding met Hallo Assessment Antimalware- en beveiligings- en Audit-oplossingen.
    - Hallo **Automation en Control** serviceaanbieding met Hallo Automation Hybrid Worker, bijhouden en oplossingen voor Update-evaluatie System (ook wel updatebeheer). Wanneer u Hallo oplossing door toevoegt, moet u een Automation-account maken.  
        ![Automation-account](./media/log-analytics-get-started/automation-account.png)  
6. U kunt bekijken Hallo oplossingen die u hebt toegevoegd tooyour werkruimte door te navigeren**logboekanalyse** > **abonnementen** > ***Werkruimtenaam***  >  **Overzicht**. Tegels voor Hallo oplossingen die u hebt toegevoegd, worden weergegeven.  
    >[!NOTE]
    >Omdat we een werkruimte agents toohello nog niet hebt verbonden, ziet u geen gegevens voor Hallo-oplossingen die u hebt toegevoegd.  

    ![oplossingstegels zonder gegevens](./media/log-analytics-get-started/solutions-no-data.png)

## <a name="4-create-a-vm-and-onboard-an-agent"></a>4 Een virtuele machine maken en een agent onboarden

Maak vervolgens een eenvoudige virtuele machine in Azure. Nadat u een virtuele machine, vrijgeven Hallo OMS-agent tooenable maken het. Verzamelen van gegevens van Hallo VM gestart en de inschakelen Hallo agent verzendt gegevens tooLog Analytics.

### <a name="toocreate-a-virtual-machine"></a>toocreate een virtuele machine

- Volg de aanwijzingen Hallo op [uw eerste virtuele Windows-machine maken in Azure-portal Hallo](../virtual-machines/virtual-machines-windows-hero-tutorial.md) en Hallo nieuwe virtuele machine te starten.

### <a name="connect-hello-virtual-machine-toolog-analytics"></a>Verbinding maken met de Hallo virtuele machine tooLog Analytics

- Volg de aanwijzingen Hallo op [verbinding maken met Azure virtuele machines tooLog Analytics](log-analytics-azure-vm-extension.md) tooconnect Hallo VM tooLog Analytics gebruiken hello Azure-portal.

## <a name="6-view-and-act-on-data"></a>6 Gegevens weergeven en er actie op ondernemen

Voorheen u Hallo activiteit Log Analytics-oplossing en Hallo beveiliging en naleving en Automation en Control serviceaanbiedingen ingeschakeld. Nu gaan we kijken naar de gegevens die door deze oplossingen zijn verzameld en naar de resultaten van zoeken in logboeken.

toostart, blik op gegevens die worden weergegeven uit binnen de oplossingen. Bekijk vervolgens de resultaten van enkele zoekopdrachten in logboeken. Logboek zoekopdrachten kunnen u toocombine en correleren machinegegevens uit meerdere bronnen binnen uw omgeving. Zie voor meer informatie [zoekopdrachten aanmelden met logboekanalyse](log-analytics-log-searches.md) of als u uw werkruimte toohello nieuwe querytaal geconverteerd, Zie [understanding logboek zoekt in logboekanalyse](log-analytics-log-search-new.md). 

### <a name="tooview-antimalware-data"></a>tooview Antimalware-gegevens

1. In Azure-portal Hallo, te navigeren**logboekanalyse** > ***uw werkruimte***.
2. Hallo-blade voor uw werkruimte onder **algemene**, klikt u op **overzicht**.  
    ![Overzicht](./media/log-analytics-get-started/overview.png)
3. Klik op Hallo **Antimalware Assessment** tegel. In dit voorbeeld ziet u dat op één computer Windows Defender is geïnstalleerd, maar dat de handtekening is verouderd.  
    ![Antimalware](./media/log-analytics-get-started/solution-antimalware.png)
4. In dit voorbeeld onder **beveiligingsstatus**, klikt u op **handtekening verouderd** tooopen logboek Zoek- en details over Hallo-computers die verouderd handtekeningen hebben. In dit voorbeeld te zien die Hallo-computer met de naam *getstarted*. Als er meer dan één computer met verouderd handtekeningen, deze alle worden weergegeven in Hallo logboek zoeken resultaten.  
    ![Antimalware verouderd](./media/log-analytics-get-started/antimalware-search.png)

### <a name="tooview-security-and-audit-data"></a>tooview beveiligings-en controle

1. Hallo-blade voor uw werkruimte onder **algemene**, klikt u op **overzicht**.  
2. Klik op Hallo **beveiligings- en Audit** tegel. In dit voorbeeld ziet u dat er twee belangrijke problemen zijn: er is een computer waarop essentiële updates ontbreken en er is een computer met onvoldoende beveiliging.  
    ![Beveiliging en controle](./media/log-analytics-get-started/security-audit.png)
3. In dit voorbeeld onder **problemen die aandacht vereisen**, klikt u op **Computers waarop essentiële updates ontbreken** tooopen logboek Zoek- en informatie over de computers waarop essentiële updates ontbreken. In dit voorbeeld ontbreekt er één essentiële update, plus nog 63 andere updates.  
    ![Zoeken in logboeken met betrekking tot beveiliging en controle](./media/log-analytics-get-started/security-audit-log-search.png)

### <a name="tooview-and-act-on-system-update-data"></a>tooview en act op systeemupdate gegevens

1. Hallo-blade voor uw werkruimte onder **algemene**, klikt u op **overzicht**.  
2. Klik op Hallo **System Update-evaluatie** tegel. In dit voorbeeld ziet u dat er een Windows-computer is met de naam *getstarted* die essentiële updates vereist en een computer die definitie-updates vereist.  
    ![Systeemupdates](./media/log-analytics-get-started/system-updates.png)
3. In dit voorbeeld onder **ontbrekende Updates**, klikt u op **essentiële Updates** tooopen logboek Zoek- en informatie over de computers waarop essentiële updates ontbreken. In dit voorbeeld ontbreekt één update en is er één vereiste update.  
    ![Zoeken in logboeken met betrekking tot systeemupdates](./media/log-analytics-get-started/system-updates-log-search.png)
4. Ga toohello [Operations Management Suite](http://microsoft.com/oms) website en meld u aan met uw Azure-account. Wanneer u bent aangemeld, ziet dat de oplossingsgegevens Hallo vergelijkbare toowhat ziet u hebt in hello Azure-portal.  
    ![OMS-portal](./media/log-analytics-get-started/oms-portal.png)
5. Klik op Hallo **updatebeheer** tegel.
6. Hallo bijwerken Management dashboard, merkt dat Hallo update systeemgegevens soortgelijke toohello systeem informatie die u in hello Azure-portal gezien hebt. Hallo echter **Update-implementaties beheren** tegel is er nieuw. Klik op Hallo **Update-implementaties beheren** tegel.  
    ![Tegel Update Management](./media/log-analytics-get-started/update-management.png)
7. Op Hallo **implementaties bijwerken** pagina, klikt u op **toevoegen** toocreate een *update-uitvoering*.  
    ![Update-implementaties](./media/log-analytics-get-started/update-management-update-deployments.png)
8.  Op Hallo **nieuwe implementatie-Update** pagina, typ een naam voor het Hallo-update-implementatie, selecteert u computers tooupdate (in dit voorbeeld *getstarted*), kiest u een planning en klik vervolgens op **Opslaan**.  
    ![Nieuwe implementatie](./media/log-analytics-get-started/new-deployment.png)  
    Nadat u de update-implementatie Hallo opslaat, ziet u Hallo gepland bijwerken.  
    ![geplande update](./media/log-analytics-get-started/scheduled-update.png)  
    Nadat Hallo update-uitvoering is voltooid, ziet de status Hallo **voltooid**.
    ![voltooide update](./media/log-analytics-get-started/completed-update.png)
9. Nadat Hallo update-uitvoering is voltooid, kunt u weergeven of Hallo voeren geslaagd of mislukt is en u meer informatie vindt over welke updates wanneer toegepast.

## <a name="after-evaluation"></a>Evaluatie van deze zelfstudie

In deze zelfstudie hebt u een agent geïnstalleerd op een virtuele machine en bent u snel aan de slag gegaan. Hallo-stappen die u hebt gevolgd is snel en eenvoudig. De meeste grote organisaties en ondernemingen hebben echter complexe on-premises IT-infrastructuren. Dus duurt verzamelen van gegevens van deze complexe omgevingen extra planning en moeite dan Hallo zelfstudie. Hallo-informatie in de volgende sectie van de volgende stappen voor koppelingen toohelpful artikelen hello te controleren.

Hallo-werkruimte die u hebt gemaakt in deze zelfstudie kunt u desgewenst verwijderen.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over het aansluiten van [Windows-agents](log-analytics-windows-agents.md) tooLog Analytics.
* Meer informatie over het aansluiten van [Operations Manager-agents](log-analytics-om-agents.md) tooLog Analytics.
* [Log Analytics-oplossingen van Hallo oplossingen galerie toevoegen](log-analytics-add-solutions.md) tooadd functionaliteit en verzamelen gegevens.
* Raken met [Meld zoekopdrachten](log-analytics-log-searches.md) tooview gedetailleerde informatie verzameld door oplossingen.
