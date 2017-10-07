---
title: aaaHow toogrant machtigingen tooa ontwikkeld met een aangepaste toepassing | Microsoft Docs
description: Hoe gebruikt door toogrant machtigingen tooyour ontwikkeld met een aangepaste toepassing hello Azure AD-portal of een URL-parameter
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
ms.openlocfilehash: e43a105fff60fbf912bdf4f60260f86ee289328d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogrant-permissions-tooa-custom-developed-application"></a>Hoe toogrant machtigingen tooa aangepaste ontwikkelde toepassing

Als u wilt dat optie preventief toogrant toestemming van uw app of worden uitgevoerd in een fout dat u tooan app geen toestemming hebt gegeven, kunt u onderstaande stappen.

## <a name="how-tooperform-admin-consent-for-your-application"></a>Hoe tooperform-beheerder toestemming voor uw toepassing

Dit heeft Hallo effect voor het verlenen van toestemming toohello-toepassing voor alle gebruikers in uw organisatie.

1. Navigeer toohello **App registraties** blade als een **hoofdbeheerder**, selecteer daarna Hallo app.

2. Selecteer **Required Permissions**, en klik tot slot op Hallo **machtiging verlenen** knop Hallo boven aan het Hallo-blade.

U kunt ook kunt u een aanvraag te maken*login.microsoftonline.com* met de configuraties van uw app en toe te voegen op *& vragen = admin\_toestemming*. Na het aanmelden met beheerdersreferenties, heeft Hallo app gekregen toestemming voor alle gebruikers.

## <a name="how-tooforce-user-consent-for-your-application"></a>Hoe tooforce gebruiker toestemming geven voor uw toepassing

* Toevoegen op auth-aanvragen *& vragen toestemming =* die eindgebruikers tooconsent vereisen telkens wanneer ze verifiëren.

## <a name="next-steps"></a>Volgende stappen

[TooAzureAD toestemming en integratie van Apps](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[Toestemming en rollen voor AzureAD v2.0 geconvergeerde Apps](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[AzureAD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory)
