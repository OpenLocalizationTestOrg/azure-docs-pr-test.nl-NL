---
title: Een aangepast domein toevoegen aan Azure AD | Microsoft Docs
description: Legt uit hoe u een aangepast domein toevoegen in Azure Active Directory.
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
ms.openlocfilehash: 4848130601ffa18ed1565e79cb0f0db3274e950f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="quickstart-add-a-custom-domain-name-to-azure-active-directory"></a>Snelstartgids: Een aangepaste domeinnaam toevoegen aan Azure Active Directory

Elke Azure AD-directory wordt geleverd met een initiële domeinnaam in de vorm van *domainname*. onmicrosoft.com. De initiële domeinnaam kan niet worden gewijzigd of verwijderd, maar u kunt uw zakelijke domeinnaam toevoegen aan Azure AD ook. Uw organisatie heeft bijvoorbeeld waarschijnlijk andere domeinnamen gebruikt voor bedrijven en gebruikers die zich aanmeldt met uw zakelijke domeinnaam. Het toevoegen van aangepaste domeinnamen naar Azure AD, kunt u gebruikersnamen toewijzen in de directory die bekend aan uw gebruikers, zoals zijn 'alice@contoso.com.' in plaats van ' Els @*<domain name>*. onmicrosoft.com'. Het proces is eenvoudig:

1. Voeg de aangepaste domeinnaam toe aan uw directory.
2. Voeg een DNS-vermelding voor de domeinnaam toe aan de domeinnaamregistrar.
3. Verifieer de aangepaste domeinnaam in Azure AD.

## <a name="add-your-custom-domain"></a>Uw aangepaste domein toevoegen
1. Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.
2. Selecteer **meer services**, voer **Azure Active Directory** in het tekstvak in en selecteer vervolgens **Enter**.
   
   ![Gebruikersbeheer openen](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Op de ***mapnaam*** blade Selecteer **domeinnamen**.
4. Op de  ***mapnaam* -domeinnamen** blade, selecteer de **toevoegen** opdracht.
   
   ![De opdracht Add selecteren](./media/active-directory-domains-add-azure-portal/add-command.png)
5. Op de **domeinnaam** blade, voer de naam van uw aangepaste domein in het vak, bijvoorbeeld 'contoso.com' en selecteer vervolgens **domein toevoegen**. Vergeet niet de extensie .com, .net of een andere extensie van het hoogste niveau toe te voegen.
6. Op de ***domeinnaam*** blade (met uw aangepaste domeinnaam in de titel), de DNS-vermeldingsgegevens gebruiken om te verifiëren dat uw organisatie eigenaar is van de aangepaste domeinnaam ophalen.
   
   ![DNS-vermelding informatie ophalen](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

> [!TIP]
> Als u van plan bent om te federeren van uw lokale Windows Server AD met Azure AD, moet u selecteert de **ik van plan bent dit domein te configureren voor eenmalige aanmelding met mijn lokale Active Directory** selectievakje wanneer u het Azure AD Connect-hulpprogramma om te worden uitgevoerd Synchroniseer uw mappen. U moet ook registreren van de dezelfde domeinnaam die u selecteert voor het federeren met uw on-premises directory in de **Azure AD Domain** stap in de wizard. [In deze instructies](./connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation) ziet u hoe die stap van de wizard eruitziet. Als u het hulpprogramma Azure AD Connect niet hebt, kunt u het [hier](http://go.microsoft.com/fwlink/?LinkId=615771) downloaden.

Nu u een domeinnaam hebt toegevoegd, moet met Azure AD worden gecontroleerd of uw organisatie de eigenaar is van de domeinnaam. Voordat deze verificatie met Azure AD kan worden uitgevoerd, moet u een DNS-vermelding toevoegen in het DNS-zonebestand voor de domeinnaam. Deze taak wordt voor de domeinnaam uitgevoerd op de website voor domeinnaamregistrar.

## <a name="add-the-dns-entry-at-the-domain-name-registrar-for-the-domain"></a>De DNS-vermelding op de domeinnaamregistrar voor het domein toevoegen
De volgende stap voor het gebruik van de aangepaste domeinnaam met Azure AD bestaat uit het bijwerken van het DNS-zonebestand voor het domein. Azure AD kunt vervolgens controleren of uw organisatie eigenaar is van de aangepaste domeinnaam.

1. Meld u aan bij de domeinnaamregistrar voor het domein. Als u geen toegang hebt om de DNS-vermelding bij te werken, vraagt u de persoon die of het team dat wel over deze toegang beschikt om stap 2 uit te voeren en u te laten weten wanneer deze is voltooid.
2. Werk het DNS-zonebestand voor het domein bij, door de DNS-vermelding toe te voegen die u van Azure AD hebt ontvangen. Met deze DNS-vermelding kan Azure AD controleren of u eigenaar bent van het domein. De DNS-vermelding leidt niet tot veranderingen in het gedrag van bijvoorbeeld mailroutering of webhosting.

Voor hulp bij het toevoegen van de DMS-vermelding leest u de [Instructies voor het toevoegen van een DNS-vermelding bij populaire DNS-registrars](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/).

## <a name="verify-the-domain-name-with-azure-ad"></a>De domeinnaam verifiëren met Azure AD
Nadat u de DNS-vermelding hebt toegevoegd, kunt u de domeinnaam bij Azure AD verifiëren.

De naam van een domein kan worden gecontroleerd nadat de DNS-records zijn doorgegeven. Deze doorgifte duurt vaak slechts enkele seconden, maar het kan ook wel eens een uur of langer duren. Als de verificatie de eerste keer niet werkt, probeer het dan later nog eens.

1. Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.
2. Selecteer **Bladeren**Gebruikersbeheer invoeren in het tekstvak en selecteer vervolgens **Enter**.
   
   ![Gebruikersbeheer openen](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Op de **Gebruikersbeheer - domeinnamen** blade, selecteer de niet-geverifieerde domeinnaam die u wilt controleren.
4. Op de ***domeinnaam*** blade (dat wil zeggen, de blade die wordt geopend met de naam van het nieuwe domein in de titel), selecteer **controleren** om de verificatie te voltooien.

> [!TIP]
> U kunt maximaal 900 aangepaste domeinnamen toevoegen, maar slechts één [ingesteld als de primaire domeinnaam voor uw Azure AD-directory](active-directory-domains-manage-azure-portal.md#set-the-primary-domain-name-for-your-azure-ad-directory) gebruikt standaard bij het maken van nieuwe accounts.

Nu kunt u cloud-gebaseerde gebruikersaccounts of update eerder gesynchroniseerd lokale gebruikersaccountgegevens met behulp van uw aangepaste domeinnaam. U kunt ook wijzigen eerder gesynchroniseerde gebruikersaccount domein achtervoegsel informatie met [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) of de [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="troubleshooting"></a>Problemen oplossen
Als u een aangepaste domeinnaam niet kan controleren, voert u de volgende probleemoplossingsstappen uit:

1. **Wacht een uur**. DNS-records moeten zijn doorgegeven voordat Azure AD het domein kan verifiëren. Dit kan een uur of langer duren.
2. **Controleer of de DNS-record is opgegeven en of deze juist is**. Voer deze stap uit op de website van de domeinnaamregistrar voor het domein. Azure AD kan de domeinnaam niet verifiëren als de DNS-vermelding niet aanwezig is in het DNS-zonebestand of als deze niet exact overeenkomt met de DNS-vermelding die u van Azure AD hebt gekregen. Als u geen toegang hebt tot de site van de domeinnaamregistrar om de DNS-records voor het domein bij te werken, deel de DNS-vermelding dan met de persoon die of het team dat in uw organisatie deze toegang heeft en vraag om de DNS-vermelding toe te voegen.
3. **Verwijder de domeinnaam uit andere mappen in Azure AD**. Een domeinnaam kan maar in één map worden geverifieerd. Als een domeinnaam eerder is geverifieerd in een andere map, moet de domeinnaam daar eerst uit worden verwijderd voordat deze kan worden geverifieerd in een nieuwe map. Zie [Aangepaste domeinnamen beheren](active-directory-domains-manage-azure-portal.md) voor meer informatie over het verwijderen van domeinnamen.    

## <a name="add-more-custom-domain-names"></a>Meer aangepaste domeinnamen toevoegen
Als uw organisatie gebruikmaakt van meer dan een aangepaste domeinnaam, zoals 'contoso.com' en 'contosobank.com', kunt u maximaal 900 meer door de stappen in dit artikel te herhalen voor elk kunt toevoegen.

### <a name="learn-more"></a>Meer informatie
[Conceptueel overzicht van aangepaste domeinnamen in Azure AD](active-directory-add-domain-concepts.md)

[Aangepaste domeinnamen beheren](active-directory-domains-manage-azure-portal.md)


## <a name="next-steps"></a>Volgende stappen
In deze snelstartgids hebt u geleerd hoe u een aangepast domein toevoegen aan Azure AD. 

De volgende koppeling kunt u een nieuw aangepast domein toevoegen in Azure AD via de Azure-portal.

> [!div class="nextstepaction"]
> [Een aangepast domein toevoegen](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/QuickStart) 