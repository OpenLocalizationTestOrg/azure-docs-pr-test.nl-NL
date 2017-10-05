---
title: Het gebruik van Power BI Embedded met REST | Microsoft Docs
description: 'Informatie over het gebruik van Power BI Embedded met REST '
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 8bcef780-cca0-4f30-9a9b-9daa1a7ae865
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 02/06/2017
ms.author: asaxton
ms.openlocfilehash: 31624b9d15772a4f08cf013ac713b3aa636acfca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-power-bi-embedded-with-rest"></a>Het gebruik van Power BI Embedded met REST

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a>Power BI Embedded: Wat is en wat het doet

Een overzicht van Power BI Embedded wordt beschreven in de officiële [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), maar we even voordat we de details over het gebruik van deze met REST krijgen.

Het is heel heel eenvoudig. u kunt de dynamische gegevensvisualisaties van gebruiken [Power BI](https://powerbi.microsoft.com) in uw eigen toepassing.

De meeste aangepaste toepassingen vereist voor het leveren van de gegevens voor hun eigen klanten, niet noodzakelijkerwijs gebruikers in hun eigen organisatie. Bijvoorbeeld, als u deel van de service voor bedrijf A en B bedrijf bieden, moeten gebruikers in bedrijf A alleen gegevens zien voor hun eigen bedrijf A. Dat wil zeggen, is de multi-tenancymodus nodig voor de bezorging.

De aangepaste toepassing mogelijk worden biedt tevens een eigen verificatiemethoden zoals formulierverificatie, basic auth, enzovoort... Vervolgens de insluiten oplossing moet werken samen met deze bestaande verificatiemethoden veilig. Het is ook nodig zijn voor gebruikers om te kunnen gebruikmaken van deze ISV-toepassingen zonder de extra aankoop of licenties van een Power BI-abonnement.

 **Power BI Embedded** is ontworpen voor nauwkeurig dit soort scenario's. Dus nu dat we deze korte inleiding uit de weg hebben, gaan we krijgen tot de details van sommige

U kunt de .NET \(C#) of Node.js-SDK voor uw toepassing met Power BI Embedded eenvoudig te maken. Maar in dit artikel wordt uitgelegd over HTTP-stroom \(inclusief AuthN) van Power BI zonder SDK's. Kennis van deze overdracht, kunt u uw toepassing bouwen **met elke programmeertaal**, en u kunt begrijpt diep de essentie van Power BI Embedded.

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a>Maken van Power BI-werkruimteverzameling en get-toegangssleutel \(inrichten)

Power BI Embedded is een van de Azure-services. Alleen de ISV die gebruikmaakt van Azure Portal wordt in rekening gebracht voor gebruikskosten \(per uur gebruikerssessie), en de gebruiker die het rapport is niet in rekening gebracht of zelfs vereisen een Azure-abonnement.
Voordat u begint onze toepassingsontwikkeling, maken we de **Power BI-werkruimteverzameling** met behulp van Azure-Portal.

Elke werkruimte van Power BI Embedded is de werkruimte voor elke klant (tenant) en we veel werkruimten in elke werkruimteverzameling kunt toevoegen. De dezelfde toegangssleutel wordt gebruikt in elke werkruimteverzameling. In de effect, de werkruimteverzameling is de beveiligingsgrens voor Power BI Embedded.

![](media/power-bi-embedded-iframe/create-workspace.png)

Wanneer we klaar bent met het maken van de werkruimteverzameling, kopieert u de toegangssleutel vanuit Azure Portal.

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> We kunnen ook de werkruimteverzameling inrichten en verkrijgen toegangssleutel via REST-API. Zie voor meer informatie, [Power BI Resource Provider-API's](https://msdn.microsoft.com/library/azure/mt712306.aspx).

## <a name="create-pbix-file-with-power-bi-desktop"></a>Pbix-bestand maken met Power BI Desktop

Vervolgens maken we moet de verbinding van gegevens en rapporten worden ingesloten.
Voor deze taak is er geen programmeren of de code. We gebruiken gewoon Power BI Desktop.
In dit artikel won't doorloopt u de details over het gebruik van Power BI Desktop. Als u moet enkele hier, raadpleegt u [aan de slag met Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/). In ons voorbeeld alleen gebruiken we de [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a>Een Power BI-werkruimte maken

Nu dat het inrichten is voltooid, aan de slag van een klant-werkruimte maken in de werkruimteverzameling via REST-API's. De volgende HTTP POST aanvragen (REST) maakt de nieuwe werkruimte in de werkruimteverzameling van onze bestaande. Dit is de [POST werkruimte API](https://msdn.microsoft.com/library/azure/mt711503.aspx). In ons voorbeeld wordt de naam van de werkruimte-verzameling is **mypbiapp**. We stelt u de toegangssleutel die we eerder hebt gekopieerd, als **App-sleutel**. Het is zeer eenvoudig verificatie.

**HTTP-aanvraag**

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

**HTTP-antwoord**

```
HTTP/1.1 201 Created
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces
RequestId: 4220d385-2fb3-406b-8901-4ebe11a5f6da

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/$metadata#workspaces/$entity",
  "workspaceId": "32960a09-6366-4208-a8bb-9e0678cdbb9d",
  "workspaceCollectionName": "mypbiapp"
}
```

De geretourneerde **workspaceId** wordt gebruikt voor de volgende volgende API-aanroepen. Onze toepassing moet deze waarde bewaren.

## <a name="import-pbix-file-into-the-workspace"></a>Pbix-bestand importeren in de werkruimte

Elk rapport in een werkruimte komt overeen met één Power BI Desktop-bestand met een gegevensset \(met inbegrip van instellingen voor gegevensbron). We kunt onze pbix-bestand importeren naar de werkruimte, zoals wordt weergegeven in de onderstaande code. Zoals u ziet, kunnen we het binaire bestand van pbix-bestand met MIME-multipart in HTTP-uploaden.

De uri-fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** is de workspaceId en queryparameter **datasetDisplayName** is de gegevenssetnaam te maken. De gemaakte gegevensset bevat alle gegevens gerelateerd artefacten in pbix-bestand bijvoorbeeld als de geïmporteerde gegevens, de pointer naar de gegevensbron, enzovoort...

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{the content (binary) of .pbix file}
--A300testx--
```

Deze importtaak kan uitvoeren voor een tijdje. Als u klaar kunt onze toepassing de status van de taak met id importeren vragen. In ons voorbeeld wordt de invoer-id is **4eec64dd-533b-47c3-a72c-6508ad854659**.

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

De volgende vraagt de status van deze import-id:

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

Als de taak niet is voltooid, kan het HTTP-antwoord zijn als volgt:

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: 614a13a5-4de7-43e8-83c9-9cd225535136

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Publishing",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "name": "mydataset01"
}
```

Als de taak voltooid is, is het mogelijk dat het HTTP-antwoord meer als volgt:

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: eb2c5a85-4d7d-4cc2-b0aa-0bafee4b1606

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Succeeded",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "reports": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://app.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c"
    }
  ],
  "datasets": [
    {
      "id": "458e0451-7215-4029-80b3-9627bf3417b0",
      "name": "mydataset01",
      "tables": [
      ],
      "webUrl": "https://app.powerbi.com/datasets/458e0451-7215-4029-80b3-9627bf3417b0"
    }
  ],
  "name": "mydataset01"
}
```

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a>Gegevensbron connectiviteit \(en multi-tenancymodus van gegevens)

Terwijl bijna alle de artefacten in pbix-bestand in de werkruimte worden geïmporteerd, zijn de referenties voor gegevensbronnen niet. Als gevolg hiervan, wanneer u **DirectQuery-modus**, het ingesloten rapport correct kan niet worden weergegeven. Maar wanneer u **importmodus**, wordt het rapport met de bestaande geïmporteerde gegevens kunt bekijken. In dat geval moet er de referentie met de volgende stappen via REST-aanroepen ingesteld.

Er moet eerst de gateway datasource ophalen. We weten dat de dataset **id** is de eerder geretourneerde-id.

**HTTP-aanvraag**

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

**HTTP-antwoord**

```
GET HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: 574b0b18-a6fa-46a6-826c-e65840cf6e15

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#gatewayDatasources",
  "value": [
    {
      "id": "5f7ee2e7-4851-44a1-8b75-3eb01309d0ea",
      "gatewayId": "ca17e77f-1b51-429b-b059-6b3e3e9685d1",
      "datasourceType": "Sql",
      "connectionDetails": "{\"server\":\"testserver.database.windows.net\",\"database\":\"testdb01\"}"
    }
  ]
}
```

De geretourneerde gateway-id en de gegevensbron-id \(Zie de vorige **gatewayId** en **id** in de geretourneerde resultatenset), kunnen we de referentie van deze gegevensbron als volgt wijzigen:

**HTTP-aanvraag**

```
PATCH https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/gateways/ca17e77f-1b51-429b-b059-6b3e3e9685d1/datasources/5f7ee2e7-4851-44a1-8b75-3eb01309d0ea
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "credentialType": "Basic",
  "basicCredentials": {
    "username": "demouser",
    "password": "P@ssw0rd"
  }
}
```

**HTTP-antwoord**

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

In productie, kunnen we ook de andere verbindingsreeks voor elke werkruimte met REST-API instellen. \(Internet Explorer, we kunt scheidt u de database voor elk klanten.)

Het volgende is het wijzigen van de verbindingsreeks van de gegevensbron via REST.

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

Of we beveiliging op rijniveau in Power BI Embedded kunnen gebruiken en we kunnen de gegevens voor elke gebruikers in een rapport scheiden. We kunnen as a Result, elke klant rapport met dezelfde pbix inrichten \(gebruikersinterface, enz.) en andere gegevensbronnen.

> [!NOTE]
> Als u **importmodus** in plaats van **DirectQuery-modus**, er is geen manier om te vernieuwen modellen via API. En on-premises gegevensbronnen via Power BI gateway nog wordt niet ondersteund in Power BI Embedded. Echter zeker wilt u het oog houden de [Power BI-blog](https://powerbi.microsoft.com/blog/) voor wat is er nieuw en wat er nieuw in toekomstige releases.

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a>Verificatie en die als host fungeert voor (insluiten) rapporten in onze webpagina

In de vorige REST-API, gebruiken we de toegangssleutel **App-sleutel** zelf als de autorisatie-header. Het is veilig omdat deze aanroepen kunnen worden verwerkt op de server back-end.

Maar als we het rapport in onze webpagina insluiten, dit soort informatie over beveiliging zou worden afgehandeld met JavaScript \(frontend). De waarde van de autorisatie-header moet vervolgens worden beveiligd. Als onze toegangssleutel wordt gedetecteerd door een kwaadwillende gebruiker of schadelijke code, kunnen ze geen bewerkingen met deze sleutel aanroepen.

Wanneer we het rapport in onze webpagina insluiten, we het berekende token moet gebruiken in plaats van de toegangssleutel **App-sleutel**. Onze toepassing moet maken OAuth Json Web Token \(JWT) die bestaat uit de claims en de berekende digitale handtekening. Zoals hieronder weergegeven, is deze OAuth JWT-tokens punt gescheiden gecodeerde tekenreeks.

![](media/power-bi-embedded-iframe/oauth-jwt.png)

Er moet eerst de invoerwaarde is ondertekend later voorbereiden. Deze waarde is de tekenreeks base64-gecodeerd url (rfc4648) van de volgende json en deze worden gescheiden door het punt \(.) teken. Later, wordt uitgelegd hoe u de id van het rapport niet ophalen.

> [!NOTE]
> Als we rij Level Security (RLS) gebruiken met Power BI Embedded willen, er moet ook opgeven **gebruikersnaam** en **rollen** in de claims.

```
{
  "typ":"JWT",
  "alg":"HS256"
}
```

```
{
  "wid":"{workspace id}",
  "rid":"{report id}",
  "wcn":"{workspace collection name}",
  "iss":"PowerBISDK",
  "ver":"0.2.0",
  "aud":"https://analysis.windows.net/powerbi/api",
  "nbf":{start time of token expiration},
  "exp":{end time of token expiration}
}
```

Vervolgens maken we de met base64 gecodeerde tekenreeks van HMAC \(de handtekening) met SHA256-algoritme. Deze ondertekende invoerwaarde is de vorige tekenreeks.

Laatste combineren we de waarde en handtekening invoerreeks periode met \(.) teken. De voltooide tekenreeks is de app-token voor het rapport insluiten. Zelfs als de app-token wordt gedetecteerd door een kwaadwillende gebruiker, kunnen ze de oorspronkelijke toegangssleutel niet ophalen. Deze app-token verloopt snel.

Hier volgt een voorbeeld van een PHP voor deze stappen:

```
<?php
// 1. power bi access key
$accesskey = "MpaUgrTv5e...";

// 2. construct input value
$token1 = "{" .
  "\"typ\":\"JWT\"," .
  "\"alg\":\"HS256\"" .
  "}";
$token2 = "{" .
  "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
  "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
  "\"wcn\":\"mypbiapp\"," . // workspace collection name
  "\"iss\":\"PowerBISDK\"," .
  "\"ver\":\"0.2.0\"," .
  "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
  "\"nbf\":" . date("U") . "," .
  "\"exp\":" . date("U" , strtotime("+1 hour")) .
  "}";
$inputval = rfc4648_base64_encode($token1) .
  "." .
  rfc4648_base64_encode($token2);

// 3. get encoded signature
$hash = hash_hmac("sha256",
    $inputval,
    $accesskey,
    true);
$sig = rfc4648_base64_encode($hash);

// 4. show result (which is the apptoken)
$apptoken = $inputval . "." . $sig;
echo($apptoken);

// helper functions
function rfc4648_base64_encode($arg) {
  $res = $arg;
  $res = base64_encode($res);
  $res = str_replace("/", "_", $res);
  $res = str_replace("+", "-", $res);
  $res = rtrim($res, "=");
  return $res;
}
?>
```

## <a name="finally-embed-the-report-into-the-web-page"></a>Ten slotte wordt het rapport insluiten in de webpagina

Voor het insluiten van onze rapport moet krijgen we de insluiten-url en het rapport **id** met de volgende REST-API.

**HTTP-aanvraag**

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

**HTTP-antwoord**

```
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: d4099022-405b-49d3-b3b7-3c60cf675958

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#reports",
  "value": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c",
      "isFromPbix": false
    }
  ]
}
```

We kunnen het rapport insluiten in de web-app met behulp van het vorige app-token.
Als we de volgende voorbeeldcode bekijkt, wordt het vorige gedeelte is hetzelfde als het vorige voorbeeld. In het laatste deel dit voorbeeld wordt de **embedUrl** \(het vorige resultaat te bekijken) in de iframe en wordt het app-token boeken in de iframe.

> [!NOTE]
> U moet de id-waarde van het rapport wijzigen in een eigen. Vanwege een fout in ons systeem inhoudsbeheer is de iframe-code in het voorbeeld Lees ook letterlijk. Verwijder de capped tekst uit het label als u kopieert en plakt deze voorbeeldcode.

```
    <?php
    // 1. power bi access key
    $accesskey = "MpaUgrTv5e...";

    // 2. construct input value
    $token1 = "{" .
      "\"typ\":\"JWT\"," .
      "\"alg\":\"HS256\"" .
      "}";
    $token2 = "{" .
      "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
      "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
      "\"wcn\":\"mypbiapp\"," . // workspace collection name
      "\"iss\":\"PowerBISDK\"," .
      "\"ver\":\"0.2.0\"," .
      "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
      "\"nbf\":" . date("U") . "," .
      "\"exp\":" . date("U" , strtotime("+1 hour")) .
      "}";
    $inputval = rfc4648_base64_encode($token1) .
      "." .
      rfc4648_base64_encode($token2);

    // 3. get encoded signature value
    $hash = hash_hmac("sha256",
        $inputval,
        $accesskey,
        true);
    $sig = rfc4648_base64_encode($hash);

    // 4. get apptoken
    $apptoken = $inputval . "." . $sig;

    // helper functions
    function rfc4648_base64_encode($arg) {
      $res = $arg;
      $res = base64_encode($res);
      $res = str_replace("/", "_", $res);
      $res = str_replace("+", "-", $res);
      $res = rtrim($res, "=");
      return $res;
    }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Test page</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
      <button id="btnView">View Report !</button>
      <div id="divView">
        <**REMOVE THIS CAPPED TEXT IF COPIED** iframe id="ifrTile" width="100%" height="400"></iframe>
      </div>
      <script>
        (function () {
          document.getElementById('btnView').onclick = function() {
            var iframe = document.getElementById('ifrTile');
            iframe.src = 'https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c';
            iframe.onload = function() {
              var msgJson = {
                action: "loadReport",
                accessToken: "<?=$apptoken?>",
                height: 500,
                width: 722
              };
              var msgTxt = JSON.stringify(msgJson);
              iframe.contentWindow.postMessage(msgTxt, "*");
            };
          };
        }());
      </script>
    </body>
```

En dit is het resultaat:

![](media/power-bi-embedded-iframe/view-report.png)

Op dit moment Power BI Embedded alleen het rapport weergegeven in de iframe. Maar let op de [Power BI Blog](https://powerbi.microsoft.com/blog/). Toekomstige verbeteringen kunnen gebruiken om nieuwe clientzijde API's die worden laat het ons informatie in de iframe verzenden, evenals informatie opvragen uit. Interessante spullen!

## <a name="see-also"></a>Zie ook
* [Verifiëren en autoriseren in Power BI Embedded](power-bi-embedded-app-token-flow.md)

Nog vragen? [Probeer de Power BI-community](http://community.powerbi.com/)

