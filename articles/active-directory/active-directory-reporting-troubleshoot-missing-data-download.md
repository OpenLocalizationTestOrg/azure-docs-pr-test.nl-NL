---
title: 'Voor probleemoplossing: Ontbrekende gegevens in Hallo gedownload Azure Active Directory-activiteitenlogboeken | Microsoft Docs'
description: Biedt u de gegevens van een oplossing toomissing in gedownloade activiteitenlogboeken van Azure Active Directory.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 027b70e6efc570f81d3c836f50ee52aaa89be71a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a>Ik kan geen gegevens vinden in hello Azure Active Directory-activiteitenlogboeken die ik heb gedownload


## <a name="symptoms"></a>Symptomen

Ik Hallo activiteitenlogboeken (audit of aanmeldingen) gedownload en alle Hallo records wordt niet weergegeven voor Hallo keer gekozen. Hoe komt dat? 

 ![Rapportage](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a>Oorzaak

Wanneer u activiteitenlogboeken in hello Azure-portal hebt gedownload, beperken we Hallo scale too120K records, gesorteerd op basis van de meeste recente. 

## <a name="resolution"></a>Oplossing

U kunt gebruikmaken van [Azure AD rapportage-API's](active-directory-reporting-api-getting-started.md) toofetch tooa miljoen records op elk gewenst moment. De aanbevolen aanpak is toorun een script dat op vaste tijden die Hallo rapportage-API's toofetch aanroept op incrementele wijze gedurende een periode registreert (bijvoorbeeld dagelijks of wekelijks).

## <a name="next-steps"></a>Volgende stappen
Zie Hallo [Azure Active Directory-rapportage Veelgestelde vragen over](active-directory-reporting-faq.md).

