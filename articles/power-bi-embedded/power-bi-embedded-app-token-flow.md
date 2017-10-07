---
title: aaaAuthenticating en autoriseren met Power BI Embedded
description: "Verifiëren en autoriseren met Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a>Verifiëren en autoriseren met Power BI Embedded

maakt gebruik van Power BI Embedded service Hallo **sleutels** en **App-Tokens** voor verificatie en autorisatie in plaats van expliciete eindgebruiker verificatie. In dit model wordt beheerd door uw toepassing verificatie en autorisatie voor uw eindgebruikers. Indien nodig, wordt uw app maakt en stuurt Hallo App-Tokens die onze service toorender vertelt Hallo gevraagde rapport. Dit ontwerp nodig uw app toouse Azure Active Directory niet voor verificatie en autorisatie, hoewel u nog steeds kunt.

## <a name="two-ways-tooauthenticate"></a>Twee manieren tooauthenticate

**Sleutel** -kunt u sleutels gebruiken voor alle Power BI Embedded REST API-aanroepen. Hallo-codes kunnen u vinden in Hallo **Azure-portal** door te klikken op **alle instellingen** en vervolgens **toegangssleutels**. Uw sleutel altijd behandeld alsof het een wachtwoord. Deze sleutels ook machtigingen toomake REST API niet aanroepen voor een bepaalde werkruimte-verzameling.

een sleutel op een REST-aanroep toouse Hallo na autorisatie-header toevoegen:            

    Authorization: AppKey {your key}

**App-token** -App-tokens worden gebruikt voor alle insluiten aanvragen. Ze zijn ontworpen toobe uitvoeren clientzijde, zodat ze beperkte tooa één rapport en de best practice tooset een verlooptijd.

App-tokens zijn een JWT (JSON Web Token) die is ondertekend door een van uw sleutels.

Uw app-token kan Hallo claims volgende bevatten:

| Claim | Beschrijving |
| --- | --- |
| **ver** |Hallo-versie van Hallo app-token. 0.2.0 is Hallo huidige versie. |
| **AUD** |Hallo bedoeld ontvanger van Hallo-token. Voor Power BI Embedded gebruik: 'https://analysis.windows.net/powerbi/api'. |
| **ISS** |Een tekenreeks die aangeeft Hallo toepassing hello token uitgegeven. |
| **type** |Hallo-type van app-token dat wordt gemaakt. Huidige Hallo alleen ondersteund type is **insluiten**. |
| **draadloze** |Werkruimte verzameling naam Hallo token wordt uitgegeven. |
| **WID** |Werkruimte-ID Hallo token wordt uitgegeven. |
| **RID** |Rapport ID Hallo token wordt uitgegeven. |
| **gebruikersnaam** (optioneel) |Gebruikt voor beveiliging op Rijniveau, is dit een tekenreeks waarmee Hallo gebruiker identificeren wanneer RLS regels toepassen. |
| **rollen** (optioneel) |Een tekenreeks met Hallo rollen tooselect bij het toepassen van regels voor beveiliging op rijniveau. Als meer dan één rol wordt doorgegeven, moeten worden doorgegeven als een String-matrix. |
| **SCP** (optioneel) |Een tekenreeks met Hallo machtigingen scopes. Als meer dan één rol wordt doorgegeven, moeten worden doorgegeven als een String-matrix. |
| **EXP** (optioneel) |Hiermee wordt aangegeven in welke Hallo-token verloopt Hallo-tijd. Deze moeten worden doorgegeven als Unix tijdstempels. |
| **NBF** (optioneel) |Geeft aan in welke Hallo token begint geldig Hallo-tijd. Deze moeten worden doorgegeven als Unix tijdstempels. |

Een voorbeeld-app-token ziet er als volgt:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

Wanneer gedecodeerd, deze wordt als volgt uitzien:

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

Er zijn methoden beschikbaar binnen Hallo SDK's die het maken van apptokens te vereenvoudigen. Bijvoorbeeld: voor .NET u kunt bekijkt hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) klasse en Hallo [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methoden.

Voor de .NET SDK hello, raadpleegt u te[Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).

## <a name="scopes"></a>Scopes

Wanneer u insluiten tokens gebruikt, kunt u toorestrict informatie over het gebruik van Hallo-resources die u toegang te geven. Daarom kunt u een token met bereik machtigingen genereren.

Hallo volgen Hallo beschikbare scopes voor Power BI Embedded.

|Bereik|Beschrijving|
|---|---|
|Dataset.Read|Machtigingsinstellingen tooread Hallo opgegeven gegevensset.|
|Dataset.Write|Biedt machtiging toowrite toohello opgegeven gegevensset.|
|Dataset.ReadWrite|Machtiging tooread en write toohello samengesteld dataset biedt.|
|Report.Read|Machtigingsinstellingen tooview Hallo opgegeven rapport.|
|Report.ReadWrite|Biedt machtiging tooview en bewerk Hallo opgegeven rapport.|
|Workspace.Report.Create|Machtiging toocreate biedt een nieuw rapport binnen Hallo opgegeven werkruimte.|
|Workspace.Report.Copy|Machtiging tooclone biedt een bestaand rapport binnen Hallo opgegeven werkruimte.|

U kunt meerdere scopes opgeven met een spatie tussen Hallo scopes Hallo volgende.

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

**Vereiste claims - scopes**

SCP: {scopesClaim} scopesClaim mag een tekenreeks of een matrix van tekenreeksen, let Hallo toegestane machtigingen tooworkspace resources (rapport, gegevensset, enz.)

Een gecodeerde token, met de scopes die zijn gedefinieerd, ziet er vergelijkbare toohello volgende.

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a>Bewerkingen en -scopes

|Bewerking|Doelbron|Token machtigingen|
|---|---|---|
|Een nieuw rapport op basis van een gegevensset voor (in het geheugen) maken.|Gegevensset|Dataset.Read|
|(In het geheugen) Maak een nieuw rapport op basis van een gegevensset en Hallo rapport opslaan.|Gegevensset|* Dataset.Read<br>* Workspace.Report.Create|
|(In het geheugen) een bestaand rapport verkennen/bewerken en weergeven. Report.Read impliceert Dataset.Read. Hierdoor kunnen geen machtigingen toosave bewerkingen.|Rapport|Report.Read|
|Bewerken en opslaan van een bestaand rapport.|Rapport|Report.ReadWrite|
|Sla een kopie van een rapport (OpslaanAls).|Rapport|* Report.Read<br>* Workspace.Report.Copy|

## <a name="heres-how-hello-flow-works"></a>Hier wordt de werking van Hallo stroom
1. Hallo-API-sleutels tooyour toepassing kopiëren. U kunt Hallo sleutels krijgen in **Azure Portal**.
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. Token een claim asserts en heeft een verlooptijd.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. Token opgehaald ondertekend met een API-sleutels voor toegang.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. Gebruiker vraagt tooview een rapport.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. Token is gevalideerd met een API-sleutels voor toegang.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. Power BI Embedded verzendt een rapport toouser.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

Na **Power BI Embedded** verzendt de gebruiker van een rapport toohello Hallo gebruiker Hallo rapport in uw aangepaste app kunt weergeven. Bijvoorbeeld, als u hebt geïmporteerd Hallo [analyseren verkoop gegevens PBIX voorbeeld](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), Hallo voorbeeld-web-app eruit als volgt:

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a>Zie ook

[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Aan de slag met Microsoft Power BI Embedded voorbeeld](power-bi-embedded-get-started-sample.md)  
[Algemene scenario's voor Microsoft Power BI Embedded](power-bi-embedded-scenarios.md)  
[Aan de slag met Microsoft Power BI Embedded](power-bi-embedded-get-started.md)  
[Power BI-CSharp Git-opslagplaats](https://github.com/Microsoft/PowerBI-CSharp)  
Nog vragen? [Probeer Hallo Power BI-Community](http://community.powerbi.com/)

