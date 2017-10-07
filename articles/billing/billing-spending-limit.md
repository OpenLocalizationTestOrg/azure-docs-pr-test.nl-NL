---
title: Azure uitgaven aaaUnderstand beperken | Microsoft Docs
description: Hierin wordt beschreven hoe u Azure uitgavenlimiet werkt en hoe tooremove deze
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: genli
ms.openlocfilehash: ed01401a07c3d0e7edebe42fb1482b7b60b1df51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-spending-limit-and-how-tooremove-it"></a>Azure uitgavenlimiet begrijpen en hoe tooremove deze

Azure uitgavenlimiet geldt een limiet op hoeveel uw Azure-abonnement kunt besteden. Alle nieuwe klanten die zich aanmeldt voor Hallo proefabonnement of de aanbiedingen die tegoed bevat over meerdere maanden hebben Hallo uitgavenlimiet is standaard ingeschakeld. Hallo uitgavenlimiet is $0. Deze kan niet worden gewijzigd. Hallo uitgavenlimiet is niet beschikbaar voor typen abonnementen zoals betalen naar gebruik abonnementen en streven plannen. Zie Hallo [volledige lijst met Azure-aanbiedingen en beschikbaarheid van uitgavenlimiet Hallo Hallo](https://azure.microsoft.com/support/legal/offer-details/).

## <a name="what-happens-when-i-reach-hello-spending-limit"></a>Wat gebeurt er wanneer ik Hallo uitgavenlimiet bereiken?

Bij het gebruik van uw resulteert in kosten die tot uitputting van de maandelijkse bedragen Hallo opgenomen in uw aanbieding, worden Hallo-services die u hebt geïmplementeerd voor de rest Hallo van die factuurmaand uitgeschakeld. Zo worden Cloud Services die u hebt geïmplementeerd uit de productie genomen, en uw virtuele machines van Azure worden stopgezet en de toewijzing ervan ongedaan gemaakt. tooprevent uw services wordt uitgeschakeld, kunt u tooremove uw bestedingslimiet. Wanneer uw services zijn uitgeschakeld, zijn Hallo-gegevens in uw storage-accounts en -databases beschikbaar in een alleen-lezen manier voor beheerders. Aan Hallo begin Hallo volgende factuurmaand, als uw aanbieding tegoed over meerdere maanden, bevat uw abonnement niet opnieuw worden ingeschakeld. Vervolgens kunt u uw Cloud-Services implementeren en volledige toegang tooyour storage-accounts en -databases hebben.

Nadat de gratis proefabonnement Hallo Hallo uitgavenlimiet bereikt, kunt u Hallo-abonnement opnieuw inschakelen en moet automatisch [upgrade tooour met standaard aanbieding betalen naar gebruik](billing-upgrade-azure-subscription.md) binnen 90 dagen.

U ontvangt meldingen wanneer u Hallo uitgavenlimiet voor uw aanbieding bereikt. Meld u aan toohello [Azure-Accountcentrum](https://account.windowsazure.com), selecteer **ACCOUNT**, en selecteer vervolgens **abonnementen**. Er worden meldingen over abonnementen die Hallo uitgavenlimiet is bereikt.

## <a name="things-you-are-charged-for-even-if-you-have-a-spending-limit-enabled"></a>Dingen die u in rekening worden gebracht zelfs als er een bestedingslimiet ingeschakeld

Sommige Azure-services en [Marketplace-aankopen](https://azure.microsoft.com/marketplace/) kunnen worden kosten in rekening onder Hallo betalingsmethode (CC) zelfs als een bestedingslimiet is ingesteld. Voorbeelden zijn licenties voor Visual studio, Azure Active Directory premium, ondersteuningsplannen en de meeste van derden huisstijl services via Hallo Marketplace verkocht.


## <a name="when-not-toouse-hello-spending-limit"></a>Wanneer niet toouse bestedingslimiet Hallo

Hallo uitgavenlimiet kan voorkomen dat u van de implementatie van of met bepaalde marketplace en Microsoft-services. Hier volgen Hallo scenario's waarbij Hallo uitgavenlimiet voor uw abonnement moet worden verwijderd.

- U van plan bent toodeploy eerste partij afbeeldingen zoals Oracle en -services, zoals Visual Studio Team Services. In dit scenario zorgt ervoor dat u uw bestedingslimiet bijna onmiddellijk tooexceed en zorgt ervoor dat uw abonnement toobe uitgeschakeld.

- U hebt services die niet mogen worden onderbroken.

- Hebt u services en bronnen met instellingen zoals virtuele IP-die u adressen niet wilt dat toolose. Deze instellingen gaan verloren wanneer het Hallo-services en bronnen toewijzing ongedaan gemaakt.


## <a name="remove-hello-spending-limit"></a>Hallo uitgavenlimiet verwijderen

U kunt Hallo uitgavenlimiet op elk gewenst moment, zolang er een geldige betalingsmethode gekoppeld aan uw abonnement is verwijderen. Voor aanbiedingen die tegoed over meerdere maanden hebt, kunt u ook weer inschakelen Hallo uitgavenlimiet aan Hallo begin van de volgende factureringscyclus.

tooremove uw bestedingslimiet, als volgt te werk:

1. Meld u aan toohello [Azure-Accountcentrum](https://account.windowsazure.com).

2. Selecteer een abonnement.

3. Als het Hallo-abonnement is uitgeschakeld vanwege toohello bestedingslimiet wordt bereikt, klikt u op deze melding: "Abonnement Hallo bestedingslimiet bereikt en is uitgeschakeld tooprevent kosten." Klik anders op **uitgavenlimiet verwijderen** in Hallo **ABONNEMENTSSTATUS** gebied.

4. Selecteer een voor u geschikte optie.

|Optie|Effect|
|-------|-----|
|Bestedingslimiet voor onbepaalde tijd verwijderen|Hiermee verwijdert u Hallo uitgavenlimiet zonder in te schakelen deze automatisch aan begin Hallo Hallo volgende factureringsperiode.|
|Uitgavenlimiet verwijderen voor de huidige periode facturering Hallo|Hiermee verwijdert u Hallo uitgavenlimiet zodat wordt automatisch terug automatisch aan begin Hallo Hallo volgende factureringsperiode.|

## <a name="need-help-contact-support"></a>Hulp nodig? Neem contact op met ondersteuning.
Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget uw probleem snel worden opgelost.
