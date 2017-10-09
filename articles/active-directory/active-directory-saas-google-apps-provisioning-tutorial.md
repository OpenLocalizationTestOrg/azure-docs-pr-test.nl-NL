---
title: 'Zelfstudie: Google Apps configureren voor het automatisch gebruikers inrichten in Azure | Microsoft Docs'
description: Meer informatie over hoe tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooGoogle Apps.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: d1fa8449bd6013d1627b3552aaa19db1c0f4f46f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a>Zelfstudie: Google Apps configureren voor het automatisch gebruikers inrichten

Hallo-doel van deze zelfstudie is tooshow Hallo van stappen u moet tooperform in Google Apps en Azure AD tooautomatically inrichten en ongedaan inrichten gebruikersaccounts vanuit Azure AD tooGoogle Apps.

## <a name="prerequisites"></a>Vereisten

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

*   Een Azure Active directory-tenant.
*   U moet een geldige tenant voor Google Apps voor werk- of Google Apps voor onderwijs hebben. U kunt een gratis proefaccount voor de service.
*   Een gebruikersaccount in Google Apps met beheerdersmachtigingen Team.

## <a name="assigning-users-toogoogle-apps"></a>Toewijzen van gebruikers tooGoogle Apps

Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd. In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.

Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD Hallo-gebruikers die toegang moeten hebben tot tooyour Google Apps app vertegenwoordigen. Als u besloten, kunt u deze app-gebruikers tooyour Google Apps toewijzen door hier Hallo-instructies te volgen: [toewijzen van een gebruiker of groep tooan enterprise-app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

> [!IMPORTANT]
>*   Het is raadzaam om één Azure AD-gebruiker tooGoogle Apps tootest Hallo inrichting configuratie worden toegewezen. Extra gebruikers en/of groepen kunnen later worden toegewezen.
>*   Wanneer u een gebruiker tooGoogle Apps toewijst, moet u Hallo gebruiker of rol van 'Groep' in het dialoogvenster voor Hallo-toewijzing. Hallo 'Default toegang' rol werkt niet voor het inrichten.

## <a name="enable-automated-user-provisioning"></a>Geautomatiseerde gebruikersinrichting inschakelen

Deze sectie helpt u bij het verbinden van uw Azure AD tooGoogle-Apps gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van toegewezen gebruikersaccounts in Google Apps op basis van gebruikers en groepen toewijzen in Azure AD .

>[!Tip]
>U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Google Apps, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com). Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.

### <a name="configure-automatic-user-account-provisioning"></a>Automatisch gebruikers inrichten van account configureren

> [!NOTE]
> Een andere geschikte optie voor het automatiseren van gebruikers inrichten tooGoogle Apps is toouse [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) die voorziet in uw lokale Active Directory identiteiten tooGoogle Apps. Daarentegen richt Hallo-oplossing in deze zelfstudie uw Azure Active Directory (cloud) gebruikers en groepen met e-mailfunctionaliteit tooGoogle Apps. 

1. Meld u aan bij Hallo [Google Apps-beheerconsole](http://admin.google.com/) met behulp van uw beheerdersaccount en klik op **beveiliging**. Als er geen Hallo-koppeling, kan het verborgen onder Hallo **meer besturingselementen** menu Hallo onder welkomstscherm aan.
   
    ![Klik op 'Security' (Beveiliging).][10]

2. Op Hallo **beveiliging** pagina, klikt u op **API Reference**.
   
    ![Klik op API-verwijzing.][15]

3. Selecteer **inschakelen API-toegang**.
   
    ![Klik op API-verwijzing.][16]

    > [!IMPORTANT]
    > Voor elke gebruiker die u van plan tooprovision tooGoogle Apps, hun gebruikersnaam in Azure Active Directory bent *moet* worden gebonden tooa aangepast domein. Bijvoorbeeld, de gebruikersnamen die lijken op bob@contoso.onmicrosoft.com wordt niet geaccepteerd door Google Apps, terwijl bob@contoso.com wordt geaccepteerd. U kunt het domein van een bestaande gebruiker wijzigen door de eigenschappen bewerken in Azure AD. Instructies voor hoe tooset een aangepast domein voor zowel de Azure Active Directory en de Google Apps zijn opgenomen in volgende stappen.
      
4. Als u een aangepast domein naam tooyour Azure Active Directory nog niet hebt toegevoegd, voert u Hallo stappen te volgen:
  
    a. In Hallo [Azure-portal](https://portal.azure.com), op Hallo navigatiedeelvenster links, klikt u op **Active Directory**. In de maplijsten hello, selecteer uw directory. 

    b. Klik op **domeinen naam** op Hallo navigatiedeelvenster links en klik vervolgens op **toevoegen**.
     
     ![Domein](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![domein toevoegen](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    c. Typ de naam van uw domein in Hallo **domeinnaam** veld. Deze domeinnaam moet Hallo dezelfde domeinnaam die u van plan toouse voor Google Apps bent. Wanneer u klaar bent, klikt u op Hallo **domein toevoegen** knop.
     
     ![Domeinnaam](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    d. Klik op **volgende** toogo toohello verificatie pagina. tooverify eigenaar van dit domein, moet u Hallo-domein-DNS-records volgens toohello-waarden die op deze pagina bewerken. U kunt met behulp van tooverify **MX-records** of **TXT-records**, afhankelijk van wat u selecteren voor Hallo **recordtype** optie. Raadpleeg voor meer uitgebreide instructies over hoe tooverify domeinnaam met Azure AD, [toevoegen van uw eigen domein naam tooAzure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).
     
     ![Domein](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    e. Herhaal de vorige stappen voor alle Hallo domeinen die u van plan tooadd tooyour directory bent Hallo.

5. Nu dat u uw domeinen met Azure AD hebt gecontroleerd, moet u nu controleren ze opnieuw met Google Apps. Voer voor elk domein dat al is niet geregistreerd bij Google Apps, Hallo stappen te volgen:
   
    a. In Hallo [Google Apps-beheerconsole](http://admin.google.com/), klikt u op **domeinen**.
     
     ![Klik op domeinen][20]

    b. Klik op **toevoegen van een domein of de domeinalias van een**.
     
     ![Een nieuw domein toevoegen][21]

    c. Selecteer **toevoegen van een ander domein**, en typt u de naam van het Hallo van Hallo-domein dat u tooadd wilt.
     
     ![Typ de domeinnaam van uw][22]

    d. Klik op **doorgaan en verifiëren dat dit domein**. Volg Hallo stappen tooverify dat u Hallo domeinnaam bezit. Voor uitgebreide instructies over hoe tooverify uw domein met Google Apps zien. [Controleer of uw site-eigendom met Google Apps](https://support.google.com/webmasters/answer/35179).

    e. Herhaal de vorige stappen voor aanvullende domeinen die u van plan tooadd tooGoogle Apps bent Hallo.
     
     > [!WARNING]
     > Als u de primaire domeincontroller Hallo voor uw tenant Google Apps wijzigen, en als u al hebt geconfigureerd eenmalige aanmelding met Azure AD, hebt u toorepeat stap #3 onder [twee stap: Schakel eenmalige aanmelding](#step-two-enable-single-sign-on).
       
6. In Hallo [Google Apps-beheerconsole](http://admin.google.com/), klikt u op **beheerdersrollen**.
   
     ![Klik op Google Apps][26]

7. Bepalen welke admin account u wilt dat toouse toomanage gebruikers inrichten. Voor Hallo **beheerrol** bewerken van dat account Hallo **bevoegdheden** voor die rol. Zorg ervoor dat deze alle Hallo **API beheerdersbevoegdheden** ingeschakeld zodat dit account kan worden gebruikt voor het inrichten.
   
     ![Klik op Google Apps][27]
   
    > [!NOTE]
    > Als u een productie-omgeving configureert, is de beste Hallo toocreate een beheerdersaccount te gebruiken in Google Apps specifiek voor deze stap. Deze accounts moeten een beheerdersrol gekoppeld met de benodigde API-bevoegdheden Hallo hebben.
     
8. In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.

9. Als u Google Apps al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van Google Apps met behulp van Hallo zoekveld opgegeven. Selecteer anders **toevoegen** en zoek naar **Google Apps** in Hallo-toepassingsgalerie. Hallo zoekresultaten van Google Apps selecteren, en voeg deze tooyour lijst met toepassingen.

10. Selecteer uw exemplaar van Google Apps en vervolgens Hallo **inrichten** tabblad.

11. Set Hallo **modus inrichting** te**automatische**. 

     ![Inrichting](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. Onder Hallo **beheerdersreferenties** sectie, klikt u op **autoriseren**. Een dialoogvenster met Google Apps autorisatie in een nieuw browservenster geopend.

13. Bevestig dat u wilt toogive Azure Active Directory toomake wijzigingen in de machtigingen die voor de tenantsleutel tooyour Google Apps. Klik op **accepteren**.
    
     ![Controleer de machtigingen.][28]

14. Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour Google Apps-app kunt verbinden. Als Hallo verbinding mislukt, zorg ervoor dat uw Google Apps-account Team beheerdersmachtigingen heeft en probeer het Hallo **'Autoriseren'** stap opnieuw.

15. Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en Hallo selectievakje.

16. Klik op **opslaan.**

17. Selecteer onder Hallo toewijzingen sectie, **tooGoogle synchroniseren Azure Active Directory-gebruikers Apps.**

18. In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD tooGoogle Apps. kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in Google Apps voor update-bewerkingen. Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.

19. tooenable Hallo inrichting Azure AD-service voor Google Apps, wijziging Hallo **inrichting Status** te**op** in Hallo Zoekinstellingen

20. Klik op **opslaan.**

Deze begint de initiële synchronisatie Hallo van alle gebruikers en/of groepen tooGoogle Apps in de sectie gebruikers en groepen Hallo toegewezen. de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd. U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw app in Google Apps inrichten.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Het beheren van gebruikers account inrichten voor zakelijke Apps](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Eenmalige aanmelding configureren](active-directory-saas-google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-auth.png