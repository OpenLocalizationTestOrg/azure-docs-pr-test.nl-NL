---
title: aaaGet de slag met Azure-logboekanalyse-integratie | Microsoft Docs
description: Ontdek hoe tooinstall hello Azure Meld integration-service en de logboeken van Azure storage, Azure controlelogboeken en waarschuwingen van Azure Security Center integreren.
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 53f67a7c-7e17-4c19-ac5c-a43fabff70e1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 07/26/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 26c19070d76ff73b1bdbd32ba77fb04978af387e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-with-azure-diagnostics-logging-and-windows-event-forwarding"></a>Azure-logboekanalyse-integratie met de logboekregistratie van Azure Diagnostics- en Windows Event Forwarding
Integratie van Azure Log (AzLog) kunt u toointegrate onbewerkte logboeken van uw Azure-resources in uw on-premises Security Information en Event Management SIEM ()-systemen. Deze integratie maakt het mogelijk toohave een dashboard geïntegreerde beveiliging voor alle activa, on-premises of in de cloud hello, zodat u samenvoegen kunt, correleren, analyseren en waarschuwen voor beveiligingsgebeurtenissen die zijn gekoppeld aan uw toepassingen.
>[!NOTE]
Voor meer informatie over Azure Log-integratie kunt u bekijken Hallo [overzicht van de integratie van Azure Log](https://docs.microsoft.com/azure/security/security-azure-log-integration-overview).

In dit artikel helpt u aan de slag met Azure Log integratie door te focussen op Hallo-installatie van Hallo Azlog service en service Hallo integreren met Azure Diagnostics. Hello Azure Log Integration-service worden vervolgens kunnen toocollect Windows-gebeurtenislogboek-informatie van de gebeurtenis beveiligingskanaal Windows hello van virtuele machines die zijn geïmplementeerd in Azure IaaS. Dit is heel vergelijkbaar te 'Event Forwarding' die u hebt gebruikt lokale.

>[!NOTE]
>Hallo mogelijkheid toobring Hallo uitvoer van de integratie van Azure-logboekanalyse in toohello SIEM wordt verstrekt door Hallo SIEM zelf. Zie artikel Hallo [integratie van Azure Log integratie met uw On-premises SIEM](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) voor meer informatie.

toobe duidelijk - hello Azure Log Integration-service wordt uitgevoerd op een fysieke of virtuele computer die van Hallo Windows Server 2008 R2 gebruikmaakt of hoger besturingssysteem (Windows Server 2012 R2 of Windows Server 2016 zijn voorkeur).

Hallo fysieke computer kunt on-premises uitgevoerd (of op een site hoster). Als u toorun hello Azure Log Integration-service op een virtuele machine kiest, waarop de virtuele machine mag zich lokaal of in een openbare cloud, zoals Microsoft Azure.

Hallo fysieke of virtuele machine met hello Azure Log Integration-service vereist network connectivity toohello Azure openbare cloud. Stappen in dit artikel vindt u informatie op Hallo-configuratie.

## <a name="prerequisites"></a>Vereisten
Hallo-installatie van AzLog vereist ten minste Hallo volgende items:
* Een **Azure-abonnement**. Als u nog geen abonnement hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/).
* Een **opslagaccount** die kunnen worden gebruikt voor diagnostische logboekregistratie voor Windows Azure (gebruik een vooraf geconfigureerde opslagaccount of maak een nieuwe – wordt gedemonstreerd hoe tooconfigure Hallo opslagaccount verderop in dit artikel)
  >[!NOTE]
  Afhankelijk van uw scenario kan een opslagaccount niet worden vereist. Voor hello Azure diagnostics scenario beschreven in dit artikel navragen.
* **Twee systemen**: een machine die hello Azure Log Integration-service wordt uitgevoerd en een machine die wordt bewaakt en de bijbehorende logboekinformatie verzonden toohello Azlog service machine hebben.
   * Een machine die u wilt dat toomonitor – dit is een virtuele machine wordt uitgevoerd als een [Azure virtuele Machine](../virtual-machines/virtual-machines-windows-overview.md)
   * Een machine die wordt uitgevoerd hello Azure-logboekanalyse integration-service; Deze computer verzamelt alle Hallo logboekgegevens die later worden geïmporteerd in uw SIEM.
    * Dit systeem kan nu on-premises of in Microsoft Azure.  
    * Het uitvoeren van een x64 toobe moet versie van WindowsServer 2008 R2 SP1 of hoger en .NET Framework 4.5.1 is geïnstalleerd. U kunt bepalen Hallo .NET versie is geïnstalleerd door de volgende Hallo artikel [hoe: bepalen dat .NET Framework-versies zijn geïnstalleerd](https://msdn.microsoft.com/library/hh925568)  
    Connectiviteit toohello Azure storage-account gebruikt voor Azure Diagnostische logboekregistratie moet hebben. We geven instructies verderop in dit artikel over hoe u deze connectiviteit kunt bevestigen

Voor een snelle demonstratie van Hallo proces een maken van een virtuele machine met hello Azure-portal te kijken Hallo video hieronder.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Create-a-Virtual-Machine/player]



## <a name="deployment-considerations"></a>Overwegingen bij de implementatie
Als u Azure Log integratie test, kunt u een systeem dat voldoet aan Hallo minimale besturingssysteemvereisten. Voor een productie-omgeving Hallo kan load vereisen echter tooplan voor schaal omhoog of uit.

Als gebeurtenis volume hoog is, kunt u meerdere exemplaren van hello Azure Log Integration-service (één exemplaar per fysieke of virtuele machine) uitvoeren. U kunt bovendien saldo opslagaccounts Azure Diagnostics voor Windows (af) en het aantal abonnementen tooprovide toohello exemplaren Hallo moeten worden gebaseerd op de capaciteit van de laden.
>[!NOTE]
Op dit moment er geen specifieke aanbevelingen voor wanneer tooscale uit exemplaren van Azure Meld integratie machines (dat wil zeggen, machines die worden uitgevoerd hello Azure-logboekanalyse integration-service), of voor storage-accounts of abonnementen. Schalen van de beslissingen die moet worden gebaseerd op uw prestaties metingen in elk van deze gebieden.

U hebt ook Hallo de tooscale optie up hello Azure Log integratie service toohelp prestaties worden verbeterd. Hallo na maatstaven voor prestaties kunt u in sizing Hallo machines toorun hello Azure-logboekanalyse integration-service te kiezen:
* Op een machine met 8-processor (core), kan één exemplaar van Azlog Integrator ongeveer 24 miljoen gebeurtenissen per dag (~1M/hour) verwerken.

* Op een machine 4-processor (core), kan één exemplaar van Azlog Integrator ongeveer 1,5 miljoen gebeurtenissen per dag (~62.5K/hour) verwerken.

## <a name="install-azure-log-integration"></a>Azure-logboekanalyse-integratie installeren
Integratie van Azure Log tooinstall, moet u toodownload hello [integratie van Azure-logboekanalyse](https://www.microsoft.com/download/details.aspx?id=53324) -bestand voor installatie. Hallo setup routine doorlopen en beslissen of u wilt dat tooprovide telemetrie informatie tooMicrosoft.  

![Installatiescherm met telemetrie selectievakje is ingeschakeld](./media/security-azure-log-integration-get-started/telemetry.png)

*
> [!NOTE]
> We raden u aan Microsoft toocollect telemetrische gegevens. U kunt verzamelen van telemetriegegevens uitschakelen door deze optie uitschakelt.
>


Hello Azure Log Integration-service verzamelt telemetriegegevens van Hallo-machine waarop deze is geïnstalleerd.  

Verzamelde telemetriegegevens is:

* Uitzonderingen die tijdens het uitvoeren van de integratie van Azure-logboekanalyse optreden
* Metrische gegevens over Hallo aantal query's en gebeurtenissen die zijn verwerkt
* Statistieken over welke Azlog.exe opdrachtregelopties worden gebruikt

Hallo-installatieproces valt Hallo video hieronder.
> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Install-Azure-Log-Integration/player]



## <a name="post-installation-and-validation-steps"></a>Na de installatie-en validatie
Na het voltooien van Hallo basisinstellingen routine, bent u gereed stap tooperform na installatie en validatie stappen:
1. Open een PowerShell-venster met verhoogde bevoegdheid en navigeer te**c:\Program Files\Microsoft Azure Log-integratie**
2. Hallo van de eerste stap moet u tootake is tooget hello die azlog Cmdlets geïmporteerd. U kunt dit doen door het Hallo-script uitvoeren **LoadAzlogModule.ps1** (kennisgeving Hallo '. \ ' in de volgende opdracht Hallo). Type **.\LoadAzlogModule.ps1** en druk op **ENTER**.  
U ziet er ongeveer zo wat wordt weergegeven in onderstaande afbeelding ziet Hallo. </br></br>
![Installatiescherm met telemetrie selectievakje is ingeschakeld](./media/security-azure-log-integration-get-started/loaded-modules.png) </br></br>
3. Nu moet u tooconfigure AzLog toouse specifieke Azure-omgeving. Een 'Azure-omgeving' is Hallo 'type' van de Azure-cloud Datacenter toowork met gewenste. Hoewel er verschillende Azure-omgevingen op dit moment, Hallo momenteel relevant zijn de versleutelingsopties **AzureCloud** of **AzureUSGovernment**.   Zorg ervoor dat u in de verhoogde PowerShell-omgeving **c:\program files\Microsoft Azure Log-integratie\** </br></br>
    Zodra er, Hallo-opdracht uitvoeren: </br>
    ``Set-AzlogAzureEnvironment -Name AzureCloud``(voor Azure commercieel)

      >[!NOTE]
      Als Hallo-opdracht is geslaagd, ontvangt u geen opmerkingen of vragen hebt.  Als u wilt dat toouse Hallo US Government Azure-cloud, gebruikt u **AzureUSGovernment** (voor Hallo - variabele naam) voor Hallo cloud van de overheid Verenigde Staten. Andere Azure-clouds worden niet ondersteund op dit moment.  
4. Voordat u een systeem kunt bewaken moet u Hallo-naam van de opslagaccount Hallo gebruikt voor Azure Diagnostics.  In hello Azure-portal te navigeren**virtuele machines** en zoekt u Hallo virtuele machine die u wilt bewaken. In Hallo **eigenschappen** sectie **diagnostische instellingen**.  Klik op **Agent** en noteer Hallo opslagaccountnaam die is opgegeven. U moet deze accountnaam voor een latere stap.
![Diagnostische instellingen voor Azure](./media/security-azure-log-integration-get-started/storage-account-large.png) </br></br>

      ![Diagnostische instellingen voor Azure](./media/security-azure-log-integration-get-started/azure-monitoring-not-enabled-large.png)
      >[!NOTE]
      Als controle is niet ingeschakeld tijdens het maken van de virtuele machine krijgt u Hallo optie tooenable het hierboven beschreven.
5. Nu schakelt we onze aandacht back toohello Azure-logboekanalyse integratie machine. Moeten we tooverify dat u hebt verbinding toohello Storage-Account van Hallo systeem waarop u Azure Log integratie hebt geïnstalleerd. Hallo fysieke computer of virtuele machine met Azure Log integratie service toegang verkrijgen toohello opslag tooretrieve accountgegevens vastgelegd door Azure Diagnostics tot moet zoals geconfigureerd in elk Hallo Hallo bewaakt systemen.  
  1. U kunt Azure Storage Explorer downloaden [hier](http://storageexplorer.com/).
  2. Hallo setup routine doorlopen
  3. Zodra het Hallo-installatie is voltooid Klik **volgende** en laat het selectievakje Hallo **Start Microsoft Azure Storage Explorer** gecontroleerd.  
  4. Meld u bij tooAzure.
  5. Controleer of u kunt zien Hallo storage-account die u hebt geconfigureerd voor Azure Diagnostics.  
![Opslagaccounts](./media/security-azure-log-integration-get-started/storage-account.jpg) </br></br>
   6. U ziet dat er een aantal opties onder storage-accounts. Een van beide is **tabellen**. Onder **tabellen** ziet u een met de naam **WADWindowsEventLogsTable**. </br></br>
   ![Storage-accounts](./media/security-azure-log-integration-get-started/storage-explorer.png) </br>

## <a name="integrate-azure-diagnostic-logging"></a>Integratie van Azure Diagnostische logboekregistratie
In deze stap configureert u Hallo machine hello Azure Log integratie service tooconnect toohello storage-account met logboekbestanden Hallo uitgevoerd.
toocomplete deze stap moeten we een aantal dingen vooraf.  
* **FriendlyNameForSource:** dit is een beschrijvende naam die u toohello storage-account dat u de gegevens van virtuele machine toostore Hallo van Azure Diagnostics hebt geconfigureerd kunt toepassen
* **StorageAccountName:** dit is de naam Hallo van Hallo storage-account die u hebt opgegeven bij het instellen van Azure diagnotics.  
* **StorageKey:** dit Hallo-opslagsleutel voor Hallo storage-account is waar hello Azure Diagnostics-gegevens voor deze virtuele machine wordt opgeslagen.  

Volgende stappen tooobtain Hallo-opslagsleutel Hallo uitvoeren:
 1. Blader toohello [Azure-portal](http://portal.azure.com).
 2. In het navigatiedeelvenster Hallo Hallo Azure-console, Schuif onder toohello en klikt u op **meer services.**

 ![Meer Services](./media/security-azure-log-integration-get-started/more-services.png)
 3. Voer **opslag** in Hallo **Filter** in het tekstvak. Klik op **opslagaccounts** (deze wordt weergegeven nadat u hebt ingevoerd **opslag**)

   ![filtervak](./media/security-azure-log-integration-get-started/filter.png)
 4. Een lijst met opslagaccounts wordt weergegeven, dubbelklikt u op het Hallo-account dat u tooLog opslag toegewezen.

   ![lijst met storage-accounts](./media/security-azure-log-integration-get-started/storage-accounts.png)
 5. Klik op **toegangssleutels** in Hallo **instellingen** sectie.

  ![Toegangstoetsen](./media/security-azure-log-integration-get-started/storage-account-access-keys.png)
 6. Kopiëren **key1** en plaatsen op een veilige locatie die toegankelijk is voor de volgende stap Hallo.

   ![twee toegangssleutels](./media/security-azure-log-integration-get-started/storage-account-access-keys.png)
 7. Open een opdrachtprompt met verhoogde bevoegdheid (Opmerking dat we maken gebruik van een verhoogd opdrachtpromptvenster hier, niet een verhoogde PowerShell-console) op Hallo server dat u Azure Log integratie geïnstalleerd.
 8. Navigeer te**c:\Program Files\Microsoft Azure Log-integratie**
 9. Voer ``Azlog source add <FriendlyNameForTheSource> WAD <StorageAccountName> <StorageKey> `` uit. </br> Bijvoorbeeld ``Azlog source add Azlogtest WAD Azlog9414 fxxxFxxxxxxxxywoEJK2xxxxxxxxxixxxJ+xVJx6m/X5SQDYc4Wpjpli9S9Mm+vXS2RVYtp1mes0t9H5cuqXEw==`` indien Hallo abonnement-ID tooshow omhoog in Hallo gebeurtenis XML gewenst, Hallo abonnement-ID toohello beschrijvende naam toevoegen: ``Azlog source add <FriendlyNameForTheSource>.<SubscriptionID> WAD <StorageAccountName> <StorageKey>`` of bijvoorbeeld``Azlog source add Azlogtest.YourSubscriptionID WAD Azlog9414 fxxxFxxxxxxxxywoEJK2xxxxxxxxxixxxJ+xVJx6m/X5SQDYc4Wpjpli9S9Mm+vXS2RVYtp1mes0t9H5cuqXEw==``

>[!NOTE]  
Wacht too60 minuten en vervolgens Hallo-gebeurtenissen die zijn opgehaald uit Hallo storage-account weergeven. tooview open **Logboeken > Windows-Logboeken > doorgestuurde gebeurtenissen** op Hallo Azlog Integrator.

Hier ziet u een video gaat over Hallo stappen hierboven besproken.
> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Enable-Diagnostics-and-Storage/player]


## <a name="what-if-data-is-not-showing-up-in-hello-forwarded-events-folder"></a>Wat gebeurt er als gegevens, wordt niet weergegeven in Hallo doorgestuurde gebeurtenissen map?
Als na een uur gegevens, niet in Hallo weergegeven wordt **doorgestuurde gebeurtenissen** map, klikt u vervolgens:

1. Hallo machine uitgevoerd hello Azure Log Integration-service en controleer of deze toegang Azure tot. tootest connectiviteit, probeer tooopen hello [Azure-portal](http://portal.azure.com) vanuit Hallo browser.
2. Zorg ervoor dat Hallo gebruikersaccount **Azlog** schrijfrechten heeft op de map Hallo **users\Azlog**.
  <ol type="a">
   <li>Open **Windows Verkenner** </li>
  <li> Navigeer te**c:\users** </li>
  <li> Klik met de rechtermuisknop op **c:\users\Azlog** </li>
  <li> Klik op **beveiliging**  </li>
  <li> Klik op **NT Service\Azlog** en controleer Hallo machtigingen voor het Hallo-account. U kunt als Hallo account op dit tabblad ontbreekt of als de juiste machtigingen Hallo momenteel niet Hallo accountrechten op dit tabblad verlenen.</li>
  </ol>
3.Zorg ervoor dat Hallo storage-account toegevoegd in de opdracht Hallo **Azlog bron toevoegen** wordt weergegeven wanneer u de opdracht Hallo uitvoert **Azlog bronlijst**.
4. Ga te**Logboeken > Windows-Logboeken > toepassing** toosee als er fouten zijn gemeld vanuit hello Azure-logboekanalyse-integratie.


Als u problemen ondervindt tijdens het Hallo-installatie en configuratie, opent u een [ondersteuningsaanvraag](../azure-supportability/how-to-create-azure-support-request.md), selecteer **logboek integratie** als Hallo service waarvoor u ondersteuning aanvraagt.

Een andere ondersteuningsoptie is Hallo [Azure Log integratie MSDN-Forum](https://social.msdn.microsoft.com/Forums/home?forum=AzureLogIntegration). Hier kunt Hallo community ondersteuning voor elkaar met vragen, antwoorden, tips en trucs over hoe tooget meest Hallo buiten Azure Log-integratie. Bovendien hello Azure Log integratie-team dit forum wordt bewaakt en wanneer we kunt.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over de integratie van Azure Log, Zie Hallo documenten te volgen:

* [Microsoft Azure Log-integratie voor Azure logboeken](https://www.microsoft.com/download/details.aspx?id=53324) : Download Center voor meer informatie over de systeemvereisten en instructies op Azure-logboekanalyse-integratie installeren.
* [Inleiding tooAzure logboek integratie](security-azure-log-integration-overview.md) : dit document vindt u tooAzure logboek integratie, de belangrijkste mogelijkheden en hoe het werkt.
* [Partner configuratiestappen](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – dit blogbericht leest u hoe tooconfigure Azure integratie toowork Meld met partneroplossingen Splunk, HP ArcSight en IBM QRadar. Dit is onze richtlijnen voor het huidige op hoe tooconfigure Hallo SIEM-onderdelen. Neem contact op met de leverancier van uw SIEM eerst voor meer informatie.
* [Azure-logboekanalyse integratie Veelgestelde vragen (FAQ)](security-azure-log-integration-faq.md) -deze Veelgestelde vragen over de antwoorden op vragen over Azure-logboekanalyse-integratie.
* [Waarschuwingen met Azure Security Center integreren Meld integratie](../security-center/security-center-integrating-alerts-with-log-integration.md) : dit document leest u hoe toosync Security Center waarschuwingen, samen met de virtuele machine beveiligingsgebeurtenissen die door Azure Diagnostics- en Azure activiteitenlogboeken, zijn verzameld met uw logboekanalyse of SIEM-oplossing.
* [Nieuwe functies voor Azure diagnoses en Azure controlelogboeken](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) : vindt u in dit blogbericht tooAzure controlelogboeken en andere functies waarmee u inzicht in Hallo bewerkingen van uw Azure-resources.
