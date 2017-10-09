Hallo-implementatiescript maakt geen Hallo virtuele omgeving op Azure als wordt gedetecteerd dat er al een compatibele virtuele omgeving bestaat.  Dit kan de implementatie aanzienlijk versnellen.  Pakketten die al zijn geïnstalleerd, worden door pip overgeslagen.

In bepaalde situaties kunt u tooforce verwijderen die virtuele omgeving.  Moet u toodo dit als u tooinclude een virtuele omgeving als onderdeel van uw opslagplaats besluit.  U kunt ook toodo dit als u nodig hebt tooget rid bepaalde pakketten of wijzigingen toorequirements.txt te testen.

Er zijn enkele opties toomanage Hallo bestaande virtuele omgeving op Azure:

### <a name="option-1-use-ftp"></a>Optie 1: FTP gebruiken
Toohello server verbinden met een FTP-client, en u zult kunnen toodelete Hallo env map.  Houd er rekening mee dat sommige FTP-clients (zoals webbrowsers) mogelijk alleen-lezen en u geen mappen toodelete, kunnen dus moet u ervoor dat toomake-toouse een FTP-client die wel die mogelijkheid.  Hallo FTP-hostnaam en een gebruiker worden weergegeven in de blade van uw web-app op Hallo [Azure Portal](https://portal.azure.com).

### <a name="option-2-toggle-runtime"></a>Optie 2: runtime wisselen
Hier volgt een alternatief wordt gebruikgemaakt van Hallo fact dat Hallo implementatiescript de map env Hallo worden verwijderd wanneer deze niet overeenkomt met de gewenste versie van Python Hallo.  Dit wordt effectief Hallo bestaande omgeving verwijderen en een nieuwe maken.

1. Switch tooa andere versie van Python (via runtime.txt of Hallo **toepassingsinstellingen** blade in hello Azure Portal)
2. Git push enkele wijzigingen (negeer pip-installatiefouten indien aanwezig)
3. Switch back tooinitial versie van Python
4. Git push sommige wijzigingen opnieuw

### <a name="option-3-customize-deployment-script"></a>Optie 3: implementatiescript aanpassen
Als u Hallo implementatiescript hebt aangepast, kunt u Hallo code in deploy.cmd tooforce het toodelete Hallo env map.

