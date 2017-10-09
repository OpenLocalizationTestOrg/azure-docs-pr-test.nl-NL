---
title: aaaTroubleshoot Wachtwoordsynchronisatie met Azure AD Connect-synchronisatie | Microsoft Docs
description: In dit artikel bevat informatie over het tootroubleshoot wachtwoord synchronisatieproblemen.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 390eafec792cb39251627c14cb754f8bb30035b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a>Wachtwoordsynchronisatie met Azure AD Connect-synchronisatie oplossen
In dit onderwerp bevat stappen voor hoe tootroubleshoot met synchronisatie van wachtwoorden problemen. Als wachtwoorden zijn niet zoals verwacht wordt gesynchroniseerd, kan het zijn voor een subset van gebruikers of voor alle gebruikers. Voor Azure Active Directory (Azure AD) implementatie verbinden met versie 1.1.524.0 of hoger, er is nu een diagnostische cmdlet waarmee u tootroubleshoot wachtwoord synchronisatieproblemen kunt:

* Als er een probleem waarbij geen wachtwoorden worden gesynchroniseerd, raadpleegt u toohello [geen wachtwoorden worden gesynchroniseerd: problemen oplossen met behulp van de diagnostische cmdlet Hallo](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) sectie.

* Als u een probleem met de afzonderlijke objecten hebt, raadpleegt u toohello [één object worden wachtwoorden niet gesynchroniseerd: problemen oplossen met behulp van de diagnostische cmdlet Hallo](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) sectie.

Voor oudere versies van Azure AD Connect-implementatie:

* Als er een probleem waarbij geen wachtwoorden worden gesynchroniseerd, raadpleegt u toohello [geen wachtwoorden worden gesynchroniseerd: handmatige stappen voor probleemoplossing](#no-passwords-are-synchronized-manual-troubleshooting-steps) sectie.

* Als u een probleem met de afzonderlijke objecten hebt, raadpleegt u toohello [één object worden wachtwoorden niet gesynchroniseerd: handmatige stappen voor probleemoplossing](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) sectie.

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-hello-diagnostic-cmdlet"></a>Er is geen wachtwoorden worden gesynchroniseerd: problemen oplossen met behulp van de diagnostische cmdlet Hallo
U kunt Hallo `Invoke-ADSyncDiagnostics` cmdlet toofigure uit waarom geen wachtwoorden worden gesynchroniseerd.

> [!NOTE]
> Hallo `Invoke-ADSyncDiagnostics` cmdlet is alleen beschikbaar voor Azure AD Connect versie 1.1.524.0 of hoger.

### <a name="run-hello-diagnostics-cmdlet"></a>Hallo diagnostics cmdlet uitvoeren
tootroubleshoot problemen waar geen wachtwoorden worden gesynchroniseerd:

1. Open een nieuw Windows PowerShell-sessie op de server van uw Azure AD Connect met Hallo **als Administrator uitvoeren** optie.

2. Voer `Set-ExecutionPolicy RemoteSigned` of `Set-ExecutionPolicy Unrestricted`.

3. Voer `Import-Module ADSyncDiagnostics` uit.

4. Voer `Invoke-ADSyncDiagnostics -PasswordSync` uit.

### <a name="understand-hello-results-of-hello-cmdlet"></a>Resultaten van de cmdlet Hallo Hallo begrijpen
Hallo diagnostische cmdlet voert controles Hallo:

* Valideert dat Hallo wachtwoordfunctie voor synchronisatie is ingeschakeld voor uw Azure AD-tenant.

* Valideert dat hello Azure AD Connect server niet in de faseringsmodus is.

* Voor elk bestaand on-premises Active Directory-connector (die overeenkomt met de bestaande Active Directory-forest tooan):

   * Valideert dat Hallo wachtwoordfunctie voor synchronisatie is ingeschakeld.
   
   * Hiermee zoekt u wachtwoord synchronisatie heartbeat gebeurtenissen in Hallo Windows toepassing gebeurtenislogboeken.

   * Voor elk Active Directory-domein onder Hallo lokale Active Directory-connector:

      * Valideert dat Hallo domein kan worden bereikt vanaf hello Azure AD Connect-server.

      * Valideert dat Hallo Active Directory Domain Services (AD DS)-accounts die worden gebruikt door Hallo lokale Active Directory-connector heeft Hallo juiste gebruikersnaam, wachtwoord en machtigingen die vereist zijn voor Wachtwoordsynchronisatie.

Hallo volgende diagram illustreert Hallo resultaten van het Hallo-cmdlet voor een lokale Active Directory-topologie van één domein:

![Diagnostische uitvoer voor Wachtwoordsynchronisatie](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

Hallo rest van deze sectie beschrijft specifieke resultaten die zijn geretourneerd door de cmdlet Hallo en bijbehorende problemen.

#### <a name="password-synchronization-feature-isnt-enabled"></a>De synchronisatiefunctie wachtwoord is niet ingeschakeld
Als u dit nog niet hebt Wachtwoordsynchronisatie met behulp van hello Azure AD Connect-wizard ingeschakeld, wordt de Hallo volgende fout geretourneerd:

![Wachtwoordsynchronisatie is niet ingeschakeld](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a>Azure AD Connect-server is in de faseringsmodus
Wachtwoordsynchronisatie is tijdelijk uitgeschakeld als hello Azure AD Connect-server in de faseringsmodus is, en hello volgende fout is geretourneerd:

![Azure AD Connect-server is in de faseringsmodus](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a>Er zijn geen wachtwoord synchronisatie heartbeat-gebeurtenissen
Elke lokale Active Directory-connector heeft een eigen synchronisatiekanaal wachtwoord. Wanneer Hallo wachtwoord synchronisatiekanaal tot stand is gebracht en er wachtwoord wijzigingen toobe gesynchroniseerd zijn, wordt elke 30 minuten onder Hallo Windows-toepassingslogboek gegenereerd in een heartbeat-gebeurtenis (EventId 654). Voor elke lokale Active Directory-connector Hallo cmdlet wordt gezocht naar overeenkomende heartbeat-gebeurtenissen in Hallo afgelopen drie uur. Als er geen heartbeat-gebeurtenis wordt gevonden, hello volgende fout is geretourneerd:

![Er is geen wachtwoord synchronisatie hartslag gebeurtenis](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a>AD DS-account heeft geen juiste machtigingen
Als Hallo AD DS-account dat wordt gebruikt door Hallo on-premises Active Directory-connector toosynchronize wachtwoord-hashes heeft geen juiste machtigingen Hallo is Hallo volgende fout geretourneerd:

![Onjuiste referenties](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a>Onjuiste gebruikersnaam van de AD DS-account of wachtwoord
Als hello AD DS-account gebruikt door hello lokale Active Directory-connector toosynchronize wachtwoord-hashes heeft een onjuiste gebruikersnaam of wachtwoord, hello volgende fout is geretourneerd:

![Onjuiste referenties](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-hello-diagnostic-cmdlet"></a>Wachtwoorden niet kan één object worden gesynchroniseerd: problemen oplossen met behulp van de diagnostische cmdlet Hallo
U kunt Hallo `Invoke-ADSyncDiagnostics` cmdlet toodetermine waarom één object wachtwoorden niet wordt gesynchroniseerd.

> [!NOTE]
> Hallo `Invoke-ADSyncDiagnostics` cmdlet is alleen beschikbaar voor Azure AD Connect versie 1.1.524.0 of hoger.

### <a name="run-hello-diagnostics-cmdlet"></a>Hallo diagnostics cmdlet uitvoeren
tootroubleshoot problemen waar geen wachtwoorden worden gesynchroniseerd:

1. Open een nieuw Windows PowerShell-sessie op de server van uw Azure AD Connect met Hallo **als Administrator uitvoeren** optie.

2. Voer `Set-ExecutionPolicy RemoteSigned` of `Set-ExecutionPolicy Unrestricted`.

3. Voer `Import-Module ADSyncDiagnostics` uit.

4. Voer Hallo volgende cmdlet:
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   Bijvoorbeeld:
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-hello-results-of-hello-cmdlet"></a>Resultaten van de cmdlet Hallo Hallo begrijpen
Hallo diagnostische cmdlet voert controles Hallo:

* Hallo-status van Active Directory-object in de adresruimte van Hallo Active Directory-connector, Metaverse en Azure Hallo onderzoekt AD connectorgebied overgebracht.

* Controleert of er synchronisatieregels Wachtwoordsynchronisatie is ingeschakeld en toohello Active Directory-object worden toegepast.

* Pogingen tooretrieve en weergave Hallo resultaten van Hallo laatste poging toosynchronize Hallo wachtwoord voor Hallo-object.

Hallo volgende diagram illustreert Hallo resultaten van de cmdlet Hallo wanneer u problemen met Wachtwoordsynchronisatie voor één object:

![Diagnostische uitvoer voor Wachtwoordsynchronisatie - enkel object](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

Hallo rest van deze sectie beschrijft specifieke resultaten geretourneerd door de cmdlet Hallo en bijbehorende problemen.

#### <a name="hello-active-directory-object-isnt-exported-tooazure-ad"></a>Hallo Active Directory-object is niet de geëxporteerde tooAzure AD
Wachtwoordsynchronisatie voor deze lokale Active Directory-account is mislukt omdat er geen bijbehorende object in hello Azure AD-tenant. Hallo volgende fout is geretourneerd:

![Azure AD-object ontbreekt.](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a>Gebruiker heeft een tijdelijk wachtwoord
Azure AD Connect ondersteunt momenteel geen tijdelijke wachtwoorden synchroniseren met Azure AD. Een wachtwoord wordt beschouwd als toobe tijdelijke als hello **wachtwoord bij volgende aanmelding wijzigen** optie is ingesteld op Hallo on-premises Active Directory-gebruiker. Hallo volgende fout is geretourneerd:

![Tijdelijke wachtwoord wordt niet geëxporteerd.](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-toosynchronize-password-arent-available"></a>Resultaten van de laatste poging toosynchronize wachtwoord niet beschikbaar
Azure AD Connect slaat standaard Hallo resultaten van synchronisatiepogingen van wachtwoord voor de zeven dagen. Als er geen resultaten beschikbaar voor Active Directory-object Hallo geselecteerd zijn, wordt Hallo volgende waarschuwing geretourneerd:

![Diagnostische uitvoer voor één object - geen wachtwoordgeschiedenis voor synchronisatie](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a>Er is geen wachtwoorden worden gesynchroniseerd: handmatige stappen voor probleemoplossing
Volg deze stappen toodetermine waarom geen wachtwoorden worden gesynchroniseerd:

1. Hallo-Connect-server in [faseringsmodus](active-directory-aadconnectsync-operations.md#staging-mode)? Een server in de faseringsmodus wachtwoorden niet wordt gesynchroniseerd.

2. Hallo-script uitvoeren in Hallo [Hallo status van wachtwoord synchronisatie-instellingen ophalen](#get-the-status-of-password-sync-settings) sectie. Dit biedt u een overzicht van de configuratie van Hallo wachtwoord synchronisatie.  

    ![PowerShell-scriptuitvoer van de synchronisatie-instellingen voor wachtwoord](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. Hallo Connect-installatiewizard als Hallo-functie niet is ingeschakeld in Azure AD of als het Hallo-synchronisatiestatus kanaal niet is ingeschakeld, worden uitgevoerd. Selecteer **aanpassen Synchronisatieopties**, en Wachtwoordsynchronisatie te deselecteren. Deze wijziging worden Hallo functie tijdelijk uitgeschakeld. Vervolgens voert u de wizard Hallo opnieuw en Wachtwoordsynchronisatie opnieuw in te schakelen. Hallo-script uitvoeren opnieuw tooverify die Hallo configuratie juist is.

4. Kijk in het Hallo-gebeurtenislogboek op fouten. Zoek naar Hallo gebeurtenissen die op een probleem duiden op te volgen:
    * Bron: 'Adreslijstsynchronisatie' ID: 0, 611, 652, 655 als u deze gebeurtenissen, ziet u hebt een verbindingsprobleem. Hallo-bericht van gebeurtenislogboek beschreven forest waar u problemen ondervindt. Zie voor meer informatie [verbindingsprobleem](#connectivity problem).

5. Als er geen heartbeat of niets anders gewerkt, uitvoeren [activeren van een volledige synchronisatie van wachtwoorden voor alle](#trigger-a-full-sync-of-all-passwords). Hallo script slechts eenmaal worden uitgevoerd.

6. Zie Hallo [oplossen van één object dat wachtwoorden niet synchroniseert](#one-object-is-not-synchronizing-passwords) sectie.

### <a name="connectivity-problems"></a>Verbindingsproblemen

Hebt u verbinding met Azure AD?

Hallo-account vereist machtigingen tooread Hallo wachtwoord-hashes in alle domeinen? Als u verbinding maken met behulp van snelle instellingen hebt geïnstalleerd, kunnen Hallo machtigingen moeten al zijn juist. 

Als u aangepaste installatie gebruikt, Hallo machtigingen handmatig instellen door Hallo volgende te doen:
    
1. toofind hello account dat wordt gebruikt door Hallo Active Directory-connector start **Synchronization Service Manager**. 
 
2. Ga te**Connectors**, en zoek vervolgens naar Hallo lokale Active Directory-forest die u wilt oplossen. 
 
3. Selecteer Hallo-connector en klik vervolgens op **eigenschappen**. 
 
4. Ga te**tooActive Directory-Forest verbinding**.  
    
    ![Account dat wordt gebruikt door Active Directory-connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    Houd er rekening mee Hallo gebruikersnaam en het Hallo-domein waar Hallo account zich bevindt.
    
5. Start **Active Directory: gebruikers en Computers**, en controleer vervolgens of Hallo-account die u eerder hebt gevonden Hallo Volg machtigingen zijn ingesteld in de hoofdmap Hallo van alle domeinen in uw forest heeft:
    * Directorywijzigingen repliceren
    * Alle repliceren Directory gewijzigd

6. Hallo-domeincontrollers kunnen worden bereikt door Azure AD Connect zijn? Als het Hallo-Connect-server kan geen verbinding met het maken van domeincontrollers tooall, configureert u **voorkeur domeincontroller alleen gebruiken**.  
    
    ![-Domeincontroller die wordt gebruikt door Active Directory-connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. Ga terug te**Synchronization Service Manager** en **mappartitie configureren**. 
 
8. Selecteer uw domein in **mappartities selecteren**, selecteer Hallo **alleen gebruiken voorkeur domeincontrollers** selectievakje en klik vervolgens op **configureren**. 

9. Voer in lijst Hallo Hallo-domeincontrollers die verbinding voor Wachtwoordsynchronisatie gebruiken moet. Hallo dezelfde lijst wordt gebruikt voor het importeren en exporteren ook. Voer deze stappen uit voor alle domeinen.

10. Als Hallo script wordt aangegeven dat er geen heartbeat, Hallo-script uitvoeren [activeren van een volledige synchronisatie van wachtwoorden voor alle](#trigger-a-full-sync-of-all-passwords).

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a>Wachtwoorden niet kan één object worden gesynchroniseerd: handmatige stappen voor probleemoplossing
U kunt eenvoudig wachtwoord synchronisatieproblemen aan de hand van de status van een object Hallo oplossen.

1. In **Active Directory: gebruikers en Computers**, zoeken naar Hallo gebruiker en controleer vervolgens dat Hallo **gebruiker moet wachtwoord bij volgende aanmelding wijzigen** selectievakje is uitgeschakeld.  

    ![Active Directory-productief wachtwoorden](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    Hallo selectievakje is ingeschakeld, vraagt u Hallo gebruiker toosign in als Hallo wachtwoord wijzigen. Tijdelijke wachtwoorden zijn niet gesynchroniseerd met Azure AD.

2. Hallo wachtwoord ziet er juist in Active Directory, volg Hallo-gebruiker in Hallo synchronisatie-engine. Volgende Hallo gebruiker van de lokale Active Directory tooAzure AD, kunt u zien of er een beschrijvend foutbericht op Hallo-object is.

    a. Hallo Start [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).

    b. Klik op **Connectors**.

    c. Selecteer Hallo **Active Directory-Connector** waar Hallo gebruiker zich bevindt.

    d. Selecteer **Connectorgebied zoeken**.

    e. In Hallo **bereik** de optie **DN-naam of het anker**, en voer de volledige DN Hallo van Hallo-gebruiker die u wilt oplossen.

    ![Zoeken naar de gebruiker in de connectorruimte met de DN-naam](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    f. Hallo gebruiker die u zoekt, en klik vervolgens op Zoeken **eigenschappen** toosee alle kenmerken Hallo. Als het Hallo-gebruiker zich niet in de zoekresultaten hello, controleert u of uw [filterregels](active-directory-aadconnectsync-configure-filtering.md) en zorg ervoor dat u uitvoert [toepassen en controleer of de wijzigingen](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) voor Hallo gebruiker tooappear in verbinding maken.

    g. Klik op toosee Hallo wachtwoord sync details van Hallo-object voor Hallo afgelopen week **logboek**.  

    ![Object-logboekgegevens](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    Als Hallo object logboek leeg is, is Azure AD Connect kan niet tooread Hallo wachtwoord-hash van Active Directory. Gaat u uw verder met [Connectiviteitsfouten](#connectivity-errors). Als er een andere waarde dan **geslaagd**, raadpleegt u de tabel toohello in [wachtwoord sync logboek](#password-sync-log).

    h. Selecteer Hallo **afkomst** tabblad en zorg ervoor dat ten minste één synchronisatieregel in Hallo **PasswordSync** kolom is **True**. In de standaardconfiguratie Hallo Hallo-naam van de synchronisatieregel Hallo is **In uit Active Directory - gebruiker AccountEnabled**.  

    ![Informatie over een gebruiker Lineage](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    ik. Klik op **eigenschappen Metaverse-Object** toodisplay een lijst met gebruikerskenmerken.  

    ![Metaverse-informatie](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    Controleer of er geen **cloudFiltered** kenmerk aanwezig. Zorg ervoor dat Hallo Domeinkenmerken (domainFQDN en domainNetBios) Hallo verwachte waarden hebben.

    j. Klik op Hallo **Connectors** tabblad. Zorg ervoor dat u connectors tooboth ziet op lokale Active Directory en Azure AD.

    ![Metaverse-informatie](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    k. Selecteer Hallo rij voor Azure AD, klikt u op **eigenschappen**, en klik vervolgens op Hallo **afkomst** tabblad Hallo connector space-object moet een uitgaande regel in Hallo **PasswordSync** kolomset te**True**. In de standaardconfiguratie Hallo Hallo-naam van de synchronisatieregel Hallo is **uit tooAAD - gebruiker toevoegen**.  

    ![Dialoogvenster voor eigenschappen van het Object ruimte connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a>Wachtwoord sync-logboek
de kolom status Hallo kan Hallo volgende waarden hebben:

| Status | Beschrijving |
| --- | --- |
| Geslaagd |Wachtwoord is gesynchroniseerd. |
| FilteredByTarget |Wachtwoord wordt ingesteld, te**gebruiker moet wachtwoord bij volgende aanmelding wijzigen**. Wachtwoord is niet gesynchroniseerd. |
| NoTargetConnection |Er is geen object in Hallo metaverse of in de ruimte van hello Azure AD-connector. |
| SourceConnectorNotPresent |Er is geen object gevonden in Hallo lokale Active Directory-connectorruimte. |
| TargetNotExportedToDirectory |Hallo-object in hello Azure AD-connectorruimte is nog niet geëxporteerd. |
| MigratedCheckDetailsForMoreInfo |Logboekvermelding is gemaakt voordat de build 1.0.9125.0 en wordt weergegeven in de oude status. |
| Fout |Service heeft een onbekende fout geretourneerd. |
| Onbekend |Er is een fout opgetreden tijdens een poging tooprocess een batch wachtwoord-hashes.  |
| MissingAttribute |Specifieke kenmerken die vereist zijn door Azure AD Domain Services (bijvoorbeeld, Kerberos-hash) zijn niet beschikbaar. |
| RetryRequestedByTarget |Specifieke kenmerken die vereist zijn door Azure AD Domain Services (bijvoorbeeld, Kerberos-hash) was eerder niet beschikbaar. Een poging tooresynchronize Hallo gebruiker wachtwoord-hash wordt gemaakt. |

## <a name="scripts-toohelp-troubleshooting"></a>Scripts toohelp probleemoplossing

### <a name="get-hello-status-of-password-sync-settings"></a>Hallo-status van wachtwoord synchronisatie-instellingen ophalen
```
Import-Module ADSync
$connectors = Get-ADSyncConnector
$aadConnectors = $connectors | Where-Object {$_.SubType -eq "Windows Azure Active Directory (Microsoft)"}
$adConnectors = $connectors | Where-Object {$_.ConnectorTypeName -eq "AD"}
if ($aadConnectors -ne $null -and $adConnectors -ne $null)
{
    if ($aadConnectors.Count -eq 1)
    {
        $features = Get-ADSyncAADCompanyFeature -ConnectorName $aadConnectors[0].Name
        Write-Host
        Write-Host "Password sync feature enabled in your Azure AD directory: "  $features.PasswordHashSync
        foreach ($adConnector in $adConnectors)
        {
            Write-Host
            Write-Host "Password sync channel status BEGIN ------------------------------------------------------- "
            Write-Host
            Get-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector.Name
            Write-Host
            $pingEvents =
                Get-EventLog -LogName "Application" -Source "Directory Synchronization" -InstanceId 654  -After (Get-Date).AddHours(-3) |
                    Where-Object { $_.Message.ToUpperInvariant().Contains($adConnector.Identifier.ToString("D").ToUpperInvariant()) } |
                    Sort-Object { $_.Time } -Descending
            if ($pingEvents -ne $null)
            {
                Write-Host "Latest heart beat event (within last 3 hours). Time " $pingEvents[0].TimeWritten
            }
            else
            {
                Write-Warning "No ping event found within last 3 hours."
            }
            Write-Host
            Write-Host "Password sync channel status END ------------------------------------------------------- "
            Write-Host
        }
    }
    else
    {
        Write-Warning "More than one Azure AD Connectors found. Please update hello script toouse hello appropriate Connector."
    }
}
Write-Host
if ($aadConnectors -eq $null)
{
    Write-Warning "No Azure AD Connector was found."
}
if ($adConnectors -eq $null)
{
    Write-Warning "No AD DS Connector was found."
}
Write-Host
```

#### <a name="trigger-a-full-sync-of-all-passwords"></a>Activeren van een volledige synchronisatie van alle wachtwoorden
> [!NOTE]
> Dit script wordt slechts één keer uitgevoerd. Als u toorun deze meer dan één keer moet, is iets anders Hallo probleem. tootroubleshoot hello probleem contact op met Microsoft ondersteuning.

U kunt een volledige synchronisatie van alle wachtwoorden activeren met behulp van Hallo script volgen:

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"
$aadConnector = "<CASE SENSITIVE AAD CONNECTOR NAME>"
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

## <a name="next-steps"></a>Volgende stappen
* [Wachtwoordsynchronisatie met Azure AD Connect-synchronisatie implementeren](active-directory-aadconnectsync-implement-password-synchronization.md)
* [Azure AD Connect-synchronisatie: Synchronisatie-opties voor aanpassen](active-directory-aadconnectsync-whatis.md)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
