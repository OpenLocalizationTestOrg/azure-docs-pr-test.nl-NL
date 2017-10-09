---
title: aaaSubmit taken tooan HPC Pack-cluster in Azure | Microsoft Docs
description: Meer informatie over hoe tooset van een lokale computer toosubmit taken tooan HPC Pack cluster in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 2918cf633917d8730487152e6a5ddb863eb8bb5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-tooan-hpc-pack-cluster-deployed-in-azure"></a>Verzenden van HPC-taken van een lokale computer tooan HPC Pack cluster geïmplementeerd in Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Configureren van een lokale client computer toosubmit taken tooa [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure. Dit artikel laat zien hoe tooset op een lokale computer client toosubmit taak tools via HTTPS toohello cluster in Azure. Op deze manier kunnen verschillende cluster gebruikers taken tooa cloud-gebaseerde HPC Pack cluster kunnen worden verzonden, maar zonder toohello hoofdknooppunt VM rechtstreeks verbinding maken of openen van een Azure-abonnement.

![Verzenden van een taak tooa-cluster in Azure][jobsubmit]

## <a name="prerequisites"></a>Vereisten
* **HPC Pack hoofdknooppunt geïmplementeerd in een Azure VM** -het is raadzaam dat u hulpprogramma's, zoals een [snelstartsjabloon met de Azure](https://azure.microsoft.com/documentation/templates/) of een [Azure PowerShell-script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toodeploy Hallo hoofdknooppunt en cluster. U moet Hallo DNS-naam van het hoofdknooppunt Hallo en Hallo referenties van een Clusterbeheerder Hallo stappen in dit artikel uit te voeren.
* **Clientcomputer** -moet u een Windows- of Windows Server-clientcomputer die HPC Pack client-hulpprogramma's kan worden uitgevoerd (Zie [systeemvereisten](https://technet.microsoft.com/library/dn535781.aspx)). Als u alleen toouse Hallo HPC Pack web-portal of REST-API toosubmit taken wilt, kunt u elke clientcomputer van uw keuze.
* **HPC Pack installatiemedia** -tooinstall Hallo HPC Pack client utilities, gratis Hallo-installatiepakket voor de nieuwste versie van HPC Pack (HPC Pack 2012 R2) is beschikbaar via de [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024). Zorg ervoor dat u Hallo downloaden dezelfde versie van HPC Pack die is geïnstalleerd op Hallo hoofdknooppunt VM.

## <a name="step-1-install-and-configure-hello-web-components-on-hello-head-node"></a>Stap 1: Installeren en configureren van Hallo webonderdelen op Hallo hoofdknooppunt
tooenable een REST-interface toosubmit taken toohello cluster via HTTPS, zorg ervoor dat Hallo HPC Pack webonderdelen zijn geconfigureerd op Hallo HPC Pack hoofdknooppunt. Als ze niet zijn geïnstalleerd, moet u eerst Hallo webonderdelen installeren door het Hallo HpcWebComponents.msi-installatiebestand uitvoeren. Configureer vervolgens Hallo onderdelen Hallo HPC PowerShell-script uit te voeren **Set HPCWebComponents.ps1**.

Zie voor gedetailleerde procedures [installeren Hallo Microsoft HPC Pack webcomponenten](http://technet.microsoft.com/library/hh314627.aspx).

> [!TIP]
> Bepaalde Azure-snelstartsjablonen voor HPC Pack installeren en configureren van webonderdelen Hallo automatisch. Als u Hallo [HPC Pack IaaS-implementatiescript](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate Hallo cluster, u kunt eventueel installeren en configureren van webonderdelen Hallo als onderdeel van Hallo-implementatie.
> 
> 

**tooinstall hello webonderdelen**

1. Verbinding toohello hoofdknooppunt VM via Hallo referenties van de Clusterbeheerder van een.
2. Uitvoeren van Hallo HPC Pack Setup, map, HpcWebComponents.msi op Hallo hoofdknooppunt.
3. Volg de stappen Hallo in Hallo wizard tooinstall Hallo-webonderdelen

**tooconfigure hello webonderdelen**

1. Start op het hoofdknooppunt Hallo HPC PowerShell als beheerder.
2. toochange directory toohello locatie van het Hallo-configuratiescript, type Hallo volgende opdracht:
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. tooconfigure Hallo REST-interface en start Hallo HPC-webservice, type Hallo volgende opdracht:
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. Wanneer na vragen aan gebruiker tooselect een certificaat kiezen Hallo certificaat die overeenkomt met openbare DNS-naam van het hoofdknooppunt Hallo toohello. Bijvoorbeeld, als het implementeren van hoofdknooppunt Hallo VM die gebruikmaakt van Hallo klassieke implementatiemodel, Hallo certificaatnaam ziet als CN eruit =&lt;*HeadNodeDnsName*&gt;. cloudapp.net. Als u Hallo Resource Manager-implementatiemodel, Hallo certificaatnaam ziet eruit als CN =&lt;*HeadNodeDnsName*&gt;.&lt; *regio*&gt;. cloudapp.azure.com.
   
   > [!NOTE]
   > U selecteert dit certificaat later wanneer u taken toohello hoofdknooppunt uit een on-premises computer indienen. Geen selecteren of een certificaat dat overeenkomt met de computernaam toohello van hoofdknooppunt in Active Directory-domein Hallo Hallo configureren (bijvoorbeeld CN =*MyHPCHeadNode.HpcAzure.local*).
   > 
   > 
5. Hallo webportal tooconfigure taak te verzenden, type Hallo volgende opdracht:
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. Nadat het Hallo-script is voltooid, stoppen en opnieuw opstarten Hallo HPC Job Scheduler-Service door Hallo volgende opdrachten te typen:
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-hello-hpc-pack-client-utilities-on-an-on-premises-computer"></a>Stap 2: Hallo HPC Pack client hulpprogramma's installeren op een on-premises computer
Als u tooinstall Hallo HPC Pack client hulpprogramma's op uw computer wilt, de HPC Pack setup-bestanden (volledige installatie) downloaden van Hallo [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024). Wanneer u Hallo installatie begint, selecteer de installatieoptie Hallo voor Hallo **HPC Pack client utilities**.

toouse hello HPC Pack clienthulpprogramma's toosubmit taken toohello hoofdknooppunt VM, u ook een certificaat van het hoofdknooppunt Hallo tooexport nodig hebt en op Hallo-clientcomputer installeren. Hallo-certificaat moet. CER-indeling.

**tooexport hello certificaat van het hoofdknooppunt Hallo**

1. Toevoegen op het hoofdknooppunt hello, Hallo certificaten module tooa Microsoft Management Console voor Hallo lokale computeraccount. Zie voor stappen tooadd Hallo-module [toevoegen Hallo module Certificaten tooan MMC](https://technet.microsoft.com/library/cc754431.aspx).
2. Vouw in de consolestructuur Hallo **certificaten-lokale Computer** > **persoonlijke**, en klik vervolgens op **certificaten**.
3. Hallo-certificaat dat u hebt geconfigureerd voor Hallo HPC Pack webonderdelen in vinden [stap 1: installeren en configureren van Hallo webonderdelen op Hallo hoofdknooppunt](#step-1:-install-and-configure-the-web-components-on-the-head-node) (bijvoorbeeld CN =&lt;*HeadNodeDnsName* &gt;. cloudapp.net).
4. Met de rechtermuisknop op het Hallo-certificaat en klik op **alle taken** > **exporteren**.
5. Klik in de Wizard Certificaat exporteren hello, **volgende**, en zorg ervoor dat **Nee, Hallo persoonlijke sleutel niet exporteren** is geselecteerd.
6. Volg Hallo resterende stappen van de wizard tooexport Hallo-certificaat in DER Hallo encoded binary X.509 (. De indeling van de CER).

**tooimport hello certificaat op de clientcomputer Hallo**

1. Hallo-certificaat dat u hebt geëxporteerd uit Hallo hoofdknooppunt tooa map op de clientcomputer Hallo kopiëren.
2. Klik op de clientcomputer Hallo certmgr.msc worden uitgevoerd.
3. Vouw in de certificaatbeheerder **certificaten-huidige gebruiker** > **Trusted Root Certification Authorities**, met de rechtermuisknop op **certificaten**, en vervolgens Klik op **alle taken** > **importeren**.
4. Klik in de Wizard Certificaat importeren hello, **volgende** en volg Hallo stappen tooimport Hallo certificaat dat u hebt geëxporteerd uit Hallo hoofdknooppunt toohello Trusted Root Certification Authorities opslaan.

> [!TIP]
> U ziet een beveiligingswaarschuwing, omdat het Hallo-certificeringsinstantie op Hallo hoofdknooppunt wordt niet herkend door Hallo-clientcomputer. Voor testdoeleinden kunt u deze waarschuwing en voltooid Hallo certificaat importeren te negeren.
> 
> 

## <a name="step-3-run-test-jobs-on-hello-cluster"></a>Stap 3: Voer testtaken op Hallo-cluster
uw configuratie, probeer actieve taken op Hallo-cluster in Azure van Hallo tooverify lokale computer. U kunt bijvoorbeeld HPC Pack GUI-hulpprogramma's of de opdrachtregelopdrachten toosubmit taken toohello cluster gebruiken. U kunt ook de taken van een web gebaseerde portal toosubmit gebruiken.

**toorun taak verzending van opdrachten op de clientcomputer Hallo**

1. Start een opdrachtprompt op een clientcomputer waarop Hallo HPC Pack client hulpprogramma's zijn geïnstalleerd.
2. Typ een voorbeeld van een opdracht. Bijvoorbeeld toolist alle taken op het Hallo-cluster, typt u een opdracht vergelijkbare tooone te volgen, afhankelijk van de volledige DNS-naam van het hoofdknooppunt Hallo HALLO hallo:
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    of
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > Hallo volledige DNS-naam van hoofdknooppunt hello, niet Hallo IP-adres in Hallo scheduler URL gebruiken. Als u Hallo IP-adres opgeeft, een fout lijkt te ' Hallo-servercertificaat tooeither moet een geldige keten van een vertrouwensrelatie of toobe geplaatst in het vertrouwde basisarchief Hallo. "
   > 
   > 
3. Wanneer u wordt gevraagd, typt u Hallo-gebruikersnaam (in de vorm Hallo &lt;DomainName&gt;\\&lt;gebruikersnaam&gt;) en het wachtwoord van HPC-Clusterbeheer hello of een ander cluster-gebruiker die u hebt geconfigureerd. U kunt toostore Hallo referenties lokaal voor meer taakbewerkingen uit te voeren.
   
    Een lijst met taken wordt weergegeven.

**toouse HPC Job Manager op de clientcomputer Hallo**

1. Als u niet eerder domeinreferenties voor een cluster gebruiker opslaat bij het indienen van een taak, kunt u Hallo-referenties in Aanmeldingsgegevensbeheer toevoegen.
   
    a. Start Referentiebeheer in het Configuratiescherm op Hallo-clientcomputer.
   
    b. Klik op **Windows-referenties** > **toevoegen van een algemene referentie**.
   
    c. Hallo internetadres opgeven (bijvoorbeeld https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler of https://&lt;HeadNodeDnsName&gt;.&lt; regio&gt;.cloudapp.azure.com/HpcScheduler), en de gebruikersnaam hello (&lt;DomainName&gt;\\&lt;gebruikersnaam&gt;) en het wachtwoord van de Clusterbeheerder hello of een ander cluster-gebruiker die u hebt geconfigureerd.
2. Start op de clientcomputer Hallo HPC Job Manager.
3. In Hallo **hoofdknooppunt selecteren** dialoogvenster, type Hallo URL toohello hoofdknooppunt in Azure (bijvoorbeeld https://&lt;HeadNodeDnsName&gt;. cloudapp.net of https://&lt;HeadNodeDnsName&gt;. &lt;regio&gt;. cloudapp.azure.com).
   
    HPC Job Manager wordt geopend en ziet u een lijst met taken op Hallo hoofdknooppunt.

**Hallo-webportal toouse uitgevoerd op het hoofdknooppunt Hallo**

1. Start een webbrowser op Hallo-clientcomputer en voer een van de volgende adressen, afhankelijk van de volledige DNS-naam van het hoofdknooppunt Hallo HALLO hallo:
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    of
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. Typ de domeinreferenties Hallo van Hallo HPC-Clusterbeheer in Hallo beveiliging in het dialoogvenster dat wordt weergegeven. (U kunt ook andere cluster gebruikers toevoegen in verschillende rollen. Zie [het beheren van gebruikers van de Cluster](https://technet.microsoft.com/library/ff919335.aspx).)
   
    Hallo-webportal wordt geopend toohello taak lijstweergave.
3. toosubmit een voorbeeld-taak die Hallo tekenreeks "Hallo wereld" uit Hallo-cluster retourneert, klik op **nieuwe taak** in de linkernavigatiebalk Hallo.
4. Op Hallo **nieuwe taak** pagina onder **van verzending van pagina's**, klikt u op **HelloWorld**. Hallo taak verzendpagina wordt weergegeven.
5. Klik op **indienen**. Als u wordt gevraagd, bieden de domeinreferenties Hallo van Hallo HPC-Clusterbeheer. Hallo-taak wordt verzonden en Hallo taak-ID wordt weergegeven op Hallo **mijn taken** pagina.
6. tooview hello resultaten van het Hallo-taak die u hebt ingediend, klikt u op Hallo taak-ID en klik vervolgens op **taken weergeven** tooview Hallo opdrachtuitvoer (onder **uitvoer**).

## <a name="next-steps"></a>Volgende stappen
* U kunt ook taken toohello Azure cluster Hello verzenden [HPC Pack REST-API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).
* Als u toosubmit cluster taken van een Linux-client wilt, Zie Hallo Python voorbeeld in Hallo [HPC Pack 2012 R2 SDK en voorbeeldcode](https://www.microsoft.com/download/details.aspx?id=41633).

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
