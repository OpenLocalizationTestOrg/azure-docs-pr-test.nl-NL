---
title: aaaAzure MFA-Server upgrade | Microsoft Docs
description: Stappen en richtlijnen tooupgrade hello Azure multi-factor Authentication-Server tooa nieuwere versie.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: aaa8d400e0e5f1c6be3a6d22cde6dd893ef4d546
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-toohello-latest-azure-multi-factor-authentication-server"></a>Upgrade toohello meest recente Azure multi-factor Authentication-Server

Dit artikel begeleidt u bij Hallo upgradeproces Azure multi-factor Authentication (MFA) Server 6.0 of hoger. Als u een oude versie van de PhoneFactor Agent Hallo tooupgrade nodig hebt, raadpleegt u te[Upgrade Hallo PhoneFactor Agent tooAzure multi-factor Authentication-Server](multi-factor-authentication-get-started-server-upgrade.md).

Als u upgraden vanaf versie 6.x of oudere toov7.x of hoger wilt, Wijzig alle onderdelen van .NET 2.0 too.NET 4.5. Alle onderdelen moeten ook Microsoft Visual C++ Redistributable Update 2015 1 of hoger. Als ze niet al zijn geïnstalleerd, installeert Hallo MFA-Server installatieprogramma beide Hallo x86- en x64 versies van deze onderdelen. Als Hallo Gebruikersportal en de webservice voor mobiele App worden uitgevoerd op afzonderlijke servers, moet u op tooinstall die pakketten vóór de upgrade van deze onderdelen. U kunt zoeken naar de nieuwste Microsoft Visual C++ 2015 Redistributable update Hallo op Hallo [Microsoft Download Center](https://www.microsoft.com/en-us/download/). 

## <a name="install-hello-latest-version-of-azure-mfa-server"></a>Installeer de nieuwste versie Hallo van Azure MFA-Server

1. Volg de instructies Hallo in [downloaden hello Azure multi-factor Authentication-Server](multi-factor-authentication-get-started-server.md#download-the-azure-multi-factor-authentication-server) tooget Hallo meest recente versie van hello Azure MFA-Server.
2. Maak een back-up van Hallo gegevensbestand voor MFA-Server zich bevindt op C:\Program Files\Multi-Factor Authentication Server\Data\PhoneFactor.pfdata (uitgaande Hallo installeren standaardlocatie) op de master MFA-Server.
3. Als u meerdere servers voor hoge beschikbaarheid uitvoeren, wijzigt u Hallo clientsystemen die toohello MFA-Server te verifiëren zodat ze stoppen met het verzenden van verkeer toohello-servers die een upgrade uitvoert. Als u een load balancer, een MFA-Server verwijderen van Hallo load balancer, Hallo upgrade en vervolgens weer in de farm Hallo toevoegen Hallo-server.
4. Hallo nieuwe installatieprogramma uitvoeren op elke MFA-Server. Ondergeschikte servers eerst upgraden omdat Hallo oude gegevensbestand gerepliceerd door Hallo master kan worden gelezen. 

  U hoeft uw huidige MFA-Server voordat u actieve Hallo-installatieprogramma niet toouninstall. Hallo-installatieprogramma voert een in-place upgrade. Hallo installatiepad wordt opgehaald uit het register van de vorige installatie Hallo Hallo zodat deze wordt geïnstalleerd in Hallo dezelfde locatie (bijvoorbeeld C:\Program Files\Multi-Factor Authentication Server). 
  
5. Als u na vragen aan gebruiker tooinstall een Microsoft Visual C++ Redistributable 2015-updatepakket voor bent, kunt u Hallo prompt accepteren. Beide versies Hallo x86- en x64 van Hallo pakket worden geïnstalleerd.
5. Als u Hallo Web Service SDK gebruikt, wordt u gevraagd tooinstall Hallo nieuwe webservice-SDK. Bij het installeren van nieuwe webservice-SDK Hallo, zorg ervoor dat naam van de virtuele map Hallo overeenkomt met de eerder geïnstalleerde Hallo virtuele map (bijvoorbeeld MultiFactorAuthWebServiceSdk).
6. Herhaal stap Hallo op alle onderliggende servers. Promoveer een van Hallo onderliggende niveaus toobe Hallo nieuwe master en vervolgens de upgrade Hallo oude masterserver. 

## <a name="upgrade-hello-user-portal"></a>Hallo User Portal bijwerken

1. Maak een back-up van Hallo web.config-bestand dat zich in de virtuele map Hallo Hallo Gebruikersportal installatielocatie (bijvoorbeeld C:\inetpub\wwwroot\MultiFactorAuth). Als er wijzigingen zijn aangebracht toohello standaardthema, moet u een back-up van Hallo App_Themes\Default map ook. Het is beter toocreate een kopie van de standaardmap Hallo en maak een nieuwe thema dan toochange Hallo standaardthema.
2. Als Hallo User Portal wordt uitgevoerd op dezelfde server als de andere onderdelen MFA-Server Hallo HALLO hallo MFA-Server-installatie wordt u gevraagd tooupdate hello Gebruikersportal. Hallo prompt accepteren en Hallo Gebruikersportal update installeert. Controleer de naam van de virtuele map van die Hallo overeenkomt met Hallo eerder geïnstalleerde virtuele map (bijvoorbeeld MultiFactorAuth).
3. Hallo User Portal is op een eigen server, Hallo MultiFactorAuthenticationUserPortalSetup64.msi bestandskopie uit Hallo installatielocatie van een van de Hallo MFA Servers als plaatsen op Hallo User Portal-webserver. Hallo-installatieprogramma wordt uitgevoerd. 

  Als er een fout optreedt vermelden 'Microsoft Visual C++ Redistributable Update 2015 1 of hoger is vereist,' download en installeer de meest recente updatepakket Hallo via Hallo [Microsoft Download Center](https://www.microsoft.com/download/). Beide versies van x86- en x64 Hallo installeren.

4. Nadat de Hallo bijgewerkt Gebruikersportal software is geïnstalleerd, vergelijken Hallo web.config back-up die u in stap 1 met het nieuwe bestand web.config Hallo hebt gemaakt. Als er geen nieuwe kenmerken aanwezig zijn in het nieuwe bestand web.config hello, kopieert u uw back-web.config in Hallo virtuele map toooverwrite Hallo nieuwe. Er is een andere optie toocopy en plakken Hallo appSettings waarden en Web Service SDK-URL van back-upbestand in de nieuwe web.config Hallo HALLO hallo.

Als u Hallo Gebruikersportal op meerdere servers hebt, herhaalt u Hallo-installatie voor al deze. 


## <a name="upgrade-hello-mobile-app-web-service"></a>Hallo Mobile App Web Service bijwerken

1. Maak een back-up van Hallo web.config-bestand dat in de virtuele map Hallo Hallo webservice voor mobiele App installatielocatie (bijvoorbeeld C:\inetpub\wwwroot\app of C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService).
2. Hallo MultiFactorAuthenticationMobileAppWebServiceSetup64.msi bestandskopie uit Hallo installatielocatie Hallo MFA-Servers en plaatsen op Hallo mobiele App registratie-webserver.
3. Hallo-installatieprogramma wordt uitgevoerd. 

  Als een fout met de mededeling optreedt dat Microsoft Visual C++ Redistributable Update 2015 1 of hoger vereist is, downloadt en installeert u de meest recente updatepakket Hallo van Hallo [Microsoft Download Center](https://www.microsoft.com/download/). Beide versies van x86- en x64 Hallo installeren.

4. Vergelijk Hallo web.config-bestand dat een back-in stap 1 met het nieuwe bestand web.config Hallo nadat Hallo bijgewerkt webservice voor mobiele App software is geïnstalleerd. Als er geen nieuwe kenmerken aanwezig zijn in het nieuwe bestand web.config hello, kunt u uw opgeslagen web.config kopiëren naar de virtuele map Hallo en Hallo nieuwe overschrijven. Er is een andere optie toocopy en plakken Hallo appSettings waarden en Web Service SDK-URL van back-upbestand in de nieuwe web.config Hallo HALLO hallo.

Als u Hallo webservice voor mobiele App op meerdere servers hebt, herhaalt u Hallo-installatie voor al deze. 

## <a name="upgrade-hello-ad-fs-adapters"></a>Upgrade Hallo AD FS-Adapters


### <a name="if-mfa-runs-on-different-servers-than-ad-fs"></a>Als MFA wordt uitgevoerd op andere servers dan de AD FS

Deze instructies zijn alleen van toepassing als u multi-factor Authentication-Server los van uw AD FS-servers uitvoeren. Als beide services zijn uitgevoerd op Hallo van dezelfde servers, kunt u deze sectie overslaan en toohello installatiestappen gaat. 

1. Sla een kopie van Hallo MultiFactorAuthenticationAdfsAdapter.config-bestand dat is geregistreerd in AD FS of met behulp van de volgende PowerShell-opdracht Hallo Hallo-configuratie te exporteren: `Export-AdfsAuthenticationProviderConfigurationData -Name [adapter name] -FilePath [path tooconfig file]`. Hallo adapternaam is 'WindowsAzureMultiFactorAuthentication' of 'AzureMfaServerAuthentication', afhankelijk van Hallo-versie die eerder is geïnstalleerd.
2. Kopieer Hallo volgende bestanden uit Hallo MFA-Server installatie locatie toohello AD FS-servers:

  - MultiFactorAuthenticationAdfsAdapterSetup64.msi
  - Register-MultiFactorAuthenticationAdfsAdapter.ps1
  - Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
  - MultiFactorAuthenticationAdfsAdapter.config

3. Hallo Register-MultiFactorAuthenticationAdfsAdapter.ps1 script bewerken door toe te voegen `-ConfigurationFilePath [path]` toohello einde van Hallo `Register-AdfsAuthenticationProvider` opdracht. Vervang *[pad]* met Hallo volledig pad toohello MultiFactorAuthenticationAdfsAdapter.config bestand of Hallo-configuratiebestand hebt geëxporteerd in de vorige stap Hallo. 

  Controleer Hallo kenmerken in het nieuwe MultiFactorAuthenticationAdfsAdapter.config toosee Hallo als deze overeenkomen met de oude configuratiebestand Hallo. Als de kenmerken die zijn toegevoegd of verwijderd in de nieuwe versie hello, Hallo kenmerkwaarden van Hallo oude configuratie bestand toohello nieuwe kopiëren of Hallo oude configuratie bestand toomatch wijzigen.

### <a name="install-new-ad-fs-adapters"></a>Nieuwe AD FS-adapters installeren

> [!IMPORTANT] 
> Uw gebruikers zich niet de vereiste tooperform in twee stappen verificatie tijdens de stappen 3-8 van deze sectie. Als u AD FS geconfigureerd in meerdere clusters, u kunt verwijderen, upgrade en terugzetten van ieder cluster in Hallo farm onafhankelijk van andere clusters tooavoid uitvaltijd Hallo.

1. Verwijder enkele AD FS-servers uit Hallo-farm. Bijwerken van deze servers tijdens het Hallo die anderen worden nog steeds uitgevoerd.
2. Hallo nieuwe AD FS-adapter installeren op elke server die is verwijderd uit Hallo AD FS-farm. Als Hallo MFA-Server op elke AD FS-server is geïnstalleerd, kunt u bijwerken via Hallo MFA-Server-beheerder UX Anders wordt bijgewerkt door het uitvoeren van de bestanden MultiFactorAuthenticationAdfsAdapterSetup64.msi. 

  Als er een fout optreedt vermelden 'Microsoft Visual C++ Redistributable Update 2015 1 of hoger is vereist,' download en installeer de meest recente updatepakket Hallo via Hallo [Microsoft Download Center](https://www.microsoft.com/download/). Beide versies van x86- en x64 Hallo installeren.

3. Ga te**AD FS** > **verificatiebeleid** > **algemeen meervoudig verificatiebeleid bewerken**. Schakel het selectievakje **WindowsAzureMultiFactorAuthentication** of **AzureMFAServerAuthentication** (afhankelijk van de huidige versie Hallo geïnstalleerd). 

  Nadat deze stap voltooid is, is verificatie in twee stappen via MFA-Server niet beschikbaar in dit cluster AD FS totdat u stap 8.

4. Unregister Hallo oudere versie van Hallo AD FS-adapter Hallo Unregister-MultiFactorAuthenticationAdfsAdapter.ps1 PowerShell-script uit te voeren. Zorg ervoor dat Hallo *-naam* parameter ('WindowsAzureMultiFactorAuthentication' of 'AzureMFAServerAuthentication') die overeenkomt met Hallo naam wordt weergegeven in stap 3. Dit geldt tooall servers in Hallo dezelfde AD FS-cluster, omdat er een centraal configuratie.
5. De nieuwe AD FS-adapter Hallo registreren Hallo Register-MultiFactorAuthenticationAdfsAdapter.ps1 PowerShell-script uit te voeren. Dit geldt tooall servers in Hallo dezelfde AD FS-cluster, omdat er een centraal configuratie.
6. Opnieuw opstarten Hallo AD FS-service op elke server die is verwijderd uit Hallo AD FS-farm.
7. Hallo bijgewerkt servers back toohello AD FS-farm en verwijder andere servers van de farm Hallo Hallo toevoegen.
8. Ga te**AD FS** > **verificatiebeleid** > **algemeen meervoudig verificatiebeleid bewerken**. Controleer **AzureMfaServerAuthentication**.
9. Herhaal stap 2 tooupdate Hallo servers nu van Hallo AD FS-farm verwijderd en opnieuw starten Hallo AD FS-service op die servers.
10. Deze servers naar Hallo AD FS-farm toevoegen.

## <a name="next-steps"></a>Volgende stappen

- Voorbeelden van ophalen [geavanceerde scenario's met Azure multi-factor Authentication en VPN's van derden](multi-factor-authentication-advanced-vpn-configurations.md)

- [MFA-Server met Windows Server Active Directory synchroniseren](multi-factor-authentication-get-started-server-dirint.md)

- [Windows-verificatie configureren](multi-factor-authentication-get-started-server-windows.md) voor uw toepassingen
