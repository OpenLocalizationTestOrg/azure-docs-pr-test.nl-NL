---
title: Cloud App Discovery-registerinstellingen voor proxyservices | Microsoft Docs
description: Het doel van dit onderwerp is om te voorzien van de stappen die u moet uitvoeren om in te stellen de vereiste poort op de computers waarop de Cloud App Discovery-agent wordt uitgevoerd.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ea15dc9a9f20a296e622c8fb1011f7ee99de3e99
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a>Cloud App Discovery-registerinstellingen voor proxyservices
De Cloud App Discovery-agent is standaard geconfigureerd om alleen de poorten 80 of 443 te gebruiken. Als u van plan bent over het installeren van Cloud App Discovery in een omgeving met een proxyserver die van een aangepaste poort (geen 80 of 443 gebruikmaakt), moet u de agents voor het gebruik van deze poort configureren. De configuratie is gebaseerd op een registersleutel.

Het doel van dit onderwerp is om te voorzien van de stappen die u moet uitvoeren om in te stellen de vereiste poort op de computers waarop de Cloud App Discovery-agent wordt uitgevoerd.

**Voor het wijzigen van de poort die wordt gebruikt door de computer waarop de Cloud App Discovery-agent wordt uitgevoerd, moet u de volgende stappen uitvoeren:**

1. Start de Registereditor. <br> ![Uitvoeren](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. Ga naar of maak de volgende registersleutel: <br> **HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint** 
3. Maak een nieuwe **met meerdere tekenreeksen** waarde met de naam **poorten**. ![Nieuw](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)
4. Openen van de **met meerdere tekenreeksen bewerken** dialoogvenster, dubbelklik op de waarde van de poorten.
5. Typ de volgende waarden in het tekstvak voor waarde-gegevens en alle aangepaste poorten die worden gebruikt door uw organisatie toevoegen: <br><br>
   **80** <br>
   **8080** <br>
   **8118** <br>
   **8888** <br>
   **81** <br>
   **12080** <br>
   **6999** <br>
   **30606** <br>
   **31595** <br>
   **4080** <br>
   **443** <br>
   **1110** <br><br>
   ![Met meerdere tekenreeksen bewerken](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)
6. Klik op **OK** sluiten de **met meerdere tekenreeksen bewerken** dialoogvenster.

**Aanvullende resources**

* [Hoe kan ik cloudapps die worden gebruikt in mijn organisatie detecteren](active-directory-cloudappdiscovery-whatis.md) 

