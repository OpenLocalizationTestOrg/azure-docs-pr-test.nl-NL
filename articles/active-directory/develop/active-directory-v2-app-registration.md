---
title: een toepassing met hello Azure AD v2.0-eindpunt met behulp van de portal Hallo aaaRegister | Microsoft Docs
description: Hoe tooregister een app met Microsoft voor het inschakelen aanmelden en toegang tot Microsoft-services met behulp van Hallo v2.0-eindpunt
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: c56c98906656062435516e820cb318a04c03149c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooregister-an-app-with-hello-v20-endpoint"></a>Hoe tooregister een app met Hallo v2.0-eindpunt
een app die zowel MSA & Azure AD accepteert toobuild aanmelden, moet u eerst een app met Microsoft tooregister.  Op dit moment kunt u won't kunnen toouse worden alle bestaande apps u met Azure AD hebt wellicht of MSA - u moet een merk nieuwe toocreate.

> [!NOTE]
> Niet alle Azure Active Directory-scenario's en functies worden ondersteund door Hallo v2.0-eindpunt.  toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).
> 
> 

## <a name="visit-hello-microsoft-app-registration-portal"></a>Ga naar Hallo-portal voor registratie van Microsoft-app
Eerste dingen eerst - Navigeer te[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).  Dit is een nieuwe app-portal voor wachtwoordregistratie waar u uw Microsoft-apps kunt beheren.

Meld u aan met ofwel een persoonlijke of werk of school Microsoft-account.  Als u geen ofwel hebt, moet u zich aanmelden voor een nieuw persoonlijk account. Opwekken, won't duurt lang - wij hier wachten.

Uitgevoerd? U moet nu worden kijken naar de lijst met Microsoft-apps, die waarschijnlijk leeg is.  Hiermee kunt wijzigen.

Klik op **een app toevoegen**, en een naam geven.  Hallo portal toewijzen uw app een globally unique identifier toepassings-Id die u later in uw code.  Als uw app een serverzijde-onderdeel bevat dat toegangstokens moet voor aanroepen API's (nadenkt: Office, Azure of uw eigen web-API), moet u toocreate een **Toepassingsgeheim** hier ook.

Voeg vervolgens Hallo Platforms die uw app wilt gebruiken.

* Voor op basis van web-apps, geeft u een **omleidings-URI** waar aanmelden berichten kunnen worden verzonden.
* Voor mobiele apps Noteer Hallo standaard omleidings-uri die automatisch voor u gemaakt.

U kunt eventueel Hallo uiterlijk van de aanmeldingspagina in Hallo-profiel.  Zorg ervoor dat tooclick **opslaan** voordat u doorgaat.

> [!NOTE]
> Wanneer u maakt een toepassing met behulp [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), Hallo toepassing wordt geregistreerd in thuis Hallo-tenant van Hallo-account dat u toosign bij Hallo-portal.  Dit betekent dat u een toepassing in uw Azure AD-tenant met behulp van een persoonlijk Microsoft-account niet kunt registreren.  Als u expliciet tooregister een toepassing in een bepaalde tenant wenst, aanmelden met een account die oorspronkelijk is gemaakt in deze tenant.
> 
> 

## <a name="build-a-quick-start-app"></a>Een App snel starten
Nu dat u een Microsoft-app hebt, kunt u een van onze v2.0 snel starten-zelfstudie te voltooien.  Hier volgen enkele aanbevelingen:

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

