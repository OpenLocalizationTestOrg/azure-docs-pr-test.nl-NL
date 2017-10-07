---
title: 'Zelfstudie: Azure Active Directory-integratie met vak | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en vak.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c959595-6e57-4954-9c0d-67ba03ee212b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: e92baabb174642c22c99e2a30bc9c71845b3b75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-box-for-automatic-user-provisioning"></a>Zelfstudie: Vak configureren voor het automatisch gebruikers inrichten

Hallo-doel van deze zelfstudie is tooshow Hallo stappen u moet tooperform in het vak en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD-tooBox.

## <a name="prerequisites"></a>Vereisten

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

*   Een Azure Active directory-tenant.
*   Een selectievakje eenmalige aanmelding ingeschakeld abonnement.
*   Een gebruikersaccount in het vak met beheerdersmachtigingen Team.

## <a name="assigning-users-toobox"></a>Gebruikers tooBox toewijzen 

Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd. In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.

Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour Box-app. Als u had besloten, kunt u deze gebruikers tooyour Box-app toewijzen door hier Hallo-instructies te volgen:

[Toewijzen van een gebruiker of groep tooan enterprise-app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

## <a name="assign-users-and-groups"></a>Gebruikers en groepen toewijzen
Hallo **vak > gebruikers en groepen** tabblad in hello Azure-portal kunt u toospecify welke gebruikers en groepen moet tooBox toegang krijgen. Toewijzing van een gebruiker of groep zorgt ervoor dat de volgende dingen toooccur Hallo:

* Azure AD is Hallo toegewezen gebruiker (zowel door rechtstreekse toewijzing toe of groepslidmaatschap) tooauthenticate tooBox toegestaan. Als een gebruiker niet is toegewezen, Azure AD staat niet toe dat ze toosign in tooBox en retourneert een fout op Hallo Azure AD-aanmeldingspagina.
* Een app-tegel voor Box toohello van de gebruiker is toegevoegd [toepassingsstartprogramma](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).
* Als automatische inrichting is ingeschakeld, worden klikt u vervolgens Hallo toegewezen gebruikers en/of groepen toegevoegd toohello inrichting wachtrij toobe automatisch worden ingericht.
  
  * Als alleen gebruikersobjecten geconfigureerde toobe ingericht zijn, vervolgens alle rechtstreeks toegewezen gebruikers in Hallo inrichting wachtrij zijn geplaatst en alle gebruikers die lid van een toegewezen groepen zijn in Hallo inrichting van de wachtrij worden geplaatst. 
  * Als groepsobjecten geconfigureerde toobe ingericht, zijn alle objecten van het toegewezen ingerichte tooBox en alle gebruikers die lid zijn van die groepen. Hallo-groep en gebruiker lidmaatschappen blijven behouden bij tooBox wordt geschreven.

U kunt Hallo **kenmerken > Single Sign-On** tooconfigure welke gebruikerskenmerken (of de claims) u tooBox tijdens verificatie op basis van SAML en Hallo vindt tabblad **kenmerken > inrichten** tabblad tooconfigure hoe gebruikers- en groepskenmerken van Azure AD-tooBox stromen tijdens het inrichten van bewerkingen.

### <a name="important-tips-for-assigning-users-toobox"></a>Belangrijke tips voor het toewijzen van gebruikers tooBox 

*   Verdient het aanbeveling om een Azure AD voor één gebruiker toegewezen tooBox tootest Hallo configuratie inrichten. Extra gebruikers en/of groepen kunnen later worden toegewezen.

*   Wanneer u een gebruiker toobox toewijst, moet u een geldige gebruikersrol. Hallo 'Default toegang' rol werkt niet voor het inrichten.

## <a name="enable-automated-user-provisioning"></a>Geautomatiseerde Gebruikersinrichting inschakelen

Deze sectie helpt bij het verbinden van uw Azure AD-tooBox gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen toegewezen gebruikersaccounts in vak op basis van gebruikers en groepen toewijzen in Azure AD.

Als automatische inrichting is ingeschakeld, worden klikt u vervolgens Hallo toegewezen gebruikers en/of groepen toegevoegd toohello inrichting wachtrij toobe automatisch worden ingericht.
    
 * Als er slechts gebruikersobjecten geconfigureerde toobe ingericht zijn, en vervolgens rechtstreeks toegewezen gebruikers in Hallo inrichting wachtrij zijn geplaatst en alle gebruikers die lid van een toegewezen groepen zijn in Hallo inrichting van de wachtrij worden geplaatst. 
    
 * Als groepsobjecten geconfigureerde toobe ingericht, zijn alle objecten van het toegewezen ingerichte tooBox en alle gebruikers die lid zijn van die groepen. Hallo-groep en gebruiker lidmaatschappen blijven behouden bij tooBox wordt geschreven.

> [!TIP] 
> U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Hallo-instructies in het vak [Azure-portal](https://portal.azure.com). Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure automatische account gebruikersaanvragen:

Hallo-doel van deze sectie is het toooutline hoe tooBox tooenable het inrichten van Active Directory-gebruiker accounts.

1. In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.

2. Als u het selectievakje voor eenmalige aanmelding al hebt geconfigureerd, kunt u zoeken naar uw exemplaar van Hallo zoekveld opgegeven voor het. Selecteer anders **toevoegen** en zoek naar **vak** in Hallo-toepassingsgalerie. Schakel in in de zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.

3. Uw exemplaar van het selectievakje selecteert en vervolgens Hallo **inrichten** tabblad.

4. Set Hallo **modus inrichting** te**automatische**. 

    ![Inrichting](./media/active-directory-saas-box-userprovisioning-tutorial/provisioning.png)

5. Onder Hallo **beheerdersreferenties** sectie, klikt u op **autoriseren** tooopen een dialoogvenster voor aanmelding in een nieuw browservenster.

6. Op Hallo **aanmelding toogrant toegang tooBox** pagina, geef referenties op Hallo vereist en klik op **autoriseren**. 
   
    ![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "automatische gebruikersinrichting inschakelen")

7. Klik op **verlenen toegang tooBox** tooauthorize deze bewerking en tooreturn toohello Azure-portal. 
   
    ![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "automatische gebruikersinrichting inschakelen")

8. Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour vak app kunt verbinden. Als Hallo verbinding mislukt, zorg ervoor dat uw account vak Team beheerdersmachtigingen heeft en probeer het Hallo **'Autoriseren'** stap opnieuw.

9. Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en Hallo selectievakje.

10. Klik op **opslaan.**

11. Selecteer onder Hallo toewijzingen sectie, **tooBox synchroniseren Azure Active Directory-gebruikers.**

12. In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooBox. kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in vak voor update-bewerkingen. Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.

13. tooenable Hallo inrichting Azure AD-service voor Box, wijziging Hallo **inrichting Status** te**op** in Hallo Zoekinstellingen

14. Klik op **opslaan.**

Hallo initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen tooBox in Hallo gebruikers en groepen sectie worden gestart. de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd. U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op de Box-app inrichten.

U kunt nu een testaccount maken. Wacht tot up too20 minuten tooverify die Hallo-account is gesynchroniseerd toobox.

In uw tenant vak gesynchroniseerde gebruikers worden vermeld in **beheerde gebruikers** in Hallo **beheerconsole**.

![Integratiestatus](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "integratie-status")


## <a name="additional-resources"></a>Aanvullende bronnen

* [Het beheren van gebruikers account inrichten voor zakelijke Apps](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Eenmalige aanmelding configureren](active-directory-saas-box-tutorial.md)