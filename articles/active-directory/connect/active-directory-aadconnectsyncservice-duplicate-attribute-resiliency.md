---
title: aaaIdentity synchronisatie en dubbel kenmerk tolerantie | Microsoft Docs
description: Nieuwe gedrag van hoe toohandle objecten met UPN- of ProxyAddress conflicten tijdens de directorysynchronisatie via Azure AD Connect.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 537a92b7-7a84-4c89-88b0-9bce0eacd931
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.openlocfilehash: e27dcbf9d71f83fa9566cae2fd99350297d1cd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="identity-synchronization-and-duplicate-attribute-resiliency"></a>Tolerantie voor synchronisatie- en duplicatiekenmerken identificeren
Dubbele kenmerk tolerantie is een functie in Azure Active Directory, die wordt veroorzaakt door wrijving elimineren **UserPrincipalName** en **ProxyAddress** veroorzaakt een conflict bij het uitvoeren van een van de hulpprogramma's voor Microsoft synchronisatie.

Deze twee kenmerken in het algemeen vereist toobe uniek zijn voor alle **gebruiker**, **groep**, of **Contact** objecten in een bepaalde Azure Active Directory-tenant.

> [!NOTE]
> Alleen gebruikers kunnen de UPN's hebben.
> 
> 

Hallo nieuw gedrag op dat met deze functie kunt Hallo cloud deel van Hallo sync pipeline, het is daarom client agnostisch en relevant is voor een Microsoft-synchronisatie product met inbegrip van Azure AD Connect, DirSync en MIM-Connector. Hallo algemene term 'sync-client' wordt gebruikt in dit document toorepresent een van deze producten.

## <a name="current-behavior"></a>Huidige gedrag
Als er een poging tooprovision een nieuw object met een UPN- of ProxyAddress-waarde die in strijd met deze beperking voor uniekheid, blokkeert Azure Active Directory dat object kunnen worden gemaakt. Op dezelfde manier als een object wordt bijgewerkt met een niet-unieke UPN of ProxyAddress, Hallo bijwerken is mislukt. Hallo inrichting poging of update is opnieuw uitgevoerd door de Hallo sync-client bij elke cyclus exporteren en toofail blijft totdat Hallo conflict opgelost is. Een e-mailbericht fout rapport wordt gegenereerd na elke poging en een fout wordt vastgelegd door Hallo sync-client.

## <a name="behavior-with-duplicate-attribute-resiliency"></a>Gedrag met dubbel kenmerk tolerantie
In plaats van volledig mislukt tooprovision of bijwerken van een object met een dubbel kenmerk Azure Active Directory 'quarantaine' hello dubbele kenmerk waardoor het Hallo-beperking voor uniekheid zou schenden. Als dit kenmerk vereist is voor het inrichten, zoals UserPrincipalName, toegewezen Hallo-service een tijdelijke aanduidingswaarde. Hallo-indeling van deze tijdelijke waarden is  
"***<OriginalPrefix>+ < 4DigitNumber > @<InitialTenantDomain>. onmicrosoft.com***'.  
Als het Hallo-kenmerk is niet vereist, zoals een **ProxyAddress**, Azure Active Directory gewoon Hallo conflict kenmerk quarantaine en wordt doorgegaan met Hallo-object maken of bijwerken.

Bij het in quarantaine plaatsen Hallo kenmerk, informatie over Hallo conflict in Hallo dezelfde fout rapport e-mailadres gebruikt in de oude gedrag Hallo verzonden. Echter, deze informatie wordt alleen weergegeven in het foutenrapport Hallo één keer als Hallo quarantaine gebeurt, deze wordt niet voortgezet toobe geregistreerd in de toekomst e-mailberichten. Bovendien aangezien Hallo exporteren voor dit object is geslaagd, Hallo sync-client wordt niet geregistreerd voor een fout en wordt niet opnieuw Hallo maken / update-bewerking op de volgende synchronisatiecycli.

Dit gedrag van een nieuw kenmerk is toosupport toohello gebruikers, groepen en neem contact op met de objectklassen toegevoegd:  
**DirSyncProvisioningErrors**

Dit is een kenmerk met meerdere waarden die gebruikte toostore Hallo conflicterende kenmerken die Hallo-beperking voor uniekheid zou schenden moeten ze worden toegevoegd normaal. Een timer achtergrondtaak is ingeschakeld in Azure Active Directory, die elk uur toolook voor dubbel kenmerk conflicten die zijn opgelost en Hallo kenmerken betrokken automatisch verwijderd uit quarantaine uitvoert.

### <a name="enabling-duplicate-attribute-resiliency"></a>Inschakelen van tolerantie voor dubbele kenmerk
Dubbele kenmerk tolerantie worden nieuwe standaardgedrag Hallo over alle Azure Active Directory-tenants. Deze bevindt zich op standaard voor alle tenants die ingeschakeld synchronisatie voor Hallo eerst 22 augustus 2016 of hoger. Tenants die synchronisatie voorafgaande toothis datum ingeschakeld hebt ingeschakeld in batches Hallo-functie. Deze implementatie begint September 2016 en een e-mailmelding wordt verzonden van de tenant tooeach technische berichtgeving contact met specifieke Hallo-datum wanneer Hallo-functie wordt ingeschakeld.

> [!NOTE]
> Nadat de tolerantie voor dubbele kenmerk is ingeschakeld kan niet worden uitgeschakeld.

toocheck als Hallo-functie is ingeschakeld voor uw tenant, kunt u doen door de meest recente versie van Azure Active Directory PowerShell-module Hallo Hallo downloaden en uitvoeren:

`Get-MsolDirSyncFeatures -Feature DuplicateUPNResiliency`

`Get-MsolDirSyncFeatures -Feature DuplicateProxyAddressResiliency`

> [!NOTE]
> U kunt Set-MsolDirSyncFeature cmdlet tooproactively inschakelen Hallo tolerantie voor dubbele kenmerk functie niet meer gebruiken voordat deze is ingeschakeld voor uw tenant. toobe kunnen tootest Hallo functie, moet u een nieuwe Azure Active Directory-tenant toocreate.

## <a name="identifying-objects-with-dirsyncprovisioningerrors"></a>Objecten met DirSyncProvisioningErrors identificeren
Er zijn momenteel twee methoden tooidentify-objecten die u deze fouten vanwege conflicten met tooduplicate eigenschap, Azure Active Directory PowerShell en Hallo Office 365-beheerportal hebt. Er zijn plannen tooextend tooadditional portal op basis van rapportage in toekomstige Hallo.

### <a name="azure-active-directory-powershell"></a>Azure Active Directory PowerShell
Voor Hallo PowerShell-cmdlets in dit onderwerp is Hallo volgende waar:

* Alle cmdlets volgen Hallo zijn hoofdlettergevoelig.
* Hallo **– ErrorCategory PropertyConflict** moet altijd worden opgenomen. Er zijn momenteel geen andere typen **ErrorCategory**, maar dit kan worden uitgebreid in toekomstige Hallo.

Eerst aan de slag door te voeren **Connect MsolService** en referenties voor een tenantbeheerder invoeren.

Vervolgens Hallo volgende-cmdlets en -operators tooview-fouten op verschillende manieren gebruiken:

1. [Alle](#see-all)
2. [Door de eigenschapstype](#by-property-type)
3. [Met conflicterende waarde](#by-conflicting-value)
4. [Met behulp van een zoekopdracht in de tekenreeks](#using-a-string-search)
5. [Gesorteerd](#sorted)
6. [In een beperkt aantal of alle](#in-a-limited-quantity-or-all)

#### <a name="see-all"></a>Alles bekijken
Eenmaal zijn verbonden, toosee een algemene lijst van fouten in de tenant Hallo inrichting kenmerk uitvoeren:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict`

Dit resulteert in een resultaat Hallo volgende:  
 ![Get-MsolDirSyncProvisioningError](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1.png "Get-MsolDirSyncProvisioningError")  

#### <a name="by-property-type"></a>Door de eigenschapstype
toosee fouten per eigenschaptype toevoegen Hallo **- PropertyName** vlag Hello **UserPrincipalName** of **ProxyAddresses** argument:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName UserPrincipalName`

of

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName ProxyAddresses`

#### <a name="by-conflicting-value"></a>Met conflicterende waarde
toosee fouten over de specifieke eigenschap tooa toevoegen Hallo **- PropertyValue** vlag (**- PropertyName** moet ook worden gebruikt bij het toevoegen van deze vlag):

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyValue User@domain.com -PropertyName UserPrincipalName`

#### <a name="using-a-string-search"></a>Met behulp van een zoekopdracht in de tekenreeks
een zoekopdracht brede tekenreeks toodo gebruiken Hallo **- zoekreeks** vlag. Dit kan onafhankelijk worden gebruikt vanaf alle Hallo hierboven vlaggen, met uitzondering van Hallo **- ErrorCategory PropertyConflict**, die is vereist:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -SearchString User`

#### <a name="in-a-limited-quantity-or-all"></a>In een beperkt aantal of alle
1. **MaxResults <Int>**  kan toolimit Hallo query tooa specifiek aantal waarden gebruikt.
2. **Alle** mag gebruikte tooensure alle resultaten worden opgehaald in geval van Hallo die een groot aantal fouten bestaat.

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -MaxResults 5`

## <a name="office-365-admin-portal"></a>Office 365-beheerportal
U kunt directory-synchronisatiefouten weergeven in Hallo Office 365-beheercentrum. rapport in Office 365 Hallo portal weergegeven Hallo **gebruiker** objecten die u deze fouten hebt. Informatie over conflicten tussen wordt niet weergegeven **groepen** en **contactpersonen**.

![Actieve gebruikers](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1234.png "actieve gebruikers")

Zie voor instructies over hoe tooview directory-synchronisatiefouten in Hallo Office 365 admin center, [identificeren van directory-synchronisatiefouten in Office 365](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067).

### <a name="identity-synchronization-error-report"></a>Identiteit synchronisatie foutenrapport
Wanneer een object met een dubbel kenmerk conflict wordt verwerkt met dit nieuwe gedrag die een melding is opgenomen in verzonden hello standaard e-identiteit synchronisatie foutenrapport die contact op met technische berichtgeving toohello voor Hallo-tenant. Er is echter een belangrijke wijziging in dit gedrag. In de afgelopen Hallo, zou informatie over een dubbel kenmerk conflict worden opgenomen in elke volgende foutrapport totdat Hallo conflict opgelost is. Met dit nieuwe gedrag wordt Hallo foutmeldingen voor een bepaalde conflict alleen weergegeven eenmaal - gelijktijdig Hallo Hallo conflicterende kenmerk in quarantaine is geplaatst.

Hier volgt een voorbeeld van welke e-mailmelding Hallo ziet er voor een conflict ProxyAddress:  
    ![Actieve gebruikers](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "actieve gebruikers")  

## <a name="resolving-conflicts"></a>Het oplossen van conflicten
Strategie en resolutie tactieken voor deze fouten oplossen moet niet verschillen van Hallo manier dubbel kenmerk fouten in de afgelopen Hallo zijn verwerkt. Hallo enige verschil is Hallo timer taak krijgen via Hallo tenant op Hallo aan servicezijde tooautomatically Hallo-kenmerk toevoegen in het juiste object van vraag toohello zodra Hallo conflict is opgelost.

Hallo volgende artikel bevat een overzicht van verschillende strategieën voor het oplossen van problemen en resolutie: [dubbele of ongeldige kenmerken te voorkomen dat directory-synchronisatie in Office 365](https://support.microsoft.com/kb/2647098).

## <a name="known-issues"></a>Bekende problemen
Geen van deze bekende problemen zorgt ervoor dat gegevens verloren gaan of de service nadelig beïnvloeden. Sommige hiervan zijn esthetische, anderen standaard veroorzaken '*vooraf tolerantie*' dubbel kenmerk fouten toobe geretourneerd in plaats van in quarantaine plaatsen Hallo conflict kenmerk en een andere zorgt ervoor dat bepaalde fouten toorequire extra handmatig bijwerken.

**Core-gedrag:**

1. Objecten van het specifieke kenmerk configuraties blijven tooreceive exportfouten als tegengestelde toohello dubbele kenmerken in quarantaine wordt geplaatst.  
   Bijvoorbeeld:
   
    a. Nieuwe gebruiker is gemaakt in AD met de UPN-  **Joe@contoso.com**  en ProxyAddress**smtp:Joe@contoso.com**
   
    b. Hallo eigenschappen van dit object in conflict met een bestaande groep, waarbij ProxyAddress is  **SMTP:Joe@contoso.com** .
   
    c. Bij het exporteren, een **ProxyAddress conflict** fout wordt gegenereerd in plaats van Hallo conflict kenmerken in quarantaine geplaatst. Hallo-bewerking wordt opnieuw geprobeerd bij elke cyclus volgende synchronisatie als zijn zou voordat Hallo tolerantiefunctie is ingeschakeld.
2. Als twee groepen worden gemaakt met on-premises Hallo dezelfde SMTP-adres, een mislukt tooprovision bij de eerste poging Hallo met een dubbele standaard **ProxyAddress** fout. Echter, Hallo dubbele waarde is juist in quarantaine geplaatst op Hallo volgende synchronisatiecyclus.

**Office-Portal rapport**:

1. Hallo gedetailleerd foutbericht voor twee objecten in een conflict UPN-set is Hallo dezelfde. Dit betekent dat ze hebben beide de UPN gewijzigd / in quarantaine geplaatst wanneer in feite alleen een van deze had geen gegevens die zijn gewijzigd.
2. Hallo gedetailleerde foutbericht voor een conflict UPN toont Hallo verkeerde weergavenaam voor een gebruiker die de UPN gewijzigd/in quarantaine heeft gehad. Bijvoorbeeld:
   
    a. **Gebruiker A** gesynchroniseerd eerst met **UPN = User@contoso.com** .
   
    b. **Gebruiker B** is geprobeerde toobe gesynchroniseerd volgende met **UPN = User@contoso.com** .
   
    c. **Gebruiker B** UPN te wordt gewijzigd **User1234@contoso.onmicrosoft.com**  en  **User@contoso.com**  te wordt toegevoegd**DirSyncProvisioningErrors**.
   
    d. Hallo foutbericht voor **gebruiker B** zou moeten aangeven die **gebruiker A** al  **User@contoso.com**  zoals u ziet een UPN, maar het **van gebruiker B** eigen Weergavenaam.

**Identiteit synchronisatie foutenrapport**:

Hallo-koppeling voor *Stapsgewijze instructies voor het tooresolve dit probleem* is onjuist:  
    ![Actieve gebruikers](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "actieve gebruikers")  

Het te moet verwijzen[https://aka.ms/duplicateattributeresiliency](https://aka.ms/duplicateattributeresiliency).

## <a name="see-also"></a>Zie ook
* [Azure AD Connect-synchronisatie](active-directory-aadconnectsync-whatis.md)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
* [Identificeren van directory-synchronisatiefouten in Office 365](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067)

