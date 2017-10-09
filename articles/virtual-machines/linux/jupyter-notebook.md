---
title: een laptop van een Jupyter/IPython aaaCreate | Microsoft Docs
description: Meer informatie over hoe toodeploy hello Jupyter/IPython laptop op een virtuele Linux-machine gemaakt met de Hallo resource manager-implementatiemodel in Azure.
services: virtual-machines-linux
documentationcenter: python
author: crwilcox
manager: wpickett
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 519f36dd-865e-4c1d-abe7-b87037796aa7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 11/10/2015
ms.author: crwilcox
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d7f2e45a8ba95163ebfb0f10babc91a2b3fd9390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a>Een Azure VM Jupyter installeren en uitvoeren van een Jupyter-Notebook in Azure maken
Hallo [Jupyter project](http://jupyter.org), voorheen Hallo [IPython project](http://ipython.org), bevat een verzameling van hulpprogramma's voor wetenschappelijke berekeningen met behulp van krachtige interactieve shells die met Hallo maken van de uitvoering van code combineren een live rekenkundige document. Deze bestanden notebook mag willekeurige tekst, rekenkundige formules, invoer code, resultaten, afbeeldingen, video's en een ander type media dat een moderne webbrowser is in staat om weer te geven. Hiermee wordt aangegeven of u bent helemaal nieuwe tooPython en toolearn wilt in een plezier, interactieve omgeving of komen een aantal ernstige parallel/technische computing, Hallo Jupyter-Notebook is een uitstekende keuze.

![Schermopname](./media/jupyter-notebook/ipy-notebook-spectral.png) met behulp van SciPy en Matplotlib pakketten tooanalyze Hallo structuur van het opnemen van een geluid.

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a>Jupyter twee manieren: De Azure-laptops of aangepaste implementatie
Azure biedt een service die u kunt ook gebruiken[snel starten met Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).  Met behulp van hello Azure Notebook Service, kunt u eenvoudig toegankelijk is via het web interface toegang tooJupyter van toegang tot schaalbare rekenkundige resources met alle Hallo stroom van Python en bijbehorende veel bibliotheken.  Omdat het Hallo-installatie wordt verwerkt door het Hallo-service, kunnen gebruikers toegang tot deze bronnen zonder dat nodig is voor beheer en configuratie door gebruiker Hallo Hallo.

Als het Hallo-notebook service werkt niet voor uw scenario blijven tooread in dit artikel die wordt leert u hoe toodeploy Hallo Jupyter-Notebook in Microsoft Azure met behulp van de virtuele Linux-machines (VM's).

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a>Maken en configureren van een virtuele machine in Azure
de eerste stap Hallo toocreate is een virtuele machine (VM) uitgevoerd op Azure.
Deze virtuele machine is een volledig besturingssysteem in de cloud Hallo en wordt gebruikt voor het uitvoeren van Hallo Jupyter-Notebook. Azure is geschikt voor Linux- en Windows virtuele machines worden uitgevoerd en wordt ingegaan op het Hallo-installatie van Jupyter op beide typen virtuele machines.

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a>Maak een Linux-VM en openen van een poort voor Jupyter
Volg de instructies Hallo [hier] [ portal-vm-linux] toocreate een virtuele machine Hallo *Ubuntu* distributie. Ubuntu Server 14.04 TNS maakt gebruik van deze zelfstudie. We gaan ervan uit dat de gebruikersnaam Hallo *azureuser*.

Nadat Hallo virtuele machine wordt geïmplementeerd, moeten we tooopen van een beveiligingsregel voor op Hallo netwerkbeveiligingsgroep.  Hallo Azure-portal, ga te**Netwerkbeveiligingsgroepen** en open Hallo tabblad voor Hallo beveiligingsgroep bijbehorende tooyour VM. Moet u een inkomende beveiligingsregel tooadd Hello volgende instellingen: **TCP** voor Hallo-protocol,  **\***  voor Hallo bronpoort (openbaar) en **9999** voor Hallo-doelpoort (particuliere).

![schermopname](./media/jupyter-notebook/azure-add-endpoint.png)

In de beveiligingsgroep van uw netwerk, klikt u op **netwerkinterfaces** en Opmerking Hallo **openbaar IP-adres** zoals het benodigde tooconnect tooyour VM in de volgende stap Hallo zal zijn.

## <a name="install-required-software-on-hello-vm"></a>Vereiste software installeren op Hallo VM
toorun Hallo Jupyter-Notebook op de virtuele machine, moet we eerst Jupyter en de bijbehorende afhankelijkheden installeren. Verbind tooyour linux vm die gebruikmaakt van ssh en Hallo gebruikersnaam en wachtwoord paar die u hebt gekozen tijdens het maken van Hallo vm. In deze zelfstudie wordt u met PuTTY en verbinding maken vanaf Windows.

### <a name="installing-jupyter-on-ubuntu"></a>Jupyter op Ubuntu installeren
Installeer Anaconda, een populaire gegevens wetenschappelijke python-distributie met behulp van een Hallo koppelingen van [continue Analytics](https://www.continuum.io/downloads).  Hallo onderstaande koppelingen zijn op Hallo moment van schrijven van dit document, Hallo meest up toodate versies.

#### <a name="anaconda-installs-for-linux"></a>Anaconda installeert voor Linux
<table>
  <th>Python 3.4</th>
  <th>Python 2.7</th>
  <tr>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64-bits</href>
    </td>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64-bits</href>
    </td>
  </tr>
  <tr>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32-bits</href>
    </td>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32-bits</href>
    </td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a>Installeren van Anaconda3 2.3.0 64-bits op Ubuntu
Een voorbeeld: dit is hoe u Anaconda op Ubuntu kunt installeren

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter toohello latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![schermopname](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a>Jupyter configureren en gebruiken van SSL
Na de installatie moet tootake een moment toosetup Hallo-configuratiebestanden voor Jupyter. Als u dreigen bij het configureren van Jupyter ervaart mogelijk handig toolook op Hallo [Jupyter-documentatie voor het uitvoeren van een Server Notebook](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).

Volgende we `cd` toohello directory toocreate onze SSL-certificaat profiel en Hallo profielen configuratiebestand bewerken.

Gebruik Hallo volgende opdracht op Linux.

    cd ~/.jupyter

Gebruik Hallo opdracht toocreate Hallo SSL-certificaat (Linux en Windows) te volgen.

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

Houd er rekening mee dat omdat u een zelfondertekend SSL-certificaat, wanneer u verbinding maakt toohello notebook uw browser u een beveiligingswaarschuwing weergegeven krijgt.  Voor gebruik in productieomgevingen op lange termijn zult u toouse een correct ondertekend certificaat dat is gekoppeld aan uw organisatie.  Aangezien Certificaatbeheer buiten bereik van deze demo hello is, wordt er tooa zelf-ondertekend certificaat stick nu.

Bovendien toousing een certificaat, moet u ook opgeven een wachtwoord tooprotect uw laptop tegen onbevoegd gebruik.  Uit veiligheidsoverwegingen Jupyter versleutelde wachtwoorden in het configuratiebestand, dus u tooencrypt moet uw wachtwoord wordt gebruikt eerst.  IPython biedt een hulpprogramma toodo Hallo volgende opdracht achter de opdrachtprompt worden uitgevoerd.

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

Dit wordt u gevraagd om een wachtwoord en de bevestiging en wordt vervolgens Hallo wachtwoord afdrukken. Let op Hallo stap

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided hello rest for security)

Vervolgens bewerken we configuratiebestand Hallo-profiel, wat de `jupyter_notebook_config.py` in Hallo-map in.  Opmerking dat dit bestand bestaat mogelijk niet--alleen maken als dit Hallo geval is.  Dit bestand heeft een aantal velden en standaard alle zijn opgenomen als opmerkingen.  U kunt dit bestand openen in een teksteditor openen van uw eigen smaak en moet u ervoor zorgen dat deze ten minste heeft Hallo volgende inhoud. **Ervoor tooreplace hello c.NotebookApp.password in de configuratie met Hallo sha1 uit de vorige stap Hallo Hallo worden**.

    c = get_config()

    # You must give hello path toohello certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-hello-jupyter-notebook"></a>Hallo Jupyter-Notebook uitvoeren
We zijn nu gereed toostart hello Jupyter-Notebook. toodo, toohello directory toostore notitieblokken in en start Hallo Jupyter-Notebook server met volgende opdracht Hallo navigeren.

    /anaconda3/bin/jupyter-notebook

U moet nu worden kunnen tooaccess uw Jupyter-Notebook op Hallo adres `https://[PUBLIC-IP-ADDRESS]:9999`.

Wanneer u uw laptop voor het eerst opent, wordt de Hallo-aanmeldingspagina om uw wachtwoord gevraagd. En wanneer u zich aanmeldt, ziet u Hallo 'Jupyter-Notebook Dashboard', die het center ontrole voor alle bewerkingen van de laptop is.  U kunt via deze pagina nieuwe notitieblokken maken en bestaande bestanden te openen.

![schermopname](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-hello-jupyter-notebook"></a>Met behulp van Hallo Jupyter-Notebook
Als u klikt op Hallo **nieuw** knop klikt, ziet u Hallo openingspagina te volgen.

![schermopname](./media/jupyter-notebook/jupyter-untitled-notebook.png)

Hallo gebied gemarkeerd met een `In []:` vragen invoergebied hello, en kunt u hier geldige Python-code invoeren en deze wordt uitgevoerd als u raakt `Shift-Enter` of klik op het pictogram Hallo 'Afspelen' (Hallo rechts driehoek op Hallo werkbalk).

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a>Een krachtige paradigma: live rekenkundige documenten met uitgebreide media
Hallo-notebook zelf erop vertrouwen dat logisch tooanyone die heeft gebruikt Python en een tekstverwerker, omdat deze zich in een aantal manieren een combinatie van beide: blokken Python-code kan worden uitgevoerd, maar u kunt ook opmerkingen en andere tekst houden door te wijzigen van de stijl van een cel vanuit 'Code' Hallo 'Ma rkdown' hello vervolgkeuzelijst met op de werkbalk.

Jupyter nog veel meer dan een tekstverwerkingsprogramma zoals kunt u de combinatie van berekening en rijke media (tekst, afbeeldingen, video en vrijwel alles die een moderne webbrowser kunt weergeven). U kunt combineren, tekst, code, video's en meer!

![schermopname](./media/jupyter-notebook/jupyter-editing-experience.png)

En met Hallo kracht van Python van veel uitstekende bibliotheken voor technische en wetenschappelijke computergebruik in Hallo volgende schermafdruk is een eenvoudige berekening Hello dezelfde als een analyse complexe netwerk in een omgeving vereenvoudigen kan worden uitgevoerd.

Dit paradigma van Hallo power van moderne web Hallo combineren met live berekening biedt veel mogelijkheden en is ideaal voor cloud Hallo; Hallo Notebook kan worden gebruikt:

* Als een rekenkundige Kladblok toorecord experimentele werken op een probleem.
* tooshare resulteert met collega's, 'live' rekenkundige vorm of in papier indelingen (HTML-, PDF-bestand).
* toodistribute aanwezig live lesmateriaal die betrekking hebben op berekening, zodat studenten onmiddellijk met echte code hello experimenteren kunnen, wijzigen en opnieuw interactief uit te voeren.
* tooprovide 'uitvoerbare papier' hello resultaten van onderzoek aanwezig zijn op een manier die direct kan worden gereproduceerd, gevalideerd en uitgebreid door anderen.
* Als een platform voor samenwerking computing: meerdere gebruikers kunnen zich aanmelden in toothe dezelfde notebook server tooshare een live rekenkundige sessie.

Wanneer u toohello IPython broncode gaat [opslagplaats][repository], vindt u een hele map met notebook voorbeelden die u kunt downloaden en vervolgens experimenteren met op uw eigen Jupyter Azure VM.  Gewoon downloaden Hallo `.ipynb` bestanden van Hallo site en uploaden naar Hallo dashboard van uw laptop virtuele machine van Azure (of deze rechtstreeks in VM Hallo downloaden).

## <a name="conclusion"></a>Conclusie
Hallo Jupyter-Notebook biedt een krachtige interface voor toegang tot interactief Hallo power van Hallo Python-ecosysteem in Azure.  Er wordt een breed scala aan gebruik gevallen, met inbegrip van eenvoudige exploratie en leren Python, data-analyse en visualisatie, simulatie en parallelle berekeningen aangegeven. Hallo resulterende Notebook documenten bevatten een volledig overzicht van Hallo berekeningen die worden uitgevoerd en kunnen worden gedeeld met andere Jupyter-gebruikers.  Hallo Jupyter-Notebook kan worden gebruikt als een lokale toepassing, maar dit is ideaal voor cloudimplementaties op Azure

Hallo kernfuncties van Jupyter zijn ook beschikbaar in Visual Studio via de [Python-Tools voor Visual Studio] [ Python Tools for Visual Studio] (PTVS). PTVS is een gratis en open-source-invoegtoepassing van Microsoft Visual Studio in een geavanceerde Python-ontwikkelomgeving waarin een geavanceerde editor met IntelliSense foutopsporing, verandert profileringsoptimalisaties en parallelle berekeningen integratie.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie, Hallo [Python Developer Center](/develop/python/).

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
