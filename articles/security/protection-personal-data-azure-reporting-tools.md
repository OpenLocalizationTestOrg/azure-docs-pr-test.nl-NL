---
title: beveiliging van persoonlijke gegevens met Azure-hulpprogramma's voor rapportage aaaDocument | Microsoft Docs
description: "hoe toouse Azure reporting services en -technologieën toohelp privacy van persoonlijke gegevens beschermen."
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 3230d26ed308a8a0e72421c001793be06334a7c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="document-protection-of-personal-data-with-azure-reporting-tools"></a>Beveiliging voor documenten van persoonlijke gegevens met Azure-hulpprogramma's voor rapportage

In dit artikel wordt beschreven hoe toouse rapportage van Azure services en technologieën toohelp privacy van persoonlijke gegevens te beschermen.

## <a name="scenario"></a>Scenario

Een grote cruise bedrijf, gevestigd in Hallo Verenigde Staten, wordt de bewerkingen toooffer routes in Hallo Middellandse, Adriatische, Baltische veiligheid ook Hallo Florida uitbreiden. toohelp deze inspanningen, heeft deze meerdere kleinere cruise regels op basis van Italië, verkregen Duitsland, Denemarken en Hallo Verenigd Koninkrijk

Hallo bedrijf gebruikmaakt van Microsoft Azure voor verwerking en opslag van bedrijfsgegevens. Dit omvat persoonlijk gegevens zoals namen, adressen, telefoonnummers en creditcardgegevens van globale klantendatabase. Dit omvat ook traditionele Human Resources informatie zoals adressen, telefoonnummers, BTW-id's en medische informatie over de werknemers van het bedrijf op alle locaties. Hallo cruise regel onderhoudt ook een grote database van derden en loyaliteit voor leden die persoonlijke gegevens tootrack relaties met de huidige en eerdere klanten bevat.

Zakelijke werknemers toegang tot het Hallo netwerk van de externe kantoren en reizen agents van het bedrijf Hallo wereld Hallo zich toegang tot toosome bedrijfsbronnen hebben.

## <a name="problem-statement"></a>Probleemformulering

Hallo bedrijf moet Hallo privacy van klanten en werknemers persoonlijke gegevens via een meerlaagse beveiligingsstrategie die gebruikmaakt van Azure management en functies tooimpose strikte beveiligingsmechanismen toegang tooand verwerking van persoonlijke gegevens van en moet beveiligen kan toodemonstrate de beschermende maatregelen toointernal en externe accountants.

## <a name="company-goal"></a>Bedrijf-doel

Als onderdeel van de beveiligingsstrategie van defense-in-depth, deze is een bedrijf doel tootrack toegang tooand verwerking van persoonlijke gegevens en zorg ervoor dat de documentatie van de juiste privacy-bescherming voor persoonlijke gegevens zijn ingesteld en functioneert.

## <a name="solutions"></a>Oplossingen

Microsoft Azure biedt een uitgebreide controle, logboekregistratie en diagnostische hulpprogramma's voor toohelp bijhouden en activiteiten en gebeurtenissen met betrekking tot toegang tot en het verwerken van persoonlijke gegevens, geografische stroom van gegevens en de toegang van derden toopersonal gegevens vastleggen. Omdat de beveiliging van persoonlijke gegevens in de cloud Hallo is een gedeelde verantwoordelijkheid, biedt Microsoft ook klanten:

- Gedetailleerde informatie over een eigen verwerken van gegevens van klanten

- Veiligheidsmaatregelen beheerd door Microsoft

- Waar en hoe het versturen van gegevens van klanten

- Details van de Microsoft privacy beoordelingen proces

### <a name="azure-active-directory"></a>Azure Active Directory

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) van Microsoft cloud-gebaseerde, multitenant directory en identity management-service is. Hallo van de service zich aanmelden en rapportagemogelijkheden audit u voorzien van gedetailleerde aanmelden en toepassing gebruik activiteit informatie toohelp u bewaken en zorg ervoor dat de juiste toegangsrechten toocustomers en werknemers persoonlijke gegevens.

Er zijn twee soorten activiteitsrapporten:

- Hallo [audit activiteitenlogboeken rapporten](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) bieden gedetailleerde gegevens over systeemtaken activiteiten

- Hallo [aanmeldingen rapport/activiteitenlogboek](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) bevat die is uitgevoerd. elke activiteit die worden vermeld in het Hallo-controlerapport

Hallo twee samen gebruikt, kunt u bijhouden Hallo geschiedenis van elke taak uit te voeren en door wie elk uitgevoerd. Beide typen rapporten kunnen worden aangepast en kunnen worden gefilterd.

#### <a name="how-do-i-access-hello-audit-and-security-logs"></a>Hoe krijg ik toegang tot Hallo controle en beveiliging Logboeken?

Hallo logboeken voor controle en beveiliging toegankelijk zijn vanuit Hallo Active Directory-portal op drie verschillende manieren: via Hallo **activiteit** sectie (Selecteer **controlelogboeken** of **aanmeldingen**), of van **gebruikers en groepen** of **bedrijfstoepassingen** onder **beheren** in Active Directory. Rapporten kunnen ook worden geopend via Azure Active Directory Hallo rapportage-API. 

1. Selecteer in de Azure-portal hello, **Azure Active Directory.**

2. In Hallo **activiteit** sectie **controlelogboeken.**

    ![](media/protection-personal-data-azure-reporting-tools/image001.png)

3. Hallo-lijstweergave aanpassen door te klikken op **kolommen** op Hallo-werkbalk.

4.  Selecteer een item in Hallo lijst weergave toosee alle beschikbare details over deze.

    ![](media/protection-personal-data-azure-reporting-tools/image003.png)

Rapportage van Azure Active Directory bevat ook twee soorten beveiligingsrapporten, **gebruikers die zijn gemarkeerd voor risico** en **riskant aanmeldingen**, waarmee u mogelijke risico's in uw Azure-omgeving bewaken.

Zie voor meer informatie over service reporting Hallo [rapportage van Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)

Ga naar [Azure Active Directory-activiteitenrapporten](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal#activity-reports) voor meer details over het Hallo-rapporten die beschikbaar zijn in Azure Active Directory. Deze site bevat meer informatie over het tooaccess en gebruik [auditlogboeken activiteitsrapporten](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) en [aanmeldingsactiviteiten rapporten](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) in Hallo-portal. Dit omvat ook informatie over [gebruikers die zijn gemarkeerd voor risico](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-user-at-risk) en [riskant aanmelden](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-risky-sign-ins) beveiligingsrapporten.

Ga naar Hallo [Azure Active Directory-audit API-verwijzing](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-audit-reference) site voor meer informatie over het tooconnect tooAzure Directory reporting via een programma.

### <a name="log-analytics"></a>Log Analytics

[Meld u Analytics](https://azure.microsoft.com/services/log-analytics/) kunt [verzamelen van gegevens van Azure Monitor](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage) toocorrelate met andere gegevens en bieden aanvullende analyse. Azure Monitor worden verzameld en analyseert bewakingsgegevens voor uw Azure-omgeving. 

Analyseprogramma's in logboekanalyse zoals logboek zoekopdrachten, weergaven en oplossingen werken tegen alle verzamelde gegevens, zonder dat u gecentraliseerde analyse van uw hele omgeving. Log Analytics kunt aggregeren en analyseren van Windows-gebeurtenislogboeken, IIS-logboeken en Syslogs waarmee detecteren van mogelijke overtredingen van persoonlijke gegevens die persoonlijke gegevens toounauthorized gebruikers worden namelijk blootgesteld.

#### <a name="how-do-i-use-log-analytics"></a>Hoe gebruik ik Log Analytics

Log Analytics is toegankelijk via Hallo OMS-portal of hello Azure-portal, via elke webbrowser. Log Analytics omvat een query language tooquickly ophalen en samenvoegen van gegevens in het Hallo-opslagplaats. U kunt maken en opslaan logboek zoekopdrachten toodirectly analyseren in Hallo-portal.

toocreate een werkruimte voor logboekanalyse in hello Azure portal Hallo te volgen:

1. Selecteer **logboekanalyse** uit de lijst Hallo van services in Hallo Marketplace.

2. Selecteer **maken,** Hallo naam opgeven van de OMS-werkruimte, selecteert u uw abonnement, resourcegroep, locatie en prijscategorie.

3. Klik op **OK** toodisplay een lijst met uw werkruimten.

4. Selecteer een werkruimte toosee de details ervan.

    ![](media/protection-personal-data-azure-reporting-tools/image004.png)

Ga naar Hallo [Log Analytics-documentatie](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) toolearn meer over Hallo-service.

Ga naar Hallo [aan de slag met een werkruimte voor logboekanalyse](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started) zelfstudie toocreate een evaluatie-werkruimte en leer Hallo basisbeginselen van hoe toouse Hallo service.

Ga naar Hallo webpagina's voor meer informatie over hoe tooconnect toouse logboekanalyse Hello registreert te volgen die hierboven worden beschreven:

[Gegevensbronnen van de Windows-gebeurtenislogboeken in Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)

[IIS-logboeken in Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs)

[Syslog-gegevensbronnen in Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-syslog)

### <a name="azure-monitorazure-activity-log"></a>Azure Monitor/Azure Activity Log 

[Monitor voor Azure](https://azure.microsoft.com/services/monitor/) basisniveau infrastructuur metrische gegevens en logboeken voor de meeste services in Microsoft Azure biedt.
Controle kunt u toogain grondige inzicht in uw Azure-toepassingen. Monitor voor Azure is afhankelijk van hello Azure extensie voor diagnostische gegevens (Windows of Linux) om de meeste niveau metrische gegevens voor een toepassing en logboeken te verzamelen. [Hello Azure Activity Log](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) is een Hallo-resources kunt u met Azure Monitor weergeven. Het houdt elke API-aanroep, en biedt een schat aan informatie over activiteiten die voorkomen in [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).
U kunt Hallo activiteitenlogboek (eerder operationele of controlelogboeken genoemd) voor meer informatie zoeken over uw resource volgens hello Azure-infrastructuur. 

Hoewel veel van Hallo gegevens vastgelegd in Hallo activiteit logboek tooperformance en service health geldt, is ook informatie die is gerelateerd tooprotection van gegevens. Hallo activiteitenlogboek gebruikt, u kunt bepalen Hallo ' wat, wie, en wanneer ' voor een (PUT, POST, verwijderen schrijfbewerkingen) die zijn gemaakt op Hallo bronnen in uw Azure-abonnement.

Het biedt bijvoorbeeld een record wanneer een beheerder verwijdert een netwerkbeveiligingsgroep dit kan invloed hebben op Hallo bescherming van persoonlijke gegevens. Logboekvermeldingen activiteit worden opgeslagen in Azure Monitor gedurende 90 dagen.

#### <a name="how-do-i-use-hello-data-collected-by-azure-monitor"></a>Hoe gebruik ik Hallo gegevens verzameld door Azure-Monitor

Er zijn een aantal manieren toouse Hallo gegevens in het activiteitenlogboek Hallo en andere bronnen van de Azure-Monitor.

- Hallo gegevenslocaties tooother in echte regel kan worden gestreamd.

- U kunt Hallo gegevens opslaan voor langere tijd dan Hallo standaardinstellingen, met behulp van een [Azure storage-account](https://docs.microsoft.com/azure/storage/common/storage-introduction) en een bewaarbeleid instellen.

- U kunt visual Hallo-gegevens in de afbeeldingen en grafieken, met behulp van Hallo [Azure-portal](https://azure.microsoft.com/features/azure-portal/), [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), [Microsoft PowerBI](https://powerbi.microsoft.com/), of hulpprogramma's van derden visualisatie.

- U kunt een query Hallo-gegevens met behulp van hello Azure Monitor REST API, CLI-opdrachten [PowerShell](https://docs.microsoft.com/powershell/) -cmdlets of Hallo .NET SDK.

Selecteer tooget gestart met Azure-Monitor **meer Services** in hello Azure-portal.

1. Schuif naar beneden te**Monitor** in Hallo **controleren en beheren van** sectie.

    ![](media/protection-personal-data-azure-reporting-tools/image005.png)

2.  Monitor wordt geopend in Hallo **activiteitenlogboek** weergeven.

    ![](media/protection-personal-data-azure-reporting-tools/image007.png)

U kunt maken en query's voor algemene filters vervolgens pincode Hallo belangrijkste query's tooa portaldashboard opslaan zodat u altijd weet als de gebeurtenissen die voldoen aan uw criteria hebben plaatsgevonden.

1. U kunt filteren Hallo weergeven per resourcegroep, timespan en categorie.

    ![](media/protection-personal-data-azure-reporting-tools/image008.png)

2. Vervolgens kunt u query's tooa portaldashboard vastmaken door te klikken op Hallo **pincode** knop. Zo kunt u één bron van informatie voor de operationele gegevens op uw services maken. de querynaam Hallo en aantal resultaten worden weergegeven op Hallo-dashboard.

U kunt ook Hallo Monitor tooview metrische gegevens voor alle Azure-resources gebruiken, configureren van instellingen voor diagnostische gegevens en waarschuwingen en Hallo logboek zoeken. Voor meer informatie over hoe toouse hello Azure Monitor en het activiteitenlogboek, Zie [aan de slag met Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started).

### <a name="azure-diagnostics"></a>Azure Diagnostics 

Hallo diagnosemogelijkheden in Azure kunt verzamelen van gegevens van diverse bronnen. Hallo Windows Logboeken, waaronder het beveiligingslogboek Hallo is vooral handig bij het bijhouden en documenteren van de beveiliging van persoonlijke gegevens. Hallo beveiligingslogboek houdt aanmelding geslaagde en mislukte gebeurtenissen, evenals wijzigingen in machtigingen, detectie van patronen die wijzen op bepaalde typen aanvallen, wijzigingen in de beleidsregels die betrekking hebben op beveiliging, beveiligingswijzigingen voor een groepslidmaatschap en nog veel meer.

Bijvoorbeeld, waarschuwingen gebeurtenis-ID 4695 u toohello geprobeerd unprotection van controleerbaar beveiligde gegevens. Dit heeft betrekking toohello Data Protection API (DPAPI), waarmee tooprotect gegevens zoals persoonlijke sleutels, opgeslagen referenties en andere vertrouwelijke informatie.

#### <a name="how-do-i-enable-hello-diagnostics-extension-for-windows-vms"></a>Hoe kan ik voor virtuele machines van Windows hello-extensie voor diagnostische gegevens inschakelen?

U kunt dus als toocollect logboekgegevens PowerShell tooenable Hallo-extensie voor diagnostische gegevens voor een virtuele machine van Windows gebruiken. Hallo stappen hiertoe afhankelijk zijn van op welk implementatiemodel u (Resource Manager of klassiek) gebruiken. tooenable hello extensie voor diagnostische gegevens op een bestaande virtuele machine die is gemaakt via Hallo Resource Manager-implementatiemodel, kunt u Hallo [Set AzureRMVMDiagnosticsExtension PowerShell-cmdlet](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension?view=azurermps-4.3.1).

   ![](media/protection-personal-data-azure-reporting-tools/image009.png)

*\$diagnosticsconfig_path* Hallo pad toohello-bestand met de configuratie van diagnostische Hallo in XML is. Zie voor meer informatie over het inschakelen van Azure Diagnostics op een virtuele machine, [Gebruik PowerShell tooenable diagnostische Azure-gegevens in een virtuele machine waarop Windows wordt uitgevoerd.](https://docs.microsoft.com/azure/virtual-machines/windows/ps-extensions-diagnostics)

Hello Azure diagnostics uitbreiding kunt zet Hallo verzamelde gegevens tooan Azure storage-account of dit tooservices zoals Application Insights te verzenden. U kunt vervolgens Hallo gegevens gebruiken voor controle.

#### <a name="how-do-i-store-and-view-diagnostic-data"></a>Hoe ik opslaan en weergeven van diagnostische gegevens?

Het is belangrijk tooremember diagnostische gegevens is niet permanent opgeslagen tenzij u deze toohello Microsoft Azure storage emulator of tooAzure opslag overdraagt. toostore en bekijkt u diagnostische gegevens in Azure Storage als volgt te werk:

1. Geef een opslagaccount in Hallo ServiceConfiguration.cscfg-bestand. Azure Diagnostics kunt Hallo Blob-service of Hallo tabel-service, afhankelijk van Hallo type gegevens gebruiken. Windows-gebeurtenislogboeken worden opgeslagen in tabelindeling.

2. Hallo gegevens overbrengen. U kunt tootransfer Hallo diagnostische gegevens via het configuratiebestand Hallo aanvragen. Voor SDK-2.4 en vorige, kunt u Hallo-aanvraag via een programma.

3. Hallo-gegevens, met weergeven [Azure Opslagverkenner](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer), [Server Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) in Visual Studio of [Azure Diagnostics Manager](https://www.cerebrata.com/products/azure-diagnostics-manager) in Azure Management Studio.

Voor meer informatie over het tooperform van de volgende stappen Zie [diagnostische gegevens opslaan en weergeven in Azure Storage.](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)

### <a name="azure-storage-analytics"></a>Azure Storage Analytics 

Storage Analytics registreert gedetailleerde informatie over geslaagde en mislukte aanvragen tooa storage-service. Deze informatie kan worden gebruikt toomonitor afzonderlijke aanvragen, die helpen kunnen bij het toegang toopersonal opgeslagen gegevens in de service Hallo documenteren. Echter is Storage Analytics logboekregistratie niet standaard ingeschakeld voor uw opslagaccount. U kunt ze inschakelen in hello Azure-portal.

#### <a name="how-do-i-configure-monitoring-for-a-storage-account"></a>Hoe configureer bewaking voor een opslagaccount?

tooconfigure bewaking voor een opslagaccount Hallo te volgen:

1. Selecteer **opslagaccounts** in hello Azure-portal, selecteert u Hallo-naam van de gewenste toomonitor Hallo-account.

    ![](media/protection-personal-data-azure-reporting-tools/image011.png)

2. In Hallo **bewaking** sectie **diagnostische gegevens.**

3.  Selecteer Hallo **type** van metrische gegevens gewenste toomonitor voor elke service (Blob, tabel-bestand). tooinstruct Azure Storage toosave diagnostische logboeken voor lezen, schrijven en verwijderen van aanvragen voor Hallo blob, table en queue-services, selecteert u **Blob-Logboeken, tabel logboeken** en **Logboeken in de wachtrij.**

    ![](media/protection-personal-data-azure-reporting-tools/image013.png)

4. Hallo schuifregelaar van Hallo onderin, ingesteld op Hallo **bewaren** beleid in dagen (de waarde van 1 – 365). Zeven dagen is Hallo standaardwaarde.

5. Selecteer **opslaan** tooapply Hallo configuratie-instellingen.

Opslag logboekregistratie logboekvermeldingen bevatten informatie over afzonderlijke aanvragen volgen Hallo:

- Timing gegevens zoals begintijd, end-to-end-latentie en latentie van de server.

- Details van de opslagbewerking Hallo zoals Hallo bewerkingstype sleutel Hallo van Hallo opslag object Hallo-client is toegang tot, geslaagd of mislukt en HTTP-statuscode Hallo toohello client geretourneerd.

- Verificatiegegevens zoals Hallo type verificatie Hallo client gebruikt.

- Gelijktijdigheid informatie zoals Hallo ETag-waarde en tijdstempel het laatst is gewijzigd.

- Hallo-grootte van de aanvraag en -antwoord voor Hallo-berichten.

Voor instructies over het gedetailleerde tooenable Opslaganalyse aan te melden, Zie [bewaken van een opslagaccount in hello Azure-portal.](https://docs.microsoft.com/azure/storage/common/storage-monitor-storage-account)

### <a name="azure-security-center"></a>Azure Security Center 

[Azure Security Center](https://azure.microsoft.com/services/security-center/) monitors Hallo beveiligingsstatus van uw Azure-resources in volgorde tooprevent en bedreigingen te detecteren en aanbevelingen voor reageert. Het biedt verschillende manieren toohelp document uw beveiligingsmaatregelen Hallo privacy van persoonlijke gegevens te beveiligen.

Beveiligingsstatus bewaken, kunt u ervoor zorgen dat aan uw beveiligingsbeleid. Beveiligingsbewaking is een proactieve strategie waarbij uw resources tooidentify systemen die niet voldoen aan de organisatie-standaarden of aanbevolen procedures controles. U kunt bewaken Hallo beveiligingsstatus van Hallo resources te volgen:

- COMPUTE (virtuele machines en cloudservices)

- Netwerken (virtuele netwerken)

- Opslag en gegevens (server en database controle en detectie van bedreigingen, TDE, versleuteling van opslag)

- Toepassingen (mogelijke beveiligingsproblemen)

Beveiligingsproblemen in een van deze categorieën kunnen een bedreiging toohello privacy van persoonlijke gegevens vormen.

#### <a name="how-do-i-view-hello-security-state-of-my-azure-resources"></a>Hoe kan ik de beveiligingsstatus Hallo van mijn Azure-resources bekijken?

Security Center analyseert periodiek Hallo beveiligingsstatus van uw Azure-resources. U kunt alle mogelijke beveiligingsproblemen die het identificeert weergeven in Hallo **preventie** sectie van het Hallo-dashboard.

   ![](media/protection-personal-data-azure-reporting-tools/image014.png)

1. In Hallo **preventie** sectie, selecteer Hallo **Compute** tegel. Ziet u hier een **overzicht** samen met de Hallo **virtuele machines** lijst van alle virtuele machines en hun status beveiliging en Hallo **Cloudservices** lijst met web-en werkrollen bewaakt door Security Center.

2. Op Hallo **overzicht** tabblad, tweede een aanbeveling tooview meer informatie.

3. Op Hallo **virtuele machines** tabblad, selecteert u een VM tooview aanvullende details.

Wanneer gegevensverzameling is ingeschakeld in Azure Security Center, Hallo Microsoft Monitoring Agent automatisch geconfigureerd zijn op alle bestaande en nieuw ondersteunde virtuele machines die zijn geïmplementeerd. Gegevens die worden verzameld van deze agent wordt opgeslagen in een bestaand [logboekanalyse](https://azure.microsoft.com/services/log-analytics/) werkruimte die zijn gekoppeld aan uw abonnement of een nieuwe werkruimte.

[Dreiging Intelligence-rapporten](https://docs.microsoft.com/azure/security-center/security-center-threat-report) worden geleverd door Security Center. Deze bieden u nuttige informatie toohelp onderscheiden van Hallo aanvaller identiteit, doelstellingen, huidige en historische aanval campagnes, en -tactieken, hulpprogramma's en procedures die worden gebruikt. Risicobeperking en het doorvoeren informatie is ook opgenomen.

Hallo primaire doel van deze rapporten bedreiging is toohelp u toorespond effectief toohello onmiddellijke dreiging en help maatregelen treffen daarna toomitigate Hallo probleem. Hallo-gegevens in Hallo rapporten kan ook worden nuttig wanneer u uw beveiligingsplan voor rapportage- en controledoeleinden documenteren.

Hallo Threat Intelligence-rapporten worden vermeld op. PDF-indeling, toegankelijk via een koppeling in Hallo **rapporten** veld Hallo **verdachte proces dat wordt uitgevoerd** blade voor elke beveiligingswaarschuwing in Azure Security Center.

Zie voor meer informatie over hoe tooview en gebruik Hallo Threat Intelligence-rapport, [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)

## <a name="next-steps"></a>Volgende stappen

[Aan de slag met Azure Active Directory-rapportage API Hallo](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started-azure-portal)

[Wat is Log Analytics?](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

[Overzicht van de bewaking in Microsoft Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

[Inleiding toohello Azure Activity Log (video)](https://azure.microsoft.com/resources/videos/intro-activity-log/)
