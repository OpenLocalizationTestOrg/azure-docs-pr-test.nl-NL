---
title: aaaSet van een virtuele machine als een server IPython Notebook | Microsoft Docs
description: Instellen van een Azure virtuele Machine voor gebruik in een omgeving met wetenschappelijke gegevens met IPython Server voor geavanceerde analyses.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 818617c1-048e-49c2-b941-f9a983f93998
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: 58386140ec7742ade1f7e183ec842a2b09b9dfca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>Een virtuele Azure-machine instellen als IPython Notebook-server voor geavanceerde analyses
Dit onderwerp wordt beschreven hoe tooprovision en configureren van een virtuele machine van Azure voor geavanceerde analyses die kunnen worden gebruikt als onderdeel van een wetenschappelijke gegevensomgeving. Hallo Windows virtuele machine is geconfigureerd met ondersteunende hulpprogramma's zoals IPython laptop, Azure Storage Explorer, AzCopy, evenals andere hulpprogramma's die handig voor geavanceerde analyses projecten zijn. Azure Storage Explorer en AzCopy, bijvoorbeeld bieden handige manieren tooupload gegevens tooAzure blob-opslag van uw lokale computer of toodownload het lokale computer tooyour van blob-opslag.

## <a name="create-vm"></a>Stap 1: Een voor algemene doeleinden Azure virtuele machine maken
Als u al een virtuele machine van Azure hebt en tooset van een server IPython Notebook erop gewoon wilt, kunt u deze stap overslaan en doorgaan te[stap 2: een eindpunt voor IPython notitieblokken tooan bestaande virtuele machine toevoegen](#add-endpoint).

Voordat u begint Hallo-proces voor het maken van een virtuele machine in Azure, moet u toodetermine Hallo grootte van Hallo-machine die gegevens van de benodigde tooprocess Hallo voor hun project. Kleinere machines minder geheugen en CPU-kernen minder dan grotere machines hebben, maar ze zijn ook minder duur. Zie voor een lijst van de machine typen en prijzen Hallo <a href="http://azure.microsoft.com/pricing/details/virtual-machines/" target="_blank">prijzen van virtuele Machines </a> pagina

1. Meld u bij te<a href="https://manage.windowsazure.com" target="_blank">klassieke Azure-portal</a>, en klik op **nieuw** in Hallo linkerbenedenhoek. Een venster wordt weergegeven. Selecteer **COMPUTE** -> **virtuele MACHINE** -> **FROM GALERIE**.
   
    ![Werkruimte maken][24]
2. Kies een van de Hallo installatiekopieën van het volgende:
   
   * Windows Server 2012 R2 Datacenter
   * Windows Server Essentials Experience (Windows Server 2012 R2)
     
     Klik vervolgens op Hallo pijl rechts op Hallo lagere rechts toogo Hallo volgende configuratiepagina.
     
     ![Werkruimte maken][25]
3. Voer een naam in voor Hallo virtuele machine die u wilt toocreate, selecteer Hallo grootte van Hallo-machine (standaard: A3) op basis van Hallo grootte van Hallo gegevens Hallo machine is momenteel tooprocess en hoe krachtig wilt Hallo machine toobe (geheugen grootte en Hallo aantal compute kernen) , voer een gebruikersnaam en wachtwoord voor Hallo-machine. Klik vervolgens op Hallo pijl-rechts toogo toohello volgende configuratiepagina.
   
    ![Werkruimte maken][26]
4. Selecteer Hallo **regio/AFFINITEIT groep/VIRTUEEL netwerk** die Hallo bevat **OPSLAGACCOUNT** dat u van plan bent toouse voor deze virtuele machine en selecteer vervolgens dit opslagaccount. Een eindpunt toevoegen aan de onderkant Hallo in Hallo **EINDPUNTEN** veld hiertoe Hallo-naam van het Hallo-eindpunt ('IPython' hier). U kunt een willekeurige tekenreeks als Hallo **naam** van Hallo-eindpunt en een geheel getal tussen 0 en 65536 die **beschikbaar** als Hallo **openbare poort**. Hallo **particuliere poort** heeft toobe **9999**. U moet **voorkomen** via openbare poorten die al zijn toegewezen voor internet-services. <a href="http://www.chebucto.ns.ca/~rakerman/port-table.html" target="_blank">Poorten voor internetservices</a> bevat een lijst met poorten die zijn toegewezen en moeten worden vermeden.
   
    ![Werkruimte maken][27]
5. Klik op Hallo vinkje toostart Hallo virtuele machine inrichtingsproces.
   
    ![Werkruimte maken][28]

Het kan 15-25 minuten toocomplete Hallo virtuele machine inrichtingsproces duren. Nadat het Hallo virtuele machine is gemaakt, Hallo status van deze machine moet worden weergegeven als **met**.

![Werkruimte maken][29]

## <a name="add-endpoint"></a>Stap 2: Een eindpunt voor IPython notitieblokken tooan bestaande virtuele machine toevoegen
Als u Hallo virtuele machine door Hallo aanwijzingen in stap 1 hebt gemaakt, Hallo-eindpunt voor de IPython Notebook is al toegevoegd en worden deze stap overgeslagen.

Hallo virtuele machine bestaat al en moet u een eindpunt tooadd voor IPython laptop die u in stap 3 hieronder wilt installeren, eerste aanmelding tooAzure klassieke portal, selecteer Hallo virtuele machine als Hallo-eindpunt voor de IPython Notebook server toevoegen. Hallo bevat volgende afbeelding een schermopname van Hallo portal nadat Hallo-eindpunt voor de IPython Notebook tooa Windows virtuele machine is toegevoegd.

![Werkruimte maken][17]

## <a name="run-commands"></a>Stap 3: IPython laptops en andere ondersteunende hulpprogramma's installeren
Nadat Hallo virtuele machine is gemaakt, gebruikt u de Remote Desktop Protocol (RDP) toolog in toohello virtuele Windows-machine. Zie voor instructies [hoe tooLog op virtuele Machine Running Windows Server tooa](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Open Hallo **opdrachtprompt** (**niet Hallo Powershell-opdrachtvenster**) als een **beheerder** en Voer Hallo de volgende opdracht.

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

Wanneer Hallo-installatie is voltooid, Hallo IPython Notebook server automatisch wordt gestart in Hallo *C:\\gebruikers\\\<gebruikersnaam\>\\documenten\\IPython Laptops* directory.

Voer desgevraagd een wachtwoord voor Hallo IPython Notebook en wachtwoord op Hallo van Hallo machine beheerder. Hierdoor Hallo IPython Notebook toorun als een service op Hallo-machine.

## <a name="access"></a>Stap 4: Toegang IPython notitieblokken van een webbrowser
tooaccess hello IPython Notebook server, open een web browser en invoer *https://&#60;virtual machine DNS-naam >: &#60; openbare poortnummer >* in tekstvak Hallo-URL. Hier Hallo *&#60; openbare poortnummer >* moet Hallo-poortnummer dat is opgegeven als hello IPython laptop-eindpunt is toegevoegd.

Hallo *&#60; de virtuele machine DNS-naam >* kan worden gevonden op Hallo klassieke Azure-portal. Nadat de logboekregistratie in de klassieke portal toohello, klikt u op **virtuele MACHINES**, selecteer Hallo machine hebt gemaakt Selecteer vervolgens **DASHBOARD**, Hallo DNS-naam wordt als volgt weergegeven:

![Werkruimte maken][19]

U ontvangt een waarschuwing dat *er is een probleem met het beveiligingscertificaat van deze website* (Internet Explorer) of *uw verbinding is niet persoonlijk* (Chrome), zoals wordt weergegeven in de volgende Hallo cijfers. Klik op **doorgaan toothis website (niet aanbevolen)** (Internet Explorer) of **Geavanceerd** en vervolgens  **te gaan &#60;* DNS-naam*> (onveilig) ** toocontinue (Chrome). Voer vervolgens Hallo wachtwoord u opgegeven eerdere tooaccess IPython notitieblokken Hallo.

**Internet Explorer:**
![werkruimte maken][20]

**Chrome:**
![werkruimte maken][21]

Nadat u zich aanmeldt toohello IPython laptop, een map *DataScienceSamples* worden weergegeven op de Hallo browser. Deze map bevat voorbeeld IPython laptops die worden gedeeld door Microsoft toohelp gebruikers verloop gegevens wetenschappelijke taken. Deze voorbeeld IPython laptops zijn uitgecheckt uit [ **GitHub-opslagplaats** ](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) toohello virtuele machines tijdens Hallo IPython Notebook server setup-proces. Microsoft onderhoudt en deze repository regelmatig worden bijgewerkt. Gebruikers kunnen bezoeken Hallo GitHub-opslagplaats tooget Hallo meest recente voorbeeld IPython laptops.
![Werkruimte maken][18]

## <a name="upload"></a>Stap 5: Een bestaande IPython laptop van een lokale computer toohello IPython Notebook server uploaden
IPython notitieblokken bieden een eenvoudige manier voor gebruikers tooupload de laptop van een bestaande IPython op hun lokale machines toohello IPython laptop-server op Hallo virtuele machines. Nadat u zich aanmeldt toohello IPython laptop in een webbrowser, klikt u op in Hallo **directory** die Hallo IPython Notebook om te worden geüpload. Selecteer een tooupload IPython Notebook .ipynb-bestand van de lokale computer Hallo in Hallo **Verkenner**, en met slepen en neerzetten toohello IPython Notebook directory op Hallo webbrowser. Klik op Hallo **uploaden** knop tooupload hello .ipynb bestand toohello IPython laptop-server. Andere gebruikers kunnen vervolgens starten voor het gebruik hiervan in vanuit hun webbrowser.

![Werkruimte maken][22]

![Werkruimte maken][23]

## <a name="shutdown"></a>Afsluiten en de virtuele machine als deze niet in gebruik toewijzen
Virtuele Machines in Azure worden berekend als **Betaal alleen voor wat u**. tooensure die u niet worden kosten in rekening gebracht wanneer de virtuele machine niet wordt gebruikt, heeft de toobe hello **gestopt (Deallocated)** status als deze niet in gebruik.

> [!NOTE]
> Als u Hallo virtuele machine afsluiten uit binnen de virtuele machine (met behulp van Windows-Energiebeheer), Hallo Hallo VM is gestopt, maar blijft toegewezen. virtuele machines van Hallo wordt altijd gestopt als u niet doorgaat toobe kosten in rekening gebracht, tooensure [klassieke Azure-portal](http://manage.windowsazure.com/). U kunt ook Hallo VM via Powershell voorkomen door het aanroepen van **ShutdownRoleOperation** met 'PostShutdownAction' gelijk aan 'StoppedDeallocated'.
> 
> 

tooshut omlaag en Hallo virtuele machine ongedaan gemaakt:

1. Meld u bij toohello [klassieke Azure-portal](http://manage.windowsazure.com/) met uw account.  
2. Selecteer **virtuele MACHINES** van Hallo linkernavigatiebalk.
3. Hallo lijst met virtuele machines, klik op het Hallo-naam van uw virtuele machine en ga toohello **DASHBOARD** pagina.
4. Klik onder aan de pagina Hallo Hallo op **afsluiten**.

![VM afsluiten][15]

Hallo virtuele machine wordt de toewijzing ongedaan gemaakt maar niet verwijderd. U kunt uw virtuele machine opnieuw opstarten op elk gewenst moment Hallo klassieke Azure-portal.

## <a name="your-azure-vm-is-ready-toouse-whats-next"></a>Uw Azure VM is gereed toouse: Wat is het volgende?
De virtuele machine is nu gereed toouse in uw gegevens wetenschappelijke oefeningen. Hallo virtuele machine is ook klaar voor gebruik als een server IPython Notebook voor Hallo exploratie en verwerking van gegevens en andere taken in combinatie met Azure Machine Learning en Hallo Team gegevens wetenschappelijke processen.

Hallo volgende stappen in de procedure van wetenschappelijke gegevens Team zijn toegewezen in Hallo Hallo [pad Learning](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) en stappen voor het verplaatsen van gegevens in HDInsight, proces en het voorbeeld ter voorbereiding van het leren van Hallo gegevens met Azure Machine bevatten mogelijk Learning.

[15]: ./media/machine-learning-data-science-setup-virtual-machine/vmshutdown.png
[17]: ./media/machine-learning-data-science-setup-virtual-machine/add-endpoints-after-creation.png
[18]: ./media/machine-learning-data-science-setup-virtual-machine/sample-ipnbs.png
[19]: ./media/machine-learning-data-science-setup-virtual-machine/dns-name-and-host-name.png
[20]: ./media/machine-learning-data-science-setup-virtual-machine/browser-warning-ie.png
[21]: ./media/machine-learning-data-science-setup-virtual-machine/browser-warning.png
[22]: ./media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-1.png
[23]: ./media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-2.png
[24]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-1.png
[25]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-2.png
[26]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-3.png
[27]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-4.png
[28]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-5.png
[29]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-6.png
