---
title: Problemen met Azure Backup-Server | Microsoft Docs
description: Installatie, de registratie van Azure Backup-Server en de back-up en herstel van de toepassing werklast oplossen
services: backup
documentationcenter: 
author: pvrk
manager: shreeshd
editor: 
ms.assetid: 2d73c349-0fc8-4ca8-afd8-8c9029cb8524
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: pullabhk;markgal;
ms.openlocfilehash: 5672bb1e17dac4ae0aaa67f936676d6c2fc5ef12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-azure-backup-server"></a>Problemen met Azure Backup Server oplossen

U kunt er zijn fouten opgetreden tijdens het gebruik van Azure Backup-Server met informatie die worden vermeld in de volgende tabel kunt oplossen.


## <a name="installation-issues"></a>Problemen met de installatie

| Bewerking | Details van fouten | Tijdelijke oplossing |
|-----------|---------------|------------|
|Installeren | Setup kan de metagegevens van het register niet bijwerken. Deze update kan leiden tot via het gebruik van opslagverbruik. Om te voorkomen dat dit de registervermelding ReFS bijsnijden werk. | De registersleutel SYSTEM\CurrentControlSet\Control\FileSystem\RefsEnableInlineTrim aanpassen. De Dword-waarde ingesteld op 1. |
|Installeren | Setup kan de metagegevens van het register niet bijwerken. Deze update kan leiden tot via het gebruik van opslagverbruik. Om te voorkomen dat dit de registervermelding Volume SnapOptimization werk. | De registersleutel, SOFTWARE\Microsoft Data Protection Manager\Configuration\VolSnapOptimization\WriteIds maken met de waarde van een lege tekenreeks. |

## <a name="registration-and-agent-related-issues"></a>Problemen met betrekking tot registratie en Agent
| Bewerking | Details van fouten | Tijdelijke oplossing |
| --- | --- | --- |
| Registreren in een kluis | Ongeldige kluisreferenties opgegeven. Het bestand is beschadigd of heeft niet hebben de meest recente referenties die zijn gekoppeld aan de herstelservice | Deze fout oplossen: <ol><li> Download het meest recente referenties uit de kluis en probeer het opnieuw <br>(OR)</li> <li> Als de bovenstaande actie niet werkt, probeert te downloaden van de referenties naar een andere lokale map of een nieuwe kluis maken <br>(OR)</li> <li> Probeer het bijwerken van de datum- en tijdinstellingen zoals vermeld in de [deze blog](https://azure.microsoft.com/blog/troubleshooting-common-configuration-issues-with-azure-backup/) <br>(OR)</li> <li> Controleer of c:\windows\temp meer dan 65000 zijn bestanden heeft. Verouderde bestanden naar een andere locatie verplaatsen of verwijderen van de items in de map Temp <br>(OR)</li> <li> Controleer de status van certificaten <br> a. Open 'Computercertificaten beheren' (in het Configuratiescherm) <br> b. Vouw het knooppunt 'Persoonlijke' en het onderliggende knooppunt 'Certificaten' <br> c.  Verwijder het certificaat 'Windows Azure-hulpprogramma's ' <br> d. Probeer de registratie in de Azure Backup-client <br> (OR) </li> <li> Controleer of een Groepsbeleid geïmplementeerd is </li></ol> |
| De agents worden gepusht op beveiligde servers | De agentbewerking is mislukt vanwege een communicatiefout met de service DPM Agent Coordinator op \<ServerName > | **Als de aanbevolen actie wordt weergegeven in het product werkt niet**, <ol><li> Als u een computer uit een niet-vertrouwd domein toevoegen wilt, voert u de [deze](https://technet.microsoft.com/library/hh757801(v=sc.12).aspx) stappen <br> (OR) </li><li> Als u een computer van een vertrouwd domein toevoegen wilt, problemen oplossen met behulp van de stappen in [deze blog](https://blogs.technet.microsoft.com/dpm/2012/02/06/data-protection-manager-agent-network-troubleshooting/) <br>(OR)</li><li> Schakelt u Antivirus het oplossen van problemen. Als het probleem is opgelost, de antivirussoftware instellingen zoals voorgesteld in [in dit artikel] wijzigen (https://technet.microsoft.com/library/hh757911.aspx)</li></ol> |
| De agents worden gepusht op beveiligde servers | De referenties die zijn opgegeven voor de server zijn ongeldig | **Als de aanbevolen actie wordt weergegeven in het product werkt niet**, <br> Probeer de beveiligingsagent handmatig installeren op de productieserver zoals opgegeven in de [in dit artikel](https://technet.microsoft.com/library/hh758186(v=sc.12).aspx#BKMK_Manual)|
| Azure Backup-Agent is geen verbinding maken met de Azure Backup-service (ID: 100050) | De Azure Backup Agent is kan geen verbinding maken met de Azure Backup-service. | **Als de aanbevolen actie wordt weergegeven in het product werkt niet**, <br>1. Voer na de opdracht uit vanaf verhoogde vragen, psexec -i -s 'c:\Program Files\Internet Explorer\iexplore.exe' het internet explorer-venster wordt geopend. <br/> 2. Ga naar Extra -> Internet-opties -> verbindingen LAN-instellingen ->. <br/> 3. Controleer de proxy-instellingen voor systeem-account. Stel Proxy IP-adres en poort. <br/> 4. Sluit Internet Explorer.|
| Installatie van Azure Backup-Agent is mislukt | De Microsoft Azure Recovery Services-installatie is mislukt. Alle wijzigingen die door de Microsoft Azure Recovery Services-installatie op het systeem zijn teruggedraaid. (ID: 4024) | Azure-Agent handmatig installeren


## <a name="configuring-protection-group"></a>Configureren van beveiligingsgroep
| Bewerking | Details van fouten | Tijdelijke oplossing |
| --- | --- | --- |
| Beveiligingsgroepen configureren | DPM kan toepassingsonderdeel op beveiligde computer (beveiligde computer Name) niet opsommen | Klik op 'Vernieuwen' in het scherm configureren bescherming groep gebruikersinterface op het niveau van de relevante datasource-component |
| Beveiligingsgroepen configureren | Kan geen beveiliging configureren | Als de beveiligde server een SQL-server is, controleert u of sysadmin-rolmachtigingen zijn verleend aan het systeemaccount (NTAuthority\System) op de beveiligde computer zoals vermeld in de [in dit artikel](https://technet.microsoft.com/library/hh757977(v=sc.12).aspx)
| Beveiligingsgroepen configureren | Er is onvoldoende beschikbare ruimte in de opslaggroep voor deze beveiligingsgroep | De schijven die worden toegevoegd aan de opslaggroep [mag niet een partitie](https://technet.microsoft.com/library/hh758075(v=sc.12).aspx). Verwijder alle bestaande volumes op de schijven en vervolgens toe te voegen aan de opslaggroep|
| Beleid wijzigen |Het back-upbeleid kan niet worden gewijzigd. Fout: De huidige bewerking is mislukt vanwege een interne servicefout [0x29834]. Probeer het later opnieuw. Neem contact op met Microsoft Ondersteuning als het probleem zich blijft voordoen. |**Oorzaak:**<br/>Deze fout wordt geleverd wanneer beveiligingsinstellingen zijn ingeschakeld, u probeert te verkort de bewaartermijn lager dan de minimale waarden die hierboven is opgegeven en u zich op een niet-ondersteunde versie (onder mal versie 2.0.9052 en update 1 voor Azure Backup-server). <br/>**Aanbevolen actie:**<br/> In dit geval moet u de bewaarperiode boven de minimale periode opgegeven bewaarperiode (zeven dagen voor dagelijks, vier weken wekelijks, drie weken voor maandelijks of één jaar voor per jaar) instellen om door te gaan met het beleid betrekking updates. Gewenste aanpak kan eventueel worden back-upagent en Azure Backup-Server wilt gebruiken voor alle beveiligingsupdates bijwerken. |

## <a name="backup"></a>Back-up
| Bewerking | Details van fouten | Tijdelijke oplossing |
| --- | --- | --- |
| Back-up | De replica is inconsistent | U vindt meer informatie over de oorzaken van replica inconsistentie en relevante suggesties [hier](https://technet.microsoft.com/library/cc161593.aspx) <br> <ol><li> In geval van een back-up van systeemstatus/BMR, Controleer of Windows Server back-up wordt geïnstalleerd of niet op de beveiligde Server </li><li> Controleren op ruimte gerelateerde problemen op de DPM-opslag-groep op de server van DPM/MABS en opslag waar nodig toewijzen </li><li> Controleer de status van de Volume shadow copy-service op de beveiligde server. Als deze uitgeschakeld is stelt u deze handmatig starten en start de service op de server. Vervolgens gaat u terug naar de DPM/MABS-console en de synchronisatie met consistentiecontrole gestart.</li></ol>|
| Back-up | Er is een onverwachte fout opgetreden bij het uitvoeren van de taak, het apparaat is niet gereed | **Als de aanbevolen actie wordt weergegeven in het product werkt niet**, <br> <ol><li>De ruimte van de opslagruimte op schaduwkopie ingesteld op onbeperkt op de Items in de beveiligingsgroep en voer de consistentiecontrole <br></li> (OR) <li>Verwijder de bestaande beveiligingsgroep en meerdere nieuwe maken: één met elk afzonderlijke item in het</li></ol> |
| Back-up | Als u een back-up alleen systeemstatus, controleert u of als er voldoende vrije ruimte beschikbaar op de beveiligde computer is voor het opslaan van de back-up van systeemstatus | <ol><li>Controleer of de WSB op de beveiligde computer is geïnstalleerd</li><li>Controleer of voldoende ruimte aanwezig is op de beveiligde computer voor de systeemstatus: de eenvoudigste manier om dit te doen is om te gaan naar de beveiligde computer, opent WSB en klikt u op via de selecties en BMR selecteert. De gebruikersinterface vervolgens vertelt u hoeveel ruimte is vereist voor dit. Open WSB -> lokale back-up -> back-up schema-back-upconfiguratie selecteren > -> volledige server (de grootte wordt weergegeven). Deze grootte wordt gebruikt voor verificatie.</li></ol>
| Back-up | Online herstelpunt is mislukt | Als het foutbericht ' Windows Azure Backup-Agent kon geen momentopname van het geselecteerde volume worden gemaakt ', probeert u de ruimte op replica en herstelpuntvolume te vergroten.
| Back-up | Online herstelpunt is mislukt | Als het foutbericht 'De Windows Azure Backup-Agent kan geen verbinding met de OBEngine-service' staat, moet u controleren of de OBEngine in de lijst bestaat met services op de computer uitgevoerd. Als de OBEngine-service wordt niet uitgevoerd. Gebruik de opdracht 'net start OBEngine' de OBEngine-service te starten.
| Back-up | Online herstelpunt is mislukt | Als het foutbericht 'de wachtwoordzin voor versleuteling voor deze server is niet ingesteld. Configureer een wachtwoordzin voor versleuteling' Probeer te configureren van een wachtwoordzin voor versleuteling. Als dit mislukt, <br> <ol><li>Controleer of de nieuwe locatie of niet bestaat. De locatie in het register HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config met de naam 'ScratchLocation' genoemd, moet bestaan.</li><li> Als de nieuwe locatie bestaat, probeert u opnieuw te registreren met de oude wachtwoordzin. **Wanneer u een wachtwoordzin voor versleuteling configureert, slaat u het op een veilige locatie**</li><ol>
| Back-up | Back-upfouten voor BMR | Als de grootte van BMR reusachtig opnieuw proberen na het verplaatsen van bepaalde toepassingsbestanden naar OS-station |
| Back-up | Fout bij het openen van gedeelde bestanden/mappen | Probeer de antivirussoftware te wijzigen zoals voorgesteld [hier](https://technet.microsoft.com/library/hh757911.aspx)|
| Back-up | Taken voor het maken van online herstelpunten voor VMware VM is mislukt. DPM heeft een fout van VMware tijdens ChangeTracking informatie ophalen. ErrorCode - FileFaultFault (ID 33621) |  1. De ctk op VMWare, voor de betrokken virtuele machines opnieuw instellen <br/> Controleer of de onafhankelijke schijf niet aanwezig zijn op VMWare is <br/> Beveiliging voor de betrokken virtuele machines stoppen en opnieuw te beveiligen met de knop Vernieuwen <br/> Een CC uitvoeren voor de betrokken virtuele machines|


## <a name="change-passphrase"></a>Wachtwoordzin wijzigen
| Bewerking | Details van fouten | Tijdelijke oplossing |
| --- | --- | --- |
| Wachtwoordzin wijzigen |Beveiliging opgegeven PINCODE is onjuist. Geef de juiste beveiliging PINCODE om deze bewerking te voltooien. |**Oorzaak:**<br/> Deze fout wordt geleverd wanneer u ongeldige of verlopen BEVEILIGINGSCODE invoeren tijdens het uitvoeren van kritieke bewerking (zoals wachtwoordzin wijzigen). <br/>**Aanbevolen actie:**<br/> Om de bewerking niet voltooien, moet u geldige BEVEILIGINGSCODE invoeren. Als u de PINCODE, aanmelden bij Azure portal en navigeer naar de Recovery Services-kluis > Instellingen > Eigenschappen > beveiliging-PINCODE genereren. Gebruik deze PINCODE wijzigen wachtwoordzin. |
| Wachtwoordzin wijzigen |Bewerking is mislukt. ID: 120002 |**Oorzaak:**<br/>Deze fout wordt geleverd wanneer beveiligingsinstellingen zijn ingeschakeld, u probeert te wijzigen wachtwoordzin en u zich op een niet-ondersteunde versie.<br/>**Aanbevolen actie:**<br/> Als u wilt wijzigen wachtwoordzin, moet u eerst backup-agent bijwerken naar de minimumversie minimale 2.0.9052 en Azure back-upserver voor minimale update 1, en voer vervolgens geldig BEVEILIGINGSCODE. Als u de PINCODE, aanmelden bij Azure portal en navigeer naar de Recovery Services-kluis > Instellingen > Eigenschappen > beveiliging-PINCODE genereren. Gebruik deze PINCODE wijzigen wachtwoordzin. |


## <a name="configure-email-notifications"></a>E-mailmeldingen configureren
| Bewerking | Details van fouten | Tijdelijke oplossing |
| --- | --- | --- |
| Wilt e-mailmeldingen met Office365 account instellen. | Fout-ID ophalen: 2013| **Oorzaak:**<br/> Het gebruik van Office 365-account <br/> **Aanbevolen actie:**<br/> Het eerste wat om ervoor te zorgen is dat 'Toestaan anonieme Relay op een Ontvangconnector' voor uw DPM-server ingesteld in Exchange is. Hier volgt een koppeling voor het configureren van dit: http://technet.microsoft.com/en-us/library/bb232021.aspx <br/> Als u kan niet een interne SMTP-relay gebruiken en moet instellen met behulp van uw Office 365-server, kunt u IIS moet een relay voor deze instellen. <br/> U moet de DPM-server om te kunnen de SMTP O365 met behulp van IIS https://technet.microsoft.com/en-us/library/aa995718(v=exchg.65).aspx to setup IIS to relay to O365 relay configureren <br/> Belangrijke opmerking: bij stap 3 g -> -> ii, zorg ervoor dat u user@domain.com indeling en niet domein\gebruiker <br/> Punt DPM lokale servername gebruiken als de SMTP-server, poort 587 en vervolgens de e-mailadres voor een gebruiker die de e-mailberichten moeten voortkomen uit. <br/> De gebruikersnaam en wachtwoord op de pagina van de installatie van DPM SMTP moet een domeinaccount in het domein met DPM. <br/> Opmerking: Bij het wijzigen van de SMTP-serveradres de wijziging aanbrengt in de nieuwe instellingen, instellingen te sluiten en opnieuw openen om er zeker van te zijn dat geeft de nieuwe waarde.  Eenvoudig wijzigen en testen duurt niet altijd de nieuwe instellingen zodat het beste testen op deze manier is. <br/> Op elk gewenst moment tijdens dit proces kunt u deze instellingen wissen uit door de DPM-console sluiten en de volgende registersleutels te bewerken:<br/> HKLM\SOFTWARE\Microsoft\Microsoft Data Protection Manager\Notification\ <br/> Verwijder SMTPPassword en SMTPUserName sleutels. <br/> U kunt deze toevoegen in de gebruikersinterface weer wanneer u deze opnieuw te starten.
