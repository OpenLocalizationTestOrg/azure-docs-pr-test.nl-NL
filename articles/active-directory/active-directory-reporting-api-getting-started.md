---
title: Aan de slag met Azure AD rapportage-API in de klassieke Azure AD-portal | Microsoft Docs
description: Hoe u aan de slag met de Azure Active Directory rapportage-API
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/18/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 5e98b660fe19bb8abebf1c3b996b6295a6c4e728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api-on-the-azure-ad-classic-portal"></a>Aan de slag met de Azure Active Directory rapportage-API in de klassieke Azure AD-portal
*In dit onderwerp maakt deel uit van de [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*

Azure Active Directory beschikt u over tal van rapporten. De gegevens van deze rapporten kunnen zeer nuttig zijn voor uw toepassingen, zoals SIEM-systemen, audit- en business intelligence-hulpprogramma's. De API's van Azure AD Reporting bieden toegang tot de gegevens op programmeerniveau via een set op REST-gebaseerde API's. U kunt deze API's vanuit een groot aantal computertalen en hulpprogramma's aanroepen.

In dit artikel biedt u de informatie die u moet aan de slag met Azure AD rapportage-API's.
In de volgende sectie stelt u meer informatie over het gebruik van de audit en meld u API's. Voor alle andere API's, Zie de [Azure AD-rapporten en events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) artikel.

Voor vragen, problemen of feedback, neem contact op met [AAD rapportage Help](mailto:aadreportinghelp@microsoft.com).

## <a name="learning-map"></a>Leertraject
1. **Voorbereiden** -voordat u uw API-voorbeelden testen kunt, u moet voltooien de [vereisten voor toegang tot de Azure AD rapportage-API](active-directory-reporting-api-prerequisites.md).
2. **Verken** -ophalen van een eerste indruk van de rapportage-API's:
   
   * [Met behulp van de voorbeelden voor de API-controle](active-directory-reporting-api-audit-samples.md) 
   * [Met behulp van de voorbeelden voor het rapport aanmeldingsactiviteiten API](active-directory-reporting-api-sign-in-activity-samples.md)
3. **Aanpassen** -Maak uw eigen oplossing: 
   
   * [Met behulp van de audit API-referentiemateriaal](active-directory-reporting-api-audit-reference.md) 
   * [Met behulp van de aanmeldingsactiviteiten rapport API-verwijzing](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a>Volgende stappen
Als u wilt alle van de beschikbare Azure AD Graph API-eindpunten bekijken door te navigeren naar [https://graph.windows.net/tenant-name/reports/$ metagegevens? api-version = beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).

