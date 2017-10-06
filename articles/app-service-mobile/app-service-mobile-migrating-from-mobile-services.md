---
title: aaaMigrate van Mobile Services tooan App Service-mobiele App
description: Meer informatie over hoe tooeasily migreert uw Mobile Services-toepassing tooan App Service-mobiele App
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 07507ea2-690f-4f79-8776-3375e2adeb9e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: glenga
ms.openlocfilehash: cd2e8d98595703389300b79da9bf51cdcefe7b40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="article-top"></a>Migreren van uw bestaande tooAzure met Azure Mobile Service-App Service
Hello [algemene beschikbaarheid van Azure App Service], Azure Mobile Services-sites kunnen gemakkelijk worden gemigreerd in-place tootake profiteren van alle functies van hello Azure App Service.  Dit document wordt uitgelegd welke tooexpect bij het migreren van uw site van Azure Mobile Services tooAzure App Service.

## <a name="what-does-migration-do"></a>Wat doet migratie tooyour site
Migratie van uw Azure Mobile Service Hiermee schakelt u uw mobiele Service in een [Azure App Service] app zonder Hallo-code.  Uw Notification Hubs, SQL gegevensverbinding verificatie-instellingen, geplande taken en domeinnaam blijven ongewijzigd.  Mobiele clients met behulp van uw Azure Mobile Service voortgezet toooperate gebruikelijke manier.  Migratie wordt uw service opnieuw gestart wanneer het overgebrachte tooAzure App Service.

[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

## <a name="why-migrate"></a>Waarom moet u uw site migreren
Microsoft is aanbevelen migreren van uw Azure Mobile Service tootake voordeel van Hallo functies van Azure App Service, waaronder:

* Nieuwe host-functies, waaronder [WebJobs] en [aangepaste domeinnamen].
* Connectiviteit tooyour lokale resources met behulp van [VNet] bovendien te[hybride verbindingen].
* Bewaking en probleemoplossing met New Relic of [Application Insights].
* Ingebouwde DevOps tooling, met inbegrip van [staging-sleuven], terugdraaien en in productie testen.
* [Automatische schaling], taakverdeling, en [prestatiebewaking].

Zie voor meer informatie over Hallo voordelen van Azure App Service Hallo [tegenover Mobile Services. App Service] onderwerp.

## <a name="before-you-begin"></a>Voordat u begint
Voordat u begint met belangrijke werk op uw site, moet u back-up van uw mobiele Service scripts en SQL-database.

## <a name="migrating-site"></a>Migreren van uw sites
Hallo-migratieproces worden gemigreerd van alle sites binnen één Azure-regio.

toomigrate uw site:

1. Meld u bij toohello [klassieke Azure-Portal].
2. Selecteer een mobiele Service in Hallo regio die u wenst toomigrate.
3. Klik op Hallo **tooApp Service migreren** knop.

   ![Hallo knop migreren][0]
4. Dialoogvenster Hallo migreren tooApp-Service worden gelezen.
5. Hallo-naam van uw mobiele Service in de daarvoor bestemde vak Hallo invoeren.  Bijvoorbeeld, als uw domeinnaam contoso.azure mobile.net is, voer dan *contoso* in Hallo daarvoor bestemde vak.
6. Klik op Hallo maatstreepjes.

Hallo-status van de migratie in activiteitsbewaking Hallo Hallo bewaken. Uw site wordt vermeld als *migreren* in Hallo klassieke Azure-Portal.

  ![Migratie-activiteitsbewaking][1]

Elke migratie kan duren vanaf 3 too15 minuten per mobiele service die wordt gemigreerd.  Uw site blijft beschikbaar tijdens de migratie Hallo.
Uw site wordt opnieuw opgestart aan einde van het migratieproces Hallo Hallo.  Hallo-site is niet beschikbaar tijdens het Hallo opnieuw wordt gestart, die een paar seconden duurt.

## <a name="finalizing-migration"></a>Hallo migratie voltooien
Plan tootest uw site van een mobiele client aan einde van het migratieproces Hallo Hallo.  Zorg ervoor dat u alle Clientacties in de algemene zonder wijzigingen toohello mobiele clients kunt uitvoeren.  

### <a name="update-app-service-tier"></a>Selecteer een geschikte App Service-prijscategorie
Hebt u meer flexibiliteit in het nadat u hebt gemigreerd tooAzure App Service-prijzen.

1. Meld u bij toohello [Azure-portal].
2. Selecteer **alle resources** of **App Services** klik vervolgens op Hallo-naam van de gemigreerde mobiele Service.
3. Standaard wordt de blade instellingen Hallo geopend.
4. Klik op **App Service-Plan** in menu Hallo-instellingen.
5. Klik op Hallo **prijscategorie** tegel.
6. Hallo tegel juiste tooyour vereisten op en klik op **Selecteer**.  Mogelijk moet u tooClick **weergeven van alle** toosee Hallo beschikbare Prijscategorieën.

Als een beginpunt aangeraden Hallo lagen te volgen:

| Prijscategorie mobiele Service | App Service-prijscategorie |
|:--- |:--- |
| Gratis |F1 Free |
| Basic |B1 Basic |
| Standard |S1 Standard |

Er is aanzienlijke flexibiliteit bij het kiezen van Hallo rechts prijscategorie voor uw toepassing.  Raadpleeg te[prijzen van App Service] voor volledige informatie over Hallo prijzen van uw nieuwe App Service.

> [!TIP]
> Hallo-App Service-standaardcategorie toegang toomany functies bevat dat u toouse kunt, met inbegrip van [staging-sleuven], automatische back-ups en automatisch schalen.  Bekijk Hallo nieuwe mogelijkheden terwijl u er bent!
>
>

### <a name="review-migration-scheduler-jobs"></a>Bekijk Hallo gemigreerd Scheduler-taken
Scheduler-taken wordt niet meer weergegeven tot ongeveer 30 minuten na de migratie.  Geplande taken worden toorun op Hallo-achtergrond voortgezet.
tooview uw geplande taken nadat ze opnieuw zichtbaar zijn:

1. Meld u bij toohello [Azure-portal].
2. Selecteer **Bladeren >**, voer **planning** in Hallo *Filter* vak en selecteer vervolgens **Scheduler verzamelingen**.

Er zijn een beperkt aantal free-scheduler-taken beschikbaar na de migratie.  Controleer de informatie over het gebruik en Hallo [Azure Scheduler plannen].

### <a name="configure-cors"></a>CORS configureren, indien nodig
Cross-origin-resources delen is een techniek tooallow een website tooaccess een Web-API in een ander domein.  Als u van Azure Mobile Services met een koppeling naar een website gebruikmaakt, moet u tooconfigure CORS als onderdeel van Hallo-migratie.  Als u Azure Mobile Services uitsluitend op mobiele apparaten gebruiken, klikt u vervolgens hoeft CORS niet geconfigureerd, behalve in uitzonderlijke gevallen toobe.

De gemigreerde CORS-instellingen zijn beschikbaar als Hallo **MS_CrossDomainWhitelist** App-instelling.  toomigrate uw site toohello App Service CORS-faciliteit:

1. Meld u bij toohello [Azure-portal].
2. Selecteer **alle resources** of **App Services** klik vervolgens op Hallo-naam van de gemigreerde mobiele Service.
3. Standaard wordt de blade instellingen Hallo geopend.
4. Klik op **CORS** in Hallo API-menu.
5. Voer geen toegestane oorsprongen in Hallo daarvoor bestemde vak, drukt u op Enter na elke opdracht.
6. Nadat uw lijst met toegestane oorsprongen correct is, klikt u op de knop Opslaan Hallo.

> [!TIP]
> Een van de voordelen van het gebruik van een Azure App Service Hallo is dat u uw website en de mobiele service op Hallo uitvoeren kunt dezelfde site.  Zie voor meer informatie, Hallo [Vervolgstappen](#next-steps) sectie.
>
>

### <a name="download-publish-profile"></a>Een nieuwe publicatieprofiel downloaden
Hallo publicatieprofiel van uw site wordt gewijzigd wanneer u migreert tooAzure App Service.  Als u van plan toopublish uw site vanuit Visual Studio bent, moet u een nieuwe publicatieprofiel.  toodownload hello nieuwe publicatieprofiel:

1. Meld u bij toohello [Azure-portal].
2. Selecteer **alle resources** of **App Services** klik vervolgens op Hallo-naam van de gemigreerde mobiele Service.
3. Klik op **Get publicatieprofiel**.

Hallo met publicatie-instellingen bestand is gedownload tooyour computer.  Normaal gesproken wordt aangeroepen *sitename*. Met publicatie-instellingen.  Importeren Hallo publicatie-instellingen in uw bestaande project:

1. Open Visual Studio en het Azure Mobile Service-project.
2. Met de rechtermuisknop op het project in Hallo **Solution Explorer** en selecteer **publiceren...**
3. Klik op **importeren**
4. Klik op **Bladeren** en selecteert u het gedownloade bestand publicatie-instellingen.  Klik op **OK**
5. Klik op **Validate Connection** tooensure Hallo instellingen werk publiceren.
6. Klik op **publiceren** toopublish uw site.

## <a name="working-with-your-site"></a>Werken met uw na de sitemigratie
Beginnen met werken met uw nieuwe App Service in Hallo [Azure-portal] na de migratie.  Hallo hieronder vindt u informatie op specifieke bewerkingen die u hebt tooperform in Hallo gebruikt [klassieke Azure-Portal], samen met hun App Service-equivalent.

### <a name="publishing-your-site"></a>Downloaden en publiceren van een gemigreerde site
Uw site is beschikbaar via de git- of FTP- en met verschillende verschillende mechanismen, met inbegrip van web Deploy, TFS, volgt, GitHub en FTP-opnieuw kan worden gepubliceerd.  Hallo-implementatiereferenties worden gemigreerd met Hallo rest van uw site.  Als u uw implementatiereferenties niet ingesteld of als u deze niet meer weet, kunt u ze opnieuw instellen:

1. Meld u bij toohello [Azure-portal].
2. Selecteer **alle resources** of **App Services** klik vervolgens op Hallo-naam van de gemigreerde mobiele Service.
3. Standaard wordt de blade instellingen Hallo geopend.
4. Klik op **implementatiereferenties** in Hallo menu publiceren.
5. Hallo nieuwe implementatiereferenties invoeren in Hallo vakken en klik vervolgens op de knop Opslaan Hallo.

U kunt deze referenties tooclone Hallo site gebruiken met git of geautomatiseerde implementaties van GitHub, TFS of volgt instellen.  Zie voor meer informatie, Hallo [Implementatiedocumentatie voor Azure App Service].

### <a name="appsettings"></a>Toepassingsinstellingen
De meeste instellingen voor een gemigreerde mobiele service zijn beschikbaar via de App-instellingen.  U kunt een lijst met Hallo app-instellingen ophalen uit Hallo [Azure-portal].
tooview of wijzig de appinstellingen van uw:

1. Meld u bij toohello [Azure-portal].
2. Selecteer **alle resources** of **App Services** klik vervolgens op Hallo-naam van de gemigreerde mobiele Service.
3. Standaard wordt de blade instellingen Hallo geopend.
4. Klik op **toepassingsinstellingen** in algemene Hallo-menu.
5. Sectie van de Appinstellingen toohello schuiven en zoek uw app-instelling.
6. Klik op Hallo-waarde van Hallo app tooedit Hallo waarde.  Klik op **opslaan** toosave Hallo waarde.

U kunt meerdere app-instellingen op Hallo bijwerken hetzelfde moment.

> [!TIP]
> Er zijn twee instellingen van de toepassing Hello dezelfde waarde.  Bijvoorbeeld, wordt er *ApplicationKey* en *MS\_ApplicationKey*.  Bijwerken van beide toepassingsinstellingen op Hallo hetzelfde moment.
>
>

### <a name="authentication"></a>Verificatie
Alle verificatieinstellingen zijn beschikbaar als de App-instellingen in uw gemigreerde site.  tooupdate uw verificatie-instellingen, moet u de juiste app-instellingen wijzigen.  Hallo volgende tabel ziet u Hallo juiste app-instellingen voor uw provider voor verificatie:

| Provider | Client-ID | Clientgeheim | Andere instellingen |
|:--- |:--- |:--- |:--- |
| Microsoft-account |**MS\_MicrosoftClientID** |**MS\_MicrosoftClientSecret** |**MS\_MicrosoftPackageSID** |
| Facebook |**MS\_FacebookAppID** |**MS\_FacebookAppSecret** | |
| Twitter |**MS\_TwitterConsumerKey** |**MS\_TwitterConsumerSecret** | |
| Google |**MS\_GoogleClientID** |**MS\_GoogleClientSecret** | |
| Azure AD |**MS\_AadClientID** | |**MS\_AadTenants** |

Opmerking: **MS\_AadTenants** wordt opgeslagen als een door komma's gescheiden lijst met tenant-domeinen (Hallo 'Tenants toegestaan' velden in Hallo Mobile Services-portal).

> [!WARNING]
> **Gebruik geen Hallo-verificatiemechanismen in het menu Hallo-instellingen**
>
> Azure App Service biedt een afzonderlijke 'zonder code' verificatie en autorisatie onder Hallo *verificatie / autorisatie* menu instellingen en hello (afgeschaft) *mobiele verificatie* de optie onder menu Hallo-instellingen.  Deze opties zijn niet compatibel met een gemigreerde Azure Mobile Service.  U kunt [upgrade van uw site](app-service-mobile-net-upgrading-from-mobile-services.md) tootake profiteren van hello Azure App Service-verificatie.
>
>

### <a name="easytables"></a>Gegevens
Hallo *gegevens* tabblad in Mobile Services is vervangen door *gemakkelijk tabellen* binnen hello Azure-portal.  tooaccess gemakkelijk tabellen:

1. Meld u bij toohello [Azure-portal].
2. Selecteer **alle resources** of **App Services** klik vervolgens op Hallo-naam van de gemigreerde mobiele Service.
3. Standaard wordt de blade instellingen Hallo geopend.
4. Klik op **gemakkelijk tabellen** in mobiele Hallo-menu.

U kunt een tabel toevoegen door te klikken op Hallo **toevoegen** knop of de bestaande tabellen openen door te klikken op de naam van een tabel.  Er zijn verschillende bewerkingen u vanaf deze blade doen kunt, met inbegrip van:

* Tabelmachtigingen wijzigen
* Hallo operationele scripts bewerken
* Hallo-tabelschema beheren
* Hallo-tabel verwijderen
* De inhoud van de tabel Hallo wissen
* Verwijderen van de specifieke rijen van de tabel Hallo

### <a name="easyapis"></a>API
Hallo *API* tabblad in Mobile Services is vervangen door *eenvoudige API's* binnen hello Azure-portal.  tooaccess eenvoudige API's:

1. Meld u bij toohello [Azure-portal].
2. Selecteer **alle resources** of **App Services** klik vervolgens op Hallo-naam van de gemigreerde mobiele Service.
3. Standaard wordt de blade instellingen Hallo geopend.
4. Klik op **eenvoudige API's** in mobiele Hallo-menu.

Uw gemigreerde API's staan al in het Hallo-blade.  U kunt ook een API toevoegen van deze blade.  toomanage een specifieke API, klikt u op Hallo-API.
U kunt nieuwe blade Hallo Hallo machtigingen aanpassen en Hallo scripts voor Hallo API bewerken.

### <a name="on-demand-jobs"></a>Scheduler-taken
Alle scheduler-taken zijn beschikbaar via Hallo Scheduler-Taakverzamelingen-sectie.  tooaccess uw scheduler-taken:

1. Meld u bij toohello [Azure-portal].
2. Selecteer **Bladeren >**, voer **planning** in Hallo *Filter* vak en selecteer vervolgens **Scheduler verzamelingen**.
3. Selecteer Hallo Taakverzameling voor uw site.  Dit sjabloon heet *sitename*-taken.
4. Klik op **instellingen**.
5. Klik op **Scheduler-taken** onder beheren.

Geplande taken worden weergegeven met Hallo frequentie die u hebt opgegeven voor de migratie.  Op aanvraag taken zijn uitgeschakeld.  een taak op aanvraag toorun:

1. Selecteer desgewenst toorun Hallo-taak.
2. Klik indien nodig op **inschakelen** tooenable Hallo taak.
3. Klik op **instellingen**, klikt u vervolgens **planning**.
4. Selecteer een herhaling van **eenmaal**, klikt u vervolgens op **opslaan**

Uw taken op aanvraag bevinden zich in `App_Data/config/scripts/scheduler post-migration`.  Het is raadzaam dat u alle taken voor op aanvraag te converteren[WebJobs] of [functies].  Schrijven van nieuwe scheduler-taken als [WebJobs] of [functies].

### <a name="notification-hubs"></a>Notification Hubs
Mobile Services maakt gebruik van Notification Hubs voor pushmeldingen.  gebruikte toolink Hallo Notification Hub tooyour Mobile Service zijn Hallo volgende App-instellingen na de migratie:

| Toepassingsinstelling | Beschrijving |
|:--- |:--- |
| **MS\_PushEntityNamespace** |Hallo Notification Hub Namespace |
| **MS\_NotificationHubName** |Hallo Notification Hub-naam |
| **MS\_NotificationHubConnectionString** |Hallo Notification Hub-verbindingsreeks |
| **MS\_NamespaceName** |Een alias voor MS_PushEntityNamespace |

Uw Notification Hub wordt beheerd via Hallo [Azure-portal].  Houd rekening met de naam van de Notification Hub hello (u kunt dit vinden met behulp van App-instellingen Hallo):

1. Meld u bij toohello [Azure-portal].
2. Selecteer **Bladeren**>, selecteer daarna **Notification Hubs**
3. Klik op de naam van de Notification Hub Hallo gekoppeld aan de mobiele service Hallo.

> [!NOTE]
> Als uw Notification HUb is een type 'Mixed', is het niet zichtbaar.  "Gemengde" Typ notification hubs gebruikmaken van zowel Notification Hubs en verouderde Service Bus-functies.  [Converteren van de gemengde naamruimten] voordat u doorgaat.  Zodra het Hallo-conversie is voltooid, uw notification hub wordt weergegeven in Hallo [Azure-portal].
>
>

Raadpleeg voor meer informatie, Hallo [Notification Hubs] documentatie.

> [!TIP]
> Notification Hubs-beheerfuncties in Hallo [Azure-portal] zijn nog steeds in preview.  Hallo [klassieke Azure-Portal] blijft beschikbaar voor het beheren van uw Notification Hubs.
>
>

### <a name="legacy-push"></a>Verouderde Push-instellingen
Als u Push geconfigureerd op uw mobiele service voordat Hallo inleiding op Notification Hubs, gebruikt u *verouderde push*.  Als u met behulp van Push en een Notification Hub die worden vermeld in de configuratie niet wordt weergegeven, dan is het waarschijnlijk u *verouderde push*.  Deze functie wordt gemigreerd met de functies.  We raden echter aan dat u een upgrade tooNotification Hubs uitvoert zodra Hallo migratie voltooid is.

In tijdelijke hello zijn alle Hallo verouderde push-instellingen (met opmerkelijke uitzondering Hallo van Hallo APNS-certificaat) beschikbaar in App-instellingen.  Hallo APNS-certificaat bijwerken door de juiste Hallo-bestand op Hallo bestandssysteem.

### <a name="app-settings"></a>Andere Appinstellingen
Hallo volgen als u meer app-instellingen zijn gemigreerde van uw mobiele Service en onder *instellingen* > *Appinstellingen*:

| Toepassingsinstelling | Beschrijving |
|:--- |:--- |
| **MS\_MobileServiceName** |Hallo-naam van uw app |
| **MS\_MobileServiceDomainSuffix** |Hallo voorvoegsel van het domein. Internet Explorer Azure-mobile.net |
| **MS\_ApplicationKey** |De sleutel van uw toepassing |
| **MS\_hoofdsleutel** |De hoofdsleutel van uw app |

Hallo-Toepassingssleutel en een hoofdsleutel zijn identiek toohello toepassing sleutels van uw oorspronkelijke mobiele Service.  In het bijzonder is Hallo Toepassingssleutel verzonden door mobiele clients toovalidate Hallo mobiele API worden gebruikt.

### <a name="cliequivalents"></a>Opdrachtregelopdrachten
U kunt meer Hallo *azure mobiele* opdracht toomanage uw Azure Mobile Services-site.  In plaats daarvan veel functies zijn vervangen door Hallo *azure site* opdracht.  Gebruik Hallo tabel toofind equivalenten voor gewone opdrachten te volgen:

| *Azure Mobile* opdracht | Gelijkwaardige *Azure Site* opdracht |
|:--- |:--- |
| mobiele locaties |locatie van sitelijst |
| lijst met mobiele |lijst met de site |
| mobiele weergeven *naam* |site weergeven *naam* |
| mobiele herstart *naam* |opnieuw opstarten site *naam* |
| mobiele opnieuw distribueren *naam* |site-implementatie opnieuw distribueren *commitId* *naam* |
| mobiele sleutelset *naam* *type* *waarde* |site appsetting verwijderen *sleutel* *naam* <br/> toevoegen van de site appsetting *sleutel*=*waarde* *naam* |
| lijst met mobiele config *naam* |sitelijst voor appsetting *naam* |
| mobiele config ophalen *naam* *sleutel* |site van appsetting weergeven *sleutel* *naam* |
| mobiele configuratieset *naam* *sleutel* |site appsetting verwijderen *sleutel* *naam* <br/> toevoegen van de site appsetting *sleutel*=*waarde* *naam* |
| lijst met mobiele domein *naam* |sitelijst voor domein *naam* |
| mobiele domein toevoegen *naam* *domein* |site-domein toevoegen *domein* *naam* |
| mobiele domein verwijderen *naam* |site domein verwijderen *domein* *naam* |
| mobiele scale weergeven *naam* |site weergeven *naam* |
| mobiele schaal wijzigen *naam* |schaal sitemodus *modus* *naam* <br /> site-exemplaren van de schaal *exemplaren* *naam* |
| lijst met mobiele appsetting *naam* |sitelijst voor appsetting *naam* |
| mobiele appsetting toevoegen *naam* *sleutel* *waarde* |toevoegen van de site appsetting *sleutel*=*waarde* *naam* |
| mobiele appsetting verwijderen *naam* *sleutel* |site appsetting verwijderen *sleutel* *naam* |
| mobiele appsetting weergeven *naam* *sleutel* |site appsetting verwijderen *sleutel* *naam* |

Verificatie- of push notification instellingen door bij te werken Hallo juiste toepassingsinstelling bijwerken.
Bestanden bewerken en de site via de FTP- of git publiceert.

### <a name="diagnostics"></a>Diagnostische gegevens en logboekregistratie
Diagnostische logboekregistratie is gewoonlijk in een Azure App Service uitgeschakeld.  Diagnostische logboekregistratie tooenable:

1. Meld u bij toohello [Azure-portal].
2. Selecteer **alle resources** of **App Services** klik vervolgens op Hallo-naam van de gemigreerde mobiele Service.
3. Standaard wordt de blade instellingen Hallo geopend.
4. Selecteer **diagnostische logboeken** onder Hallo functies menu.
5. Klik op **ON** voor Hallo volgende Logboeken: **toepassingslogboeken (bestandssysteem)**, **gedetailleerde foutberichten**, en **tracering van mislukte aanvragen**
6. Klik op **bestandssysteem** voor logboekregistratie van webserver
7. Klik op **opslaan**

tooview hello Logboeken:

1. Meld u bij toohello [Azure-portal].
2. Selecteer **alle resources** of **App Services** klik vervolgens op Hallo-naam van de gemigreerde mobiele Service.
3. Klik op Hallo **extra** knop
4. Selecteer **Logboekstream** onder Hallo OBSERVE menu.

Logboeken worden weergegeven in Hallo venster nadat ze zijn gegenereerd.  U kunt ook downloaden Hallo-logboeken voor latere analyse met behulp van de implementatiereferenties van uw. Zie voor meer informatie, Hallo [logboekregistratie] documentatie.

## <a name="known-issues"></a>Bekende problemen
### <a name="deleting-a-migrated-mobile-app-clone-causes-a-site-outage"></a>Verwijderen van een kloon mobiele App gemigreerd zorgt ervoor dat een onderbreking van deze site
Als u uw gemigreerde mobiele service met Azure PowerShell, wordt verwijderen Hallo kloon klonen, wordt Hallo DNS-vermelding voor uw productieservice verwijderd.  Uw site is niet langer toegankelijk is vanaf Internet Hallo.  

Oplossing: Als u wenst dat tooclone uw site, doen via Hallo-portal.

### <a name="changing-webconfig-does-not-work"></a>Het wijzigen van Web.config werkt niet
Als u een ASP.NET-website hebt, wijzigt u toohello `Web.config` bestand komen niet toegepast.  Hello Azure App Service bouwt geschikte `Web.config` bestand tijdens opstarten toosupport Hallo Mobile Services runtime.  U kunt bepaalde instellingen (zoals aangepaste headers) met behulp van een XML-transformatiebestand overschrijven.  Maak een bestand in aangeroepen `applicationHost.xdt` -dit bestand moet terechtkomen op Hallo `D:\home\site` directory op Hallo Azure-Service.  Upload de `applicationHost.xdt` bestand via een aangepaste implementatie scripts of rechtstreeks met behulp van Kudu.  Hallo hieronder vindt u een voorbeelddocument:

```
<?xml version="1.0" encoding="utf-8"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <httpProtocol>
      <customHeaders>
        <add name="X-Frame-Options" value="DENY" xdt:Transform="Replace" />
        <remove name="X-Powered-By" xdt:Transform="Insert" />
      </customHeaders>
    </httpProtocol>
    <security>
      <requestFiltering removeServerHeader="true" xdt:Transform="SetAttributes(removeServerHeader)" />
    </security>
  </system.webServer>
</configuration>
```

Zie voor meer informatie, Hallo [XDT transformeren voorbeelden] documentatie op GitHub.

### <a name="migrated-mobile-services-cannot-be-added-tootraffic-manager"></a>Gemigreerde Mobile Services kan niet tooTraffic Manager worden toegevoegd
Wanneer u een Traffic Manager-profiel maakt, kunt u niet rechtstreeks een gemigreerde mobiele service toohello profiel kiezen.  Gebruik een 'Extern eindpunt'.  Het externe eindpunt kan alleen worden toegevoegd via PowerShell.  Zie voor meer informatie de [Traffic Manager-zelfstudie](https://azure.microsoft.com/blog/azure-traffic-manager-external-endpoints-and-weighted-round-robin-via-powershell/).

## <a name="next-steps"></a>Volgende stappen
Nu dat uw toepassing gemigreerde tooApp Service wordt, zijn er nog meer functies die u kunt gebruiken:

* Implementatie [staging-sleuven] kunt u toostage wijzigingen tooyour site en uitvoeren van A / B-tests.
* [WebJobs] bieden een vervanging voor On-demand geplande taken.
* U kunt [continu implementeren] uw site door koppelen aan uw site tooGitHub, TFS of volgt.
* U kunt [Application Insights] toomonitor uw site.
* Hallo dezelfde code dienst een website en een mobiele API uit.

### <a name="upgrading-your-site"></a>Een upgrade van uw Mobile Services site tooAzure Mobile Apps SDK
* Voor de server op basis van een Node.js-projecten Hallo nieuwe [Mobile Apps Node.js SDK] biedt verschillende nieuwe functies. Bijvoorbeeld: u kunt nu doen lokale ontwikkeling en foutopsporing, een Node.js-versie hoger 0.10 en aanpassen met een middleware Express.js.
* Voor. NET gebaseerde serverprojecten, nieuwe Hallo [Mobile Apps SDK NuGet-pakketten](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) meer flexibiliteit in NuGet afhankelijkheden hebben.  Deze pakketten Hallo nieuwe App Service-verificatie te ondersteunen en samenstellen met een ASP.NET-project. Zie voor meer informatie over het upgraden, [Upgrade van uw bestaande Mobile Service voor .NET-tooApp Service](app-service-mobile-net-upgrading-from-mobile-services.md).

<!-- Images -->
[0]: ./media/app-service-mobile-migrating-from-mobile-services/migrate-to-app-service-button.PNG
[1]: ./media/app-service-mobile-migrating-from-mobile-services/migration-activity-monitor.png
[2]: ./media/app-service-mobile-migrating-from-mobile-services/triggering-job-with-postman.png

<!-- Links -->
[App Service-prijzen]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[Application Insights]: ../application-insights/app-insights-overview.md
[Automatische schaling]: ../app-service-web/web-sites-scale.md
[Azure App Service]: ../app-service/app-service-value-prop-what-is.md
[Implementatiedocumentatie voor Azure App Service]: ../app-service-web/web-sites-deploy.md
[klassieke Azure-Portal]: https://manage.windowsazure.com
[Azure-portal]: https://portal.azure.com
[Azure Region]: https://azure.microsoft.com/en-us/regions/
[Azure Scheduler plannen]: ../scheduler/scheduler-plans-billing.md
[continu implementeren]: ../app-service-web/app-service-continuous-deployment.md
[Converteren van de gemengde naamruimten]: https://azure.microsoft.com/en-us/blog/updates-from-notification-hubs-independent-nuget-installation-model-pmt-and-more/
[curl]: http://curl.haxx.se/
[aangepaste domeinnamen]: ../app-service-web/web-sites-custom-domain-name.md
[Fiddler]: http://www.telerik.com/fiddler
[algemene beschikbaarheid van Azure App Service]: https://azure.microsoft.com/blog/announcing-general-availability-of-app-service-mobile-apps/
[hybride verbindingen]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[logboekregistratie]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Mobile Apps Node.js SDK]: https://github.com/azure/azure-mobile-apps-node
[tegenover Mobile Services. App Service]: app-service-mobile-value-prop-migration-from-mobile-services.md
[Notification Hubs]: ../notification-hubs/notification-hubs-push-notification-overview.md
[prestatiebewaking]: ../app-service-web/web-sites-monitor.md
[Postman]: http://www.getpostman.com/
[staging-sleuven]: ../app-service-web/web-sites-staged-publishing.md
[VNet]: ../app-service-web/web-sites-integrate-with-vnet.md
[WebJobs]: ../app-service-web/websites-webjobs-resources.md
[XDT transformeren voorbeelden]: https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples
[functies]: ../azure-functions/functions-overview.md
