---
title: aaaUsing hello Visual Studio publiceren Wizard Azure-toepassing | Microsoft Docs
description: Meer informatie over hoe tooconfigure verschillende instellingen in Visual Studio publiceren Wizard Azure-toepassing hello Hallo
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d8f1ac9-e439-47e0-a183-0642c4ea1920
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3f0b580d0054cc246372597660d8ae317d9b8686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-visual-studio-publish-azure-application-wizard"></a>Met behulp van Visual Studio publiceren Wizard Azure-toepassing hello
Nadat u een webtoepassing in Visual Studio ontwikkelen, kunt u die toepassing tooan Azure-cloudservice publiceren met behulp van Hallo **Publish Azure Application** wizard. 

> [!NOTE]
> Dit onderwerp gaat over het implementeren van services toocloud, niet tooweb sites. Zie voor meer informatie over het implementeren van tooweb sites [hoe een Azure-website tooDeploy](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false).
> 
> 

## <a name="accessing-hello-publish-azure-application-wizard"></a>Toegang tot Hallo Publish Azure Application wizard

Hallo Publish Azure Application wizard op twee manieren afhankelijk van Hallo type Visual Studio-project hebt, kunt u openen.

**Als u een Azure-cloud service-project hebt:**

1. Maak of open een Azure-cloud service-project in Visual Studio.

1. In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer in het contextmenu hello, **publiceren**.

**Als u een toepassing webproject dat niet is ingeschakeld voor Azure hebt:**

1. Maak of open een Azure-cloud service-project in Visual Studio.

1. In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer in het contextmenu hello, **converteren** > **tooAzure Cloudserviceproject converteren**. 

1. In **Solution Explorer**, met de rechtermuisknop op Hallo nieuw gemaakte Azure-project en, in het contextmenu hello, selecteert u **publiceren**.

## <a name="sign-in-page"></a>Aanmeldingspagina

![Aanmeldingspagina](./media/vs-azure-tools-publish-azure-application-wizard/sign-in.png)

**Account** : Selecteer een account of selecteer **account toevoegen** in de vervolgkeuzelijst Hallo-account.

**Kies uw abonnement** -Hallo abonnement toouse voor uw implementatie kiezen.
   
## <a name="settings-page---common-settings-tab"></a>Voor instellingenpagina - tabblad algemene instellingen   

![Algemene instellingen](./media/vs-azure-tools-publish-azure-application-wizard/settings-common-settings.png)

**Cloudservice** -Hallo dropdown gebruikt, selecteert u een bestaande cloud service of selecteer  **&lt;Nieuw >**, en maak een cloudservice. Hallo-Datacenter wordt tussen haakjes weergegeven voor elke cloudservice. Het is raadzaam dat Hallo center gegevenslocatie voor hello cloudservice Hallo dezelfde als Hallo data center locatie voor het opslagaccount hello (geavanceerde instellingen).  

**Omgeving** -optie **productie** of **fasering**. Kiezen staging-omgeving als u wilt dat toodeploy Hallo uw toepassing in een testomgeving. 

**Configuratie bouwen** -optie **Debug** of **Release**.

**Configuratie van de service** -optie **Cloud** of **lokale**.
   
**Extern bureaublad inschakelen voor alle functies** -controle van deze optie als u wilt dat toobe kunnen tooremotely connect toohello-service. Deze optie wordt voornamelijk gebruikt voor het oplossen van problemen. Als u dit selectievakje inschakelt, Hallo **configuratie voor extern bureaublad** dialoogvenster wordt weergegeven. Kies Hallo **instellingen** koppeling toochange Hallo configuratie.
   
**Web Deploy inschakelen voor alle functies van web** -deze optie, tooenable web implementatie voor Hallo-service controleren. U moet selecteren Hallo **extern bureaublad inschakelen voor alle rollen** optie toouse deze functie. Zie voor meer informatie [ [publiceren van een Azure-cloudservice met Visual Studio](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx). 

## <a name="settings-page---advanced-settings-tab"></a>Voor instellingenpagina - instellingen tabblad Geavanceerd

![Geavanceerde instellingen](./media/vs-azure-tools-publish-azure-application-wizard/settings-advanced-settings.png)

**Implementatielabel** -accepteer de standaardnaam Hallo of voer een naam van uw keuze. tooappend hello datum toohello implementatielabel, laat de eigenschap Hallo-selectievakje is ingeschakeld. 
   
**Storage-account** : Selecteer Hallo storage account toouse voor deze implementatie **&lt;Nieuw > toocreate een opslagaccount. Hallo-Datacenter wordt tussen haakjes weergegeven voor elke storage-account. Het is raadzaam dat Hallo center gegevenslocatie voor hello opslagaccount Hallo dezelfde als Hallo data center locatie voor de cloudservice hello (algemene instellingen).  
   
Hello Azure storage-account worden Hallo-pakket voor de implementatie van de toepassing hello opgeslagen. Nadat het Hallo-toepassing is geïmplementeerd, wordt Hallo pakket verwijderd uit Hallo storage-account.

**Verwijderen van implementatie bij fout** -Selecteer deze optie toohave Hallo implementatie verwijderd als er fouten tijdens de publicatie optreden. Dit moet worden uitgeschakeld als u wilt dat toomaintain een constante virtueel IP-adres voor de cloudservice.

**Implementatie-update** -Selecteer deze optie als u wilt dat toodeploy alleen de bijgewerkte componenten heeft. Dit type implementatie verloopt waarschijnlijk sneller dan een volledige implementatie. Dit moet worden gecontroleerd als u wilt dat toomaintain een constante virtueel IP-adres voor de cloudservice. 

**Implementatie-update - instellingen** -dit dialoogvenster wordt gebruikt toofurther aangeven hoe Hallo rollen toobe bijgewerkt. Als u ervoor kiest **incrementele update**, elk exemplaar van uw toepassing is bijgewerkt na de andere, zodat die toepassing hello altijd beschikbaar. Als u ervoor kiest **gelijktijdig bijwerken**, alle exemplaren van uw toepassing worden bijgewerkt op Hallo hetzelfde moment. Gelijktijdige bijwerken is sneller, maar de service mogelijk niet beschikbaar tijdens het updateproces Hallo. 

![Implementatie-instellingen](./media/vs-azure-tools-publish-azure-application-wizard/deployment-settings.png)

**Inschakelen van IntelliTrace** -opgeven of u wilt dat tooenable IntelliTrace. U kunt uitgebreide foutopsporingsinformatie voor een rolexemplaar van met IntelliTrace registreren wanneer deze wordt uitgevoerd in Azure. Als u toofind Hallo oorzaak van een probleem moet, kunt u Hallo IntelliTrace-logboeken toostep via uw code vanuit Visual Studio als in Azure werd uitgevoerd. Zie voor meer informatie over het gebruik van IntelliTrace [foutopsporing van een gepubliceerde Azure-cloudservice met Visual Studio en IntelliTrace](./vs-azure-tools-intellitrace-debug-published-cloud-services.md). 

**Schakel profilering** -opgeven of u tooenable prestaties profilering wilt. Hallo Visual Studio profiler kunt tooget een grondige analyse van Hallo rekenkundige aspecten van hoe uw cloudservice wordt uitgevoerd. Zie voor meer informatie over het gebruik van Visual Studio-profiler Hallo [Hallo prestaties van een Azure cloudservice testen](./vs-azure-tools-performance-profiling-cloud-services.md).

**Externe foutopsporing inschakelen voor alle rollen** -als u foutopsporing op afstand tooenable wilt opgeven. Zie voor meer informatie over foutopsporing van cloudservices met Visual Studio [foutopsporing van een Azure-cloudservice of virtuele machine in Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md).

## <a name="diagnostics-settings-page"></a>Diagnostische instellingen voor pagina

![Instellingen voor diagnostische gegevens](./media/vs-azure-tools-publish-azure-application-wizard/diagnostic-settings.png)

Diagnostische gegevens kunt u een Azure cloudservice tootroubleshoot (of virtuele machine van Azure). Zie voor meer informatie over diagnostische gegevens [diagnostische gegevens configureren voor Azure Cloud Services en virtuele Machines](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md). Zie voor meer informatie over Application Insights [wat is Application Insights?](./application-insights/app-insights-overview.md).

## <a name="summary-page"></a>Overzichtspagina

![Samenvatting](./media/vs-azure-tools-publish-azure-application-wizard/summary.png)

**Profiel als doel** -kunt u toocreate een publicatieprofiel Hallo-instellingen die u hebt gekozen. U kunt bijvoorbeeld een profiel voor een testomgeving en één voor productie maken. toosave dit profiel kiezen Hallo **opslaan** pictogram. Hallo Hallo-profiel wordt gemaakt en opgeslagen in Hallo Visual Studio-project. toomodify hello profielnaam open Hallo **profiel als doel** lijst en kies vervolgens **< beheren... >**.
   
   > [!NOTE]
   > Hallo publicatieprofiel wordt weergegeven in Solution Explorer in Visual Studio en Hallo profielinstellingen tooa-bestand met de extensie .azurePubxml worden geschreven. Instellingen worden opgeslagen als kenmerken van XML-codes.
   > 
   > 

## <a name="publishing-your-application"></a>Uw toepassing te publiceren

Als u alle Hallo-instellingen voor uw project implementatie configureert, selecteert u **publiceren** Hallo Hallo dialoogvenster onderaan in. U kunt de processtatus Hallo in Hallo bewaken **uitvoer** venster in Visual Studio.

## <a name="next-steps"></a>Volgende stappen
- [Migreer en publiceren van een webtoepassing tooan Azure cloudservice vanuit Visual Studio](./vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)
- [Meer informatie over hoe toouse Visual Studio toopublish een Azure-cloudservice](./vs-azure-tools-publishing-a-cloud-service.md)
- [Een gepubliceerde Azure-cloudservice met Visual Studio en IntelliTrace-foutopsporing](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)
- [Hallo-prestaties van een Azure cloudservice testen](./vs-azure-tools-performance-profiling-cloud-services.md)
- [Diagnostische gegevens configureren voor Azure-Cloudservices en virtuele Machines](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md). 
- [Wat is Application Insights?](./application-insights/app-insights-overview.md)