---
title: 'Azure AD Connect: Inzicht in declaratieve inrichting | Microsoft Docs'
description: Legt uit Hallo declaratieve inrichting configuratiemodel in Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: cfbb870d-be7d-47b3-ba01-9e78121f0067
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f11e078f0aafacf94d69f0726ae41629a8470336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning"></a>Azure AD Connect-synchronisatie: inzicht declaratieve inrichting
Dit onderwerp wordt uitgelegd Hallo configuratiemodel in Azure AD Connect. Hallo model heet declaratieve inrichting en kunt u een configuratiewijziging met gemak toomake. Groot aantal dingen beschreven in dit onderwerp zijn geavanceerde en niet vereist voor de meeste scenario's van klanten.

## <a name="overview"></a>Overzicht
Declaratieve inrichting is verwerken van objecten die binnenkomen vanaf een verbonden bronmap en bepaalt hoe Hallo object en kenmerken van een bron tooa doel moeten worden omgezet. Een object in een pijplijn synchronisatie wordt verwerkt en Hallo pijplijn wordt dezelfde Hallo voor regels voor binnenkomend en uitgaand. Een inkomende regel is van een connector ruimte toohello metaverse en een uitgaande regel afkomstig is van Hallo metaverse tooa connectorgebied overgebracht.

![Synchronisatie-pipeline](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/sync1.png)  

Hallo pipeline heeft verschillende andere modules. Elk criterium is verantwoordelijk voor één concept in object-synchronisatie.

![Synchronisatie-pipeline](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/pipeline.png)  

* Bron, het bronobject Hallo
* [Bereik](#scope), vindt u alle synchronisatie-regels die in het bereik
* [Deelnemen aan](#join), bepaalt de relatie tussen connectorruimte en metaverse
* [Transformeren](#transform), berekent hoe kenmerken moeten worden omgezet en stroom
* [Prioriteit](#precedence), conflicterende kenmerk bijdragen wordt omgezet
* Doel, Hallo doelobject

## <a name="scope"></a>Bereik
Hallo bereik module evalueert een object en bepaalt Hallo-regels die in het bereik en moeten worden opgenomen in het Hallo-verwerking. Synchronisatie van andere regels zijn afhankelijk van de waarden van de Hallo kenmerken op Hallo-object, geëvalueerde toobe binnen het bereik. Een uitgeschakelde gebruiker geen Exchange-postvak heeft bijvoorbeeld andere regels dan een ingeschakelde gebruiker met een postvak.  
![Bereik](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/scope1.png)  

Hallo-bereik is gedefinieerd als groepen en componenten. Hallo-componenten zijn in een groep. Een logische en wordt gebruikt tussen alle componenten in een groep. Bijvoorbeeld: (afdeling = IT en land = Denemarken). Een logische OR wordt gebruikt tussen groepen.

![Bereik](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/scope2.png)  
Hallo-bereik in deze afbeelding moet worden gelezen als (afdeling = IT en land = Denemarken) of (land = Zweden). Als groep 1 of groep 2 geëvalueerde tootrue is, wordt de Hallo regel in het bereik.

Hallo bereik module biedt ondersteuning voor Hallo bewerkingen te volgen.

| Bewerking | Beschrijving |
| --- | --- |
| GELIJK, NOTEQUAL |Het vergelijken van een tekenreeks die wordt geëvalueerd als de waarde is gelijk toohello waarde in het Hallo-kenmerk. Zie ISIN en ISNOTIN voor kenmerken met meerdere waarden. |
| LESSTHAN, LESSTHAN_OR_EQUAL |Een tekenreeks vergelijken die wordt geëvalueerd als de waarde is minder dan Hallo-waarde in het Hallo-kenmerk. |
| BEVAT, NOTCONTAINS |Het vergelijken van een tekenreeks die wordt geëvalueerd als waarde kan worden gevonden ergens in de waarde in het Hallo-kenmerk. |
| STARTSWITH, NOTSTARTSWITH |Het vergelijken van een tekenreeks die wordt geëvalueerd als waarde in Hallo begin van Hallo-waarde in het Hallo-kenmerk. |
| ENDSWITH, NOTENDSWITH |Het vergelijken van een tekenreeks die wordt geëvalueerd als waarde in Hallo einde van Hallo-waarde in het Hallo-kenmerk. |
| GROTER DAN, GREATERTHAN_OR_EQUAL |Het vergelijken van een tekenreeks die wordt geëvalueerd als waarde groter dan van Hallo-waarde in het Hallo-kenmerk is. |
| ISNULL, ISNOTNULL |Evalueert als Hallo-kenmerk ontbreekt uit het Hallo-object. Als Hallo-kenmerk is niet aanwezig en daarom is null, wordt de Hallo regel in het bereik. |
| ISIN, ISNOTIN |Evalueert als Hallo-waarde aanwezig zijn in het kenmerk Hallo gedefinieerd. Deze bewerking is Hallo met meerdere waarden variatie gelijk en NOTEQUAL. Hallo-kenmerk moet een kenmerk met meerdere waarden toobe en als Hallo-waarde kan worden gevonden in een van de kenmerkwaarden hello, vervolgens Hallo regel in het bereik. |
| ISBITSET, ISNOTBITSET |Evalueert als een bepaalde bit is ingesteld. Bijvoorbeeld, kan worden gebruikt tooevaluate Hallo bits in userAccountControl toosee als een gebruiker is ingeschakeld of uitgeschakeld. |
| ISMEMBEROF, ISNOTMEMBEROF |Hallo-waarde moet een groep DN tooa in Hallo connectorruimte bevatten. Als het Hallo-object is lid van het Hallo-groep die is opgegeven, is het Hallo-regel binnen het bereik. |

## <a name="join"></a>Koppelen
Hallo join-module in Hallo sync pijplijn is verantwoordelijk voor het Hallo-relatie tussen het Hallo-object in de Hallo bron en een object zoeken in Hallo doel. Deze relatie zou een object in een connectorruimte om een relatie-object tooan in Hallo metaverse te vinden zijn in een inkomende regel.  
![Deelnemen aan tussen cs en mv](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join1.png)  
Hallo doel toosee als er nog een object in de metaverse hello, gemaakt door een andere Connector is, moet worden gekoppeld. Bijvoorbeeld in een account-resource forest Hallo gebruiker uit het accountforest Hallo moet lid zijn van met Hallo gebruiker van Hallo bron-forest.

Joins grotendeels op binnenkomende regels toojoin connector ruimte objecten samen toohello worden gebruikt dezelfde metaverse-object.

Hallo joins zijn gedefinieerd als een of meer groepen. U hebt componenten in een groep. Een logische en wordt gebruikt tussen alle componenten in een groep. Een logische OR wordt gebruikt tussen groepen. Hallo groepen worden in volgorde van de bovenste toobottom verwerkt. Als één groep exact één overeenkomst met een object in Hallo doel gevonden is, worden geen andere regels voor lid worden geëvalueerd. Als nul of meer dan één object is gevonden, blijft verwerking van de volgende groep toohello van regels. Om deze reden moeten Hallo regels worden gemaakt in Hallo volgorde van meest expliciete eerste en meer fuzzy Hallo achter.  
![Lid worden van definitie](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join2.png)  
Hallo joins in deze afbeelding worden van bovenste toobottom verwerkt. Eerste Hallo sync pijplijn ziet als er een overeenkomst op werknemer-id is. Als dat niet het geval is, de tweede regel Hallo ziet als Hallo accountnaam gebruikte toojoin Hallo objecten samen kan worden. Als dit niet overeen met ofwel, is Hallo derde regel meer algoritmecode door Hallo-naam van gebruiker.

Als alle join-regels zijn geëvalueerd en niet exact overeen met één is, Hallo **koppelingstype** op Hallo **beschrijving** pagina wordt gebruikt. Als deze optie is ingesteld, te**inrichten**, wordt een nieuw object in Hallo doel gemaakt.  
![Inrichten of join](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join3.png)  

Een object mag alleen één enkele synchronisatieregel met join regels binnen het bereik hebben. Als er meerdere synchronisatie-regels waarvoor join is gedefinieerd, wordt er een fout optreedt. Prioriteit is niet gebruikte tooresolve join conflicten. Een object moet een join-regel hebben binnen het bereik van kenmerken tooflow Hello dezelfde binnenkomend en uitgaand richting. Als u tooflow moet zowel binnenkomende als uitgaande toohello kenmerken hetzelfde object, moet u een inkomende en een synchronisatieregel voor uitgaande met join hebben.

Uitgaande join is een speciaal gedrag bij een poging tooprovision een object tooa doel connectorgebied overgebracht. Hallo DN-kenmerk is gebruikte toofirst probeer een reverse-join. Als er al een object in de Hallo doel connectorruimte met Hallo dezelfde DN-naam, de Hallo objecten zijn gekoppeld.

Hallo join module wordt alleen beoordeeld zodra wanneer een nieuwe synchronisatieregel in het bereik komt. Wanneer een object is gekoppeld, is het niet verwijderen zelfs als Hallo join criteria niet meer wordt voldaan. Als u een object toodisjoin wilt, moet Hallo synchronisatieregel die lid Hallo objecten buiten het bereik vallen.

### <a name="metaverse-delete"></a>Metaverse verwijderen
Metaverse-object blijft zolang er is een synchronisatieregel binnen het bereik met **koppelingstype** instellen te**inrichten** of **StickyJoin**. Een StickyJoin wordt gebruikt wanneer een Connector is niet toegestaan voor tooprovision een nieuwe toohello metaverse-object, maar wanneer deze is gekoppeld, moet worden verwijderd in de Hallo bron voordat Hallo metaverse-object is verwijderd.

Wanneer een metaverse-object is verwijderd, alle objecten gekoppeld met een synchronisatieregel voor uitgaande gemarkeerd voor **inrichten** zijn gemarkeerd voor verwijderen.

## <a name="transformations"></a>Transformaties
Hallo transformaties zijn gebruikte toodefine hoe kenmerken van Hallo bron toohello doel stromen moeten. Hallo stromen kunnen hebben een van de volgende Hallo **stromen typen**: directe, constante of -expressie. Een directe stroom loopt een kenmerkwaarde als-is met geen extra transformaties. Een constante waarde sets Hallo waarde opgegeven. Een expressie Hallo declaratieve inrichting expressie taal tooexpress hoe Hallo transformatie moet worden gebruikt. Hallo details voor Hallo expressietaal kan worden gevonden in Hallo [begrijpen declaratieve inrichting expressietaal](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) onderwerp.

![Inrichten of join](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/transformations1.png)  

Hallo **eenmaal toepassen** selectievakje definieert die Hallo kenmerk moet alleen worden ingesteld wanneer het Hallo-object in eerste instantie is gemaakt. Deze configuratie kan bijvoorbeeld gebruikte tooset een eerste wachtwoord voor een nieuwe gebruikersobject.

### <a name="merging-attribute-values"></a>Kenmerkwaarden samenvoegen
In Hallo kenmerkstromen is er een instelling toodetermine als kenmerken met meerdere waarden moeten worden samengevoegd met verschillende andere connectoren. Hallo-standaardwaarde is **Update**, wat aangeeft dat deze synchronisatieregel Hallo met de hoogste prioriteit moet win.

![Typen samenvoegen](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/mergetype.png)  

Er is ook **samenvoegen** en **MergeCaseInsensitive**. Deze opties kunnen u toomerge waarden van verschillende bronnen. Het kan bijvoorbeeld zijn dat gebruikte toomerge Hallo lid of proxyAddresses kenmerk uit diverse verschillende forests. Als u deze optie gebruikt, alle regels in het bereik synchroniseren voor een object Hallo gebruikmaken van hetzelfde type samenvoeging. U kunt geen definiëren **Update** van één Connector en **samenvoegen** van een andere. Als u probeert, ontvangt u een fout opgetreden.

verschil tussen Hallo **samenvoegen** en **MergeCaseInsensitive** is hoe tooprocess dubbele kenmerkwaarden. Hallo synchronisatie-engine zorgt u er dubbele waarden zijn niet ingevoegd in Hallo target-kenmerk. Met **MergeCaseInsensitive**, dubbele waarden met alleen een verschil in geval zullen toobe aanwezig. Bijvoorbeeld, niet ziet u beide 'SMTP:bob@contoso.com'en'smtp:bob@contoso.com' in hello target-kenmerk. **Samenvoegen** is alleen bekijkt hello exacte en meerdere waarden waarbij er alleen een verschil in kan de aanvraag aanwezig zijn.

Hallo optie **vervangen** is gelijk aan Hallo **Update**, maar wordt niet gebruikt.

### <a name="control-hello-attribute-flow-process"></a>Hallo kenmerk stroom proces
Wanneer meerdere regels voor binnenkomende synchronisatie geconfigureerde toocontribute toohello zijn dezelfde metaverse-kenmerk en vervolgens voorrang gebruikte toodetermine Hallo winnaar is. Hallo synchronisatieregel met de hoogste prioriteit (laagste numerieke waarde) gaat toocontribute Hallo waarde. Hallo die dezelfde voor uitgaande regels gebeurt. Hallo synchronisatieregel met de hoogste prioriteit wins en bijdragen Hallo waarde toohello gekoppelde adreslijst.

In sommige gevallen, in plaats van een waarde bijdragen moet Hallo synchronisatieregel bepalen hoe de andere regels zich moeten gedragen. Er zijn enkele speciale letterlijke waarden voor deze aanvraag.

Voor binnenkomende synchronisatieregels Hallo letterlijke **NULL** gebruikte tooindicate dat Hallo-stroom geen waarde toocontribute heeft kan zijn. Een andere regel met een lagere prioriteit kan een waarde bijdragen. Als er geen regel een waarde bijgedragen, vervolgens Hallo metaverse-kenmerk wordt verwijderd. Voor een uitgaande regel als **NULL** Hallo uiteindelijke waarde nadat alle regels voor synchronisatie is verwerkt, wordt vervolgens Hallo-waarde in de gekoppelde adreslijst Hallo is verwijderd.

Hallo letterlijke **AuthoritativeNull** lijkt te**NULL** echter Hallo verschil dat geen prioriteitsregels met lagere een waarde kunnen bijdragen.

Een kenmerkstroom kunt **IgnoreThisFlow**. Het is vergelijkbaar tooNULL in Hallo zin dat deze aangeeft dat er is niets toocontribute. Hallo verschil is dat wordt niet verwijderd een al bestaande waarde in Hallo doel. Het lijkt dan Hallo kenmerkstroom is nooit er.

Hier volgt een voorbeeld:

In *uit tooAD - gebruiker Exchange hybride* Hallo na stroom kan worden gevonden:  
`IIF([cloudSOAExchMailbox] = True,[cloudMSExchSafeSendersHash],IgnoreThisFlow)`  
Deze expressie moet worden gelezen als: bij Hallo gebruikerspostvak bevindt zich in Azure AD, vervolgens Hallo-kenmerk van Azure AD tooAD stromen. Als dit niet het geval is, loopt u alles back tooActive Directory niet terug. In dit geval zou het Hallo bestaande waarde in AD behouden.

### <a name="importedvalue"></a>ImportedValue
Hallo-functie ImportedValue is anders dan alle andere functies sinds Hallo kenmerknaam aanhalingstekens in plaats van vierkante haken tussen moet:  
`ImportedValue("proxyAddresses")`.

Meestal tijdens synchronisatie gebruikt een kenmerk Hallo verwachtingswaarde, zelfs als deze nog nog niet zijn uitgevoerd of is een fout ontvangen tijdens het exporteren ('top van Hallo tower'). Een inkomende synchronisatie wordt ervan uitgegaan dat een kenmerk dat nog niet is bereikt een gekoppelde adreslijst uiteindelijk wordt bereikt. In sommige gevallen is het belangrijk tooonly synchroniseren een waarde die is bevestigd door de gekoppelde adreslijst hello ('hologram en delta-tower importeren').

Een voorbeeld van deze functie kunt u vinden in Hallo out-of-box Synchronisatieregel *In uit Active Directory-gebruiker algemene vanuit Exchange*. In hybride Exchange moet Hallo waarde toegevoegd door de Exchange online alleen worden gesynchroniseerd wanneer deze is bevestigd Hallo-waarde is geëxporteerd:  
`proxyAddresses` <- `RemoveDuplicates(Trim(ImportedValue("proxyAddresses")))`

## <a name="precedence"></a>Prioriteit
Wanneer verschillende synchronisatie regels probeert toocontribute Hallo hetzelfde kenmerk waarde toohello doel, Hallo prioriteitswaarde gebruikte toodetermine Hallo winnaar is. Hallo regel met de hoogste prioriteit, de laagste numerieke waarde gaat toocontribute Hallo kenmerk in een conflict.

![Typen samenvoegen](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/precedence1.png)  

Deze volgorde kan worden gebruikt toodefine nauwkeurigere stromen voor een kleine subset van objecten van het kenmerk. Bijvoorbeeld, Hallo out-van-box-regels controleren die kenmerken van een account ingeschakeld (**gebruiker AccountEnabled**) hebben voorrang van andere accounts.

Prioriteit kan worden gedefinieerd tussen Connectors. Waarmee Connectors met betere toocontribute gegevenswaarden eerst.

### <a name="multiple-objects-from-hello-same-connector-space"></a>Meerdere objecten van dezelfde connectorruimte Hallo
Als er meerdere objecten in Hallo dezelfde connector gekoppelde toohello ruimte dezelfde metaverse-object, prioriteit moet worden aangepast. Als meerdere objecten in het bereik zijn van Hallo dezelfde regel synchroniseren, is Hallo synchronisatie-engine niet kunnen toodetermine voorrang. Het is niet-eenduidige welke bronobject bijdraagt Hallo waarde toohello metaverse. Deze configuratie wordt gerapporteerd als niet-eenduidige zelfs als Hallo kenmerken in de bron Hallo Hallo hebben dezelfde waarde.  
![Meerdere objecten die lid zijn van de toohello hetzelfde mv-object](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/multiple1.png)  

In dit scenario moet u toochange Hallo bereik van Hallo sync regels zodat Hallo bronobjecten verschillende synchronisatie regels binnen het bereik hebben. Hierdoor kunt u verschillende voorrang toodefine.  
![Meerdere objecten die lid zijn van de toohello hetzelfde mv-object](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/multiple2.png)  

## <a name="next-steps"></a>Volgende stappen
* Lees meer over Hallo expressietaal in [Understanding declaratieve inrichting expressies](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).
* Zie hoe declaratieve inrichting is gebruikte out of box in [Understanding Hallo standaardconfiguratie](active-directory-aadconnectsync-understanding-default-configuration.md).
* Zie hoe een praktisch toomake wijzigen met behulp van declaratieve inrichting [hoe een wijziging toohello toomake standaard configuratie](active-directory-aadconnectsync-change-the-configuration.md).
* Hoe gebruikers en contactpersonen samenwerken in tooread gaan [inzicht krijgen in gebruikers en contactpersonen](active-directory-aadconnectsync-understanding-users-and-contacts.md).

**Overzichtsonderwerpen**

* [Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen](active-directory-aadconnectsync-whatis.md)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)

**Onderwerpen met naslaginformatie**

* [Azure AD Connect-synchronisatie: functieverwijzing](active-directory-aadconnectsync-functions-reference.md)
