---
title: Continue leveringsmethode voor cloud services met Visual Studio Online | Microsoft Docs
description: Meer informatie over het instellen van continue leveringsmethode voor Azure cloud-apps zonder opslagsleutel diagnostische gegevens opslaan in de configuratiebestanden van de service
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 148b2959-c5db-4e4a-a7e9-fccb252e7e8a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 7e70f92d4d1333ca6cbac5876e5ccbc763bd915c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-to-azure-using-visual-studio-online"></a>Securely Cloud Services Diagnostics opslagsleutel opslaan en Setup continue integratie en implementatie naar Azure met Visual Studio Online
 Het is een gebruikelijk om bronprojecten te openen tegenwoordig. Opslaan van de toepassing geheimen in configuratiebestanden is niet meer veilig practice als beveiligingsrisico's beschikbaar worden gesteld van geheimen van besturingselementen voor openbare gegevensbronnen wordt gelekt. Geheim opslaan als tekst zonder opmaak in een bestand in een pijplijn continue integratie niet beveiligd is ofwel omdat buildservers kunnen worden gedeeld met resources op de cloudomgeving. Dit artikel wordt uitgelegd hoe Visual Studio en Visual Studio Online vermindert de beveiligingsproblemen tijdens ontwikkeling en het proces voor continue integratie.

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a>Diagnostische gegevens opslag sleutel geheim verwijderen in het configuratiebestand van Project
Extensie voor diagnostische gegevens van cloud-Services vereist Azure-opslag voor het opslaan van resultaten van de diagnostische gegevens. Voorheen de verbindingsreeks voor opslag is opgegeven in de Cloud Services-configuratiebestanden (.cscfg) en kan worden ingecheckt met resourcebeheer. In de nieuwste Azure SDK-versie gewijzigd we het gedrag voor het opslaan van slechts een gedeeltelijke verbindingsreeks met de sleutel vervangen door een token. De volgende stappen wordt beschreven hoe de nieuwe Cloudservices tooling werkt:

### <a name="1-open-the-role-designer"></a>1. Open de rol designer
* Dubbelklik op of klik met de rechtermuisknop op een Cloud Services-rol rol designer openen

![Rol openen designer][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a>2. Onder de sectie diagnostische gegevens, het selectievakje nieuwe 'niet verwijderen geheim project-opslagsleutel' is toegevoegd
* Als u van de emulator van de lokale opslag gebruikmaakt, dit selectievakje is uitgeschakeld omdat er geen geheim beheren voor de lokale verbindingsreeks, UseDevelopmentStorage = true.

![Lokale opslag emulator-verbindingstekenreeks is geen geheime][1]

* Als u een nieuw project maakt, zijn is dit selectievakje standaard uitgeschakeld. Dit resulteert in de belangrijkste sectie van de opslag van de geselecteerde opslagverbindingsreeks wordt vervangen door een token. De waarde van het token worden gevonden in de huidige gebruiker AppData Roaming map, bijvoorbeeld: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService

> Houd er rekening mee dat de map user\AppData toegang beheerd door de gebruiker zich aanmelden en wordt beschouwd als een veilige plaats voor het opslaan van ontwikkeling geheimen.
> 
> 

![Opslagsleutel wordt opgeslagen in de gebruikersprofielmap][2]

### <a name="3-select-a-diagnostics-storage-account"></a>3. Selecteer een opslagaccount voor diagnostische gegevens
* Selecteer een opslagaccount van het dialoogvenster gestart door te klikken op de '...' te klikken. U ziet hoe de verbindingsreeks voor de opslag gegenereerde geen sleutel van het opslagaccount.
* Bijvoorbeeld: DefaultEndpointsProtocol = https; AccountName = contosostorage; AccountKey = $(*clouddiagstrg.key*)

### <a name="4----debugging-the-project"></a>4.    Foutopsporing voor het project
* F5 in Visual Studio foutopsporing te starten. Alles wat u moet werken op dezelfde manier als voor.
  ![Lokaal foutopsporing starten][3]

### <a name="5-publish-project-from-visual-studio"></a>5. Visual Studio-project publiceren
* Start het dialoogvenster publiceren en verdergaan met het aanmelden instructies voor het publiceren van de applicaion naar Azure.

### <a name="6-additional-information"></a>6. Aanvullende informatie
> Opmerking: Het paneel met toepassingsinstellingen in de ontwerpfunctie voor rol blijven omdat deze nu. Als u gebruiken van de geheime beheerfunctie voor diagnostische gegevens wilt, gaat u naar het tabblad configuraties.
> 
> 

![Instellingen toevoegen][4]

> Opmerking: Als ingeschakeld, de Application Insights-sleutel wordt opgeslagen als tekst zonder opmaak. De sleutel wordt alleen gebruikt voor het uploaden van inhoud, dus geen gevoelige gegevens risico wordt aangetast.
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a>Maken en publiceren van een Cloud Services-Project met behulp van Visual Studio online taaksjablonen
* De volgende stappen ziet u hoe continue integratie instellen voor Cloud Services-project met behulp van Visual Studio online taken:
  ### <a name="1----obtain-a-vso-account"></a>1.    Een account VSO verkrijgen
* [Visual Studio Online-account maken] [ Create Visual Studio Online account] als u nog niet hebt
* [Maken van teamproject] [ Create team project] in uw Visual Studio online-account

### <a name="2----setup-source-control-in-visual-studio"></a>2.    Setup van broncodebeheer in Visual Studio
* Verbinding maken met een teamproject

![Verbinding maken met teamproject][5]

![Selecteer teamproject verbinding maken met][6]

* Uw project toevoegen aan bronbeheer

![Project toevoegen aan bronbeheer][7]

![Project worden toegewezen aan een besturingselement bronmap][8]

* Controleer in uw project vanuit de Explorer-Team

![Controleer in het project met resourcebeheer][9]

### <a name="3----configure-build-process"></a>3.    Buildproces configureren
* Blader naar uw teamproject en voegt u een nieuwe buildproces sjablonen

![Een nieuwe build toevoegen][10]

* Selecteer opbouwtaak

![Een taak build toevoegen][11]

![Visual Studio bouwen taak sjabloon selecteren][12]

* Build taak invoer bewerken. Controleer de parameters build volgens uw behoeften aanpassen

![Opbouwtaak configureren][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* Build variabelen configureren

![Build variabelen configureren][14]

* Toevoegen van een taak voor het uploaden van build neerzetten

![Kies neerzetten opbouwtaak publiceren][15]

![Configureer neerzetten opbouwtaak publiceren][16]

* De build uitvoeren

![Nieuwe Wachtrijvorming][17]

![Overzicht van de build weergeven][18]

* Als de build geslaagd is ziet u een resultaat vergelijkbaar met hieronder

![Resultaat bouwen][19]

### <a name="4----configure-release-process"></a>4.    Release-proces configureren
* Een nieuwe release gemaakt

![Nieuwe release gemaakt][20]

* Selecteer de implementatie van Azure Cloud Services-taak

![Selecteer taak voor Azure Cloud Services-implementatie][21]

* Als de sleutel van het opslagaccount met resourcebeheer niet is ingeschakeld, moeten we de geheime sleutel voor het instellen van extensies van diagnostische gegevens opgeven. Vouw de **geavanceerde opties voor nieuwe Service maken** sectie en bewerkt u de **toegangscodes voor opslag van diagnostische gegevens** parameter invoer. Deze invoer nodig is op meerdere regels van sleutel-waardepaar in de indeling van **[RoleName]:$(StorageAccountKey)**

> Opmerking: als uw opslagaccount voor diagnostische gegevens onder hetzelfde abonnement is als waar u de Cloud Services-toepassing wilt publiceren, hebt u niet in te voeren van de sleutel in de invoer van de implementatie taak; de implementatie wordt programmatisch de storage-gegevens ophalen uit uw abonnement
> 
> 

![Taak voor Cloud Services-implementatie configureren][22]

* Gebruik geheim bouwen variabelen Opslagsleutels opslaan. Voor het maskeren van een variabele als geheim klikt u op het vergrendelingspictogram aan de rechterkant van de invoer-variabelen

![Opslagsleutels opslaan in geheime build variabelen][23]

* Een releaserecord maken en implementeren van uw project naar Azure

![Nieuwe release gemaakt][24]

## <a name="next-steps"></a>Volgende stappen
Raadpleeg voor meer informatie over het instellen van extensies van diagnostische gegevens voor Azure Cloud Services, [diagnostische gegevens in Azure Cloud Services met behulp van PowerShell inschakelen][Enable diagnostics in Azure Cloud Services using PowerShell]

[Create Visual Studio Online account]:https://www.visualstudio.com/team-services/
[Create team project]: https://www.visualstudio.com/it-it/docs/setup-admin/team-services/connect-to-visual-studio-team-services
[Enable diagnostics in Azure Cloud Services using PowerShell]:https://azure.microsoft.com/en-us/documentation/articles/cloud-services-diagnostics-powershell/

[0]: ./media/cloud-services-vs-ci/vs-01.png
[1]: ./media/cloud-services-vs-ci/vs-02.png
[2]: ./media/cloud-services-vs-ci/file-01.png
[3]: ./media/cloud-services-vs-ci/vs-03.png
[4]: ./media/cloud-services-vs-ci/vs-04.png
[5]: ./media/cloud-services-vs-ci/vs-05.png
[6]: ./media/cloud-services-vs-ci/vs-06.png
[7]: ./media/cloud-services-vs-ci/vs-07.png
[8]: ./media/cloud-services-vs-ci/vs-08.png
[9]: ./media/cloud-services-vs-ci/vs-09.png
[10]: ./media/cloud-services-vs-ci/vso-01.png
[11]: ./media/cloud-services-vs-ci/vso-02.png
[12]: ./media/cloud-services-vs-ci/vso-03.png
[13]: ./media/cloud-services-vs-ci/vso-04.png
[14]: ./media/cloud-services-vs-ci/vso-05.png
[15]: ./media/cloud-services-vs-ci/vso-06.png
[16]: ./media/cloud-services-vs-ci/vso-07.png
[17]: ./media/cloud-services-vs-ci/vso-08.png
[18]: ./media/cloud-services-vs-ci/vso-09.png
[19]: ./media/cloud-services-vs-ci/vso-10.png
[20]: ./media/cloud-services-vs-ci/vso-11.png
[21]: ./media/cloud-services-vs-ci/vso-12.png
[22]: ./media/cloud-services-vs-ci/vso-13.png
[23]: ./media/cloud-services-vs-ci/vso-14.png
[24]: ./media/cloud-services-vs-ci/vso-15.png
