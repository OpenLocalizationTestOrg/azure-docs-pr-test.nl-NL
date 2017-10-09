---
title: aaaContinuous leveringsmethode voor cloud services met Visual Studio Online | Microsoft Docs
description: Meer informatie over hoe tooset up continue leveringsmethode voor Azure cloud-apps zonder op te slaan diagnostics opslagbestanden sleutel toohello service configuration
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
ms.openlocfilehash: dc87d049e46daf8b8a26ee4450ebd9b7910f287b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-tooazure-using-visual-studio-online"></a>Securely Cloud Services Diagnostics opslagsleutel opslaan en Setup continue integratie en implementatie tooAzure met behulp van Visual Studio Online
 Een algemene practice tooopen bronprojecten is tegenwoordig. Opslaan van de toepassing geheimen in configuratiebestanden is niet meer veilig practice als beveiligingsrisico's beschikbaar worden gesteld van geheimen van besturingselementen voor openbare gegevensbronnen wordt gelekt. Geheim opslaan als tekst zonder opmaak in een bestand in een pijplijn continue integratie niet beveiligd is gedeelde ofwel omdat buildservers kunnen bronnen op Hallo cloudomgeving. Dit artikel wordt uitgelegd hoe Visual Studio en Visual Studio Online vermindert Hallo beveiligingskwesties weergegeven tijdens het ontwikkelen en continue integratie-proces.

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a>Diagnostische gegevens opslag sleutel geheim verwijderen in het configuratiebestand van Project
Extensie voor diagnostische gegevens van cloud-Services vereist Azure-opslag voor het opslaan van resultaten van de diagnostische gegevens. Voorheen Hallo-verbindingsreeks voor opslag is opgegeven in Hallo Cloudservices (.cscfg) configuratiebestanden en toosource controle kan worden gecontroleerd. In de nieuwste Azure SDK versie Hallo gewijzigd we Hallo gedrag tooonly store een gedeeltelijke connection string met Hallo sleutel vervangen door een token. Hallo stappen wordt beschreven hoe Hallo nieuwe Cloudservices tooling werkt:

### <a name="1-open-hello-role-designer"></a>1. Hallo rol designer openen
* Dubbelklik op of klik met de rechtermuisknop op een Cloud Services-rol tooopen rol designer

![Rol openen designer][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a>2. Onder de sectie diagnostische gegevens, het selectievakje nieuwe 'niet verwijderen geheim project-opslagsleutel' is toegevoegd
* Als u van de lokale opslagemulator Hallo gebruikmaakt, dit selectievakje is uitgeschakeld omdat er geen geheime toomanage Hallo lokale verbindingsreeks, namelijk UseDevelopmentStorage = true.

![Lokale opslag emulator-verbindingstekenreeks is geen geheime][1]

* Als u een nieuw project maakt, zijn is dit selectievakje standaard uitgeschakeld. Dit resulteert in Hallo opslag sleutel sectie van de verbindingsreeks voor opslag van Hallo geselecteerd wordt vervangen door een token. Hallo waarde Hallo-token worden gevonden onder Hallo van de huidige gebruiker AppData Roaming map, bijvoorbeeld: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService

> Houd er rekening mee Hallo user\AppData map toegang beheerd is door de gebruiker zich aanmelden en wordt beschouwd als een veilige plaats toostore ontwikkeling geheimen.
> 
> 

![Opslagsleutel wordt opgeslagen in de gebruikersprofielmap][2]

### <a name="3-select-a-diagnostics-storage-account"></a>3. Selecteer een opslagaccount voor diagnostische gegevens
* Selecteer een opslagaccount van Hallo dialoogvenster gestart door te klikken op '...' Hallo te klikken. U ziet hoe Hallo opslagverbindingsreeks gegenereerd geen sleutel Hallo opslagaccount.
* Bijvoorbeeld: DefaultEndpointsProtocol = https; AccountName = contosostorage; AccountKey = $(*clouddiagstrg.key*)

### <a name="4----debugging-hello-project"></a>4.    Foutopsporing Hallo-project
* F5 toostart foutopsporing in Visual Studio. Alles wat u moet werken in Hallo dezelfde manier als voorheen.
  ![Lokaal foutopsporing starten][3]

### <a name="5-publish-project-from-visual-studio"></a>5. Visual Studio-project publiceren
* Start Hallo dialoogvenster publiceren en verdergaan met het aanmelden instructies toopublish hello applicaion tooAzure.

### <a name="6-additional-information"></a>6. Aanvullende informatie
> Opmerking: paneel met toepassingsinstellingen Hallo in Hallo rol designer blijven omdat deze nu. Als u wilt dat toouse Hallo geheime beheerfunctie voor diagnostische gegevens, gaat u toohello configuraties tabblad.
> 
> 

![Instellingen toevoegen][4]

> Opmerking: Als ingeschakeld, Hallo Application Insights sleutel wordt opgeslagen als tekst zonder opmaak. Hallo-sleutel wordt alleen gebruikt voor het uploaden van inhoud dus geen gevoelige gegevens risico wordt aangetast.
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a>Maken en publiceren van een Cloud Services-Project met behulp van Visual Studio online taaksjablonen
* Hallo stappen ziet u hoe toosetup continue integratie voor Cloud Services-project met behulp van Visual Studio online taken:
  ### <a name="1----obtain-a-vso-account"></a>1.    Een account VSO verkrijgen
* [Visual Studio Online-account maken] [ Create Visual Studio Online account] als u nog niet hebt
* [Maken van teamproject] [ Create team project] in uw Visual Studio online-account

### <a name="2----setup-source-control-in-visual-studio"></a>2.    Setup van broncodebeheer in Visual Studio
* Verbinding maken met tooa teamproject

![Verbinding maken met tooteam project][5]

![Team project tooconnect te selecteren][6]

* Uw project toosource besturingselement toevoegen

![Project toosource besturingselement toevoegen][7]

![Project tooa bronmap besturingselement toewijzen][8]

* Controleer in uw project vanuit de Explorer-Team

![Controleer in het project toosource besturingselement][9]

### <a name="3----configure-build-process"></a>3.    Buildproces configureren
* Blader tooyour teamproject en voegt u een nieuwe buildproces sjablonen

![Een nieuwe build toevoegen][10]

* Selecteer opbouwtaak

![Een taak build toevoegen][11]

![Visual Studio bouwen taak sjabloon selecteren][12]

* Build taak invoer bewerken. Hallo-build parameters volgens tooyour moeten aanpassen

![Opbouwtaak configureren][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* Build variabelen configureren

![Build variabelen configureren][14]

* Een taak tooupload build afname toevoegen

![Kies neerzetten opbouwtaak publiceren][15]

![Configureer neerzetten opbouwtaak publiceren][16]

* Hallo build uitvoeren

![Nieuwe Wachtrijvorming][17]

![Overzicht van de build weergeven][18]

* Als Hallo build geslaagd is ziet u een vergelijkbare toobelow resultaat

![Resultaat bouwen][19]

### <a name="4----configure-release-process"></a>4.    Release-proces configureren
* Een nieuwe release gemaakt

![Nieuwe release gemaakt][20]

* Selecteer hello Azure Cloud Services-implementatie taak

![Selecteer taak voor Azure Cloud Services-implementatie][21]

* Naarmate de opslagaccountsleutel Hallo niet toosource controle is ingeschakeld, moeten we toospecify Hallo geheime sleutel voor het instellen van extensies van diagnostische gegevens. Vouw Hallo **geavanceerde opties voor nieuwe Service maken** sectie en Hallo bewerken **Opslagaccountsleutels Diagnostics** parameter invoer. Deze invoer nodig is op meerdere regels van sleutel-waardepaar Hallo indeling **[RoleName]:$(StorageAccountKey)**

> Opmerking: als uw opslagaccount onder de ligt diagnostics hello hetzelfde abonnement als waar u Hallo Cloud Services-toepassing wilt publiceren, hebt u niet tooenter Hallo sleutel in de invoer voor Hallo implementatie taak; Hallo-implementatie wordt programmatisch Hallo storage-gegevens ophalen uit uw abonnement
> 
> 

![Taak voor Cloud Services-implementatie configureren][22]

* Gebruik geheim bouwen variabelen toosave Opslagsleutels. een variabele als geheim klikt u op Hallo vergrendelingspictogram aan de rechterkant Hallo Hallo toomask variabelen invoer

![Opslagsleutels opslaan in geheime build variabelen][23]

* Een releaserecord maken en implementeren van uw project tooAzure

![Nieuwe release gemaakt][24]

## <a name="next-steps"></a>Volgende stappen
Zie de toolearn meer informatie over het instellen van extensies van diagnostische gegevens voor Azure Cloud Services [diagnostische gegevens in Azure Cloud Services met behulp van PowerShell inschakelen][Enable diagnostics in Azure Cloud Services using PowerShell]

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
