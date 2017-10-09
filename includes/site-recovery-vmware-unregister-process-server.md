<span data-ttu-id="3ddc3-101">Hallo stappen toounregister processerver, is afhankelijk van de verbindingsstatus Hello configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="3ddc3-101">hello steps toounregister a process server differs depending on its connection status with hello Configuration Server.</span></span>

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a><span data-ttu-id="3ddc3-102">De registratie ongedaan maken van een processerver die is verbonden</span><span class="sxs-lookup"><span data-stu-id="3ddc3-102">Unregister a process server that is in a connected state</span></span>

1. <span data-ttu-id="3ddc3-103">De afstand in de processerver Hallo als beheerder.</span><span class="sxs-lookup"><span data-stu-id="3ddc3-103">Remote into hello process server as an Administrator.</span></span>
2. <span data-ttu-id="3ddc3-104">Hallo starten **Configuratiescherm** en open **programma's > een programma verwijderen**</span><span class="sxs-lookup"><span data-stu-id="3ddc3-104">Launch hello **Control Panel** and open **Programs > Uninstall a program**</span></span>
3. <span data-ttu-id="3ddc3-105">Een programma verwijderen met de naam van de Hallo **Microsoft Azure Site Recovery configuratieproces/Server**</span><span class="sxs-lookup"><span data-stu-id="3ddc3-105">Uninstall a program by hello name **Microsoft Azure Site Recovery Configuration/Process Server**</span></span>
4. <span data-ttu-id="3ddc3-106">Nadat stap 3 is voltooid, verwijdert u **Microsoft Azure Site Recovery-configuratie-/processerverafhankelijkheden**</span><span class="sxs-lookup"><span data-stu-id="3ddc3-106">Once step 3 is completed, you can uninstall **Microsoft Azure Site Recovery Configuration/Process Server Dependencies**</span></span>

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a><span data-ttu-id="3ddc3-107">De registratie ongedaan maken van een processerver die niet is verbonden</span><span class="sxs-lookup"><span data-stu-id="3ddc3-107">Unregister a process server that is in a disconnected state</span></span>

> [!WARNING]
> <span data-ttu-id="3ddc3-108">Hallo Gebruik onderstaande stappen moet worden gebruikt als er geen manier toorevive Hallo virtuele machine op welke Hallo Process-Server is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3ddc3-108">Use hello below steps should be used if there is no way toorevive hello virtual machine on which hello Process Server was installed.</span></span>

1. <span data-ttu-id="3ddc3-109">Meld u als beheerder op de configuratieserver tooyour.</span><span class="sxs-lookup"><span data-stu-id="3ddc3-109">Log on tooyour configuration server as an Administrator.</span></span>
2. <span data-ttu-id="3ddc3-110">Open een beheeropdrachtprompt en bladeren door mappen toohello `%ProgramData%\ASR\home\svsystems\bin`.</span><span class="sxs-lookup"><span data-stu-id="3ddc3-110">Open an Administrative command prompt and browse toohello directory `%ProgramData%\ASR\home\svsystems\bin`.</span></span>
3. <span data-ttu-id="3ddc3-111">Voer nu Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="3ddc3-111">Now run hello command.</span></span>

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. <span data-ttu-id="3ddc3-112">Dit wordt Hallo details van de processerver Hallo leegmaken van het Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="3ddc3-112">This will purge hello details of hello process server from hello system.</span></span>
