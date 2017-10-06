---
title: Toepassingsproxy van Azure AD-apps in Teams aaaAccess | Microsoft Docs
description: Azure AD-toepassingsproxy tooaccess uw on-premises toepassing via Microsoft-Teams gebruiken.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 13c36e43ae6349df09272e308ad4f40451cbbeb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a>Toegang tot uw on-premises toepassingen via Microsoft-Teams

Azure Active Directory-toepassingsproxy hebt u één aanmelding tooon-premises toepassingen ongeacht waar u zich bevindt en Microsoft-Teams stroomlijnt uw gezamenlijke inspanningen op één plek. Hallo integreren betekent twee samen dat uw gebruikers productiever te maken met hun teamleden in een situatie. 

Uw gebruikers kunnen toevoegen cloud-apps tootheir Teams kanalen [tabbladen](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), maar wat er gebeurt als SharePoint-site of ze allemaal gebruik van hulpprogramma lokale gehost? Toepassingsproxy is Hallo-oplossing. Ze kunnen apps toevoegen gepubliceerd via toepassingsproxy tootheir Hallo kanalen met dezelfde externe URL's die ze altijd tooaccess hun apps op afstand gebruiken. En omdat Application Proxy worden geverifieerd via Azure Active Directory, Hallo dezelfde single sign-on-ervaring via uitvoert.


## <a name="install-hello-application-proxy-connector-and-publish-your-app"></a>Hallo Application Proxy connector installeert en uw app publiceren

Als u dat nog niet gedaan hebt, [Application Proxy configureren voor uw tenant en het Hallo-connector installeert](active-directory-application-proxy-enable.md). Vervolgens [publiceren van uw on-premises toepassing](application-proxy-publish-azure-portal.md) voor externe toegang. Wanneer u Hallo app publiceert, noteer de externe URL Hallo omdat uw eindgebruikers die gegevens moeten wanneer ze Hallo app tooTeams toevoegen.

Als u al uw Apps die zijn gepubliceerd maar weet niet meer van de externe URL's, ze in opzoeken Hallo [Azure-portal](https://portal.azure.com). Meld u aan en vervolgens te navigeren**Azure Active Directory** > **bedrijfstoepassingen** > **alle toepassingen** > uw app selecteren > **Toepassingsproxy**.

## <a name="add-your-app-tooteams"></a>Uw app tooTeams toevoegen

Zodra u Hallo app via toepassingsproxy publiceert, uw gebruikers laten weten dat ze deze als een tabblad rechtstreeks in hun kanalen Teams toevoegen kunnen. Hebben ze deze drie stappen:

1. Navigeer toohello Teams channel waar u tooadd deze app en selecteer  **+**  tooadd een tabblad.

   ![Selecteer een tabblad toevoegen](./media/application-proxy-teams/add-tab.png)

2. Selecteer **Website** uit Hallo tabbladopties.

   ![Een website toevoegen](./media/application-proxy-teams/website.png)

3. Geef een naam op Hallo tabblad en Hallo URL toohello toepassingsproxy externe URL ingesteld. 

   ![Tabbladnaam en URL configureren](./media/application-proxy-teams/tab-name-url.png)

Wanneer een lid van een team Hallo tabblad wordt toegevoegd, wordt deze weergegeven voor iedereen in Hallo-kanaal. Alle gebruikers die toegang toohello app worden geopend voor één aanmelding met Hallo-referenties die ze voor Microsoft-Teams gebruiken. Alle gebruikers die geen toegang tot toohello app Hallo-tabblad in Teams wordt weergegeven, maar worden geblokkeerd totdat u hen machtigingen toohello lokale app geven en de Azure portal de gepubliceerde versie van de app Hallo Hallo. 

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over hoe te[lokale SharePoint-sites publiceren](application-proxy-enable-remote-access-sharepoint.md) met toepassingsproxy.
- Configureren van uw apps toouse [aangepaste domeinen](active-directory-application-proxy-custom-domains.md) voor de externe URL. 
