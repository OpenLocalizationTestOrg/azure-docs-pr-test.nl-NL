---
title: aaaClassic portal Azure AD-toepassingsproxy connectors | Microsoft Docs
description: Dekt hoe toocreate en beheren van groepen van connectors in Azure AD-toepassingsproxy.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b283796a-9679-4c79-b703-802bb850f65d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 43559b0f4ffc3c7dbbf00901e89ac276d01796e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a>Publiceren van toepassingen op afzonderlijke netwerken en locaties met groepen van de connector
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-application-proxy-connectors-azure-portal.md)
> * [Klassieke Azure Portal](active-directory-application-proxy-connectors.md)
>
>

Connector-groepen zijn handig voor verschillende scenario's, waaronder:

* -Sites met meerdere onderling verbonden datacenters. In dit geval u tookeep zoveel verkeer binnen Hallo datacenter mogelijk omdat cross-datacenter koppelingen dure en traag zijn. U kunt connectoren in elk datacenter tooserve alleen Hallo toepassingen die zich bevinden in Hallo datacenter kunt implementeren. Deze aanpak minimaliseert cross-datacenter koppelingen en biedt een volledig transparant ervaring tooyour gebruikers.
* Het beheren van toepassingen die zijn geïnstalleerd op de geïsoleerde netwerken die geen deel uitmaken van de belangrijkste bedrijfsnetwerk Hallo. U kunt connector groepen tooinstall dedicated connectors in geïsoleerde netwerken tooalso isoleren toepassingen toohello netwerk gebruiken.
* Toepassingen die zijn geïnstalleerd op IaaS voor toegang tot de cloud, bieden connector groepen een algemene service toosecure Hallo toegang tooall Hallo-apps. Groepen van de connector geen extra afhankelijkheid in uw bedrijfsnetwerk maken of fragment Hallo van apps. Connectors kunnen worden geïnstalleerd op elke clouddatacenter en dienen alleen toepassingen die zich in dit netwerk bevinden. U kunt verschillende connectors tooachieve hoge beschikbaarheid installeren.
* Ondersteuning voor meerdere forests omgevingen waarin specifieke connectors kunnen worden geïmplementeerd per forest en tooserve specifieke toepassingen ingesteld.
* Connector-groepen kunnen worden gebruikt in herstel na noodgevallen sites tooeither failover detecteren of als back-up voor Hallo belangrijkste site.
* Groepen van de connector kunnen ook worden gebruikt tooserve meerdere bedrijven van een enkele tenant.

## <a name="prerequisite-create-your-connectors"></a>Voorwaarde: Uw connectors maken
toogroup uw connectors [meerdere connectors installeren](active-directory-application-proxy-enable.md), geef de naam en ze te groeperen. Ten slotte het hebben van tooassign ze toospecific apps.

## <a name="step-1-create-connector-groups"></a>Stap 1: Connector groepen maken
U kunt zoveel connector groepen als u wilt maken. Het maken van connector wordt uitgevoerd in Hallo klassieke Azure-portal.

1. Selecteer uw directory en klik op **configureren**.  
    ![Toepassingsproxy, schermafbeelding configureren: klik op de connector-groepen beheren](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)
2. Klik onder Application Proxy op **Connector groepen beheren** en maakt u een groep connector door Hallo groep een naam geven.  
    ![Connector voor toepassingsproxy schermafbeelding - groep voor de nieuwe groepen](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)

## <a name="step-2-assign-connectors-tooyour-groups"></a>Stap 2: Toewijzen connectors tooyour groepen
Als Hallo connector groepen zijn gemaakt, verplaatst u Hallo connectors toohello juiste groep.

1. Onder **toepassingsproxy**, klikt u op **Connectors beheren**.
2. Onder **groep**, selecteer Hallo groep die u voor elke connector. Het kan Hallo connectors up too10 minuten toobecome actief is in de nieuwe groep Hallo duren.  
    ![Schermafbeelding van Application proxy connectors - selecte groep uit de vervolgkeuzelijst](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)

## <a name="step-3-assign-applications-tooyour-connector-groups"></a>Stap 3: Toepassingen tooyour connector groepen toewijzen
de laatste stap Hallo tooset wordt elke toepassing toohello connector groepen die aan deze.

1. In de klassieke Azure-portal in uw directory Hallo Selecteer toepassing die u wilt dat tooassign toohello groep en klikt u op Hallo **configureren**.
2. Onder **Connector groep**, selecteer gewenste toepassing toouse Hallo Hallo-groep. Deze wijziging wordt onmiddellijk toegepast.  
    ![Application proxy connector groep schermafbeelding - selecte groep uit de vervolgkeuzelijst](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)

## <a name="see-also"></a>Zie ook
* [Toepassingsproxy inschakelen](active-directory-application-proxy-enable.md)
* [Eenmalige aanmelding inschakelen](active-directory-application-proxy-sso-using-kcd.md)
* [Voorwaardelijke toegang inschakelen](active-directory-application-proxy-conditional-access.md)
* [Oplossen van problemen met toepassingsproxy](active-directory-application-proxy-troubleshoot.md)

Bekijk voor Hallo laatste nieuws en updates Hallo [blog over toepassingsproxy](http://blogs.technet.com/b/applicationproxyblog/)
