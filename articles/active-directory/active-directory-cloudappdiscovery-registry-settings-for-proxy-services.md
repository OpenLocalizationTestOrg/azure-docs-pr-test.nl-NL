---
title: aaaCloud App Discovery-registerinstellingen voor Proxy Services | Microsoft Docs
description: Hallo-doel van dit onderwerp is tooperform tooset Hallo vereist poort op Hallo van computers Hallo Cloud App Discovery agent tooprovide u Hello stappen die u nodig hebt.
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
ms.openlocfilehash: bb1fe20016459160b4f67cb0125b1781a0260c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a>Cloud App Discovery-registerinstellingen voor proxyservices
Hallo Cloud App Discovery agent is standaard geconfigureerd toouse alleen Hallo poorten 80 of 443. Als u van plan bent over het installeren van Cloud App Discovery in een omgeving met een proxyserver die van een aangepaste poort (geen 80 of 443 gebruikmaakt), moet u tooconfigure uw agents toouse deze poort. Hallo-configuratie is gebaseerd op een registersleutel.

Hallo-doel van dit onderwerp is tooperform tooset Hallo vereist poort op Hallo van computers Hallo Cloud App Discovery agent tooprovide u Hello stappen die u nodig hebt.

**toomodify Hallo poort wordt gebruikt door het Hallo-computers Hallo Cloud App Discovery agent, Voer Hallo stappen te volgen:**

1. Start Hallo Register-editor. <br> ![Voer](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. Navigeer tooor maken Hallo volgende registersleutel: <br> **HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint** 
3. Maak een nieuwe **met meerdere tekenreeksen** waarde met de naam **poorten**. ![Nieuw](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)
4. Hallo tooopen **met meerdere tekenreeksen bewerken** dialoogvenster, dubbelklik op Hallo poorten waarde.
5. In Hallo waarde gegevens textbox, typt u Hallo waarden te volgen en voeg alle aangepaste poorten die worden gebruikt door uw organisatie: <br><br>
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
6. Klik op **OK** tooclose hello **met meerdere tekenreeksen bewerken** dialoogvenster.

**Aanvullende resources**

* [Hoe kan ik cloudapps die worden gebruikt in mijn organisatie detecteren](active-directory-cloudappdiscovery-whatis.md) 

