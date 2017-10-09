---
title: aaaConfigure meldingen en e-mailsjablonen in Azure API Management | Microsoft Docs
description: Meer informatie over hoe tooconfigure meldingen en e-mailsjablonen in Azure API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: ee25f26d-4752-433b-af9c-3817db38aed5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: dc23289c25a1641992b73cb955099b3f207b6968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-notifications-and-email-templates-in-azure-api-management"></a>Hoe tooconfigure meldingen en e-mailsjablonen in Azure API Management
API Management biedt de mogelijkheid Hallo tooconfigure meldingen voor specifieke gebeurtenissen en tooconfigure Hallo e-mailsjablonen die zijn gebruikt toocommunicate met Hallo-beheerders en ontwikkelaars van exemplaar van API Management. Dit onderwerp wordt beschreven hoe tooconfigure meldingen voor beschikbare gebeurtenissen hello, en biedt een overzicht van het configureren van e-mailsjablonen Hallo gebruikt deze gebeurtenissen.

## <a name="publisher-notifications"></a>Publisher meldingen configureren
tooconfigure meldingen, klikt u op **publicatieportal** in hello Azure-Portal voor uw API Management-service. Hiermee gaat u toohello API Management-publicatieportal.

![Publicatieportal][api-management-management-console]

> [!NOTE] 
> Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.

Klik op **meldingen** van Hallo **API Management** menu op Hallo links tooview Hallo beschikbare meldingen.

![Meldingen van de uitgever][api-management-publisher-notifications]

Hallo kan volgende lijst van gebeurtenissen die worden geconfigureerd voor meldingen.

* **Verzoeken om abonnementen (goedkeuring wordt vereist)** - Hallo opgegeven e-mailontvangers en ontvangen gebruikers e-mailmeldingen over verzoeken om abonnementen voor API-producten goedkeuring wordt vereist.
* **Nieuwe abonnementen** - Hallo opgegeven e-mailontvangers en e-mailmeldingen over nieuwe abonnementen voor API-product ontvangt de gebruiker.
* **Galerie toepassingsaanvragen** - Hallo opgegeven e-mailontvangers en gebruikers e-mailmeldingen ontvangen wanneer nieuwe toepassingen ingediend toohello-toepassingsgalerie zijn.
* **BCC** - Hallo opgegeven e-mailontvangers en blind kopie van alle e-mailberichten verzonden toodevelopers e-mailbericht ontvangt de gebruiker.
* **Nieuwe probleem of opmerking** - Hallo opgegeven e-mailontvangers en e-mailmeldingen wanneer een nieuw probleem ontvangt de gebruiker of opmerking wordt ingediend op Hallo-portal voor ontwikkelaars.
* **Account sluiten bericht** - Hallo opgegeven e-mailontvangers en gebruikers e-mailmeldingen ontvangen wanneer een account wordt gesloten.
* **Bijna abonnement quotumlimiet** - Hallo e-mailontvangers te volgen en ontvangen gebruikers e-mailmeldingen wanneer abonnement gebruik sluiten toousage quotum opgehaald.

Voor elke gebeurtenis kunt u e-mailontvangers Hallo e-mailadres tekstvak met opgeven of u gebruikers kunt kiezen uit een lijst.

toospecify Hallo e-mailadressen toobe gewaarschuwd, ze in het tekstvak voor Hallo e-mailadres invoeren. Als er meerdere e-mailadressen, scheiden met komma's.

![Geadresseerden voor meldingen][api-management-email-addresses]

toospecify hello gebruikers toobe melding ontvangt, klikt u op **ontvanger toevoegen**Hallo selectievakje naast Hallo gebruikers toobe gewaarschuwd en klikt u op **OK**.

> [!NOTE] 
> Alleen beheerders worden in Hallo lijst weergegeven.


Klik na het configureren van de ontvangers van meldingen Hallo **opslaan** tooapply Hallo bijgewerkt geadresseerden voor meldingen.

> [!NOTE] 
> Als u Hallo verlaat **Publisher meldingen** tabblad Hallo publicatieportal waarschuwt u als er niet-opgeslagen wijzigingen.


## <a name="email-templates"></a>E-mailsjablonen configureren
API Management biedt e-mailsjablonen voor Hallo e-mailberichten die worden verzonden in Hallo verloop van beheer en Hallo-service. Hallo volgende e-mailsjablonen worden geleverd.

* Toepassing galerie inzending is goedgekeurd
* Ontwikkelaars afscheidstekst letter
* Ontwikkelaars quotalimiet bijna melding
* Gebruiker uitnodigen
* Nieuwe opmerking toegevoegd tooan probleem
* Nieuwe probleem ontvangen
* Nieuw abonnement geactiveerd
* Abonnement wordt verlengd bevestigen
* Abonnementaanvraag heeft geweigerd
* Abonnementaanvraag ontvangen

Deze sjablonen kunnen worden gewijzigd naar wens.

tooview en e-mailsjablonen Hallo voor uw exemplaar van API Management configureren, klikt u op **meldingen** van Hallo **API Management** menu op Hallo links en selecteer Hallo **e-mailsjablonen**  tabblad.

![E-mailsjablonen][api-management-email-templates]

tooview of een specifieke sjabloon niet wijzigen, selecteert u deze in Hallo **sjablonen** vervolgkeuzelijst.

![E-Sjabloonlijst][api-management-email-templates-list]

Elk e-mailsjabloon heeft een onderwerp als tekst zonder opmaak en de definitie van een instantie in HTML-indeling. Elk item kan worden aangepast naar wens.

![Editor voor e-sjabloon][api-management-email-template]

Hallo **Parameters** lijst bevat een lijst met parameters, die tijdens ingevoegd in Hallo onderwerp of de hoofdtekst, vervangen Hallo aangewezen waarde wanneer Hallo e-mailbericht verzonden. een parameter tooinsert Hallo cursor waarin u wilt Hallo parameter toogo en klikt u op Hallo pijl toohello links van de parameternaam Hallo plaatsen.

Klik op **Preview** of **een test verzenden** toosee hoe Hallo e wordt zoeken of een testbericht verzenden.

> [!NOTE] 
> Hallo-parameters zijn niet vervangen door feitelijke waarden wanneer een voorbeeldweergave of een test verzenden.

toosave hello wijzigingen toohello e-mailsjabloon, klikt u op **opslaan**, of toocancel Hallo wijzigingen, klikt u op **annuleren**.
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
