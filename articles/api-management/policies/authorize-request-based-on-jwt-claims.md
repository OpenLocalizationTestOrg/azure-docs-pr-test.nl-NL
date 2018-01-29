---
title: 'Azure API management-beleid steekproef: machtig toegang op basis van claims JWT | Microsoft Docs'
description: Azure API management-beleid-voorbeeld - demonstreert hoe u toegang verlenen aan specifieke HTTP-methoden op een op basis van claims van JWT-API.
services: api-management
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/13/2017
ms.author: apimpm
ms.openlocfilehash: 15bd99eeda35161b15e110c3bde0b0bb08fe6d64
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/04/2017
---
# <a name="authorize-access-based-on-jwt-claims"></a>Op basis van claims JWT toegang verlenen

Dit artikel ziet een Azure API management-beleid-voorbeeldtoepassing die u laat zien hoe u toegang verlenen aan specifieke HTTP-methoden op een op basis van claims van JWT-API. Volg de stappen in wilt instellen of bewerken van een beleid code, [instellen of bewerken van een beleid](../set-edit-policies.md). Zie voor andere voorbeelden [beleid voorbeelden](../policy-samples.md).

## <a name="policy"></a>Beleid

Plak de code in de **inkomende** blok.

[!code-xml[Main](../../../api-management-policy-samples/Snippets/Pre-authorize requests based on HTTP method with validate-jwt.policy.xml)]

## <a name="next-steps"></a>Volgende stappen

Meer informatie over APIM beleid:

+ [Transformatiebeleid](../api-management-transformation-policies.md)
+ [Voorbeelden van beleid](../policy-samples.md)

