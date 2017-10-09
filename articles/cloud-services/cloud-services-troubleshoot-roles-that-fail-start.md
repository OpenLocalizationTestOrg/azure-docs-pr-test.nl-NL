---
title: aaaTroubleshoot-functies die niet voldoen aan toostart | Microsoft Docs
description: Hier volgen enkele veelvoorkomende redenen waarom een Service in de Cloud-rol toostart kan mislukken. Oplossingen voor problemen toothese worden ook gegeven.
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: e2fbecb08a10984add79dfc74e73de6869bb314f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-toostart"></a>Cloudservice-functies die niet voldoen aan toostart oplossen
Hier volgen enkele veelvoorkomende problemen en oplossingen gerelateerde tooAzure Cloud Services-functies die niet voldoen aan toostart.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a>Ontbrekende dll's of afhankelijkheden
Niet-reagerende rollen en functies die zijn functioneert tussen **Bezig met initialiseren**, **bezet**, en **stoppen** statussen kunnen zijn veroorzaakt door ontbrekende dll-bestanden of assembly's.

Problemen met ontbrekende dll's of assembly's zijn:

* De rolinstantie is doorlopen **Bezig met initialiseren**, **bezet**, en **stoppen** statussen.
* Uw rolexemplaar is verplaatst, te**gereed** , maar als u de webtoepassing tooyour navigeert, Hallo pagina wordt niet weergegeven.

Er zijn verschillende aanbevolen methoden om deze problemen te onderzoeken.

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a>Vaststellen van problemen met ontbrekende dll-bestand in een Webrol
Wanneer u tooa-website die wordt geïmplementeerd in een Webrol navigeren en een server fout vergelijkbare toohello volgende wordt weergegeven in Hallo browser, kan dit wijzen op een DLL-bestand ontbreekt.

![Serverfout in '/' toepassing.](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a>Problemen vaststellen door het uitschakelen van aangepaste fouten
Gedetailleerde foutinformatie kan worden bekeken door Hallo web.config voor Hallo web rol tooset Hallo aangepaste fout modus tooOff configureren en het Hallo-service opnieuw te implementeren.

fouten tooview meer voltooid zonder te maken met extern bureaublad:

1. Hallo-oplossing in Microsoft Visual Studio openen.
2. In Hallo **Solution Explorer**, Hallo web.config-bestand vinden en te openen.
3. Zoek de sectie system.web Hallo in Hallo web.config-bestand en Hallo volgt regel toevoegen:

    ```xml
    <customErrors mode="Off" />
    ```
4. Hallo-bestand opslaan.
5. Opnieuw verpakken en implementeer Hallo-service opnieuw.

Wanneer het Hallo-service is geïmplementeerd, ziet u een foutbericht met de naam van de Hallo Hallo assembly- of DLL-bestand ontbreekt.

## <a name="diagnose-issues-by-viewing-hello-error-remotely"></a>Problemen vaststellen door op afstand Hallo fout weer te geven
U kunt Extern bureaublad tooaccess Hallo rol gebruiken en gedetailleerde foutinformatie extern weergeven. Volgende stappen tooview Hallo fouten met behulp van extern bureaublad hello gebruiken:

1. Zorg ervoor dat de Azure SDK 1.3 of hoger is geïnstalleerd.
2. Tijdens de implementatie van Hallo-oplossing met behulp van Visual Studio hello te kiezen '... verbindingen met extern bureaublad configureren'. Zie voor meer informatie over het configureren van extern bureaublad-verbinding Hallo [met behulp van extern bureaublad met de Azure-rollen](../vs-azure-tools-remote-desktop-roles.md).
3. In Hallo Microsoft klassieke Azure portal, zodra het Hallo-exemplaar wordt de status van **gereed**, klikt u op een Hallo rolinstanties.
4. Klikt u op Hallo **Connect** pictogram in Hallo **RAS** gebied van Hallo-lint.
5. Meld u toohello virtuele machine met behulp van Hallo-referenties die zijn opgegeven bij de configuratie van extern bureaublad Hallo.
6. Open een opdrachtvenster.
7. Typ `IPconfig`.
8. Noteer de waarde van het Hallo IPV4-adres.
9. Open Internet Explorer.
10. Typ Hallo-adres en de naam van de Hallo van Hallo-webtoepassing. Bijvoorbeeld `http://<IPV4 Address>/default.aspx`.

Navigeren toohello retourneert website nu gedetailleerde foutberichten:

* Serverfout in '/' toepassing.
* Beschrijving: Er is een onverwerkte uitzondering opgetreden tijdens het uitvoeren van de huidige webaanvraag Hallo Hallo. Bekijk Hallo stacktracering voor meer informatie over de fout Hallo en oorsprong ervan in Hallo-code.
* Details van uitzondering: System.IO.FIleNotFoundException: kan niet worden geladen, bestand of assembly ' Microsoft.WindowsAzure.StorageClient, versie 1.1.0.0, Culture = neutral, PublicKeyToken = 31bf856ad364e35 =' of een van de afhankelijkheden ervan. Hallo vinden bestand niet Hallo opgegeven.

Bijvoorbeeld:

![Expliciete Serverfout in '/' toepassing](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-hello-compute-emulator"></a>Problemen met behulp van de rekenemulator Hallo vaststellen
U kunt gebruiken Hallo Microsoft Azure compute-emulator toodiagnose en oplossen van problemen met ontbrekende afhankelijkheden en fouten van web.config.

Voor de beste resultaten bij het gebruik van deze methode van de diagnose van, moet u een computer of virtuele machine waarop een schone installatie van Windows is. toobest hello Azure-omgeving te simuleren, gebruikt u Windows Server 2008 R2 x64.

1. Installeer Hallo zelfstandige versie van Hallo [Azure SDK](https://azure.microsoft.com/downloads/).
2. Op de ontwikkelcomputer hello, Hallo cloudserviceproject te bouwen.
3. Navigeer in Windows Verkenner toohello bin\debug map van Hallo cloudserviceproject.
4. Hallo .csx map- en .cscfg-bestand toohello computer dat u van toodebug Hallo problemen gebruikmaakt kopiëren.
5. Open op Hallo schone computer, een Azure SDK-opdrachtpromptvenster en typ `csrun.exe /devstore:start`.
6. Typ het volgende achter de opdrachtprompt Hallo `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.
7. Wanneer de rol Hallo wordt gestart, ziet u de gedetailleerde foutinformatie in Internet Explorer. U kunt ook de standaard-Windows-hulpprogramma's voor probleemoplossing toofurther diagnose Hallo probleem.

## <a name="diagnose-issues-by-using-intellitrace"></a>Problemen met behulp van IntelliTrace vaststellen
Voor worker en webservice-functies die er gebruik van .NET Framework 4, kunt u [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), die beschikbaar is in Microsoft Visual Studio Enterprise.

Volg deze stappen toodeploy Hallo-service met IntelliTrace ingeschakeld:

1. Controleer of de Azure SDK 1.3 of hoger is geïnstalleerd.
2. Hallo-oplossing implementeren met behulp van Visual Studio. Tijdens de implementatie controleren Hallo **IntelliTrace inschakelen voor .NET 4 rollen** selectievakje.
3. Zodra het Hallo-exemplaar wordt gestart, opent u Hallo **Server Explorer**.
4. Vouw Hallo **Azure\\Cloudservices** knooppunt en zoek Hallo-implementatie.
5. Vouw Hallo implementatie totdat er Hallo rolinstanties. Met de rechtermuisknop op een van de Hallo-exemplaren.
6. Kies **weergave IntelliTrace-logboeken**. Hallo **IntelliTrace samenvatting** wordt geopend.
7. Ga naar Hallo uitzonderingen sectie Hallo samenvatting. Als er uitzonderingen, Hallo sectie heet **uitzonderingsgegevens**.
8. Vouw Hallo **uitzonderingsgegevens** en zoekt u **System.IO.FileNotFoundException** fouten vergelijkbare toohello volgende:

![Uitzonderingsgegevens, ontbreekt een bestand of assembly](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a>Adres van de ontbrekende dll's en verzamelingen
DLL-bestand en de assembly-fouten, ontbrekende tooaddress als volgt te werk:

1. Hallo-oplossing in Visual Studio openen.
2. In **Solution Explorer**Open Hallo **verwijzingen** map.
3. Klik op Hallo assembly in Hallo fout geïdentificeerd.
4. In Hallo **eigenschappen** deelvenster, zoek **lokale kopie van de eigenschap** en stelt u Hallo waarde te**True**.
5. Implementeer Hallo cloud-service opnieuw in.

Zodra u hebt gecontroleerd dat alle fouten hebt gecorrigeerd, kunt u Hallo service implementeren zonder te controleren of Hallo **IntelliTrace inschakelen voor .NET 4 rollen** selectievakje.

## <a name="next-steps"></a>Volgende stappen
Meer [probleemoplossing artikelen](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) voor cloudservices.

Zie hoe tootroubleshoot cloud service rol problemen met behulp van Azure PaaS computer diagnostische gegevens toolearn [blogreeks van Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
