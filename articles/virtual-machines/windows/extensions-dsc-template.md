---
title: Desired State Configuration Resource Manager-sjabloon | Microsoft Docs
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
ms.openlocfilehash: 4292f9d8cd181073fdf0adff99fcb9624e0e9f55
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a><span data-ttu-id="f2616-103">Windows VMSS en Desired State Configuration met Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="f2616-103">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>
<span data-ttu-id="f2616-104">In dit artikel beschrijft de Resource Manager-sjabloon voor de [Desired State Configuration extensie handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f2616-104">This article describes the Resource Manager template for the [Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="template-example-for-a-windows-vm"></a><span data-ttu-id="f2616-105">Voorbeeld van de sjabloon voor een virtuele machine van Windows</span><span class="sxs-lookup"><span data-stu-id="f2616-105">Template example for a Windows VM</span></span>
<span data-ttu-id="f2616-106">Er geldt het volgende fragment in de sectie Resource van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f2616-106">The following snippet goes into the Resource section of the template.</span></span>

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

## <a name="template-example-for-windows-vmss"></a><span data-ttu-id="f2616-107">Voorbeeld van de sjabloon voor Windows VMSS</span><span class="sxs-lookup"><span data-stu-id="f2616-107">Template example for Windows VMSS</span></span>
<span data-ttu-id="f2616-108">Een knooppunt VMSS heeft een sectie 'Eigenschappen' met de 'VirtualMachineProfile', 'extensionProfile'-kenmerk.</span><span class="sxs-lookup"><span data-stu-id="f2616-108">A VMSS node has a "properties" section with the "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="f2616-109">DSC wordt toegevoegd onder 'extensions'.</span><span class="sxs-lookup"><span data-stu-id="f2616-109">DSC is added under "extensions".</span></span> 

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

## <a name="detailed-settings-information"></a><span data-ttu-id="f2616-110">Informatie over de gedetailleerde instellingen</span><span class="sxs-lookup"><span data-stu-id="f2616-110">Detailed Settings Information</span></span>
<span data-ttu-id="f2616-111">Het volgende schema is voor het gedeelte instellingen van de Azure DSC-uitbreiding in een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f2616-111">The following schema is for the settings portion of the Azure DSC extension in an Azure Resource Manager template.</span></span>

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

## <a name="details"></a><span data-ttu-id="f2616-112">Details</span><span class="sxs-lookup"><span data-stu-id="f2616-112">Details</span></span>
| <span data-ttu-id="f2616-113">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="f2616-113">Property Name</span></span> | <span data-ttu-id="f2616-114">Type</span><span class="sxs-lookup"><span data-stu-id="f2616-114">Type</span></span> | <span data-ttu-id="f2616-115">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f2616-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f2616-116">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="f2616-116">settings.wmfVersion</span></span> |<span data-ttu-id="f2616-117">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="f2616-117">string</span></span> |<span data-ttu-id="f2616-118">Hiermee geeft u de versie van het Windows Management Framework die op de virtuele machine moet worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f2616-118">Specifies the version of the Windows Management Framework that should be installed on your VM.</span></span> <span data-ttu-id="f2616-119">Als u deze eigenschap instelt op 'nieuwste' installeert de meest recente versie van WMF.</span><span class="sxs-lookup"><span data-stu-id="f2616-119">Setting this property to 'latest' installs the most updated version of WMF.</span></span> <span data-ttu-id="f2616-120">Mogelijke waarden voor deze eigenschap alleen huidige zijn **'4.0', '5.0', ' 5.0PP' en 'nieuwste'**.</span><span class="sxs-lookup"><span data-stu-id="f2616-120">The only current possible values for this property are **'4.0', '5.0', '5.0PP', and 'latest'**.</span></span> <span data-ttu-id="f2616-121">Deze mogelijke waarden zijn onderworpen aan updates.</span><span class="sxs-lookup"><span data-stu-id="f2616-121">These possible values are subject to updates.</span></span> <span data-ttu-id="f2616-122">De standaardwaarde is 'nieuwste'.</span><span class="sxs-lookup"><span data-stu-id="f2616-122">The default value is 'latest'.</span></span> |
| <span data-ttu-id="f2616-123">Settings.Configuration.URL</span><span class="sxs-lookup"><span data-stu-id="f2616-123">settings.configuration.url</span></span> |<span data-ttu-id="f2616-124">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="f2616-124">string</span></span> |<span data-ttu-id="f2616-125">Hiermee geeft u de URL-locatie van waaruit u uw DSC configuration zip-bestand te downloaden.</span><span class="sxs-lookup"><span data-stu-id="f2616-125">Specifies the URL location from which to download your DSC configuration zip file.</span></span> <span data-ttu-id="f2616-126">Als de URL die u een SAS-token is vereist om toegang te krijgen, moet u de eigenschap protectedSettings.configurationUrlSasToken ingesteld op de waarde van de SAS-token.</span><span class="sxs-lookup"><span data-stu-id="f2616-126">If the URL provided requires a SAS token for access, you need to set the protectedSettings.configurationUrlSasToken property to the value of your SAS token.</span></span> <span data-ttu-id="f2616-127">Deze eigenschap is vereist als settings.configuration.script en/of settings.configuration.function zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="f2616-127">This property is required if settings.configuration.script and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="f2616-128">Settings.Configuration.script</span><span class="sxs-lookup"><span data-stu-id="f2616-128">settings.configuration.script</span></span> |<span data-ttu-id="f2616-129">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="f2616-129">string</span></span> |<span data-ttu-id="f2616-130">Hiermee geeft u de bestandsnaam van het script met de definitie van de DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="f2616-130">Specifies the file name of the script that contains the definition of your DSC configuration.</span></span> <span data-ttu-id="f2616-131">Dit script moet zich in de hoofdmap van het zip-bestand van de URL die is opgegeven door de eigenschap configuration.url gedownload.</span><span class="sxs-lookup"><span data-stu-id="f2616-131">This script must be in the root folder of the zip file downloaded from the URL specified by the configuration.url property.</span></span> <span data-ttu-id="f2616-132">Deze eigenschap is vereist als settings.configuration.url en/of settings.configuration.script zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="f2616-132">This property is required if settings.configuration.url and/or settings.configuration.script are defined.</span></span> |
| <span data-ttu-id="f2616-133">Settings.Configuration.Function</span><span class="sxs-lookup"><span data-stu-id="f2616-133">settings.configuration.function</span></span> |<span data-ttu-id="f2616-134">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="f2616-134">string</span></span> |<span data-ttu-id="f2616-135">Geeft de naam van de DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="f2616-135">Specifies the name of your DSC configuration.</span></span> <span data-ttu-id="f2616-136">De configuratie met de naam moet worden opgenomen in het script dat is gedefinieerd door configuration.script.</span><span class="sxs-lookup"><span data-stu-id="f2616-136">The configuration named must be contained in the script defined by configuration.script.</span></span> <span data-ttu-id="f2616-137">Deze eigenschap is vereist als settings.configuration.url en/of settings.configuration.function zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="f2616-137">This property is required if settings.configuration.url and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="f2616-138">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="f2616-138">settings.configurationArguments</span></span> |<span data-ttu-id="f2616-139">Verzameling</span><span class="sxs-lookup"><span data-stu-id="f2616-139">Collection</span></span> |<span data-ttu-id="f2616-140">Hiermee definieert u de parameters die u wilt doorgeven aan uw DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="f2616-140">Defines any parameters you would like to pass to your DSC configuration.</span></span> <span data-ttu-id="f2616-141">Deze eigenschap is niet versleuteld.</span><span class="sxs-lookup"><span data-stu-id="f2616-141">This property is not encrypted.</span></span> |
| <span data-ttu-id="f2616-142">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="f2616-142">settings.configurationData.url</span></span> |<span data-ttu-id="f2616-143">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="f2616-143">string</span></span> |<span data-ttu-id="f2616-144">Geeft de URL waaruit u uw gegevens (.psd1) configuratiebestand te downloaden om te gebruiken als invoer voor uw DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="f2616-144">Specifies the URL from which to download your configuration data (.psd1) file to use as input for your DSC configuration.</span></span> <span data-ttu-id="f2616-145">Als de URL die u een SAS-token is vereist om toegang te krijgen, moet u de eigenschap protectedSettings.configurationDataUrlSasToken ingesteld op de waarde van de SAS-token.</span><span class="sxs-lookup"><span data-stu-id="f2616-145">If the URL provided requires a SAS token for access, you need to set the protectedSettings.configurationDataUrlSasToken property to the value of your SAS token.</span></span> |
| <span data-ttu-id="f2616-146">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="f2616-146">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="f2616-147">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="f2616-147">string</span></span> |<span data-ttu-id="f2616-148">Schakelt verzamelen van telemetriegegevens in of uit.</span><span class="sxs-lookup"><span data-stu-id="f2616-148">Enables or disables telemetry collection.</span></span> <span data-ttu-id="f2616-149">De enige mogelijke waarden voor deze eigenschap zijn **'Inschakelen', 'Uitschakelen', ', of $null**.</span><span class="sxs-lookup"><span data-stu-id="f2616-149">The only possible values for this property are **'Enable', 'Disable', '', or $null**.</span></span> <span data-ttu-id="f2616-150">Als u deze eigenschap leeg of null kan telemetrie.</span><span class="sxs-lookup"><span data-stu-id="f2616-150">Leaving this property blank or null enables telemetry.</span></span> <span data-ttu-id="f2616-151">De standaardwaarde is % d.</span><span class="sxs-lookup"><span data-stu-id="f2616-151">The default value is ''.</span></span> [<span data-ttu-id="f2616-152">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="f2616-152">More Information</span></span>](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| <span data-ttu-id="f2616-153">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="f2616-153">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="f2616-154">Verzameling</span><span class="sxs-lookup"><span data-stu-id="f2616-154">Collection</span></span> |<span data-ttu-id="f2616-155">Hiermee definieert u alternatieve locaties waarvan de WMF downloaden.</span><span class="sxs-lookup"><span data-stu-id="f2616-155">Defines alternate locations from which to download the WMF.</span></span> [<span data-ttu-id="f2616-156">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="f2616-156">More Information</span></span>](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| <span data-ttu-id="f2616-157">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="f2616-157">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="f2616-158">Verzameling</span><span class="sxs-lookup"><span data-stu-id="f2616-158">Collection</span></span> |<span data-ttu-id="f2616-159">Hiermee definieert u de parameters die u wilt doorgeven aan uw DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="f2616-159">Defines any parameters you would like to pass to your DSC configuration.</span></span> <span data-ttu-id="f2616-160">Deze eigenschap is versleuteld.</span><span class="sxs-lookup"><span data-stu-id="f2616-160">This property is encrypted.</span></span> |
| <span data-ttu-id="f2616-161">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="f2616-161">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="f2616-162">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="f2616-162">string</span></span> |<span data-ttu-id="f2616-163">Hiermee geeft u de SAS-token voor toegang tot de URL die is gedefinieerd door configuration.url.</span><span class="sxs-lookup"><span data-stu-id="f2616-163">Specifies the SAS token to access the URL defined by configuration.url.</span></span> <span data-ttu-id="f2616-164">Deze eigenschap is versleuteld.</span><span class="sxs-lookup"><span data-stu-id="f2616-164">This property is encrypted.</span></span> |
| <span data-ttu-id="f2616-165">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="f2616-165">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="f2616-166">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="f2616-166">string</span></span> |<span data-ttu-id="f2616-167">Hiermee geeft u de SAS-token voor toegang tot de URL die is gedefinieerd door configurationData.url.</span><span class="sxs-lookup"><span data-stu-id="f2616-167">Specifies the SAS token to access the URL defined by configurationData.url.</span></span> <span data-ttu-id="f2616-168">Deze eigenschap is versleuteld.</span><span class="sxs-lookup"><span data-stu-id="f2616-168">This property is encrypted.</span></span> |

## <a name="settings-vs-protectedsettings"></a><span data-ttu-id="f2616-169">Vs instellingen. ProtectedSettings</span><span class="sxs-lookup"><span data-stu-id="f2616-169">Settings vs. ProtectedSettings</span></span>
<span data-ttu-id="f2616-170">Alle instellingen worden opgeslagen in een tekstbestand instellingen op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f2616-170">All settings are saved in a settings text file on the VM.</span></span>
<span data-ttu-id="f2616-171">Eigenschappen onder 'instellingen' zijn eigenschappen public, omdat ze niet zijn versleuteld in het tekstbestand instellingen.</span><span class="sxs-lookup"><span data-stu-id="f2616-171">Properties under 'settings' are public properties because they are not encrypted in the settings text file.</span></span>
<span data-ttu-id="f2616-172">Eigenschappen onder 'protectedSettings' zijn versleuteld met een certificaat en worden niet weergegeven als tekst zonder opmaak in dit bestand op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f2616-172">Properties under 'protectedSettings' are encrypted with a certificate and are not shown in plain text in this file on the VM.</span></span>

<span data-ttu-id="f2616-173">Als de configuratie moet referenties, kunnen ze worden opgenomen in protectedSettings:</span><span class="sxs-lookup"><span data-stu-id="f2616-173">If the configuration needs credentials, they can be included in protectedSettings:</span></span>

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

## <a name="example"></a><span data-ttu-id="f2616-174">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="f2616-174">Example</span></span>
<span data-ttu-id="f2616-175">Het volgende voorbeeld is afgeleid van de sectie 'Aan de slag' van de [overzichtspagina DSC-uitbreiding Handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f2616-175">The following example derives from the "Getting Started" section of the [DSC Extension Handler Overview page](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
<span data-ttu-id="f2616-176">In dit voorbeeld maakt gebruik van Resource Manager-sjablonen in plaats van de cmdlets voor het implementeren van de extensie.</span><span class="sxs-lookup"><span data-stu-id="f2616-176">This example uses Resource Manager templates instead of cmdlets to deploy the extension.</span></span> <span data-ttu-id="f2616-177">Sla de configuratie 'IisInstall.ps1', plaats deze in een. ZIP-bestand en upload het bestand in een toegankelijke URL.</span><span class="sxs-lookup"><span data-stu-id="f2616-177">Save the "IisInstall.ps1" configuration, place it in a .ZIP file, and upload the file in an accessible URL.</span></span> <span data-ttu-id="f2616-178">In dit voorbeeld gebruikt Azure blob-opslag, maar het is mogelijk te downloaden. ZIP-bestanden vanaf elke willekeurige locatie.</span><span class="sxs-lookup"><span data-stu-id="f2616-178">This example uses Azure blob storage, but it is possible to download .ZIP files from any arbitrary location.</span></span>

<span data-ttu-id="f2616-179">De volgende code wordt in de Azure Resource Manager-sjabloon, de virtuele machine het juiste bestand downloaden en uitvoeren van de betreffende PowerShell-functie:</span><span class="sxs-lookup"><span data-stu-id="f2616-179">In the Azure Resource Manager template, the following code instructs the VM to download the correct file and run the appropriate PowerShell function:</span></span>

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

## <a name="updating-from-the-previous-format"></a><span data-ttu-id="f2616-180">Bijwerken van de vorige indeling</span><span class="sxs-lookup"><span data-stu-id="f2616-180">Updating from the Previous Format</span></span>
<span data-ttu-id="f2616-181">Alle instellingen in de vorige indeling (met de openbare eigenschappen ModulesUrl, ConfigurationFunction, SasToken of eigenschappen) automatisch aanpassen aan de huidige indeling en uitgevoerd, net zoals vroeger.</span><span class="sxs-lookup"><span data-stu-id="f2616-181">Any settings in the previous format (containing the public properties ModulesUrl, ConfigurationFunction, SasToken, or Properties) automatically adapt to the current format and run just as they did before.</span></span>

<span data-ttu-id="f2616-182">Het volgende schema is wat de vorige instellingenschema staande:</span><span class="sxs-lookup"><span data-stu-id="f2616-182">The following schema is what the previous settings schema looked like:</span></span>

```json
"settings": {
    "WMFVersion": "latest",
    "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
    "SasToken": "SAS Token if ModulesUrl points to private Azure Blob Storage",
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

<span data-ttu-id="f2616-183">Hier ziet u hoe de vorige indeling wordt aangepast aan de huidige indeling:</span><span class="sxs-lookup"><span data-stu-id="f2616-183">Here's how the previous format adapts to the current format:</span></span>

| <span data-ttu-id="f2616-184">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="f2616-184">Property Name</span></span> | <span data-ttu-id="f2616-185">Vorige Schema Equivalent</span><span class="sxs-lookup"><span data-stu-id="f2616-185">Previous Schema Equivalent</span></span> |
| --- | --- |
| <span data-ttu-id="f2616-186">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="f2616-186">settings.wmfVersion</span></span> |<span data-ttu-id="f2616-187">Instellingen. WMFVersion</span><span class="sxs-lookup"><span data-stu-id="f2616-187">settings.WMFVersion</span></span> |
| <span data-ttu-id="f2616-188">Settings.Configuration.URL</span><span class="sxs-lookup"><span data-stu-id="f2616-188">settings.configuration.url</span></span> |<span data-ttu-id="f2616-189">Instellingen. ModulesUrl</span><span class="sxs-lookup"><span data-stu-id="f2616-189">settings.ModulesUrl</span></span> |
| <span data-ttu-id="f2616-190">Settings.Configuration.script</span><span class="sxs-lookup"><span data-stu-id="f2616-190">settings.configuration.script</span></span> |<span data-ttu-id="f2616-191">Eerste deel van de instellingen. ConfigurationFunction (voordat '\\\\')</span><span class="sxs-lookup"><span data-stu-id="f2616-191">First part of settings.ConfigurationFunction (before '\\\\')</span></span> |
| <span data-ttu-id="f2616-192">Settings.Configuration.Function</span><span class="sxs-lookup"><span data-stu-id="f2616-192">settings.configuration.function</span></span> |<span data-ttu-id="f2616-193">Tweede deel van de instellingen. ConfigurationFunction (nadat '\\\\')</span><span class="sxs-lookup"><span data-stu-id="f2616-193">Second part of settings.ConfigurationFunction (after '\\\\')</span></span> |
| <span data-ttu-id="f2616-194">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="f2616-194">settings.configurationArguments</span></span> |<span data-ttu-id="f2616-195">Instellingen. Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="f2616-195">settings.Properties</span></span> |
| <span data-ttu-id="f2616-196">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="f2616-196">settings.configurationData.url</span></span> |<span data-ttu-id="f2616-197">protectedSettings.DataBlobUri (zonder SAS-token)</span><span class="sxs-lookup"><span data-stu-id="f2616-197">protectedSettings.DataBlobUri (without SAS token)</span></span> |
| <span data-ttu-id="f2616-198">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="f2616-198">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="f2616-199">Instellingen. Privacy.DataEnabled</span><span class="sxs-lookup"><span data-stu-id="f2616-199">settings.Privacy.DataEnabled</span></span> |
| <span data-ttu-id="f2616-200">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="f2616-200">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="f2616-201">Instellingen. AdvancedOptions.DownloadMappings</span><span class="sxs-lookup"><span data-stu-id="f2616-201">settings.AdvancedOptions.DownloadMappings</span></span> |
| <span data-ttu-id="f2616-202">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="f2616-202">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="f2616-203">protectedSettings.Properties</span><span class="sxs-lookup"><span data-stu-id="f2616-203">protectedSettings.Properties</span></span> |
| <span data-ttu-id="f2616-204">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="f2616-204">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="f2616-205">Instellingen. SasToken</span><span class="sxs-lookup"><span data-stu-id="f2616-205">settings.SasToken</span></span> |
| <span data-ttu-id="f2616-206">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="f2616-206">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="f2616-207">SAS-token van protectedSettings.DataBlobUri</span><span class="sxs-lookup"><span data-stu-id="f2616-207">SAS token from protectedSettings.DataBlobUri</span></span> |

## <a name="troubleshooting---error-code-1100"></a><span data-ttu-id="f2616-208">Probleemoplossing - foutcode 1100</span><span class="sxs-lookup"><span data-stu-id="f2616-208">Troubleshooting - Error Code 1100</span></span>
<span data-ttu-id="f2616-209">Foutcode 1100 geeft aan dat er een probleem met de invoer van de gebruiker toe aan de DSC-uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="f2616-209">Error Code 1100 indicates that there is a problem with the user input to the DSC extension.</span></span>
<span data-ttu-id="f2616-210">De tekst van deze fouten variabele en kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="f2616-210">The text of these errors is variable and may change.</span></span>
<span data-ttu-id="f2616-211">Hier zijn enkele van de fouten die mogelijk worden uitgevoerd in- en hoe u deze kunt oplossen.</span><span class="sxs-lookup"><span data-stu-id="f2616-211">Here are some of the errors you may run into and how you can fix them.</span></span>

### <a name="invalid-values"></a><span data-ttu-id="f2616-212">Ongeldige waarden</span><span class="sxs-lookup"><span data-stu-id="f2616-212">Invalid Values</span></span>
<span data-ttu-id="f2616-213">'Privacy.dataCollection is {0}.</span><span class="sxs-lookup"><span data-stu-id="f2616-213">"Privacy.dataCollection is '{0}'.</span></span> <span data-ttu-id="f2616-214">De enige mogelijke waarden zijn ", 'Enable' en 'Disable'" 'WmfVersion is {0}.</span><span class="sxs-lookup"><span data-stu-id="f2616-214">The only possible values are '', 'Enable', and 'Disable'" "WmfVersion is '{0}'.</span></span> <span data-ttu-id="f2616-215">Alleen de mogelijke waarden zijn...</span><span class="sxs-lookup"><span data-stu-id="f2616-215">Only possible values are …</span></span> <span data-ttu-id="f2616-216">en de 'nieuwste' '</span><span class="sxs-lookup"><span data-stu-id="f2616-216">and 'latest'"</span></span>

<span data-ttu-id="f2616-217">Probleem: Een opgegeven waarde is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="f2616-217">Problem: A provided value is not allowed.</span></span>

<span data-ttu-id="f2616-218">Oplossing: Wijzig de ongeldige waarde in een geldige waarde.</span><span class="sxs-lookup"><span data-stu-id="f2616-218">Solution: Change the invalid value to a valid value.</span></span> <span data-ttu-id="f2616-219">Zie de tabel in de sectie Details.</span><span class="sxs-lookup"><span data-stu-id="f2616-219">See the table in the Details section.</span></span>

### <a name="invalid-url"></a><span data-ttu-id="f2616-220">Ongeldige URL</span><span class="sxs-lookup"><span data-stu-id="f2616-220">Invalid URL</span></span>
<span data-ttu-id="f2616-221">'ConfigurationData.url is {0}.</span><span class="sxs-lookup"><span data-stu-id="f2616-221">"ConfigurationData.url is '{0}'.</span></span> <span data-ttu-id="f2616-222">Dit is geen geldige URL' 'DataBlobUri is {0}.</span><span class="sxs-lookup"><span data-stu-id="f2616-222">This is not a valid URL" "DataBlobUri is '{0}'.</span></span> <span data-ttu-id="f2616-223">Dit is geen geldige URL' 'Configuration.url is {0}.</span><span class="sxs-lookup"><span data-stu-id="f2616-223">This is not a valid URL" "Configuration.url is '{0}'.</span></span> <span data-ttu-id="f2616-224">Dit is geen geldige URL'</span><span class="sxs-lookup"><span data-stu-id="f2616-224">This is not a valid URL"</span></span>

<span data-ttu-id="f2616-225">Probleem: Een opgegeven dat URL is niet geldig.</span><span class="sxs-lookup"><span data-stu-id="f2616-225">Problem: A provided URL is not valid.</span></span>

<span data-ttu-id="f2616-226">Oplossing: Controleer de opgegeven URL's.</span><span class="sxs-lookup"><span data-stu-id="f2616-226">Solution: Check all your provided URLs.</span></span> <span data-ttu-id="f2616-227">Zorg ervoor dat alle URL's omgezet naar geldige locaties dat de uitbreiding op de externe computer openen kunt.</span><span class="sxs-lookup"><span data-stu-id="f2616-227">Make sure all URLs resolve to valid locations that the extension can access on the remote machine.</span></span>

### <a name="invalid-configurationargument-type"></a><span data-ttu-id="f2616-228">Ongeldig Type voor ConfigurationArgument</span><span class="sxs-lookup"><span data-stu-id="f2616-228">Invalid ConfigurationArgument Type</span></span>
<span data-ttu-id="f2616-229">'Ongeldige configurationArguments type {0}'</span><span class="sxs-lookup"><span data-stu-id="f2616-229">"Invalid configurationArguments type {0}"</span></span>

<span data-ttu-id="f2616-230">Probleem: De eigenschap ConfigurationArguments kan niet worden omgezet in een hash-object.</span><span class="sxs-lookup"><span data-stu-id="f2616-230">Problem: The ConfigurationArguments property cannot resolve to a Hashtable object.</span></span> 

<span data-ttu-id="f2616-231">Oplossing: Controleer de eigenschap ConfigurationArguments een hashtabel.</span><span class="sxs-lookup"><span data-stu-id="f2616-231">Solution: Make your ConfigurationArguments property a Hashtable.</span></span> <span data-ttu-id="f2616-232">Volg de indeling die is opgegeven in het voorgaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f2616-232">Follow the format provided in the preceeding example.</span></span> <span data-ttu-id="f2616-233">Kijk uit voor aanhalingstekens, komma's en accolades.</span><span class="sxs-lookup"><span data-stu-id="f2616-233">Watch out for quotes, commas, and braces.</span></span>

### <a name="duplicate-configurationarguments"></a><span data-ttu-id="f2616-234">Dubbele ConfigurationArguments</span><span class="sxs-lookup"><span data-stu-id="f2616-234">Duplicate ConfigurationArguments</span></span>
<span data-ttu-id="f2616-235">'Dubbele argumenten {0} gevonden in de openbare en beveiligde configurationArguments'</span><span class="sxs-lookup"><span data-stu-id="f2616-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments"</span></span>

<span data-ttu-id="f2616-236">Probleem: De ConfigurationArguments in instellingen voor openbare en de ConfigurationArguments in beveiligde instellingen bevatten eigenschappen met dezelfde naam.</span><span class="sxs-lookup"><span data-stu-id="f2616-236">Problem: The ConfigurationArguments in public settings and the ConfigurationArguments in protected settings contain properties with the same name.</span></span>

<span data-ttu-id="f2616-237">Oplossing: Verwijder een van de dubbele eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="f2616-237">Solution: Remove one of the duplicate properties.</span></span>

### <a name="missing-properties"></a><span data-ttu-id="f2616-238">Ontbrekende eigenschappen</span><span class="sxs-lookup"><span data-stu-id="f2616-238">Missing Properties</span></span>
<span data-ttu-id="f2616-239">"Configuration.function moet configuration.url of configuration.module worden opgegeven."</span><span class="sxs-lookup"><span data-stu-id="f2616-239">"Configuration.function requires that configuration.url or configuration.module is specified"</span></span>

<span data-ttu-id="f2616-240">"Configuration.url vereist dat configuration.script is opgegeven."</span><span class="sxs-lookup"><span data-stu-id="f2616-240">"Configuration.url requires that configuration.script is specified"</span></span>

<span data-ttu-id="f2616-241">"Configuration.script vereist dat configuration.url is opgegeven."</span><span class="sxs-lookup"><span data-stu-id="f2616-241">"Configuration.script requires that configuration.url is specified"</span></span>

<span data-ttu-id="f2616-242">"Configuration.url vereist dat configuration.function is opgegeven."</span><span class="sxs-lookup"><span data-stu-id="f2616-242">"Configuration.url requires that configuration.function is specified"</span></span>

<span data-ttu-id="f2616-243">"ConfigurationUrlSasToken vereist dat configuration.url is opgegeven."</span><span class="sxs-lookup"><span data-stu-id="f2616-243">"ConfigurationUrlSasToken requires that configuration.url is specified"</span></span>

<span data-ttu-id="f2616-244">"ConfigurationDataUrlSasToken vereist dat configurationData.url is opgegeven."</span><span class="sxs-lookup"><span data-stu-id="f2616-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified"</span></span>

<span data-ttu-id="f2616-245">Probleem: Een gedefinieerde eigenschap moet een andere eigenschap die ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="f2616-245">Problem: A defined property needs another property that is missing.</span></span>

<span data-ttu-id="f2616-246">Oplossingen:</span><span class="sxs-lookup"><span data-stu-id="f2616-246">Solutions:</span></span> 

* <span data-ttu-id="f2616-247">Geef de eigenschap ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="f2616-247">Provide the missing property.</span></span>
* <span data-ttu-id="f2616-248">Verwijder de eigenschap die de eigenschap ontbreekt moet.</span><span class="sxs-lookup"><span data-stu-id="f2616-248">Remove the property that needs the missing property.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2616-249">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f2616-249">Next Steps</span></span>
<span data-ttu-id="f2616-250">Meer informatie over DSC en virtuele-machineschaalsets [virtuele Machine schaal wordt ingesteld met de Azure DSC-extensie](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span><span class="sxs-lookup"><span data-stu-id="f2616-250">Learn about DSC and virtual machine scale sets in [Using Virtual Machine Scale Sets with the Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span></span>

<span data-ttu-id="f2616-251">Meer informatie vinden op [van DSC beveiligde Referentiebeheer](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f2616-251">Find more details on [DSC's secure credential management](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="f2616-252">Zie voor meer informatie over de Azure DSC-uitbreiding handler [Inleiding tot de extensie Azure Desired State Configuration handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f2616-252">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="f2616-253">Voor meer informatie over PowerShell DSC [gaat u naar de PowerShell-documentatiecentrum](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="f2616-253">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

