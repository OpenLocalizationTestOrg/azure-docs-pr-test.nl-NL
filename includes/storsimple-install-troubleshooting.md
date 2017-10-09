<!--author=alkohli last changed: 03/17/16-->

## <a name="troubleshooting-update-failures"></a>Problemen oplossen met mislukte updates
**Wat gebeurt er als u een melding ziet dat Hallo controles van vóór de upgrade is mislukt?**

Als een controle vooraf mislukt, zorg er dan voor dat u Hallo gedetailleerde meldingsbalk onderaan Hallo van Hallo pagina hebt bekeken. Dit biedt richtlijnen, zoals controle vooraf voor toowhich is mislukt. Hallo volgende afbeelding ziet u een exemplaar waarin deze kennisgeving wordt weergegeven. In dit geval Hallo controller statuscontrole en statuscontrole van de hardware-onderdeel is mislukt. Onder Hallo **hardwarestatus** sectie, kunt u zien dat beide **Controller 0** en **Controller 1** onderdelen aandacht vereisen.

  ![Controle vooraf mislukt](./media/storsimple-install-troubleshooting/HCS_PreUpdateCheckFailed-include.png)

Moet u ervoor dat beide domeincontrollers in orde en online zijn toomake. Ook moet u ervoor dat alle Hallo hardwareonderdelen in Hallo StorSimple-apparaat worden weergegeven toobe in orde op de pagina Onderhoud Hallo toomake. Vervolgens kunt u proberen tooinstall updates. Als u niet kunt toofix Hallo hardwareproblemen onderdeel, wordt u toocontact Microsoft Support moet voor de volgende stappen.

**Wat gebeurt er als u het foutbericht 'Kan updates niet installeren' en Hallo aanbeveling is toorefer toohello update handleiding toodetermine Hallo oorzaak van de Hallo fout oplossen?**

Een waarschijnlijke oorzaak voor dit kan zijn dat u geen connectiviteit toohello Microsoft Update-servers hebt. Dit is een handmatige controle die toobe uitgevoerd behoeften. Als u connectiviteit toohello updateserver verliest, zou uw bijwerktaak mislukt. U kunt Hallo connectiviteit controleren door het uitvoeren van de volgende cmdlet uit de Windows PowerShell-interface Hallo van uw StorSimple-apparaat Hallo:

 `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter>`

Hallo-cmdlet uitvoeren op beide domeincontrollers.

Als u hebt gecontroleerd Hallo connectiviteit bestaat en u dit probleem toosee blijven, neem contact met Microsoft Support voor de volgende stappen.

**Wat gebeurt er als er een update-fout bij het bijwerken van uw apparaat tooUpdate 4 en beide domeincontrollers Hallo Update 4 worden uitgevoerd?**

Vanaf Update 4 als beide domeincontrollers Hallo uitgevoerd Hallo dezelfde softwareversie en als er een update mislukt, gaan Hallo domeincontrollers niet in de herstelmodus overgaat. Deze situatie kan zich voordoen als hello apparaat software hotfix (1e volgorde update) is toegepast tooboth Hallo domeincontrollers is maar andere hotfixes (2e volgorde en 3e volgorde) zijn nog toobe toegepast. Starten van de Update 4 gaat Hallo domeincontrollers in de herstelmodus overgaat alleen als u twee domeincontrollers Hallo andere softwareversies worden uitgevoerd. 

Als Hallo gebruiker een update mislukt ziet wanneer beide domeincontrollers bijwerken 4 worden uitgevoerd, raden wij aan dat ze een paar minuten wacht en probeer het vervolgens opnieuw bijwerken. Als Hallo opnieuw proberen niet slaagt, moeten ze contact met Microsoft Support.
