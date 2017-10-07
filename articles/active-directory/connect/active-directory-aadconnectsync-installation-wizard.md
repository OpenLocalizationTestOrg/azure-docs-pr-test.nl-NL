---
title: Opnieuw uit te voeren hello Azure AD Connect-installatiewizard | Microsoft Docs
description: Wordt uitgelegd hoe Hallo-installatiewizard werkt Hallo tweede keer dat u deze uitvoert.
keywords: Hello Azure AD Connect-installatiewizard kunt u de tweede keer dat u het uitvoeren van onderhoud instellingen Hallo configureren
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a>Azure AD Connect-synchronisatie: Hallo-installatiewizard een tweede keer uitgevoerd
Hallo u eerste keer hello Azure AD Connect-installatiewizard uitvoert deze laat zien hoe u tooconfigure uw installatie. Als u de installatiewizard Hallo opnieuw uitvoert, biedt opties voor onderhoud.

U vindt Hallo-installatiewizard in Hallo Startmenu met de naam **Azure AD Connect**.

![Het menu Start](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

Wanneer u Hallo-installatiewizard te starten, ziet u een pagina met deze opties:

![Pagina met een lijst van extra taken](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

Als u AD FS hebt geïnstalleerd met Azure AD Connect, hebt u nog meer opties. aanvullende opties die u hebt voor AD FS zijn gedocumenteerd in Hallo [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).

Selecteer een van de Hallo taken en klikt u op **volgende** toocontinue.

> [!IMPORTANT]
> Terwijl u Hallo-installatiewizard open zijn, worden alle bewerkingen in de synchronisatie-engine Hallo onderbroken. Zorg ervoor dat u de installatiewizard Hallo sluiten als u uw wijzigingen in de configuratie hebt voltooid.
>
>

## <a name="view-current-configuration"></a>De huidige configuratie weergeven
Deze optie biedt een overzicht van de momenteel geconfigureerde opties.

![Pagina met een lijst met alle opties en hun status](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

Klik op **vorige** toogo terug. Als u selecteert **afsluiten**, u Hallo-installatiewizard sluit.

## <a name="customize-synchronization-options"></a>Opties voor synchronisatie aanpassen
Deze optie is configuratie gebruikte toomake wijzigingen toohello-synchronisatie. Er is een subset van de opties in het installatiepad van Hallo aangepaste configuratie. U ziet deze optie ook als u snelle installatie in eerste instantie worden gebruikt.

* [Toevoegen van meer mappen](active-directory-aadconnect-get-started-custom.md#connect-your-directories). Zie voor het verwijderen van een map [verwijderen van een Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).
* [Wijzigen van domein en OE filteren](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).
* Filteren van de groep verwijderen.
* [Optionele functies wijzigen](active-directory-aadconnect-get-started-custom.md#optional-features).

Hallo andere opties van de eerste installatie Hallo kunnen niet worden gewijzigd en zijn niet beschikbaar. Deze opties zijn:

* Hallo kenmerk toouse voor userPrincipalName en sourceAnchor wijzigen.
* Lid worden van de methode voor objecten van een ander forest Hallo wijzigen.
* Filteren op basis van een groep inschakelen.

## <a name="refresh-directory-schema"></a>Directory-schema vernieuwen
Deze optie wordt gebruikt als u Hallo schema hebt gewijzigd in een van uw on-premises AD DS-forests. Bijvoorbeeld, kan ook Exchange zijn geïnstalleerd of bijgewerkt schema met apparaatobjecten tooa Windows Server 2012. In dit geval moet tooinstruct Azure AD Connect tooread Hallo schema opnieuw uit AD DS en de cache niet bijwerken. Deze actie wordt ook Hallo Sync regels opnieuw gegenereerd. Als u Hallo Exchange-schema, bijvoorbeeld toevoegt, worden Hallo Sync regels voor Exchange toohello configuratie toegevoegd.

Wanneer u deze optie selecteert, worden alle Hallo mappen in uw configuratie weergegeven. U kunt Hallo standaardinstelling behouden en Vernieuw alle forests of selectie ervan opheffen enkele ervan.

![Pagina met een lijst met alle mappen in Hallo-omgeving](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a>Faseringsmodus configureren
Deze optie kunt u tooenable en schakel de faseringsmodus op Hallo server uit. Meer informatie over modus en hoe deze wordt gebruikt voor gefaseerde installatie vindt u in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).

Hallo-optie ziet als tijdelijke momenteel is ingeschakeld of uitgeschakeld:  
![Optie die ook Hallo huidige status van de faseringsmodus wordt weergegeven](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

toochange Hallo status, selecteer deze optie en selecteren of selectie Hallo selectievakje.  
![Optie die ook Hallo huidige status van de faseringsmodus wordt weergegeven](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a>Gebruikersaanmelding wijzigen
Deze optie kunt u toochange van wachtwoord sync toofederation of Hallo andersom. U niet te wijzigen**niet configureert**.

Zie voor meer informatie over deze optie [gebruikersaanmelding](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over Hallo configuratiemodel gebruikt door Azure AD Connect-synchronisatie in [Understanding declaratieve inrichting](active-directory-aadconnectsync-understanding-declarative-provisioning.md).

**Overzichtsonderwerpen**

* [Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen](active-directory-aadconnectsync-whatis.md)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
