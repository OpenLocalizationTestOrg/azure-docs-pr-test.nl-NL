---
title: aaaResolve licentieproblemen voor een groep in Azure Active Directory | Microsoft Docs
description: Hoe tooidentify en los licentie toewijzing problemen wanneer u Azure Active Directory-groepen gebaseerde licentieverlening
services: active-directory
keywords: Azure AD-licentieverlening
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ec9c74214a9e246f21fcf767b0bbd586ae702445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="identify-and-resolve-license-assignment-problems-for-a-group-in-azure-active-directory"></a>Het identificeren en oplossen van problemen met licentie-toewijzing voor een groep in Azure Active Directory

Op basis van een groep licentieverlening in Azure Active Directory (Azure AD) introduceert Hallo concept van gebruikers in een foutstatus licentieverlening. In dit artikel wordt uitgelegd we Hallo redenen waarom de gebruikers in deze staat terechtkomen mogelijk.

Wanneer u gebruikers hebt toegewezen licenties rechtstreeks tooindividual, zonder gebruik te maken op basis van een groep-licentieverlening, mislukt Hallo toewijzing. Bijvoorbeeld bij het uitvoeren van PowerShell-cmdlet Hallo `Set-MsolUserLicense` van een gebruiker Hallo-cmdlet voor een aantal redenen die gerelateerd toobusiness logica zijn kan mislukken. Bijvoorbeeld, kunnen er onvoldoende licenties of een conflict tussen twee service-abonnementen kunnen niet worden toegewezen op Hallo dezelfde tijd. Hallo probleem wordt onmiddellijk gerapporteerd back-tooyou.

Wanneer u Groepsbeleid-licentieverlening, Hallo dezelfde fouten kunnen optreden, maar ze gebeuren op Hallo achtergrond wanneer hello Azure AD-service is licenties toewijzen. Om deze reden Hallo fouten kunnen niet worden gecommuniceerd tooyou onmiddellijk. Ze zijn in plaats daarvan op Hallo gebruikersobject geregistreerd en wordt gerapporteerd, via beheerdersrechten Hallo-portal. Houd er rekening mee dat Hallo oorspronkelijke opzet toolicense Hallo gebruiker nooit verloren, maar deze wordt vastgelegd in een foutstatus voor toekomstig onderzoek en omzetten.

## <a name="how-toofind-license-assignment-errors"></a>Hoe toofind toewijzingsfouten licentie

1. toofind gebruikers in een foutstatus van een specifieke groep, open Hallo blade voor Hallo-groep. Onder **licenties**, zal er een melding weergegeven als er geen gebruikers in een foutstatus.

![Groep foutmeldingen](media/active-directory-licensing-group-problem-resolution-azure-portal/group-error-notification.png)

2. Klik op Hallo melding tooopen een lijst met alle betrokken gebruikers. U kunt klikken op elke gebruiker afzonderlijk toosee om meer details.

![Groep lijst met gebruikers in de foutstatus](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-users-with-errors.png)

3. toofind alle groepen met ten minste één fout, op Hallo **Azure Active Directory** blade Selecteer **licenties** en vervolgens **overzicht**. Een info wordt weergegeven wanneer u een aantal groepen uw aandacht vereisen.

![Overzicht van informatie over groepen in de foutstatus](media/active-directory-licensing-group-problem-resolution-azure-portal/group-errors-widget.png)

4. Klik op Hallo vak toosee een lijst van alle groepen met fouten. U kunt klikken op elke groep voor meer informatie.

![Overzicht van lijst met groepen met fouten](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-groups-with-errors.png)


Hieronder volgt een beschrijving van elke potentiële probleem en Hallo manier tooresolve deze.

## <a name="not-enough-licenses"></a>Niet voldoende licenties

**Probleem:** er niet voldoende beschikbare licenties voor een Hallo producten die is opgegeven in het Hallo-groep. U moet tooeither koop meer licenties voor Hallo product of niet-gebruikte licenties van andere gebruikers of groepen vrijmaken.

toosee hoeveel licenties beschikbaar zijn, gaat u te**Azure Active Directory** > **licenties** > **alle producten**.

toosee welke gebruikers en groepen verbruiken licenties, klikt u op een product. Onder **gelicentieerde gebruikers**, ziet u alle gebruikers die direct of via een of meer groepen toegewezen licenties hebt. Onder **groepen in licentie gegeven**, ziet u alle groepen met dat product dat is toegewezen.

**PowerShell:** PowerShell-cmdlets rapporteer deze fout als _CountViolation_.

## <a name="conflicting-service-plans"></a>Conflicterende service-abonnementen

**Probleem:** een Hallo producten die is opgegeven in de groep Hallo bevat een service-abonnement dat conflicteert met een andere service-abonnement is al toegewezen toohello gebruiker via een ander product. Sommige service-abonnementen zijn geconfigureerd op een manier die ze kunnen niet worden toegewezen toohello dezelfde gebruiker die een andere gerelateerde service-abonnement.

Houd rekening met Hallo voorbeeld te volgen. Een gebruiker een licentie voor Office 365 Enterprise heeft **E1** rechtstreeks, toegewezen met alle Hallo plannen ingeschakeld. Hallo-gebruiker is toegevoegd tooa-groep met Office 365 Enterprise Hallo **E3** tooit product toegewezen. Dit product bevat service-abonnementen die elkaar niet overlappen met Hallo plannen die zijn opgenomen in E1, zodat het Hallo-groepstoewijzing licentie mislukt met fout 'Serviceplannen conflicterende' Hallo. In dit voorbeeld zijn de Hallo conflicterende service-abonnementen:

-   SharePoint Online (2 plannen) veroorzaakt een conflict met SharePoint Online (1 plannen).
-   Exchange Online (2 plannen) veroorzaakt een conflict met Exchange Online (1 plannen).

toosolve dit conflict u toodisable deze twee plannen op Hallo E1 dat rechtstreeks toegewezen toohello gebruiker licentie nodig. Of u toomodify Hallo hele groep licentietoewijzing nodig hebt en Hallo plannen in Hallo E3-licentie uitschakelen. U kunt ook tooremove Hallo E1 licentie van Hallo gebruiker besluiten als het in de context van Hallo E3 licentie Hallo redundant.

Hallo beslissing over hoe tooresolve conflicterende productlicenties altijd behoort toohello beheerder. Azure AD oplossen niet automatisch licentie conflicten.

**PowerShell:** PowerShell-cmdlets rapporteer deze fout als _MutuallyExclusiveViolation_.

## <a name="other-products-depend-on-this-license"></a>Andere producten zijn afhankelijk van deze licentie

**Probleem:** een Hallo producten die is opgegeven in de groep Hallo een serviceplan dat moet worden ingeschakeld voor een andere service-abonnement in een ander product, naar de functie bevat. Deze fout treedt op wanneer Azure AD tooremove Hallo onderliggende service-abonnement probeert. Dit kan bijvoorbeeld gebeuren als gevolg van Hallo gebruiker wordt verwijderd uit groep Hallo.

toosolve dit probleem, moet u ervoor dat Hallo vereist plan is nog steeds toegewezen toousers via een andere methode, of dat Hallo afhankelijke services zijn uitgeschakeld voor deze gebruikers toomake. Nadat u dat doet, kunt u goed Hallo groepslicentie verwijderen van deze gebruikers.

**PowerShell:** PowerShell-cmdlets rapporteer deze fout als _DependencyViolation_.

## <a name="usage-location-isnt-allowed"></a>Gebruikslocatie is niet toegestaan

**Probleem:** sommige Microsoft-services zijn niet beschikbaar op alle locaties vanwege lokale wet- en regelgeving. Voordat u een licentie tooa-gebruiker toewijzen kunt, moet u toospecify Hallo 'Gebruikslocatie'-eigenschap voor Hallo gebruiker hebben. U kunt dit doen onder Hallo **gebruiker** > **profiel** > **instellingen** sectie in hello Azure-portal.

Wanneer Azure AD tooassign een groep licentie tooa gebruiker waarvan gebruikslocatie wordt niet ondersteund probeert, wordt deze mislukt en deze fout op Hallo gebruiker registreren.

toosolve dit probleem op door gebruikers verwijderen vanaf ondersteunde locaties van de groep Hallo in licentie gegeven. Ook als Hallo huidige gebruik locatie waarden niet de werkelijke gebruikerslocatie Hallo vertegenwoordigen, kunt u ze aanpassen zodat Hallo licenties correct volgende keer zijn toegewezen (als de nieuwe locatie hello wordt ondersteund).

**PowerShell:** PowerShell-cmdlets rapporteer deze fout als _ProhibitedInUsageLocationViolation_.

> [!NOTE]
> Als Azure AD groep licenties toewijst, nemen alle gebruikers zonder een gebruikslocatie opgegeven Hallo-locatie van Hallo map. Raden wij aan dat beheerders Hallo juist gebruik waarden van de locatie van gebruikers voordat u licentiegegevens toocomply op basis van een groep met lokale wet- en regelgeving.

## <a name="what-happens-when-theres-more-than-one-product-license-on-a-group"></a>Wat gebeurt er wanneer er meer dan één productlicentie op een groep?

U kunt meer dan één product tooa licentiegroep toewijzen. Bijvoorbeeld, u kunt Office 365 Enterprise E3 toewijzen en Enterprise Mobility + Security tooa groep tooeasily alle inbegrepen services inschakelt voor gebruikers.

Azure AD probeert tooassign alle licenties die zijn opgegeven in Hallo groep tooeach gebruiker. Als Azure AD kan niet toewijzen een van de producten Hallo vanwege zakelijke logica problemen (bijvoorbeeld, als er niet voldoende licenties voor alle, of als er conflicten met andere services die zijn ingeschakeld op Hallo gebruiker zijn), het Hallo andere licenties in de groep Hallo won't toewijzen beide.

U zult kunnen toosee Hallo gebruikers die is toegewezen tooget mislukt is mislukt en welke producten zijn beïnvloed door dit selectievakje.

## <a name="license-assignment-fails-silently-for-a-user-due-tooduplicate-proxy-addresses-in-exchange-online"></a>De licentietoewijzing ongemerkt voor een gebruiker vanwege tooduplicate proxyadressen in Exchange Online

Als u Exchange Online, sommige gebruikers in uw tenant mogelijk niet juist geconfigureerd Hello dezelfde waarde voor proxy-adres. Wanneer Groepsbeleid licentieverlening tooassign een licentie toosuch een gebruiker probeert, het zal mislukken en wordt een fout niet opgenomen (in tegenstelling tot in Hallo andere foutgevallen die hierboven worden beschreven) - Dit is een beperking in Hallo preview-versie van deze functie en gaan we tooaddress het eerder  *Algemene beschikbaarheid*.

> [!TIP]
> Als u merkt dat sommige gebruikers geen licentie is ontvangen en er geen fout vastgelegd op die gebruikers is, moet u eerst controleren als er dubbele proxyadres.
> Dit kan worden gedaan door het uitvoeren van de volgende PowerShell-cmdlet op basis van Exchange Online Hallo:
```
Run Get-Recipient | where {$_.EmailAddresses -match "user@contoso.onmicrosoft.com"} | fL Name, RecipientType,emailaddresses
```
> [In dit artikel](https://support.microsoft.com/help/3042584/-proxy-address-address-is-already-being-used-error-message-in-exchange-online) bevat meer informatie over dit probleem op door met informatie over [hoe tooconnect tooExchange Online met externe PowerShell](https://technet.microsoft.com/library/jj984289.aspx).

Nadat de proxy-adres problemen zijn opgelost voor Hallo van invloed op gebruikers, moet u ervoor dat tooforce licentie verwerking op Hallo groep toomake ervoor licenties nu opnieuw kunnen worden toegepast.

## <a name="how-do-you-force-license-processing-in-a-group-tooresolve-errors"></a>Hoe u licentie worden verwerkt in een groep tooresolve fouten afdwingen?

Afhankelijk van welke stappen u tooresolve fouten hebt gemaakt, kan het benodigde toomanually trigger verwerking van de status van een groep tooupdate Hallo gebruiker zijn.

Bijvoorbeeld, als u een aantal licenties vrijgemaakt door het verwijderen van directe licentietoewijzingen van gebruikers, moet u tootrigger verwerking van groepen die eerder is mislukt toofully licentie alle leden van de gebruiker. toodo die vinden Hallo groep blade open **licenties**, en selecteer Hallo **opnieuw verwerken** knop op Hallo-werkbalk.

## <a name="next-steps"></a>Volgende stappen

toolearn meer informatie over andere scenario's voor Licentiebeheer via groepen, Hallo ziet:

* [Toewijzen van licenties tooa groep in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [Wat is licentieverlening in Azure Active Directory op basis van groep?](active-directory-licensing-whatis-azure-portal.md)
* [Hoe toomigrate afzonderlijk in licentie gegeven gebruikers licentieverlening in Azure Active Directory op basis van toogroup](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory-licentieverlening voor aanvullende scenario's op basis van groep](active-directory-licensing-group-advanced.md)
