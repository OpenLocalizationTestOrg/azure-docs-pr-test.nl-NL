---
title: aaaHow toouse een overzicht van Azure Active Direcory tenant directory | Microsoft Docs
description: Wordt uitgelegd wat een Azure AD-tenant is, en hoe toomanage Azure met Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: it-pro;oldportal
ms.openlocfilehash: ddb16d89bf06a3753ed5106bd95162130ad51b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-ad-directory"></a>Uw Azure AD-directory beheren

## <a name="what-is-an-azure-ad-tenant"></a>Wat is een Azure AD-tenant?
In Azure Active Directory (Azure AD) is een tenant het exclusieve exemplaar van een Azure Active-directory dat uw organisatie na aanmelding voor een Microsoft-cloudservice (zoals Azure of Office 365) krijgt toegewezen. Elke Azure AD-directory is uniek en werkt afzonderlijk van andere Azure AD-directory’s. Net zoals een kantoorgebouw is een specifieke tooonly beveiligd bedrijfsmiddel is van uw organisatie, er is ook een Azure AD-directory ontworpen toobe een beveiligd bedrijfsmiddel alleen door uw organisatie. Hello Azure AD-architectuur isoleert klant- en identiteitsgegevens informatie zodat gebruikers en beheerders van een Azure AD-directory kunnen niet per ongeluk of opzettelijk toegang gegevens in een andere map tot.

![Azure Active Directory beheren](./media/active-directory-administer/aad_portals.png)

## <a name="how-can-i-get-an-azure-ad-directory"></a>Hoe krijg ik een Azure AD-directory?
Azure AD levert Hallo core directory- en identiteitsbeheer identiteitsbeheermogelijkheden voor de meeste Microsoft cloud-services, waaronder:

* Azure
* Microsoft Office 365
* Microsoft Dynamics CRM Online
* Microsoft Intune

U krijgt een Azure AD-directory wanneer u zich aanmeldt voor een van deze Microsoft-cloudservices. U kunt naar behoefte aanvullende directory’s maken. Zo kunt u bijvoorbeeld uw eerste directory gebruiken als productiedirectory en nog een tweede directory maken voor testen en fasering.

### <a name="using-hello-azure-ad-directory-that-comes-with-a-new-azure-subscription"></a>Met behulp van hello Azure AD-directory die wordt geleverd met een nieuwe Azure-abonnement

Het is raadzaam dat u Hallo administrator-account die u hebt voor uw eerste service hebt gebruikt toen u zich aanmeldt voor andere Microsoft-services. Hallo informatie die u verstrekt Hallo eerste keer dat u zich aanmeldt voor een Microsoft-service gebruikte toocreate een nieuwe Azure is AD-directory-exemplaar voor uw organisatie. Als u dat directory tooauthenticate aanmelden wanneer u zich abonneert tooother Microsoft-services, kunt u Hallo bestaande gebruikersaccounts, beleidsregels, instellingen of on-premises directory-integratie die u in de standaardmap configureren.

Bijvoorbeeld, als u zich aanmeldt voor een abonnement op Microsoft Intune en uw lokale Active Directory verder met uw Azure AD-directory te synchroniseren, u kunt zich aanmelden voor een andere Microsoft-service zoals Office 365 en eenvoudig bereiken Hallo dezelfde directory voordelen voor integratie met Microsoft Intune.

Zie [Uw on-premises directory's integreren met Azure Active Directory](active-directory-aadconnect.md) voor meer informatie over de integratie van uw on-premises directory in Azure AD.

### <a name="associate-an-existing-azure-ad-directory-with-a-new-azure-subscription"></a>Een bestaande Azure AD-directory koppelen aan een nieuw Azure-abonnement
U kunt een nieuwe Azure-abonnement koppelen aan Hallo dezelfde directory waarmee wordt geverifieerd aanmelden voor een bestaand Office 365 of Microsoft Intune-abonnement. Zie voor meer informatie over dit scenario [het eigendom overdraagt van een Azure-abonnement tooanother-account](../billing/billing-subscription-transfer.md)

### <a name="create-an-azure-ad-directory-by-signing-up-for-a-microsoft-cloud-service-as-an-organization"></a>Een Azure AD-directory maken door u als organisatie te registreren voor een Microsoft-cloudservice
Als u nog een abonnement tooa Microsoft-cloudservice hebt, kunt u een van de Hallo koppelingen toosign opvolgen. Als u zich voor uw eerste service registreert, wordt er automatisch een Azure AD-directory gemaakt.

* [Microsoft Azure](https://account.azure.com/organization)
* [Office 365](http://products.office.com/business/compare-office-365-for-business-plans/)
* [Microsoft Intune](https://portal.office.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0%20)

### <a name="how-toochange-hello-default-directory-for-a-subscription"></a>Hoe toochange Hallo standaarddirectory voor een abonnement

1. Meld u aan toohello [Azure-Accountcentrum](https://account.windowsazure.com/Home/Index) met een account dat Hallo accountbeheerder van Hallo abonnement tootransfer abonnement eigendom.
2. Zorg ervoor dat Hallo-gebruiker die u eigenaar toobe Hallo-abonnement is in de map Hallo gericht.
3. Klik op **Abonnement overdragen**.
4. Hallo ontvanger opgeven. Hallo geadresseerde ontvangt automatisch een e-mail met een koppeling acceptatie.
5. Hallo-ontvanger op Hallo koppeling klikt en Hallo instructies gevolgd die zijn, met inbegrip van de betaalgegevens invoeren. Als de ontvanger Hallo is geslaagd, wordt Hallo abonnement overgedragen. 
6. Hallo standaarddirectory van Hallo abonnement wordt gewijzigd toohello directory die gebruiker Hallo wordt als Hallo eigendom abonnementsoverdracht voltooid is.

### <a name="manage-hello-default-directory-in-azure"></a>De standaardmap Hallo in Azure beheren
Wanneer u zich registreert voor Azure, wordt er een standaarddirectory van Azure AD gekoppeld aan uw abonnement. Er zijn geen kosten verbonden aan het gebruik van Azure AD en uw directory's zijn eveneens gratis. Er zijn betaalde Azure AD-services waarvoor een afzonderlijke licentie nodig is en die aanvullende functionaliteit bieden, zoals de huisstijl van het bedrijf in het aanmeldingsscherm en selfservice voor wachtwoordherstel. U kunt ook een aangepast domein met een DNS-naam die u bezit in plaats van standaard Hallo maken *. onmicrosoft.com-domein.

## <a name="how-can-i-manage-directory-data"></a>Hoe kan ik directorygegevens beheren?
tooadminister een of meer Microsoft cloud service-abonnementen, kunt u Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com), Microsoft Intune-accountportal Hallo of Hallo [Office 365-beheercentrum](https://portal.office.com/) toomanage uw directory-gegevens van de organisatie. U kunt ook [Azure Active Directory PowerShell-cmdlets](https://docs.microsoft.com/powershell/azure/active-directory) toohelp u gegevens die zijn opgeslagen in Azure AD beheren.

Via deze portals (en cmdlets) kunt u het volgende doen:

* Accounts voor gebruikers en groepen maken en beheren
* Gerelateerde cloudservices beheren voor de abonnementen van uw organisatie
* On-premises integratie met services van Azure AD voor identiteitscontrole en verificatie instellen

Hello Azure AD-beheercentrum, Office 365-beheercentrum, Microsoft Intune-accountportal en hello Azure AD-cmdlets lezen uit en schrijven van tooa één gedeeld exemplaar van Azure AD dat is gekoppeld aan de directory van uw organisatie. Elk van deze hulpprogramma's fungeert als een front-interface die gegevens in de directory ophaalt of wijzigt.

Wanneer u gegevens van uw organisatie met behulp van een Hallo portals of cmdlets in de context van een van deze services Hallo aangemeld wijzigt, Hallo wijzigingen worden ook weergegeven in Hallo andere portals Hallo wanneer die u zich aanmeldt. Deze gegevens worden verdeeld over Hallo Microsoft cloud services toowhich die u zich hebt geabonneerd.

Bijvoorbeeld als u Hallo Office 365-beheercentrum tooblock een gebruiker zich aanmeldt, die actie blokken Hallo gebruiker tooany andere toowhich service van uw organisatie heeft momenteel abonnement op. Als u hello bekijkt dezelfde gebruikersaccount in Microsoft Intune-accountportal hello, ziet u ook die Hallo-gebruiker is geblokkeerd.

## <a name="how-can-i-add-and-manage-multiple-directories"></a>Hoe kan ik meerdere directory’s toevoegen en beheren?
U kunt [toevoegen van een Azure AD-directory in hello Azure-portal](https://portal.azure.com/#create/Microsoft.AzureActiveDirectory). Hallo gegevens invullen en selecteer **maken**.

U kunt elke directory als volledig onafhankelijke resource beheren: elke directory is een peer, volledig uitgerust en logisch onafhankelijk van andere directory's die u beheert. Er is geen sprake van een structuur met boven- en onderliggende directory's. Onder deze onafhankelijkheid van uw directory’s vallen ook resourceonafhankelijkheid, beheeronafhankelijkheid en synchronisatieonafhankelijkheid.

* **Resourceonafhankelijkheid**. Als u maken of verwijderen van een resource in één directory, heeft dit geen invloed op alle bronnen in andere directory's gedeeltelijke uitzondering Hallo van externe gebruikers. Als u voor een bepaalde directory het aangepaste domein contoso.com gebruikt, kan dit domein niet meer voor andere directory’s worden gebruikt.
* **Beheeronafhankelijkheid**.  Als een gebruiker die geen beheerder is van de directory Contoso een testdirectory Test maakt:
  
  * Beheerders van de map 'Contoso' Hello hebben geen directe beheerdersrechten toodirectory 'Test', tenzij een beheerder van 'Test' specifiek hun deze rechten verleent. Van 'Contoso' kunnen beheerders toegang toodirectory 'Test' doordat hun beheer van gebruikersaccount Hallo die gemaakt van 'Test'.
    
  * Als u toewijzen of verwijderen van een beheerdersrol voor een gebruiker in een bepaalde map, Hallo wijzigen heeft geen invloed op een beheerdersrol wordt die gebruiker mogelijk in een andere map.
* **Synchronisatieonafhankelijkheid**. U kunt elke Azure AD-tenant onafhankelijk tooget gegevens worden gesynchroniseerd vanuit een enkele instantie hello Azure AD Connect directory-synchronisatie.

In tegenstelling tot andere Azure-resources, zijn uw directory's geen onderliggende resources van een Azure-abonnement. Dus als u uw Azure-abonnement tooexpire toestaan of annuleren, u kunt nog steeds toegang tot uw directorygegevens via Azure AD PowerShell, hello Azure Graph API of andere interfaces zoals Hallo Office 365-beheercentrum. U kunt ook een ander abonnement koppelen met Hallo-directory.

## <a name="how-tooprepare-toodelete-an-azure-ad-directory"></a>Hoe tooprepare toodelete een Azure Active directory
Een globale beheerder kunt u een Azure AD-directory verwijderen uit Hallo-portal. Wanneer een map wordt verwijderd, worden ook alle resources die zijn opgenomen in de directory Hallo verwijderd. Controleer of dat u niet nodig Hallo directory voordat u deze verwijdert.

> [!NOTE]
> Als Hallo gebruiker is aangemeld met een account voor werk of school, moet Hallo gebruiker niet proberen toodelete hun oorspronkelijke directory. Bijvoorbeeld, als hello gebruiker is aangemeld als joe@contoso.onmicrosoft.com, kan die gebruiker Hallo-directory die contoso.onmicrosoft.com gebruikt als standaarddomein niet verwijderen.

Azure AD is vereist dat aan bepaalde voorwaarden voldaan toodelete een map wordt. Dit vermindert het risico dat als u een map negatieve heeft gevolgen voor gebruikers of toepassingen, zoals de mogelijkheid Hallo van gebruikers toosign in tooOffice 365 of toegang tot bronnen in Azure. Bijvoorbeeld, als een map voor een abonnement per ongeluk is verwijderd, klikt u vervolgens gebruikers geen toegang tot hello Azure-resources voor dat abonnement.

Hallo volgende voorwaarden worden gecontroleerd:

* Hallo moet alleen Hallo directory-gebruiker hoofdbeheerder Hallo die toodelete Hallo map. Andere gebruikers moeten worden verwijderd voordat de directory Hallo kan worden verwijderd. Als gebruikers on-premises worden gesynchroniseerd en vervolgens synchronisatie moet worden uitgeschakeld en Hallo gebruikers moeten worden verwijderd in Hallo clouddirectory via hello Azure portal of Azure PowerShell-cmdlets. Er is geen vereiste toodelete groepen of contactpersonen, zoals contactpersonen die zijn toegevoegd vanuit Hallo Office 365-beheercentrum.
* Er kunnen geen toepassingen in de map Hallo aanwezig zijn. Alle toepassingen moeten worden verwijderd voordat de directory Hallo kan worden verwijderd.
* Geen multi-factor authentication-providers kunnen gekoppelde toohello directory zijn.
* Kan er geen abonnementen voor Microsoft Online Services zoals Microsoft Azure, Office 365 of Azure AD Premium Hallo directory gekoppeld. Als er bijvoorbeeld een standaarddirectory voor u is gemaakt in Azure, kunt u deze directory niet verwijderen als uw Azure-abonnement deze directory gebruikt voor verificatie. Het is evenmin mogelijk om een directory te verwijderen als een andere gebruiker er een abonnement aan heeft gekoppeld. 


## <a name="next-steps"></a>Volgende stappen
* [Azure AD Forum](https://social.msdn.microsoft.com/Forums/home?forum=WindowsAzureAD)
* [Azure Multi-Factor Authentication-forum](https://social.msdn.microsoft.com/Forums/home?forum=windowsazureactiveauthentication)
* [Vragen over Azure op Stack Overflow (Engelstalig)](http://stackoverflow.com/questions/tagged/azure)
* [Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory)
* [Beheerdersrollen toewijzen in Azure AD](active-directory-assign-admin-roles.md)
