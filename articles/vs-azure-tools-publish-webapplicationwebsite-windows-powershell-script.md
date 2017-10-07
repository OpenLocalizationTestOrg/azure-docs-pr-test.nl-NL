---
title: aaaPublish-WebApplicationWebSite (Windows PowerShell-script) | Microsoft Docs
description: Meer informatie over hoe toopublish een web project tooan Azure-website. Dit script maakt Hallo vereist resources in uw Azure-abonnement als deze nog niet bestaan.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a>Publiceren WebApplicationWebSite (Windows PowerShell-script)
## <a name="syntax"></a>Syntaxis
Een web project tooan Azure-website publiceert. Hallo script maakt Hallo vereist resources in uw Azure-abonnement als deze nog niet bestaan.

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a>Configuratie
Hallo pad toohello JSON-configuratiebestand dat Hallo details van Hallo implementatie beschrijft.

| Parameter | Standaardwaarde |
| --- | --- |
| Aliassen |Geen |
| Vereist? |De waarde True |
| Positie |Met de naam |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |ONWAAR |
| Jokertekens accepteren? |ONWAAR |

## <a name="subscriptionname"></a>SubscriptionName
Hallo-naam van hello Azure-abonnement dat u wilt dat toocreate Hallo website in.

| Parameter | Standaardwaarde |
| --- | --- |
| Aliassen |Geen |
| Vereist? |ONWAAR |
| Positie |Met de naam |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |ONWAAR |
| Jokertekens accepteren? |ONWAAR |

## <a name="webdeploypackage"></a>WebDeployPackage
Hallo pad toohello web deployment pakket toopublish toohello website. U kunt dit pakket kunt maken met behulp van de wizard webpublicatie Hallo in Visual Studio. Zie voor meer informatie [aan de slag met Azure Cloud Services en ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).

| Parameter | Standaardwaarde |
| --- | --- |
| Aliassen |Geen |
| Vereist? |ONWAAR |
| Positie |Met de naam |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |ONWAAR |
| Jokertekens accepteren? |ONWAAR |

## <a name="databaseserverpassword"></a>DatabaseServerPassword
Hallo-gebruikersnaam en wachtwoord voor Hallo SQL-database in Azure.

| Parameter | Standaardwaarde |
| --- | --- |
| Aliassen |Geen |
| Vereist? |ONWAAR |
| Positie |Met de naam |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |ONWAAR |
| Jokertekens accepteren? |ONWAAR |

## <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
Indien waar, uitvoer afdrukken berichten van Hallo script toohello stroom.

| Parameter | Standaardwaarde |
| --- | --- |
| Aliassen |Geen |
| Vereist? |ONWAAR |
| Positie |Met de naam |
| Standaardwaarde |ONWAAR |
| Pijpleidinginvoer accepteren? |ONWAAR |
| Jokertekens accepteren? |ONWAAR |

## <a name="remarks"></a>Opmerkingen
Voor een volledige beschrijving van hoe toouse Hallo script toocreate Dev- en testomgevingen, Zie [tooPublish tooDev van Windows PowerShell-Scripts en testomgevingen](vs-azure-tools-publishing-using-powershell-scripts.md).

Hallo JSON-configuratiebestand geeft details over Hallo van wat toobe geïmplementeerd is. Het bevat Hallo-informatie die u hebt opgegeven tijdens het maken van Hallo-project, zoals Hallo naam- en gebruikersnaam voor Hallo website. Dit omvat ook Hallo database tooprovision, indien van toepassing. Hallo volgende code toont een voorbeeld van de JSON-configuratiebestand:

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

Hallo JSON configuration file toochange wat wordt geïmplementeerd, kunt u bewerken. Een gedeelte van de webSite is vereist, maar Hallo database sectie is optioneel.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie [publiceren-WebApplicationVM (Windows PowerShell-script)](vs-azure-tools-publish-webapplicationvm.md)

