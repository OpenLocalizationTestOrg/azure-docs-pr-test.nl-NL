---
title: Profileren van een Cloudservice lokaal in de Rekenemulator | Microsoft Docs
services: cloud-services
description: Het onderzoeken van prestatieproblemen in cloudservices met de profiler Visual Studio
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
ms.openlocfilehash: 51c8192d8312dc5cf546b4c357aeecf6f19d56b8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="testing-the-performance-of-a-cloud-service-locally-in-the-azure-compute-emulator-using-the-visual-studio-profiler"></a><span data-ttu-id="7f9dc-103">De prestaties van een Cloudservice lokaal te testen in de Azure-Rekenemulator met behulp van de Profiler Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7f9dc-103">Testing the Performance of a Cloud Service Locally in the Azure Compute Emulator Using the Visual Studio Profiler</span></span>
<span data-ttu-id="7f9dc-104">Tal van hulpprogramma's en technieken zijn beschikbaar voor het testen van de prestaties van cloudservices.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-104">A variety of tools and techniques are available for testing the performance of cloud services.</span></span>
<span data-ttu-id="7f9dc-105">Wanneer u een cloudservice naar Azure publiceert, kunt u Visual Studio profileringsgegevens verzamelen en deze vervolgens te analyseren hebt lokaal, zoals beschreven in [profileren van een Azure-toepassing][1].</span><span class="sxs-lookup"><span data-stu-id="7f9dc-105">When you publish a cloud service to Azure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="7f9dc-106">U kunt ook diagnostische gegevens gebruiken voor het bijhouden van tal van prestatiemeteritems, zoals beschreven in [met behulp van de prestatiemeteritems in Azure][2].</span><span class="sxs-lookup"><span data-stu-id="7f9dc-106">You can also use diagnostics to track a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="7f9dc-107">U kunt ook het profiel van uw toepassing lokaal in de rekenemulator voordat u deze implementeert in de cloud.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-107">You might also want to profile your application locally in the compute emulator before deploying it to the cloud.</span></span>

<span data-ttu-id="7f9dc-108">Dit artikel behandelt de profileringsmethode voor CPU-sampling, die lokaal kan worden uitgevoerd in de emulator.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-108">This article covers the CPU Sampling method of profiling, which can be done locally in the emulator.</span></span> <span data-ttu-id="7f9dc-109">CPU-steekproeven is een methode voor het samenstellen van profiel die niet zeer hoog.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="7f9dc-110">De profiler maakt op een aangewezen steekproefinterval een momentopname van de aanroepstack.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-110">At a designated sampling interval, the profiler takes a snapshot of the call stack.</span></span> <span data-ttu-id="7f9dc-111">De gegevens worden verzameld over een tijdsperiode, en in een rapport weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-111">The data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="7f9dc-112">Deze methode van profilering doorgaans om aan te geven waar in een toepassing rekenkracht meeste CPU werk wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-112">This method of profiling tends to indicate where in a computationally intensive application most of the CPU work is being done.</span></span>  <span data-ttu-id="7f9dc-113">Hierdoor kunt u zich kunt richten op het 'hot 'pad waar de toepassing de meeste tijd besteedt.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-113">This gives you the opportunity to focus on the "hot path" where your application is spending the most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="7f9dc-114">1: Visual Studio voor profilering configureren</span><span class="sxs-lookup"><span data-stu-id="7f9dc-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="7f9dc-115">Er zijn eerst enkele Visual Studio-configuratieopties die nuttig zijn kunnen bij het samenstellen van profiel.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="7f9dc-116">Om het zinvol zijn van de profilering rapporten, moet u symbolen (.pdb-bestanden) voor uw toepassing en ook symbolen voor systeembibliotheken.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-116">To make sense of the profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="7f9dc-117">Moet u ervoor zorgen dat u verwijst naar de beschikbare symbool-servers.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-117">You'll want to make sure that you reference the available symbol servers.</span></span> <span data-ttu-id="7f9dc-118">Om dit te doen, op de **extra** in het menu in Visual Studio **opties**, en kies vervolgens **foutopsporing**, klikt u vervolgens **symbolen**.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-118">To do this, on the **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="7f9dc-119">Zorg ervoor dat Microsoft symbool Servers wordt vermeld onder **symbool bestandslocaties (.pdb)**.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="7f9dc-120">U kunt ook verwijzen naar http://referencesource.microsoft.com/symbols deze heeft mogelijk extra symboolbestanden.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![Symboolopties][4]

<span data-ttu-id="7f9dc-122">Indien gewenst, kunt u de rapporten die de profiler wordt gegenereerd door in te stellen alleen mijn Code vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-122">If desired, you can simplify the reports that the profiler generates by setting Just My Code.</span></span> <span data-ttu-id="7f9dc-123">Functie-aanroep stacks zijn met alleen mijn Code is ingeschakeld, vereenvoudigd zodat aanroepen volledig interne bibliotheken en .NET Framework zijn verborgen voor de rapporten.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal to libraries and the .NET Framework are hidden from the reports.</span></span> <span data-ttu-id="7f9dc-124">Op de **extra** menu kiezen **opties**.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-124">On the **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="7f9dc-125">Vouw de **prestatiehulpprogramma's** knooppunt, en kies **algemene**.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-125">Then expand the **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="7f9dc-126">Schakel het selectievakje voor **inschakelen alleen mijn Code voor de profiler rapporten**.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-126">Select the checkbox for **Enable Just My Code for profiler reports**.</span></span>

![Alleen mijn Code opties][17]

<span data-ttu-id="7f9dc-128">U kunt deze instructies met een bestaand project of met een nieuw project.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="7f9dc-129">Als u een nieuw project om te proberen de hieronder beschreven technieken maakt, kiest u een C# **Azure Cloud Service** project en selecteer een **Webrol** en een **Werkrol**.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-129">If you create a new project to try the techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Azure Cloud Service-Projectrollen][5]

<span data-ttu-id="7f9dc-131">Bijvoorbeeld toevoegen toepassing, code aan uw project die ervoor zorgt dat veel tijd ziet u een prestatieprobleem voor de hand liggende.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-131">For example purposes, add some code to your project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="7f9dc-132">Bijvoorbeeld, voeg de volgende code naar een werkrolproject:</span><span class="sxs-lookup"><span data-stu-id="7f9dc-132">For example, add the following code to a worker role project:</span></span>

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

<span data-ttu-id="7f9dc-133">Deze code aanroepen vanuit de RunAsync-methode in de werkrol RoleEntryPoint afgeleide klasse.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-133">Call this code from the RunAsync method in the worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="7f9dc-134">(Negeer de waarschuwing over de methode synchroon uitgevoerd.)</span><span class="sxs-lookup"><span data-stu-id="7f9dc-134">(Ignore the warning about the method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace the following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="7f9dc-135">Bouwen en uitvoeren van uw cloudservice lokaal zonder foutopsporing (Ctrl + F5) met de oplossingsconfiguratie ingesteld op **Release**.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-135">Build and run your cloud service locally without debugging (Ctrl+F5), with the solution configuration set to **Release**.</span></span> <span data-ttu-id="7f9dc-136">Dit zorgt ervoor dat alle bestanden en mappen worden gemaakt voor het uitvoeren van de toepassing lokaal en zorgt ervoor dat alle emulators worden gestart.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-136">This ensures that all files and folders are created for running the application locally, and ensures that all the emulators are started.</span></span> <span data-ttu-id="7f9dc-137">De gebruikersinterface van de Emulator Compute starten vanaf de taakbalk om te controleren of uw werkrol wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-137">Start the Compute Emulator UI from the taskbar to verify that your worker role is running.</span></span>

## <a name="2-attach-to-a-process"></a><span data-ttu-id="7f9dc-138">2: koppelen aan een proces</span><span class="sxs-lookup"><span data-stu-id="7f9dc-138">2: Attach to a process</span></span>
<span data-ttu-id="7f9dc-139">In plaats van de toepassing vanaf de Visual Studio 2010 IDE profilering, moet u de profiler koppelen aan een proces dat wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-139">Instead of profiling the application by starting it from the Visual Studio 2010 IDE, you must attach the profiler to a running process.</span></span> 

<span data-ttu-id="7f9dc-140">De profiler koppelen aan een proces op de **analyseren** menu kiezen **Profiler** en **Attach/Detach**.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-140">To attach the profiler to a process, on the **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![Optie profiel koppelen][6]

<span data-ttu-id="7f9dc-142">Zoek het WaWorkerHost.exe-proces voor een werkrol.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-142">For a worker role, find the WaWorkerHost.exe process.</span></span>

![WaWorkerHost proces][7]

<span data-ttu-id="7f9dc-144">Als de projectmap zich op een netwerkstation bevindt, vraagt de profiler u een andere locatie om op te slaan de profilering rapporten bieden.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-144">If your project folder is on a network drive, the profiler will ask you to provide another location to save the profiling reports.</span></span>

 <span data-ttu-id="7f9dc-145">U kunt ook koppelen aan een Webrol door aan WaIISHost.exe te koppelen.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-145">You can also attach to a web role by attaching to WaIISHost.exe.</span></span>
<span data-ttu-id="7f9dc-146">Als er meerdere werkprocessen functie in uw toepassing zijn, moet u de proces-id gebruiken om ze te onderscheiden.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-146">If there are multiple worker role processes in your application, you need to use the processID to distinguish them.</span></span> <span data-ttu-id="7f9dc-147">U kunt de processID programmatisch opvragen door het openen van het procesobject.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-147">You can query the processID programmatically by accessing the Process object.</span></span> <span data-ttu-id="7f9dc-148">Als u deze code aan de methode Run van de klasse die is afgeleid van RoleEntryPoint in een rol toevoegen, kunt u kunt bijvoorbeeld voor zoeken in het logbestand in de gebruikersinterface van de Emulator Compute weten welk proces verbinding maken met.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-148">For example, if you add this code to the Run method of the RoleEntryPoint-derived class in a role, you can look at the log in the Compute Emulator UI to know what process to connect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="7f9dc-149">Als u wilt weergeven in het logboek, start de gebruikersinterface van de Emulator Compute.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-149">To view the log, start the Compute Emulator UI.</span></span>

![Start de gebruikersinterface van de Rekenemulator][8]

<span data-ttu-id="7f9dc-151">Open het consolevenster worker-rol logboek in de gebruikersinterface van de Emulator berekenen door te klikken op de titelbalk van het consolevenster.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-151">Open the worker role log console window in the Compute Emulator UI by clicking on the console window's title bar.</span></span> <span data-ttu-id="7f9dc-152">U ziet de proces-ID in het logboek.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-152">You can see the process ID in the log.</span></span>

![Proces-ID weergeven][9]

<span data-ttu-id="7f9dc-154">Een u hebt gekoppeld, voer de stappen in de gebruikersinterface van uw toepassing (indien nodig) om het scenario.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-154">One you've attached, perform the steps in your application's UI (if needed) to reproduce the scenario.</span></span>

<span data-ttu-id="7f9dc-155">Als u stoppen profilering wilt, kiest u de **stoppen profilering** koppeling.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-155">When you want to stop profiling, choose the **Stop Profiling** link.</span></span>

![Profileren van de optie stoppen][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="7f9dc-157">3: prestatierapporten weergeven</span><span class="sxs-lookup"><span data-stu-id="7f9dc-157">3: View performance reports</span></span>
<span data-ttu-id="7f9dc-158">Het prestatierapport voor uw toepassing wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-158">The performance report for your application is displayed.</span></span>

<span data-ttu-id="7f9dc-159">Op dit moment de profiler stopt met het uitvoeren van gegevens worden opgeslagen in een bestand .vsp en een rapport een analyse van deze gegevens bevat worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-159">At this point, the profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![Profiler rapport][11]

<span data-ttu-id="7f9dc-161">Als u String.wstrcpy in de Hot pad ziet, klik op alleen mijn Code voor het wijzigen van de weer te geven alleen gebruikerscode.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-161">If you see String.wstrcpy in the Hot Path, click on Just My Code to change the view to show user code only.</span></span>  <span data-ttu-id="7f9dc-162">Als u String.Concat ziet, drukt u op de knop alle Code weergeven.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-162">If you see String.Concat, try pressing the Show All Code button.</span></span>

<span data-ttu-id="7f9dc-163">U ziet de samenvoegen methode en String.Concat inneemt een groot deel van de uitvoeringstijd.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-163">You should see the Concatenate method and String.Concat taking up a large portion of the execution time.</span></span>

![Analyse van rapport][12]

<span data-ttu-id="7f9dc-165">Als u de code van de samengevoegde tekenreeks in dit artikel hebt toegevoegd, ziet u een waarschuwing in de taaklijst voor deze.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-165">If you added the string concatenation code in this article, you should see a warning in the Task List for this.</span></span> <span data-ttu-id="7f9dc-166">U ziet ook een waarschuwing dat er is een uitzonderlijk groot aantal garbagecollection die wordt veroorzaakt door het aantal tekenreeksen die zijn gemaakt en verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-166">You may also see a warning that there is an excessive amount of garbage collection, which is due to the number of strings that are created and disposed.</span></span>

![Waarschuwingen voor prestaties][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="7f9dc-168">4: wijzigingen aanbrengen en vergelijkt u prestaties</span><span class="sxs-lookup"><span data-stu-id="7f9dc-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="7f9dc-169">U kunt ook de prestaties voor en na een codewijziging vergelijken.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-169">You can also compare the performance before and after a code change.</span></span>  <span data-ttu-id="7f9dc-170">Stoppen van het proces dat wordt uitgevoerd en de code ter vervanging van de bewerking van de samengevoegde tekenreeks met het gebruik van StringBuilder bewerken:</span><span class="sxs-lookup"><span data-stu-id="7f9dc-170">Stop the running process, and edit the code to replace the string concatenation operation with the use of StringBuilder:</span></span>

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

<span data-ttu-id="7f9dc-171">Uitvoeren van een andere prestaties doen, en vervolgens vergelijken de prestaties.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-171">Do another performance run, and then compare the performance.</span></span> <span data-ttu-id="7f9dc-172">De Explorer prestaties als het wordt uitgevoerd in dezelfde sessie, u kunt alleen Selecteer in beide rapporten, open het snelmenu, en kies **prestatierapporten vergelijken**.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-172">In the Performance Explorer, if the runs are in the same session, you can just select both reports, open the shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="7f9dc-173">Als u vergelijken met een wordt uitgevoerd in een andere prestatiesessie wilt, opent u de **analyseren** menu en kies **prestatierapporten vergelijken**.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-173">If you want to compare with a run in another performance session, open the **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="7f9dc-174">Geef beide bestanden in het dialoogvenster dat wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-174">Specify both files in the dialog box that appears.</span></span>

![Optie voor prestaties van rapporten vergelijken][15]

<span data-ttu-id="7f9dc-176">De rapporten Markeer verschillen tussen de twee wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-176">The reports highlight differences between the two runs.</span></span>

![Van vergelijkingsrapport][16]

<span data-ttu-id="7f9dc-178">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-178">Congratulations!</span></span> <span data-ttu-id="7f9dc-179">U slag bent gegaan met de profiler.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-179">You've gotten started with the profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7f9dc-180">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="7f9dc-180">Troubleshooting</span></span>
* <span data-ttu-id="7f9dc-181">Controleer of u een Release-build zijn profilering en starten zonder foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="7f9dc-182">Als de optie Attach/Detach is niet ingeschakeld in het menu Profiler, voert u de Wizard prestaties.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-182">If the Attach/Detach option is not enabled on the Profiler menu, run the Performance Wizard.</span></span>
* <span data-ttu-id="7f9dc-183">De Emulator Compute gebruikersinterface gebruiken om de status van uw toepassing weer te geven.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-183">Use the Compute Emulator UI to view the status of your application.</span></span> 
* <span data-ttu-id="7f9dc-184">Als u problemen ondervindt bij het starten van toepassingen in de emulator of koppelen van de profiler, sluit de rekenemulator omlaag en start deze opnieuw.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-184">If you have problems starting applications in the emulator, or attaching the profiler, shut down the compute emulator and restart it.</span></span> <span data-ttu-id="7f9dc-185">Als dit het probleem niet oplost, opnieuw op te starten.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-185">If that doesn't solve the problem, try rebooting.</span></span> <span data-ttu-id="7f9dc-186">Dit probleem kan optreden als u de Compute-Emulator gebruiken om te onderbreken en verwijderen van actieve implementaties.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-186">This problem can occur if you use the Compute Emulator to suspend and remove running deployments.</span></span>
* <span data-ttu-id="7f9dc-187">Als u een van de profilering opdrachten vanaf de opdrachtregel, met name de algemene instellingen hebt gebruikt moet VSPerfClrEnv /globaloff is aangeroepen en dat VsPerfMon.exe is afgesloten.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-187">If you have used any of the profiling commands from the command line, especially the global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="7f9dc-188">Als een steekproef nemen, ziet u het bericht ' PRF0025: is er geen gegevens verzameld, "Controleer of het proces dat u hebt gekoppeld aan CPU-activiteit is.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-188">If when sampling, you see the message "PRF0025: No data was collected," check that the process you attached to has CPU activity.</span></span> <span data-ttu-id="7f9dc-189">Toepassingen die niet alle rekenwerk doen produceert mogelijk niet alle gegevens steekproeven.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="7f9dc-190">Het is ook mogelijk dat het proces is afgesloten voordat alle steekproeven werd uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-190">It's also possible that the process exited before any sampling was done.</span></span> <span data-ttu-id="7f9dc-191">Controleer dat de Run-methode voor een functie die u zijn profilering niet beëindigt.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-191">Check to see that the Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f9dc-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7f9dc-192">Next Steps</span></span>
<span data-ttu-id="7f9dc-193">Azure binaire bestanden in de emulator instrumenteren wordt niet ondersteund in de Visual Studio-profiler, maar als u testen geheugentoewijzing wilt, kunt u die optie kiezen bij het samenstellen van profiel.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-193">Instrumenting Azure binaries in the emulator is not supported in the Visual Studio profiler, but if you want to test memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="7f9dc-194">U kunt ook gelijktijdigheid profilering, waarmee u bepalen of threads zijn verspilling tijd concurreren voor vergrendelingen of laag interactie profilering, waarmee u prestatieproblemen sporen zijn wanneer de interactie tussen lagen van een toepassing, meest vaak tussen de gegevenslaag en een werkrol.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between the data tier and a worker role.</span></span>  <span data-ttu-id="7f9dc-195">U kunt bekijken van de database-query's die uw app wordt gegenereerd en de profileringsgegevens gebruiken voor het verbeteren van uw gebruik van de database.</span><span class="sxs-lookup"><span data-stu-id="7f9dc-195">You can view the database queries that your app generates and use the profiling data to improve your use of the database.</span></span> <span data-ttu-id="7f9dc-196">Zie voor informatie over laag interactie profilering, het blogbericht [Walkthrough: met behulp van de laag interactie Profiler in Visual Studio Team System 2010][3].</span><span class="sxs-lookup"><span data-stu-id="7f9dc-196">For information about tier interaction profiling, see the blog post [Walkthrough: Using the Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

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
