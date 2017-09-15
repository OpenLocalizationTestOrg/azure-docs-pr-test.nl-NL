<span data-ttu-id="8298a-101">De stappen om de registratie van een processerver ongedaan te maken, verschillen afhankelijk van de status van de verbinding met de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="8298a-101">The steps to unregister a process server differs depending on its connection status with the Configuration Server.</span></span>

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a><span data-ttu-id="8298a-102">De registratie ongedaan maken van een processerver die is verbonden</span><span class="sxs-lookup"><span data-stu-id="8298a-102">Unregister a process server that is in a connected state</span></span>

1. <span data-ttu-id="8298a-103">Meld u extern bij de processerver aan als beheerder.</span><span class="sxs-lookup"><span data-stu-id="8298a-103">Remote into the process server as an Administrator.</span></span>
2. <span data-ttu-id="8298a-104">Start het **Configuratiescherm** en open **Programma's > Een programma verwijderen**</span><span class="sxs-lookup"><span data-stu-id="8298a-104">Launch the **Control Panel** and open **Programs > Uninstall a program**</span></span>
3. <span data-ttu-id="8298a-105">Verwijder het programma met de naam **Microsoft Azure Site Recovery-configuratie-/processerver**</span><span class="sxs-lookup"><span data-stu-id="8298a-105">Uninstall a program by the name **Microsoft Azure Site Recovery Configuration/Process Server**</span></span>
4. <span data-ttu-id="8298a-106">Nadat stap 3 is voltooid, verwijdert u **Microsoft Azure Site Recovery-configuratie-/processerverafhankelijkheden**</span><span class="sxs-lookup"><span data-stu-id="8298a-106">Once step 3 is completed, you can uninstall **Microsoft Azure Site Recovery Configuration/Process Server Dependencies**</span></span>

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a><span data-ttu-id="8298a-107">De registratie ongedaan maken van een processerver die niet is verbonden</span><span class="sxs-lookup"><span data-stu-id="8298a-107">Unregister a process server that is in a disconnected state</span></span>

> [!WARNING]
> <span data-ttu-id="8298a-108">Volg onderstaande stappen als het niet lukt om de virtuele machine te reactiveren waarop de processerver is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8298a-108">Use the below steps should be used if there is no way to revive the virtual machine on which the Process Server was installed.</span></span>

1. <span data-ttu-id="8298a-109">Meld u bij uw configuratieserver aan als beheerder.</span><span class="sxs-lookup"><span data-stu-id="8298a-109">Log on to your configuration server as an Administrator.</span></span>
2. <span data-ttu-id="8298a-110">Open een beheeropdrachtprompt en blader naar de map `%ProgramData%\ASR\home\svsystems\bin`.</span><span class="sxs-lookup"><span data-stu-id="8298a-110">Open an Administrative command prompt and browse to the directory `%ProgramData%\ASR\home\svsystems\bin`.</span></span>
3. <span data-ttu-id="8298a-111">Voer nu de opdracht uit.</span><span class="sxs-lookup"><span data-stu-id="8298a-111">Now run the command.</span></span>

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. <span data-ttu-id="8298a-112">Hiermee worden de gegevens van de processerver van het systeem verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8298a-112">This will purge the details of the process server from the system.</span></span>
