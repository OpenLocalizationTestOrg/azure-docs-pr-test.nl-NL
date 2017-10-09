---
title: aaaPublish WebApplicationVM | Microsoft Docs
description: Meer informatie over hoe toodeploy een web application tooa virtuele machine. Dit script maakt Hallo vereist resources in uw Azure-abonnement als deze nog niet bestaan.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: e4b52b620bebf44b87ddfc3b19c155bb65111814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a>Publiceren WebApplicationVM (Windows PowerShell-script)
Een web application tooa virtuele machine implementeert. Hallo script maakt Hallo vereist resources in uw Azure-abonnement als deze nog niet bestaan.

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a>Configuratie
Hallo pad toohello JSON-configuratiebestand dat Hallo details van Hallo implementatie beschrijft.

| Aliassen | Geen |
| --- | --- |
| Vereist? |De waarde True |
| Positie |Met de naam |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |ONWAAR |
| Jokertekens accepteren? |ONWAAR |

### <a name="subscriptionname"></a>SubscriptionName
Hallo-naam van hello Azure-abonnement waaraan u toocreate Hallo virtuele machine wilt.

| Aliassen | Geen |
| --- | --- |
| Vereist? |ONWAAR |
| Positie |Met de naam |
| Standaardwaarde |Maakt gebruik van het eerste abonnement Hallo in Hallo abonnementsbestand |
| Pijpleidinginvoer accepteren? |ONWAAR |
| Jokertekens accepteren? |ONWAAR |

### <a name="webdeploypackage"></a>WebDeployPackage
Hallo pad toohello web deployment pakket toopublish toohello virtuele machine. U kunt dit pakket kunt maken met behulp van de wizard webpublicatie Hallo in Visual Studio. Zie [procedure: een Web-implementatiepakket maken in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).

| Aliassen | Geen |
| --- | --- |
| Vereist? |ONWAAR |
| Positie |Met de naam |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |ONWAAR |
| Jokertekens accepteren? |ONWAAR |

### <a name="allowuntrusted"></a>AllowUntrusted
Indien waar, mogen Hallo gebruik van certificaten die niet zijn ondertekend door een vertrouwde basiscertificeringsinstantie.

| Aliassen | Geen |
| --- | --- |
| Vereist? |ONWAAR |
| Positie |Met de naam |
| Standaardwaarde |ONWAAR |
| Pijpleidinginvoer accepteren? |ONWAAR |
| Jokertekens accepteren? |ONWAAR |

### <a name="vmpassword"></a>VMPassword
Hallo-referenties voor de account van de virtuele machine Hallo. Voorbeeld: - VMPassword @{naam = 'admin'; Wachtwoord = 'password'}

| Aliassen | Geen |
| --- | --- |
| Vereist? |ONWAAR |
| Positie |Met de naam |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |ONWAAR |
| Jokertekens accepteren? |ONWAAR |

### <a name="databaseserverpassword"></a>DatabaseServerPassword
Hallo-referenties voor Hallo SQL-database in Azure. Voorbeeld: - DatabaseServerPassword @{naam = 'admin'; Wachtwoord = 'password'}

| Aliassen | Geen |
| --- | --- |
| Vereist? |ONWAAR |
| Positie |Met de naam |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |ONWAAR |
| Jokertekens accepteren? |ONWAAR |

### <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
Indien waar, uitvoer afdrukken berichten van Hallo script toohello stroom.

| Aliassen | Geen |
| --- | --- |
| Vereist? |ONWAAR |
| Positie |Met de naam |
| Standaardwaarde |ONWAAR |
| Pijpleidinginvoer accepteren? |ONWAAR |
| Jokertekens accepteren? |ONWAAR |

## <a name="remarks"></a>Opmerkingen
Voor een volledige beschrijving van hoe toouse Hallo script toocreate Dev- en testomgevingen, Zie [tooPublish tooDev van Windows PowerShell-Scripts en testomgevingen](vs-azure-tools-publishing-using-powershell-scripts.md).

Hallo JSON-configuratiebestand geeft details over Hallo van wat toobe geïmplementeerd is. Deze bevat Hallo-informatie die u hebt opgegeven toen u Hallo-project, zoals het Hallo-naam, affiniteitsgroep, VHD-installatiekopie en grootte van Hallo virtuele machine hebt gemaakt. Ook bevat Hallo-eindpunten op Hallo virtuele machine, Hallo databases tooprovision, indien van toepassing en web-implementatieparameters. Hallo volgende code toont een voorbeeld van de JSON-configuratiebestand:

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

Hallo JSON configuration file toochange wat is ingericht, kunt u bewerken. Een virtuele machine en een cloudservice zijn vereist, maar Hallo database sectie is optioneel.

