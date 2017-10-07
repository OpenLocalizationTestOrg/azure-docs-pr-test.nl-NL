---
title: aaaHow tooconfigure een toepassing toepassingsproxy | Microsoft Docs
description: Meer informatie over hoe toocreate een configureren van een toepassing toepassingsproxy in een paar eenvoudige stappen
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a>Hoe een toepassing toepassingsproxy tooconfigure

In dit artikel kunt u toounderstand hoe een toepassing toepassingsproxy in Azure AD-tooexpose tooconfigure uw lokale toepassingen toohello cloud.

## <a name="recommended-documents"></a>Aanbevolen documenten 

toolearn over Hallo initiële configuraties en het maken van een toepassing toepassingsproxy via Hallo-beheerportal, volg Hallo [toepassingen publiceren met Azure AD-toepassingsproxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

Zie voor meer informatie over het configureren van Connectors [toepassingsproxy inschakelen in Azure-portal Hallo](active-directory-application-proxy-enable.md).

Zie voor meer informatie over het uploaden van certificaten en gebruiken van aangepaste domeinen [werken met aangepaste domeinen in Azure AD-toepassingsproxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).

## <a name="create-hello-applicationsetting-hello-urls"></a>Hallo toepassingsinstelling/Hallo-URL's maken

Als u volgt Hallo stappen voor het Hallo [toepassingen publiceren met Azure AD-toepassingsproxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentatie en weet Hallo foutdetails voor informatie en suggesties voor het ophalen van een fout bij het maken van de toepassing hello, Zie toofix Hallo-toepassing. De meeste foutberichten bevatten een voorgestelde oplossing. veelvoorkomende fouten tooavoid, controleert u of:

-   U bent een beheerder met de machtiging toocreate een toepassingsproxy-toepassing

-   Interne URL Hallo is uniek.

-   de externe URL Hallo is uniek.

-   Hallo URL's starten met http of https en eindigen met een "/"

-   Hallo-URL moet een domeinnaam, geen IP-adres

Fout bij het Hallo-bericht moet worden weergegeven in de rechterbovenhoek Hallo wanneer u de toepassing hello maakt. U kunt ook Hallo melding pictogram toosee Hallo foutberichten selecteren.

   ![Prompt voor melding](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a>Connectors/connector groepen configureren

Als u problemen bij het configureren van uw toepassing vanwege een waarschuwing over Hallo connectors en connector groepen ondervindt, raadpleegt u instructies over het inschakelen van toepassingsproxy voor meer informatie over het toodownload connectors. Als u meer informatie over connectors toolearn wilt, raadpleegt u Hallo [connectors documentatie](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).

Als uw connectors niet actief zijn, betekent dit dat ze niet kan tooreach Hallo service zijn. Dit is vaak omdat niet alle vereiste Hallo poorten geopend zijn. een lijst met vereiste poorten toosee Zie Hallo vereisten sectie Hallo documentatie toepassingsproxy inschakelen.

## <a name="upload-certificates-for-custom-domains"></a>Certificaten voor aangepaste domeinen uploaden

Aangepaste domeinen toestaan toospecify Hallo domein van de externe URL's. toouse aangepaste domeinen, moet u tooupload Hallo certificaat voor dat domein. Zie voor meer informatie over het gebruik van aangepaste domeinen en certificaten [werken met aangepaste domeinen in Azure AD-toepassingsproxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains). 

Als er problemen zijn uw certificaat uploaden, zoekt u Hallo foutberichten in de portal Hallo voor meer informatie over Hallo probleem is met Hallo certificaat. Algemene problemen met de certificaten zijn onder andere:

-   Verlopen certificaat

-   Certificaat is zelfondertekend

-   Certificaat ontbreekt Hallo persoonlijke sleutel

Hallo-berichtweergave van fouten in Hallo rechterbovenhoek als u tooupload Hallo certificaat probeert. U kunt ook Hallo melding pictogram toosee Hallo foutberichten selecteren.

   ![Prompt voor melding](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a>Volgende stappen
[Toepassingen publiceren met Azure AD-toepassingsproxy](application-proxy-publish-azure-portal.md)
