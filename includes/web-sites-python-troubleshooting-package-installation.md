Sommige pakketten kunnen niet worden geïnstalleerd met pip wanneer ze worden uitgevoerd op Azure.  Dit kan eenvoudig komen dat Hallo-pakket is niet beschikbaar op Hallo Python Package Index.  Kan het zijn dat een compiler vereist is (een compiler is niet beschikbaar op Hallo machine uitgevoerd Hallo web-app in Azure App Service).

In deze sectie zullen we manieren toodeal bij dit probleem.

### <a name="request-wheels"></a>Wheels aanvragen
Als het Hallo-pakketinstallatie een compiler vereist, moet u Neem contact op met Hallo pakket eigenaar toorequest wheels beschikbaar gesteld voor Hallo-pakket.

Met de recente beschikbaarheid Hallo van [Microsoft Visual C++ Compiler voor Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], is nu eenvoudiger toobuild pakketten met systeemeigen code voor Python 2.7.

### <a name="build-wheels-requires-windows"></a>Wheels bouwen (vereist Windows)
Opmerking: Wanneer u deze optie gebruikt, zorg ervoor dat toocompile Hallo pakket met behulp van een Python-omgeving die overeenkomt met de Hallo platform of architectuur of versie die wordt gebruikt op Hallo web-app in Azure App Service (Windows/32-bit/2.7 of 3.4).

Hallo-pakket wordt niet geïnstalleerd omdat het een compiler vereist, kunt u Hallo compiler installeren op uw lokale machine en een wheel bouwen voor Hallo-pakket dat u vervolgens kunt in uw opslagplaats opnemen.

Gebruikers van Mac/Linux: Als u geen toegang tot tooa Windows-computer, Zie [maken van een virtuele Machine met Windows] [ Create a Virtual Machine Running Windows] voor het toocreate een virtuele machine in Azure.  U kunt toobuild Hallo wheels worden gebruikt, deze opslagplaats toohello toevoegen en Hallo VM desgewenst verwijderen. 

U kunt installeren voor Python 2.7 [Microsoft Visual C++ Compiler voor Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].

U kunt installeren voor Python 3.4 [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].

wheels toobuild, hebt u Hallo wheel-pakket nodig:

    env\scripts\pip install wheel

U `pip wheel` toocompile een afhankelijkheid:

    env\scripts\pip wheel azure==0.8.4

Hiermee maakt u een .whl-bestand in de map \wheelhouse Hallo.  De map \wheelhouse hello en wheel-bestanden tooyour opslagplaats toevoegen.

Bewerken van uw requirements.txt tooadd hello `--find-links` optie Hallo bovenaan. Hiermee wordt de pip toolook schrijfopdrachten naar een exacte overeenkomst in de lokale map Hallo voor voortdurende toohello python package index.

    --find-links wheelhouse
    azure==0.8.4

Als u wilt dat alle afhankelijkheden in Hallo \wheelhouse map en geen gebruik Hallo python-pakket index helemaal tooinclude, kunt u pip tooignore Hallo package index forceren door toe te voegen `--no-index` toohello boven Requirements.txt.

    --no-index

### <a name="customize-installation"></a>Installatie aanpassen
U kunt aanpassen Hallo implementatie script tooinstall een pakket in Hallo virtuele omgeving met een alternatief installatieprogramma zoals easy\_installeren.  Zie deploy.cmd voor een voorbeeld met opmerkingen.  Zorg ervoor dat dergelijke pakketten zijn niet opgenomen in requirements.txt tooprevent pip ze installeert.

Dit script toohello implementatie toevoegen:

    env\scripts\easy_install somepackage

Hebt u mogelijk ook kunnen eenvoudig toouse\_tooinstall installeren vanaf een exe-installatieprogramma (sommige zijn zip-compatibel, dus eenvoudige\_installatie ondersteunt).  Voeg Hallo installatieprogramma tooyour opslagplaats toe en roep easy\_installeren met de Hallo pad toohello uitvoerbare doorgeven.

Dit script toohello implementatie toevoegen:

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a>Hallo virtuele omgeving opnemen in Hallo-opslagplaats (vereist Windows)
Opmerking: Wanneer u deze optie gebruikt, zorg ervoor dat toouse een virtuele omgeving die overeenkomt met de Hallo platform of architectuur of versie die wordt gebruikt op Hallo web-app in Azure App Service (Windows/32-bit/2.7 of 3.4).

Als u Hallo virtuele omgeving in de opslagplaats hello opneemt, kunt u voorkomen dat het implementatiescript Hallo virtuele omgeving op Azure beheeractiviteiten doen door een leeg bestand te maken:

    .skipPythonDeployment

Het is raadzaam dat u Hallo bestaande virtuele omgeving op Hallo app tooprevent er bestanden overblijven uit verwijdert wanneer Hallo virtuele omgeving automatisch werd beheerd.

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
