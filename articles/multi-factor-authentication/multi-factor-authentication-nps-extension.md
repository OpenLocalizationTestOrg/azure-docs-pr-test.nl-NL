---
title: aaaUse bestaande NPS-servers tooprovide Azure MFA mogelijkheden | Microsoft Docs
description: Hallo Network Policy Server-extensie voor Azure multi-factor Authentication is een eenvoudige oplossing tooadd in twee stappen cloud-gebaseerde vericiation mogelijkheden tooyour bestaande verificatie-infrastructuur.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: e9fc495b06873d45f06233f1aa618db9d94f8bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-existing-nps-infrastructure-with-azure-multi-factor-authentication"></a>Uw bestaande NPS-infrastructuur integreren met Azure multi-factor Authentication

Hallo Network Policy Server (NPS)-extensie voor Azure MFA toevoegen cloud-gebaseerde MFA mogelijkheden tooyour verificatie-infrastructuur met behulp van uw bestaande servers U kunt met Hallo NPS-extensie, telefoongesprek, tekstbericht of telefoon-app verificatie tooyour bestaande authenticatiestroom toevoegen zonder tooinstall, configureren en onderhouden van nieuwe servers. 

Deze uitbreiding is gemaakt voor organisaties die tooprotect VPN-verbindingen willen zonder hello Azure MFA-Server implementeren. Hallo NPS extensie fungeert als een adapter tussen RADIUS- en cloud-gebaseerde Azure MFA tooprovide een tweede factor-verificatie voor federatieve of gesynchroniseerde gebruikers.

Wanneer u Hallo NPS-extensie voor Azure MFA, omvat authenticatiestroom Hallo Hallo volgende onderdelen: 

1. **NAS/VPN-Server** ontvangt verzoeken van VPN-clients en converteert deze naar RADIUS-aanvragen tooNPS servers. 
2. **NPS-Server** tooActive Directory tooperform Hallo primaire verificatie voor Hallo RADIUS aanvragen en, als dit lukt, geeft Hallo aanvraag tooany geïnstalleerd extensies verbindt.  
3. **NPS-extensie** een aanvraag tooAzure MFA voor Hallo secundaire verificatie wordt geactiveerd. Zodra het Hallo-extensie antwoord Hallo ontvangt, en als Hallo MFA-controle is geslaagd, is Hallo authenticatie-aanvraag voltooid door beveiligingstokens waarin een claim MFA, uitgegeven door Azure STS Hallo NPS-server te bieden.  
4. **Azure MFA** communiceert met Azure Active Directory tooretrieve Hallo de gegevens van gebruiker en Hallo van de secundaire verificatie met behulp van een gebruiker verificatie methode geconfigureerd toohello uitvoert.

Hallo volgende diagram ziet u deze op hoog niveau authenticatiestroom voor aanvraag: 

![Stroomdiagram voor verificatie](./media/multi-factor-authentication-nps-extension/auth-flow.png)

## <a name="plan-your-deployment"></a>Uw implementatie plannen

Hallo NPS extensie verwerkt automatisch redundantie, dus u een speciale configuratie hoeft.

U kunt zoveel Azure MFA-functionaliteit van NPS-servers als u nodig hebt. Als u meerdere servers installeert, moet u een clientcertificaat verschil voor elk van deze. Een certificaat voor elke server maakt, wordt u kunt elke cert afzonderlijk bijwerken en u geen zorgen over uitvaltijd in al uw servers.

VPN-servers routeren verificatieaanvragen, zodat ze toobe op de hoogte van Hallo nieuwe Azure MFA-functionaliteit van NPS-servers nodig.

## <a name="prerequisites"></a>Vereisten

Hallo NPS-extensie is bedoeld toowork in uw bestaande infrastructuur. Zorg ervoor dat u hebt Hallo volgende vereisten voordat u begint.

### <a name="licenses"></a>Licenties

Hallo NPS-extensie voor Azure MFA is beschikbaar toocustomers met [licenties voor Azure multi-factor Authentication](multi-factor-authentication.md) (meegeleverd bij Azure AD Premium, EMS of een MFA-abonnement).

### <a name="software"></a>Software

Windows Server 2008 R2 SP1 of hoger.

### <a name="libraries"></a>Bibliotheken

Deze bibliotheken worden automatisch geïnstalleerd met de Hallo-extensie.
-   [Visual C++ Redistributable Packages for Visual Studio 2013 (X64)](https://www.microsoft.com/download/details.aspx?id=40784)
-   [Microsoft Azure Active Directory-Module voor Windows PowerShell versie 1.1.166.0](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)

### <a name="azure-active-directory"></a>Azure Active Directory

Iedereen met Hallo NPS extensie moet gesynchroniseerde tooAzure Active Directory via Azure AD Connect en moet worden geregistreerd voor MFA.

Wanneer u Hallo extensie installeert, moet u Hallo directory-ID en de Administrator-referenties voor uw Azure AD-tenant. U vindt de ID van uw directory in Hallo [Azure-portal](https://portal.azure.com). Meld u aan als beheerder, selecteer Hallo **Azure Active Directory** pictogram aan de linkerkant hello, selecteer vervolgens **eigenschappen**. Kopiëren Hallo GUID in Hallo **map-ID** vak en op te slaan. Gebruikt u deze GUID als Hallo tenant-ID wanneer u Hallo NPS extensie installeert.

![De ID van uw Directory onder de eigenschappen van de Azure Active Directory zoeken](./media/multi-factor-authentication-nps-extension/find-directory-id.png)

## <a name="prepare-your-environment"></a>Uw omgeving voorbereiden

Voordat u Hallo NPS extensie installeert, kunt u tooprepare u omgeving toohandle Hallo verificatieverkeer.

### <a name="enable-hello-nps-role-on-a-domain-joined-server"></a>Hallo NPS-rol op een domein-server inschakelen

Hallo NPS-server verbindt tooAzure Active Directory en verifieert Hallo MFA aanvragen. Kies een server voor deze rol. Het is raadzaam om het kiezen van een server die aanvragen van andere services kunnen niet worden verwerkt omdat Hallo NPS extensie genereert fouten voor alle aanvragen die niet zijn van RADIUS.

1. Open op uw server Hallo **Wizard Functies toevoegen en onderdelen** van Hallo Serverbeheer Quickstart-menu.
2. Kies **op basis van functie of onderdeel gebaseerde installatie** voor uw installatietype.
3. Selecteer Hallo **Network Policy and Access Services** serverfunctie. Een venster kan pop-tooinform u vereiste onderdelen toorun deze rol.
4. Hallo wizard vervolgen tot Hallo bevestigingspagina. Selecteer **installeren**.

Nu dat u een aangewezen voor NPS-server hebt, moet u ook deze toohandle server configureren binnenkomende RADIUS-aanvragen van Hallo VPN-oplossing.

### <a name="configure-your-vpn-solution-toocommunicate-with-hello-nps-server"></a>Uw VPN-oplossing toocommunicate met Hallo NPS-server configureren

Hallo stappen tooconfigure uw RADIUS-verificatiebeleid variëren afhankelijk van welke VPN-oplossing u gebruikt. Dit beleid toopoint tooyour NPS RADIUS-server configureren.

### <a name="sync-domain-users-toohello-cloud"></a>Synchronisatie van domein gebruikers toohello cloud

Deze stap is mogelijk al voltooid voor uw tenant, maar het is goed toodouble te controleren of Azure AD Connect uw databases onlangs is gesynchroniseerd.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com) als beheerder.
2. Selecteer **Azure Active Directory** > **Azure AD Connect**
3. Controleer of de synchronisatiestatus van uw **ingeschakeld** en dat de laatste synchronisatie minder dan een uur geleden.

Als u tookick uit een nieuwe ronde van synchronisatie moet, ons instructies in Hallo [Azure AD Connect-synchronisatie: Scheduler](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler).

### <a name="determine-which-authentication-methods-your-users-can-use"></a>Bepalen welke verificatiemethoden die uw gebruikers gebruiken kunnen.

Er zijn twee factoren die van invloed zijn op welke verificatiemethoden zijn beschikbaar bij de implementatie van een NPS-extensie:

1. Hallo wachtwoord-versleutelingsalgoritme gebruikt tussen Hallo RADIUS-client (VPN, Netscaler-server, of andere) en Hallo NPS-servers.
   - **PAP** ondersteunt alle Hallo-verificatiemethoden van Azure MFA in de cloud Hallo: telefoonoproep, eenzijdige SMS-bericht, mobiele-appmelding en verificatiecode mobiele app.
   - **CHAPv2** en **EAP** telefoongesprek en mobiele-appmelding ondersteunen.
2. Hallo invoer methoden die Hallo van client-toepassing (VPN, Netscaler-server, of andere) kan verwerken. Bijvoorbeeld, Hallo VPN-client heeft een manier tooallow Hallo gebruiker tootype in een verificatiecode uit een tekst- of mobiele app?

Wanneer u een uitbreiding van Hallo NPS implementeert, gebruikt u deze factoren tooevaluate welke methoden zijn beschikbaar voor uw gebruikers. Als de RADIUS-client PAP ondersteunt, maar Hallo client UX geen invoervelden voor een verificatiecode, vervolgens zijn telefoongesprek en mobiele-appmelding Hallo twee ondersteunde opties.

U kunt [uitschakelen van niet-ondersteunde verificatiemethoden](multi-factor-authentication-whats-next.md#selectable-verification-methods) in Azure.

### <a name="enable-users-for-mfa"></a>Gebruikers voor MFA inschakelen

Voordat u de volledige NPS-extensie Hallo implementeert, moet u tooenable MFA voor dat u wilt dat de verificatie in twee stappen tooperform Hallo-gebruikers. Meer onmiddellijk tootest Hallo extensie als u deze implementeert, moet u minstens één test-account dat volledig is geregistreerd voor multi-factor Authentication.

Gebruik deze stappen tooget een testaccount gestart:
1. Aanmelden te[https://aka.ms/mfasetup](https://aka.ms/mfasetup) met een testaccount. 
2. Ga als volgt Hallo prompts tooset van een verificatiemethode.
3. Maak een beleid voor voorwaardelijke toegang of [wijzigen van de gebruikersstatus Hallo](multi-factor-authentication-get-started-user-states.md) Hallo testaccount toorequire %0 verificatie. 

Uw gebruikers moeten ook toofollow deze stappen tooenroll voordat ze kunnen worden geverifieerd met Hallo NPS-extensie.

## <a name="install-hello-nps-extension"></a>Hallo NPS uitbreiding installeren

> [!IMPORTANT]
> Hallo NPS uitbreiding installeren op een andere server dan Hallo VPN-toegangspunt.

### <a name="download-and-install-hello-nps-extension-for-azure-mfa"></a>Download en installeer Hallo NPS-extensie voor Azure MFA

1.  [Hallo NPS-uitbreiding downloaden](https://aka.ms/npsmfa) van Hallo Microsoft Download Center.
2.  Hallo binaire toohello Network Policy Server u tooconfigure wilt kopiëren.
3.  Voer *setup.exe* en volg Hallo installatie-instructies. Als er fouten optreden, controleer dan dat Hallo twee tapewisselaars van sectie Hallo-vereisten zijn geïnstalleerd.

### <a name="run-hello-powershell-script"></a>Hallo PowerShell-script uitvoeren

Hallo-installatieprogramma maakt een PowerShell-script op deze locatie: `C:\Program Files\Microsoft\AzureMfa\Config` (waarbij C:\ is voor uw installatiestation). Deze PowerShell-script voert Hallo van de volgende activiteiten:

-   Een zelfondertekend certificaat maken.
-   De openbare sleutel Hallo Hallo certificaat toohello service-principal over Azure AD koppelt.
-   Hallo cert opslaan in certificaatarchief Hallo-lokale computer.
-   Verleen toegang toohello van certificaat persoonlijke sleutel tooNetwork gebruiker.
-   Opnieuw opstarten Hallo NPS.

Tenzij u wilt toouse uw eigen certificaten (in plaats van Hallo zelfondertekende certificaten die PowerShell script genereert Hallo), PowerShell-Script Hallo toocomplete Hallo installatie uitvoeren. Als u Hallo-extensie op meerdere servers installeert, moet elk criterium een eigen certificaat hebben.

1. Voer Windows PowerShell als beheerder.
2. Wijzig de mappen.

   `cd "C:\Program Files\Microsoft\AzureMfa\Config"`

3. Hallo PowerShell-script is gemaakt door Hallo installatieprogramma uitvoeren.

   `.\AzureMfaNpsExtnConfigSetup.ps1`

4. PowerShell wordt u gevraagd om uw tenant-ID. Hallo Directory ID GUID die u hebt gekopieerd uit hello Azure-portal in de sectie vereisten hello gebruiken.
5. Meld u aan tooAzure AD als beheerder.
6. PowerShell ziet een bericht wanneer het Hallo-script is voltooid.  

Herhaal deze stappen uit op eventuele aanvullende NPS-servers die u wilt dat tooset voor taakverdeling.

>[!NOTE]
>Als u uw eigen certificaten gebruiken in plaats van genereren van certificaten met Hallo PowerShell-script, ervoor zorgen dat ze toohello NPS naamconventie uitgelijnd. Hallo onderwerpnaam moet **CN =\<TenantID\>, OU = Microsoft NPS extensie**. 

## <a name="configure-your-nps-extension"></a>De NPS-uitbreiding configureren

Deze sectie bevat overwegingen bij het ontwerpen en suggesties voor geslaagde implementaties voor NPS-extensie.

### <a name="configuration-limitations"></a>Configuratie-beperkingen

- Hallo NPS-extensie voor Azure MFA omvat geen extra toomigrate gebruikers en -instellingen van MFA-Server toohello cloud. Daarom is het raadzaam met Hallo-extensie voor nieuwe implementaties in plaats van bestaande implementatie. Als u Hallo-extensie op een bestaande implementatie gebruikt, uw gebruikers hebben tooperform bewijs-up opnieuw toopopulate hun MFA details in Hallo cloud.  
- Hallo NPS extensie Hallo UPN van Hallo lokale Active directory tooidentify Hallo gebruiker op de Azure MFA voor het uitvoeren van Hallo secundaire Auth. Hallo extensie geconfigureerde toouse een andere id zoals alternatieve aanmeldings-ID of aangepaste Active Directory kunnen worden gebruikt veld dan UPN. Zie [geavanceerde configuratieopties voor Hallo NPS-extensie voor multi-factor Authentication](multi-factor-authentication-advanced-vpn-configurations.md) voor meer informatie.
- Niet alle versleuteling protocollen ondersteunen alle verificatiemethoden voor.
   - **PAP** ondersteunt telefoongesprek, eenzijdige SMS-bericht, mobiele-appmelding en verificatiecode mobiele app
   - **CHAPv2** en **EAP** ondersteuning voor telefoongesprekken en meldingen voor mobiele Apps

### <a name="control-radius-clients-that-require-mfa"></a>Besturingselement RADIUS-clients die MFA vereisen

Zodra u MFA voor een RADIUS-client met behulp van Hallo NPS-extensie inschakelen, worden alle verificaties voor deze client vereist tooperform MFA. Als u tooenable MFA voor bepaalde RADIUS-clients, maar andere niet wilt, kunt u twee NPS-servers configureren en installeren van Hallo-extensie op slechts een van deze. RADIUS-clients die u wilt toorequire MFA toosend aanvragen toohello NPS-server geconfigureerd met Hallo-uitbreiding en andere RADIUS-clients toohello NPS-server niet is geconfigureerd met de extensie Hallo configureren.

### <a name="prepare-for-users-that-arent-enrolled-for-mfa"></a>Voorbereiden voor gebruikers die niet zijn geregistreerd voor MFA

Als u gebruikers die niet zijn geregistreerd voor MFA hebt, kunt u bepalen wat er gebeurt wanneer ze tooauthenticate proberen. Gebruik de registerinstelling Hallo *REQUIRE_USER_MATCH* in het registerpad Hallo *HKLM\Software\Microsoft\AzureMFA* toocontrol Hallo functie gedrag. Deze instelling heeft een configuratie voor één optie:

| Sleutel | Waarde | Standaard |
| --- | ----- | ------- |
| REQUIRE_USER_MATCH | WAAR/ONWAAR | Niet ingesteld (gelijkwaardige tooTRUE) |

doel van deze instelling Hallo toodetermine is welke toodo wanneer een gebruiker niet is ingeschreven voor MFA. Wanneer Hallo sleutel bestaat niet, is niet ingesteld of tooTRUE, is ingesteld en Hallo gebruiker niet is ingeschreven en vervolgens Hallo-uitbreiding niet Hallo MFA uitdaging. Wanneer Hallo sleutel tooFALSE is ingesteld en Hallo gebruiker niet is ingeschreven, wordt de authenticatie voortgezet zonder dat u MFA uitvoert.

U kunt kiezen toocreate deze sleutel en stel deze tooFALSE terwijl uw gebruikers voorbereiding zijn en kunnen niet allemaal worden ingeschreven voor Azure MFA nog. Aangezien Hallo instellingssleutel kan gebruikers die niet zijn geregistreerd voor MFA toosign in, moet u deze sleutel voordat tooproduction gaat verwijderen.

## <a name="troubleshooting"></a>Problemen oplossen

### <a name="how-do-i-verify-that-hello-client-cert-is-installed-as-expected"></a>Hoe kan ik controleren dat die cert Hallo-client is geïnstalleerd, zoals verwacht?

Zoek voor Hallo zelfondertekend certificaat gemaakt door installatieprogramma in Hallo-certificaatarchief en controleer of de persoonlijke sleutel Hallo Hallo machtigingen verleend toouser heeft **netwerkservice**. Hallo-certificaat heeft een onderwerpnaam van **CN \<tenantid\>, OU = Microsoft NPS-uitbreiding**

-------------------------------------------------------------

### <a name="how-can-i-verify-that-my-client-cert-is-associated-toomy-tenant-in-azure-active-directory"></a>Hoe kan ik dat mijn client-certificaat gekoppeld toomy tenant in Azure Active Directory is controleren?

Open PowerShell-opdrachtprompt en Voer Hallo volgende opdrachten:

```
import-module MSOnline
Connect-MsolService
Get-MsolServicePrincipalCredential -AppPrincipalId "981f26a1-7f43-403b-a875-f8b09b8cd720" -ReturnKeyValues 1 
```

Deze opdrachten afdrukken alle Hallo certificaten koppelen van uw tenant aan uw exemplaar van Hallo NPS-uitbreiding in uw PowerShell-sessie. Zoek uw certificaat door uw client-certificaat exporteren als een 'Base 64-gecodeerd X.509(.cer)'-bestand zonder persoonlijke sleutel Hallo en vergelijken met het Hallo-lijst van PowerShell.

Geldige-van en geldig-totdat tijdstempels die leesbare vorm, gebruikte toofilter uit voor de hand liggende misfits zijn kan als Hallo opdracht meer dan één certificaat retourneert.

-------------------------------------------------------------

### <a name="why-are-my-requests-failing-with-adal-token-error"></a>Waarom wordt mijn aanvragen waarbij ADAL-token optreedt?

Deze fout kan worden veroorzaakt door tooone van verschillende redenen. Volg deze stappen toohelp oplossen:

1. De NPS-server opnieuw.
2. Controleer of dat die cert client is geïnstalleerd, zoals verwacht.
3. Controleer of dat Hallo-certificaat is gekoppeld aan uw tenant op Azure AD.
4. Controleer of dat deze https://login.microsoftonline.com/ is toegankelijk vanuit Hallo server Hallo-extensie uitgevoerd.

-------------------------------------------------------------

### <a name="why-does-authentication-fail-with-an-error-in-http-logs-stating-that-hello-user-is-not-found"></a>Waarom faalt verificatie met een fout in HTTP-logboeken met de mededeling dat Hallo-gebruiker is niet gevonden

Verifieer dat AD Connect wordt uitgevoerd en die gebruiker Hallo aanwezig in zowel Windows Active Directory en Azure Active Directory is.

------------------------------------------------------------

### <a name="why-do-i-see-http-connect-errors-in-logs-with-all-my-authentications-failing"></a>Waarom zie ik HTTP-fouten in Logboeken verbinden met alle mijn verificaties mislukt?

Controleer of deze https://adnotifications.windowsazure.com bereikbaar is vanaf Hallo server Hallo NPS extensie uitgevoerd.


## <a name="next-steps"></a>Volgende stappen

- Alternatieve-id's voor aanmelding configureren of stelt u een lijst met uitzonderingen voor IP-adressen die verificatie in twee stappen in mag niet uitvoeren [geavanceerde configuratieopties voor Hallo NPS-extensie voor multi-factor Authentication](nps-extension-advanced-configuration.md)

- [Foutberichten van Hallo NPS-extensie voor Azure multi-factor Authentication oplossen](multi-factor-authentication-nps-errors.md)
