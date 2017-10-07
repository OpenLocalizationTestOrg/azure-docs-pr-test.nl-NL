---
title: een Azure Active Directory met behulp van verbonden Services in Visual Studio aaaAdding | Microsoft Docs
description: Een Azure Active Directory toevoegen via Hallo Visual Studio verbonden dialoogvenster Services toevoegen
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f599de6b-e369-436f-9cdc-48a0165684cb
ms.service: active-directory
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: kraigb
ms.openlocfilehash: 26c8f68edf9ec5f7bf65cbab34e4f9b4085ed18d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-an-azure-active-directory-by-using-connected-services-in-visual-studio"></a>Een Azure Active Directory toe te voegen met behulp van verbonden Services in Visual Studio
Met behulp van Azure Active Directory (Azure AD), kunt u eenmalige aanmelding (SSO) voor ASP.NET MVC-webtoepassingen of Active Directory-verificatie te ondersteunen in een Web API-services. Met Azure Active Directory-verificatie, kunnen uw gebruikers kunnen hun accounts van Azure Active Directory tooconnect tooyour webtoepassingen gebruiken. Hallo voordelen van Azure Active Directory-verificatie met Web-API bevatten verbeterde gegevensbeveiliging wanneer het blootstellen van een API vanuit een webtoepassing. Met Azure AD, hoeft u geen toomanage een afzonderlijke verificatiesysteem met een eigen account en gebruiker management.

## <a name="prerequisites"></a>Vereisten
- Azure-account: als u geen Azure-account, kunt u [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) of [uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

### <a name="connect-tooazure-active-directory-using-hello-connected-services-dialog"></a>Verbinding maken met Active Directory met Hallo verbonden Services tooAzure dialoogvenster
1. Maken of openen van een ASP.NET MVC-project of een ASP.NET Web API-project in Visual Studio.

1. Met de rechtermuisknop op Hallo van Hallo Solution Explorer, **verbonden Services** knooppunt, en selecteer in het contextmenu hello, **verbonden Services toevoegen**.

1. Op Hallo **verbonden Services** pagina **verificatie met Azure Active Directory**.
   
    ![Pagina verbonden Services](./media/vs-azure-tools-connected-services-add-active-directory/connected-services-add-active-directory.png)

1. Op Hallo **inleiding** pagina Hallo **configureren Azure AD Authentication** wizard selecteert u **volgende**.
   
    ![Introductiepagina](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-1.png)

1. Op Hallo **eenmalige aanmelding op** pagina Hallo **configureren Azure AD Authentication** wizard, selecteert u een domein via Hallo **domein** vervolgkeuzelijst. Hallo-lijst met domeinen bevat alle domeinen die toegankelijk is door Hallo-accounts die worden vermeld in Hallo Accountinstellingen dialoogvenster. Als alternatief kunt u een domeinnaam kunt invoeren als u geen vindt Hallo u, zoals zoekt `mydomain.onmicrosoft.com`. U kunt kiezen Hallo optie toocreate van een Azure Active Directory-app of Hallo-instellingen van een bestaande Azure Active Directory-app gebruiken. Selecteer **volgende** wanneer u klaar bent.
   
    ![Eenmalige aanmelding op de pagina](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-2.png)

1. Op Hallo **maptoegang** pagina Hallo **configureren Azure AD Authentication** wizard ervoor te zorgen dat Hallo **mapgegevens lezen** optie is ingeschakeld. 
   
    ![Directorypagina-toegang](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-3.png)

1. Selecteer **voltooien** tooadd Hallo vereiste configuratie code en verwijzingen tooenable uw project voor Azure AD-verificatie. U ziet Hallo Active Directory-domein op Hallo [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Visual Studio, ziet u een [wat is er gebeurd](#how-your-project-is-modified) artikel tooshow u hoe uw project is gewijzigd. Als u toocheck dat alles gewerkt wilt, opent u een van de configuratiebestanden Hallo gewijzigd en controleer of Hallo-instellingen die zijn vermeld in artikel Hallo zijn er. 

## <a name="how-your-project-is-modified"></a>Hoe uw project is gewijzigd
Wanneer u Hallo-wizard uitvoert, wordt in Visual Studio Azure Active Directory en de bijbehorende verwijzingen tooyour project toegevoegd. Configuratiebestanden en codebestanden in uw project zijn ook gewijzigde tooadd ondersteuning voor Azure AD. Hallo specifieke wijzigingen die Visual Studio maakt, is afhankelijk van het projecttype Hallo. Zie voor gedetailleerde informatie over hoe ASP.NET MVC-projecten zijn gewijzigd, [welke happened – MVC projecten](http://go.microsoft.com/fwlink/p/?LinkID=513809). Zie voor een Web API-projecten [wat is er gebeurd – Web API-projecten](http://go.microsoft.com/fwlink/p/?LinkId=513810).

## <a name="next-steps"></a>Volgende stappen
* [MSDN-Forum voor Azure Active Directory](https://social.msdn.microsoft.com/forums/azure/home?forum=WindowsAzureAD)
* [Azure Active Directory-documentatie](https://azure.microsoft.com/documentation/services/active-directory/)
* [Blogbericht: Inleiding tooAzure Active Directory](http://blogs.msdn.com/b/brunoterkaly/archive/2014/03/03/introduction-to-windows-azure-active-directory.aspx)

