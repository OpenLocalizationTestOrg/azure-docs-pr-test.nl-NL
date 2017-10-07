---
title: Rapportage van Azure Active Directory automatisch gebruikersaccount inrichten tooSaaS toepassingen | Microsoft Docs
description: Meer informatie over hoe toocheck Hallo status van automatische gebruikersaccount inrichten en hoe tootroubleshoot Hallo inrichting van afzonderlijke gebruikers.
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: asmalser-msft
ms.openlocfilehash: 5dcf9e5dbaacf3a2c81183c5d81e331858671b86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-reporting-on-automatic-user-account-provisioning"></a>Zelfstudie: Rapportage over automatische gebruikers account inrichten


Azure Active Directory bevat een [gebruikersaccount-service inricht](active-directory-saas-app-provisioning.md) die helpt om Hallo inrichting ongedaan van de inrichting van gebruikersaccounts in de SaaS-apps en andere systemen, Hallo doel-end-to-end-identity lifecycle automatiseren beheer. Azure AD biedt ondersteuning voor vooraf geïntegreerde gebruikers inrichten van connectors voor alle Hallo toepassingen en systemen in de sectie 'Aanbevolen' Hallo Hallo [Azure AD-toepassingsgalerie](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured).

Dit artikel wordt beschreven hoe toocheck Hallo status van inrichting nadat ze zijn ingesteld, en taken tootroubleshoot Hallo inrichting van afzonderlijke gebruikers en groepen.

## <a name="overview"></a>Overzicht

Inrichting connectors zijn voornamelijk ingesteld en geconfigureerd met behulp van Hallo [Azure-beheerportal](https://portal.azure.com), door de volgende Hallo [documentatie opgegeven](active-directory-saas-tutorial-list.md) voor Hallo-toepassing waarbij gebruikersaccount inrichten gewenst is. Zodra de geconfigureerde en actieve worden inrichten voor een toepassing gerapporteerd over het gebruik van een van twee methoden:

* **Azure-beheerportal** -in dit artikel beschrijft voornamelijk bij het ophalen van rapportgegevens uit Hallo [Azure-beheerportal](https://portal.azure.com), waarmee u zowel een overzichtsrapport inrichten als gedetailleerde inrichten controlelogboeken voor een bepaalde toepassing.

* **Audit API** -Azure Active Directory biedt ook een Audit API schakelt programmatische voor het ophalen van Hallo inrichting gedetailleerde controlelogboeken. Zie [Azure Active Directory-audit API-referentiemateriaal](active-directory-reporting-api-audit-reference.md) voor specifieke toousing documentatie deze API. Terwijl dit artikel niet specifiek hoe toouse API hello omvat, het Hallo typen gebeurtenissen die zijn vastgelegd in het controlelogboek Hallo inrichting toegelicht.

### <a name="definitions"></a>Definities

In dit artikel maakt gebruik van Hallo termen, zoals hieronder gedefinieerd, te volgen:

* **Bronsysteem** -Hallo-opslagplaats voor gebruikers die Azure AD-inrichting service Hallo synchroniseert uit. Azure Active Directory is het bronsysteem Hallo voor Hallo meerderheid van de vooraf geïntegreerde connectors inrichting, zijn echter enkele uitzonderingen (voorbeeld: Workday inkomende synchronisatie).

* **Doelsysteem** -opslagplaats van gebruikers die Azure AD-inrichting service Hallo Hallo synchroniseert op. Dit is doorgaans een SaaS-toepassing (voorbeelden: Salesforce, ServiceNow, Google Apps, Dropbox voor bedrijven), maar in sommige gevallen kan een on-premises systeem, zoals Active Directory (voorbeeld: Workday inkomende synchronisatie tooActive Directory).


## <a name="getting-provisioning-reports-from-hello-azure-management-portal"></a>Inrichting van rapporten van hello Azure-beheerportal ophalen

tooget rapport Inrichtingsgegevens voor een bepaalde toepassing starten door het starten van Hallo [Azure-beheerportal](https://portal.azure.com) en bladeren door toohello bedrijfstoepassing waarvoor inrichting is geconfigureerd. Als u gebruikers tooLinkedIn uitbreiden inricht, is bijvoorbeeld Hallo navigatie pad toohello App-details:

**Azure Active Directory > bedrijfstoepassingen > alle toepassingen > LinkedIn uitbreiden**

Hier kunt u toegang hebt tot het overzichtsrapport voor Hallo inrichten en inrichting controlelogboeken Hallo, beide die hieronder worden beschreven.


### <a name="provisioning-summary-report"></a>Het overzichtsrapport voor inrichting

Hallo overzichtsrapport inrichting is zichtbaar in Hallo **inrichten** tabblad voor de opgegeven toepassing. Bevindt het zich in de sectie van de informatie over de synchronisatie Hallo onder **instellingen**, en biedt de volgende informatie Hallo:

* Hallo totaal aantal gebruikers en groepen op die zijn gesynchroniseerd en zijn momenteel in het bereik voor het inrichten van tussen Hallo bronsysteem en Hallo doelsysteem.

* Hallo laatste tijd Hallo synchronisatie is uitgevoerd. Synchronisaties optreden doorgaans elke 20-40 minuten nadat een volledige synchronisatie is voltooid.

* Of er een initiële volledige synchronisatie is voltooid.

* Wel of niet Hallo inrichtingsproces in quarantaine zijn geplaatst en welke Hallo reden voor de status van de quarantaine Hallo is bijvoorbeeld (fout toocommunicate met doelsysteem vanwege tooinvalid beheerdersreferenties)

Hallo inrichting overzichtsrapport moet Hallo eerste plaats admins uiterlijk toocheck op de operationele status van de taak Hallo Hallo.

 ![Het overzichtsrapport voor](./media/active-directory-saas-provisioning-reporting/summary_report.PNG)

### <a name="provisioning-audit-logs"></a>Inrichting controlelogboeken
Alle activiteiten uitgevoerd door Hallo-service inricht worden vastgelegd in de controlelogboeken hello Azure AD, die kunnen worden bekeken in Hallo **controlelogboeken** tabblad onder Hallo **Account inrichten** categorie. Geregistreerde activiteit gebeurtenistypen zijn onder andere:

* **Gebeurtenissen importeren** -telkens inrichting hello Azure AD-service informatie over een afzonderlijke gebruiker of groep uit een bronsysteem of doelsysteem haalt wordt een 'import' gebeurtenis vastgelegd. Tijdens de synchronisatie worden gebruikers opgehaald uit het bronsysteem Hallo eerst met Hallo resultaten als 'importeren' gebeurtenissen vastgelegd. Hallo overeenkomende id's van gebruikers Hallo opgehaald worden vervolgens een query uitgevoerd op Hallo doel system toocheck indien aanwezig, met Hallo resultaten ook vastgelegd als 'importeren' gebeurtenissen. Deze gebeurtenissen opnemen alle toegewezen gebruikerskenmerken en hun waarden die zijn zichtbaar voor inrichting hello Azure AD-service bij Hallo Hallo gebeurtenis. 

* **Synchronisatie regel gebeurtenissen** - deze gebeurtenissen rapporteert over Hallo resultaten van de toewijzingsregels Hallo-kenmerk en een bereik filters geconfigureerd nadat gebruikersgegevens is geïmporteerd en geëvalueerd op basis van Hallo bron en doel-systemen. Bijvoorbeeld, als een gebruiker in een bronsysteem wordt geacht toobe binnen het bereik van de inrichting en veronderstelde toonot aanwezig zijn in het doelsysteem hello, worden vervolgens deze gebeurtenis legt vast dat Hallo gebruiker ingericht in het doelsysteem Hallo. 

* **Gebeurtenissen exporteren** -een "export" gebeurtenis vastgelegd elke keer inrichting hello Azure AD-service een gebruiker of de groep object tooa doelsysteem schrijft. Deze gebeurtenissen opnemen alle gebruikerskenmerken en hun waarden die zijn geschreven Hallo inrichting Azure AD-service op Hallo moment van Hallo-gebeurtenis. Als er een fout opgetreden is tijdens het schrijven van Hallo gebruiker account of groep object toohello doelsysteem, wordt deze hier weergegeven.

* **Escrow gebeurtenissen verwerken** -proces borgen optreden wanneer hello inrichten service een fout aangetroffen tijdens een poging een bewerking en activiteiten in een interval van back-off Hallo tijd tooretry begint. Telkens wanneer die een inrichtingsbewerking buiten gebruik werd gesteld, wordt een 'escrow' gebeurtenis vastgelegd.

Wanneer inrichting gebeurtenissen voor een afzonderlijke gebruiker bekijkt, Hallo normaal gebeurtenissen in deze volgorde:

1. Importeren van gebeurtenis: gebruiker wordt opgehaald uit het bronsysteem Hallo.

2. Importeren van gebeurtenis: doelsysteem is van de query toocheck Hallo bestaan van de gebruiker Hallo opgehaald.

3. Regel synchronisatiegebeurtenis: gebruikersgegevens van de bron en doel-systemen worden geëvalueerd op basis van Hallo geconfigureerd kenmerk mapping regels en filters toodetermine scoping welke actie, indien van toepassing, moet worden uitgevoerd.

4. Gebeurtenis exporteren: als de regel synchronisatiegebeurtenis Hallo bepaald dat een actie moet worden uitgevoerd (bijvoorbeeld toevoegen, bijwerken, verwijderen), en vervolgens Hallo resultaten van Hallo actie worden vastgelegd in een Export-gebeurtenis.

![Een Azure AD-testgebruiker maken](./media/active-directory-saas-provisioning-reporting/audit_logs.PNG)


### <a name="looking-up-provisioning-events-for-a-specific-user"></a>Opzoeken van de inrichting van gebeurtenissen voor een specifieke gebruiker

Hallo is meest voorkomende gebruiksvoorbeeld voor Hallo controlelogboeken inrichting toocheck Hallo status van een afzonderlijk gebruikersaccount inrichten. toolook hello laatste inrichting gebeurtenissen voor een specifieke gebruiker:

1. Ga toohello **controlelogboeken** sectie.

2. Van Hallo **categorie** selecteert u **Account inrichten**.

3. In Hallo **datumbereik** menu, selecteer Hallo datumbereik dat u wilt dat toosearch,

4. In Hallo **Search** balk, Hallo gebruikersnaam invoeren van Hallo gebruiker gewenste toosearch voor. Hallo-indeling van de id-waarde moet overeenkomen met wat u hebt geselecteerd als primaire overeenkomende ID in Hallo kenmerk toewijzingsconfiguratie (bijvoorbeeld userPrincipalName of werknemer-ID-nummer) Hallo. Hallo id-waarde is vereist, zijn zichtbaar in Hallo doel(en) kolom.

5. Druk op Enter toosearch. meest recente gebeurtenissen inrichting Hallo eerst geretourneerd.

6. Als er gebeurtenissen zijn geretourneerd, houd er rekening mee Hallo activiteitstypen en of ze is geslaagd of mislukt. Als er geen resultaten worden geretourneerd, dan betekent dit dat Hallo gebruiker bestaat niet, of nog niet is gedetecteerd door Hallo inrichtingsproces als een volledige synchronisatie is nog niet voltooid.

7. Klik op afzonderlijke gebeurtenissen tooview uitgebreide informatie, zoals de alle eigenschappen van de gebruiker die zijn opgehaald, geëvalueerd of als onderdeel van de gebeurtenis Hallo geschreven.


### <a name="tips-for-viewing-hello-provisioning-audit-logs"></a>Tips voor het weergeven van Hallo controlelogboeken inrichten

Selecteer voor de beste leesbaarheid in hello Azure-portal Hallo **kolommen** knop en kies deze kolommen:

* **Datum** -toont Hallo Hallo gebeurtenis is opgetreden.
* **Doel(en)** -Hallo-app en gebruikers-ID die Hallo onderwerpen van Hallo gebeurtenis bevat.
* **Activiteit** -Hallo activiteitstype, zoals eerder beschreven.
* **Status** - of Hallo gebeurtenis is voltooid of niet.
* **Statusreden** -een overzicht van wat is er gebeurd in Hallo gebeurtenis inrichten.


## <a name="troubleshooting"></a>Problemen oplossen

Hallo inrichting samenvatting rapport en audit logboeken spelen een belangrijke rol helpen beheerders verschillende gebruikersaccount inrichten problemen oplossen.

Voor instructies voor het scenario's gebaseerde tootroubleshoot automatisch gebruikers inrichten, Zie [problemen bij het configureren en inrichten van gebruikers tooan toepassing](active-directory-application-provisioning-content-map.md).


## <a name="additional-resources"></a>Aanvullende resources

* [Het beheren van gebruikers account inrichten voor zakelijke Apps](active-directory-enterprise-apps-manage-provisioning.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
