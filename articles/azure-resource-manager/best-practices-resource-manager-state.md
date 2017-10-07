---
title: aaaPass complexe waarden tussen Azure-sjablonen | Microsoft Docs
description: Bevat aanbevolen methoden voor het gebruik van complexe objecten tooshare statusgegevens met Azure Resource Manager-sjablonen en gekoppelde sjablonen.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fd2f5e2d-d56d-4e01-a57d-34f3eaead4a9
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: tomfitz
ms.openlocfilehash: 72df1dee351446cea6ce15269e6db288b1f1db79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="share-state-tooand-from-azure-resource-manager-templates"></a>Share status tooand van Azure Resource Manager-sjablonen
Dit onderwerp bevat aanbevolen procedures voor het beheren en delen van de status in sjablonen. Hallo parameters en variabelen die worden weergegeven in dit onderwerp vindt u voorbeelden van het type objecten die u kunt definiëren Hallo tooconveniently uw implementatievereisten organiseren. U kunt uw eigen objecten met eigenschapswaarden die geschikt zijn voor uw omgeving implementeren van deze voorbeelden.

In dit onderwerp maakt deel uit van een grotere technisch document. tooread hello volledige papier downloaden [World klasse Resource Manager-sjablonen overwegingen en procedures bewezen](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).

## <a name="provide-standard-configuration-settings"></a>Geef de standaardconfiguratie-instellingen
In plaats van een sjabloon die voorziet in totaal flexibiliteit en talloze variaties bieden, is een algemene patroon tooprovide een selectie van bekende configuraties. Gebruikers kunnen in feite standaard t-shirt grootten zoals sandbox, kleine, middelgrote en grote selecteren. Andere voorbeelden van t-shirt grootten zijn de producten, zoals community edition of enterprise edition. In andere gevallen mogelijk werklastspecifiek configuraties van een technologie – zoals kaart verminderen of er zijn geen sql.

U kunt met complexe objecten variabelen maken die verzamelingen van gegevens, ook wel aangeduid als 'Eigenschappenverzamelingen' bevatten en die gegevens toodrive Hallo de brondeclaratie gebruiken in uw sjabloon. Deze aanpak geeft goede, bekende configuraties van verschillende grootten die vooraf zijn geconfigureerd voor klanten. Zonder bekende configuraties zijn de gebruikers van de sjabloon Hallo moeten cluster sizing op hun eigen, factor in resourcebeperkingen platform bepalen en de handelingen math tooidentify Hallo resulterende partitionering van storage-accounts en andere bronnen (vanwege toocluster grootte en resourcebeperkingen). Bovendien toomaking een betere ervaring voor de klant hello, enkele bekende configuraties zijn eenvoudiger toosupport en kunnen u een hoger niveau van de dichtheid leveren.

Hallo volgende voorbeeld wordt getoond hoe toodefine variabelen die voor het voorstellen van verzamelingen van gegevens naar complexe objecten bevatten. Hallo verzamelingen definiëren waarden die worden gebruikt voor de grootte van virtuele machine, netwerkinstellingen, besturingssysteeminstellingen en instellingen voor beschikbaarheid.

    "variables": {
      "tshirtSize": "[variables(concat('tshirtSize', parameters('tshirtSize')))]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      },
      "tshirtSizeMedium": {
        "vmSize": "Standard_A3",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-8disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1],
          "jumpbox": 0
        }
      },
      "tshirtSizeLarge": {
        "vmSize": "Standard_A4",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-16disk-resources.json')]",
        "vmCount": 3,
        "slaveCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1,1],
          "jumpbox": 0
        }
      },
      "osSettings": {
        "scripts": [
          "[concat(variables('templateBaseUrl'), 'install_postgresql.sh')]",
          "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/shared_scripts/ubuntu/vm-disk-utils-0.1.sh"
        ],
        "imageReference": {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "14.04.2-LTS",
          "version": "latest"
        }
      },
      "networkSettings": {
        "vnetName": "[parameters('virtualNetworkName')]",
        "addressPrefix": "10.0.0.0/16",
        "subnets": {
          "dmz": {
            "name": "dmz",
            "prefix": "10.0.0.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          },
          "data": {
            "name": "data",
            "prefix": "10.0.1.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          }
        }
      },
      "availabilitySetSettings": {
        "name": "pgsqlAvailabilitySet",
        "fdCount": 3,
        "udCount": 5
      }
    }

U ziet dat Hallo **tshirtSize** variabele worden aaneengeschakeld Hallo t-shirt grootte die u hebt opgegeven via een parameter (**kleine**, **gemiddeld**, **grote**) toohello tekst **tshirtSize**. U gebruikt deze variabele tooretrieve Hallo gekoppeld complexe objectvariabele dat formaat t-shirt.

Vervolgens kunt u deze variabelen verderop in de sjabloon Hallo raadplegen. Hallo mogelijkheid tooreference met de naam-variabelen en hun eigenschappen Hallo Sjabloonsyntaxis vereenvoudigt en maakt het eenvoudig toounderstand context. Hallo volgende voorbeeld definieert een toodeploy resource met behulp van Hallo-objecten die eerder tooset waarden weergegeven. Bijvoorbeeld, Hallo VM-grootte is ingesteld door op te halen Hallo-waarde voor `variables('tshirtSize').vmSize` tijdens het Hallo-waarde voor de schijfgrootte hello wordt opgehaald uit `variables('tshirtSize').diskSize`. Bovendien Hallo URI voor een gekoppelde sjabloon is ingesteld met een waarde voor Hallo `variables('tshirtSize').vmTemplate`.

    "name": "master-node",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "dependsOn": [
        "[concat('Microsoft.Resources/deployments/', 'shared')]"
    ],
    "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('tshirtSize').vmTemplate]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "value": "[parameters('adminPassword')]"
          },
          "replicatorPassword": {
            "value": "[parameters('replicatorPassword')]"
          },
          "osSettings": {
            "value": "[variables('osSettings')]"
          },
          "subnet": {
            "value": "[variables('networkSettings').subnets.data]"
          },
          "commonSettings": {
            "value": {
              "region": "[parameters('region')]",
              "adminUsername": "[parameters('adminUsername')]",
              "namespace": "ms"
            }
          },
          "storageSettings": {
            "value":"[variables('tshirtSize').storage]"
          },
          "machineSettings": {
            "value": {
              "vmSize": "[variables('tshirtSize').vmSize]",
              "diskSize": "[variables('tshirtSize').diskSize]",
              "vmCount": 1,
              "availabilitySet": "[variables('availabilitySetSettings').name]"
            }
          },
          "masterIpAddress": {
            "value": "0"
          },
          "dbType": {
            "value": "MASTER"
          }
        }
      }
    }

## <a name="pass-state-tooa-template"></a>Status tooa sjabloon doorgeven
U delen staat in een sjabloon via parameters die u tijdens de implementatie opgeeft.

Hallo volgende parameters voor een lijst met gebruikte in sjablonen.

| Naam | Waarde | Beschrijving |
| --- | --- | --- |
| location |De tekenreeks in een beperkte lijst met Azure-regio 's |Hallo-locatie waar Hallo resources worden geïmplementeerd. |
| storageAccountNamePrefix |Tekenreeks |Unieke DNS-naam op voor Hallo Opslagaccount waar Hallo van de virtuele machine-schijven worden geplaatst |
| Domeinnaam |Tekenreeks |Domeinnaam van Hallo openbaar toegankelijk jumpbox VM Hallo indeling: **{domainName}. { Location}.cloudapp.com** bijvoorbeeld: **mydomainname.westus.cloudapp.azure.com** |
| adminUsername |Tekenreeks |Gebruikersnaam voor Hallo virtuele machines |
| adminPassword |Tekenreeks |Wachtwoord voor Hallo virtuele machines |
| tshirtSize |Tekenreeks van een beperkte lijst aangeboden t-shirt grootten |Hallo met de naam scale unit grootte tooprovision. Bijvoorbeeld 'Klein', 'Gemiddeld', 'Groot' |
| virtualNetworkName |Tekenreeks |Naam van het virtuele netwerk Hallo die de consument Hallo wil toouse. |
| enableJumpbox |De tekenreeks in een beperkte lijst (ingeschakeld/uitgeschakeld) |Parameter die aangeeft of tooenable een jumpbox voor Hallo-omgeving. Waarden: "ingeschakeld", "uitgeschakeld" |

Hallo **tshirtSize** parameter die wordt gebruikt in de vorige sectie Hallo is gedefinieerd als:

    "parameters": {
      "tshirtSize": {
        "type": "string",
        "defaultValue": "Small",
        "allowedValues": [
          "Small",
          "Medium",
          "Large"
        ],
        "metadata": {
          "Description": "T-shirt size of hello MongoDB deployment"
        }
      }
    }


## <a name="pass-state-toolinked-templates"></a>Status toolinked sjablonen doorgeven
Wanneer u verbinding maakt toolinked sjablonen, vaak gebruik een combinatie van statische en variabelen gegenereerd.

### <a name="static-variables"></a>Statische variabelen
Statische variabelen zijn vaak gebruikte tooprovide basiswaarden, zoals URL's die in een sjabloon worden gebruikt.

In Hallo volgende fragment van de sjabloon, `templateBaseUrl` Hiermee geeft u de hoofdlocatie Hallo voor Hallo-sjabloon in GitHub. de volgende regel Hallo bouwt u een nieuwe variabele `sharedTemplateUrl` die Hallo basis-URL met bekende naam Hallo van Hallo gedeelde bronnen sjabloon worden aaneengeschakeld. Onder deze regel een variabele complexe object is gebruikte toostore een grootte t-shirt waarbij Hallo basis-URL aaneengeschakelde toohello bekende locatie van de configuratie-sjabloon en opgeslagen in Hallo `vmTemplate` eigenschap.

Hallo voordeel van deze benadering is dat als locatie van de sjabloon hello wordt gewijzigd, hoeft u alleen toochange Hallo statische variabele op één plek die wordt doorgegeven in de gehele Hallo gekoppelde sjablonen.

    "variables": {
      "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
      "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "slaveCount": 1,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      }
    }

### <a name="generated-variables"></a>Variabelen voor de gegenereerde
Meerdere variabelen worden in toevoeging toostatic variabelen, dynamisch gegenereerd. Deze sectie worden algemene typen gegenereerde variabelen Hallo.

#### <a name="tshirtsize"></a>tshirtSize
U bent bekend met deze variabele gegenereerde van Hallo bovenstaande voorbeelden.

#### <a name="networksettings"></a>networkSettings
In een Hallo capaciteit, mogelijkheid of bereik voor end-to-end-oplossingssjabloon maken gekoppelde sjablonen meestal resources die bestaan op een netwerk. Een eenvoudige benadering is toouse complexe object toostore netwerkinstellingen en ze toolinked sjablonen doorgeven.

Hieronder ziet u een voorbeeld van netwerkinstellingen communiceren.

    "networkSettings": {
      "vnetName": "[parameters('virtualNetworkName')]",
      "addressPrefix": "10.0.0.0/16",
      "subnets": {
        "dmz": {
          "name": "dmz",
          "prefix": "10.0.0.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        },
        "data": {
          "name": "data",
          "prefix": "10.0.1.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        }
      }
    }

#### <a name="availabilitysettings"></a>availabilitySettings
Resources die zijn gemaakt in de gekoppelde sjablonen worden vaak geplaatst in een beschikbaarheidsset. In Hallo voorbeeld te volgen, naam van de beschikbaarheidsset Hallo is opgegeven en ook Hallo foutdomein en domein aantal toouse bijwerken.

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

Als u meerdere beschikbaarheidssets (bijvoorbeeld één voor hoofdknooppunten) en een andere voor gegevensknooppunten, kunt u een naam op als een voorvoegsel moet, Geef meerdere beschikbaarheidssets of Hallo model eerder weergegeven voor het maken van een variabele voor een specifieke t-shirt grootte volgen.

#### <a name="storagesettings"></a>storageSettings
Details van de opslag worden vaak gedeeld met gekoppelde sjablonen. In Hallo voorbeeld hieronder, een *storageSettings* object bevat informatie over Hallo storage-account en de container namen.

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a>osSettings
Met gekoppelde sjablonen moet u mogelijk toopass besturingssysteem instellingen toovarious knooppunten typen andere configuratie voor bekende typen. Een complex object is een eenvoudige manier toostore en delen informatie over het besturingssysteem en maakt het ook eenvoudiger toosupport meerdere besturingssystemen kiezen voor implementatie.

Hallo volgende voorbeeld ziet u een object voor *osSettings*:

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a>machineSettings
Een gegenereerde variabele *machineSettings* is een complex object met een combinatie van core variabelen voor het maken van een virtuele machine. Hallo-variabelen zijn beheerdersgebruikersnaam en wachtwoord, een voorvoegsel voor Hallo VM-namen en een verwijzing naar het afbeelding van het besturingssysteem.

    "machineSettings": {
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "machineNamePrefix": "mongodb-",
        "osImageReference": {
            "publisher": "[variables('osFamilySpec').imagePublisher]",
            "offer": "[variables('osFamilySpec').imageOffer]",
            "sku": "[variables('osFamilySpec').imageSKU]",
            "version": "latest"
        }
    },

Houd er rekening mee dat *osImageReference* haalt de waarden van Hallo Hallo *osSettings* variabele in Hallo belangrijkste sjabloon worden gedefinieerd. Dit betekent dat u kunt eenvoudig hello besturingssysteem wijzigen voor een VM-geheel of op basis van Hallo voorkeur van de consument van een sjabloon.

#### <a name="vmscripts"></a>vmScripts
Hallo *vmScripts* object bevat details over Hallo scripts toodownload en uitvoeren op een VM-instantie, inclusief externe en interne verwijzingen. Buiten bevatten verwijzingen Hallo-infrastructuur.
Binnen verwijzingen zijn hello geïnstalleerd software is geïnstalleerd en configuratie.

Gebruik van Hallo *scriptsToDownload* eigenschap toolist Hallo scripts toodownload toohello VM. Dit object bevat ook verwijzingen toocommand regel argumenten voor verschillende soorten acties. Deze acties omvatten het uitvoeren van de standaardinstallatie Hallo voor elke afzonderlijke knooppunten, een installatie die wordt uitgevoerd nadat alle knooppunten worden geïmplementeerd en eventuele extra scripts die mogelijk specifieke tooa opgegeven sjabloon.

In dit voorbeeld is van een sjabloon die wordt gebruikt toodeploy MongoDB, die een hoge beschikbaarheid voor instellingen toodeliver vereist. Hallo *arbiterNodeInstallCommand* te zijn toegevoegd*vmScripts* tooinstall Hallo instellingen.

sectie met sjabloonvariabelen Hallo is waar u Hallo variabelen die Hallo specifieke tekst tooexecute Hallo script met de juiste waarden Hallo definiëren vinden.

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a>Geretourneerde status van een sjabloon
Niet alleen kunt u gegevens doorgeven aan een sjabloon, kunt u ook share back toohello aanroepen gegevenssjabloon. In Hallo **levert** gedeelte van een gekoppelde sjabloon, kunt u sleutel-waardeparen die kunnen worden gebruikt door de bronsjabloon Hallo opgeven.

Hallo volgende voorbeeld ziet u hoe toopass Hallo privé IP-adres in een gekoppelde sjabloon gegenereerd.

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

In de belangrijkste sjabloon hello, kunt u die gegevens Hello de volgende syntaxis:

    "[reference('master-node').outputs.masterip.value]"

U kunt deze expressie in Hallo uitvoer sectie of Hallo resources gedeelte van de belangrijkste sjabloon hello gebruiken. U kunt Hallo expressie gebruiken in de sectie met sjabloonvariabelen Hallo omdat is afhankelijk van de runtimestatus Hallo. tooreturn hello belangrijkste sjabloon gebruiken voor deze waarde:

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

Zie voor een voorbeeld van het gebruik van Hallo sectie van een gekoppelde sjabloon tooreturn gegevensschijven voor een virtuele machine levert, [meerdere gegevensschijven maken voor een virtuele Machine](resource-group-create-multiple.md).

## <a name="define-authentication-settings-for-virtual-machine"></a>Verificatie-instellingen voor virtuele machine definiëren
U kunt Hallo hetzelfde patroon dat eerder voor configuratie-instellingen toospecify Hallo verificatie-instellingen voor een virtuele machine wordt weergegeven. U maakt een parameter voor het doorgeven in Hallo type verificatie.

    "parameters": {
      "authenticationType": {
        "allowedValues": [
          "password",
          "sshPublicKey"
        ],
        "defaultValue": "password",
        "metadata": {
          "description": "Authentication type"
        },
        "type": "string"
      }
    }

U toevoegen variabelen voor de verschillende verificatietypen Hallo en een variabele toostore welk type wordt gebruikt voor deze implementatie op basis van de waarde van parameter Hallo Hallo.

    "variables": {
      "osProfile": "[variables(concat('osProfile', parameters('authenticationType')))]",
      "osProfilepassword": {
        "adminPassword": "[parameters('adminPassword')]",
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]"
      },
      "osProfilesshPublicKey": {
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]",
        "linuxConfiguration": {
          "disablePasswordAuthentication": "true",
          "ssh": {
            "publicKeys": [
              {
                "keyData": "[parameters('sshPublicKey')]",
                "path": "/home/notused/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
    }

Bij het definiëren van Hallo virtuele machine u Hallo instellen **osProfile** toohello variabele die u hebt gemaakt.

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a>Volgende stappen
* toolearn hello secties van de sjabloon hello, Zie [Azure Resource Manager-sjablonen ontwerpen](resource-group-authoring-templates.md)
* Zie toosee Hallo functies die beschikbaar zijn in een sjabloon [Azure Resource Manager-sjabloonfuncties](resource-group-template-functions.md)
