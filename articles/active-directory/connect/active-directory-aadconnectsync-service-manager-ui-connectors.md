---
title: aaaConnectors in hello Azure AD Synchronization Service Manager UI | Microsoft-Docs
description: Hallo Connectors tabblad in Hallo Synchronization Service Manager begrijpen voor Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c0969630313178b1e299385b1289360c8f787cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-with-hello-azure-ad-connect-sync-service-manager"></a>Met behulp van connectors met hello Azure AD Connect Sync-Service Manager

![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

Hallo Connectors tabblad is gebruikte toomanage alle systemen Hallo synchronisatie-engine is verbonden met.

## <a name="connector-actions"></a>Connector-acties
| Actie | Opmerking |
| --- | --- |
| Maken |Gebruik geen. Gebruik de wizard Hallo voor het verbinden van tooadditional AD-forests. |
| Eigenschappen |Gebruikt voor het domein en OE filteren. |
| [Verwijderen](#delete) |Gebruikte tooeither Hallo-gegevens in Hallo connector ruimte of toodelete verbinding forest tooa verwijderen. |
| [Profielen uitvoeren configureren](#configure-run-profiles) |Met uitzondering van domein filteren, niets tooconfigure hier. U kunt deze actie uitvoeringsprofielen toosee al is geconfigureerd. |
| Voer |Een ad-hoc uitvoeren van een profiel toostart gebruikt. |
| Stoppen |Een Connector die momenteel wordt uitgevoerd een profiel stopt. |
| Exporteren van de Connector |Gebruik geen. |
| Connector importeren |Gebruik geen. |
| Update-Connector |Gebruik geen. |
| Schema vernieuwen |In de cache schema Hallo vernieuwt. Het is aanbevolen toouse Hallo optie in de installatiewizard Hallo in plaats daarvan sinds die updates ook regels synchroniseren. |
| [Connectorgebied zoeken](#search-connector-space) |Gebruikte toofind objecten en te[volgen op een object en de gegevens via Hallo systeem](#follow-an-object-and-its-data-through-the-system). |

### <a name="delete"></a>Verwijderen
Hallo verwijderingsactie wordt gebruikt voor twee verschillende dingen.  
![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

Hallo optie **alleen connectorruimte verwijderen** Hiermee verwijdert u alle gegevens, maar houd Hallo configuratie.

Hallo optie **Connector verwijderen en connector ruimte** Hallo gegevens en configuratie van de Hallo verwijdert. Deze optie wordt gebruikt wanneer u niet dat tooconnect tooa forest niet meer wilt.

Beide opties alle objecten synchroniseren en Hallo metaverse objecten bijwerken. Deze actie is een langdurige bewerking.

### <a name="configure-run-profiles"></a>Profielen uitvoeren configureren
Deze optie kunt u toosee hello uitvoeringsprofielen geconfigureerd voor een Connector.

![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a>Connectorgebied zoeken
connector Hallo-ruimte zoekactie is nuttig toofind objecten en gegevensproblemen oplossen.

![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

Begin met het selecteren een **bereik**. U kunt zoeken op basis van gegevens (RDN, DN-naam, anker substructuur), of de status van Hallo-object (voor alle opties).  
![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)  
Als u bijvoorbeeld substructuur zoeken wilt, krijgt u alle objecten in een organisatie-eenheid.  
![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)  
Vanaf dit raster kunt u een object selecteert, selecteert u **eigenschappen**, en [hieraan](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) van Hallo bron connectorgebied overgebracht via het Hallo-metaverse en toohello doel connectorgebied overgebracht.

### <a name="changing-hello-ad-ds-account-password"></a>Hallo AD DS accountwachtwoord wijzigen
Als u het accountwachtwoord Hallo wijzigt, Hallo-synchronisatieservice niet langer kunnen tooimport/exporteren wijzigingen tooon lokale AD.   Hallo volgende weergegeven:

- Hallo voor importeren/exporteren stap voor AD-connector Hallo mislukt met fout 'geen start referenties'.
- Onder de functie Logboeken van Windows bevat hello logboek voor toepassingsgebeurtenissen een fout met 6000 van gebeurtenis-ID en het bericht "hello management agent 'contoso.com' kan niet toorun omdat Hallo referenties ongeldig zijn."

tooresolve hello uitgeeft, update gebruikersaccount in AD DS Hallo Hallo volgende met:


1. Hallo Synchronization Service Manager (START → Synchronization Service) starten.
</br>![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)
2. Ga toohello **Connectors** tabblad.
3. Selecteer Hallo AD-Connector die geconfigureerde toouse Hallo AD DS-account.
4. Selecteer onder acties **eigenschappen**.
5. Selecteer in het pop-upvenster hello, Connect tooActive Directory-Forest:
6. Hallo-forestnaam geeft Hallo bijbehorende on-premises AD.
7. Hallo-gebruikersnaam geeft Hallo AD DS-account voor synchronisatie te gebruiken.
8. Geef de nieuwe wachtwoord Hallo Hallo AD DS-account in Hallo wachtwoordtekstvak ![Azure AD Connect-synchronisatie versleuteling sleutel hulpprogramma](media/active-directory-aadconnectsync-encryption-key/key6.png)
9. Klik op OK toosave Hallo nieuwe wachtwoord en start opnieuw Hallo synchronisatieservice tooremove Hallo oude wachtwoord uit cachegeheugen.



## <a name="next-steps"></a>Volgende stappen
Meer informatie over Hallo [Azure AD Connect-synchronisatie](active-directory-aadconnectsync-whatis.md) configuratie.

Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory ](active-directory-aadconnect.md).
