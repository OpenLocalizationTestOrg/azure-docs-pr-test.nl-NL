---
title: 'Azure Active Directory Domain Services: Beheerdershandleiding | Microsoft Docs'
description: Maken van een organisatie-eenheid (OE) in Azure AD Domain Services beheerd-domeinen
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 52602ad8-2b93-4082-8487-427bdcfa8126
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: ce7539e5d5c7c1bf9505ef229f2d31d84c00da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-organizational-unit-ou-on-an-azure-ad-domain-services-managed-domain"></a>Maken van een organisatie-eenheid (OE) op een beheerd domein van Azure AD Domain Services
Azure AD Domain Services beheerde domeinen bevatten twee ingebouwde containers respectievelijk 'AADDC Computers' en 'AADDC gebruikers' genoemd. Hallo AADDC Computers' heeft de container computerobjecten voor alle computers die zijn gekoppeld toohello beheerd domein. Hallo 'AADDC gebruikers' container bevat gebruikers en groepen in hello Azure AD-tenant. In sommige gevallen kan het zijn nodig toocreate serviceaccounts op Hallo beheerd domein toodeploy werkbelastingen. U kunt voor dit doel een aangepaste organisatie-eenheid (OU) maken op Hallo beheerd domein en serviceaccounts binnen de organisatie-eenheid maken. Dit artikel ziet u hoe toocreate een organisatie-eenheid in uw beheerde domein.

## <a name="before-you-begin"></a>Voordat u begint
tooperform hello taken die in dit artikel worden vermeld, hebt u nodig:

1. Een geldige **Azure-abonnement**.
2. Een **Azure AD-directory** -ofwel gesynchroniseerd met een on-premises adreslijst of een map alleen in de cloud.
3. **Azure AD Domain Services** moet zijn ingeschakeld voor hello Azure AD-directory. Als u dit nog niet hebt gedaan, volgt u alle Hallo taken die worden beschreven in Hallo [handleiding](active-directory-ds-getting-started.md).
4. Domein-virtuele machines van waaruit u hello Azure AD Domain Services beheren beheerd domein. Als u dergelijke een virtuele machine geen hebt, volgt u alle Hallo taken die worden beschreven in artikel Hallo [lid worden van een beheerd domein voor Windows virtuele machine tooa](active-directory-ds-admin-guide-join-windows-vm.md).
5. U moet referenties op Hallo van een **account behoren toohello 'AAD DC-beheerders' gebruikersgroep** in uw directory toocreate een aangepaste organisatie-eenheid op uw beheerde domein.

## <a name="install-ad-administration-tools-on-a-domain-joined-virtual-machine-for-remote-administration"></a>AD-beheerprogramma's installeren op een virtuele machine domein voor extern beheer
Azure AD Domain Services beheerde domeinen kunnen worden beheerd op afstand met vertrouwd Active Directory-beheerprogramma's zoals Hallo Active Directory-beheercentrum (ADAC) of AD PowerShell. Tenantbeheerders hebt geen rechten tooconnect toodomain controllers op Hallo beheerd domein via Extern bureaublad. tooadminister Hallo beheerd domein, Hallo AD administration tools onderdeel installeren op een virtuele machine gekoppelde toohello beheerd domein. Raadpleeg artikel toohello [een Azure AD Domain Services beheerd domein beheren](active-directory-ds-admin-guide-administer-domain.md) voor instructies.

## <a name="create-an-organizational-unit-on-hello-managed-domain"></a>Maken van een organisatie-eenheid op Hallo beheerd domein
Nu Hallo AD beheerprogramma's zijn geïnstalleerd op Hallo domein virtuele machine, kunnen we gebruiken deze toocreate hulpprogramma's voor een organisatie-eenheid op Hallo beheerd domein. Voer Hallo stappen te volgen:

> [!NOTE]
> Alleen leden van Hallo ' AAD DC' beheerdersgroep hebben vereiste bevoegdheden toocreate Hallo een aangepaste organisatie-eenheid. Zorg ervoor dat u de volgende stappen uit als een gebruiker die lid is van de groep toothis Hallo uitvoert.
>
>

1. Vanuit het startscherm hello, klikt u op **Systeembeheer**. U ziet Systeembeheer Hallo AD op Hallo virtuele machine geïnstalleerd.

    ![Beheerprogramma's geïnstalleerd op server](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. Klik op **Active Directory-beheercentrum**.

    ![Active Directory-beheercentrum](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. tooview hello domein, klikt u op Hallo-domeinnaam in het linkerdeelvenster hello (bijvoorbeeld, contoso100.com').

    ![Active Directory-Beheercentrum - domein weergeven](./media/active-directory-domain-services-admin-guide/create-ou-adac-overview.png)
4. Aan de rechterkant Hallo **taken** deelvenster, klikt u op **nieuw** onder de naam domeinknooppunt Hallo. In dit voorbeeld klikt raadzaam **nieuw** onder Hallo 'contoso100(local)' knooppunt aan de rechterkant Hallo **taken** deelvenster.

    ![Active Directory-Beheercentrum - nieuwe organisatie-eenheid](./media/active-directory-domain-services-admin-guide/create-ou-adac-new-ou.png)
5. U ziet Hallo optie toocreate een organisatie-eenheid. Klik op **organisatie-eenheid** toolaunch hello **organisatie-eenheid maken** dialoogvenster.
6. In Hallo **organisatie-eenheid maken** dialoogvenster, Geef een **naam** voor Hallo nieuwe organisatie-eenheid. Geef een korte beschrijving voor Hallo organisatie-eenheid. U kunt ook instellen Hallo **beheerd door** veld voor Hallo organisatie-eenheid. toocreate Hallo aangepaste organisatie-eenheid, klikt u op **OK**.

    ![Active Directory-Beheercentrum - dialoogvenster van de organisatie-eenheid maken](./media/active-directory-domain-services-admin-guide/create-ou-dialog.png)
7. Hallo nieuw gemaakte organisatie-eenheid wordt nu weergegeven in Hallo AD-beheercentrum (ADAC).

    ![Active Directory-Beheercentrum - organisatie-eenheid gemaakt](./media/active-directory-domain-services-admin-guide/create-ou-done.png)

## <a name="permissionssecurity-for-newly-created-ous"></a>Machtigingen/beveiliging voor de zojuist gemaakte organisatie-eenheden
Standaard Hallo Hallo gebruiker (lid van groep Hallo 'AAD DC Administrators') die gemaakt Hallo aangepaste OE bevoegdheden als beheerder (volledig beheer) wordt verleend via de organisatie-eenheid. Hallo-gebruiker kunt opwekken en bevoegdheden tooother gebruikers of toohello ' AAD DC' beheerdersgroep naar wens verlenen. Zoals u in de volgende schermafbeelding Hallo, gebruiker Hallo 'bob@domainservicespreview.onmicrosoft.com' wie gemaakte Hallo nieuwe 'MyCustomOU' organisatie-eenheid volledige controle over het is verleend.

 ![Active Directory-Beheercentrum - nieuwe beveiliging van de organisatie-eenheid](./media/active-directory-domain-services-admin-guide/create-ou-permissions.png)

## <a name="notes-on-administering-custom-ous"></a>Opmerkingen over het beheren van aangepaste organisatie-eenheden
Nu dat u een aangepaste organisatie-eenheid hebt gemaakt, kunt u doorgaan en gebruikers, groepen, computers en serviceaccounts maken in deze organisatie-eenheid. U kunt gebruikers of groepen niet verplaatsen vanuit Hallo 'AADDC gebruikers' OE toocustom organisatie-eenheden.

> [!WARNING]
> Gebruikersaccounts, groepen, service-accounts en computerobjecten die u op aangepaste OE's maakt zijn niet beschikbaar in uw Azure AD-tenant. Met andere woorden, weergeven deze objecten niet met behulp van hello Azure AD Graph API of in hello Azure AD-gebruikersinterface. Deze objecten zijn alleen beschikbaar in uw beheerde domein van Azure AD Domain Services.
>
>

## <a name="related-content"></a>Gerelateerde inhoud
* [Een beheerd domein van Azure AD Domain Services beheren](active-directory-ds-admin-guide-administer-domain.md)
* [Groepsbeleid configureren op een beheerd domein](active-directory-ds-admin-guide-administer-group-policy.md)
* [Active Directory-beheercentrum: Aan de slag](https://technet.microsoft.com/library/dd560651.aspx)
* [Stapsgewijze handleiding voor Service-Accounts](https://technet.microsoft.com/library/dd548356.aspx)
