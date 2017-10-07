---
title: analyse van aaaLog voor Azure CDN | Microsoft Docs
description: De klant kunt logboekanalyse inschakelen voor Azure CDN.
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a>Diagnostische logboeken voor Azure CDN

Nadat de CDN is ingeschakeld voor uw toepassing, wordt u waarschijnlijk wilt toomonitor Hallo CDN gebruik, Controleer de status van uw levering Hallo en mogelijke problemen. Azure CDN biedt deze mogelijkheden met [CDN basisanalyse](cdn-analyze-usage-patterns.md) en [diagnostische logboeken](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)

## <a name="cdn-core-analytics"></a>CDN-basisanalyse
Als een huidige Azure CDN-gebruiker met Verizon standard of premium-profiel bent u al basisanalyse kunnen tooview in Hallo aanvullende portal toegankelijk via 'Beheren' Hallo-optie van hello Azure-portal. 

## <a name="azure-diagnostic-logs"></a>Azure diagnostische logboeken

Azure met deze nieuwe functie, u kunt nu zien basisanalyse en deze opslaan in een of meer bestemmingen, met inbegrip van:

 - Azure-opslagaccount
 - Azure Event Hubs
 - [De opslagplaats OMS Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 Deze functie is beschikbaar voor alle CDN-eindpunten die behoren tooVerizon (Standard en Premium) en CDN-profielen van Akamai (standaard).

Logboeken met diagnostische gegevens kunnen u tooexport basisgebruik metrische gegevens van uw CDN-eindpunt tooa verschillende bronnen, zodat u ze in een aangepaste manier gebruiken kunt. Bijvoorbeeld, u kunt doen Hallo volgende soorten gegevens exporteren:

- Gegevensopslag tooblob exporteren, tooCSV exporteren en grafieken genereren in excel.
- Exporteer gegevens tooevent hubs en correleren met gegevens van andere azure-services.
- Exporteren van gegevens toolog analytics weergave gegevens en in uw eigen OMS-werkruimte

Hallo toont volgende afbeelding een typische basisanalyse CDN-overzicht van gegevens.

![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/01_OMS-workspace.png)

*Afbeelding 1: CDN basisanalyse weergeven*

Hallo volgen stapsgewijze Kennismaking gaat door het Hallo-schema van Hallo core analytische gegevens, stappen voor het Hallo-functie inschakelen en gebruiken van deze bestemmingen leveren van toovarious bestemmingen.

## <a name="enable-logging-with-azure-portal"></a>Inschakelen van logboekregistratie met Azure-portal

> [!NOTE]
> Hallo diagnostische logboeken zijn ingeschakeld **uit** standaard. 

Hallo stappen hieronder tooenable logboekregistratie met CDN basisanalyse:

Meld u aan toohello [Azure-portal](http://portal.azure.com). Als u nog niet ingeschakeld voor uw werkstroom CDN hebt [Azure CDN inschakelen](cdn-create-new-endpoint.md) voordat u doorgaat.

1. Navigeer te in Hallo portal**CDN-profiel**.
2. Selecteer een CDN-profiel en vervolgens Hallo CDN-eindpunt dat u wilt dat tooenable **diagnostische logboeken**.

    ![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. Ga te**diagnostische logboeken** blade onder **bewaking** sectie en klik vervolgens op Hallo status te**op**.

    ![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a>Logboekregistratie met Azure Storage inschakelen
    
Selecteer toouse Azure Storage toostore Hallo logboeken **archiveren tooa storage-account**, selecteer de dagen bewaren en op **CoreAnalytics** onder **logboek**.

![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

*Afbeelding 2 - logboekregistratie met Azure Storage*

### <a name="logging-with-oms-log-analytics"></a>Logboekregistratie met OMS Log Analytics

toouse OMS Log Analytics toostore Hallo Logboeken als volgt te werk:

1. Van Hallo **diagnostische logboeken** blade onder **bewaking**, selecteer **tooLog Analytics verzenden** uit 

    ![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. Hallo logboekanalyse logboekregistratie configureren door te klikken op configureren. Hiermee gaat u tooa dialoogvenster kunt u een vorige werkruimte selecteren of een nieuwe maken.

    ![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. Klik op **Maak nieuwe werkruimte**.

    ![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/07_Create-new.png)

4. Vervolgens moet u een nieuwe naam van de werkruimte, bestaande abonnement, resourcegroep (nieuwe of bestaande), locatie en prijscategorie. U hebt de optie Hallo van dit configuration tooyour dashboard vastmaken. Klik op OK toocomplete Hallo configuratie.

    U ziet naast uw werkruimte met uw namen OMS-werkruimte en de Resource. Namen moeten uniek zijn en gebruiken kunnen alleen letters, cijfers en afbreekstreepjes. Spaties en onderstrepingstekens bevatten, zijn niet toegestaan. 

    ![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. U wordt vervolgens een kort bericht vermeld dat uw werkruimte is gemaakt en u logboekregistratie van het Configuratiescherm tooyour worden geretourneerd. U kunt bevestigen Hallo-naam van de werkruimte voor logboekanalyse.

    ![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    Als u een Hallo logboekanalyse configuratie hebt ingesteld, moet dat u ook selectievakje Hallo CoreAnalytics voor CDN-logboekregistratie.

6. Als alles tooyour eigen smaak, klikt u op Hallo **opslaan** knop Hallo boven aan het dialoogvenster Hallo-configuratie.

    ![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/10_Save-me.png)

    Hallo **opslaan** knop bestaat niet meer actief is en dat Hallo in/uit-knop is nu ingeschakeld, maar blauw in plaats van paars.

7. Als u wilt uw nieuwe OMS-werkruimte toosee, klik Ga tooyour Azure-portal-Dashboard Hallo-naam van de werkruimte voor logboekanalyse. Vervolgens ziet u uw werkruimte (Zorg ervoor dat de OMS-werkruimte is geselecteerd op Hallo links). Klik op Hallo OMS-Portal tegel toosee uw werkruimte in Hallo OMS-opslagplaats. 

    ![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    De OMS-opslagplaats is nu gereed toolog gegevens. In volgorde tooconsume die gegevens, moet u een [OMS oplossing](#consuming-oms-log-analytics-data), gedekte verderop in dit artikel.

Ga voor meer informatie over het logboek gegevens vertragingen [hier](#log-data-delays).

## <a name="enable-logging-with-powershell"></a>Inschakelen van logboekregistratie met PowerShell

Hieronder volgt een voorbeeld van hoe tooenable en get diagnostische logboeken via hello Azure PowerShell-Cmdlets.

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a>Inschakelen van diagnostische logboeken in een Opslagaccount

Meldt u zich eerst en selecteer een abonnement:

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


logboeken met diagnostische gegevens in een Opslagaccount tooEnable Gebruik deze opdracht:

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
tooEnable diagnostische logboeken in een OMS-werkruimte, gebruikt u deze opdracht:

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a>Diagnostische logboeken van Azure Storage gebruiken
Deze sectie beschrijft Hallo-schema van Hallo CDN basisanalyse, hoe deze zijn ingedeeld binnen een Azure Storage-Account en biedt voorbeeld code toodownload Hallo Logboeken in tooa CSV-bestand.

### <a name="using-microsoft-azure-storage-explorer"></a>Met behulp van Microsoft Azure Opslagverkenner
Voordat u Hallo core analytische gegevens vanaf hello Azure Storage-Account openen kunt, moet u eerst een hulpprogramma tooaccess Hallo inhoud in een opslagaccount. Er zijn verschillende hulpprogramma's beschikbaar in de markt Hallo, is Hallo dat het is raadzaam Hallo Microsoft Azure Storage Explorer. U kunt downloaden Hallo hulpprogramma van [hier](http://storageexplorer.com/). Nadat het Hallo-software downloaden en installeren configureert Hallo toouse hetzelfde Azure-Opslagaccount die is geconfigureerd als een bestemming toohello CDN diagnostische logboeken.

1.  Open **Microsoft Azure Opslagverkenner**
2.  Zoek Hallo storage-account
3.  Ga toohello **'Blob-Containers'** knooppunt onder deze opslag account en het Hallo-knooppunt uitvouwen
4.  Selecteer Hallo-container met de naam **'insights-logboeken-coreanalytics'** en dubbelklik erop
5.  Weergeven van resultaten op Hallo rechterdeelvenster beginnen met Hallo eerst niveau, ziet eruit als **' resourceId = "**. Blijf klikken alle Hallo manier totdat er Hallo bestand **PT1H.json**. Zie Hallo Opmerking voor een uitleg van Hallo pad te volgen.
6.  Elke blob **PT1H.json** vertegenwoordigt Hallo analytics logboeken gedurende één uur voor een specifieke CDN-eindpunt of het aangepaste domein.
7.  Hallo-schema van Hallo inhoud van dit JSON-bestand wordt beschreven in Hallo sectie Schema Hallo Core Analytics Logboeken


> [!NOTE]
> **BLOB-padindeling**
> 
> Core Analytics logboeken worden elk uur gegenereerd. Alle gegevens voor een uur zijn verzameld en opgeslagen in één Azure Blob als JSON-nettolading. Hallo pad toothis Azure Blob wordt weergegeven als er een hiërarchische structuur is. Dit is omdat Hallo Storage explorer hulpprogramma interpreteert '/' als een mapscheidingsteken en toont Hallo hiërarchie voor het gemak. Hallo hele pad vertegenwoordigt eigenlijk alleen Hallo blob-naam. Deze naam van de blob Hallo volgt Hallo naamconventie volgen 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

**Beschrijving van velden:**

|waarde|description|
|-------|---------|
|Abonnements-id    |ID van hello Azure-abonnement. Dit is in Hallo Guid-indeling.|
|Resource |Groepsnaam van Hallo resource groep toowhich Hallo CDN resources behoren.|
|Profielnaam |Naam van Hallo CDN-profiel|
|Naam van het eindpunt |Naam van Hallo CDN-eindpunt|
|jaar|  4-cijferige representatie van Hallo jaar bijvoorbeeld 2017|
|Maand| 2 cijfers weergave van Hallo nummer van de maand. 01 januari =... 12 December =|
|Dag|   weergave van de dag van de maand Hallo Hallo 2 cijfers|
|PT1H.JSON| Werkelijke JSON-bestand waarin Hallo analytische gegevens is opgeslagen|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a>Hallo Core analytische gegevens tooa CSV-bestand exporteren

toomake it eenvoudig tooaccess Hallo basisanalyse, bieden we een voorbeeld van code voor een hulpprogramma waarmee Hallo JSON-bestanden downloaden naar een platte door komma's gescheiden bestandsindeling, wat kan gebruikte tooeasily grafieken of andere aggregaties maken.

Dit is hoe u Hallo hulpprogramma kunt gebruiken:

1.  Ga naar Hallo github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )
2.  Hallo code downloaden
3.  Volg de instructies toocompile en configureren
4.  Hallo-hulpprogramma uitvoeren
5.  Resulterende CSV-bestand bevat Hallo analytische gegevens in een eenvoudige platte hiërarchie.

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a>Diagnostische logboeken van een opslagplaats OMS Log Analytics gebruiken
Log Analytics is een service in Operations Management Suite (OMS) die uw cloud en on-premises omgevingen toomaintain de beschikbaarheid en prestaties bewaakt. Gegevens die zijn gegenereerd door de resources in uw cloud en on-premises omgevingen en van andere bewaking extra tooprovide analysis over meerdere bronnen worden verzameld. 

toouse Log Analytics, moet u [logboekregistratie inschakelen](#enable-logging-with-azure-storage) toohello Azure-logboekanalyse OMS-opslagplaats, die eerder in dit artikel wordt besproken.

### <a name="using-hello-oms-repository"></a>Met behulp van Hallo OMS-opslagplaats

 Hallo volgende diagram ziet u Hallo-architectuur van Hallo invoer en uitvoer van Hallo opslagplaats:

![OMS Log Analytics-opslagplaats](./media/cdn-diagnostics-log/12_Repo-overview.png)

*Afbeelding 3 - Log Analytics-opslagplaats*

U kunt Hallo gegevens op verschillende manieren weergeven met behulp van oplossingen voor het beheer. U kunt beheeroplossingen verkrijgen van Hallo [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).

U kunt beheeroplossingen vanuit Azure marketplace installeren door te klikken op Hallo **nu downloaden** koppeling onderin Hallo van elke oplossing.

### <a name="adding-an-oms-cdn-management-solution"></a>Toevoegen van een oplossing voor het beheer van OMS CDN

Volg deze stappen tooadd een oplossing voor:

1.   Als u dit nog niet hebt gedaan, toohello aanmelden met Azure portal met behulp van uw Azure-abonnement en ga tooyour Dashboard.
    ![Azure-Dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)

2. In Hallo **nieuw** blade onder **Marketplace**, selecteer **bewaking + management**.

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. In Hallo **bewaking + management** blade, klikt u op **alle**.

    ![Alles bekijken](./media/cdn-diagnostics-log/15_See-all.png)

4.  Zoeken naar de CDN in het zoekvak Hallo.

    ![Alles bekijken](./media/cdn-diagnostics-log/16_Search-for.png)

5.  Selecteer **Azure CDN basisanalyse**. 

    ![Alles bekijken](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  Wanneer u op **maken**, kunt u zich toocreate gevraagd een nieuwe OMS-werkruimte of gebruik een bestaande. 

    ![Alles bekijken](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  Hallo-werkruimte die u hebt gemaakt voordat selecteren. Vervolgens moet u tooadd een automation-account.

    ![Alles bekijken](./media/cdn-diagnostics-log/19_Add-automation.png)

8. Hallo ziet volgende scherm Hallo automation-accountformulier die moet invullen. 

    ![Alles bekijken](./media/cdn-diagnostics-log/20_Automation.png)

9. Nadat u Hallo automation-account hebt gemaakt, u bent klaar tooadd uw oplossing. Klik op Hallo **maken** knop.

    ![Alles bekijken](./media/cdn-diagnostics-log/21_Ready.png)

10. Uw oplossing is nu tooyour werkruimte toegevoegd. Ga terug tooyour Azure-portal Dashboard.

    ![Alles bekijken](./media/cdn-diagnostics-log/22_Dashboard.png)

    Klik op de werkruimte voor logboekanalyse Hallo u toogo tooyour werkruimte gemaakt. 

11. Klik op Hallo **OMS-Portal** tegel toosee uw nieuwe oplossing in Hallo OMS-portal.

    ![Alles bekijken](./media/cdn-diagnostics-log/23_workspace.png)

12. De OMS-portal ziet er nu als Hallo scherm te volgen:

    ![Alles bekijken](./media/cdn-diagnostics-log/24_OMS-solution.png)

    Klik op een van de Hallo tegels toosee verschillende weergaven in uw gegevens.

    ![Alles bekijken](./media/cdn-diagnostics-log/25_Interior-view.png)

    Kunt u zelf schuiven links of rechts toosee meer tegels die afzonderlijke weergaven in Hallo-gegevens. 

    Op een Hallo tegels te klikken, kunt u meer informatie over uw gegevens.

     ![Alles bekijken](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a>Aanbiedingen en Prijscategorieën

U kunt zien aanbiedingen en Prijscategorieën voor OMS-beheeroplossingen voor [hier](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).

### <a name="customizing-views"></a>Weergaven aanpassen

U kunt Hallo weergave aanpassen in uw gegevens met behulp van Hallo **ontwerper**. Ga tooyour OMS-werkruimte en ontwerpen beginnen door te klikken op Hallo **ontwerper** tegel.

![Designer weergeven](./media/cdn-diagnostics-log/27_Designer.png)

U kunt slepen en neerzetten grafiektypen van Hallo links en vul in Hallo Gegevensdetails tooanalyze op Hallo van links gewenste.

![Designer weergeven](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a>Logboek gegevens vertragingen

Verizon logboek gegevens vertragingen | Akamai logboek gegevens vertragingen
--- | ---
Logboekgegevens van Verizon is 1 uur vertraging en een too2 uren toostart verschijnen na voltooiing van de endpoint-doorgifte in beslag nemen. | Logboekgegevens Akamai is 24 uur vertraging en too2 uren toostart verschijnen als deze meer dan 24 uur geleden is gemaakt in beslag neemt. Als u onlangs is gemaakt, kan het Hallo logboeken toostart verschijnen too25 uur duren.

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a>Diagnostische logboeken typen voor CDN-basisanalyse

Momenteel bieden we alleen basisanalyse logboeken met HTTP-antwoord statistieken en uitgaande gezien vanaf Hallo CDN POP's / randen metrische gegevens bevatten.

### <a name="core-analytics-metrics-details"></a>Core Analytics metrische gegevens
Hallo volgende tabel bevat een overzicht van metrische gegevens beschikbaar zijn in Hallo die basisanalyse registreert. Niet alle metrische gegevens zijn beschikbaar in alle providers, hoewel deze verschillen minimaal zijn. Hallo ook volgende van de tabel wordt aangegeven als een metriek beschikbaar van een provider. Houd er rekening mee dat Hallo metrische gegevens beschikbaar zijn voor de CDN-eindpunten die verkeer op deze hebben.


|Gegevens                     | Beschrijving   | Verizon  | Akamai 
|---------------------------|---------------|---|---|
| RequestCountTotal         |Totaal aantal treffers aanvraag tijdens deze periode| Ja  |Ja   |
| RequestCountHttpStatus2xx |Telling van alle aanvragen dat heeft geresulteerd in een 2xx HTTP-code (bijvoorbeeld 200, 202)              | Ja  |Ja   |
| RequestCountHttpStatus3xx | Telling van alle aanvragen dat heeft geresulteerd in een 3xx HTTP-code (bijvoorbeeld 300, 302)              | Ja  |Ja   |
| RequestCountHttpStatus4xx |Telling van alle aanvragen dat heeft geresulteerd in een 4xx HTTP-code (bijvoorbeeld 400, 404)               | Ja   |Ja   |
| RequestCountHttpStatus5xx | Telling van alle aanvragen dat heeft geresulteerd in een 5xx HTTP-code (bijvoorbeeld 500, 504)              | Ja  |Ja   |
| RequestCountHttpStatusOthers |  Telling van alle andere HTTP-codes (buiten 2xx-5xx) | Ja  |Ja   |
| RequestCountHttpStatus200 | Telling van alle aanvragen dat heeft geresulteerd in een HTTP-antwoord voor 200 code              |Nee   |Ja   |
| RequestCountHttpStatus206 | Telling van alle aanvragen dat heeft geresulteerd in een HTTP-antwoord voor 206 code              |Nee   |Ja   |
| RequestCountHttpStatus302 | Telling van alle aanvragen dat heeft geresulteerd in een HTTP-antwoord voor 302 code              |Nee   |Ja   |
| RequestCountHttpStatus304 |  Telling van alle aanvragen dat heeft geresulteerd in een HTTP-antwoord voor 304 code             |Nee   |Ja   |
| RequestCountHttpStatus404 | Telling van alle aanvragen dat heeft geresulteerd in een 404 HTTP-code-antwoord              |Nee   |Ja   |
| RequestCountCacheHit |Telling van alle aanvragen dat heeft geresulteerd in een treffers in de Cache. Dit betekent dat Hallo asset rechtstreeks vanuit Hallo POP toohello Client in behandeling is genomen.               | Ja  |Nee   |
| RequestCountCacheMiss | Telling van alle aanvragen dat heeft geresulteerd in een Cache ontbreekt. Dit betekent Hallo asset is niet gevonden op Hallo POP dichtstbijzijnde toohello client en daarom is opgehaald uit de Hallo oorsprong.              |Ja   | Nee  |
| RequestCountCacheNoCache | Telling van alle aanvragen tooan asset die niet worden opgeslagen vanwege de Gebruikersconfiguratie tooa op Hallo rand.              |Ja   | Nee  |
| RequestCountCacheUncacheable | Telling van alle tooassets die niet worden opgeslagen door Hallo asset van Cache-Control-aanvragen en -headers die aangeven dat deze mag niet worden opgeslagen op een pop-server of door Hallo HTTP-client is verlopen                |Ja   |Nee   |
| RequestCountCacheOthers | Telling van alle aanvragen met de status van de cache niet wordt gedekt door hierboven.              |Ja   | Nee  |
| EgressTotal | Uitgaande gegevensoverdracht in GB              |Ja   |Ja   |
| EgressHttpStatus2xx | Uitgaande gegevens overdracht * voor antwoorden met 2xx HTTP-statuscodes in GB            |Ja   |Nee   |
| EgressHttpStatus3xx | Uitgaande gegevensoverdracht voor antwoorden met 3xx HTTP-statuscodes in GB              |Ja   |Nee   |
| EgressHttpStatus4xx | Uitgaande gegevensoverdracht voor antwoorden met 4xx HTTP-statuscodes in GB               |Ja   | Nee  |
| EgressHttpStatus5xx | Uitgaande gegevensoverdracht voor antwoorden met 5xx HTTP-statuscodes in GB               |Ja   |  Nee |
| EgressHttpStatusOthers | Uitgaande gegevensoverdracht voor antwoorden met andere HTTP-statuscodes in GB                |Ja   |Nee   |
| EgressCacheHit |  Uitgaande gegevensoverdracht voor antwoorden die zijn geleverd direct van Hallo CDN cache op Hallo CDN POP's / randen  |Ja   |  Nee |
| EgressCacheMiss | Uitgaande gegevensoverdracht voor reacties waarbij zijn niet gevonden op Hallo dichtstbijzijnde POP-server en opgehaald uit de bronserver Hallo              |Ja   |  Nee |
| EgressCacheNoCache | Uitgaande gegevensoverdracht voor bedrijfsmiddelen die niet worden opgeslagen vanwege de Gebruikersconfiguratie tooa op Hallo rand.                |Ja   |Nee   |
| EgressCacheUncacheable | Uitgaande gegevensoverdracht voor bedrijfsmiddelen die niet worden opgeslagen door Hallo asset van Cache-Control en/of Expires-koppen die aangeven dat deze mag niet worden opgeslagen op een pop-server of door Hallo HTTP-client                    |Ja   | Nee  |
| EgressCacheOthers |  Uitgaande gegevensoverdracht voor andere scenario's met cache.             |Ja   | Nee  |

* Uitgaande gegevensoverdracht verwijst tootraffic van CDN pop-locatie servers toohello client geleverd.


### <a name="schema-of-hello-core-analytics-logs"></a>Schema van Hallo Core Analytics Logboeken 

Alle logboeken worden opgeslagen in de JSON-indeling en elk item heeft tekenreeksvelden Hallo hieronder schema te volgen:

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

Waar vertegenwoordigt tijd' Hallo' hello begintijd van Hallo uur grens waarvoor Hallo statistieken is gemeld. Wanneer een waarde niet wordt ondersteund door een CDN-provider in plaats van een dubbel of integer-waarde, zal er een null-waarde. Deze null-waarde duidt Hallo afwezigheid van een metriek en deze verschilt van de waarde 0. Rekening mee dat er een set met deze metrische gegevens per domein geconfigureerd op Hallo-eindpunt worden.

Van de Voorbeeldeigenschappen van onderstaande:

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a>Aanvullende bronnen

* [Azure diagnostische logboeken](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [Basisanalyse via de aanvullende portal Azure CDN](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [OMS Azure Log Analytics](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [Azure-logboekanalyse REST-API](https://docs.microsoft.com/en-us/rest/api/loganalytics)







