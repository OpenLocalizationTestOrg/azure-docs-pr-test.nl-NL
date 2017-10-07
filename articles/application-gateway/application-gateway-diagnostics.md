---
title: aaaMonitor toegang tot logboeken, Prestatielogboeken, back-end-status en metrische gegevens voor de toepassingsgateway | Microsoft Docs
description: Meer informatie over hoe tooenable en beheren van toegang en Prestatielogboeken voor Application Gateway
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: 36ebf15c28f776158350ef8e73d617ef68e09266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a>Back-end-status, diagnostische logboeken en metrische gegevens voor Application Gateway

U kunt de bronnen in de volgende manieren Hallo bewaken met behulp van Azure Application Gateway:

* [Status van de back-end](#back-end-health): Application Gateway biedt Hallo mogelijkheid toomonitor Hallo status van servers in Hallo Hallo back-end-adresgroepen via hello Azure-portal en via PowerShell. U vindt ook Hallo status van de back-end-adresgroepen Hallo via Hallo prestaties diagnostische logboeken.

* [Logboeken](#diagnostic-logs): Logboeken toestaan voor toegang, prestaties en andere gegevens toobe opgeslagen of gebruikt van een resource voor controledoeleinden.

* [Metrische gegevens](#metrics): Application Gateway is momenteel een waarde. Met deze metriek meet Hallo doorvoer van de toepassingsgateway Hallo in bytes per seconde.

## <a name="back-end-health"></a>Back-end-status

Toepassingsgateway biedt Hallo mogelijkheid toomonitor Hallo status van afzonderlijke onderdelen van de back-end-adresgroepen Hallo via Hallo-portal, PowerShell en Hallo-opdrachtregelinterface (CLI). U kunt ook een geaggregeerde status vinden samenvatting van back-end-adresgroepen via Hallo prestaties diagnostische logboeken. 

back-end-statusrapport Hallo weerspiegelt Hallo-uitvoer van Hallo Application Gateway health test toohello back-end-exemplaren. Als scannen is voltooid en Hallo terug end kan verkeer ontvangen, als in orde wordt beschouwd. Anders wordt deze orde beschouwd.

> [!IMPORTANT]
> Als er een netwerkbeveiligingsgroep (NSG) op een Application Gateway-subnet, opent u poortbereiken 65503 65534 op Hallo Application Gateway-subnet voor binnenkomend verkeer. Deze poorten zijn vereist voor Hallo back-end health API toowork.


### <a name="view-back-end-health-through-hello-portal"></a>Status van de back-end via de portal Hallo weergeven

In de portal Hallo back-end health automatisch opgegeven. Selecteer in een bestaande toepassingsgateway **bewaking** > **back-end health**. 

Elk lid in Hallo back-endpool wordt vermeld op deze pagina (of het is een NIC, IP of FQDN). De naam van de back-endpool, poort, HTTP-instellingen voor de naam van back-end en gezondheidsstatus worden weergegeven. Geldige waarden voor gezondheidsstatus zijn **goed**, **niet in orde**, en **onbekende**.

> [!NOTE]
> Als er een back-end-gezondheidsstatus van **onbekende**, zorg ervoor dat toegang toohello back-end niet wordt geblokkeerd door een regel voor het NSG, een door de gebruiker opgegeven routes (UDR) of een aangepaste DNS-server in het virtuele netwerk Hallo.

![Back-end-status][10]

### <a name="view-back-end-health-through-powershell"></a>Status van de back-end via PowerShell weergeven

Hallo volgende PowerShell-code toont hoe tooview back-end health met behulp van Hallo `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a>Status van de back-end via Azure CLI 2.0 weergeven

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a>Resultaten

Hallo volgende fragment toont een voorbeeld van antwoord Hallo:

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <a name="diagnostic-logging"></a>Diagnostische logboeken

U kunt verschillende typen Logboeken gebruiken in Azure toomanage en toepassingsgateways oplossen. U kunt toegang tot sommige van deze logboeken via Hallo-portal. Alle logboeken kunnen worden opgehaald uit Azure Blob storage en weergegeven in de verschillende hulpprogramma's, zoals [logboekanalyse](../log-analytics/log-analytics-azure-networking-analytics.md), Excel en Power BI. U kunt meer informatie over Hallo verschillende typen logboeken van Hallo volgende lijst:

* **Activiteitenlogboek**: U kunt [Azure activiteitenlogboeken](../monitoring-and-diagnostics/insights-debugging-with-events.md) (voorheen bekend als operationele logboeken en controlelogboeken) tooview alle bewerkingen die zijn ingediend tooyour Azure-abonnement en hun status. Logboekvermeldingen activiteit worden standaard verzameld en u kunt ze weergeven in hello Azure-portal.
* **Toegangslogboek**: U kunt gebruikmaken van deze patronen logboek tooview Application Gateway toegang en belangrijke informatie, inclusief Hallo aanroeper IP aangevraagde URL, antwoord latentie, retourcode en bytes in en uit analyseren. Een toegangslogboek verzameld om de 300 seconden. Dit logboek bevat één record per exemplaar van de toepassingsgateway. Hallo Application Gateway-exemplaar kan worden geïdentificeerd door de eigenschap instanceId Hallo.
* **Prestatielogboek**: U kunt dit logboek tooview hoe Application Gateway-exemplaren uitvoert. Dit logboek bevat informatie over de prestaties voor elk exemplaar, met inbegrip van totaal aantal aanvragen die worden geleverd, doorvoer in bytes, totaal aantal aanvragen dat wordt geleverd, aantal mislukte aanvragen en in orde en slecht backend-exemplaren. Een prestatielogboek worden verzameld om de 60 seconden.
* **Firewall-logboek**: U kunt dit logboek tooview Hallo aanvragen die zijn geregistreerd via de modus voor detectie of ter voorkoming van een toepassingsgateway die is geconfigureerd met Hallo web application firewall.

> [!NOTE]
> Logboeken zijn alleen beschikbaar voor resources geïmplementeerd in hello Azure Resource Manager-implementatiemodel. U kunt Logboeken niet gebruiken voor bronnen in het klassieke implementatiemodel Hallo. Zie voor een beter begrip van Hallo twee modellen, Hallo [Understanding Resource Manager-implementatie en klassieke implementatie](../azure-resource-manager/resource-manager-deployment-model.md) artikel.

Hebt u drie opties voor het opslaan van uw logboeken:

* **Storage-account**: Storage-accounts beste kunnen worden gebruikt voor Logboeken wanneer logboeken worden opgeslagen voor een langere duur en gelezen wanneer deze nodig is.
* **Event hubs**: Event hubs zijn een goede optie voor het integreren met andere informatie over beveiliging en beheer van gebeurtenissen (SEIM) hulpprogramma's tooget waarschuwingen op uw resources.
* **Meld u Analytics**: Log Analytics is het meest geschikt voor algemene realtime-controle van uw toepassing of trends kijken.

### <a name="enable-logging-through-powershell"></a>Schakel logboekregistratie in via PowerShell

Activiteit-logboekregistratie is standaard ingeschakeld voor elke Resource Manager-resource. U moet toegang en prestaties logboekregistratie toostart Hallo gegevens beschikbaar zijn via deze logboeken verzamelt inschakelen. tooenable logboekregistratie van gebruik Hallo stappen te volgen:

1. Houd er rekening mee uw storage-account resource-ID, waar Hallo logboekgegevens worden opgeslagen. Deze waarde is van het formulier Hallo: /subscriptions/\<subscriptionId\>/resourceGroups/\<Resourcegroepnaam\>/providers/Microsoft.Storage/storageAccounts/\<opslagaccountnaam\>. U kunt opslagaccount gebruiken in uw abonnement. U kunt deze informatie hello Azure portal toofind.

    ![Portal: resource-ID voor het opslagaccount](./media/application-gateway-diagnostics/diagnostics1.png)

2. Houd er rekening mee resource-ID van de toepassingsgateway van uw waarvoor logboekregistratie is ingeschakeld. Deze waarde is van het formulier Hallo: /subscriptions/\<subscriptionId\>/resourceGroups/\<Resourcegroepnaam\>/providers/Microsoft.Network/applicationGateways/\<toepassingsgateway naam\>. U kunt deze informatie Hallo portal toofind.

    ![Portal: resource-ID voor de toepassingsgateway](./media/application-gateway-diagnostics/diagnostics2.png)

3. Diagnostische logboekregistratie inschakelen met behulp van de volgende PowerShell-cmdlet Hallo:

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
>Activiteitenlogboeken vereisen een afzonderlijke opslagaccount niet. Hallo gebruik van opslag voor toegang en prestatieregistratie leidt ertoe dat de kosten.

### <a name="enable-logging-through-hello-azure-portal"></a>Inschakelen van logboekregistratie via hello Azure-portal

1. In hello Azure-portal, zoek de bron en klik op **diagnostische logboeken**.

   Er zijn drie logboeken beschikbaar voor Application Gateway:

   * Toegangslogboek
   * Prestatielogboek
   * Firewall-logboek

2. toostart verzamelen van gegevens, klikt u op **diagnostische gegevens inschakelen**.

   ![Diagnostische gegevens inschakelen][1]

3. Hallo **diagnostische instellingen** blade biedt Hallo-instellingen voor Hallo diagnostische logboeken. In dit voorbeeld Slaat logboekanalyse Hallo Logboeken. Klik op **configureren** onder **logboekanalyse** tooconfigure uw werkruimte. U kunt ook event hubs en een storage account toosave Hallo diagnostische logboeken.

   ![Hallo configuratieproces wordt gestart][2]

4. Kies een bestaande werkruimte van Operations Management Suite (OMS) of een nieuwe maken. In dit voorbeeld wordt een bestaande.

   ![Opties voor OMS werkruimten][3]

5. Hallo-instellingen bevestigen en klikt u op **opslaan**.

   ![Diagnostische instellingenblade met selecties][4]

### <a name="activity-log"></a>Activiteitenlogboek

Activiteitenlogboek hello Azure genereert standaard. Hallo-logboeken worden bewaard gedurende 90 dagen in hello Azure gebeurtenislogboeken store. Meer informatie over deze logboeken door te lezen Hallo [weergeven van gebeurtenissen en het activiteitenlogboek](../monitoring-and-diagnostics/insights-debugging-with-events.md) artikel.

### <a name="access-log"></a>Toegangslogboek

Hallo toegangslogboek is gegenereerd, alleen als u deze op elk exemplaar van de toepassingsgateway, zoals beschreven in de vorige stappen Hallo hebt ingeschakeld. Hallo-gegevens worden opgeslagen in Hallo storage-account die u hebt opgegeven dat wanneer u Hallo-logboekregistratie is ingeschakeld. Elke toegang van Application Gateway wordt geregistreerd in JSON-indeling, zoals wordt weergegeven in het volgende voorbeeld Hallo:


|Waarde  |Beschrijving  |
|---------|---------|
|Exemplaar-id     | Toepassingsgateway die aanvraag aangeboden Hallo-exemplaar.        |
|client-IP     | Oorspronkelijke IP-adres voor Hallo-aanvraag.        |
|enterpriseclient     | Oorspronkelijke poort voor het Hallo-aanvraag.       |
|HttpMethod     | HTTP-methode die wordt gebruikt door het Hallo-aanvraag.       |
|requestUri     | URI van Hallo-aanvraag ontvangen.        |
|RequestQuery     | **Server-gerouteerd**: Back-end-pool-exemplaar dat Hallo-aanvraag is verzonden. </br> **X-AzureApplicationGateway-logboek-ID**: correlatie-ID Hallo aanvraag gebruikt. Het kan gebruikte tootroubleshoot verkeer problemen op Hallo back-endservers zijn. </br>**STATUS van de SERVER**: HTTP-antwoordcode Application Gateway van Hallo back-end ontvangen.       |
|UserAgent     | De gebruikersagent van Hallo HTTP-aanvraag-header.        |
|httpStatus     | HTTP-statuscode geretourneerd toohello client Application Gateway.       |
|Httpversie     | HTTP-versie van Hallo-aanvraag.        |
|ReceivedBytes     | Grootte van het pakket ontvangen in bytes.        |
|SentBytes| Grootte van het pakket dat is verzonden, in bytes.|
|timeTaken| Totale tijdsduur (in milliseconden) die het duurt voordat een aanvraag toobe verwerkt en de antwoord-toobe verzonden. Dit wordt berekend als hello-interval van Hallo tijd wanneer de toepassingsgateway Hallo eerste byte van een HTTP-aanvraag toohello tijd wanneer de bewerking is voltooid voor het verzenden van antwoord Hallo ontvangt. Het is belangrijk toonote die meestal tijd veld Hallo Hallo tijd Hallo-aanvraag en antwoord-pakketten worden overgebracht via Hallo netwerk bevat. |
|sslEnabled| Hiermee wordt aangegeven of communicatie toohello back-end-adresgroepen SSL gebruikt. Geldige waarden zijn in- of uitschakelen.|
```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2017-04-26T19:27:38Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId": "ApplicationGatewayRole_IN_0",
        "clientIP": "191.96.249.97",
        "clientPort": 46886,
        "httpMethod": "GET",
        "requestUri": "/phpmyadmin/scripts/setup.php",
        "requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=874f1f0f-6807-41c9-b7bc-f3cfa74aa0b1&SERVER-STATUS=404",
        "userAgent": "-",
        "httpStatus": 404,
        "httpVersion": "HTTP/1.0",
        "receivedBytes": 65,
        "sentBytes": 553,
        "timeTaken": 205,
        "sslEnabled": "off"
    }
}
```

### <a name="performance-log"></a>Prestatielogboek

Hallo prestatielogboek wordt alleen gegenereerd als u deze hebt ingeschakeld op elk exemplaar van de toepassingsgateway, zoals beschreven in de vorige stappen Hallo. Hallo-gegevens worden opgeslagen in Hallo storage-account die u hebt opgegeven dat wanneer u Hallo-logboekregistratie is ingeschakeld. Hallo prestatielogboekgegevens wordt gegenereerd met intervallen van 1 minuut. Hallo volgt gegevens worden geregistreerd:


|Waarde  |Beschrijving  |
|---------|---------|
|Exemplaar-id     |  Application Gateway-exemplaren waarvoor gegevens wordt gegenereerd. Er is een rij per exemplaar voor een toepassingsgateway met meerdere-exemplaar.        |
|healthyHostCount     | Het aantal orde hosts in Hallo back-endpool.        |
|unHealthyHostCount     | Het aantal beschadigde hosts in Hallo back-endpool.        |
|requestCount     | Het aantal geleverde aanvragen.        |
|Latentie | Latentie (in milliseconden) van aanvragen van Hallo exemplaar toohello back-end die Hallo aanvragen fungeert. |
|failedRequestCount| Het aantal mislukte aanvragen.|
|Doorvoer| Gemiddelde doorvoersnelheid sinds de laatste logboek hello, gemeten in bytes per seconde.|

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> Latentie wordt berekend door Hallo tijd wanneer de eerste byte Hallo van Hallo HTTP-aanvraag is ontvangen toohello tijd wanneer de laatste byte Hallo Hallo HTTP-antwoord wordt verzonden. De Hallo som van de toepassingsgateway verwerkingstijd Hallo plus hello netwerk kosten toohello terug beëindigen, plus Hallo hoelang back-end vergt tooprocess Hallo aanvraag Hallo.

### <a name="firewall-log"></a>Firewall-logboek

Hallo firewall-logboek is gegenereerd alleen als u deze hebt ingeschakeld voor elke application gateway, zoals beschreven in de vorige stappen Hallo. Dit logboek is ook vereist dat deze Hallo web application firewall op een application gateway is geconfigureerd. Hallo-gegevens worden opgeslagen in Hallo storage-account die u hebt opgegeven dat wanneer u Hallo-logboekregistratie is ingeschakeld. Hallo volgt gegevens worden geregistreerd:


|Waarde  |Beschrijving  |
|---------|---------|
|Exemplaar-id     | Gateway toepassingsexemplaar voor welke firewall worden gegevens gegenereerd. Er is een rij per exemplaar voor een toepassingsgateway met meerdere-exemplaar.         |
|client-IP     |   Oorspronkelijke IP-adres voor Hallo-aanvraag.      |
|enterpriseclient     |  Oorspronkelijke poort voor het Hallo-aanvraag.       |
|requestUri     | URL van het Hallo-aanvraag ontvangen.       |
|ruleSetType     | Type van de regelset. Hallo beschikbare waarde is OWASP.        |
|ruleSetVersion     | Regelset versie die wordt gebruikt. Beschikbare waarden zijn 2.2.9 en 3.0.     |
|ruleId     | Regel-ID van Hallo gebeurtenis.        |
|Bericht     | Gebruiksvriendelijke bericht voor Hallo gebeurtenis. Meer informatie vindt u in de sectie details Hallo.        |
|Actie     |  Actie op die op het Hallo-aanvraag. Beschikbare waarden zijn geblokkeerd en toegestaan.      |
|Site     | De site voor welke Hallo logboek is gegenereerd. Alleen globale wordt momenteel, omdat er regels zijn globale vermeld.|
|Meer informatie     | Details van gebeurtenis Hallo.        |
|Details.Message     | Beschrijving van regel Hallo.        |
|Details.Data     | Specifieke gegevens gevonden in de aanvraag die overeenkomende Hallo-regel.         |
|Details.File     | Configuratiebestand die Hallo regel opgenomen.        |
|Details.line     | Regelnummer in Hallo-configuratiebestand dat Hallo-gebeurtenis.       |

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

### <a name="view-and-analyze-hello-activity-log"></a>Weergeven en analyseren van Hallo activiteitenlogboek

U kunt weergeven en analyseren van logboekgegevens van de activiteit met behulp van de volgende methoden Hallo:

* **Azure-hulpprogramma's**: gegevens ophalen uit Hallo activiteitenlogboek via Azure PowerShell, Hallo Hallo REST-API van Azure, Azure CLI of hello Azure-portal. Stapsgewijze instructies voor elke methode zijn aangegeven in Hallo [activiteit bewerkingen met Resource Manager](../azure-resource-manager/resource-group-audit.md) artikel.
* **Power BI**: als u nog geen hebt een [Power BI](https://powerbi.microsoft.com/pricing) account, kunt u proberen deze gratis. Met behulp van Hallo [activiteitenlogboeken Azure pack voor Power BI inhoud](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), u kunt uw gegevens analyseren met vooraf geconfigureerde dashboards die u gebruiken kunt of aanpassen.

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a>Weergeven en analyseren Hallo toegang, prestaties en firewall-Logboeken

Azure [logboekanalyse](../log-analytics/log-analytics-azure-networking-analytics.md) Hallo teller en de gebeurtenislogboek bestanden kan verzamelen van uw Blob storage-account. Het bevat visualisaties en krachtige zoekopdrachten mogelijkheden tooanalyze uw Logboeken.

U kunt ook verbinding maken met tooyour storage-account en ophalen van Hallo JSON logboekvermeldingen voor toegang en prestaties van Logboeken. Nadat u Hallo JSON-bestanden hebt gedownload, kunt u deze tooCSV converteren en ze weergeven in Excel, Power BI of een ander hulpprogramma voor de weergave van gegevens.

> [!TIP]
> Als u bekend met Visual Studio en de basisconcepten bent van het wijzigen van waarden voor de constanten en variabelen in C#, kunt u Hallo [Meld converter extra](https://github.com/Azure-Samples/networking-dotnet-log-converter) beschikbaar is via GitHub.
> 
> 

## <a name="metrics"></a>Metrische gegevens

Metrische gegevens zijn een functie voor bepaalde waar u prestatiemeteritems in de portal hello bekijken kunt Azure-resources. Voor Application Gateway is een waarde nu beschikbaar. Met deze metriek wordt de doorvoer en kunt u deze bekijken in Hallo-portal. Toepassingsgateway tooan bladeren en klik op **metrische gegevens**. tooview hello waarden, selecteer doorvoer in Hallo **beschikbare metrische gegevens** sectie. In Hallo installatiekopie te volgen, kunt u een voorbeeld met Hallo filters waarmee u toodisplay Hallo gegevens in andere bereiken kunt bekijken.

![Metrische weergave met filters][5]

toosee een actuele lijst met metrische gegevens, Zie [ondersteund met een Azure-Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).

### <a name="alert-rules"></a>Regels voor waarschuwingen

U kunt regels voor waarschuwingen op basis van de metrische gegevens voor een bron op te starten. Bijvoorbeeld, een waarschuwing een webhook aanroepen of e-beheerder als het Hallo-doorvoer van toepassingsgateway Hallo boven, onder of met een drempelwaarde voor een opgegeven periode is.

Hallo volgende voorbeeld wordt u begeleid bij een waarschuwingsregel die beheerder tooan e-mailbericht na schendingen van doorvoer een drempelwaarde verzendt:

1. Klik op **metrische waarschuwing toevoegen** tooopen hello **regel toevoegen** blade. U kunt ook deze blade Hallo metrische gegevens blade bereiken.

   ![Knop 'Metrische waarschuwing toevoegen'][6]

2. Op Hallo **regel toevoegen** blade invullen Hallo-naam, voorwaarde en secties melden en op **OK**.

   * In Hallo **voorwaarde** selector, selecteert u een van de Hallo vier waarden: **groter is dan**, **groter dan of gelijk**, **minder dan**, of  **Kleiner dan of gelijk zijn aan**.

   * In Hallo **periode** selector, selecteer een periode van 5 minuten too6 uur.

   * Als u selecteert **e-eigenaren, bijdragers en lezers**, Hallo e-mail zijn dynamische op basis van het Hallo-gebruikers die toegang toothat bron hebben. Anders kunt u een door komma's gescheiden lijst met gebruikers in Hallo opgeven **aanvullende beheerder email(s)** vak.

   ![Blade regel toevoegen][7]

Als Hallo drempelwaarde wordt overschreden, ontvangt een e-mailbericht is vergelijkbaar toohello in Hallo installatiekopie te volgen:

![E-mailadres voor geschonden drempelwaarde][8]

Een lijst met waarschuwingen wordt weergegeven nadat u een waarschuwing voor een metriek maken. Deze biedt een overzicht van alle Hallo waarschuwingsregels.

![Lijst met waarschuwingen en regels][9]

toolearn meer informatie over waarschuwingsmeldingen, Zie [meldingen van waarschuwingen ontvangen](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

toounderstand meer informatie over webhooks en hoe u ze kunt gebruiken met waarschuwingen, gaat u naar [een webhook configureren op een Azure metrische waarschuwing](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

## <a name="next-steps"></a>Volgende stappen

* Teller en de gebeurtenislogboeken visualiseren met behulp van [logboekanalyse](../log-analytics/log-analytics-azure-networking-analytics.md).
* [Uw Azure activiteitenlogboek met Power BI visualiseren](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blogbericht.
* [Weergeven en analyseren van Azure activiteitenlogboeken in Power BI en meer](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blogbericht.

[1]: ./media/application-gateway-diagnostics/figure1.png
[2]: ./media/application-gateway-diagnostics/figure2.png
[3]: ./media/application-gateway-diagnostics/figure3.png
[4]: ./media/application-gateway-diagnostics/figure4.png
[5]: ./media/application-gateway-diagnostics/figure5.png
[6]: ./media/application-gateway-diagnostics/figure6.png
[7]: ./media/application-gateway-diagnostics/figure7.png
[8]: ./media/application-gateway-diagnostics/figure8.png
[9]: ./media/application-gateway-diagnostics/figure9.png
[10]: ./media/application-gateway-diagnostics/figure10.png
