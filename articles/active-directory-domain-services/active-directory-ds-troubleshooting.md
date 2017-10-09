---
title: 'Azure Active Directory Domain Services: Troubleshooting Guide | Microsoft Docs'
description: Gids voor probleemoplossing voor Azure AD Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 4bc8c604-f57c-4f28-9dac-8b9164a0cf0b
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 86eb3513b7bc921c59287600b1b76eeda20c1356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services---troubleshooting-guide"></a>Azure AD Domain Services - probleemoplossingsgids
Dit artikel bevat tips voor probleemoplossing voor problemen die optreden kunnen bij het instellen of het beheer van Azure Active Directory (AD) Domain Services.

## <a name="you-cannot-enable-azure-ad-domain-services-for-your-azure-ad-directory"></a>U kunt Azure AD Domain Services voor uw Azure AD-directory niet inschakelen
Dit gedeelte kunt u fouten oplossen wanneer u tooenable Azure AD Domain Services voor uw directory probeert en deze mislukt opgehaald of ingesteld uitgeschakeld back too'Disabled'.

Kies Hallo stappen die overeenkomen met het foutbericht toohello die u tegenkomt voor probleemoplossing.

| **Foutbericht** | **Naamomzetting** |
| --- |:--- |
| *Hallo naam contoso100.com is al in gebruik is op dit netwerk. Geef een naam op die niet in gebruik is.* |[Naamconflict domein in het virtuele netwerk Hallo](active-directory-ds-troubleshooting.md#domain-name-conflict) |
| *Domain Services kunnen niet worden ingeschakeld in deze Azure AD-tenant. Hallo-service beschikt niet over voldoende machtigingen toohello toepassing met de naam 'Azure AD Domain Services Sync'. Hallo toepassing met de naam 'Azure AD Domain Services Sync' verwijderen en probeer vervolgens tooenable Domain Services voor uw Azure AD-tenant.* |[Domain Services beschikt niet over voldoende machtigingen toohello synchroniseren van Azure AD Domain Services-toepassing](active-directory-ds-troubleshooting.md#inadequate-permissions) |
| *Domain Services kunnen niet worden ingeschakeld in deze Azure AD-tenant. Hallo Domain Services-toepassing in uw Azure AD-tenant niet hebben Hallo vereist machtigingen tooenable Domain Services. Hallo-toepassing met Hallo toepassing id d87dcbc6-a371-462e-88e3-28ad15ec4e64 verwijderen en probeer vervolgens tooenable Domain Services voor uw Azure AD-tenant.* |[Hallo Domain Services-toepassing is niet juist geconfigureerd in uw tenant](active-directory-ds-troubleshooting.md#invalid-configuration) |
| *Domain Services kunnen niet worden ingeschakeld in deze Azure AD-tenant. Microsoft Azure AD-toepassing Hello is uitgeschakeld in uw Azure AD-tenant. Hallo-toepassing met Hallo toepassing id 00000002-0000-0000-c000-000000000000 inschakelen en probeer het vervolgens tooenable Domain Services voor uw Azure AD-tenant.* |[Hallo Microsoft Graph-toepassing is uitgeschakeld in uw Azure AD-tenant](active-directory-ds-troubleshooting.md#microsoft-graph-disabled) |

### <a name="domain-name-conflict"></a>Conflicten met domein
**Foutbericht:**

*Hallo naam contoso100.com is al in gebruik is op dit netwerk. Geef een naam op die niet in gebruik is.*

**Herstel:**

Zorg ervoor dat u geen een bestaand domein met Hallo hebt dezelfde domeinnaam beschikbaar is op dit virtuele netwerk. Bijvoorbeeld, wordt ervan uitgegaan hebben van een domein genaamd 'contoso.com' al beschikbaar op Hallo van de geselecteerde virtuele netwerk. Later kunt u een beheerd domein van Azure AD Domain Services met Hallo tooenable probeert dezelfde domeinnaam (dat wil zeggen, ' contoso.com') op dit virtuele netwerk. Er optreedt een fout bij een poging tooenable Azure AD Domain Services.

Deze fout is vanwege conflicten tooname voor Hallo-domeinnaam op dit virtuele netwerk. In dit geval moet u een andere naam tooset van uw Azure AD Domain Services beheerd domein. U kunt ook ongedaan inrichten Hallo bestaand domein en vervolgens doorgaan tooenable Azure AD Domain Services.

### <a name="inadequate-permissions"></a>Onvoldoende machtigingen
**Foutbericht:**

*Domain Services kunnen niet worden ingeschakeld in deze Azure AD-tenant. Hallo-service beschikt niet over voldoende machtigingen toohello toepassing met de naam 'Azure AD Domain Services Sync'. Hallo toepassing met de naam 'Azure AD Domain Services Sync' verwijderen en probeer vervolgens tooenable Domain Services voor uw Azure AD-tenant.*

**Herstel:**

Controleer toosee als er een toepassing met Hallo-naam 'Azure AD Domain Services Sync' in uw Azure AD-directory. Als deze toepassing bestaat, verwijderen en Azure AD Domain Services opnieuw inschakelen.

Voer Hallo volgende stappen toocheck op Hallo aanwezigheid van de toepassing hello en toodelete, als de toepassing hello bestaat:

1. Navigeer toohello **klassieke Azure-portal** ([https://manage.windowsazure.com](https://manage.windowsazure.com)).
2. Selecteer Hallo **Active Directory** knooppunt in het linkerdeelvenster Hallo.
3. Selecteer hello Azure AD-tenant (directory) waarvoor u tooenable wilt dat Azure AD Domain Services.
4. Navigeer toohello **toepassingen** tabblad.
5. Selecteer Hallo **toepassingen mijn bedrijf eigenaar is van** optie Hallo vervolgkeuzelijst.
6. Controleer voor een toepassing met de naam **Azure AD Domain Services Sync**. Als de toepassing hello bestaat, gaat u verder toodelete deze.
7. Zodra u de toepassing hello hebt verwijderd, probeer het nogmaals tooenable Azure AD Domain Services.

### <a name="invalid-configuration"></a>Ongeldige configuratie
**Foutbericht:**

*Domain Services kunnen niet worden ingeschakeld in deze Azure AD-tenant. Hallo Domain Services-toepassing in uw Azure AD-tenant niet hebben Hallo vereist machtigingen tooenable Domain Services. Hallo-toepassing met Hallo toepassing id d87dcbc6-a371-462e-88e3-28ad15ec4e64 verwijderen en probeer vervolgens tooenable Domain Services voor uw Azure AD-tenant.*

**Herstel:**

Controleer de toosee als u een toepassing met de naam van de Hallo 'AzureActiveDirectoryDomainControllerServices' (met een toepassings-id van d87dcbc6-a371-462e-88e3-28ad15ec4e64) in uw Azure AD-directory hebt. Als deze toepassing bestaat, moet u toodelete deze en klikt u vervolgens opnieuw in te schakelen Azure AD Domain Services.

Gebruik van de volgende PowerShell-script toofind Hallo toepassing hello en verwijder deze.

> [!NOTE]
> Dit script gebruikt **Azure AD PowerShell versie 2** cmdlets. Lees voor een volledige lijst met alle beschikbare cmdlets en toodownload Hallo module Hallo [AzureAD PowerShell naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt757189.aspx).
>
>

```
$InformationPreference = "Continue"
$WarningPreference = "Continue"

$aadDsSp = Get-AzureADServicePrincipal -Filter "AppId eq 'd87dcbc6-a371-462e-88e3-28ad15ec4e64'" -ErrorAction Ignore
if ($aadDsSp -ne $null)
{
    Write-Information "Found Azure AD Domain Services application. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $aadDsSp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services application."
}

$identifierUri = "https://sync.aaddc.activedirectory.windowsazure.com"
$appFilter = "IdentifierUris eq '" + $identifierUri + "'"
$app = Get-AzureADApplication -Filter $appFilter
if ($app -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync application. Deleting it ..."
    Remove-AzureADApplication -ObjectId $app.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync application."
}

$spFilter = "ServicePrincipalNames eq '" + $identifierUri + "'"
$sp = Get-AzureADServicePrincipal -Filter $spFilter
if ($sp -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync service principal. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $sp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync service principal."
}
```
<br>

### <a name="microsoft-graph-disabled"></a>Microsoft Graph uitgeschakeld
**Foutbericht:**

Domain Services kunnen niet worden ingeschakeld in deze Azure AD-tenant. Microsoft Azure AD-toepassing Hello is uitgeschakeld in uw Azure AD-tenant. Hallo-toepassing met Hallo toepassing id 00000002-0000-0000-c000-000000000000 inschakelen en probeer het vervolgens tooenable Domain Services voor uw Azure AD-tenant.

**Herstel:**

Controleer de toosee als u een toepassing met Hallo id 00000002-0000-0000-c000-000000000000 hebt uitgeschakeld. Deze toepassing is Microsoft Azure AD-toepassing hello en biedt Graph API toegang tooyour Azure AD-tenant. Azure AD Domain Services moet u deze toepassing toobe ingeschakeld toosynchronize uw Azure AD-tenant tooyour beheerd domein.

tooresolve deze fout inschakelen van deze toepassing en probeer het vervolgens tooenable Domain Services voor uw Azure AD-tenant.

## <a name="users-are-unable-toosign-in-toohello-azure-ad-domain-services-managed-domain"></a>Gebruikers kunnen zich toosign in toohello beheerd domein van Azure AD Domain Services
Als een of meer gebruikers in uw Azure AD-tenant niet kan toosign in het beheerde domein toohello nieuw gemaakt, voert u Hallo volgende stappen uit:

* **Meld u aan met de UPN-indeling:** probeer toosign in Hallo UPN-indeling (bijvoorbeeld 'joeuser@contoso.com') in plaats van Hallo SAMAccountName-indeling (CONTOSO\joeuser). Hallo SAMAccountName kan automatisch worden gegenereerd voor gebruikers wiens UPN-voorvoegsel is te lang of is dezelfde als een andere gebruiker op het beheerde domein Hallo Hallo. Hallo UPN-indeling kan worden gegarandeerd toobe uniek zijn binnen een Azure AD-tenant.

> [!NOTE]
> U kunt het beste Hallo UPN-indeling toosign in toohello Azure AD Domain Services beheerd domein gebruikt.
>
>

* Zorg ervoor dat er [ingeschakeld Wachtwoordsynchronisatie](active-directory-ds-getting-started-password-sync.md) in overeenstemming met Hallo stappen in Hallo handleiding aan de slag.
* **Externe accounts:** Controleer Hallo van invloed op een gebruikersaccount is niet een externe account in hello Azure AD-tenant. Voorbeelden van externe accounts zijn Microsoft-accounts (bijvoorbeeld 'joe@live.com') of gebruikersaccounts uit een extern Azure AD-directory. Omdat Azure AD Domain Services heeft geen referenties voor dergelijke gebruikersaccounts, kunnen deze gebruikers toohello beheerd domein aanmelden.
* **Accounts die gesynchroniseerd:** als Hallo van invloed op gebruikersaccounts worden gesynchroniseerd vanuit een on-premises adreslijst, controleert u of die:

  * U hebt geïmplementeerd of bijgewerkt toohello [meest recente versie van Azure AD Connect aanbevolen](https://www.microsoft.com/en-us/download/details.aspx?id=47594).
  * U hebt Azure AD Connect te geconfigureerd[een volledige synchronisatie uitvoeren](active-directory-ds-getting-started-password-sync.md).
  * Afhankelijk van de grootte van de Hallo van uw directory, kan het even duren voor gebruikersaccounts en referentie-hashes toobe beschikbaar zijn in Azure AD Domain Services. Zorg ervoor dat u lang genoeg voordat u verificatie (afhankelijk van de grootte van de Hallo van uw directory - enkele uren tooa dag of twee bij grote mappen) wachten.
  * Als Hallo probleem zich blijft voordoen nadat u hebt gecontroleerd Hallo vorige stappen, probeert u het Hallo Microsoft Azure AD Sync-Service opnieuw te starten. Op uw machine synchronisatie starten vanaf de opdrachtprompt en Voer Hallo volgende opdrachten:

    1. net stop 'Microsoft Azure AD Sync'
    2. net start 'Microsoft Azure AD Sync'
* **Alleen in de cloud accounts**: als Hallo van invloed op een gebruikersaccount een alleen-gebruikersaccount is, zorg er dan van die gebruiker Hallo hun wachtwoord is gewijzigd nadat u Azure AD Domain Services hebt ingeschakeld. Deze stap zorgt ervoor dat Hallo referentie-hashes voor Azure AD Domain Services toobe gegenereerd.

## <a name="users-removed-from-your-azure-ad-tenant-are-not-removed-from-your-managed-domain"></a>Gebruikers van uw Azure AD-tenant is verwijderd, worden niet verwijderd van uw beheerde domein
Azure AD voorkomt dat u onbedoeld gebruikersobjecten verwijdert. Wanneer u een gebruikersaccount van uw Azure AD-tenant verwijdert, is de bijbehorende gebruikersobject Hallo verplaatste toohello Prullenbak. Wanneer u deze bewerking is gesynchroniseerde tooyour beheerd domein, wordt veroorzaakt Hallo overeenkomende gebruiker account toobe gemarkeerd als uitgeschakeld. Deze functie kunt u herstellen of later Hallo gebruikersaccount verwijderen ongedaan maken.

Hallo gebruikersaccount Hallo blijft uitgeschakeld staat in uw beheerde domein, zelfs als u een gebruikersaccount met de opnieuw maken Hallo dezelfde UPN in uw Azure AD-directory. Hallo gebruikersaccount tooremove van uw beheerde domein, moet u tooforce verwijderen uit uw Azure AD-tenant.

tooremove Hallo-gebruikersaccount volledig uit uw beheerde domein, wordt de Hallo gebruiker permanent verwijderen uit uw Azure AD-tenant. Hallo verwijderen MsolUser PowerShell-cmdlet gebruiken met Hallo '-RemoveFromRecycleBin' optie, zoals beschreven in dit [MSDN-artikel](https://msdn.microsoft.com/library/azure/dn194132.aspx).

## <a name="contact-us"></a>Contact opnemen
Contact opnemen met hello Azure Active Directory Domain Services-productteam te[feedback delen of voor ondersteuning](active-directory-ds-contact-us.md).
