---
title: een Cloud Service lokaal in Hallo Compute-Emulator aaaProfiling | Microsoft Docs
services: cloud-services
description: Het onderzoeken van prestatieproblemen in cloudservices met Visual Studio-profiler Hallo
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
tags: 
ms.assetid: 25e40bf3-eea0-4b0b-9f4a-91ffe797f6c3
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: fc37c85dad4db4cc0310f73afad56fc0fe5f3963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a>Hallo prestaties van een Cloud-Service lokaal in Hallo hello Azure Compute-Emulator met behulp van Visual Studio Profiler testen
Tal van hulpprogramma's en technieken zijn beschikbaar voor het Hallo-prestaties van cloudservices testen.
Wanneer u een cloud service tooAzure publiceert, kunt u Visual Studio profileringsgegevens verzamelen en deze vervolgens te analyseren hebt lokaal, zoals beschreven in [profileren van een Azure-toepassing][1].
U kunt ook diagnostische gegevens tootrack tal van de prestaties van tellers, zoals beschreven in [met behulp van de prestatiemeteritems in Azure][2].
U kunt uw toepassing lokaal in de rekenemulator Hallo voordat u deze toohello cloud implementeert ook tooprofile.

In dit artikel bevat informatie over Hallo CPU steekproeven methode van profilering, die kan lokaal worden uitgevoerd in Hallo-emulator. CPU-steekproeven is een methode voor het samenstellen van profiel die niet zeer hoog. Hallo profiler maakt op een aangewezen steekproefinterval een momentopname van Hallo aanroepstack. Hallo gegevens gedurende een periode worden verzameld en weergegeven in een rapport. Deze methode van profilering doorgaans tooindicate waarbij in een toepassing rekenkracht meeste Hallo CPU werk wordt uitgevoerd.  Dit biedt u toofocus kans op Hallo 'hot pad' Hallo waar uw toepassing uitgeeft Hallo meeste tijd.

## <a name="1-configure-visual-studio-for-profiling"></a>1: Visual Studio voor profilering configureren
Er zijn eerst enkele Visual Studio-configuratieopties die nuttig zijn kunnen bij het samenstellen van profiel. toomake beeld krijgt van Hallo profilering rapporten, moet u symbolen (.pdb-bestanden) voor uw toepassing en ook symbolen voor systeembibliotheken. Moet u ervoor dat u verwijst naar Hallo beschikbaar symbool servers toomake. toodo dit op Hallo **extra** in het menu in Visual Studio **opties**, en kies vervolgens **foutopsporing**, klikt u vervolgens **symbolen**. Zorg ervoor dat Microsoft symbool Servers wordt vermeld onder **symbool bestandslocaties (.pdb)**.  U kunt ook verwijzen naar http://referencesource.microsoft.com/symbols deze heeft mogelijk extra symboolbestanden.

![Symboolopties][4]

Indien gewenst, kunt u vereenvoudigen Hallo rapporten die profiler Hallo door in te stellen alleen mijn Code genereert. Met alleen mijn Code is ingeschakeld, worden functie aanroep stacks vereenvoudigd zodat die volledig interne toolibraries aanroept en Hallo .NET Framework zijn verborgen voor Hallo-rapporten. Op Hallo **extra** menu kiezen **opties**. Vouw vervolgens Hallo **prestatiehulpprogramma's** knooppunt, en kies **algemene**. Schakel dit selectievakje in Hallo voor **inschakelen alleen mijn Code voor de profiler rapporten**.

![Alleen mijn Code opties][17]

U kunt deze instructies met een bestaand project of met een nieuw project.  Als u een nieuw project tootry Hallo hieronder beschreven technieken maakt, kiest u een C# **Azure Cloud Service** project en selecteer een **Webrol** en een **Werkrol**.

![Azure Cloud Service-Projectrollen][5]

Bijvoorbeeld toevoegen doeleinden, sommige tooyour CodeProject die ervoor zorgt dat veel tijd ziet u enkele duidelijk prestatieprobleem. Bijvoorbeeld, voeg Hallo code tooa werkrolproject te volgen:

    public class Concatenator
    {
        public static string Concatenate(int number)
        {
            int count;
            string s = "";
            for (count = 0; count < number; count++)
            {
                s += "\n" + count.ToString();
            }
            return s;
        }
    }

Deze code aanroepen vanuit Hallo RunAsync-methode in Hallo-werkrol van RoleEntryPoint afgeleide klasse. (Negeren Hallo-waarschuwing over Hallo methode synchroon uitgevoerd.)

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

Bouwen en uitvoeren van uw cloudservice lokaal zonder foutopsporing (Ctrl + F5) met Hallo oplossing configuratieset te**Release**. Dit zorgt ervoor dat alle bestanden en mappen worden gemaakt voor het Hallo-toepassing lokaal uitvoert en zorgt ervoor dat alle Hallo emulators worden gestart. Hallo Compute-Emulator UI starten vanuit Hallo taakbalk tooverify die uw werkrol wordt uitgevoerd.

## <a name="2-attach-tooa-process"></a>2: tooa proces koppelen
In plaats van de toepassing hello vanaf Hallo Visual Studio 2010 IDE profilering, koppelt u Hallo profiler tooa process uitgevoerd. 

tooattach hello profiler tooa proces, op Hallo **analyseren** menu kiezen **Profiler** en **Attach/Detach**.

![Optie profiel koppelen][6]

Voor een werkrol vinden Hallo WaWorkerHost.exe proces.

![WaWorkerHost proces][7]

Als de projectmap zich op een netwerkstation bevindt, wordt Hallo profiler u gevraagd tooprovide een andere locatie toosave Hallo profileren van rapporten.

 U kunt ook tooa Webrol koppelen door het tooWaIISHost.exe koppelen.
Als er meerdere werkprocessen functie in uw toepassing, moet u toouse Hallo processID toodistinguish ze. U kunt Hallo processID programmatisch opvragen door het openen van het procesobject Hallo. Bijvoorbeeld als u deze code toohello-Run-methode van Hallo RoleEntryPoint afgeleide klasse aan een rol toevoegen, kunt u het logboek in bekijken Hallo Compute-Emulator UI tooknow welke tooconnect proces aan.

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

tooview hello logboek start Hallo Compute-Emulator gebruikersinterface.

![Hallo Compute-Emulator UI starten][8]

Hallo worker-rol logboek-consolevenster in Hallo Compute-Emulator UI door te klikken op de titelbalk Hallo consolevenster openen Hallo proces-ID in Hallo logboek, kunt u zien.

![Proces-ID weergeven][9]

Een u hebt gekoppeld, Hallo stappen uitvoeren in uw toepassing UI (indien nodig) tooreproduce Hallo scenario.

Als u wilt dat toostop profilering, kiest u Hallo **stoppen profilering** koppeling.

![Profileren van de optie stoppen][10]

## <a name="3-view-performance-reports"></a>3: prestatierapporten weergeven
Rapport over systeemprestaties Hallo voor uw toepassing wordt weergegeven.

Op dit moment Hallo profiler stopt met het uitvoeren van gegevens worden opgeslagen in een bestand .vsp en een rapport een analyse van deze gegevens bevat worden weergegeven.

![Profiler rapport][11]

Als u String.wstrcpy in Hot pad hello, klikt u op alleen mijn Code toochange Hallo weergave tooshow gebruikerscode alleen ziet.  Als u String.Concat ziet, kunt u Hallo alle Code weergeven knop.

U ziet Hallo samenvoegen methode en een groot deel van de uitvoeringstijd Hallo inneemt String.Concat.

![Analyse van rapport][12]

Als u Hallo tekenreeks samenvoeging code in dit artikel hebt toegevoegd, ziet u een waarschuwing in de lijst met taken Hallo voor deze. U ziet ook een waarschuwing dat er een uitzonderlijk groot aantal garbagecollection is, vervalt toohello aantal tekenreeksen die zijn gemaakt en verwijderd.

![Waarschuwingen voor prestaties][14]

## <a name="4-make-changes-and-compare-performance"></a>4: wijzigingen aanbrengen en vergelijkt u prestaties
U kunt ook Hallo prestaties voor en na een codewijziging vergelijken.  Hallo process uitgevoerd stoppen en Hallo code tooreplace Hallo samenvoeging bewerking van de tekenreeks met Hallo gebruik van StringBuilder bewerken:

    public static string Concatenate(int number)
    {
        int count;
        System.Text.StringBuilder builder = new System.Text.StringBuilder("");
        for (count = 0; count < number; count++)
        {
             builder.Append("\n" + count.ToString());
        }
        return builder.ToString();
    }

Uitvoeren van een andere prestaties doen, en vervolgens vergelijken Hallo prestaties. In Hallo prestaties Explorer, als hello wordt uitgevoerd, zich in Hallo dezelfde sessie, u kunt alleen beide rapporten te selecteren, snelmenu Hallo openen en kies **prestatierapporten vergelijken**. Als u toocompare met een wordt uitgevoerd in een andere prestatiesessie wilt, open Hallo **analyseren** menu en kies **prestatierapporten vergelijken**. Geef beide bestanden in Hallo dialoogvenster dat wordt weergegeven.

![Optie voor prestaties van rapporten vergelijken][15]

Hallo rapporten Markeer verschillen tussen Hallo twee wordt uitgevoerd.

![Van vergelijkingsrapport][16]

Gefeliciteerd. U slag bent gegaan met Hallo profiler.

## <a name="troubleshooting"></a>Problemen oplossen
* Controleer of u een Release-build zijn profilering en starten zonder foutopsporing.
* Als Hallo Attach/Detach optie is niet ingeschakeld op Hallo Profiler menu, voert u Hallo prestaties Wizard.
* Hallo Compute-Emulator UI tooview Hallo status van uw toepassing gebruiken. 
* Als er problemen optreden bij het starten van toepassingen in Hallo-emulator of profiler koppelen hello, Hallo rekenemulator afsluiten en opnieuw. Als dit Hallo probleem niet oplost, kunt u proberen opnieuw op te starten. Dit probleem kan optreden als u Hallo Compute-Emulator toosuspend gebruiken en verwijderen van actieve implementaties.
* Als u een van de opdrachten vanaf de opdrachtregel profilering Hallo hebt gebruikt, met name Hallo globale instellingen, zorg ervoor dat VSPerfClrEnv /globaloff is aangeroepen en dat VsPerfMon.exe is afgesloten.
* Als als steekproef nemen, u het Hallo-bericht ziet ' PRF0025: Er is geen gegevens verzameld, "Controleer of de Hallo proces toohas CPU-activiteit die is gekoppeld. Toepassingen die niet alle rekenwerk doen produceert mogelijk niet alle gegevens steekproeven.  Het is ook mogelijk dat Hallo het proces is afgesloten voordat alle steekproeven werd uitgevoerd. Controleer toosee die Hallo Run-methode voor een functie die u zijn profilering niet wordt beëindigd.

## <a name="next-steps"></a>Volgende stappen
Azure binaire bestanden in de emulator Hallo instrumenteren wordt niet ondersteund in Hallo Visual Studio profiler, maar als u de geheugentoewijzing tootest wilt, kunt u deze optie kiezen wanneer profilering. U kunt ook gelijktijdigheid profilering, waarmee u bepalen of threads zijn verspilling tijd concurreren voor vergrendelingen of laag interactie profilering, waarmee u prestatieproblemen sporen zijn wanneer de interactie tussen lagen van een toepassing, meest vaak tussen de gegevenslaag Hallo en een werkrol.  U kunt bekijken Hallo databasequery's die uw app wordt gegenereerd en Hallo profileren tooimprove gegevens van uw gebruik van Hallo database gebruiken. Zie voor informatie over laag interactie profilering Hallo blogbericht [Walkthrough: met behulp van laag interactie Profiler in Visual Studio Team System 2010 Hallo][3].

[1]: http://msdn.microsoft.com/library/azure/hh369930.aspx
[2]: http://msdn.microsoft.com/library/azure/hh411542.aspx
[3]: http://blogs.msdn.com/b/habibh/archive/2009/06/30/walkthrough-using-the-tier-interaction-profiler-in-visual-studio-team-system-2010.aspx
[4]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally09.png
[5]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally10.png
[6]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally02.png
[7]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally05.png
[8]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally010.png
[9]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally07.png
[10]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally06.png
[11]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally03.png
[12]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally011.png
[14]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally04.png 
[15]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally013.png
[16]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally012.png
[17]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally08.png
