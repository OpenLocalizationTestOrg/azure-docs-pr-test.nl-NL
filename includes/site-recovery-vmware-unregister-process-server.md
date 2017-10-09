Hallo stappen toounregister processerver, is afhankelijk van de verbindingsstatus Hello configuratieserver.

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a>De registratie ongedaan maken van een processerver die is verbonden

1. De afstand in de processerver Hallo als beheerder.
2. Hallo starten **Configuratiescherm** en open **programma's > een programma verwijderen**
3. Een programma verwijderen met de naam van de Hallo **Microsoft Azure Site Recovery configuratieproces/Server**
4. Nadat stap 3 is voltooid, verwijdert u **Microsoft Azure Site Recovery-configuratie-/processerverafhankelijkheden**

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a>De registratie ongedaan maken van een processerver die niet is verbonden

> [!WARNING]
> Hallo Gebruik onderstaande stappen moet worden gebruikt als er geen manier toorevive Hallo virtuele machine op welke Hallo Process-Server is geïnstalleerd.

1. Meld u als beheerder op de configuratieserver tooyour.
2. Open een beheeropdrachtprompt en bladeren door mappen toohello `%ProgramData%\ASR\home\svsystems\bin`.
3. Voer nu Hallo-opdracht.

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. Dit wordt Hallo details van de processerver Hallo leegmaken van het Hallo-systeem.
