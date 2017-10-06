---
title: aaaAzure Active Directory Connect Health operations
description: "Dit artikel wordt beschreven aanvullende bewerkingen die kunnen worden uitgevoerd nadat u Azure AD Connect Health hebt geïmplementeerd."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 86cc3840-60fb-43f9-8b2a-8598a9df5c94
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 1dddcee0bca3150ce08621c045a92a1b3ad9df30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-connect-health-operations"></a>Azure Active Directory Connect Health-bewerkingen
Dit onderwerp wordt beschreven Hallo verschillende bewerkingen kunt uitvoeren met behulp van Azure Active Directory (Azure AD) Connect Health.

## <a name="enable-email-notifications"></a>E-mailmeldingen inschakelen
U kunt hello Azure AD Connect Health-service toosend e-mailmeldingen configureren wanneer waarschuwingen wijzen op uw infrastructuur voor identiteiten is niet gezond. Dit gebeurt wanneer een waarschuwing wordt gegenereerd en wanneer het is opgelost.

![Schermopname van Azure AD Connect Health e-mailinstellingen voor meldingen](./media/active-directory-aadconnect-health/email_noti_discover.png)

> [!NOTE]
> E-mailmeldingen zijn standaard ingeschakeld.
>
>

### <a name="tooenable-azure-ad-connect-health-email-notifications"></a>tooenable Azure AD Connect Health e-mailmeldingen
1. Open Hallo **waarschuwingen** blade voor Hallo service waarvoor u tooreceive e-mailmeldingen wilt.
2. Hallo actiebalk, klik op **meldingsinstellingen**.
3. Selecteer bij Hallo e-mailmelding switch **ON**.
4. Schakel Hallo selectievakje in als u wilt dat alle globale beheerders tooreceive e-mailmeldingen.
5. Als u wilt dat tooreceive e-mailmeldingen op andere e-mailadressen, geeft u ze op Hallo **extra e-mailontvangers** vak. tooremove een e-mailadres in deze lijst met de rechtermuisknop op Hallo en selecteer **verwijderen**.
6. toofinalize hello wijzigingen, klikt u op **opslaan**. Wijzigingen van kracht nadat u opslaan.

## <a name="delete-a-server-or-service-instance"></a>Verwijderen van een server of -service-exemplaar

In sommige gevallen kunt u een server uit bewaakt tooremove. Dit is wat u moet tooknow tooremove een server uit hello Azure AD Connect Health-service.

Wanneer u een server verwijdert, worden op de hoogte van de volgende Hallo:

* Deze actie stopt geen verdere gegevens verzameld van die server. Deze server wordt verwijderd uit het Hallo-service te controleren. Na deze actie bent u geen nieuwe waarschuwingen kunnen tooview, bewaking of gebruik analytische gegevens voor deze server.
* Deze actie verwijderd Hallo Health-Agent niet van uw server. Als u Hallo Health-Agent niet hebt verwijderd voordat u deze stap uitvoert, ziet u mogelijk fouten gerelateerde toohello Health-Agent op Hallo-server.
* Deze actie verwijdert geen Hallo-gegevens die al zijn verzameld van deze server. Dat gegevens worden verwijderd volgens Hallo bewaarbeleid voor gegevens van Azure.
* Nadat u deze actie uitvoert, als u wilt dat dezelfde server toostart bewaking Hallo opnieuw, u moet verwijderen en opnieuw Hallo Health-Agent installeren op deze server.

### <a name="toodelete-a-server-from-hello-azure-ad-connect-health-service"></a>toodelete een server uit hello Azure AD Connect Health-service
Azure AD Connect Health voor Active Directory Federatieservices (AD FS) en Azure AD Connect (Sync):

1. Open Hallo **Server** blade van Hallo **serverlijst** blade door het selecteren van Hallo server name toobe verwijderd.
2. Op Hallo **Server** blade van actiebalk hello, klikt u op **verwijderen**.
3. Hallo-server door naam te typen in het bevestigingsvenster Hallo bevestigen.
4. Klik op **Verwijderen**.

Azure AD Connect Health voor Azure Active Directory Domain Services:

1. Open Hallo **domeincontrollers** dashboard.
2. Selecteer Hallo domain controller toobe verwijderd.
3. Hallo actiebalk, klik op **verwijderen ingeschakeld**.
4. Bevestig Hallo actie toodelete Hallo-server.
5. Klik op **Verwijderen**.

### <a name="delete-a-service-instance-from-azure-ad-connect-health-service"></a>Verwijderen van een service-exemplaar van Azure AD Connect Health-service
In sommige gevallen kunt u tooremove een service-exemplaar. Dit is wat u moet tooknow tooremove een service-exemplaar van hello Azure AD Connect Health-service.

Wanneer u een service-exemplaar verwijdert, worden op de hoogte van de volgende Hallo:

* Deze actie verwijdert Hallo huidige service-exemplaar uit Hallo bewaking van de service.
* Deze actie niet verwijderen of Hallo Health-Agent verwijderen uit een Hallo-servers die als onderdeel van dit service-exemplaar zijn gecontroleerd. Als u Hallo Health-Agent niet hebt verwijderd voordat u deze stap uitvoert, ziet u mogelijk fouten gerelateerde toohello Health-Agent op Hallo-servers.
* Alle gegevens van deze service-exemplaar is verwijderd in overeenstemming met Hallo bewaarbeleid voor gegevens van Azure.
* Na het uitvoeren van deze actie als u toostart Hallo-service controleren wilt, verwijderen en opnieuw installeren van Hallo Health-Agent op alle Hallo-servers. Hallo Health-Agent op die server na het uitvoeren van deze actie als u wilt dat toostart bewaking Hallo dezelfde server opnieuw, verwijderen, opnieuw te installeren en registreren.

#### <a name="toodelete-a-service-instance-from-hello-azure-ad-connect-health-service"></a>toodelete een service-exemplaar van hello Azure AD Connect Health-service
1. Open Hallo **Service** blade van Hallo **servicelijst** blade door het Hallo-service-id (farmnaam) dat u wilt dat tooremove selecteren.
2. Op Hallo **Server** blade van actiebalk hello, klikt u op **verwijderen**.
3. Bevestig door Hallo service-naam te typen in het bevestigingsvenster hello (bijvoorbeeld: sts.contoso.com).
4. Klik op **Verwijderen**.
   <br><br>

[//]: # (Start of RBAC section)
## <a name="manage-access-with-role-based-access-control"></a>Toegang beheren met toegangsbeheer op basis van rollen
[Op rollen gebaseerde toegangsbeheer (RBAC)](../role-based-access-control-configure.md) voor Azure AD Connect Health toegang tot toousers en groepen dan globale beheerders biedt. RBAC toegewezen rollen toohello bedoeld gebruikers en groepen en biedt een mechanisme toolimit Hallo globale beheerders binnen uw directory.

### <a name="roles"></a>Rollen
Azure AD Connect Health ondersteunt Hallo ingebouwde rollen te volgen:

| Rol | Machtigingen |
| --- | --- |
| Eigenaar |Eigenaars kunnen *toegang beheren* (bijvoorbeeld een rol tooa gebruiker of groep toewijzen), *alle informatie bekijken* (bijvoorbeeld waarschuwingen weergeven) vanuit de portal Hallo en *instellingen wijzigen* () bijvoorbeeld: e-mailmeldingen) in Azure AD Connect Health. <br>Standaard globale beheerders van Azure AD aan deze rol zijn toegewezen, en dit kan niet worden gewijzigd. |
| Inzender |Inzenders kunnen *alle informatie bekijken* (bijvoorbeeld waarschuwingen weergeven) vanuit de portal Hallo en *instellingen wijzigen* (bijvoorbeeld e-mailmeldingen) in Azure AD Connect Health. |
| Lezer |Lezers kunnen *alle informatie bekijken* (bijvoorbeeld waarschuwingen weergeven) vanuit de portal Hallo binnen Azure AD Connect Health. |

Alle andere functies (zoals beheerders van de gebruiker toegang of DevTest Labs gebruikers) hebben geen invloed tooaccess binnen Azure AD Connect Health, zelfs als Hallo functies beschikbaar in de portal Hallo-ervaring zijn.

### <a name="access-scope"></a>Toegangsbereik
Azure AD Connect Health biedt ondersteuning voor het beheer van toegang op twee niveaus:

* **Alle exemplaren van de service**: dit pad in de meeste gevallen aanbevolen Hallo is. Hiermee kunt u toegang voor alle exemplaren van de service (bijvoorbeeld een AD FS-farm) alle functie-typen die worden bewaakt door Azure AD Connect Health.
* **Service-exemplaar**: In sommige gevallen moet u wellicht toosegregate toegang op basis van rollen typen of door een service-exemplaar. In dit geval kunt u op instantieniveau Hallo-service toegang beheren.  

Machtiging wordt toegewezen als de gebruiker toegang op Hallo directory of service heeft level-instantie.

### <a name="allow-users-or-groups-access-tooazure-ad-connect-health"></a>Toestaan dat gebruikers of groepen toegang tooAzure AD Connect Health
Hallo volgende stappen laten zien hoe tooallow toegang tot.
#### <a name="step-1-select-hello-appropriate-access-scope"></a>Stap 1: Selecteer de juiste toegangsbereik Hallo
een gebruikerstoegang op Hallo tooallow *alle service-exemplaren* niveau binnen de Azure AD Connect Health, open Hallo hoofdblade in Azure AD Connect Health.<br>

#### <a name="step-2-add-users-and-groups-and-assign-roles"></a>Stap 2: Gebruikers en groepen toevoegen en toewijzen van rollen
1. Van Hallo **configureren** sectie, klikt u op **gebruikers**.<br>
   ![Schermopname van Azure AD Connect Health RBAC hoofdblade, met gebruikers die zijn gemarkeerd](./media/active-directory-aadconnect-health/RBAC_main_blade.png)
2. Selecteer **Toevoegen**.
3. In Hallo **Selecteer een rol** deelvenster een rol selecteren (bijvoorbeeld **eigenaar**).<br>
   ![Schermopname van Azure AD Connect Health RBAC gebruikers venster](./media/active-directory-aadconnect-health/RBAC_add.png)
4. Typ Hallo-naam of id van Hallo gericht gebruiker of groep. Kunt u een of meer gebruikers of groepen op Hallo hetzelfde moment. Klik op **Selecteren**.
   ![Schermopname van Azure AD Connect Health RBAC gebruikers venster](./media/active-directory-aadconnect-health/RBAC_select_users.png)
5. Selecteer **OK**.<br>
6. Nadat de roltoewijzing Hallo voltooid is, worden Hallo-gebruikers en groepen in de lijst Hallo weergegeven.<br>
   ![Schermopname van Azure AD Connect Health RBAC venster gebruikers met nieuwe gebruikers die zijn gemarkeerd](./media/active-directory-aadconnect-health/RBAC_user_list.png)

Nu Hallo weergegeven voor gebruikers en groepen hebben toegang tot, op basis van rollen toegewezen tootheir.

> [!NOTE]
> * Globale beheerders altijd hebben volledige toegang tooall Hallo bewerkingen, maar globale beheerdersaccounts zijn niet aanwezig in Hallo voorafgaand aan de lijst.
> * Hallo gebruikers uitnodigen functie wordt niet ondersteund in Azure AD Connect Health.
>
>

#### <a name="step-3-share-hello-blade-location-with-users-or-groups"></a>Stap 3: Hallo blade locatie delen met gebruikers of groepen
1. Nadat u machtigingen toewijzen, een gebruiker toegang krijgen tot Azure AD Connect Health door te gaan [hier](http://aka.ms/aadconnecthealth).
2. Hallo-gebruiker kunt op Hallo blade vastmaken Hallo-blade of verschillende onderdelen van het dashboard toohello. Klik op Hallo **pincode toodashboard** pictogram.<br>
   ![Schermopname van Azure AD Connect Health RBAC blade vastmaken, met Punaisepictogram gemarkeerd](./media/active-directory-aadconnect-health/RBAC_pin_blade.png)

> [!NOTE]
> Een gebruiker met de rol Lezer Hallo toegewezen, is geen kunnen tooget Azure AD Connect Health-extensie van hello Azure Marketplace. Hallo-gebruiker kan Hallo nodig 'maken' bewerking toodo dus niet uitvoeren. Hallo-gebruiker kunt toohello blade krijgen door gaat toohello voorgaande link. Voor de volgende syntaxis kunt Hallo gebruiker Hallo blade toohello dashboard vastmaken.
>
>

### <a name="remove-users-or-groups"></a>Gebruikers of groepen verwijderen
U kunt een gebruiker of groep toegevoegd verwijderen tooAzure AD Connect Health RBAC. Gewoon met de rechtermuisknop op Hallo gebruiker of groep en selecteer **verwijderen**.<br>
![Schermopname van Azure AD Connect Health RBAC gebruikers venster verwijderen die zijn gemarkeerd](./media/active-directory-aadconnect-health/RBAC_remove.png)

[//]: # (End of RBAC section)

## <a name="next-steps"></a>Volgende stappen
* [Azure AD Connect Health (Engelstalig)](active-directory-aadconnect-health.md)
* [De Azure AD Connect Health-agent installeren](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health gebruiken met AD FS](active-directory-aadconnect-health-adfs.md)
* [Azure AD Connect Health for Sync gebruiken](active-directory-aadconnect-health-sync.md)
* [Azure AD Connect Health gebruiken met AD DS](active-directory-aadconnect-health-adds.md)
* [Veelgestelde vragen over Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Versiegeschiedenis van Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
