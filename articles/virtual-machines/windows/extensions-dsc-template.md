---
title: aaaDesired status configuratie Resource Manager-sjabloon | Microsoft Docs
description: Definitie van de Resource Manager-sjabloon voor Desired State Configuration in Azure met voorbeelden en het oplossen van problemen
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: b5402e5a-1768-4075-8c19-b7f7402687af
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: fc47ac149b1179d9305797eaa8ed8a83c0958c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a>Windows VMSS en Desired State Configuration met Azure Resource Manager-sjablonen
Dit artikel wordt beschreven Hallo Resource Manager-sjabloon voor Hallo [Desired State Configuration extensie handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="template-example-for-a-windows-vm"></a>Voorbeeld van de sjabloon voor een virtuele machine van Windows
Hallo probeert volgende fragment het Hallo gedeelte van de Resource van Hallo-sjabloon.

```json
            "name": "Microsoft.Powershell.DSC",
            "type": "extensions",
             "location": "[resourceGroup().location]",
             "apiVersion": "2015-06-15",
             "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "dscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }

```

## <a name="template-example-for-windows-vmss"></a>Voorbeeld van de sjabloon voor Windows VMSS
Een knooppunt VMSS heeft een sectie 'Eigenschappen' Hello 'VirtualMachineProfile', 'extensionProfile'-kenmerk. DSC wordt toegevoegd onder 'extensions'. 

```json
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": true,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
        }
```

## <a name="detailed-settings-information"></a>Informatie over de gedetailleerde instellingen
Hallo is volgende schema Hallo instellingen deel van het hello Azure DSC-uitbreiding in een Azure Resource Manager-sjabloon.

```json

"settings": {
  "wmfVersion": "latest",
  "configuration": {
    "url": "http://validURLToConfigLocation",
    "script": "ConfigurationScript.ps1",
    "function": "ConfigurationFunction"
  },
  "configurationArguments": {
    "argument1": "Value1",
    "argument2": "Value2"
  },
  "configurationData": {
    "url": "https://foo.psd1"
  },
  "privacy": {
    "dataCollection": "enable"
  },
  "advancedOptions": {
    "downloadMappings": {
      "customWmfLocation": "http://myWMFlocation"
    }
  } 
},
"protectedSettings": {
  "configurationArguments": {
    "parameterOfTypePSCredential1": {
      "userName": "UsernameValue1",
      "password": "PasswordValue1"
    },
    "parameterOfTypePSCredential2": {
      "userName": "UsernameValue2",
      "password": "PasswordValue2"
    }
  },
  "configurationUrlSasToken": "?g!bber1sht0k3n",
  "configurationDataUrlSasToken": "?dataAcC355T0k3N"
}

```

## <a name="details"></a>Details
| De naam van eigenschap | Type | Beschrijving |
| --- | --- | --- |
| settings.wmfVersion |Tekenreeks |Hiermee wordt de versie Hallo Hallo Windows Management Framework die op de virtuele machine moet worden geïnstalleerd. Deze eigenschap too'latest instellen ' installeert Hallo meest recente versie van WMF. Hallo alleen huidige mogelijke waarden voor deze eigenschap zijn **'4.0', '5.0', ' 5.0PP' en 'nieuwste'**. Deze mogelijke waarden zijn tooupdates onderwerp. Hallo-standaardwaarde is 'nieuwste'. |
| Settings.Configuration.URL |Tekenreeks |Hiermee geeft u het zip-bestand van de DSC-configuratie Hallo URL-locatie van welke toodownload. Als een SAS-token Hallo-URL opgegeven om toegang te krijgen vereist, moet u tooset hello protectedSettings.configurationUrlSasToken toohello eigenschapswaarde van SAS-token. Deze eigenschap is vereist als settings.configuration.script en/of settings.configuration.function zijn gedefinieerd. |
| Settings.Configuration.script |Tekenreeks |Geeft de bestandsnaam Hallo van Hallo-script dat Hallo definitie van de DSC-configuratie bevat. Dit script moet in de hoofdmap Hallo van Hallo zip-bestand is gedownload van Hallo URL die is opgegeven door Hallo configuration.url eigenschap. Deze eigenschap is vereist als settings.configuration.url en/of settings.configuration.script zijn gedefinieerd. |
| Settings.Configuration.Function |Tekenreeks |Hiermee geeft u Hallo-naam van de DSC-configuratie. Hallo-configuratie met de naam moet worden opgenomen in Hallo script gedefinieerd door configuration.script. Deze eigenschap is vereist als settings.configuration.url en/of settings.configuration.function zijn gedefinieerd. |
| settings.configurationArguments |Verzameling |Hiermee definieert u de parameters die u wilt dat toopass tooyour DSC-configuratie. Deze eigenschap is niet versleuteld. |
| settings.configurationData.url |Tekenreeks |Hiermee geeft u Hallo-URL van welke toodownload uw configuratiegegevens (.psd1) toouse bestand als invoer voor uw DSC-configuratie. Als een SAS-token Hallo-URL opgegeven om toegang te krijgen vereist, moet u tooset hello protectedSettings.configurationDataUrlSasToken toohello eigenschapswaarde van SAS-token. |
| settings.privacy.dataEnabled |Tekenreeks |Schakelt verzamelen van telemetriegegevens in of uit. Hallo alleen mogelijke waarden voor deze eigenschap zijn **'Inschakelen', 'Uitschakelen', ', of $null**. Als u deze eigenschap leeg of null kan telemetrie. de standaardwaarde Hallo is ''. [Meer informatie](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| settings.advancedOptions.downloadMappings |Verzameling |Alternatieve locaties die van welke toodownload Hallo WMF definieert. [Meer informatie](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| protectedSettings.configurationArguments |Verzameling |Hiermee definieert u de parameters die u wilt dat toopass tooyour DSC-configuratie. Deze eigenschap is versleuteld. |
| protectedSettings.configurationUrlSasToken |Tekenreeks |Hiermee geeft u Hallo SAS-token tooaccess Hallo URL die is gedefinieerd door configuration.url. Deze eigenschap is versleuteld. |
| protectedSettings.configurationDataUrlSasToken |Tekenreeks |Hiermee geeft u Hallo SAS-token tooaccess Hallo URL die is gedefinieerd door configurationData.url. Deze eigenschap is versleuteld. |

## <a name="settings-vs-protectedsettings"></a>Vs instellingen. ProtectedSettings
Alle instellingen worden opgeslagen in een tekstbestand instellingen op Hallo VM.
Eigenschappen onder 'instellingen' zijn eigenschappen public, omdat ze niet zijn versleuteld in tekstbestand Hallo-instellingen.
Eigenschappen onder 'protectedSettings' zijn versleuteld met een certificaat en worden niet weergegeven als tekst zonder opmaak in dit bestand op Hallo VM.

Als Hallo configuratie moet referenties, kunnen ze worden opgenomen in protectedSettings:

```json
"protectedSettings": {
    "configurationArguments": {
        "parameterOfTypePSCredential1": {
               "userName": "UsernameValue1",
               "password": "PasswordValue1"
        }
    }
}
```

## <a name="example"></a>Voorbeeld
Hallo volgende voorbeeld is afgeleid van Hallo sectie 'Aan de slag' Hallo [overzichtspagina DSC-uitbreiding Handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
In dit voorbeeld maakt gebruik van Resource Manager-sjablonen in plaats van cmdlets toodeploy Hallo-extensie. Hallo 'IisInstall.ps1' configuratie op te slaan, plaatst u deze in een. ZIP-bestand en het uploaden van Hallo-bestand in een toegankelijke URL. In dit voorbeeld wordt een Azure blob-opslag, maar het is mogelijk toodownload. ZIP-bestanden vanaf elke willekeurige locatie.

In hello Azure Resource Manager-sjabloon, hello volgende code geeft opdracht Hallo VM toodownload Hallo juiste bestand en Voer Hallo betreffende PowerShell functie:

```json
"settings": {
    "configuration": {
        "url": "https://demo.blob.core.windows.net/",
        "script": "IisInstall.ps1",
        "function": "IISInstall"
    }
    } 
},
"protectedSettings": {
    "configurationUrlSasToken": "odLPL/U1p9lvcnp..."
}
```

## <a name="updating-from-hello-previous-format"></a>Bijwerken van Hallo vorige indeling
De instellingen in Hallo vorige indeling (met de openbare eigenschappen Hallo ModulesUrl, ConfigurationFunction, SasToken of eigenschappen) automatisch aanpassen van de huidige indeling toohello en voer net zoals voor.

Hallo schema na is welke Hallo vorige-instellingenschema staande:

```json
"settings": {
    "WMFVersion": "latest",
    "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
    "SasToken": "SAS Token if ModulesUrl points tooprivate Azure Blob Storage",
    "ConfigurationFunction": "ConfigurationScript.ps1\\ConfigurationFunction",
    "Properties":  {
        "ParameterToConfigurationFunction1":  "Value1",
        "ParameterToConfigurationFunction2":  "Value2",
        "ParameterOfTypePSCredential1": {
            "UserName": "UsernameValue1",
            "Password": "PrivateSettingsRef:Key1" 
        },
        "ParameterOfTypePSCredential2": {
            "UserName": "UsernameValue2",
            "Password": "PrivateSettingsRef:Key2"
        }
    }
},
"protectedSettings": { 
    "Items": {
        "Key1": "PasswordValue1",
        "Key2": "PasswordValue2"
    },
    "DataBlobUri": "https://UrlToConfigurationDataWithOptionalSasToken.psd1"
}
```

Hier ziet u hoe de vorige indeling Hallo toohello huidige indeling aanpast:

| De naam van eigenschap | Vorige Schema Equivalent |
| --- | --- |
| settings.wmfVersion |Instellingen. WMFVersion |
| Settings.Configuration.URL |Instellingen. ModulesUrl |
| Settings.Configuration.script |Eerste deel van de instellingen. ConfigurationFunction (voordat '\\\\') |
| Settings.Configuration.Function |Tweede deel van de instellingen. ConfigurationFunction (nadat '\\\\') |
| settings.configurationArguments |Instellingen. Eigenschappen |
| settings.configurationData.url |protectedSettings.DataBlobUri (zonder SAS-token) |
| settings.privacy.dataEnabled |Instellingen. Privacy.DataEnabled |
| settings.advancedOptions.downloadMappings |Instellingen. AdvancedOptions.DownloadMappings |
| protectedSettings.configurationArguments |protectedSettings.Properties |
| protectedSettings.configurationUrlSasToken |Instellingen. SasToken |
| protectedSettings.configurationDataUrlSasToken |SAS-token van protectedSettings.DataBlobUri |

## <a name="troubleshooting---error-code-1100"></a>Probleemoplossing - foutcode 1100
Foutcode 1100 geeft aan dat er een probleem met de Hallo gebruikersinvoer toohello DSC-uitbreiding.
de tekst Hello van deze fouten variabele en kan worden gewijzigd.
Hier volgen enkele Hallo-fouten kunt en hoe u deze kunt oplossen.

### <a name="invalid-values"></a>Ongeldige waarden
'Privacy.dataCollection is {0}. Hallo alleen mogelijke waarden zijn ", 'Enable' en 'Disable'" 'WmfVersion is {0}. Alleen de mogelijke waarden zijn... en de 'nieuwste' '

Probleem: Een opgegeven waarde is niet toegestaan.

Oplossing: Hallo is een ongeldige waarde tooa geldige waarde wijzigen. Zie tabel in de sectie Details Hallo Hallo.

### <a name="invalid-url"></a>Ongeldige URL
'ConfigurationData.url is {0}. Dit is geen geldige URL' 'DataBlobUri is {0}. Dit is geen geldige URL' 'Configuration.url is {0}. Dit is geen geldige URL'

Probleem: Een opgegeven dat URL is niet geldig.

Oplossing: Controleer de opgegeven URL's. Zorg ervoor dat alle URL's oplossen toovalid locaties waartoe toegang op de externe computer Hallo Hallo-extensie heeft.

### <a name="invalid-configurationargument-type"></a>Ongeldig Type voor ConfigurationArgument
'Ongeldige configurationArguments type {0}'

Probleem: Hallo ConfigurationArguments-eigenschap kan tooa Hashtable-object niet omzetten. 

Oplossing: Controleer de eigenschap ConfigurationArguments een hashtabel. Ga als volgt in het voorgaande voorbeeld van Hallo Hallo-indeling. Kijk uit voor aanhalingstekens, komma's en accolades.

### <a name="duplicate-configurationarguments"></a>Dubbele ConfigurationArguments
'Dubbele argumenten {0} gevonden in de openbare en beveiligde configurationArguments'

Probleem: Hallo ConfigurationArguments in instellingen voor openbare en hello ConfigurationArguments in de instellingen van beveiligde eigenschappen bevatten Hello dezelfde naam.

Oplossing: Een van de dubbele eigenschappen Hallo verwijderen.

### <a name="missing-properties"></a>Ontbrekende eigenschappen
"Configuration.function moet configuration.url of configuration.module worden opgegeven."

"Configuration.url vereist dat configuration.script is opgegeven."

"Configuration.script vereist dat configuration.url is opgegeven."

"Configuration.url vereist dat configuration.function is opgegeven."

"ConfigurationUrlSasToken vereist dat configuration.url is opgegeven."

"ConfigurationDataUrlSasToken vereist dat configurationData.url is opgegeven."

Probleem: Een gedefinieerde eigenschap moet een andere eigenschap die ontbreekt.

Oplossingen: 

* Ontbrekende eigenschap Hallo bieden.
* Hallo-eigenschap die Hallo ontbrekende eigenschap moet te verwijderen.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over DSC en virtuele-machineschaalsets [met behulp van virtuele Machine Scale ingesteld Hello Azure DSC-uitbreiding](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)

Meer informatie vinden op [van DSC beveiligde Referentiebeheer](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Zie voor meer informatie over hello Azure DSC-uitbreiding handler [inleiding toohello Azure Desired State Configuration extensie handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Voor meer informatie over PowerShell DSC [gaat u naar de PowerShell-documentatiecentrum hello](https://msdn.microsoft.com/powershell/dsc/overview). 

