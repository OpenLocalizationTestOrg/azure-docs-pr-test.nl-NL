---
title: 'Azure AD Connect: Het oplossen van problemen tijdens de synchronisatie | Microsoft Docs'
description: Legt uit hoe tootroubleshoot fouten aangetroffen tijdens de synchronisatie met Azure AD Connect.
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 2209d5ce-0a64-447b-be3a-6f06d47995f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: af262dfe95d686e34697454c0dfe8b4a6d8693c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-errors-during-synchronization"></a>Het oplossen van problemen tijdens de synchronisatie
Er kunnen optreden wanneer id-gegevens worden gesynchroniseerd vanuit Windows Server Active Directory (AD DS) tooAzure Active Directory (Azure AD). Dit artikel bevat een overzicht van de verschillende soorten synchronisatiefouten enkele mogelijke scenario's voor een Hallo die deze fouten en mogelijke manieren toofix Hallo fouten veroorzaken. Dit artikel bevat de algemene fouttypen Hallo en kan geen betrekking op alle Hallo mogelijke fouten.

 In dit artikel wordt ervan uitgegaan dat Hallo lezer bekend bent met het onderliggende hello [ontwerpen concepten van Azure AD en Azure AD Connect](active-directory-aadconnect-design-concepts.md).

Met de meest recente versie van Azure AD Connect Hallo \(augustus 2016 of hoger\), een rapport van synchronisatie van fouten is beschikbaar in Hallo [Azure Portal](https://aka.ms/aadconnecthealth) als onderdeel van Azure AD Connect Health voor synchroniseren.

Vanaf 1 September 2016 [Azure Active Directory dubbel kenmerk tolerantie](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) functie wordt ingeschakeld voor alle Hallo standaard *nieuwe* Azure Active Directory-Tenants. Deze functie wordt automatisch ingeschakeld voor bestaande tenants in de komende maanden Hallo.

Azure AD Connect voert 3 soorten bewerkingen van Hallo directory's gesynchroniseerd blijven: Import, synchronisatie en exporteren. Fouten kunnen worden uitgevoerd in alle Hallo-bewerkingen. In dit artikel richt zich voornamelijk op fouten tijdens de Export tooAzure AD.

## <a name="errors-during-export-tooazure-ad"></a>Fouten tijdens de Export tooAzure AD
Beschrijving van verschillende typen volgende sectie van de synchronisatie van fouten die optreden tijdens het Hallo export bewerking tooAzure AD met behulp van kunnen Azure AD-connector Hallo. Deze connector kan worden geïdentificeerd door de indeling van de Hallo wordt 'contoso. *onmicrosoft.com*'.
Fouten tijdens de Export tooAzure AD aangeven die bewerking Hallo \(toevoegen, bijwerken en verwijderen enzovoort\) geprobeerd met Azure AD Connect \(synchronisatie-Engine\) op Azure Active Directory is mislukt.

![Overzicht van fouten exporteren](./media/active-directory-aadconnect-troubleshoot-sync-errors/Export_Errors_Overview_01.png)

## <a name="data-mismatch-errors"></a>Gegevens komen niet overeen fouten
### <a name="invalidsoftmatch"></a>InvalidSoftMatch
#### <a name="description"></a>Beschrijving
* Wanneer Azure AD Connect \(synchronisatie-engine\) Hiermee geeft u Azure Active Directory-tooadd of update objecten, Azure AD komt overeen met binnenkomende-object op met de Hallo Hallo **sourceAnchor** toohello kenmerk  **onveranderbare id genoemd** kenmerk van objecten in Azure AD. Deze overeenkomst, heet een **harde overeen met**.
* Wanneer Azure AD **vindt geen** elk object dat overeenkomt met de Hallo **onveranderbare id genoemd** kenmerk met de Hallo **sourceAnchor** kenmerk van inkomende hello-object, voordat u inricht een Nieuw object valt terug toouse Hallo ProxyAddresses en UserPrincipalName kenmerken toofind een overeenkomst. Deze overeenkomst, heet een **zachte overeen met**. Hallo zachte overeenkomst is ontworpen toomatch objecten al aanwezig in Azure AD (die afkomstig zijn in Azure AD) met Hallo nieuwe objecten worden toegevoegd/bijgewerkt tijdens de synchronisatie met daarin Hallo dezelfde entiteit (gebruikers, groepen) on-premises.
* **InvalidSoftMatch** fout treedt op wanneer hello harde overeenkomst geen overeenkomende objecten vindt **en** zachte overeen met een overeenkomende object vindt, maar dat object heeft een andere waarde van *onveranderbare id genoemd* dan Hallo binnenkomende object *SourceAnchor*, voorstellen die Hallo die overeenkomt met object is gesynchroniseerd met een ander object op basis van on-premises Active Directory.

Met andere woorden, in volgorde voor Hallo zachte overeen toowork Hallo object toobe voorlopig komt overeen met moet niet een waarde hebben voor Hallo *onveranderbare id genoemd*. Als een met object *onveranderbare id genoemd* set met een waarde is niet mogelijk Hallo harde-match maar voldoen aan Hallo soft-match criteria, Hallo bewerking resulteert in een synchronisatiefout InvalidSoftMatch.

Azure Active Directory schema staat niet toe dat twee of meer objecten toohave dezelfde waarde voor de volgende Hallo Hallo kenmerken. \(Dit is geen uitputtende lijst.\)

* ProxyAddresses
* UserPrincipalName
* onPremisesSecurityIdentifier
* object-id

> [!NOTE]
> [Azure AD-kenmerk dubbel kenmerk tolerantie](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) functie wordt ook worden geïnstalleerd als standaardgedrag Hallo van Azure Active Directory.  Zo beperkt u Hallo aantal synchronisatiefouten gezien door Azure AD Connect (evenals andere clients sync) door Azure AD toleranter in Hallo wijze die gedupliceerde ProxyAddresses en UserPrincipalName kenmerken aanwezig zijn in on-premises AD worden verwerkt omgevingen. Deze functie niet wordt opgelost Hallo dubbele elementen. Hallo gegevens moet daarom nog steeds toobe vast. Maar kunt inrichten van nieuwe objecten die anders is geblokkeerd vanwege tooduplicated waarden wordt ingericht in Azure AD. Zo beperkt u ook Hallo aantal synchronisatiefouten toohello synchronisatie client geretourneerd.
> Als deze functie is ingeschakeld voor uw Tenant, worden er geen Hallo InvalidSoftMatch synchronisatie van fouten weergegeven tijdens het inrichten van nieuwe objecten.
>
>

#### <a name="example-scenarios-for-invalidsoftmatch"></a>Voorbeeldscenario's voor InvalidSoftMatch
1. Twee of meer objecten met dezelfde waarde voor kenmerk ProxyAddresses in on-premises Active Directory bestaat Hallo. Slechts één wordt ophalen ingericht in Azure AD.
2. Twee of meer objecten met dezelfde waarde voor userPrincipalName in on-premises Active Directory bestaat Hallo. Slechts één wordt ophalen ingericht in Azure AD.
3. Een object is toegevoegd in Hallo on-premises Active Directory Hello dezelfde waarde van kenmerk ProxyAddresses als die van een bestaand object in Azure Active Directory. Hallo-object toegevoegd on-premises is niet ophalen van ingericht in Azure Active Directory.
4. Een object is toegevoegd in on-premises Active Directory Hello dezelfde waarde van het kenmerk userPrincipalName als die van een account in Azure Active Directory. Hallo-object is niet ophalen van ingericht in Azure Active Directory.
5. Een gesynchroniseerde-account is verplaatst in Forest A tooForest B. Azure AD Connect (sync engine) is ObjectGUID kenmerk toocompute hello SourceAnchor met. Hallo-waarde van Hallo SourceAnchor is na Hallo forest verplaatsen, anders. Nieuw object hello (van Forest B) mislukt toosync met het bestaande object Hallo in Azure AD.
6. Een gesynchroniseerd object per ongeluk hebt verwijderd uit on-premises Active Directory en een nieuw object is gemaakt in Active Directory voor Hallo dezelfde entiteit (zoals gebruiker) zonder Hallo-account in Azure Active Directory te verwijderen. de nieuwe account Hallo mislukt toosync met Hallo bestaande Azure AD-object.
7. Azure AD Connect is verwijderd en opnieuw geïnstalleerd. Tijdens het Hallo opnieuw installeren, is een ander kenmerk gekozen als Hallo SourceAnchor. Alle Hallo-objecten die eerder was gesynchroniseerd gestopt synchroniseren met InvalidSoftMatch fout.

#### <a name="example-case"></a>Voorbeeld van de case:
1. **Bob Smith** is een gesynchroniseerde gebruiker in Azure Active Directory vanuit de on-premises Active Directory van *contoso.com*
2. Bob Smith **UserPrincipalName** is ingesteld als  **bobs@contoso.com** .
3. **' abcdefghijklmnopqrstuv == "** Hallo is **SourceAnchor** berekend door Azure AD Connect met Bob Smith **objectGUID** van on-premises Active Directory, die is Hallo **onveranderbare id genoemd** voor Bob Smith bij Azure Active Directory.
4. Bob heeft ook de volgende waarden voor Hallo **proxyAddresses** kenmerk:
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
5. Een nieuwe gebruiker **Bob Taylor**, toohello on-premises Active Directory wordt toegevoegd.
6. Bob Taylor van **UserPrincipalName** is ingesteld als  **bobt@contoso.com** .
7. **' abcdefghijkl0123456789 == ""** Hallo is **sourceAnchor** berekend door Azure AD Connect met Bob Taylor van **objectGUID** premises uit op Active Directory. Bob Taylor van object is niet gesynchroniseerd tooAzure Active Directory.
8. Bob Taylor heeft de volgende waarden voor Hallo proxyAddresses kenmerk Hallo
   * smtp:bobt@contoso.com
   * smtp:bob.taylor@contoso.com
   * **smtp:bob@contoso.com**
9. Tijdens de synchronisatie, Azure AD Connect wordt herkend Hallo toevoeging van Bob Taylor in on-premises Active Directory en vraagt u Azure AD toomake Hallo dezelfde wijziging.
10. Azure AD wordt eerst harde overeen uitvoeren. Dat wil zeggen, zoekt als er een object met Hallo onveranderbare id genoemd gelijk te ' abcdefghijkl0123456789 == ". Vaste overeen zal mislukken als er geen andere objecten in Azure AD die onveranderbare id genoemd hebben.
11. Azure AD probeert vervolgens toosoft-match Bob Taylor. Dat wil zeggen, zoekt als er een object met proxyAddresses gelijk toohello drie waarden, waarondersmtp:bob@contoso.com
12. Azure AD vinden van Bob Smith object toomatch Hallo soft-match criteria. Maar dit object Hallo waarde heeft van onveranderbare id genoemd = "abcdefghijklmnopqrstuv ==". wat aangeeft dat dit object is gesynchroniseerd vanuit een ander object van on-premises Active Directory. Dus Azure AD kan niet soft-match deze objecten en resulteert in een **InvalidSoftMatch** synchronisatiefout.

#### <a name="how-toofix-invalidsoftmatch-error"></a>Hoe toofix InvalidSoftMatch fout
Hallo meest voorkomende reden voor fout InvalidSoftMatch Hallo is twee objecten met verschillende SourceAnchor \(onveranderbare id genoemd\) hebben dezelfde waarde voor Hallo ProxyAddresses en/of UserPrincipalName kenmerken, die worden gebruikt tijdens het Hallo Hallo Soft-match-proces op Azure AD. In de volgorde toofix Hallo ongeldig zachte overeenkomend

1. Identificeer Hallo gedupliceerd proxyAddresses, userPrincipalName of andere kenmerkwaarde die Hallo fout veroorzaakt. Ook bepalen welke twee \(of meer\) objecten in Hallo conflict zijn betrokken. rapport is gegenereerd door Hallo [Azure AD Connect Health voor synchroniseren](https://aka.ms/aadchsyncerrors) kunt u Hallo twee objecten identificeren.
2. Welk object toohave Hallo gedupliceerd waarde moet blijven en welk object beter niet identificeren.
3. Hallo gedupliceerd waarde uit het Hallo-object dat deze waarde mag geen verwijderen. Houd er rekening mee dat moet u Hallo wijzigen van het Hallo-directory waar Hallo object afkomstig is uit. In sommige gevallen moet u toodelete een van de objecten Hallo in conflict.
4. Als u Hallo wijzigen in Hallo on-premises AD hebt gemaakt, kunt u Azure AD Connect-synchronisatie Hallo wijzigen.

Vergeet niet dat synchronisatie foutenrapport in Azure AD Connect Health voor synchroniseren elke 30 minuten bijgewerkt wordt en Hallo-fouten van de laatste synchronisatiepoging Hallo bevat.

> [!NOTE]
> Onveranderbare id genoemd, moet per definitie niet wijzigen in Hallo levensduur van Hallo-object. Als Azure AD Connect is niet geconfigureerd met een aantal scenario's Hallo rekening van Hallo boven lijst, kan het uiteindelijke in een situatie waarin Azure AD Connect wordt berekend met een andere waarde Hallo SourceAnchor voor Hallo AD-object dat vertegenwoordigt dezelfde entiteit Hallo (dezelfde gebruiker / groep/contact enzovoort) die een bestaand Azure AD-Object dat u met behulp van toocontinue wilt heeft.
>
>

#### <a name="related-articles"></a>Verwante artikelen
* [Dubbel of ongeldige kenmerken te voorkomen dat directory-synchronisatie in Office 365](https://support.microsoft.com/en-us/kb/2647098)

### <a name="objecttypemismatch"></a>ObjectTypeMismatch
#### <a name="description"></a>Beschrijving
Wanneer Azure AD toosoft overeen twee objecten probeert, is het mogelijk dat twee objecten van verschillende "objecttype' (zoals een gebruiker, groep-, enz. Neem contact op met) hebben Hallo dezelfde waarden voor Hallo kenmerken tooperform Hallo zachte overeen gebruikt. Als deze kenmerken worden gedupliceerd is niet toegestaan in Azure AD, Hallo-bewerking kan leiden tot synchronisatiefout 'ObjectTypeMismatch'.

#### <a name="example-scenarios-for-objecttypemismatch-error"></a>Voorbeeldscenario's voor ObjectTypeMismatch fout
* Een e-mailtoegang beveiligingsgroep wordt gemaakt in Office 365. Beheerder voegt een nieuwe gebruiker of neem contact op met in on-premises AD (die tooAzure AD nog niet gesynchroniseerd) met dezelfde voor Hallo ProxyAddresses kenmerk als die van Office 365 Hallo waarde Hallo groeperen.

#### <a name="example-case"></a>Voorbeeld van de aanvraag
1. De beheerder maakt een nieuwe beveiligingsgroep voor e-mailtoegang in Office 365 voor Hallo btw afdeling en biedt een e-mailadres als tax@contoso.com. Dit wijst Hallo ProxyAddresses kenmerk voor deze groep met de Hallo waarde**smtp:tax@contoso.com**
2. Een nieuwe gebruiker koppelt Contoso.com en een account is gemaakt voor de gebruiker Hallo on-premises met Hallo proxyAddress als**smtp:tax@contoso.com**
3. Wanneer u Azure AD Connect synchroniseert Hallo nieuwe gebruikersaccount, krijgt het Hallo 'ObjectTypeMismatch'-fout.

#### <a name="how-toofix-objecttypemismatch-error"></a>Hoe toofix ObjectTypeMismatch fout
meest voorkomende reden voor Hallo ObjectTypeMismatch fout Hallo is twee objecten van het andere type (gebruiker, groep-, enz. Neem contact op met) hebben dezelfde voor Hallo ProxyAddresses kenmerk waarde Hallo. In de volgorde toofix hello ObjectTypeMismatch:

1. Hallo gedupliceerd identificeren proxyAddresses (of een ander kenmerk) waarde dat veroorzaakt Hallo-fout. Ook bepalen welke twee \(of meer\) objecten in Hallo conflict zijn betrokken. rapport is gegenereerd door Hallo [Azure AD Connect Health voor synchroniseren](https://aka.ms/aadchsyncerrors) kunt u Hallo twee objecten identificeren.
2. Welk object toohave Hallo gedupliceerd waarde moet blijven en welk object beter niet identificeren.
3. Hallo gedupliceerd waarde uit het Hallo-object dat deze waarde mag geen verwijderen. Houd er rekening mee dat moet u Hallo wijzigen van het Hallo-directory waar Hallo object afkomstig is uit. In sommige gevallen moet u toodelete een van de objecten Hallo in conflict.
4. Als u Hallo wijzigen in Hallo on-premises AD hebt gemaakt, kunt u Azure AD Connect-synchronisatie Hallo wijzigen. Synchronisatie foutenrapport in Azure AD Connect Health voor synchroniseren wordt elke 30 minuten bijgewerkt en Hallo-fouten van de laatste synchronisatiepoging Hallo bevat.

## <a name="duplicate-attributes"></a>Dubbele kenmerken
### <a name="attributevaluemustbeunique"></a>AttributeValueMustBeUnique
#### <a name="description"></a>Beschrijving
Azure Active Directory schema staat niet toe dat twee of meer objecten toohave dezelfde waarde voor de volgende Hallo Hallo kenmerken. Dat elk object in Azure AD is gedwongen toohave een unieke waarde van deze kenmerken op een opgegeven exemplaar is.

* ProxyAddresses
* UserPrincipalName

Als Azure AD Connect probeert tooadd een nieuw object of een bestaand object bijwerken met een waarde voor Hallo hierboven kenmerken die tooanother-object in Azure Active Directory al is toegewezen, wordt Hallo bewerking resulteert in Hallo 'AttributeValueMustBeUnique' synchronisatiefout.

#### <a name="possible-scenarios"></a>Mogelijke scenario's:
1. Dubbele waarde is toegewezen tooan al gesynchroniseerd object, wat een conflict met een ander gesynchroniseerd object veroorzaakt.

#### <a name="example-case"></a>Voorbeeld van de case:
1. **Bob Smith** is een gesynchroniseerde gebruiker in Azure Active Directory vanuit de on-premises Active Directory contoso.com
2. Bob Smith **UserPrincipalName** on-premises is ingesteld als  **bobs@contoso.com** .
3. Bob heeft ook de volgende waarden voor Hallo **proxyAddresses** kenmerk:
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
4. Een nieuwe gebruiker **Bob Taylor**, toohello on-premises Active Directory wordt toegevoegd.
5. Bob Taylor van **UserPrincipalName** is ingesteld als  **bobt@contoso.com** .
6. **Bob Taylor** heeft de volgende waarden voor Hallo Hallo **ProxyAddresses** kenmerk i. smtp:bobt@contoso.comII. smtp:bob.taylor@contoso.com
7. Bob Taylor van object wordt gesynchroniseerd met Azure AD is.
8. Beheerder besloten tooupdate Bob Taylor **ProxyAddresses** kenmerk met de volgende waarde Hallo: ik. **smtp:bob@contoso.com**
9. Azure AD probeert tooupdate Bob Taylor object in Azure AD Hello boven waarde, maar die bewerking mislukken als ProxyAddresses waarde is al toegewezen tooBob Smith, waardoor fout 'AttributeValueMustBeUnique'.

#### <a name="how-toofix-attributevaluemustbeunique-error"></a>Hoe toofix AttributeValueMustBeUnique fout
Hallo meest voorkomende reden voor fout AttributeValueMustBeUnique Hallo is twee objecten met verschillende SourceAnchor \(onveranderbare id genoemd\) Hallo dezelfde voor Hallo ProxyAddresses en/of UserPrincipalName kenmerken waarde hebben. In de volgorde toofix AttributeValueMustBeUnique fout

1. Identificeer Hallo gedupliceerd proxyAddresses, userPrincipalName of andere kenmerkwaarde die Hallo fout veroorzaakt. Ook bepalen welke twee \(of meer\) objecten in Hallo conflict zijn betrokken. rapport is gegenereerd door Hallo [Azure AD Connect Health voor synchroniseren](https://aka.ms/aadchsyncerrors) kunt u Hallo twee objecten identificeren.
2. Welk object toohave Hallo gedupliceerd waarde moet blijven en welk object beter niet identificeren.
3. Hallo gedupliceerd waarde uit het Hallo-object dat deze waarde mag geen verwijderen. Houd er rekening mee dat moet u Hallo wijzigen van het Hallo-directory waar Hallo object afkomstig is uit. In sommige gevallen moet u toodelete een van de objecten Hallo in conflict.
4. Als u Hallo wijzigen in Hallo on-premises AD hebt gemaakt, kunt u Azure AD Connect-synchronisatie Hallo voor Hallo fout tooget vaste wijzigen.

#### <a name="related-articles"></a>Verwante artikelen
-[Dubbel of ongeldige kenmerken te voorkomen dat directory-synchronisatie in Office 365](https://support.microsoft.com/en-us/kb/2647098)

## <a name="data-validation-failures"></a>Mislukte gegevensvalidatie
### <a name="identitydatavalidationfailed"></a>IdentityDataValidationFailed
#### <a name="description"></a>Beschrijving
Azure Active Directory wordt afgedwongen voor verschillende beperkingen op Hallo gegevens zelf voordat u toestaat dat gegevens toobe naar Hallo-map geschreven. Dit is tooensure die eindgebruikers Hallo best mogelijke ervaring tijdens het gebruik van Hallo-toepassingen die afhankelijk van deze gegevens zijn ophalen.

#### <a name="scenarios"></a>Scenario's
a. Hallo waarde van het kenmerk UserPrincipalName heeft ongeldig/niet-ondersteunde tekens.
b. Hallo UserPrincipalName kenmerk voldoet niet aan de vereiste indeling Hallo.

#### <a name="how-toofix-identitydatavalidationfailed-error"></a>Hoe toofix IdentityDataValidationFailed fout
a. Zorg ervoor dat Hallo userPrincipalName-kenmerk heeft tekens en de vereiste indeling wordt ondersteund.

#### <a name="related-articles"></a>Verwante artikelen
* [Tooprovision gebruikers via de directory-synchronisatie tooOffice 365 voorbereiden](https://support.office.com/en-us/article/Prepare-to-provision-users-through-directory-synchronization-to-Office-365-01920974-9e6f-4331-a370-13aea4e82b3e)

### <a name="federateddomainchangeerror"></a>FederatedDomainChangeError
#### <a name="description"></a>Beschrijving
Dit is een specifieke aanvraag die resulteert in een **'FederatedDomainChangeError'** synchronisatiefout wanneer Hallo-achtervoegsel van de UserPrincipalName van een gebruiker uit een federatieve domein tooanother federatieve domein wordt gewijzigd.

#### <a name="scenarios"></a>Scenario's
Voor een gesynchroniseerde gebruiker is Hallo UserPrincipalName achtervoegsel gewijzigd van een federatieve domein tooanother federatieve domein on-premises. Bijvoorbeeld: *UserPrincipalName = bob@contoso.com*  te is gewijzigd*UserPrincipalName = bob@fabrikam.com* .

#### <a name="example"></a>Voorbeeld
1. Bob Smith, een account voor Contoso.com is, wordt toegevoegd als een nieuwe gebruiker in Active Directory met Hallo UserPrincipalNamebob@contoso.com
2. Bob verplaatst tooa verschillende deling contoso.com Fabrikam.com en zijn UserPrincipalName wordt gewijzigd.toobob@fabrikam.com
3. Contoso.com en fabrikam.com domeinen zijn gefedereerde met Azure Active Directory-domeinen.
4. Berend userPrincipalName niet wordt bijgewerkt en resulteert in een synchronisatiefout 'FederatedDomainChangeError'.

#### <a name="how-toofix"></a>Hoe toofix
Als een gebruiker UserPrincipalName achtervoegsel is bijgewerkt van bob @**contoso.com** toobob @**fabrikam.com**, waarbij beide **contoso.com** en **fabrikam.com** zijn **domeinen federatieve**, volg deze stappen toofix Hallo-synchronisatiefout

1. Bijwerken van de gebruiker Hallo UserPrincipalName in Azure AD van bob@contoso.com toobob@contoso.onmicrosoft.com. Kunt u de volgende PowerShell-opdracht met hello Azure AD PowerShell-Module hello gebruiken:`Set-MsolUserPrincipalName -UserPrincipalName bob@contoso.com -NewUserPrincipalName bob@contoso.onmicrosoft.com`
2. Hallo volgende synchronisatie cyclus tooattempt synchronisatie toestaan. Deze tijdsynchronisatie kan worden geverifieerd en wordt bijgewerkt Hallo UserPrincipalName van Bob toobob@fabrikam.com zoals verwacht.

#### <a name="related-articles"></a>Verwante artikelen
* [Wijzigingen zijn niet gesynchroniseerd door hello Azure Active Directory-synchronisatie nadat u Hallo UPN van een gebruiker account toouse een ander federatieve domein wijzigen](https://support.microsoft.com/en-us/help/2669550/changes-aren-t-synced-by-the-azure-active-directory-sync-tool-after-you-change-the-upn-of-a-user-account-to-use-a-different-federated-domain)

## <a name="largeobject"></a>LargeObject
### <a name="description"></a>Beschrijving
Wanneer een kenmerk toegestane maximale grootte, de lengtelimiet of de limiet voor het aantal ingesteld met Azure Active Directory-schema hello overschrijdt, Hallo synchronisatiebewerking resulteert in Hallo **LargeObject** of **ExceededAllowedLength** synchronisatiefout. Deze fout treedt doorgaans op voor Hallo na kenmerken

* userCertificate
* userSMIMECertificate
* thumbnailPhoto
* proxyAddresses

### <a name="possible-scenarios"></a>Mogelijke scenario 's
1. Berend userCertificate kenmerk is te veel certificaten worden toegewezen tooBob opslaan. Deze kunnen oudere, verlopen certificaten bevatten. Hallo vaste limiet is 15 certificaten. Voor meer informatie over hoe toohandle LargeObject fouten met userCertificate kenmerk toe, neem verwijzen tooarticle [LargeObject afhandeling van fouten als gevolg van userCertificate kenmerk](active-directory-aadconnectsync-largeobjecterror-usercertificate.md).
2. Berend userSMIMECertificate kenmerk is te veel certificaten worden toegewezen tooBob opslaan. Deze kunnen oudere, verlopen certificaten bevatten. Hallo vaste limiet is 15 certificaten.
3. Berend thumbnailPhoto instellen in Active Directory is te groot toobe in Azure AD gesynchroniseerd.
4. Tijdens het vullen met automatische van Hallo ProxyAddresses kenmerk in Active Directory heeft een object te veel ProxyAddresses toegewezen.

### <a name="how-toofix"></a>Hoe toofix
1. Zorg ervoor dat Hallo-kenmerk Hallo fout veroorzaakt binnen Hallo beperking toegestaan.

## <a name="related-links"></a>Verwante koppelingen
* [Het vinden van Active Directory-objecten in Active Directory-beheercentrum](https://technet.microsoft.com/library/dd560661.aspx)
* [Hoe tooquery Azure Active Directory voor een object met behulp van Azure Active Directory PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx)
