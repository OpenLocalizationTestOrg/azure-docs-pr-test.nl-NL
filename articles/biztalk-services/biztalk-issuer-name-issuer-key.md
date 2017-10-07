---
title: aaaIssuer naam en sleutel van verlener in BizTalk Services | Microsoft Docs
description: Meer informatie over hoe tooretrieve verlener naam en sleutel van verlener voor Service Bus of Access Control (ACS) in BizTalk Services. MABS, WABS
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a>BizTalk Services: naam en sleutel van verlener

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Azure BizTalk Services maakt gebruik van Hallo naam van Service Bus verlener en sleutel van verlener en Hallo Access Control certificaatverlener en sleutel van verlener. Specifiek:

| Taak | Welke naam van verlener en sleutel van verlener |
| --- | --- |
| Implementeren van uw toepassing vanuit Visual Studio |Toegang tot de naam van de certificaatverlener besturingselement en de sleutel van verlener |
| Hello Azure BizTalk Services-Portal configureren |Toegang tot de naam van de certificaatverlener besturingselement en de sleutel van verlener |
| LOB-Relays maken Hello BizTalk Adapter Services in Visual Studio |Naam van Service Bus verlener en sleutel van verlener |

In dit onderwerp bevat Hallo stappen tooretrieve Hallo naam van verlener en sleutel van verlener. 

## <a name="access-control-issuer-name-and-issuer-key"></a>Toegang tot de naam van de certificaatverlener besturingselement en de sleutel van verlener
Hallo Access Control verlener naam en sleutel van verlener worden gebruikt door de volgende Hallo:

* Uw Azure BizTalk Service-toepassing in Visual Studio gemaakt: toosuccessfully uw BizTalk Service-toepassing in Visual Studio tooAzure implementeert, kunt u Hallo Access Control verlener naam en sleutel van verlener invoeren. 
* Hello Azure BizTalk Services-Portal: als u een BizTalk Service maakt en geopend Hallo BizTalk Services-Portal, de naam van uw Access Control verlener en sleutel van verlener worden automatisch geregistreerd voor uw implementaties met Hallo dezelfde Access Control-waarden.

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a>Ophalen van Hallo Access Control verlener naam en sleutel van verlener

toouse ACS voor verificatie en get Hallo waarden voor naam van de verlener en sleutel van verlener, hello algemene stappen omvatten:

1. Hallo installeren [Azure Powershell-cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
2. Uw Azure-account toevoegen:`Add-AzureAccount`
3. Retourneert de abonnementsnaam van uw:`get-azuresubscription`
4. Selecteer uw abonnement:`select-azuresubscription <name of your subscription>` 
5. Maak een nieuwe naamruimte:`new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`

    Voorbeeld:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`
      
5. Wanneer Hallo nieuwe ACS-naamruimte wordt gemaakt (dit kan enkele minuten duren), vindt u in verbindingsreeks Hallo Hallo-naam van verlener en sleutel van verlener waarden: 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

toosummarize:  
De naam van certificaatverlener SharedSecretIssuer =  
Sleutel van verlener SharedSecretKey =

Meer informatie over Hallo [nieuw AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet. 

## <a name="service-bus-issuer-name-and-issuer-key"></a>Naam van Service Bus verlener en sleutel van verlener
Naam van Service Bus verlener en sleutel van verlener worden gebruikt door de BizTalk Adapter Services. In uw BizTalk Services-project in Visual Studio gebruikt u Hallo BizTalk Adapter Services tooconnect tooan on-premises Line-of-Business (LOB)-systeem. tooconnect, u Hallo Relay LOB maken en voer de details van uw LOB-systeem. Wanneer u dit doet, Voer u ook Hallo naam van Service Bus verlener en sleutel van verlener.

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a>tooretrieve hello naam van Service Bus verlener en sleutel van verlener
1. Meld u aan toohello [klassieke Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Selecteer in de Hallo navigatiedeelvenster links **Service Bus**.
3. Selecteer de naamruimte. Selecteer in de taakbalk Hallo **verbindingsgegevens**. Hallo ziet **standaard verlener** (naam van de certificaatverlener) en **standaard sleutel** (sleutel van verlener). De waarden kunnen worden gekopieerd.  

toosummarize:  
De naam van certificaatverlener = standaard certificaatverlener  
Sleutel van verlener standaardsleutel =

## <a name="next"></a>Volgende
Aanvullende onderwerpen voor Azure BizTalk Services:

* [Hello Azure BizTalk Services SDK installeren](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [Zelfstudies: Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [Hoe gaan gebruiken Azure BizTalk Services SDK Hallo](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>Zie ook
* [Hoe: gebruik ACS-Management-Service tooConfigure Service-identiteiten](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [BizTalk Services: Developer, Basic, Standard en Premium-edities grafiek](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [BizTalk Services: Inrichten met behulp van Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [BizTalk Services: statusgrafiek voor de inrichting](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [BizTalk Services: de tabbladen Dashboard, Bewaken en Schalen](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [BizTalk Services: back-ups maken en herstellen](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [BizTalk Services: beperking](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

