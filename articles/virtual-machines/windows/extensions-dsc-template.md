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
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a><span data-ttu-id="6d823-103">Windows VMSS en Desired State Configuration met Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="6d823-103">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>
<span data-ttu-id="6d823-104">Dit artikel wordt beschreven Hallo Resource Manager-sjabloon voor Hallo [Desired State Configuration extensie handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6d823-104">This article describes hello Resource Manager template for hello [Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="template-example-for-a-windows-vm"></a><span data-ttu-id="6d823-105">Voorbeeld van de sjabloon voor een virtuele machine van Windows</span><span class="sxs-lookup"><span data-stu-id="6d823-105">Template example for a Windows VM</span></span>
<span data-ttu-id="6d823-106">Hallo probeert volgende fragment het Hallo gedeelte van de Resource van Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="6d823-106">hello following snippet goes into hello Resource section of hello template.</span></span>

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

## <a name="template-example-for-windows-vmss"></a><span data-ttu-id="6d823-107">Voorbeeld van de sjabloon voor Windows VMSS</span><span class="sxs-lookup"><span data-stu-id="6d823-107">Template example for Windows VMSS</span></span>
<span data-ttu-id="6d823-108">Een knooppunt VMSS heeft een sectie 'Eigenschappen' Hello 'VirtualMachineProfile', 'extensionProfile'-kenmerk.</span><span class="sxs-lookup"><span data-stu-id="6d823-108">A VMSS node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="6d823-109">DSC wordt toegevoegd onder 'extensions'.</span><span class="sxs-lookup"><span data-stu-id="6d823-109">DSC is added under "extensions".</span></span> 

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

## <a name="detailed-settings-information"></a><span data-ttu-id="6d823-110">Informatie over de gedetailleerde instellingen</span><span class="sxs-lookup"><span data-stu-id="6d823-110">Detailed Settings Information</span></span>
<span data-ttu-id="6d823-111">Hallo is volgende schema Hallo instellingen deel van het hello Azure DSC-uitbreiding in een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="6d823-111">hello following schema is for hello settings portion of hello Azure DSC extension in an Azure Resource Manager template.</span></span>

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

## <a name="details"></a><span data-ttu-id="6d823-112">Details</span><span class="sxs-lookup"><span data-stu-id="6d823-112">Details</span></span>
| <span data-ttu-id="6d823-113">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="6d823-113">Property Name</span></span> | <span data-ttu-id="6d823-114">Type</span><span class="sxs-lookup"><span data-stu-id="6d823-114">Type</span></span> | <span data-ttu-id="6d823-115">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6d823-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d823-116">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="6d823-116">settings.wmfVersion</span></span> |<span data-ttu-id="6d823-117">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6d823-117">string</span></span> |<span data-ttu-id="6d823-118">Hiermee wordt de versie Hallo Hallo Windows Management Framework die op de virtuele machine moet worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6d823-118">Specifies hello version of hello Windows Management Framework that should be installed on your VM.</span></span> <span data-ttu-id="6d823-119">Deze eigenschap too'latest instellen ' installeert Hallo meest recente versie van WMF.</span><span class="sxs-lookup"><span data-stu-id="6d823-119">Setting this property too'latest' installs hello most updated version of WMF.</span></span> <span data-ttu-id="6d823-120">Hallo alleen huidige mogelijke waarden voor deze eigenschap zijn **'4.0', '5.0', ' 5.0PP' en 'nieuwste'**.</span><span class="sxs-lookup"><span data-stu-id="6d823-120">hello only current possible values for this property are **'4.0', '5.0', '5.0PP', and 'latest'**.</span></span> <span data-ttu-id="6d823-121">Deze mogelijke waarden zijn tooupdates onderwerp.</span><span class="sxs-lookup"><span data-stu-id="6d823-121">These possible values are subject tooupdates.</span></span> <span data-ttu-id="6d823-122">Hallo-standaardwaarde is 'nieuwste'.</span><span class="sxs-lookup"><span data-stu-id="6d823-122">hello default value is 'latest'.</span></span> |
| <span data-ttu-id="6d823-123">Settings.Configuration.URL</span><span class="sxs-lookup"><span data-stu-id="6d823-123">settings.configuration.url</span></span> |<span data-ttu-id="6d823-124">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6d823-124">string</span></span> |<span data-ttu-id="6d823-125">Hiermee geeft u het zip-bestand van de DSC-configuratie Hallo URL-locatie van welke toodownload.</span><span class="sxs-lookup"><span data-stu-id="6d823-125">Specifies hello URL location from which toodownload your DSC configuration zip file.</span></span> <span data-ttu-id="6d823-126">Als een SAS-token Hallo-URL opgegeven om toegang te krijgen vereist, moet u tooset hello protectedSettings.configurationUrlSasToken toohello eigenschapswaarde van SAS-token.</span><span class="sxs-lookup"><span data-stu-id="6d823-126">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationUrlSasToken property toohello value of your SAS token.</span></span> <span data-ttu-id="6d823-127">Deze eigenschap is vereist als settings.configuration.script en/of settings.configuration.function zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="6d823-127">This property is required if settings.configuration.script and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="6d823-128">Settings.Configuration.script</span><span class="sxs-lookup"><span data-stu-id="6d823-128">settings.configuration.script</span></span> |<span data-ttu-id="6d823-129">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6d823-129">string</span></span> |<span data-ttu-id="6d823-130">Geeft de bestandsnaam Hallo van Hallo-script dat Hallo definitie van de DSC-configuratie bevat.</span><span class="sxs-lookup"><span data-stu-id="6d823-130">Specifies hello file name of hello script that contains hello definition of your DSC configuration.</span></span> <span data-ttu-id="6d823-131">Dit script moet in de hoofdmap Hallo van Hallo zip-bestand is gedownload van Hallo URL die is opgegeven door Hallo configuration.url eigenschap.</span><span class="sxs-lookup"><span data-stu-id="6d823-131">This script must be in hello root folder of hello zip file downloaded from hello URL specified by hello configuration.url property.</span></span> <span data-ttu-id="6d823-132">Deze eigenschap is vereist als settings.configuration.url en/of settings.configuration.script zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="6d823-132">This property is required if settings.configuration.url and/or settings.configuration.script are defined.</span></span> |
| <span data-ttu-id="6d823-133">Settings.Configuration.Function</span><span class="sxs-lookup"><span data-stu-id="6d823-133">settings.configuration.function</span></span> |<span data-ttu-id="6d823-134">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6d823-134">string</span></span> |<span data-ttu-id="6d823-135">Hiermee geeft u Hallo-naam van de DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="6d823-135">Specifies hello name of your DSC configuration.</span></span> <span data-ttu-id="6d823-136">Hallo-configuratie met de naam moet worden opgenomen in Hallo script gedefinieerd door configuration.script.</span><span class="sxs-lookup"><span data-stu-id="6d823-136">hello configuration named must be contained in hello script defined by configuration.script.</span></span> <span data-ttu-id="6d823-137">Deze eigenschap is vereist als settings.configuration.url en/of settings.configuration.function zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="6d823-137">This property is required if settings.configuration.url and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="6d823-138">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="6d823-138">settings.configurationArguments</span></span> |<span data-ttu-id="6d823-139">Verzameling</span><span class="sxs-lookup"><span data-stu-id="6d823-139">Collection</span></span> |<span data-ttu-id="6d823-140">Hiermee definieert u de parameters die u wilt dat toopass tooyour DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="6d823-140">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="6d823-141">Deze eigenschap is niet versleuteld.</span><span class="sxs-lookup"><span data-stu-id="6d823-141">This property is not encrypted.</span></span> |
| <span data-ttu-id="6d823-142">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="6d823-142">settings.configurationData.url</span></span> |<span data-ttu-id="6d823-143">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6d823-143">string</span></span> |<span data-ttu-id="6d823-144">Hiermee geeft u Hallo-URL van welke toodownload uw configuratiegegevens (.psd1) toouse bestand als invoer voor uw DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="6d823-144">Specifies hello URL from which toodownload your configuration data (.psd1) file toouse as input for your DSC configuration.</span></span> <span data-ttu-id="6d823-145">Als een SAS-token Hallo-URL opgegeven om toegang te krijgen vereist, moet u tooset hello protectedSettings.configurationDataUrlSasToken toohello eigenschapswaarde van SAS-token.</span><span class="sxs-lookup"><span data-stu-id="6d823-145">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationDataUrlSasToken property toohello value of your SAS token.</span></span> |
| <span data-ttu-id="6d823-146">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="6d823-146">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="6d823-147">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6d823-147">string</span></span> |<span data-ttu-id="6d823-148">Schakelt verzamelen van telemetriegegevens in of uit.</span><span class="sxs-lookup"><span data-stu-id="6d823-148">Enables or disables telemetry collection.</span></span> <span data-ttu-id="6d823-149">Hallo alleen mogelijke waarden voor deze eigenschap zijn **'Inschakelen', 'Uitschakelen', ', of $null**.</span><span class="sxs-lookup"><span data-stu-id="6d823-149">hello only possible values for this property are **'Enable', 'Disable', '', or $null**.</span></span> <span data-ttu-id="6d823-150">Als u deze eigenschap leeg of null kan telemetrie.</span><span class="sxs-lookup"><span data-stu-id="6d823-150">Leaving this property blank or null enables telemetry.</span></span> <span data-ttu-id="6d823-151">de standaardwaarde Hallo is ''.</span><span class="sxs-lookup"><span data-stu-id="6d823-151">hello default value is ''.</span></span> [<span data-ttu-id="6d823-152">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="6d823-152">More Information</span></span>](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| <span data-ttu-id="6d823-153">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="6d823-153">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="6d823-154">Verzameling</span><span class="sxs-lookup"><span data-stu-id="6d823-154">Collection</span></span> |<span data-ttu-id="6d823-155">Alternatieve locaties die van welke toodownload Hallo WMF definieert.</span><span class="sxs-lookup"><span data-stu-id="6d823-155">Defines alternate locations from which toodownload hello WMF.</span></span> [<span data-ttu-id="6d823-156">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="6d823-156">More Information</span></span>](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| <span data-ttu-id="6d823-157">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="6d823-157">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="6d823-158">Verzameling</span><span class="sxs-lookup"><span data-stu-id="6d823-158">Collection</span></span> |<span data-ttu-id="6d823-159">Hiermee definieert u de parameters die u wilt dat toopass tooyour DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="6d823-159">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="6d823-160">Deze eigenschap is versleuteld.</span><span class="sxs-lookup"><span data-stu-id="6d823-160">This property is encrypted.</span></span> |
| <span data-ttu-id="6d823-161">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="6d823-161">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="6d823-162">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6d823-162">string</span></span> |<span data-ttu-id="6d823-163">Hiermee geeft u Hallo SAS-token tooaccess Hallo URL die is gedefinieerd door configuration.url.</span><span class="sxs-lookup"><span data-stu-id="6d823-163">Specifies hello SAS token tooaccess hello URL defined by configuration.url.</span></span> <span data-ttu-id="6d823-164">Deze eigenschap is versleuteld.</span><span class="sxs-lookup"><span data-stu-id="6d823-164">This property is encrypted.</span></span> |
| <span data-ttu-id="6d823-165">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="6d823-165">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="6d823-166">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6d823-166">string</span></span> |<span data-ttu-id="6d823-167">Hiermee geeft u Hallo SAS-token tooaccess Hallo URL die is gedefinieerd door configurationData.url.</span><span class="sxs-lookup"><span data-stu-id="6d823-167">Specifies hello SAS token tooaccess hello URL defined by configurationData.url.</span></span> <span data-ttu-id="6d823-168">Deze eigenschap is versleuteld.</span><span class="sxs-lookup"><span data-stu-id="6d823-168">This property is encrypted.</span></span> |

## <a name="settings-vs-protectedsettings"></a><span data-ttu-id="6d823-169">Vs instellingen. ProtectedSettings</span><span class="sxs-lookup"><span data-stu-id="6d823-169">Settings vs. ProtectedSettings</span></span>
<span data-ttu-id="6d823-170">Alle instellingen worden opgeslagen in een tekstbestand instellingen op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="6d823-170">All settings are saved in a settings text file on hello VM.</span></span>
<span data-ttu-id="6d823-171">Eigenschappen onder 'instellingen' zijn eigenschappen public, omdat ze niet zijn versleuteld in tekstbestand Hallo-instellingen.</span><span class="sxs-lookup"><span data-stu-id="6d823-171">Properties under 'settings' are public properties because they are not encrypted in hello settings text file.</span></span>
<span data-ttu-id="6d823-172">Eigenschappen onder 'protectedSettings' zijn versleuteld met een certificaat en worden niet weergegeven als tekst zonder opmaak in dit bestand op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="6d823-172">Properties under 'protectedSettings' are encrypted with a certificate and are not shown in plain text in this file on hello VM.</span></span>

<span data-ttu-id="6d823-173">Als Hallo configuratie moet referenties, kunnen ze worden opgenomen in protectedSettings:</span><span class="sxs-lookup"><span data-stu-id="6d823-173">If hello configuration needs credentials, they can be included in protectedSettings:</span></span>

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

## <a name="example"></a><span data-ttu-id="6d823-174">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="6d823-174">Example</span></span>
<span data-ttu-id="6d823-175">Hallo volgende voorbeeld is afgeleid van Hallo sectie 'Aan de slag' Hallo [overzichtspagina DSC-uitbreiding Handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6d823-175">hello following example derives from hello "Getting Started" section of hello [DSC Extension Handler Overview page](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
<span data-ttu-id="6d823-176">In dit voorbeeld maakt gebruik van Resource Manager-sjablonen in plaats van cmdlets toodeploy Hallo-extensie.</span><span class="sxs-lookup"><span data-stu-id="6d823-176">This example uses Resource Manager templates instead of cmdlets toodeploy hello extension.</span></span> <span data-ttu-id="6d823-177">Hallo 'IisInstall.ps1' configuratie op te slaan, plaatst u deze in een. ZIP-bestand en het uploaden van Hallo-bestand in een toegankelijke URL.</span><span class="sxs-lookup"><span data-stu-id="6d823-177">Save hello "IisInstall.ps1" configuration, place it in a .ZIP file, and upload hello file in an accessible URL.</span></span> <span data-ttu-id="6d823-178">In dit voorbeeld wordt een Azure blob-opslag, maar het is mogelijk toodownload. ZIP-bestanden vanaf elke willekeurige locatie.</span><span class="sxs-lookup"><span data-stu-id="6d823-178">This example uses Azure blob storage, but it is possible toodownload .ZIP files from any arbitrary location.</span></span>

<span data-ttu-id="6d823-179">In hello Azure Resource Manager-sjabloon, hello volgende code geeft opdracht Hallo VM toodownload Hallo juiste bestand en Voer Hallo betreffende PowerShell functie:</span><span class="sxs-lookup"><span data-stu-id="6d823-179">In hello Azure Resource Manager template, hello following code instructs hello VM toodownload hello correct file and run hello appropriate PowerShell function:</span></span>

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

## <a name="updating-from-hello-previous-format"></a><span data-ttu-id="6d823-180">Bijwerken van Hallo vorige indeling</span><span class="sxs-lookup"><span data-stu-id="6d823-180">Updating from hello Previous Format</span></span>
<span data-ttu-id="6d823-181">De instellingen in Hallo vorige indeling (met de openbare eigenschappen Hallo ModulesUrl, ConfigurationFunction, SasToken of eigenschappen) automatisch aanpassen van de huidige indeling toohello en voer net zoals voor.</span><span class="sxs-lookup"><span data-stu-id="6d823-181">Any settings in hello previous format (containing hello public properties ModulesUrl, ConfigurationFunction, SasToken, or Properties) automatically adapt toohello current format and run just as they did before.</span></span>

<span data-ttu-id="6d823-182">Hallo schema na is welke Hallo vorige-instellingenschema staande:</span><span class="sxs-lookup"><span data-stu-id="6d823-182">hello following schema is what hello previous settings schema looked like:</span></span>

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

<span data-ttu-id="6d823-183">Hier ziet u hoe de vorige indeling Hallo toohello huidige indeling aanpast:</span><span class="sxs-lookup"><span data-stu-id="6d823-183">Here's how hello previous format adapts toohello current format:</span></span>

| <span data-ttu-id="6d823-184">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="6d823-184">Property Name</span></span> | <span data-ttu-id="6d823-185">Vorige Schema Equivalent</span><span class="sxs-lookup"><span data-stu-id="6d823-185">Previous Schema Equivalent</span></span> |
| --- | --- |
| <span data-ttu-id="6d823-186">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="6d823-186">settings.wmfVersion</span></span> |<span data-ttu-id="6d823-187">Instellingen. WMFVersion</span><span class="sxs-lookup"><span data-stu-id="6d823-187">settings.WMFVersion</span></span> |
| <span data-ttu-id="6d823-188">Settings.Configuration.URL</span><span class="sxs-lookup"><span data-stu-id="6d823-188">settings.configuration.url</span></span> |<span data-ttu-id="6d823-189">Instellingen. ModulesUrl</span><span class="sxs-lookup"><span data-stu-id="6d823-189">settings.ModulesUrl</span></span> |
| <span data-ttu-id="6d823-190">Settings.Configuration.script</span><span class="sxs-lookup"><span data-stu-id="6d823-190">settings.configuration.script</span></span> |<span data-ttu-id="6d823-191">Eerste deel van de instellingen. ConfigurationFunction (voordat '\\\\')</span><span class="sxs-lookup"><span data-stu-id="6d823-191">First part of settings.ConfigurationFunction (before '\\\\')</span></span> |
| <span data-ttu-id="6d823-192">Settings.Configuration.Function</span><span class="sxs-lookup"><span data-stu-id="6d823-192">settings.configuration.function</span></span> |<span data-ttu-id="6d823-193">Tweede deel van de instellingen. ConfigurationFunction (nadat '\\\\')</span><span class="sxs-lookup"><span data-stu-id="6d823-193">Second part of settings.ConfigurationFunction (after '\\\\')</span></span> |
| <span data-ttu-id="6d823-194">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="6d823-194">settings.configurationArguments</span></span> |<span data-ttu-id="6d823-195">Instellingen. Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="6d823-195">settings.Properties</span></span> |
| <span data-ttu-id="6d823-196">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="6d823-196">settings.configurationData.url</span></span> |<span data-ttu-id="6d823-197">protectedSettings.DataBlobUri (zonder SAS-token)</span><span class="sxs-lookup"><span data-stu-id="6d823-197">protectedSettings.DataBlobUri (without SAS token)</span></span> |
| <span data-ttu-id="6d823-198">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="6d823-198">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="6d823-199">Instellingen. Privacy.DataEnabled</span><span class="sxs-lookup"><span data-stu-id="6d823-199">settings.Privacy.DataEnabled</span></span> |
| <span data-ttu-id="6d823-200">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="6d823-200">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="6d823-201">Instellingen. AdvancedOptions.DownloadMappings</span><span class="sxs-lookup"><span data-stu-id="6d823-201">settings.AdvancedOptions.DownloadMappings</span></span> |
| <span data-ttu-id="6d823-202">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="6d823-202">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="6d823-203">protectedSettings.Properties</span><span class="sxs-lookup"><span data-stu-id="6d823-203">protectedSettings.Properties</span></span> |
| <span data-ttu-id="6d823-204">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="6d823-204">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="6d823-205">Instellingen. SasToken</span><span class="sxs-lookup"><span data-stu-id="6d823-205">settings.SasToken</span></span> |
| <span data-ttu-id="6d823-206">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="6d823-206">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="6d823-207">SAS-token van protectedSettings.DataBlobUri</span><span class="sxs-lookup"><span data-stu-id="6d823-207">SAS token from protectedSettings.DataBlobUri</span></span> |

## <a name="troubleshooting---error-code-1100"></a><span data-ttu-id="6d823-208">Probleemoplossing - foutcode 1100</span><span class="sxs-lookup"><span data-stu-id="6d823-208">Troubleshooting - Error Code 1100</span></span>
<span data-ttu-id="6d823-209">Foutcode 1100 geeft aan dat er een probleem met de Hallo gebruikersinvoer toohello DSC-uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="6d823-209">Error Code 1100 indicates that there is a problem with hello user input toohello DSC extension.</span></span>
<span data-ttu-id="6d823-210">de tekst Hello van deze fouten variabele en kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="6d823-210">hello text of these errors is variable and may change.</span></span>
<span data-ttu-id="6d823-211">Hier volgen enkele Hallo-fouten kunt en hoe u deze kunt oplossen.</span><span class="sxs-lookup"><span data-stu-id="6d823-211">Here are some of hello errors you may run into and how you can fix them.</span></span>

### <a name="invalid-values"></a><span data-ttu-id="6d823-212">Ongeldige waarden</span><span class="sxs-lookup"><span data-stu-id="6d823-212">Invalid Values</span></span>
<span data-ttu-id="6d823-213">'Privacy.dataCollection is {0}.</span><span class="sxs-lookup"><span data-stu-id="6d823-213">"Privacy.dataCollection is '{0}'.</span></span> <span data-ttu-id="6d823-214">Hallo alleen mogelijke waarden zijn ", 'Enable' en 'Disable'" 'WmfVersion is {0}.</span><span class="sxs-lookup"><span data-stu-id="6d823-214">hello only possible values are '', 'Enable', and 'Disable'" "WmfVersion is '{0}'.</span></span> <span data-ttu-id="6d823-215">Alleen de mogelijke waarden zijn...</span><span class="sxs-lookup"><span data-stu-id="6d823-215">Only possible values are …</span></span> <span data-ttu-id="6d823-216">en de 'nieuwste' '</span><span class="sxs-lookup"><span data-stu-id="6d823-216">and 'latest'"</span></span>

<span data-ttu-id="6d823-217">Probleem: Een opgegeven waarde is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="6d823-217">Problem: A provided value is not allowed.</span></span>

<span data-ttu-id="6d823-218">Oplossing: Hallo is een ongeldige waarde tooa geldige waarde wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6d823-218">Solution: Change hello invalid value tooa valid value.</span></span> <span data-ttu-id="6d823-219">Zie tabel in de sectie Details Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="6d823-219">See hello table in hello Details section.</span></span>

### <a name="invalid-url"></a><span data-ttu-id="6d823-220">Ongeldige URL</span><span class="sxs-lookup"><span data-stu-id="6d823-220">Invalid URL</span></span>
<span data-ttu-id="6d823-221">'ConfigurationData.url is {0}.</span><span class="sxs-lookup"><span data-stu-id="6d823-221">"ConfigurationData.url is '{0}'.</span></span> <span data-ttu-id="6d823-222">Dit is geen geldige URL' 'DataBlobUri is {0}.</span><span class="sxs-lookup"><span data-stu-id="6d823-222">This is not a valid URL" "DataBlobUri is '{0}'.</span></span> <span data-ttu-id="6d823-223">Dit is geen geldige URL' 'Configuration.url is {0}.</span><span class="sxs-lookup"><span data-stu-id="6d823-223">This is not a valid URL" "Configuration.url is '{0}'.</span></span> <span data-ttu-id="6d823-224">Dit is geen geldige URL'</span><span class="sxs-lookup"><span data-stu-id="6d823-224">This is not a valid URL"</span></span>

<span data-ttu-id="6d823-225">Probleem: Een opgegeven dat URL is niet geldig.</span><span class="sxs-lookup"><span data-stu-id="6d823-225">Problem: A provided URL is not valid.</span></span>

<span data-ttu-id="6d823-226">Oplossing: Controleer de opgegeven URL's.</span><span class="sxs-lookup"><span data-stu-id="6d823-226">Solution: Check all your provided URLs.</span></span> <span data-ttu-id="6d823-227">Zorg ervoor dat alle URL's oplossen toovalid locaties waartoe toegang op de externe computer Hallo Hallo-extensie heeft.</span><span class="sxs-lookup"><span data-stu-id="6d823-227">Make sure all URLs resolve toovalid locations that hello extension can access on hello remote machine.</span></span>

### <a name="invalid-configurationargument-type"></a><span data-ttu-id="6d823-228">Ongeldig Type voor ConfigurationArgument</span><span class="sxs-lookup"><span data-stu-id="6d823-228">Invalid ConfigurationArgument Type</span></span>
<span data-ttu-id="6d823-229">'Ongeldige configurationArguments type {0}'</span><span class="sxs-lookup"><span data-stu-id="6d823-229">"Invalid configurationArguments type {0}"</span></span>

<span data-ttu-id="6d823-230">Probleem: Hallo ConfigurationArguments-eigenschap kan tooa Hashtable-object niet omzetten.</span><span class="sxs-lookup"><span data-stu-id="6d823-230">Problem: hello ConfigurationArguments property cannot resolve tooa Hashtable object.</span></span> 

<span data-ttu-id="6d823-231">Oplossing: Controleer de eigenschap ConfigurationArguments een hashtabel.</span><span class="sxs-lookup"><span data-stu-id="6d823-231">Solution: Make your ConfigurationArguments property a Hashtable.</span></span> <span data-ttu-id="6d823-232">Ga als volgt in het voorgaande voorbeeld van Hallo Hallo-indeling.</span><span class="sxs-lookup"><span data-stu-id="6d823-232">Follow hello format provided in hello preceeding example.</span></span> <span data-ttu-id="6d823-233">Kijk uit voor aanhalingstekens, komma's en accolades.</span><span class="sxs-lookup"><span data-stu-id="6d823-233">Watch out for quotes, commas, and braces.</span></span>

### <a name="duplicate-configurationarguments"></a><span data-ttu-id="6d823-234">Dubbele ConfigurationArguments</span><span class="sxs-lookup"><span data-stu-id="6d823-234">Duplicate ConfigurationArguments</span></span>
<span data-ttu-id="6d823-235">'Dubbele argumenten {0} gevonden in de openbare en beveiligde configurationArguments'</span><span class="sxs-lookup"><span data-stu-id="6d823-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments"</span></span>

<span data-ttu-id="6d823-236">Probleem: Hallo ConfigurationArguments in instellingen voor openbare en hello ConfigurationArguments in de instellingen van beveiligde eigenschappen bevatten Hello dezelfde naam.</span><span class="sxs-lookup"><span data-stu-id="6d823-236">Problem: hello ConfigurationArguments in public settings and hello ConfigurationArguments in protected settings contain properties with hello same name.</span></span>

<span data-ttu-id="6d823-237">Oplossing: Een van de dubbele eigenschappen Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="6d823-237">Solution: Remove one of hello duplicate properties.</span></span>

### <a name="missing-properties"></a><span data-ttu-id="6d823-238">Ontbrekende eigenschappen</span><span class="sxs-lookup"><span data-stu-id="6d823-238">Missing Properties</span></span>
<span data-ttu-id="6d823-239">"Configuration.function moet configuration.url of configuration.module worden opgegeven."</span><span class="sxs-lookup"><span data-stu-id="6d823-239">"Configuration.function requires that configuration.url or configuration.module is specified"</span></span>

<span data-ttu-id="6d823-240">"Configuration.url vereist dat configuration.script is opgegeven."</span><span class="sxs-lookup"><span data-stu-id="6d823-240">"Configuration.url requires that configuration.script is specified"</span></span>

<span data-ttu-id="6d823-241">"Configuration.script vereist dat configuration.url is opgegeven."</span><span class="sxs-lookup"><span data-stu-id="6d823-241">"Configuration.script requires that configuration.url is specified"</span></span>

<span data-ttu-id="6d823-242">"Configuration.url vereist dat configuration.function is opgegeven."</span><span class="sxs-lookup"><span data-stu-id="6d823-242">"Configuration.url requires that configuration.function is specified"</span></span>

<span data-ttu-id="6d823-243">"ConfigurationUrlSasToken vereist dat configuration.url is opgegeven."</span><span class="sxs-lookup"><span data-stu-id="6d823-243">"ConfigurationUrlSasToken requires that configuration.url is specified"</span></span>

<span data-ttu-id="6d823-244">"ConfigurationDataUrlSasToken vereist dat configurationData.url is opgegeven."</span><span class="sxs-lookup"><span data-stu-id="6d823-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified"</span></span>

<span data-ttu-id="6d823-245">Probleem: Een gedefinieerde eigenschap moet een andere eigenschap die ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="6d823-245">Problem: A defined property needs another property that is missing.</span></span>

<span data-ttu-id="6d823-246">Oplossingen:</span><span class="sxs-lookup"><span data-stu-id="6d823-246">Solutions:</span></span> 

* <span data-ttu-id="6d823-247">Ontbrekende eigenschap Hallo bieden.</span><span class="sxs-lookup"><span data-stu-id="6d823-247">Provide hello missing property.</span></span>
* <span data-ttu-id="6d823-248">Hallo-eigenschap die Hallo ontbrekende eigenschap moet te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="6d823-248">Remove hello property that needs hello missing property.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d823-249">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6d823-249">Next Steps</span></span>
<span data-ttu-id="6d823-250">Meer informatie over DSC en virtuele-machineschaalsets [met behulp van virtuele Machine Scale ingesteld Hello Azure DSC-uitbreiding](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span><span class="sxs-lookup"><span data-stu-id="6d823-250">Learn about DSC and virtual machine scale sets in [Using Virtual Machine Scale Sets with hello Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span></span>

<span data-ttu-id="6d823-251">Meer informatie vinden op [van DSC beveiligde Referentiebeheer](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6d823-251">Find more details on [DSC's secure credential management](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="6d823-252">Zie voor meer informatie over hello Azure DSC-uitbreiding handler [inleiding toohello Azure Desired State Configuration extensie handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6d823-252">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="6d823-253">Voor meer informatie over PowerShell DSC [gaat u naar de PowerShell-documentatiecentrum hello](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="6d823-253">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

