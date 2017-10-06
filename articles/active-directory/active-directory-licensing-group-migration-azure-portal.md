---
title: aaaHow toomigrate uw afzonderlijke gelicentieerde gebruikers tooa groeperen in Azure Active Directory | Microsoft Docs
description: Hoe tooswitch van afzonderlijke gebruiker licenties toogroup gebaseerde licentieverlening met Azure Active Directory
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
ms.openlocfilehash: 25e5c760b7e632ba71edde10d937fe580aa6ed35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-licensed-users-tooa-group-for-licensing-in-azure-active-directory"></a>Hoe tooadd licentie gegeven tooa gebruikersgroep voor licentieverlening in Azure Active Directory

Mogelijk hebt u bestaande licenties geïmplementeerd toousers Hallo organisaties via 'rechtstreekse toewijzing'; dat wil zeggen, gebruikt PowerShell-scripts of andere hulpprogramma's voor tooassign afzonderlijke gebruikerslicenties. Als u toostart gebruikt licentieverlening toomanage-licenties op basis van een groep in uw organisatie dat wilt, moet u een migratie plan tooseamlessly vervangen door bestaande oplossingen op basis van een groep licenties.

Hallo belangrijkste ding tookeep rekening is dat u een situatie waarin migreren op basis van toogroup licentieverlening leidt ertoe dat gebruikers tijdelijk verlies van de momenteel toegewezen licenties moet voorkomen. Elke proces dat tot de verwijdering van de licenties leiden kan moet worden vermeden tooremove Hallo risico's van gebruikers die toegang tooservices en de bijbehorende gegevens verliezen.

## <a name="recommended-migration-process"></a>Aanbevolen migratieproces

1. U hebt bestaande automatisering (bijvoorbeeld PowerShell) voor het beheren van de licentietoewijzing en verwijderen voor gebruikers. Laat het actief is.

2. Maak een nieuwe groep in de licentieverlening (of bepalen welke bestaande groepen toouse) en zorg ervoor dat alle vereiste dat gebruikers worden toegevoegd als leden.

3. Licenties toe te wijzen Hallo vereist toothose groepen; Hallo tooreflect moet uw doel zijn hetzelfde licentieverlening staat uw bestaande automatisering (bijvoorbeeld PowerShell) toepast toothose gebruikers.

4. Controleer of de licenties zijn toegepaste tooall gebruikers in deze groepen. Dit kan worden gedaan door het controleren van de verwerkingsstatus Hallo op elke groep en door te controleren van controlelogboeken.

  - Kunt u afzonderlijke gebruikers controle door te kijken hun licentiegegevens. U ziet dat ze hebben dezelfde licenties toegewezen 'rechtstreeks' en 'overgenomen' Hallo van groepen.

  - U kunt een PowerShell-script te uitvoeren[controleren hoe licenties zijn toegewezen en toousers](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).

  - Wanneer hello dezelfde productlicentie is toegewezen toohello gebruiker zowel direct als door een groep, wordt slechts één licentie verbruikt door Hallo-gebruiker. Er zijn geen aanvullende licenties daarom vereist tooperform migratie.

5. Controleer of dat er geen licentietoewijzingen niet door het controleren van elke groep voor gebruikers in een foutstatus. Zie voor meer informatie [identificeren en oplossen van licentieproblemen met een voor een groep](active-directory-licensing-group-problem-resolution-azure-portal.md).

6. Houd rekening met het oorspronkelijke direct toewijzingen Hallo; verwijderen u kunt toodo geleidelijk in 'golven', toomonitor resultaat op een subset van gebruikers eerst Hallo.

  U kan Hallo oorspronkelijke direct toewijzingen op laat gebruikers, maar wanneer Hallo gebruikers hun licentiegroepen ze nog steeds behoudt verlaten Hallo oorspronkelijke-licentie is mogelijk niet wilt dat u wilt.

## <a name="an-example"></a>Een voorbeeld

We hebben een organisatie met 1000 gebruikers. Alle gebruikers vereisen Enterprise Mobility + Security (EMS)-licenties. 200 gebruikers zijn in de afdeling Financiën Hallo en Office 365 Enterprise E3-licenties vereist. We hebben een PowerShell-script met on-premises toevoegen en verwijderen van licenties van gebruikers als ze worden geleverd en gaat. We willen tooreplace Hallo script dat op basis van een groep zodat de licenties worden automatisch beheerd door Azure AD-licentieverlening.

Hier wordt het migratieproces van welke Hallo kan uitzien als:

1. Met behulp van Azure portal toewijzen Hallo EMS-licentie toohello Hallo **alle gebruikers** groep in Azure AD. Hallo E3 licentie toohello toewijzen **de afdeling financiën** groep met alle gebruikers van Hallo vereist.

2. Bevestig dat de licentietoewijzing is voltooid voor alle gebruikers voor elke groep. Ga toohello blade voor elke groep, selecteer **licenties**, en controleer verwerkingsstatus Hallo Hallo boven aan het Hallo **licenties** blade.

  - Zoek voor 'laatste licentie wijzigingen zijn toegepast tooall gebruikers' tooconfirm verwerking is voltooid.

  - Zoek naar een melding op de voorgrond over alle gebruikers voor wie licenties mogelijk niet met succes is toegewezen. Heeft we uitgevoerd buiten de licenties voor sommige gebruikers? Beschikt over sommige gebruikers conflicterende licentie-SKU's die voorkomen dat ze groep licenties overnemen?

3. Positie Controleer sommige gebruikers tooverify die ze hebben Hallo direct zowel groep licenties die zijn toegepast. Ga toohello blade voor een gebruiker, schakelt **licenties**, en bekijk het Hallo-status van licenties.

  - Dit is Hallo verwacht de status van gebruiker tijdens de migratie:

      ![verwachte gebruikersstatus](media/active-directory-licensing-group-migration-azure-portal/expected-user-state.png)

  Hiermee bevestigt u dat die Hallo de gebruiker heeft direct en overgenomen licenties. Zien we dat beide **EMS** en **E3** zijn toegewezen.

  - Selecteer de details van elke licentie tooshow over services Hallo ingeschakeld. Dit kan gebruikte toocheck zijn als hello direct- en groep licenties inschakelen exact dezelfde serviceniveaus voor de gebruiker Hallo Hallo.

      ![Controleer de service-abonnementen](media/active-directory-licensing-group-migration-azure-portal/check-service-plans.png)

4. Nadat is bevestigd dat direct en groep licenties equivalent zijn, kunt u beginnen door directe licenties van gebruikers te verwijderen. U kunt dit testen door deze te verwijderen voor afzonderlijke gebruikers in Hallo-portal en voer vervolgens automation scripts toohave die ze bulksgewijs verwijderd. Hier volgt een voorbeeld van dezelfde gebruiker met directe Hallo-licenties worden verwijderd via de portal Hallo Hallo. U ziet dat de licentiestatus Hallo ongewijzigd blijft, maar niet meer we direct toewijzingen zien.

  ![directe licenties die zijn verwijderd](media/active-directory-licensing-group-migration-azure-portal/direct-licenses-removed.png)


## <a name="next-steps"></a>Volgende stappen

toolearn meer informatie over andere scenario's voor Licentiebeheer via groepen, lezen

* [Toewijzen van licenties tooa groep in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [Wat is licentieverlening in Azure Active Directory op basis van groep?](active-directory-licensing-whatis-azure-portal.md)
* [Opsporen en oplossen van licentieproblemen met een voor een groep in Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Azure Active Directory-licentieverlening voor aanvullende scenario's op basis van groep](active-directory-licensing-group-advanced.md)
