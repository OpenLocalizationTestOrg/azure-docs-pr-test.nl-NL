---
title: 'Azure Active Directory Domain Services: Azure Active Directory Domain Services inschakelen | Microsoft Docs'
description: Azure Active Directory Domain Services met behulp van de klassieke Azure-portal Hallo inschakelen
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>Azure Active Directory Domain Services met behulp van de klassieke Azure-portal Hallo inschakelen

## <a name="task-3-enable-azure-active-directory-domain-services"></a>Taak 3: Azure Active Directory Domain Services inschakelen
In deze taak schakelt u Azure Active Directory Domain Services (Azure AD DS) voor uw directory Hallo volgende stappen uit als volgt:

1. Ga toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Selecteer in het linkerdeelvenster Hallo Hallo **Active Directory** knop.
3. Hello Azure Active Directory (Azure AD) tenant (directory) waarvoor u tooenable Azure AD DS wilt selecteren.

    ![Azure AD-directory selecteren](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Op Hallo **preview directory** pagina, klikt u op Hallo **configureren** tabblad.

    ![Tabblad Configureren van directory](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. Onder **domeinservices**, Hallo wijzigen **domeinservices inschakelen voor deze map** te optie**Ja**.  
    Extra configuratieopties voor Azure Active Directory Domain Services weergegeven op Hallo pagina.

    ![Domain Services inschakelen](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > Wanneer u Azure Active Directory Domain Services voor uw tenant inschakelt, wordt Azure AD genereert en Hallo Kerberos en NTLM referentie-hashes die vereist zijn voor het verifiëren van gebruikers opslaat.
   >
   >
6. Geef Hallo **DNS-domeinnaam van domeinservices**.

   * Hallo standaarddomeinnaam van Hallo-map (met een **. onmicrosoft.com** achtervoegsel) is standaard geselecteerd.

   * Hallo lijst bevat alle domeinen die zijn geconfigureerd voor uw Azure AD-directory, waaronder zowel geverifieerd en niet-geverifieerde domeinen die u op Hallo configureert **domeinen** tabblad.

   * U kunt ook een aangepaste domeinnaam opgeven. In dit voorbeeld wordt de aangepaste domeinnaam Hallo is *contoso100.com*.

     > [!WARNING]
     > Hallo-voorvoegsel van de opgegeven domeinnaam (bijvoorbeeld *contoso100* in Hallo *contoso100.com* domeinnaam) moet 15 of minder tekens bevatten. U kunt geen Azure Active Directory Domain Services-domein maken met een voorvoegsel van meer dan 15 tekens.
     >
     >
7. Zorg ervoor dat die Hallo DNS-domeinnaam die u hebt gekozen voor Hallo beheerd domein nog niet bestaat in het virtuele netwerk Hallo. In het bijzonder of toosee controleren:

   * U hebt al een domein met Hallo dezelfde DNS-domeinnaam op Hallo virtueel netwerk.

   * Hallo virtueel netwerk dat u hebt geselecteerd heeft een VPN-verbinding met uw on-premises netwerk, en u een domein met Hallo dezelfde DNS-domeinnaam op uw on-premises netwerk.

   * U hebt een bestaande cloudservice met die naam op Hallo virtueel netwerk.
8. Selecteer een virtueel netwerk waarop u wilt dat Azure Active Directory Domain Services toobe beschikbaar. Selecteer Hallo virtueel netwerk en u hebt gemaakt in Hallo-toegewezen subnet **Connect domain services-toothis virtueel netwerk** vervolgkeuzelijst. Houd ook rekening Hallo volgende:

   * Zorg ervoor dat Hallo virtuele netwerk dat u hebt opgegeven tooan Azure-regio die wordt ondersteund door Azure Active Directory Domain Services behoort. tooascertain Hallo Azure-regio's waar Azure Active Directory Domain Services beschikbaar is, Zie [Azure-services per regio](https://azure.microsoft.com/regions/#services/).

   * Virtuele netwerken die deel uitmaken van tooa regio waar Azure Active Directory Domain Services niet wordt ondersteund, worden niet weergegeven in de vervolgkeuzelijst Hallo.

   * Gebruik een specifieke subnet in het virtuele netwerk Hallo voor Azure Active Directory Domain Services. Voer *niet* Selecteer Hallo gatewaysubnet. Zie [Aandachtspunten voor netwerken](active-directory-ds-networking.md).

   * Virtuele netwerken die zijn gemaakt met behulp van Azure Resource Manager niet op dezelfde manier in de vervolgkeuzelijst Hallo. Virtuele netwerken op basis van Resource Manager worden momenteel niet ondersteund door Azure Active Directory Domain Services.
9. tooenable Azure Active Directory Domain Services in het taakvenster Hallo onderin Hallo Hallo pagina, klikt u op **opslaan**.
    * Terwijl de Azure Active Directory Domain Services is ingeschakeld voor uw directory, Hallo pagina een status weer van *in behandeling*.

        ![Het venster Domain Services inschakelen](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > Azure Active Directory Domain Services zorgt voor maximale beschikbaarheid voor uw beheerde domein. Nadat u Azure Active Directory Domain Services hebt ingeschakeld, zijn Hallo IP-adressen op welk domein services beschikbaar in het virtuele netwerk Hallo is weergegeven één voor één opnieuw. Hallo tweede IP-adres kort na Hallo eerst weergegeven, zoals snel Hallo maximale beschikbaarheid is ingeschakeld voor uw domein. Wanneer maximale beschikbaarheid is geconfigureerd en actief is voor uw domein, ziet u twee IP-adressen in Hallo **domeinservices** sectie Hallo **configureren** tabblad.
        >
        >
    * Na ongeveer 20 too30 minuten Hallo eerste IP-adres op welk domein services beschikbaar in het virtuele netwerk in Hallo is **IP-adres** op Hallo **configureren** pagina.

        ![Het venster Domain Services met het eerste IP-adres dat is ingericht](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * Wanneer maximale beschikbaarheid ingeschakeld voor uw domein is, worden twee IP-adressen op Hallo pagina weergegeven. Het beheerde domein is op deze twee IP-adressen beschikbaar in het geselecteerde virtuele netwerk.

10. Houd er rekening mee Hallo twee IP-adressen zodat u Hallo DNS-instellingen voor het virtuele netwerk bijwerken kunt. In dat geval kunt virtuele machines op Hallo virtueel netwerk tooconnect toohello domein voor bewerkingen, zoals domeindeelname.

    ![Het venster Domain Services met beide ingerichte IP-adressen](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> Afhankelijk van de grootte van de Hallo van uw Azure AD-tenant (bijvoorbeeld Hallo aantal gebruikers of groepen) duurt synchronisatie tooyour beheerd domein. Dit synchronisatieproces wordt op de achtergrond Hallo. Voor grote tenants met tienduizenden objecten duurt het mogelijk een dag of twee voor alle gebruikers, groepslidmaatschappen en referenties toobe gesynchroniseerd.
>
>

## <a name="next-step"></a>Volgende stap
[Taak 4: Hallo DNS-instellingen bijwerken voor Hallo virtuele Azure-netwerk](active-directory-ds-getting-started-update-dns.md)
