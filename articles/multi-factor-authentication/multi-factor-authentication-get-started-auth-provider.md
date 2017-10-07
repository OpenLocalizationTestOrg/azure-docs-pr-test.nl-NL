---
title: Azure multi-factor Authentication-Provider is gestart aaaGet | Microsoft Docs
description: Meer informatie over hoe toocreate een Azure multi-factor Authentication-Provider.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: a7dd5030-7d40-4654-8fbd-88e53ddc1ef5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 00ea967a80b43baff38c1de586c54d95c9abac2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-an-azure-multi-factor-auth-provider"></a>Aan de slag met een Azure Multi-Factor Authentication-provider
Verificatie in twee stappen is standaard beschikbaar voor globale beheerders van Azure Active Directory- en Office 365-gebruikers. Echter, als u profiteren van tootake wilt [geavanceerde functies](multi-factor-authentication-whats-next.md) en vervolgens moet u Hallo volledige versie van Azure multi-factor Authentication (MFA) aanschaffen.

Een Azure multi-factor Authentication-Provider wordt gebruikt tootake profiteren van de functies die worden geleverd door Hallo volledige versie van Azure MFA. Deze is bestemd voor gebruikers die **geen licenties via Azure MFA, Azure AD Premium of Enterprise Mobility + Security (EMS)** hebben.  Azure MFA, Azure AD Premium en EMS bevatten Hallo volledige versie van Azure MFA standaard. Als u licenties hebt, hebt u geen Azure Multi-Factor Authentication-provider nodig.

Een Azure multi-factor Authentication-provider is vereist toodownload Hallo SDK.

> [!IMPORTANT]
> toodownload Hallo SDK, moet u een Azure multi-factor Authentication-Provider toocreate zelfs als u Azure MFA, AAD Premium of EMS-licenties hebt.  Als u een Azure multi-factor Authentication-Provider voor dit doel maken en licenties al hebt, moet u ervoor toocreate Hallo Provider Hello **Per ingeschakelde gebruiker** model. Koppel vervolgens Hallo Provider toohello map waarin hello Azure MFA, Azure AD Premium of EMS-licenties. Deze configuratie zorgt ervoor dat u wordt alleen gefactureerd als er meer unieke gebruikers verificatie in twee stappen dan het aantal licenties dat u bezit Hallo uitvoeren.

## <a name="what-is-an-azure-multi-factor-auth-provider"></a>Wat is een Azure Multi-Factor Authentication-provider?

Als er geen licenties voor Azure multi-factor Authentication, kunt u een verificatie auth provider toorequire in twee stappen voor uw gebruikers. Als u een aangepaste app ontwikkelt en tooenable Azure MFA, maakt u een Authentication-provider en [Hallo SDK downloaden](multi-factor-authentication-sdk.md).

Er zijn twee soorten auth-providers en Hallo onderscheid is rond hoe uw Azure-abonnement wordt in rekening gebracht. de optie voor de per authenticatie Hallo berekend Hallo aantal authenticaties van uw tenant uitgevoerd in een maand. Deze optie wordt aanbevolen als u een aantal gebruikers hebt die slechts sporadisch verifiëren, bijvoorbeeld als u MFA vereist voor een aangepaste toepassing. de optie voor de per gebruiker Hallo berekend Hallo aantal personen in uw tenant die verificatie in twee stappen in een maand uitvoeren. Deze optie wordt aanbevolen als u sommige gebruikers met licenties hebt maar tooextend MFA toomore gebruikers buiten de grenzen van uw licentie nodig.

## <a name="create-a-multi-factor-auth-provider"></a>Een Multi-Factor Authentication-provider maken
Gebruik Hallo stappen toocreate een Azure multi-factor Authentication-Provider te volgen. Azure multi-factor Auth-Providers kunnen alleen worden gemaakt in Hallo klassieke Azure-portal. Als u toohello klassieke Azure-portal niet kunt aanmelden, controleert u ervoor dat uw Azure AD-tenant is toomake [die zijn gekoppeld aan een Azure-abonnement](../active-directory/active-directory-how-subscriptions-associated-directory.md). 

1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com) als beheerder.
2. Selecteer aan de linkerkant Hallo **Active Directory**.
3. Selecteer op Hallo Active Directory-pagina bovenaan Hallo **multi-factor Authentication-Providers**.
   
   ![Een MFA-provider maken](./media/multi-factor-authentication-get-started-auth-provider/authprovider1.png)

4. Klik onder Hallo op **nieuw**.
   
   ![Een MFA-provider maken](./media/multi-factor-authentication-get-started-auth-provider/authprovider2.png)

5. Onder App Services selecteert u **Multi-Factor Authentication-provider**
   
   ![Een MFA-provider maken](./media/multi-factor-authentication-get-started-auth-provider/authprovider3.png)

6. Selecteer **Snelle invoer**.
   
   ![Een MFA-provider maken](./media/multi-factor-authentication-get-started-auth-provider/authprovider4.png)

7. Vul Hallo velden te volgen en selecteer **maken**.
   1. **Naam** – hello naam van het Hallo multi-factor Authentication-Provider.
   2. **Gebruiksmodel**: kies een van de volgende twee opties:
      * Per verificatie – koopmodel waarin per verificatie wordt betaald. Wordt doorgaans gebruikt in scenario's die gebruikmaken van Azure Multi-Factor Authentication in een toepassing waarmee consumenten te maken krijgen.
      * Per ingeschakelde gebruiker – koopmodel waarin voor elke ingeschakelde gebruiker wordt betaald. Doorgaans gebruikt voor werknemers toegang tooapplications zoals Office 365. Kies deze optie als sommige gebruikers al een licentie voor Azure MFA hebben.
   3. **Directory** – hello Azure Active Directory-tenant die Hallo multi-factor Authentication-Provider is gekoppeld. Let op Hallo volgende:
      * U hoeft niet in een Azure AD-directory toocreate een multi-Factor Authentication-Provider. Laat dit vak leeg als u van plan bent alleen toodownload hello Azure multi-factor Authentication-Server of de SDK.
      * Hallo multi-factor Authentication-Provider moet worden gekoppeld aan een Azure AD directory tootake voordeel van Hallo geavanceerde functies.
      * Er kan slechts één Multi-Factor Authentication-provider worden gekoppeld aan één Azure AD-adreslijst.  
      ![Een MFA-provider maken](./media/multi-factor-authentication-get-started-auth-provider/authprovider5.png)

8. Nadat u op maken, Hallo multi-factor Authentication-Provider gemaakt en u ziet een bericht weergegeven: **multi-factor Authentication-Provider is gemaakt**. Klik op **OK**.  
   
   ![Een MFA-provider maken](./media/multi-factor-authentication-get-started-auth-provider/authprovider6.png)  

## <a name="manage-your-multi-factor-auth-provider"></a>Een Multi-Factor Authentication-provider beheren

U kunt Hallo gebruik niet wijzigen (per ingeschakelde gebruiker of per authenticatie) model nadat een MFA-provider is gemaakt. U kunt echter Hallo MFA-provider verwijderen en maak vervolgens een met een andere gebruiksmodel.

Als hello huidige multi-factor Authentication-Provider wordt gekoppeld aan een Azure AD-directory (ook wel bekend als een Azure AD-tenant), kunt u veilig Hallo MFA-provider verwijderen en een gekoppelde toohello dezelfde Azure AD-tenant maken. U kunt ook als u onvoldoende MFA, Azure AD Premium of Enterprise Mobility + Security (EMS) licenties toocover alle gebruikers die zijn ingeschakeld voor MFA aangeschaft, kunt u verwijderen Hallo MFA-provider helemaal.

Als de MFA-provider niet gekoppeld tooan Azure AD-tenant is of koppelen van Hallo nieuwe MFA-provider tooa andere Azure AD-tenant, instellingen en configuratie-opties niet overgedragen. Bovendien moet bestaande Azure MFA-Servers toobe opnieuw geactiveerd met behulp van activering referenties gegenereerd via Hallo nieuwe MFA-Provider. Hallo MFA Servers toolink reactiveren ze toohello nieuwe MFA-Provider heeft geen invloed op telefoongesprek en tekstberichtverificatie, maar de mobiele app meldingen niet meer zal werken voor alle gebruikers totdat ze Hallo mobiele app activeren.

## <a name="next-steps"></a>Volgende stappen

[Hallo multi-factor Authentication SDK downloaden](multi-factor-authentication-sdk.md)

[Multi-Factor Authentication-instellingen configureren](multi-factor-authentication-whats-next.md)
