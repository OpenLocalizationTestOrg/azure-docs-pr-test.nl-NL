---
title: Uw aangepaste domeinnaam toevoegen aan Azure Active Directory | Microsoft Docs
description: "Hier leest u hoe u de domeinnamen van uw bedrijf kunt toevoegen aan Azure Active Directory en hoe u de domeinnaam kunt verifiëren."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d97e57c6-578a-4929-8fb8-42e858a711c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: ad72f768add7edc1d34a85c27dc2aa1b4e4b3a50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="add-a-custom-domain-name-to-azure-active-directory"></a>Een aangepaste domeinnaam toevoegen aan Azure Active Directory
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-domains-add-azure-portal.md)
> * [Klassieke Azure Portal](active-directory-add-domain.md)
> 

Met Azure Active Directory (Azure AD), kunt u uw zakelijke domeinnaam toevoegen aan Azure AD ook. U hebt mogelijk een domeinnamen die door uw organisatie worden gebruikt voor bedrijven en gebruikers die zich aanmeldt met uw zakelijke domeinnaam. De domeinnaam toevoegen aan Azure AD, kunt u gebruikersnamen toewijzen in de directory die bekend aan uw gebruikers, zoals zijn 'alice@contoso.com.' Het proces is eenvoudig:

1. Voeg de aangepaste domeinnaam toe aan uw directory.
2. Voeg een DNS-vermelding voor de domeinnaam toe aan de domeinnaamregistrar.
3. Verifieer de aangepaste domeinnaam in Azure AD.

## <a name="how-do-i-add-a-domain-name"></a>Hoe kan ik een domeinnaam toevoegen
1. Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.
2. Selecteer **meer services**, voer **Azure Active Directory** in het tekstvak in en selecteer vervolgens **Enter**.
   
   ![Gebruikersbeheer openen](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Op de ***mapnaam*** blade Selecteer **domeinnamen**.
4. Op de  ***mapnaam* -domeinnamen** blade, selecteer de **toevoegen** opdracht.
   
   ![De opdracht Add selecteren](./media/active-directory-domains-add-azure-portal/add-command.png)
5. Op de **domeinnaam** blade, voer de naam van uw aangepaste domein in het vak, bijvoorbeeld 'contoso.com' en selecteer vervolgens **domein toevoegen**. Vergeet niet de extensie .com, .net of een andere extensie van het hoogste niveau toe te voegen.
6. Op de ***domainname*** blade (dat wil zeggen, de blade die wordt geopend met de naam van het nieuwe domein in de titel), de DNS-vermeldingsgegevens die door Azure AD wordt gebruikt om te controleren of uw organisatie eigenaar is van de aangepaste domeinnaam ophalen.
   
   ![DNS-vermelding informatie ophalen](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

Nu u een domeinnaam hebt toegevoegd, moet met Azure AD worden gecontroleerd of uw organisatie de eigenaar is van de domeinnaam. Voordat deze verificatie met Azure AD kan worden uitgevoerd, moet u een DNS-vermelding toevoegen in het DNS-zonebestand voor de domeinnaam. Deze taak wordt voor de domeinnaam uitgevoerd op de website voor domeinnaamregistrar.

## <a name="add-the-dns-entry-at-the-domain-name-registrar-for-the-domain"></a>De DNS-vermelding op de domeinnaamregistrar voor het domein toevoegen
De volgende stap voor het gebruik van de aangepaste domeinnaam met Azure AD bestaat uit het bijwerken van het DNS-zonebestand voor het domein. Hierdoor kan Azure AD verifiëren of uw organisatie eigenaar is van de aangepaste domeinnaam.

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
4. Op de ***domainname*** blade (dat wil zeggen, de blade die wordt geopend met de naam van het nieuwe domein in de titel), selecteer **controleren** om de verificatie te voltooien.

Nu kunt u [gebruikersnamen toewijzen die uw aangepaste domeinnaam omvatten](active-directory-users-create-azure-portal.md).

## <a name="troubleshooting"></a>Problemen oplossen
Als u een aangepaste domeinnaam niet kunt verifiëren, probeert u het volgende. We beginnen met de meest voorkomende en werken de lijst af naar de minst voorkomende.

1. **Wacht een uur**. DNS-records moeten zijn doorgegeven voordat Azure AD het domein kan verifiëren. Dit kan een uur of langer duren.
2. **Controleer of de DNS-record is opgegeven en of deze juist is**. Voer deze stap uit op de website van de domeinnaamregistrar voor het domein. Azure AD kan de domeinnaam niet verifiëren als de DNS-vermelding niet aanwezig is in het DNS-zonebestand of als deze niet exact overeenkomt met de DNS-vermelding die u van Azure AD hebt gekregen. Als u geen toegang hebt tot de site van de domeinnaamregistrar om de DNS-records voor het domein bij te werken, deel de DNS-vermelding dan met de persoon die of het team dat in uw organisatie deze toegang heeft en vraag om de DNS-vermelding toe te voegen.
3. **Verwijder de domeinnaam uit andere mappen in Azure AD**. Een domeinnaam kan maar in één map worden geverifieerd. Als een domeinnaam eerder is geverifieerd in een andere map, moet de domeinnaam daar eerst uit worden verwijderd voordat deze kan worden geverifieerd in een nieuwe map. Zie [Aangepaste domeinnamen beheren](active-directory-domains-manage-azure-portal.md) voor meer informatie over het verwijderen van domeinnamen.    

## <a name="add-more-custom-domain-names"></a>Meer aangepaste domeinnamen toevoegen
Als uw organisatie meerdere aangepaste domeinnamen gebruikt, zoals contoso.com en contosobank.com, kunt u tot maximaal 900 domeinnamen toevoegen. Gebruik dezelfde stappen in dit artikel om elke domeinnaam toe te voegen.

## <a name="next-steps"></a>Volgende stappen
[Aangepaste domeinnamen beheren](active-directory-domains-manage-azure-portal.md)

