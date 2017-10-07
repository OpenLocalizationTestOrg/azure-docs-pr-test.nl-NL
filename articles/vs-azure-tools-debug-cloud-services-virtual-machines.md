---
title: aaaDebugging een Azure cloud service of de virtuele machine in Visual Studio | Microsoft Docs
description: Foutopsporing van een Cloudservice of virtuele Machine in Visual Studio
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 945e06e0-2100-41af-b218-72347367ddab
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 32a326430021ba2ea9317a6a71fa005d4b87c273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-an-azure-cloud-service-or-virtual-machine-in-visual-studio"></a>Foutopsporing van een Azure-cloudservice of virtuele machine in Visual Studio
Visual Studio biedt verschillende opties voor het opsporen van Azure-cloudservices en virtuele machines.

## <a name="debug-your-cloud-service-on-your-local-computer"></a>Fouten opsporen in uw cloudservice op de lokale computer
U kunt opslaan tijd en geld met behulp van hello Azure compute-emulator toodebug uw cloudservice op een lokale computer. U kunt door foutopsporing lokaal een service in voordat u deze implementeert, betrouwbaarheid en prestaties verbeteren zonder te betalen voor compute-tijd. Echter een aantal fouten optreden alleen wanneer u een cloudservice uitvoert in Azure zelf. U kunt deze fouten opsporen als u foutopsporing op afstand inschakelen wanneer u uw service publiceren en koppel vervolgens Hallo foutopsporingsprogramma tooa rolinstantie.

Hallo-emulator simuleert hello Azure Compute-service en wordt uitgevoerd in uw lokale omgeving zodat u kunt testen en fouten opsporen in uw cloudservice voordat u deze implementeert. Hallo-emulator ingangen Hallo levenscyclus van uw rolinstanties en biedt toegang toosimulated resources, zoals lokale opslag. Wanneer u foutopsporing of uitvoeren van uw service vanuit Visual Studio, Hallo emulator automatisch gestart als een achtergrondtoepassing en implementeert vervolgens uw service toohello-emulator. U kunt de Hallo emulator tooview uw service wanneer deze wordt uitgevoerd in de lokale omgeving Hallo. U kunt uitvoeren Hallo volledige versie of express Hallo-versie van Hallo-emulator. (Vanaf Azure 2.3 kunt Hallo express-versie van de emulator Hallo is standaard Hallo.) Zie [tooRun Emulator Express gebruiken en een Cloud-Service lokaal foutopsporing](https://msdn.microsoft.com/library/dn339018.aspx).

### <a name="toodebug-your-cloud-service-on-your-local-computer"></a>toodebug uw cloud-service op de lokale computer
1. Kies op de menubalk Hallo **Debug**, **foutopsporing starten** toorun uw Azure-cloud service-project. Als alternatief kunt u op F5 drukken. U ziet een bericht dat Hallo Compute-Emulator wordt gestart. Wanneer het Hallo-emulator wordt gestart, wordt het door Hallo pictogram op de taakbalk bevestigt.

    ![Azure-emulator in het systeemvak Hallo](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC783828.png)
2. Hallo-gebruikersinterface voor Hallo rekenemulator weergeven door het Hallo snelmenu voor hello Azure pictogram in systeemvak Hallo openen en selecteer vervolgens **weergeven Compute-Emulator UI**.

    Hallo linkerdeelvenster Hallo UI Hallo-services die momenteel zijn geïmplementeerd toohello compute-emulator en Hallo rolexemplaren die elke service wordt uitgevoerd. U kunt Hallo service of functies toodisplay levenscyclus, logboekregistratie en diagnostische gegevens in het rechterdeelvenster Hallo. Als u Hallo focus in Hallo bovenmarge van een venster opgenomen, maar deze wordt uitgebreid toofill Hallo rechterdeelvenster.
3. Stap via Hallo-toepassing met de opdrachten op Hallo **Debug** menu's en onderbrekingspunten instellen in uw code. Tijdens het doorlopen van toepassing hello in Hallo foutopsporingsprogramma Hallo bijgewerkt met de huidige status van de toepassing hello Hallo. Wanneer u stopt met het opsporen van fouten, wordt Hallo-toepassingsimplementatie verwijderd. Als uw toepassing een Webrol bevat en u Hallo starten van de actie eigenschap toostart Hallo-webbrowser hebt ingesteld, wordt uw webtoepassing in de browser Hallo in Visual Studio gestart. Als u het aantal exemplaren van een rol in de serviceconfiguratie Hallo Hallo wijzigt, moet u uw cloudservice stoppen en opnieuw starten zodat u fouten voor deze nieuwe exemplaren van de rol Hallo opsporen kunt-foutopsporing.

    **Opmerking:** wanneer u stopt met het uitvoeren of foutopsporing van uw service Hallo lokale rekenemulator en opslagemulator niet worden gestopt. U moet ze expliciet stoppen van Hallo-systeemvak.

## <a name="debug-a-cloud-service-in-azure"></a>Fouten opsporen in een cloudservice in Azure
toodebug een cloudservice vanaf een externe computer, moet u inschakelen dat de functionaliteit expliciet wanneer u uw cloudservice implementeert, zodat de vereiste services (bijvoorbeeld msvsmon.exe) op Hallo virtuele machines met uw rolinstanties zijn geïnstalleerd. Als u niet foutopsporing op afstand inschakelen wanneer u Hallo service gepubliceerd, hebt u toorepublish Hallo service voor foutopsporing op afstand is ingeschakeld.

Als u foutopsporing op afstand voor een cloudservice inschakelt, kan deze niet slechtere prestaties levert of extra kosten. U kunt foutopsporing op afstand voor een productieservice niet gebruikt omdat clients die gebruikmaken van Hallo-service mogelijk nadelig worden beïnvloed.

> [!NOTE]
> Wanneer u een cloudservice vanuit Visual Studio publiceert, kunt u inschakelen **IntelliTrace** voor alle functies in die service die doel Hallo .NET Framework 4 of .NET Framework 4.5 Hallo. Met behulp van **IntelliTrace**, kunt u gebeurtenissen die hebben plaatsgevonden in een rolexemplaar van in de afgelopen Hallo onderzoeken en reproduceren Hallo context vanaf dat moment. Zie [foutopsporing van een gepubliceerde cloudservice met IntelliTrace en Visual Studio](http://go.microsoft.com/fwlink/?LinkID=623016) en [met behulp van IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx).
>
>

### <a name="tooenable-remote-debugging-for-a-cloud-service"></a>foutopsporing op afstand voor een cloudservice tooenable
1. Open de snelmenu Hallo voor hello Azure-project en selecteer vervolgens **publiceren**.
2. Selecteer Hallo **fasering** omgeving en Hallo **Debug** configuratie.

    Dit is slechts een richtlijn. U kunt ervoor kiezen toorun uw testomgevingen in een productieomgeving. U kan echter gebruikers nadelig beïnvloeden als u foutopsporing op afstand op Hallo productie-omgeving inschakelen. U kunt Hallo Release-configuratie, maar Hallo foutopsporing configuratie is foutopsporing gemakkelijker.

    ![Kies Hallo foutopsporing configuratie](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746717.gif)
3. Volg de gebruikelijke stappen Hallo maar selecteer Hallo **externe foutopsporing inschakelen voor alle rollen** selectievakje op Hallo **geavanceerde instellingen** tabblad.

    ![Fouten opsporen in configuratie](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746718.gif)

### <a name="tooattach-hello-debugger-tooa-cloud-service-in-azure"></a>tooattach hello foutopsporingsprogramma tooa cloudservice in Azure
1. Vouw in Server Explorer Hallo knooppunt voor de cloudservice.
2. Open Hallo snelmenu voor het Hallo-rol of functie exemplaar toowhich u wilt tooattach en selecteer vervolgens **foutopsporingsprogramma koppelen**.

    Als u fouten opsporen in een rol, koppelt de foutopsporingsfunctie Hallo tooeach exemplaar van deze rol. Hallo-foutopsporing verbreekt op een onderbrekingspunt voor het eerste rolexemplaar hello, die wordt uitgevoerd die regel en voldoet aan alle voorwaarden van deze onderbrekingspunt. Als u een exemplaar debug, gekoppeld Hallo foutopsporingsprogramma tooonly dat exemplaar en -einden op een onderbrekingspunt alleen wanneer dat specifieke exemplaar wordt uitgevoerd die regel en voldoet aan de voorwaarden van onderbrekingspunt Hallo.

    ![Foutopsporingsprogramma koppelen](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746719.gif)
3. Nadat het Hallo-foutopsporingsprogramma koppelt tooan exemplaar, zoals gebruikelijk foutopsporing. Hallo-foutopsporingsprogramma worden automatisch de juiste hostproces toohello voor uw rol gekoppeld. Afhankelijk van welke Hallo-rol is, Hallo debugger wordt toow3wp.exe, WaWorkerHost.exe of WaIISHost.exe. tooverify hello proces toowhich Hallo foutopsporing is gekoppeld, vouw Hallo exemplaar knooppunt in Server Explorer. Zie [Azure rol architectuur](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx) voor meer informatie over Azure-processen.

    ![Dialoogvenster voor code-type selecteren](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
4. tooidentify hello processen toowhich Hallo foutopsporing is gekoppeld, Hallo processen het dialoogvenster openen door op Hallo menubalk, foutopsporing, Windows, processen te kiezen. (Toetsenbord: Ctrl + Alt + Z) toodetach een specifiek proces het snelmenu openen en selecteer vervolgens **loskoppelen proces**. Of, Hallo exemplaar knooppunt niet vinden in Server Explorer, Hallo proces vinden, opent u het snelmenu en selecteer vervolgens **loskoppelen proces**.

    ![Processen voor foutopsporing](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC690787.gif)

> [!WARNING]
> Lange wordt gestopt bij onderbrekingspunten wanneer externe voorkomen foutopsporing. Azure beschouwt een proces dat langer dan een paar minuten als niet-reagerende wordt gestopt en stopt met het verzenden van verkeer toothat exemplaar. Als u al lang stopt, losgekoppeld msvsmon.exe van Hallo-proces.
>
>

toodetach hello foutopsporingsprogramma van alle processen in uw exemplaar of de rol, open Hallo snelmenu voor Hallo functie of het exemplaar dat u fouten opspoort in en selecteer vervolgens **loskoppelen foutopsporingsprogramma**.

## <a name="limitations-of-remote-debugging-in-azure"></a>Beperkingen van foutopsporing op afstand in Azure
Van de Azure SDK 2.3 heeft foutopsporing op afstand Hallo beperkingen te volgen.

* Met foutopsporing op afstand is ingeschakeld, kunt u een cloudservice waarin een rol meer dan 25 exemplaren heeft niet publiceren.
* Hallo-foutopsporingsprogramma gebruikt 30400 too30424 poorten, 31400 too31424 en 32400 too32424. Als u toouse een van deze poorten probeert, u niet kunt toopublish uw service en een van de volgende foutberichten hello wordt weergegeven in het gebeurtenissenlogboek Hallo voor Azure:

  * Fout bij het valideren van bestand van de Hallo cscfg tegen Hallo csdef-bestand.
    poortbereik 'range' Hello gereserveerd voor het eindpunt die Microsoft.windowsazure.plugins.remotedebugger.connector van de rol 'rol' met een reeds gedefinieerde poort of een bereik overlapt.
  * Toewijzing is mislukt. Probeer het later opnieuw, Verminder Hallo VM-grootte of het aantal rolinstanties of probeer andere regio tooa implementeren.

## <a name="debugging-azure-virtual-machines"></a>Foutopsporing van virtuele machines in Azure
U kunt fouten opsporen in programma's die worden uitgevoerd op virtuele machines in Azure met behulp van de Server Explorer in Visual Studio. Wanneer u foutopsporing op afstand op een virtuele machine van Azure inschakelt, installeert Azure Hallo-extensie voor externe foutopsporing op Hallo virtuele machine. U kunt vervolgens tooprocesses op Hallo virtuele machine te koppelen en fouten opsporen in normaal.

> [!NOTE]
> Virtuele machines die zijn gemaakt via hello Azure resource manager-stack kan op afstand fouten opgespoord via Cloud Explorer in Visual Studio 2015. Zie voor meer informatie [Azure-Resources beheren met Cloud Explorer](http://go.microsoft.com/fwlink/?LinkId=623031).
>
>

### <a name="toodebug-an-azure-virtual-machine"></a>toodebug Azure een virtuele machine
1. Vouw in Server Explorer Hallo virtuele Machines en selecteer Hallo knooppunten van Hallo virtuele machine die u toodebug wilt.
2. Hallo contextmenu te openen en selecteer **inschakelen foutopsporing**. Wanneer u wordt gevraagd of u zeker als u wilt dat tooenable foutopsporing op Hallo virtuele machine, selecteer **Ja**.

    Azure installeert externe foutopsporing extensie Hallo Hallo virtuele machine tooenable om op te lossen.

    ![Virtuele machine foutopsporing-opdracht inschakelen](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Activiteitenlogboek van Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)
3. Nadat Hallo externe foutopsporing extensie installatie heeft voltooid, opent u contextmenu Hallo virtuele machine en selecteer **foutopsporingsprogramma koppelen...**

    Azure opgehaald van een lijst met Hallo processen op Hallo virtuele machine en laat ze in het dialoogvenster Hallo Attach-tooProcess.

    ![De opdracht foutopsporingsprogramma koppelen](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)
4. In Hallo **koppelen tooProcess** dialoogvenster, **Selecteer** toolimit Hallo resultaten lijst tooshow alleen Hallo typen code dat u wilt dat toodebug. U kunt fouten opsporen 32 - of 64-bits beheerde code, systeemeigen code of beide.

    ![Dialoogvenster voor code-type selecteren](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
5. Selecteer Hallo processen u wilt toodebug op Hallo virtuele machine en selecteer vervolgens **Attach**. U kunt bijvoorbeeld Hallo w3wp.exe-proces selecteren als u deze toodebug een web-app op Hallo virtuele machine wilde. Zie [fouten opsporen in een of meer processen in Visual Studio](https://msdn.microsoft.com/library/jj919165.aspx) en [Azure rol architectuur](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx) voor meer informatie.

## <a name="create-a-web-project-and-a-virtual-machine-for-debugging"></a>Maak een webproject en een virtuele machine voor het opsporen van fouten
Voordat u uw Azure-project publiceert, het wellicht handig tootest in een ingesloten omgeving die ondersteuning biedt voor foutopsporing en testen van scenario's en waar u testen en controleren of programma's kunt installeren. Eenzijdige toodo dit is tooremotely fouten opsporen in uw app op een virtuele machine.

Visual Studio ASP.NET-projecten bieden een optie toocreate een handige virtuele machine die u voor het testen van de app gebruiken kunt. Hallo virtuele machine bevat meestal nodig eindpunten zoals PowerShell, extern bureaublad en Web Deploy.

### <a name="toocreate-a-web-project-and-a-virtual-machine-for-debugging"></a>toocreate een webproject en een virtuele machine voor foutopsporing
1. In Visual Studio maakt een nieuwe ASP.NET-webtoepassing.
2. In het dialoogvenster Nieuw ASP.NET-Project hello, in hello Azure sectie kiezen **virtuele Machine** in de vervolgkeuzelijst Hallo. Hallo laat **maken van externe bronnen** selectievakje is ingeschakeld. Selecteer **OK** tooproceed.

    Hallo **virtuele machine in Azure maken** dialoogvenster wordt weergegeven.

    ![Dialoogvenster voor ASP.NET web project maken](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746723.png)

    **Opmerking:** wordt u gevraagd toosign in tooyour Azure-account als u nog niet bent aangemeld.

1. Selecteer Hallo verschillende instellingen voor Hallo virtuele machine en selecteer vervolgens **OK**. Zie [virtuele Machines](http://go.microsoft.com/fwlink/?LinkId=623033) voor meer informatie.

    Hallo-naam die u voor DNS-naam invoert worden Hallo-naam van Hallo virtuele machine.

    ![Virtuele machine op in het dialoogvenster Azure maken](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746724.png)

    Azure maakt Hallo virtuele machine en vervolgens de bepalingen en configureert u Hallo eindpunten, zoals Extern bureaublad- en Web Deploy
2. Na het Hallo virtuele machine volledig is geconfigureerd, selecteert u knooppunt Hallo virtuele machine in Server Explorer.
3. Hallo contextmenu te openen en selecteer **inschakelen foutopsporing**. Wanneer u wordt gevraagd of u zeker als u wilt dat tooenable foutopsporing op Hallo virtuele machine, selecteer **Ja**.

    Azure installeert Hallo foutopsporing extensie toohello virtuele machine tooenable foutopsporing op afstand.

    ![Virtuele machine foutopsporing-opdracht inschakelen](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Activiteitenlogboek van Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)
4. Publiceren van uw project, zoals wordt beschreven in [procedure: een Web-Project met één klik publiceren in Visual Studio implementeren](https://msdn.microsoft.com/library/dd465337.aspx). Omdat u wilt dat toodebug op Hallo virtuele machine op Hallo **instellingen** pagina Hallo **webpublicatie** wizard selecteert u **Debug** als Hallo-configuratie. Dit zorgt ervoor dat de symbolen code beschikbaar tijdens het opsporen van fouten zijn.

    ![Publicatie-instellingen](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718349.png)
5. In Hallo **opties voor het publiceren van bestand**, selecteer **aanvullende bestanden op de bestemming verwijderen** als Hallo project is al geïmplementeerd op een eerder tijdstip.
6. Nadat het Hallo-project wordt gepubliceerd, in het contextmenu Hallo virtuele machine in Server Explorer, selecteert u **foutopsporingsprogramma koppelen...**

    Azure opgehaald van een lijst met Hallo processen op Hallo virtuele machine en laat ze in het dialoogvenster Hallo Attach-tooProcess.

    ![De opdracht foutopsporingsprogramma koppelen](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)
7. In Hallo **koppelen tooProcess** dialoogvenster, **Selecteer** toolimit Hallo resultaten lijst tooshow alleen Hallo typen code dat u wilt dat toodebug. U kunt fouten opsporen 32 - of 64-bits beheerde code, systeemeigen code of beide.

    ![Dialoogvenster voor code-type selecteren](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
8. Selecteer Hallo processen u wilt toodebug op Hallo virtuele machine en selecteer vervolgens **Attach**. U kunt bijvoorbeeld Hallo w3wp.exe-proces selecteren als u deze toodebug een web-app op Hallo virtuele machine wilde. Zie [fouten opsporen in een of meer processen in Visual Studio](https://msdn.microsoft.com/library/jj919165.aspx) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen
* Gebruik **Intellitrace** toocollect een logboek van aanroepen en gebeurtenissen van een release-server. Zie [foutopsporing van een gepubliceerde Cloudservice met IntelliTrace en Visual Studio](http://go.microsoft.com/fwlink/?LinkID=623016).
* Gebruik **Azure Diagnostics** toolog gedetailleerde informatie in rollen, code wordt uitgevoerd of Hallo functies worden uitgevoerd in de ontwikkelomgeving Hallo of in Azure. Zie [logboekgegevens verzamelen met behulp van Azure Diagnostics](http://go.microsoft.com/fwlink/p/?LinkId=400450).
