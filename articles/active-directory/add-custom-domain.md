---
title: een aangepast domein tooAzure AD aaaAdd | Microsoft Docs
description: Legt uit hoe tooadd een aangepast domein in Azure Active Directory.
services: active-directory
author: jeffgilb
manager: femila
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 878cecad364ec47f1c6755d742aaccbce627dc5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-a-custom-domain-name-tooazure-active-directory"></a>Snelstartgids: Een aangepast domein naam tooAzure Active Directory toevoegen

Elke Azure AD-directory wordt geleverd met een initiële domeinnaam in de vorm van Hallo *domainname*. onmicrosoft.com. Hallo initiële domeinnaam kan niet worden gewijzigd of verwijderd, maar u kunt uw bedrijfsdomein naam tooAzure AD ook toevoegen. Uw organisatie heeft bijvoorbeeld waarschijnlijk andere domein namen gebruikt toodo bedrijfs- en gebruikers die zich aanmeldt met uw zakelijke domeinnaam. Toevoegen van aangepast domein namen tooAzure AD kunt u tooassign gebruikersnamen in Hallo directory die bekend tooyour gebruikers, zoals 'alice@contoso.com.' in plaats van ' Els @*<domain name>*. onmicrosoft.com'. Hallo-proces is eenvoudig:

1. Hallo aangepast domein naam tooyour map toevoegen
2. Een DNS-vermelding voor de domeinnaam Hallo op Hallo domeinnaamregistrar toevoegen
3. Controleer of de aangepaste domeinnaam Hallo in Azure AD

## <a name="add-your-custom-domain"></a>Uw aangepaste domein toevoegen
1. Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.
2. Selecteer **meer services**, voer **Azure Active Directory** in het tekstvak Hallo en selecteer vervolgens **Enter**.
   
   ![Gebruikersbeheer openen](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Op Hallo ***mapnaam*** blade Selecteer **domeinnamen**.
4. Op Hallo  ***mapnaam* -domeinnamen** blade, selecteer Hallo **toevoegen** opdracht.
   
   ![Hallo Add-opdracht selecteren](./media/active-directory-domains-add-azure-portal/add-command.png)
5. Op Hallo **domeinnaam** blade Hallo-naam van uw aangepaste domein in Hallo vak opgeven, bijvoorbeeld 'contoso.com' en selecteer vervolgens **domein toevoegen**. Ervoor tooinclude Hallo .com, .net of een andere extensie op het hoogste niveau zijn.
6. Op Hallo ***domeinnaam*** blade (met uw aangepaste domeinnaam in Hallo titel), DNS-vermelding informatie toouse tooverify dat uw organisatie eigenaar is van de aangepaste domeinnaam Hallo Hallo ophalen.
   
   ![DNS-vermelding informatie ophalen](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

> [!TIP]
> Als u van plan toofederate uw lokale Windows Server AD met Azure AD bent, moet u tooselect hello **ik rekening houden tooconfigure dit domein voor eenmalige aanmelding met mijn lokale Active Directory** selectievakje wanneer u hello Azure AD Connect-hulpprogramma uitvoert toosynchronize uw adreslijsten. U moet ook tooregister dezelfde domeinnaam die u selecteert voor het federeren met uw on-premises directory in Hallo Hallo **Azure AD Domain** stap in de wizard Hallo. U kunt zien welke stap in het Hallo-wizard lijkt [in deze instructies](./connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation). Als u geen hello Azure AD Connect-hulpprogramma hebt, kunt u [hier downloaden](http://go.microsoft.com/fwlink/?LinkId=615771).

Nu dat u Hallo domeinnaam hebt toegevoegd, moet uw organisatie eigenaar is van de domeinnaam Hallo Azure AD controleren. Azure AD om deze verificatie te kan uitvoeren, moet u een DNS-vermelding toevoegen in Hallo DNS-zonebestand voor Hallo domeinnaam. Deze taak wordt uitgevoerd op Hallo-website voor domeinnaamregistrar voor Hallo domeinnaam.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Hallo DNS-vermelding op Hallo domeinnaamregistrar voor Hallo domein toevoegen
Hallo volgende stap toouse uw aangepaste domeinnaam met Azure AD is tooupdate Hallo DNS-zonebestand voor Hallo-domein. Azure AD kunt vervolgens controleren of uw organisatie eigenaar is van de aangepaste domeinnaam Hallo.

1. Meld u aan toohello domeinnaamregistrar voor Hallo-domein. Als u geen toegang tot tooupdate Hallo DNS-vermelding, vraagt u Hallo persoon of het team dat deze toegang toocomplete stap 2 is en toolet die u weet wanneer deze is voltooid.
2. Update Hallo DNS-zonebestand voor Hallo domein door toe te voegen Hallo DNS-vermelding opgegeven tooyou door Azure AD. Deze DNS-vermelding kan Azure AD tooverify u eigenaar bent van Hallo-domein. Hallo DNS-vermelding is niet gewijzigd gedrag van bijvoorbeeld mailroutering of webhosting.

Lees voor meer informatie over deze toe te voegen DNS-vermelding voor hello, [instructies voor het toevoegen van een DNS-vermelding bij populaire DNS-registrars](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Controleer of de domeinnaam Hallo met Azure AD
Nadat u Hallo DNS-vermelding hebt toegevoegd, bent u klaar tooverify Hallo domeinnaam met Azure AD.

De naam van een domein kan worden gecontroleerd nadat de Hallo DNS-records zijn doorgegeven. Deze doorgifte duurt vaak slechts enkele seconden, maar het kan ook wel eens een uur of langer duren. Als verificatie niet Hallo eerst werkt, probeer het later opnieuw.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.
2. Selecteer **Bladeren**Gebruikersbeheer invoeren in het tekstvak Hallo en selecteer vervolgens **Enter**.
   
   ![Gebruikersbeheer openen](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Op Hallo **Gebruikersbeheer - domeinnamen** blade, selecteer Hallo niet-geverifieerde domeinnaam die u tooverify wilt.
4. Op Hallo ***domeinnaam*** blade (dat wil zeggen, Hallo blade die wordt geopend met de naam van het nieuwe domein in Hallo titel), selecteer **controleren** toocomplete Hallo verificatie.

> [!TIP]
> U kunt toevoegen, too900 aangepaste domeinnamen, maar slechts één [instellen als primaire Hallo-domeinnaam voor uw Azure AD-directory](active-directory-domains-manage-azure-portal.md#set-the-primary-domain-name-for-your-azure-ad-directory) gebruikt standaard bij het maken van nieuwe accounts.

Nu kunt u cloud-gebaseerde gebruikersaccounts of update eerder gesynchroniseerd lokale gebruikersaccountgegevens met behulp van uw aangepaste domeinnaam. U kunt ook wijzigen eerder gesynchroniseerde gebruikersaccount domein achtervoegsel informatie met [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) of Hallo [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="troubleshooting"></a>Problemen oplossen
Als u een aangepaste domeinnaam niet kan controleren, probeert u Hallo stappen te volgen:

1. **Wacht een uur**. DNS-records moeten toopropagate voordat u Azure AD domain Hallo kunt controleren. Dit kan een uur of langer duren.
2. **Zorg ervoor dat Hallo DNS-record is ingevoerd en of deze juist is**. Deze stap op Hallo-website voor domeinnaamregistrar voor domein Hallo Hallo hebt voltooid. Azure AD kan Hallo domeinnaam niet controleren als Hallo DNS-vermelding niet is aanwezig zijn op Hallo DNS-zonebestand, of als het is niet exact overeen met de Hallo DNS-vermelding die Azure AD u opgegeven. Als u geen toegang tot tooupdate DNS-records voor Hallo domein op Hallo domeinnaamregistrar, Hallo DNS-vermelding delen met Hallo persoon die of het team van uw organisatie die deze toegang heeft en vraagt u ze tooadd Hallo DNS-vermelding.
3. **Hallo-domeinnaam verwijderen uit een andere map in Azure AD**. Een domeinnaam kan maar in één map worden geverifieerd. Als een domeinnaam eerder is geverifieerd in een andere map, moet de domeinnaam daar eerst uit worden verwijderd voordat deze kan worden geverifieerd in een nieuwe map. toolearn over het verwijderen van domeinnamen gelezen [aangepaste domeinnamen beheren](active-directory-domains-manage-azure-portal.md).    

## <a name="add-more-custom-domain-names"></a>Meer aangepaste domeinnamen toevoegen
Als uw organisatie gebruikmaakt van meer dan een aangepaste domeinnaam, zoals 'contoso.com' en 'contosobank.com', kunt u meer up too900 toevoegen door de stappen in dit artikel Hallo herhalen voor elk.

### <a name="learn-more"></a>Meer informatie
[Conceptueel overzicht van aangepaste domeinnamen in Azure AD](active-directory-add-domain-concepts.md)

[Aangepaste domeinnamen beheren](active-directory-domains-manage-azure-portal.md)


## <a name="next-steps"></a>Volgende stappen
In deze snelstartgids hebt u geleerd hoe tooadd een aangepast domein tooAzure AD. 

U kunt Hallo volgende koppeling tooadd een nieuw aangepast domein in Azure AD uit hello Azure-portal gebruiken.

> [!div class="nextstepaction"]
> [Een aangepast domein toevoegen](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/QuickStart) 