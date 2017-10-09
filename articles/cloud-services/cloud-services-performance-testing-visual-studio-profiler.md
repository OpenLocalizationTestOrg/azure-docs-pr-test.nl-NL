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
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a><span data-ttu-id="4796b-103">Hallo prestaties van een Cloud-Service lokaal in Hallo hello Azure Compute-Emulator met behulp van Visual Studio Profiler testen</span><span class="sxs-lookup"><span data-stu-id="4796b-103">Testing hello Performance of a Cloud Service Locally in hello Azure Compute Emulator Using hello Visual Studio Profiler</span></span>
<span data-ttu-id="4796b-104">Tal van hulpprogramma's en technieken zijn beschikbaar voor het Hallo-prestaties van cloudservices testen.</span><span class="sxs-lookup"><span data-stu-id="4796b-104">A variety of tools and techniques are available for testing hello performance of cloud services.</span></span>
<span data-ttu-id="4796b-105">Wanneer u een cloud service tooAzure publiceert, kunt u Visual Studio profileringsgegevens verzamelen en deze vervolgens te analyseren hebt lokaal, zoals beschreven in [profileren van een Azure-toepassing][1].</span><span class="sxs-lookup"><span data-stu-id="4796b-105">When you publish a cloud service tooAzure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="4796b-106">U kunt ook diagnostische gegevens tootrack tal van de prestaties van tellers, zoals beschreven in [met behulp van de prestatiemeteritems in Azure][2].</span><span class="sxs-lookup"><span data-stu-id="4796b-106">You can also use diagnostics tootrack a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="4796b-107">U kunt uw toepassing lokaal in de rekenemulator Hallo voordat u deze toohello cloud implementeert ook tooprofile.</span><span class="sxs-lookup"><span data-stu-id="4796b-107">You might also want tooprofile your application locally in hello compute emulator before deploying it toohello cloud.</span></span>

<span data-ttu-id="4796b-108">In dit artikel bevat informatie over Hallo CPU steekproeven methode van profilering, die kan lokaal worden uitgevoerd in Hallo-emulator.</span><span class="sxs-lookup"><span data-stu-id="4796b-108">This article covers hello CPU Sampling method of profiling, which can be done locally in hello emulator.</span></span> <span data-ttu-id="4796b-109">CPU-steekproeven is een methode voor het samenstellen van profiel die niet zeer hoog.</span><span class="sxs-lookup"><span data-stu-id="4796b-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="4796b-110">Hallo profiler maakt op een aangewezen steekproefinterval een momentopname van Hallo aanroepstack.</span><span class="sxs-lookup"><span data-stu-id="4796b-110">At a designated sampling interval, hello profiler takes a snapshot of hello call stack.</span></span> <span data-ttu-id="4796b-111">Hallo gegevens gedurende een periode worden verzameld en weergegeven in een rapport.</span><span class="sxs-lookup"><span data-stu-id="4796b-111">hello data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="4796b-112">Deze methode van profilering doorgaans tooindicate waarbij in een toepassing rekenkracht meeste Hallo CPU werk wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4796b-112">This method of profiling tends tooindicate where in a computationally intensive application most of hello CPU work is being done.</span></span>  <span data-ttu-id="4796b-113">Dit biedt u toofocus kans op Hallo 'hot pad' Hallo waar uw toepassing uitgeeft Hallo meeste tijd.</span><span class="sxs-lookup"><span data-stu-id="4796b-113">This gives you hello opportunity toofocus on hello "hot path" where your application is spending hello most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="4796b-114">1: Visual Studio voor profilering configureren</span><span class="sxs-lookup"><span data-stu-id="4796b-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="4796b-115">Er zijn eerst enkele Visual Studio-configuratieopties die nuttig zijn kunnen bij het samenstellen van profiel.</span><span class="sxs-lookup"><span data-stu-id="4796b-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="4796b-116">toomake beeld krijgt van Hallo profilering rapporten, moet u symbolen (.pdb-bestanden) voor uw toepassing en ook symbolen voor systeembibliotheken.</span><span class="sxs-lookup"><span data-stu-id="4796b-116">toomake sense of hello profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="4796b-117">Moet u ervoor dat u verwijst naar Hallo beschikbaar symbool servers toomake.</span><span class="sxs-lookup"><span data-stu-id="4796b-117">You'll want toomake sure that you reference hello available symbol servers.</span></span> <span data-ttu-id="4796b-118">toodo dit op Hallo **extra** in het menu in Visual Studio **opties**, en kies vervolgens **foutopsporing**, klikt u vervolgens **symbolen**.</span><span class="sxs-lookup"><span data-stu-id="4796b-118">toodo this, on hello **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="4796b-119">Zorg ervoor dat Microsoft symbool Servers wordt vermeld onder **symbool bestandslocaties (.pdb)**.</span><span class="sxs-lookup"><span data-stu-id="4796b-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="4796b-120">U kunt ook verwijzen naar http://referencesource.microsoft.com/symbols deze heeft mogelijk extra symboolbestanden.</span><span class="sxs-lookup"><span data-stu-id="4796b-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![Symboolopties][4]

<span data-ttu-id="4796b-122">Indien gewenst, kunt u vereenvoudigen Hallo rapporten die profiler Hallo door in te stellen alleen mijn Code genereert.</span><span class="sxs-lookup"><span data-stu-id="4796b-122">If desired, you can simplify hello reports that hello profiler generates by setting Just My Code.</span></span> <span data-ttu-id="4796b-123">Met alleen mijn Code is ingeschakeld, worden functie aanroep stacks vereenvoudigd zodat die volledig interne toolibraries aanroept en Hallo .NET Framework zijn verborgen voor Hallo-rapporten.</span><span class="sxs-lookup"><span data-stu-id="4796b-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal toolibraries and hello .NET Framework are hidden from hello reports.</span></span> <span data-ttu-id="4796b-124">Op Hallo **extra** menu kiezen **opties**.</span><span class="sxs-lookup"><span data-stu-id="4796b-124">On hello **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="4796b-125">Vouw vervolgens Hallo **prestatiehulpprogramma's** knooppunt, en kies **algemene**.</span><span class="sxs-lookup"><span data-stu-id="4796b-125">Then expand hello **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="4796b-126">Schakel dit selectievakje in Hallo voor **inschakelen alleen mijn Code voor de profiler rapporten**.</span><span class="sxs-lookup"><span data-stu-id="4796b-126">Select hello checkbox for **Enable Just My Code for profiler reports**.</span></span>

![Alleen mijn Code opties][17]

<span data-ttu-id="4796b-128">U kunt deze instructies met een bestaand project of met een nieuw project.</span><span class="sxs-lookup"><span data-stu-id="4796b-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="4796b-129">Als u een nieuw project tootry Hallo hieronder beschreven technieken maakt, kiest u een C# **Azure Cloud Service** project en selecteer een **Webrol** en een **Werkrol**.</span><span class="sxs-lookup"><span data-stu-id="4796b-129">If you create a new project tootry hello techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Azure Cloud Service-Projectrollen][5]

<span data-ttu-id="4796b-131">Bijvoorbeeld toevoegen doeleinden, sommige tooyour CodeProject die ervoor zorgt dat veel tijd ziet u enkele duidelijk prestatieprobleem.</span><span class="sxs-lookup"><span data-stu-id="4796b-131">For example purposes, add some code tooyour project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="4796b-132">Bijvoorbeeld, voeg Hallo code tooa werkrolproject te volgen:</span><span class="sxs-lookup"><span data-stu-id="4796b-132">For example, add hello following code tooa worker role project:</span></span>

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

<span data-ttu-id="4796b-133">Deze code aanroepen vanuit Hallo RunAsync-methode in Hallo-werkrol van RoleEntryPoint afgeleide klasse.</span><span class="sxs-lookup"><span data-stu-id="4796b-133">Call this code from hello RunAsync method in hello worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="4796b-134">(Negeren Hallo-waarschuwing over Hallo methode synchroon uitgevoerd.)</span><span class="sxs-lookup"><span data-stu-id="4796b-134">(Ignore hello warning about hello method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="4796b-135">Bouwen en uitvoeren van uw cloudservice lokaal zonder foutopsporing (Ctrl + F5) met Hallo oplossing configuratieset te**Release**.</span><span class="sxs-lookup"><span data-stu-id="4796b-135">Build and run your cloud service locally without debugging (Ctrl+F5), with hello solution configuration set too**Release**.</span></span> <span data-ttu-id="4796b-136">Dit zorgt ervoor dat alle bestanden en mappen worden gemaakt voor het Hallo-toepassing lokaal uitvoert en zorgt ervoor dat alle Hallo emulators worden gestart.</span><span class="sxs-lookup"><span data-stu-id="4796b-136">This ensures that all files and folders are created for running hello application locally, and ensures that all hello emulators are started.</span></span> <span data-ttu-id="4796b-137">Hallo Compute-Emulator UI starten vanuit Hallo taakbalk tooverify die uw werkrol wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4796b-137">Start hello Compute Emulator UI from hello taskbar tooverify that your worker role is running.</span></span>

## <a name="2-attach-tooa-process"></a><span data-ttu-id="4796b-138">2: tooa proces koppelen</span><span class="sxs-lookup"><span data-stu-id="4796b-138">2: Attach tooa process</span></span>
<span data-ttu-id="4796b-139">In plaats van de toepassing hello vanaf Hallo Visual Studio 2010 IDE profilering, koppelt u Hallo profiler tooa process uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4796b-139">Instead of profiling hello application by starting it from hello Visual Studio 2010 IDE, you must attach hello profiler tooa running process.</span></span> 

<span data-ttu-id="4796b-140">tooattach hello profiler tooa proces, op Hallo **analyseren** menu kiezen **Profiler** en **Attach/Detach**.</span><span class="sxs-lookup"><span data-stu-id="4796b-140">tooattach hello profiler tooa process, on hello **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![Optie profiel koppelen][6]

<span data-ttu-id="4796b-142">Voor een werkrol vinden Hallo WaWorkerHost.exe proces.</span><span class="sxs-lookup"><span data-stu-id="4796b-142">For a worker role, find hello WaWorkerHost.exe process.</span></span>

![WaWorkerHost proces][7]

<span data-ttu-id="4796b-144">Als de projectmap zich op een netwerkstation bevindt, wordt Hallo profiler u gevraagd tooprovide een andere locatie toosave Hallo profileren van rapporten.</span><span class="sxs-lookup"><span data-stu-id="4796b-144">If your project folder is on a network drive, hello profiler will ask you tooprovide another location toosave hello profiling reports.</span></span>

 <span data-ttu-id="4796b-145">U kunt ook tooa Webrol koppelen door het tooWaIISHost.exe koppelen.</span><span class="sxs-lookup"><span data-stu-id="4796b-145">You can also attach tooa web role by attaching tooWaIISHost.exe.</span></span>
<span data-ttu-id="4796b-146">Als er meerdere werkprocessen functie in uw toepassing, moet u toouse Hallo processID toodistinguish ze.</span><span class="sxs-lookup"><span data-stu-id="4796b-146">If there are multiple worker role processes in your application, you need toouse hello processID toodistinguish them.</span></span> <span data-ttu-id="4796b-147">U kunt Hallo processID programmatisch opvragen door het openen van het procesobject Hallo.</span><span class="sxs-lookup"><span data-stu-id="4796b-147">You can query hello processID programmatically by accessing hello Process object.</span></span> <span data-ttu-id="4796b-148">Bijvoorbeeld als u deze code toohello-Run-methode van Hallo RoleEntryPoint afgeleide klasse aan een rol toevoegen, kunt u het logboek in bekijken Hallo Compute-Emulator UI tooknow welke tooconnect proces aan.</span><span class="sxs-lookup"><span data-stu-id="4796b-148">For example, if you add this code toohello Run method of hello RoleEntryPoint-derived class in a role, you can look at the log in hello Compute Emulator UI tooknow what process tooconnect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="4796b-149">tooview hello logboek start Hallo Compute-Emulator gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="4796b-149">tooview hello log, start hello Compute Emulator UI.</span></span>

![Hallo Compute-Emulator UI starten][8]

<span data-ttu-id="4796b-151">Hallo worker-rol logboek-consolevenster in Hallo Compute-Emulator UI door te klikken op de titelbalk Hallo consolevenster openen</span><span class="sxs-lookup"><span data-stu-id="4796b-151">Open hello worker role log console window in hello Compute Emulator UI by clicking on hello console window's title bar.</span></span> <span data-ttu-id="4796b-152">Hallo proces-ID in Hallo logboek, kunt u zien.</span><span class="sxs-lookup"><span data-stu-id="4796b-152">You can see hello process ID in hello log.</span></span>

![Proces-ID weergeven][9]

<span data-ttu-id="4796b-154">Een u hebt gekoppeld, Hallo stappen uitvoeren in uw toepassing UI (indien nodig) tooreproduce Hallo scenario.</span><span class="sxs-lookup"><span data-stu-id="4796b-154">One you've attached, perform hello steps in your application's UI (if needed) tooreproduce hello scenario.</span></span>

<span data-ttu-id="4796b-155">Als u wilt dat toostop profilering, kiest u Hallo **stoppen profilering** koppeling.</span><span class="sxs-lookup"><span data-stu-id="4796b-155">When you want toostop profiling, choose hello **Stop Profiling** link.</span></span>

![Profileren van de optie stoppen][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="4796b-157">3: prestatierapporten weergeven</span><span class="sxs-lookup"><span data-stu-id="4796b-157">3: View performance reports</span></span>
<span data-ttu-id="4796b-158">Rapport over systeemprestaties Hallo voor uw toepassing wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4796b-158">hello performance report for your application is displayed.</span></span>

<span data-ttu-id="4796b-159">Op dit moment Hallo profiler stopt met het uitvoeren van gegevens worden opgeslagen in een bestand .vsp en een rapport een analyse van deze gegevens bevat worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4796b-159">At this point, hello profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![Profiler rapport][11]

<span data-ttu-id="4796b-161">Als u String.wstrcpy in Hot pad hello, klikt u op alleen mijn Code toochange Hallo weergave tooshow gebruikerscode alleen ziet.</span><span class="sxs-lookup"><span data-stu-id="4796b-161">If you see String.wstrcpy in hello Hot Path, click on Just My Code toochange hello view tooshow user code only.</span></span>  <span data-ttu-id="4796b-162">Als u String.Concat ziet, kunt u Hallo alle Code weergeven knop.</span><span class="sxs-lookup"><span data-stu-id="4796b-162">If you see String.Concat, try pressing hello Show All Code button.</span></span>

<span data-ttu-id="4796b-163">U ziet Hallo samenvoegen methode en een groot deel van de uitvoeringstijd Hallo inneemt String.Concat.</span><span class="sxs-lookup"><span data-stu-id="4796b-163">You should see hello Concatenate method and String.Concat taking up a large portion of hello execution time.</span></span>

![Analyse van rapport][12]

<span data-ttu-id="4796b-165">Als u Hallo tekenreeks samenvoeging code in dit artikel hebt toegevoegd, ziet u een waarschuwing in de lijst met taken Hallo voor deze.</span><span class="sxs-lookup"><span data-stu-id="4796b-165">If you added hello string concatenation code in this article, you should see a warning in hello Task List for this.</span></span> <span data-ttu-id="4796b-166">U ziet ook een waarschuwing dat er een uitzonderlijk groot aantal garbagecollection is, vervalt toohello aantal tekenreeksen die zijn gemaakt en verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4796b-166">You may also see a warning that there is an excessive amount of garbage collection, which is due toohello number of strings that are created and disposed.</span></span>

![Waarschuwingen voor prestaties][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="4796b-168">4: wijzigingen aanbrengen en vergelijkt u prestaties</span><span class="sxs-lookup"><span data-stu-id="4796b-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="4796b-169">U kunt ook Hallo prestaties voor en na een codewijziging vergelijken.</span><span class="sxs-lookup"><span data-stu-id="4796b-169">You can also compare hello performance before and after a code change.</span></span>  <span data-ttu-id="4796b-170">Hallo process uitgevoerd stoppen en Hallo code tooreplace Hallo samenvoeging bewerking van de tekenreeks met Hallo gebruik van StringBuilder bewerken:</span><span class="sxs-lookup"><span data-stu-id="4796b-170">Stop hello running process, and edit hello code tooreplace hello string concatenation operation with hello use of StringBuilder:</span></span>

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

<span data-ttu-id="4796b-171">Uitvoeren van een andere prestaties doen, en vervolgens vergelijken Hallo prestaties.</span><span class="sxs-lookup"><span data-stu-id="4796b-171">Do another performance run, and then compare hello performance.</span></span> <span data-ttu-id="4796b-172">In Hallo prestaties Explorer, als hello wordt uitgevoerd, zich in Hallo dezelfde sessie, u kunt alleen beide rapporten te selecteren, snelmenu Hallo openen en kies **prestatierapporten vergelijken**.</span><span class="sxs-lookup"><span data-stu-id="4796b-172">In hello Performance Explorer, if hello runs are in hello same session, you can just select both reports, open hello shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="4796b-173">Als u toocompare met een wordt uitgevoerd in een andere prestatiesessie wilt, open Hallo **analyseren** menu en kies **prestatierapporten vergelijken**.</span><span class="sxs-lookup"><span data-stu-id="4796b-173">If you want toocompare with a run in another performance session, open hello **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="4796b-174">Geef beide bestanden in Hallo dialoogvenster dat wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4796b-174">Specify both files in hello dialog box that appears.</span></span>

![Optie voor prestaties van rapporten vergelijken][15]

<span data-ttu-id="4796b-176">Hallo rapporten Markeer verschillen tussen Hallo twee wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4796b-176">hello reports highlight differences between hello two runs.</span></span>

![Van vergelijkingsrapport][16]

<span data-ttu-id="4796b-178">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="4796b-178">Congratulations!</span></span> <span data-ttu-id="4796b-179">U slag bent gegaan met Hallo profiler.</span><span class="sxs-lookup"><span data-stu-id="4796b-179">You've gotten started with hello profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="4796b-180">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="4796b-180">Troubleshooting</span></span>
* <span data-ttu-id="4796b-181">Controleer of u een Release-build zijn profilering en starten zonder foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="4796b-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="4796b-182">Als Hallo Attach/Detach optie is niet ingeschakeld op Hallo Profiler menu, voert u Hallo prestaties Wizard.</span><span class="sxs-lookup"><span data-stu-id="4796b-182">If hello Attach/Detach option is not enabled on hello Profiler menu, run hello Performance Wizard.</span></span>
* <span data-ttu-id="4796b-183">Hallo Compute-Emulator UI tooview Hallo status van uw toepassing gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4796b-183">Use hello Compute Emulator UI tooview hello status of your application.</span></span> 
* <span data-ttu-id="4796b-184">Als er problemen optreden bij het starten van toepassingen in Hallo-emulator of profiler koppelen hello, Hallo rekenemulator afsluiten en opnieuw.</span><span class="sxs-lookup"><span data-stu-id="4796b-184">If you have problems starting applications in hello emulator, or attaching hello profiler, shut down hello compute emulator and restart it.</span></span> <span data-ttu-id="4796b-185">Als dit Hallo probleem niet oplost, kunt u proberen opnieuw op te starten.</span><span class="sxs-lookup"><span data-stu-id="4796b-185">If that doesn't solve hello problem, try rebooting.</span></span> <span data-ttu-id="4796b-186">Dit probleem kan optreden als u Hallo Compute-Emulator toosuspend gebruiken en verwijderen van actieve implementaties.</span><span class="sxs-lookup"><span data-stu-id="4796b-186">This problem can occur if you use hello Compute Emulator toosuspend and remove running deployments.</span></span>
* <span data-ttu-id="4796b-187">Als u een van de opdrachten vanaf de opdrachtregel profilering Hallo hebt gebruikt, met name Hallo globale instellingen, zorg ervoor dat VSPerfClrEnv /globaloff is aangeroepen en dat VsPerfMon.exe is afgesloten.</span><span class="sxs-lookup"><span data-stu-id="4796b-187">If you have used any of hello profiling commands from the command line, especially hello global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="4796b-188">Als als steekproef nemen, u het Hallo-bericht ziet ' PRF0025: Er is geen gegevens verzameld, "Controleer of de Hallo proces toohas CPU-activiteit die is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="4796b-188">If when sampling, you see hello message "PRF0025: No data was collected," check that hello process you attached toohas CPU activity.</span></span> <span data-ttu-id="4796b-189">Toepassingen die niet alle rekenwerk doen produceert mogelijk niet alle gegevens steekproeven.</span><span class="sxs-lookup"><span data-stu-id="4796b-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="4796b-190">Het is ook mogelijk dat Hallo het proces is afgesloten voordat alle steekproeven werd uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4796b-190">It's also possible that hello process exited before any sampling was done.</span></span> <span data-ttu-id="4796b-191">Controleer toosee die Hallo Run-methode voor een functie die u zijn profilering niet wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="4796b-191">Check toosee that hello Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4796b-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4796b-192">Next Steps</span></span>
<span data-ttu-id="4796b-193">Azure binaire bestanden in de emulator Hallo instrumenteren wordt niet ondersteund in Hallo Visual Studio profiler, maar als u de geheugentoewijzing tootest wilt, kunt u deze optie kiezen wanneer profilering.</span><span class="sxs-lookup"><span data-stu-id="4796b-193">Instrumenting Azure binaries in hello emulator is not supported in hello Visual Studio profiler, but if you want tootest memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="4796b-194">U kunt ook gelijktijdigheid profilering, waarmee u bepalen of threads zijn verspilling tijd concurreren voor vergrendelingen of laag interactie profilering, waarmee u prestatieproblemen sporen zijn wanneer de interactie tussen lagen van een toepassing, meest vaak tussen de gegevenslaag Hallo en een werkrol.</span><span class="sxs-lookup"><span data-stu-id="4796b-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between hello data tier and a worker role.</span></span>  <span data-ttu-id="4796b-195">U kunt bekijken Hallo databasequery's die uw app wordt gegenereerd en Hallo profileren tooimprove gegevens van uw gebruik van Hallo database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4796b-195">You can view hello database queries that your app generates and use hello profiling data tooimprove your use of hello database.</span></span> <span data-ttu-id="4796b-196">Zie voor informatie over laag interactie profilering Hallo blogbericht [Walkthrough: met behulp van laag interactie Profiler in Visual Studio Team System 2010 Hallo][3].</span><span class="sxs-lookup"><span data-stu-id="4796b-196">For information about tier interaction profiling, see hello blog post [Walkthrough: Using hello Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

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
