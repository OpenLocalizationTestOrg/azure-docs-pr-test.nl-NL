---
title: certificaten met Enterprise Integration Pack aaaUsing | Microsoft Docs
description: Meer informatie over hoe toouse certificaten Hello Enterprise Integration Pack | Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a>Meer informatie over certificaten en het Enterprise Integration Pack
## <a name="overview"></a>Overzicht
Enterprise integration maakt gebruik van certificaten toosecure B2B-communicatie. U kunt twee typen certificaten gebruiken in uw onderneming integratie-apps:

* Openbare certificaten, moeten worden aangeschaft van een certificeringsinstantie (CA).
* Persoonlijke certificaten, kunt u zelf uitgeven. Deze certificaten zijn soms waarnaar wordt verwezen tooas zelfondertekende certificaten.

## <a name="what-are-certificates"></a>Wat zijn certificaten?
Certificaten worden digitale documenten die Hallo identiteit van de deelnemers Hallo in elektronische communicatie verifiëren en die ook elektronische communicatie beveiligen.

## <a name="why-use-certificates"></a>Waarom certificaten gebruiken?
Soms moet B2B-communicatie vertrouwelijk worden behandeld. Enterprise integration maakt gebruik van certificaten toosecure deze communicatie op twee manieren:

* Door het Hallo-inhoud van berichten versleutelen
* Door berichten digitaal te ondertekenen  

## <a name="upload-a-public-certificate"></a>Een openbaar certificaat uploaden

toouse een *openbaar certificaat* in logic apps met B2B-mogelijkheden, moet u eerst tooupload Hallo certificaat bij uw account integratie.  

Nadat u een certificaat hebt geüpload, is beschikbaar toohelp beveiligen van uw B2B-berichten bij het definiëren van de eigenschappen in Hallo [overeenkomsten](logic-apps-enterprise-integration-agreements.md) die u maakt.  

Hier volgen gedetailleerde stappen voor het uploaden van uw certificaten voor openbare toegang tot je account integratie nadat u zich aanmeldt toohello Azure-portal Hallo:

1. Selecteer **meer services** en voer **integratie** in zoekvak Hallo-filter. Selecteer **Integratieaccounts** uit de lijst met resultaten Hallo     
![Selecteer Bladeren](media/logic-apps-enterprise-integration-certificates/overview-1.png)  
2. Hallo-integratie account toowhich u tooadd Hallo certificaat wilt selecteren.  
![Hallo-integratie account toowhich gewenste tooadd Hallo certificaat selecteren](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. Selecteer Hallo **certificaten** tegel.  
![Selecteer Hallo certificaten tegel](media/logic-apps-enterprise-integration-certificates/certificate-1.png)
4. In Hallo **certificaten** blade die wordt geopend, selecteer Hallo **toevoegen** knop.   
![Klik op de knop toevoegen Hallo](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
5. Voer een **naam** voor het certificaat en selecteer vervolgens Hallo certificaattype als **openbare** uit Hallo vervolgkeuzelijst.  
6. Selecteer Hallo mappictogram aan de rechterkant Hallo Hallo **certificaat** in het tekstvak. Wanneer de bestandskiezer hello wordt geopend, zoeken en Hallo certificaatbestand dat u wilt dat tooupload tooyour integratie account selecteren.
7. Hallo certificaat selecteren en selecteer vervolgens **OK** in Hallo bestandskiezer. Dit valideert en uploadt Hallo certificaat tooyour integratie-account.
8. Ten slotte op Hallo back **certificaat toevoegen** blade, selecteer Hallo **OK** knop.  
![Selecteer OK om Hallo](media/logic-apps-enterprise-integration-certificates/certificate-3.png)  
9. Selecteer Hallo **certificaten** tegel. U ziet Hallo toegevoegde certificaat.  
![Zie het nieuwe certificaat Hallo](media/logic-apps-enterprise-integration-certificates/certificate-4.png)  

## <a name="upload-a-private-certificate"></a>Een persoonlijk certificaat uploaden

toouse een *persoonlijk certificaat* in logic apps met B2B-mogelijkheden, kunt u een persoonlijk certificaat tooyour integratie account uploaden door duurt Hallo stappen te volgen

1. [Uploaden van uw persoonlijke sleutel tooKey kluis](../key-vault/key-vault-get-started.md "meer informatie over Sleutelkluis") en geef een **sleutelnaam** 
   
   > [!TIP]
   > U moet Logic Apps tooperform bewerkingen op Sleutelkluis autoriseren. U kunt toegang toohello Logic Apps-service-principal met behulp van de volgende PowerShell-opdracht Hallo verlenen:`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`  
   > 
   > 

Nadat u Hallo vorige stap hebt gemaakt, moet u een persoonlijk certificaat toointegration-account toevoegen.

Hieronder worden de gedetailleerde stappen voor het uploaden van uw persoonlijke certificaten bij uw account integratie nadat u Azure-portal toohello aanmelden Hallo:  
 
1. Selecteer Hallo integratie account toowhich u tooadd Hallo certificaat wilt en selecteer Hallo **certificaten** tegel.  
![Selecteer Hallo certificaten tegel](media/logic-apps-enterprise-integration-certificates/certificate-1.png)  
2. In Hallo **certificaten** blade die wordt geopend, selecteer Hallo **toevoegen** knop.   
![Klik op de knop toevoegen Hallo](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
3. Voer een **naam** voor het certificaat en selecteer Hallo certificaattype als **persoonlijke** uit Hallo vervolgkeuzelijst.   
4. Selecteer Hallo mappictogram aan de rechterkant Hallo Hallo **certificaat** in het tekstvak. Wanneer Hallo bestandskiezer wordt geopend, Hallo overeenkomende openbare-certificaat vinden dat u wilt dat tooupload tooyour integratie rekening.   
   
   > [!Note]
   > Tijdens het toevoegen van een persoonlijk certificaat is het belangrijk tooshow in van het certificaat overeenkomt openbare tooadd [AS2-overeenkomst](logic-apps-enterprise-integration-as2.md) instellingen voor het ondertekenen en versleutelen Hallo-berichten verzenden en ontvangen.
   > 
   >   

5. Selecteer Hallo **resourcegroep**, **Sleutelkluis**, **sleutelnaam** en selecteer Hallo **OK** knop.  
![Certificaat toevoegen](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)  
6. Selecteer Hallo **certificaten** tegel. U ziet Hallo toegevoegde certificaat.
![Zie het nieuwe certificaat Hallo](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)  



* [Maken van een B2B-overeenkomst](logic-apps-enterprise-integration-agreements.md)  
* [Meer informatie over Sleutelkluis](../key-vault/key-vault-get-started.md "meer informatie over Sleutelkluis")  

