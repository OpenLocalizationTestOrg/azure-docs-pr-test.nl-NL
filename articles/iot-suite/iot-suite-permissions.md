---
title: aaaAzure IoT Suite en Azure Active Directory | Microsoft Docs
description: Hierin wordt beschreven hoe Azure IoT Suite maakt gebruik van Azure Active Directory toomanage machtigingen.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: dobett
ms.openlocfilehash: 4768630f2de4bb431731fbd4e8929232bc80b9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-on-hello-azureiotsuitecom-site"></a>Machtigingen op Hallo azureiotsuite.com site

## <a name="what-happens-when-you-sign-in"></a>Wat gebeurt er wanneer u zich aanmeldt

eerste keer dat u zich aanmelden op Hallo [azureiotsuite.com][lnk-azureiotsuite], Hallo site bepaalt aan Hallo machtigingsniveaus hebben op basis van Hallo momenteel geselecteerde tenant van Azure Active Directory (AAD) en Azure abonnement.

1. Eerst toopopulate Hallo lijst van de volgende tooyour gebruikersnaam tenants gezien Hallo site vindt uit van Azure welke AAD tenants u deel uitmaakt. Hallo site kan op dit moment alleen gebruikerstokens voor één tenant verkrijgen tegelijk. Daarom wanneer u tenants met behulp van Hallo vervolgkeuzelijst in de rechterbovenhoek hello overschakelt, registreert Hallo site u in toothat tenant tooobtain Hallo tokens voor deze tenant.

2. Hallo-site vindt vervolgens uit vanuit Azure welke abonnementen u hebt gekoppeld aan Hallo tenant geselecteerd. Beschikbare abonnementen Hallo ziet u wanneer u een nieuwe vooraf geconfigureerde oplossing maakt.

3. Ten slotte Hallo site haalt alle bronnen op Hallo in Hallo abonnementen en resourcegroepen gelabeld als vooraf geconfigureerde oplossingen en Hallo tegels op Hallo-startpagina gevuld.

Hallo volgende secties beschrijven Hallo-functies waarmee toegang toohello vooraf geconfigureerde oplossingen.

## <a name="aad-roles"></a>AAD-functies

Hallo AAD rollen Hallo mogelijkheid inrichten van de vooraf geconfigureerde oplossingen te controleren en beheren van gebruikers in een vooraf geconfigureerde oplossing.

U vindt meer informatie over beheerdersrollen in AAD in [beheerdersrollen toewijzen in Azure AD][lnk-aad-admin]. Hallo huidige artikel is gericht op Hallo **hoofdbeheerder** en Hallo **gebruiker** directory-functies gebruikt door Hallo vooraf geconfigureerde oplossingen.

### <a name="global-administrator"></a>Globale beheerder

Er zijn veel globale beheerders per AAD-tenant:

* Wanneer u een AAD-tenant maakt, bent u door standaard Hallo globale beheerder van deze tenant.
* Hallo-hoofdbeheerder kan een vooraf geconfigureerde oplossing inricht en is toegewezen een **Admin** rol voor de toepassing hello binnen hun AAD-tenant.
* Als een andere gebruiker in dezelfde Hallo AAD-tenant wordt gemaakt van een toepassing, Hallo standaardrol verleend toohello globale beheerder is **ReadOnly**.
* Een globale beheerder tooroles voor toepassingen die gebruikmaken van Hallo gebruikers kunt toewijzen [Azure-portal][lnk-portal].

### <a name="domain-user"></a>Domeingebruiker

Er zijn veel domeingebruikers per AAD-tenant:

* Een domeingebruiker kan inrichten met een vooraf geconfigureerde oplossing via Hallo [azureiotsuite.com] [ lnk-azureiotsuite] site. Standaard krijgt domeingebruiker Hallo Hallo **Admin** rol in Hallo ingericht toepassing.
* Een domeingebruiker kan een toepassing maken met Hallo build.cmd script in Hallo [azure-iot-remote-monitoring][lnk-rm-github-repo], [azure-iot-predictive-maintenance] [ lnk-pm-github-repo], of [azure-iot-verbonden-factory] [ lnk-cf-github-repo] opslagplaats. Echter Hallo standaardrol verleend toohello domeingebruiker is **ReadOnly**, omdat een domeingebruiker geen machtiging tooassign rollen heeft.
* Als een andere gebruiker op Hallo AAD-tenant wordt gemaakt van een toepassing, de domeingebruiker Hallo Hallo is toegewezen **ReadOnly** rol standaard voor die toepassing.
* Rollen voor toepassingen, kan niet worden toegewezen door een domeingebruiker Daarom toevoegen een domeingebruiker niet gebruikers of rollen voor gebruikers voor een toepassing zelfs als ze deze ingericht.

### <a name="guest-user"></a>Gastgebruiker

Er zijn veel gastgebruikers per AAD-tenant. Gastgebruikers hebben een beperkte set rechten in Hallo AAD-tenant. Gastgebruikers kunnen niet als gevolg hiervan voorzien in een vooraf geconfigureerde oplossing in Hallo AAD-tenant.

Zie voor meer informatie over gebruikers en rollen in AAD Hallo resources te volgen:

* [Gebruikers maken in Azure AD][lnk-create-edit-users]
* [Gebruikers tooapps toewijzen][lnk-assign-app-roles]

## <a name="azure-subscription-administrator-roles"></a>Beheerdersrollen van Azure-abonnement

Hello Azure-beheerdersrollen beheren Hallo mogelijkheid toomap een Azure-abonnement tooan AD-tenant.

Meer informatie over hello Azure beheerdersrollen in Hallo artikel [hoe tooadd of Medebeheerder van Azure, servicebeheerder en accountbeheerder wijzigen][lnk-admin-roles].

## <a name="application-roles"></a>Toepassingsrollen

Hallo toepassingsrollen beheren toodevices toegang in uw vooraf geconfigureerde oplossing.

Er zijn twee gedefinieerde rollen en één impliciete rol gedefinieerd in een ingerichte toepassing:

* **Admin:** heeft volledig beheer tooadd, beheren, verwijdert u apparaten en instellingen wijzigen.
* **Alleen-lezen:** apparaten, regels, taken, acties en telemetrie kunt weergeven.

U vindt Hallo machtigingen toegewezen tooeach rol in Hallo [RolePermissions.cs] [ lnk-resource-cs] bronbestand.

### <a name="changing-application-roles-for-a-user"></a>Het wijzigen van de rollen van de toepassing voor een gebruiker

U kunt hello te volgen procedure toomake een gebruiker in uw Active Directory-beheerder van uw vooraf geconfigureerde oplossing gebruiken.

U moet een AAD globale toochange beheerdersrollen voor een gebruiker:

1. Ga toohello [Azure-portal][lnk-portal].
2. Selecteer **Azure Active Directory**.
3. Zorg ervoor dat u Hallo-directory die u hebt gekozen bij het inrichten van uw oplossing op azureiotsuite.com werkt. Als u meerdere mappen die zijn gekoppeld aan uw abonnement hebt, kunt u schakelen tussen deze als u de naam van uw account op Hallo rechtsboven van Hallo-portal op.
4. Klik op **bedrijfstoepassingen**, klikt u vervolgens **alle toepassingen**.
4. Weergeven **alle toepassingen** met **eventuele** status. Zoek vervolgens naar een toepassing met de naam van uw vooraf geconfigureerde oplossing.
5. Klik op Hallo-naam van de toepassing hello die overeenkomt met de naam van uw vooraf geconfigureerde oplossing.
6. Klik op **gebruikers en groepen**.
7. Selecteer Hallo gebruiker gewenste tooswitch rollen.
8. Klik op **toewijzen** en selecteer Hallo-rol (zoals **Admin**) gewenst tooassign toohello gebruiker, klikt u op het vinkje Hallo.

## <a name="faq"></a>Veelgestelde vragen

### <a name="im-a-service-administrator-and-id-like-toochange-hello-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a>Ik ben een servicebeheerder en toewijzing van toochange Hallo map staat wilt tussen mijn abonnement en een specifieke AAD-tenant. Hoe worden deze taak voltooien?

1. Ga toohello [klassieke Azure-portal][lnk-classic-portal], klikt u op **instellingen** in Hallo lijst met services aan de linkerkant Hallo.
2. Hallo abonnement toewijzing van toochange Hallo map te gewenst selecteren.
3. Klik op **Directory bewerken**.
4. Selecteer Hallo **Directory** gewenst toouse Hallo vervolgkeuzelijst. Klik op Hallo pijl naar rechts.
5. Toewijzing van de map Hallo bevestigen en van invloed op een CO-beheerders. Als u van een andere map verplaatst, worden alle Hallo medebeheerders uit de oorspronkelijke directory Hallo verwijderd.

### <a name="im-a-domain-usermember-on-hello-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a>Ik ben gebruiker/lid van een domein op Hallo AAD-tenant en ik een vooraf geconfigureerde oplossing hebt gemaakt. Hoe ik ophalen een bepaalde rol voor de toepassing?

Een globale beheerder toomake vraagt u een globale beheerder zijn op Hallo AAD-tenant en rollen toousers uzelf toewijzen. U kunt ook een globale beheerder tooassign vragen u rechtstreeks een rol. Als u uw vooraf geconfigureerde oplossing is geïmplementeerd dat wilt voor van toochange Hallo AAD-tenant, ziet u Hallo volgende vraag.

### <a name="how-do-i-switch-hello-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a>Hoe schakel ik Hallo AAD-tenant die mijn vooraf geconfigureerde oplossing voor externe controle en de toepassing zijn toegewezen aan

U kunt een cloudimplementatie uit uitvoeren <https://github.com/Azure/azure-iot-remote-monitoring> en implementeren met een nieuwe AAD-tenant. Omdat u standaard een globale beheerder bent wanneer u een AAD-tenant, maakt u machtigingen tooadd gebruikers en rollen toewijzen toothose gebruikers.

1. Maak een AAD-directory in Hallo [Azure-portal][lnk-portal].
2. Ga te<https://github.com/Azure/azure-iot-remote-monitoring>.
3. Voer `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (bijvoorbeeld `build.cmd cloud debug myRMSolution`)
4. Als u wordt gevraagd, stelt u Hallo **tenantid** toobe uw nieuwe tenant in plaats van uw vorige tenant.

### <a name="i-want-toochange-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a>Ik wil toochange een servicebeheerder of Medebeheerder wanneer aangemeld met een account organisatorische

Zie Hallo ondersteuning-artikel [wijzigen servicebeheerder en Medebeheerder wanneer aangemeld met een account organisatorische][lnk-service-admins].

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-hello-proper-permissions-toocreate-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a>Waarom krijg ik deze fout te zien? 'Uw account heeft geen Hallo juiste machtigingen toocreate een oplossing. Neem contact op met uw accountbeheerder of probeer met een ander account."

Bekijkt hello diagram voor richtlijnen te volgen:

![][img-flowchart]

> [!NOTE]
> Als u doorgaat toosee Hallo fout na het valideren van een globale beheerder zijn op Hallo AAD-tenant en medebeheerder op Hallo abonnement, hebt u uw accountbeheerder Hallo gebruiker verwijderen en opnieuw toewijzen van benodigde machtiging in deze volgorde. Eerst Hallo gebruiker toevoegen als een globale beheerder bent en vervolgens gebruiker toevoegen als medebeheerder op Hallo Azure-abonnement. Als de problemen zich blijven voordoen, neem dan contact op met [Help en ondersteuning voor][lnk-help-support].

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-toocreate-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a>Waarom krijg ik deze fout zien wanneer ik een Azure-abonnement hebben? "Een Azure-abonnement is vereist toocreate vooraf geconfigureerde oplossingen. U kunt een gratis proefaccount maken binnen een paar minuten."

Als u zeker weet dat u hebt een Azure-abonnement, Hallo huurder toewijzen voor uw abonnement te valideren en controleer Hallo juist tenant is geselecteerd in de vervolgkeuzelijst Hallo. Als u hebt gevalideerd Hallo gewenst tenant klopt, volg Hallo voorgaande diagram en valideren van Hallo toewijzing van uw abonnement en deze AAD-tenant.

## <a name="next-steps"></a>Volgende stappen
meer informatie over IoT Suite toocontinue Zie hoe u kunt [aanpassen van een vooraf geconfigureerde oplossing][lnk-customize].

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-classic-portal]: https://manage.windowsazure.com/
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
