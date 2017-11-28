---
title: Azure Diagnostics-extensie 1.3 en hoger configuratieschema | Microsoft Docs
description: Schemaversie 1.3 en hoger Azure diagnostics geleverd als onderdeel van de Microsoft Azure SDK 2.4 en hoger.
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: robb
ms.openlocfilehash: 0d814825fb08452238a254ccd30bde230380c74c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a><span data-ttu-id="0273c-103">Azure Diagnostics 1.3 en hoger configuratieschema</span><span class="sxs-lookup"><span data-stu-id="0273c-103">Azure Diagnostics 1.3 and later configuration schema</span></span>
> [!NOTE]
> <span data-ttu-id="0273c-104">De extensie Azure Diagnostics is het onderdeel dat wordt gebruikt voor het verzamelen van prestatiemeteritems en andere statistieken van:</span><span class="sxs-lookup"><span data-stu-id="0273c-104">The Azure Diagnostics extension is the component used to collect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="0273c-105">Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="0273c-105">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="0273c-106">Schaalsets voor virtuele machines</span><span class="sxs-lookup"><span data-stu-id="0273c-106">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="0273c-107">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0273c-107">Service Fabric</span></span> 
> - <span data-ttu-id="0273c-108">Cloudservices</span><span class="sxs-lookup"><span data-stu-id="0273c-108">Cloud Services</span></span> 
> - <span data-ttu-id="0273c-109">Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="0273c-109">Network Security Groups</span></span>
> 
> <span data-ttu-id="0273c-110">Deze pagina is alleen relevant als u een van deze services.</span><span class="sxs-lookup"><span data-stu-id="0273c-110">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="0273c-111">Deze pagina is ongeldig voor versies 1.3 en nieuwere (Azure SDK 2,4 en hoger).</span><span class="sxs-lookup"><span data-stu-id="0273c-111">This page is valid for versions 1.3 and newer (Azure SDK 2.4 and newer).</span></span> <span data-ttu-id="0273c-112">Nieuwere configuratiesecties zijn opgenomen als opmerkingen om weer te geven in welke versie ze zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="0273c-112">Newer configuration sections are commented to show in what version they were added.</span></span>  

<span data-ttu-id="0273c-113">Het configuratiebestand dat hier wordt beschreven, wordt gebruikt om diagnostische configuratie-instellingen wanneer de monitor diagnostics wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="0273c-113">The configuration file described here is used to set diagnostic configuration settings when the diagnostics monitor starts.</span></span>  

<span data-ttu-id="0273c-114">De uitbreiding wordt gebruikt in combinatie met andere Microsoft-producten voor diagnostische gegevens zoals Azure Monitor, Application Insights en Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="0273c-114">The extension is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>



<span data-ttu-id="0273c-115">De schemadefinitie van de openbare configuratie bestand downloaden door het uitvoeren van de volgende PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="0273c-115">Download the public configuration file schema definition by executing the following PowerShell command:</span></span>  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

<span data-ttu-id="0273c-116">Zie voor meer informatie over het gebruik van Azure Diagnostics [Azure-extensie voor diagnostische gegevens](azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="0273c-116">For more information about using Azure Diagnostics, see [Azure Diagnostics Extension](azure-diagnostics.md).</span></span>  

## <a name="example-of-the-diagnostics-configuration-file"></a><span data-ttu-id="0273c-117">Voorbeeld van het configuratiebestand van de diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="0273c-117">Example of the diagnostics configuration file</span></span>  
 <span data-ttu-id="0273c-118">Het volgende voorbeeld ziet u een configuratiebestand typische diagnostische gegevens:</span><span class="sxs-lookup"><span data-stu-id="0273c-118">The following example shows a typical diagnostics configuration file:</span></span>  

```xml  
<?xml version="1.0" encoding="utf-8"?>  
<DiagnosticsConfiguration  xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">   
  <PublicConfig>  
    <WadCfg>  
      <DiagnosticMonitorConfiguration overallQuotaInMB="10000">  

        <PerformanceCounters scheduledTransferPeriod="PT1M">  
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />  
        </PerformanceCounters>  

        <Directories scheduledTransferPeriod="PT5M">  
          <IISLogs containerName="iislogs" />  
          <FailedRequestLogs containerName="iisfailed" />  

          <DataSources>  
            <DirectoryConfiguration containerName="mynewprocess">  
              <Absolute path="C:\MyNewProcess" expandEnvironment="false" />  
            </DirectoryConfiguration>  
            <DirectoryConfiguration containerName="badapp">  
              <Absolute path="%SYSTEMDRIVE%\BadApp" expandEnvironment="true" />  
            </DirectoryConfiguration>  
            <DirectoryConfiguration containerName="goodapp">  
              <LocalResource name="Skippy" relativePath="..\PeanutButter"/>  
            </DirectoryConfiguration>  
          </DataSources>  

        </Directories>  

        <EtwProviders>  
          <EtwEventSourceProviderConfiguration   
                       provider="MyProviderClass"   
                       scheduledTransferPeriod="PT5M">  
            <Event id="0"/>  
            <Event id="1" eventDestination="errorTable"/>  
            <DefaultEvents />  
          </EtwEventSourceProviderConfiguration>  
          <EtwManifestProviderConfiguration provider="5974b00b-84c2-44bc-9e58-3a2451b4e3ad" scheduledTransferLogLevelFilter="Information" scheduledTransferPeriod="PT2M">  
            <Event id="0"/>  
            <DefaultEvents eventDestination="defaultTable"/>  
          </EtwManifestProviderConfiguration>  
        </EtwProviders>  

        <WindowsEventLog scheduledTransferPeriod="PT5M">  
          <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>  
          <DataSource name="System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]" />  
          <DataSource name="System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]" />  
        </WindowsEventLog>  

        <Logs  bufferQuotaInMB="1024"   
             scheduledTransferPeriod="PT1M"   
             scheduledTransferLogLevelFilter="Verbose"   
             sinks="ApplicationInsights.AppLogs"/>  <!-- sinks attribute added in 1.5 -->  

        <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
          <CrashDumpConfiguration processName="mynewprocess.exe" />  
          <CrashDumpConfiguration processName="badapp.exe"/>  
        </CrashDumps>  

        <DockerSources> <!-- Added in 1.9 --> 
          <Stats enabled="true" sampleRate="PT1M" scheduledTransferPeriod="PT1M" />
        </DockerSources>

      </DiagnosticMonitorConfiguration>  

      <SinksConfig>   <!-- Added in 1.5 -->  
        <Sink name="ApplicationInsights">   
          <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>   
          <Channels>   
            <Channel logLevel="Error" name="Errors"  />   
            <Channel logLevel="Verbose" name="AppLogs"  />   
          </Channels>   
        </Sink>   
        <Sink name="EventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryEventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryStorageAccount"> <!-- Added in 1.7 -->
          <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" />
        </Sink>
   </SinksConfig>

  </WadCfg>  

  <StorageAccount>diagstorageaccount</StorageAccount>
  <StorageType>TableAndBlob</StorageType> <!-- Added in 1.8 -->  
  </PublicConfig>  

  <PrivateConfig>  <!-- Added in 1.3 -->  
    <StorageAccount name="" key="" endpoint="" sasToken="{sas token}"  />  <!-- sasToken in Private config added in 1.8.1 -->  
    <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
   
    <SecondaryStorageAccounts>
       <StorageAccount name="secondarydiagstorageaccount" key="{base64 encoded key}" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
   
    <SecondaryEventHubs>
       <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
    </SecondaryEventHubs>

  </PrivateConfig>  
  <IsEnabled>true</IsEnabled>  
</DiagnosticsConfiguration>  

```  

<span data-ttu-id="0273c-119">JSON-equivalent van het vorige XML-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="0273c-119">JSON equivalent of the previous XML configuration file.</span></span> 

<span data-ttu-id="0273c-120">De PublicConfig en PrivateConfig worden gescheiden omdat in de meeste gevallen voor json-gebruik, de als verschillende variabelen worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="0273c-120">The PublicConfig and PrivateConfig are separated because in most json usage cases, they are passed as different variables.</span></span> <span data-ttu-id="0273c-121">Deze gevallen zijn onder andere Resource Manager-sjablonen, virtuele-machineschaalset PowerShell en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0273c-121">These cases include Resource Manager templates, Virtual Machine Scale set PowerShell, and Visual Studio.</span></span> 

```json
"PublicConfig" {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 10000,
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT1M",
                        "unit": "percent"
                    }
                ]
            },
            "Directories": {
                "scheduledTransferPeriod": "PT5M",
                "IISLogs": {
                    "containerName": "iislogs"
                },
                "FailedRequestLogs": {
                    "containerName": "iisfailed"
                },
                "DataSources": [
                    {
                        "containerName": "mynewprocess",
                        "Absolute": {
                            "path": "C:\\MyNewProcess",
                            "expandEnvironment": false
                        }
                    },
                    {
                        "containerName": "badapp",
                        "Absolute": {
                            "path": "%SYSTEMDRIVE%\\BadApp",
                            "expandEnvironment": true
                        }
                    },
                    {
                        "containerName": "goodapp",
                        "LocalResource": {
                            "relativePath": "..\\PeanutButter",
                            "name": "Skippy"
                        }
                    }
                ]
            },
            "EtwProviders": {
                "sinks": "",
                "EtwEventSourceProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT5M",
                        "provider": "MyProviderClass",
                        "Event": [
                            {
                                "id": 0
                            },
                            {
                                "id": 1,
                                "eventDestination": "errorTable"
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ],
                "EtwManifestProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT2M",
                        "scheduledTransferLogLevelFilter": "Information",
                        "provider": "5974b00b-84c2-44bc-9e58-3a2451b4e3ad",
                        "Event": [
                            {
                                "id": 0
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT5M",
                "DataSource": [
                    {
                        "name": "System!*[System[Provider[@Name='Microsoft Antimalware']]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Verbose",
                "sinks": "ApplicationInsights.AppLogs"
            },
            "CrashDumps": {
                "directoryQuotaPercentage": 30,
                "dumpType": "Mini",
                "containerName": "wad-crashdumps",
                "CrashDumpConfiguration": [
                    {
                        "processName": "mynewprocess.exe"
                    },
                    {
                        "processName": "badapp.exe"
                    }
                ]
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "ApplicationInsights",
                    "ApplicationInsights": "{Insert InstrumentationKey}",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "Errors"
                            },
                            {
                                "logLevel": "Verbose",
                                "name": "AppLogs"
                            }
                        ]
                    }
                },
                {
                    "name": "EventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryEventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryStorageAccount",
                    "StorageAccount": {
                        "name": "secondarydiagstorageaccount",
                        "endpoint": "https://core.windows.net"
                    }
                }
            ]
        }
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```json
"PrivateConfig" {
    "storageAccountName": "diagstorageaccount",
    "storageAccountKey": "{base64 encoded key}",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "EventHub": {
        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    },
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "key": "{base64 encoded key}",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    },
    "SecondaryEventHubs": {
        "EventHub": [
            {
                "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                "SharedAccessKeyName": "SendRule",
                "SharedAccessKey": "{base64 encoded key}"
            }
        ]
    }
}

```

## <a name="reading-this-page"></a><span data-ttu-id="0273c-122">Deze pagina lezen</span><span class="sxs-lookup"><span data-stu-id="0273c-122">Reading this page</span></span>  
 <span data-ttu-id="0273c-123">De volgende codes zijn ongeveer in volgorde weergegeven in het voorgaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="0273c-123">The tags following are roughly in order shown in the preceding example.</span></span>  <span data-ttu-id="0273c-124">Als u niet een volledige beschrijving waar u verwacht ziet, zoekt u de pagina voor het element of kenmerk.</span><span class="sxs-lookup"><span data-stu-id="0273c-124">If you don't see a full description where you expect it, search the page for the element or attribute.</span></span>  

## <a name="common-attribute-types"></a><span data-ttu-id="0273c-125">Algemene kenmerktypen</span><span class="sxs-lookup"><span data-stu-id="0273c-125">Common Attribute Types</span></span>  
 <span data-ttu-id="0273c-126">**scheduledTransferPeriod** kenmerk wordt weergegeven in verschillende elementen.</span><span class="sxs-lookup"><span data-stu-id="0273c-126">**scheduledTransferPeriod** attribute appears in several elements.</span></span> <span data-ttu-id="0273c-127">Het interval tussen de geplande overdrachten naar opslag afgerond naar het dichtstbijzijnde aantal minuten is.</span><span class="sxs-lookup"><span data-stu-id="0273c-127">It is the interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="0273c-128">De waarde is een [XML "Duur van het gegevenstype."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="0273c-128">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span>


## <a name="diagnosticsconfiguration-element"></a><span data-ttu-id="0273c-129">DiagnosticsConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="0273c-129">DiagnosticsConfiguration Element</span></span>  
 <span data-ttu-id="0273c-130">*Structuur: Root - DiagnosticsConfiguration*</span><span class="sxs-lookup"><span data-stu-id="0273c-130">*Tree: Root - DiagnosticsConfiguration*</span></span>

<span data-ttu-id="0273c-131">In versie 1.3 toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="0273c-131">Added in version 1.3.</span></span>  

<span data-ttu-id="0273c-132">Het element op het hoogste niveau van het configuratiebestand van de diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="0273c-132">The top-level element of the diagnostics configuration file.</span></span>  

<span data-ttu-id="0273c-133">**Kenmerk** xmlns - de XML-naamruimte voor de diagnostics-configuratiebestand is:</span><span class="sxs-lookup"><span data-stu-id="0273c-133">**Attribute**  xmlns - The XML namespace for the diagnostics configuration file is:</span></span>  
<span data-ttu-id="0273c-134">http://schemas.Microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="0273c-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span></span>  


|<span data-ttu-id="0273c-135">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="0273c-135">Child Elements</span></span>|<span data-ttu-id="0273c-136">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-136">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0273c-137">**PublicConfig**</span><span class="sxs-lookup"><span data-stu-id="0273c-137">**PublicConfig**</span></span>|<span data-ttu-id="0273c-138">Vereist.</span><span class="sxs-lookup"><span data-stu-id="0273c-138">Required.</span></span> <span data-ttu-id="0273c-139">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="0273c-139">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0273c-140">**PrivateConfig**</span><span class="sxs-lookup"><span data-stu-id="0273c-140">**PrivateConfig**</span></span>|<span data-ttu-id="0273c-141">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="0273c-141">Optional.</span></span> <span data-ttu-id="0273c-142">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="0273c-142">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0273c-143">**IsEnabled**</span><span class="sxs-lookup"><span data-stu-id="0273c-143">**IsEnabled**</span></span>|<span data-ttu-id="0273c-144">Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="0273c-144">Boolean.</span></span> <span data-ttu-id="0273c-145">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="0273c-145">See description elsewhere on this page.</span></span>|  

## <a name="publicconfig-element"></a><span data-ttu-id="0273c-146">PublicConfig Element</span><span class="sxs-lookup"><span data-stu-id="0273c-146">PublicConfig Element</span></span>  
 <span data-ttu-id="0273c-147">*Structuur: Basis - DiagnosticsConfiguration - PublicConfig*</span><span class="sxs-lookup"><span data-stu-id="0273c-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span></span>

 <span data-ttu-id="0273c-148">Beschrijft de configuratie van de openbare diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="0273c-148">Describes the public diagnostics configuration.</span></span>  

|<span data-ttu-id="0273c-149">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="0273c-149">Child Elements</span></span>|<span data-ttu-id="0273c-150">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-150">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0273c-151">**WadCfg**</span><span class="sxs-lookup"><span data-stu-id="0273c-151">**WadCfg**</span></span>|<span data-ttu-id="0273c-152">Vereist.</span><span class="sxs-lookup"><span data-stu-id="0273c-152">Required.</span></span> <span data-ttu-id="0273c-153">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="0273c-153">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0273c-154">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="0273c-154">**StorageAccount**</span></span>|<span data-ttu-id="0273c-155">De naam van de Azure Storage-account voor het opslaan van de gegevens in.</span><span class="sxs-lookup"><span data-stu-id="0273c-155">The name of the Azure Storage account to store the data in.</span></span> <span data-ttu-id="0273c-156">Kan ook worden opgegeven als parameter bij het uitvoeren van de cmdlet Set-AzureServiceDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="0273c-156">May also be specified as a parameter when executing the Set-AzureServiceDiagnosticsExtension cmdlet.</span></span>|  
|<span data-ttu-id="0273c-157">**StorageType**</span><span class="sxs-lookup"><span data-stu-id="0273c-157">**StorageType**</span></span>|<span data-ttu-id="0273c-158">Kan *tabel*, *Blob*, of *TableAndBlob*.</span><span class="sxs-lookup"><span data-stu-id="0273c-158">Can be *Table*, *Blob*, or *TableAndBlob*.</span></span> <span data-ttu-id="0273c-159">De tabel is standaard.</span><span class="sxs-lookup"><span data-stu-id="0273c-159">Table is default.</span></span> <span data-ttu-id="0273c-160">Wanneer TableAndBlob is gekozen, diagnostische gegevens worden geschreven tweemaal--eenmaal voor elk type.</span><span class="sxs-lookup"><span data-stu-id="0273c-160">When TableAndBlob is chosen, diagnostic data is written twice -- once to each type.</span></span>|  
|<span data-ttu-id="0273c-161">**LocalResourceDirectory**</span><span class="sxs-lookup"><span data-stu-id="0273c-161">**LocalResourceDirectory**</span></span>|<span data-ttu-id="0273c-162">De map op de virtuele machine waar de gebeurtenisgegevens worden opgeslagen in de Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="0273c-162">The directory on the virtual machine where the Monitoring Agent stores event data.</span></span> <span data-ttu-id="0273c-163">Als dat niet wordt is ingesteld, de standaardmap gebruikt:</span><span class="sxs-lookup"><span data-stu-id="0273c-163">If not, set, the default directory is used:</span></span><br /><br /> <span data-ttu-id="0273c-164">Voor een functie Worker/webservice:`C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span><span class="sxs-lookup"><span data-stu-id="0273c-164">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span></span><br /><br /> <span data-ttu-id="0273c-165">Voor een virtuele Machine:`C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span><span class="sxs-lookup"><span data-stu-id="0273c-165">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span></span><br /><br /> <span data-ttu-id="0273c-166">Vereiste kenmerken zijn:</span><span class="sxs-lookup"><span data-stu-id="0273c-166">Required attributes are:</span></span><br /><br /> <span data-ttu-id="0273c-167">- **pad** -de map op het systeem moet worden gebruikt door Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="0273c-167">- **path** - The directory on the system to be used by Azure Diagnostics.</span></span><br /><br /> <span data-ttu-id="0273c-168">- **expandEnvironment** -Hiermee wordt bepaald of omgevingsvariabelen in de padnaam worden uitgevouwen.</span><span class="sxs-lookup"><span data-stu-id="0273c-168">- **expandEnvironment** - Controls whether environment variables are expanded in the path name.</span></span>|  

## <a name="wadcfg-element"></a><span data-ttu-id="0273c-169">WadCFG Element</span><span class="sxs-lookup"><span data-stu-id="0273c-169">WadCFG Element</span></span>  
 <span data-ttu-id="0273c-170">*Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG-*</span><span class="sxs-lookup"><span data-stu-id="0273c-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span></span>
 
 <span data-ttu-id="0273c-171">Identificeert en configureert u de telemetriegegevens te verzamelen.</span><span class="sxs-lookup"><span data-stu-id="0273c-171">Identifies and configures the telemetry data to be collected.</span></span>  


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="0273c-172">DiagnosticMonitorConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="0273c-172">DiagnosticMonitorConfiguration Element</span></span> 
 <span data-ttu-id="0273c-173">*Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span><span class="sxs-lookup"><span data-stu-id="0273c-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span></span>

 <span data-ttu-id="0273c-174">Vereist</span><span class="sxs-lookup"><span data-stu-id="0273c-174">Required</span></span> 

|<span data-ttu-id="0273c-175">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="0273c-175">Attributes</span></span>|<span data-ttu-id="0273c-176">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-176">Description</span></span>|  
|----------------|-----------------|  
| <span data-ttu-id="0273c-177">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="0273c-177">**overallQuotaInMB**</span></span> | <span data-ttu-id="0273c-178">De maximale hoeveelheid ruimte op lokale schijf die kan worden gebruikt door de verschillende typen diagnostische gegevens verzameld door Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="0273c-178">The maximum amount of local disk space that may be consumed by the various types of diagnostic data collected by Azure Diagnostics.</span></span> <span data-ttu-id="0273c-179">De standaardinstelling is 5120 MB.</span><span class="sxs-lookup"><span data-stu-id="0273c-179">The default setting is 5120 MB.</span></span><br />
|<span data-ttu-id="0273c-180">**useProxyServer**</span><span class="sxs-lookup"><span data-stu-id="0273c-180">**useProxyServer**</span></span> | <span data-ttu-id="0273c-181">Azure Diagnostics voor het gebruik van de proxy-instellingen zoals in de instellingen van Internet Explorer configureren.</span><span class="sxs-lookup"><span data-stu-id="0273c-181">Configure Azure Diagnostics to use the proxy server settings as set in IE settings.</span></span>|  

<br /> <br />

|<span data-ttu-id="0273c-182">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="0273c-182">Child Elements</span></span>|<span data-ttu-id="0273c-183">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-183">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0273c-184">**CrashDumps**</span><span class="sxs-lookup"><span data-stu-id="0273c-184">**CrashDumps**</span></span>|<span data-ttu-id="0273c-185">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="0273c-185">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0273c-186">**DiagnosticInfrastructureLogs**</span><span class="sxs-lookup"><span data-stu-id="0273c-186">**DiagnosticInfrastructureLogs**</span></span>|<span data-ttu-id="0273c-187">Inschakelen van verzamelen van logboeken die worden gegenereerd door Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="0273c-187">Enable collection of logs generated by Azure Diagnostics.</span></span> <span data-ttu-id="0273c-188">De infrastructuur voor diagnostische logboeken zijn nuttig voor het oplossen van het systeem diagnostische gegevens zelf.</span><span class="sxs-lookup"><span data-stu-id="0273c-188">The diagnostic infrastructure logs are useful for troubleshooting the diagnostics system itself.</span></span> <span data-ttu-id="0273c-189">Optionele kenmerken zijn:</span><span class="sxs-lookup"><span data-stu-id="0273c-189">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="0273c-190">- **scheduledTransferLogLevelFilter** -configureert u de minimale ernst van de logboeken die worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="0273c-190">- **scheduledTransferLogLevelFilter** - Configures the minimum severity level of the logs collected.</span></span><br /><br /> <span data-ttu-id="0273c-191">- **scheduledTransferPeriod** -het interval tussen de geplande overdrachten naar opslag naar boven afgerond op de dichtstbijzijnde minuut.</span><span class="sxs-lookup"><span data-stu-id="0273c-191">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="0273c-192">De waarde is een [XML "Duur van het gegevenstype."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="0273c-192">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="0273c-193">**Mappen**</span><span class="sxs-lookup"><span data-stu-id="0273c-193">**Directories**</span></span>|<span data-ttu-id="0273c-194">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="0273c-194">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0273c-195">**EtwProviders**</span><span class="sxs-lookup"><span data-stu-id="0273c-195">**EtwProviders**</span></span>|<span data-ttu-id="0273c-196">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="0273c-196">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0273c-197">**Metrische gegevens**</span><span class="sxs-lookup"><span data-stu-id="0273c-197">**Metrics**</span></span>|<span data-ttu-id="0273c-198">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="0273c-198">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0273c-199">**PerformanceCounters**</span><span class="sxs-lookup"><span data-stu-id="0273c-199">**PerformanceCounters**</span></span>|<span data-ttu-id="0273c-200">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="0273c-200">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0273c-201">**WindowsEventLog**</span><span class="sxs-lookup"><span data-stu-id="0273c-201">**WindowsEventLog**</span></span>|<span data-ttu-id="0273c-202">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="0273c-202">See description elsewhere on this page.</span></span>| 
|<span data-ttu-id="0273c-203">**DockerSources**</span><span class="sxs-lookup"><span data-stu-id="0273c-203">**DockerSources**</span></span>|<span data-ttu-id="0273c-204">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="0273c-204">See description elsewhere on this page.</span></span> | 



## <a name="crashdumps-element"></a><span data-ttu-id="0273c-205">CrashDumps Element</span><span class="sxs-lookup"><span data-stu-id="0273c-205">CrashDumps Element</span></span>  
 <span data-ttu-id="0273c-206">*Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps-*</span><span class="sxs-lookup"><span data-stu-id="0273c-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span></span>
 
 <span data-ttu-id="0273c-207">Schakel het verzamelen van crashdumps.</span><span class="sxs-lookup"><span data-stu-id="0273c-207">Enable the collection of crash dumps.</span></span>  

|<span data-ttu-id="0273c-208">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="0273c-208">Attributes</span></span>|<span data-ttu-id="0273c-209">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-209">Description</span></span>|  
|----------------|-----------------|  
|<span data-ttu-id="0273c-210">**containerName**</span><span class="sxs-lookup"><span data-stu-id="0273c-210">**containerName**</span></span>|<span data-ttu-id="0273c-211">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="0273c-211">Optional.</span></span> <span data-ttu-id="0273c-212">De naam van de blob-container in uw Azure Storage-account moet worden gebruikt voor het opslaan van crashdumps.</span><span class="sxs-lookup"><span data-stu-id="0273c-212">The name of the blob container in your Azure Storage account to be used to store crash dumps.</span></span>|  
|<span data-ttu-id="0273c-213">**crashDumpType**</span><span class="sxs-lookup"><span data-stu-id="0273c-213">**crashDumpType**</span></span>|<span data-ttu-id="0273c-214">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="0273c-214">Optional.</span></span>  <span data-ttu-id="0273c-215">Hiermee configureert u Azure Diagnostics voor het verzamelen van dumpbestanden voor mini of volledige loopt vast.</span><span class="sxs-lookup"><span data-stu-id="0273c-215">Configures Azure Diagnostics to collect mini or full crash dumps.</span></span>|  
|<span data-ttu-id="0273c-216">**directoryQuotaPercentage**</span><span class="sxs-lookup"><span data-stu-id="0273c-216">**directoryQuotaPercentage**</span></span>|<span data-ttu-id="0273c-217">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="0273c-217">Optional.</span></span>  <span data-ttu-id="0273c-218">Hiermee configureert u het percentage **overallQuotaInMB** moet worden gereserveerd voor crashdumps op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0273c-218">Configures the percentage of **overallQuotaInMB** to be reserved for crash dumps on the VM.</span></span>|  

|<span data-ttu-id="0273c-219">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="0273c-219">Child Elements</span></span>|<span data-ttu-id="0273c-220">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-220">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0273c-221">**CrashDumpConfiguration**</span><span class="sxs-lookup"><span data-stu-id="0273c-221">**CrashDumpConfiguration**</span></span>|<span data-ttu-id="0273c-222">Vereist.</span><span class="sxs-lookup"><span data-stu-id="0273c-222">Required.</span></span> <span data-ttu-id="0273c-223">Hiermee definieert u configuratiewaarden voor elk proces.</span><span class="sxs-lookup"><span data-stu-id="0273c-223">Defines configuration values for each process.</span></span><br /><br /> <span data-ttu-id="0273c-224">Het volgende kenmerk is ook vereist:</span><span class="sxs-lookup"><span data-stu-id="0273c-224">The following attribute is also required:</span></span><br /><br /> <span data-ttu-id="0273c-225">**Procesnaam** -de naam van het proces wilt u diagnostische Azure-gegevens voor het verzamelen van een crashdump voor.</span><span class="sxs-lookup"><span data-stu-id="0273c-225">**processName** - The name of the process you want Azure Diagnostics to collect a crash dump for.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="0273c-226">Mappen Element</span><span class="sxs-lookup"><span data-stu-id="0273c-226">Directories Element</span></span> 
 <span data-ttu-id="0273c-227">*Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - mappen*</span><span class="sxs-lookup"><span data-stu-id="0273c-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span></span>

 <span data-ttu-id="0273c-228">Kan de verzameling van de inhoud van een map, logboeken van IIS is mislukt toegang aanvragen en/of IIS-logboeken.</span><span class="sxs-lookup"><span data-stu-id="0273c-228">Enables the collection of the contents of a directory, IIS failed access request logs and/or IIS logs.</span></span>  

 <span data-ttu-id="0273c-229">Optionele **scheduledTransferPeriod** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="0273c-229">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="0273c-230">Zie eerder uitleg.</span><span class="sxs-lookup"><span data-stu-id="0273c-230">See explanation earlier.</span></span>  

|<span data-ttu-id="0273c-231">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="0273c-231">Child Elements</span></span>|<span data-ttu-id="0273c-232">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-232">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0273c-233">**IISLogs**</span><span class="sxs-lookup"><span data-stu-id="0273c-233">**IISLogs**</span></span>|<span data-ttu-id="0273c-234">Met inbegrip van dit element in de configuratie, kunt de verzameling van IIS-logboeken:</span><span class="sxs-lookup"><span data-stu-id="0273c-234">Including this element in the configuration enables the collection of IIS logs:</span></span><br /><br /> <span data-ttu-id="0273c-235">**containerName** -de naam van de blob-container in uw Azure Storage-account moet worden gebruikt voor het opslaan van de IIS-logboeken.</span><span class="sxs-lookup"><span data-stu-id="0273c-235">**containerName** - The name of the blob container in your Azure Storage account to be used to store the IIS logs.</span></span>|   
|<span data-ttu-id="0273c-236">**FailedRequestLogs**</span><span class="sxs-lookup"><span data-stu-id="0273c-236">**FailedRequestLogs**</span></span>|<span data-ttu-id="0273c-237">Met inbegrip van dit element in de configuratie kunt verzamelen van logboeken over mislukte aanvragen voor een IIS-site of toepassing.</span><span class="sxs-lookup"><span data-stu-id="0273c-237">Including this element in the configuration enables collection of logs about failed requests to an IIS site or application.</span></span> <span data-ttu-id="0273c-238">U moet ook de traceringsopties onder inschakelen **system. WebServer** in **Web.config**.</span><span class="sxs-lookup"><span data-stu-id="0273c-238">You must also enable tracing options under **system.WebServer** in **Web.config**.</span></span>|  
|<span data-ttu-id="0273c-239">**Gegevensbronnen**</span><span class="sxs-lookup"><span data-stu-id="0273c-239">**DataSources**</span></span>|<span data-ttu-id="0273c-240">Een lijst met mappen om te controleren.</span><span class="sxs-lookup"><span data-stu-id="0273c-240">A list of directories to monitor.</span></span>| 




## <a name="datasources-element"></a><span data-ttu-id="0273c-241">Gegevensbronnen Element</span><span class="sxs-lookup"><span data-stu-id="0273c-241">DataSources Element</span></span>  
 <span data-ttu-id="0273c-242">*Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - mappen - gegevensbronnen*</span><span class="sxs-lookup"><span data-stu-id="0273c-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span></span>

 <span data-ttu-id="0273c-243">Een lijst met mappen om te controleren.</span><span class="sxs-lookup"><span data-stu-id="0273c-243">A list of directories to monitor.</span></span>  

|<span data-ttu-id="0273c-244">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="0273c-244">Child Elements</span></span>|<span data-ttu-id="0273c-245">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-245">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0273c-246">**DirectoryConfiguration**</span><span class="sxs-lookup"><span data-stu-id="0273c-246">**DirectoryConfiguration**</span></span>|<span data-ttu-id="0273c-247">Vereist.</span><span class="sxs-lookup"><span data-stu-id="0273c-247">Required.</span></span> <span data-ttu-id="0273c-248">Vereist kenmerk:</span><span class="sxs-lookup"><span data-stu-id="0273c-248">Required attribute:</span></span><br /><br /> <span data-ttu-id="0273c-249">**containerName** -de naam van de blob-container in uw Azure Storage-account dat moet worden gebruikt voor het opslaan van de logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="0273c-249">**containerName** - The name of the blob container in your Azure Storage account that to be used to store the log files.</span></span>|  





## <a name="directoryconfiguration-element"></a><span data-ttu-id="0273c-250">DirectoryConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="0273c-250">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="0273c-251">*Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - mappen - gegevensbronnen - DirectoryConfiguration-*</span><span class="sxs-lookup"><span data-stu-id="0273c-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span></span>

 <span data-ttu-id="0273c-252">Mogelijk bevat de **Absolute** of **LocalResource** element, maar niet beide.</span><span class="sxs-lookup"><span data-stu-id="0273c-252">May include either the **Absolute** or **LocalResource** element but not both.</span></span>  

|<span data-ttu-id="0273c-253">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="0273c-253">Child Elements</span></span>|<span data-ttu-id="0273c-254">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-254">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0273c-255">**Absolute**</span><span class="sxs-lookup"><span data-stu-id="0273c-255">**Absolute**</span></span>|<span data-ttu-id="0273c-256">Het absolute pad naar de map bewaken.</span><span class="sxs-lookup"><span data-stu-id="0273c-256">The absolute path to the directory to monitor.</span></span> <span data-ttu-id="0273c-257">De volgende kenmerken zijn vereist:</span><span class="sxs-lookup"><span data-stu-id="0273c-257">The following attributes are required:</span></span><br /><br /> <span data-ttu-id="0273c-258">- **Pad** -het absolute pad naar de map bewaken.</span><span class="sxs-lookup"><span data-stu-id="0273c-258">- **Path** - The absolute path to the directory to monitor.</span></span><br /><br /> <span data-ttu-id="0273c-259">- **expandEnvironment** -configureert u of omgevingsvariabelen in pad worden uitgevouwen.</span><span class="sxs-lookup"><span data-stu-id="0273c-259">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span></span>|  
|<span data-ttu-id="0273c-260">**LocalResource**</span><span class="sxs-lookup"><span data-stu-id="0273c-260">**LocalResource**</span></span>|<span data-ttu-id="0273c-261">Het pad ten opzichte van een lokale bron om te controleren.</span><span class="sxs-lookup"><span data-stu-id="0273c-261">The path relative to a local resource to monitor.</span></span> <span data-ttu-id="0273c-262">Vereiste kenmerken zijn:</span><span class="sxs-lookup"><span data-stu-id="0273c-262">Required attributes are:</span></span><br /><br /> <span data-ttu-id="0273c-263">- **Naam** -de lokale resource die de map voor het bewaken van bevat</span><span class="sxs-lookup"><span data-stu-id="0273c-263">- **Name** - The local resource that contains the directory to monitor</span></span><br /><br /> <span data-ttu-id="0273c-264">- **relativePath** -het pad ten opzichte van de naam die de map voor het bewaken van bevat</span><span class="sxs-lookup"><span data-stu-id="0273c-264">- **relativePath** - The path relative to Name that contains the directory to monitor</span></span>|  



## <a name="etwproviders-element"></a><span data-ttu-id="0273c-265">EtwProviders Element</span><span class="sxs-lookup"><span data-stu-id="0273c-265">EtwProviders Element</span></span>  
 <span data-ttu-id="0273c-266">*Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders-*</span><span class="sxs-lookup"><span data-stu-id="0273c-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span></span>

 <span data-ttu-id="0273c-267">Hiermee configureert u de verzameling van ETW-gebeurtenissen van EventSource en/of ETW Manifest op basis van providers.</span><span class="sxs-lookup"><span data-stu-id="0273c-267">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span></span>  

|<span data-ttu-id="0273c-268">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="0273c-268">Child Elements</span></span>|<span data-ttu-id="0273c-269">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-269">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0273c-270">**EtwEventSourceProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="0273c-270">**EtwEventSourceProviderConfiguration**</span></span>|<span data-ttu-id="0273c-271">Hiermee configureert u de verzameling van gebeurtenissen die worden gegenereerd op basis van [EventSource klasse](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="0273c-271">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span> <span data-ttu-id="0273c-272">Vereist kenmerk:</span><span class="sxs-lookup"><span data-stu-id="0273c-272">Required attribute:</span></span><br /><br /> <span data-ttu-id="0273c-273">**provider** -de naam van de klasse van de gebeurtenis EventSource.</span><span class="sxs-lookup"><span data-stu-id="0273c-273">**provider** - The class name of the EventSource event.</span></span><br /><br /> <span data-ttu-id="0273c-274">Optionele kenmerken zijn:</span><span class="sxs-lookup"><span data-stu-id="0273c-274">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="0273c-275">- **scheduledTransferLogLevelFilter** -de minimum ernst om over te dragen naar uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="0273c-275">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span></span><br /><br /> <span data-ttu-id="0273c-276">- **scheduledTransferPeriod** -het interval tussen de geplande overdrachten naar opslag naar boven afgerond op de dichtstbijzijnde minuut.</span><span class="sxs-lookup"><span data-stu-id="0273c-276">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="0273c-277">De waarde is een [XML "Duur van het gegevenstype."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="0273c-277">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="0273c-278">**EtwManifestProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="0273c-278">**EtwManifestProviderConfiguration**</span></span>|<span data-ttu-id="0273c-279">Vereist kenmerk:</span><span class="sxs-lookup"><span data-stu-id="0273c-279">Required attribute:</span></span><br /><br /> <span data-ttu-id="0273c-280">**provider** -de GUID van de gebeurtenisprovider</span><span class="sxs-lookup"><span data-stu-id="0273c-280">**provider** - The GUID of the event provider</span></span><br /><br /> <span data-ttu-id="0273c-281">Optionele kenmerken zijn:</span><span class="sxs-lookup"><span data-stu-id="0273c-281">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="0273c-282">- **scheduledTransferLogLevelFilter** -de minimum ernst om over te dragen naar uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="0273c-282">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span></span><br /><br /> <span data-ttu-id="0273c-283">- **scheduledTransferPeriod** -het interval tussen de geplande overdrachten naar opslag naar boven afgerond op de dichtstbijzijnde minuut.</span><span class="sxs-lookup"><span data-stu-id="0273c-283">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="0273c-284">De waarde is een [XML "Duur van het gegevenstype."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="0273c-284">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="etweventsourceproviderconfiguration-element"></a><span data-ttu-id="0273c-285">EtwEventSourceProviderConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="0273c-285">EtwEventSourceProviderConfiguration Element</span></span>  
 <span data-ttu-id="0273c-286">*Structuur: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwEventSourceProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="0273c-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span></span>

 <span data-ttu-id="0273c-287">Hiermee configureert u de verzameling van gebeurtenissen die worden gegenereerd op basis van [EventSource klasse](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="0273c-287">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span>  

|<span data-ttu-id="0273c-288">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="0273c-288">Child Elements</span></span>|<span data-ttu-id="0273c-289">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-289">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0273c-290">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="0273c-290">**DefaultEvents**</span></span>|<span data-ttu-id="0273c-291">Het optionele kenmerk:</span><span class="sxs-lookup"><span data-stu-id="0273c-291">Optional attribute:</span></span><br/><br/> <span data-ttu-id="0273c-292">**eventDestination** -de naam van de tabel voor het opslaan van de gebeurtenissen in</span><span class="sxs-lookup"><span data-stu-id="0273c-292">**eventDestination** - The name of the table to store the events in</span></span>|  
|<span data-ttu-id="0273c-293">**Gebeurtenis**</span><span class="sxs-lookup"><span data-stu-id="0273c-293">**Event**</span></span>|<span data-ttu-id="0273c-294">Vereist kenmerk:</span><span class="sxs-lookup"><span data-stu-id="0273c-294">Required attribute:</span></span><br /><br /> <span data-ttu-id="0273c-295">**id** -de id van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="0273c-295">**id** - The id of the event.</span></span><br /><br /> <span data-ttu-id="0273c-296">Het optionele kenmerk:</span><span class="sxs-lookup"><span data-stu-id="0273c-296">Optional attribute:</span></span><br /><br /> <span data-ttu-id="0273c-297">**eventDestination** -de naam van de tabel voor het opslaan van de gebeurtenissen in</span><span class="sxs-lookup"><span data-stu-id="0273c-297">**eventDestination** - The name of the table to store the events in</span></span>|  



## <a name="etwmanifestproviderconfiguration-element"></a><span data-ttu-id="0273c-298">EtwManifestProviderConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="0273c-298">EtwManifestProviderConfiguration Element</span></span>  
 <span data-ttu-id="0273c-299">*Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="0273c-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span></span>

|<span data-ttu-id="0273c-300">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="0273c-300">Child Elements</span></span>|<span data-ttu-id="0273c-301">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-301">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0273c-302">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="0273c-302">**DefaultEvents**</span></span>|<span data-ttu-id="0273c-303">Het optionele kenmerk:</span><span class="sxs-lookup"><span data-stu-id="0273c-303">Optional attribute:</span></span><br /><br /> <span data-ttu-id="0273c-304">**eventDestination** -de naam van de tabel voor het opslaan van de gebeurtenissen in</span><span class="sxs-lookup"><span data-stu-id="0273c-304">**eventDestination** - The name of the table to store the events in</span></span>|  
|<span data-ttu-id="0273c-305">**Gebeurtenis**</span><span class="sxs-lookup"><span data-stu-id="0273c-305">**Event**</span></span>|<span data-ttu-id="0273c-306">Vereist kenmerk:</span><span class="sxs-lookup"><span data-stu-id="0273c-306">Required attribute:</span></span><br /><br /> <span data-ttu-id="0273c-307">**id** -de id van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="0273c-307">**id** - The id of the event.</span></span><br /><br /> <span data-ttu-id="0273c-308">Het optionele kenmerk:</span><span class="sxs-lookup"><span data-stu-id="0273c-308">Optional attribute:</span></span><br /><br /> <span data-ttu-id="0273c-309">**eventDestination** -de naam van de tabel voor het opslaan van de gebeurtenissen in</span><span class="sxs-lookup"><span data-stu-id="0273c-309">**eventDestination** - The name of the table to store the events in</span></span>|  



## <a name="metrics-element"></a><span data-ttu-id="0273c-310">Element van de metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="0273c-310">Metrics Element</span></span>  
 <span data-ttu-id="0273c-311">*Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - metrische gegevens*</span><span class="sxs-lookup"><span data-stu-id="0273c-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span></span>

 <span data-ttu-id="0273c-312">Hiermee kunt u voor het genereren van een tabel van prestaties teller die is geoptimaliseerd voor snelle query's.</span><span class="sxs-lookup"><span data-stu-id="0273c-312">Enables you to generate a performance counter table that is optimized for fast queries.</span></span> <span data-ttu-id="0273c-313">Elk prestatiemeteritem dat is gedefinieerd in de **PerformanceCounters** element is opgeslagen in de tabel metrische gegevens naast het prestatiemeteritem-tabel.</span><span class="sxs-lookup"><span data-stu-id="0273c-313">Each performance counter that is defined in the **PerformanceCounters** element is stored in the Metrics table in addition to the Performance Counter table.</span></span>  

 <span data-ttu-id="0273c-314">De **resourceId** kenmerk is vereist.</span><span class="sxs-lookup"><span data-stu-id="0273c-314">The **resourceId** attribute is required.</span></span>  <span data-ttu-id="0273c-315">De resource-ID van de virtuele Machine die u om Azure Diagnostics implementeert.</span><span class="sxs-lookup"><span data-stu-id="0273c-315">The resource ID of the Virtual Machine you are deploying Azure Diagnostics to.</span></span> <span data-ttu-id="0273c-316">Ophalen van de **resourceID** van de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0273c-316">Get the **resourceID** from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0273c-317">Selecteer **Bladeren** -> **resourcegroepen** -> **< naam\>**.</span><span class="sxs-lookup"><span data-stu-id="0273c-317">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span></span> <span data-ttu-id="0273c-318">Klik op de **eigenschappen** tegel en kopieer de waarde van de **ID** veld.</span><span class="sxs-lookup"><span data-stu-id="0273c-318">Click the **Properties** tile and copy the value from the **ID** field.</span></span>  

|<span data-ttu-id="0273c-319">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="0273c-319">Child Elements</span></span>|<span data-ttu-id="0273c-320">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-320">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0273c-321">**MetricAggregation**</span><span class="sxs-lookup"><span data-stu-id="0273c-321">**MetricAggregation**</span></span>|<span data-ttu-id="0273c-322">Vereist kenmerk:</span><span class="sxs-lookup"><span data-stu-id="0273c-322">Required attribute:</span></span><br /><br /> <span data-ttu-id="0273c-323">**scheduledTransferPeriod** -het interval tussen de geplande overdrachten naar opslag naar boven afgerond op de dichtstbijzijnde minuut.</span><span class="sxs-lookup"><span data-stu-id="0273c-323">**scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="0273c-324">De waarde is een [XML "Duur van het gegevenstype."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="0273c-324">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="performancecounters-element"></a><span data-ttu-id="0273c-325">PerformanceCounters Element</span><span class="sxs-lookup"><span data-stu-id="0273c-325">PerformanceCounters Element</span></span>  
 <span data-ttu-id="0273c-326">*Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters-*</span><span class="sxs-lookup"><span data-stu-id="0273c-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span></span>

 <span data-ttu-id="0273c-327">Hiermee kunt het verzamelen van prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="0273c-327">Enables the collection of performance counters.</span></span>  

 <span data-ttu-id="0273c-328">Het optionele kenmerk:</span><span class="sxs-lookup"><span data-stu-id="0273c-328">Optional attribute:</span></span>  

 <span data-ttu-id="0273c-329">Optionele **scheduledTransferPeriod** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="0273c-329">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="0273c-330">Zie eerder uitleg.</span><span class="sxs-lookup"><span data-stu-id="0273c-330">See explanation earlier.</span></span>

|<span data-ttu-id="0273c-331">Onderliggend Element</span><span class="sxs-lookup"><span data-stu-id="0273c-331">Child Element</span></span>|<span data-ttu-id="0273c-332">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-332">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="0273c-333">**PerformanceCounterConfiguration**</span><span class="sxs-lookup"><span data-stu-id="0273c-333">**PerformanceCounterConfiguration**</span></span>|<span data-ttu-id="0273c-334">De volgende kenmerken zijn vereist:</span><span class="sxs-lookup"><span data-stu-id="0273c-334">The following attributes are required:</span></span><br /><br /> <span data-ttu-id="0273c-335">- **counterSpecifier** -de naam van het prestatiemeteritem.</span><span class="sxs-lookup"><span data-stu-id="0273c-335">- **counterSpecifier** - The name of the performance counter.</span></span> <span data-ttu-id="0273c-336">Bijvoorbeeld `\Processor(_Total)\% Processor Time`.</span><span class="sxs-lookup"><span data-stu-id="0273c-336">For example, `\Processor(_Total)\% Processor Time`.</span></span> <span data-ttu-id="0273c-337">Als u een lijst met prestatiemeteritems op de host, voert u de opdracht `typeperf`.</span><span class="sxs-lookup"><span data-stu-id="0273c-337">To get a list of performance counters on your host, run the command `typeperf`.</span></span><br /><br /> <span data-ttu-id="0273c-338">- **sampleRate** -hoe vaak de teller moet actieve.</span><span class="sxs-lookup"><span data-stu-id="0273c-338">- **sampleRate** - How often the counter should be sampled.</span></span><br /><br /> <span data-ttu-id="0273c-339">Het optionele kenmerk:</span><span class="sxs-lookup"><span data-stu-id="0273c-339">Optional attribute:</span></span><br /><br /> <span data-ttu-id="0273c-340">**eenheid** -de eenheid van de teller.</span><span class="sxs-lookup"><span data-stu-id="0273c-340">**unit** - The unit of measure of the counter.</span></span>|  




## <a name="windowseventlog-element"></a><span data-ttu-id="0273c-341">WindowsEventLog Element</span><span class="sxs-lookup"><span data-stu-id="0273c-341">WindowsEventLog Element</span></span>
 <span data-ttu-id="0273c-342">*Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog-*</span><span class="sxs-lookup"><span data-stu-id="0273c-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span></span>
 
 <span data-ttu-id="0273c-343">Kan de verzameling van het Windows-gebeurtenislogboeken.</span><span class="sxs-lookup"><span data-stu-id="0273c-343">Enables the collection of Windows Event Logs.</span></span>  

 <span data-ttu-id="0273c-344">Optionele **scheduledTransferPeriod** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="0273c-344">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="0273c-345">Zie eerder uitleg.</span><span class="sxs-lookup"><span data-stu-id="0273c-345">See explanation  earlier.</span></span>  

|<span data-ttu-id="0273c-346">Onderliggend Element</span><span class="sxs-lookup"><span data-stu-id="0273c-346">Child Element</span></span>|<span data-ttu-id="0273c-347">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-347">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="0273c-348">**Gegevensbron**</span><span class="sxs-lookup"><span data-stu-id="0273c-348">**DataSource**</span></span>|<span data-ttu-id="0273c-349">De Windows-gebeurtenislogboeken te verzamelen.</span><span class="sxs-lookup"><span data-stu-id="0273c-349">The Windows Event logs to collect.</span></span> <span data-ttu-id="0273c-350">Vereist kenmerk:</span><span class="sxs-lookup"><span data-stu-id="0273c-350">Required attribute:</span></span><br /><br /> <span data-ttu-id="0273c-351">**naam** : de XPath-query met een beschrijving van de windows-gebeurtenissen te verzamelen.</span><span class="sxs-lookup"><span data-stu-id="0273c-351">**name** - The XPath query describing the windows events to be collected.</span></span> <span data-ttu-id="0273c-352">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0273c-352">For example:</span></span><br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> <span data-ttu-id="0273c-353">Geef voor het verzamelen van alle gebeurtenissen, ' * '</span><span class="sxs-lookup"><span data-stu-id="0273c-353">To collect all events, specify "*"</span></span>|  




## <a name="logs-element"></a><span data-ttu-id="0273c-354">Logboeken Element</span><span class="sxs-lookup"><span data-stu-id="0273c-354">Logs Element</span></span>  
 <span data-ttu-id="0273c-355">*Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logboeken*</span><span class="sxs-lookup"><span data-stu-id="0273c-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span></span>

 <span data-ttu-id="0273c-356">Aanwezig zijn op versie 1.0 en 1.1.</span><span class="sxs-lookup"><span data-stu-id="0273c-356">Present in version 1.0 and 1.1.</span></span> <span data-ttu-id="0273c-357">1.2 ontbreken.</span><span class="sxs-lookup"><span data-stu-id="0273c-357">Missing in 1.2.</span></span> <span data-ttu-id="0273c-358">Terug in 1.3 toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="0273c-358">Added back in 1.3.</span></span>  

 <span data-ttu-id="0273c-359">Definieert de configuratie van de buffer voor basic-Azure Logboeken.</span><span class="sxs-lookup"><span data-stu-id="0273c-359">Defines the buffer configuration for basic Azure logs.</span></span>  

|<span data-ttu-id="0273c-360">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="0273c-360">Attribute</span></span>|<span data-ttu-id="0273c-361">Type</span><span class="sxs-lookup"><span data-stu-id="0273c-361">Type</span></span>|<span data-ttu-id="0273c-362">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-362">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="0273c-363">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="0273c-363">**bufferQuotaInMB**</span></span>|<span data-ttu-id="0273c-364">**unsignedInt**</span><span class="sxs-lookup"><span data-stu-id="0273c-364">**unsignedInt**</span></span>|<span data-ttu-id="0273c-365">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="0273c-365">Optional.</span></span> <span data-ttu-id="0273c-366">Hiermee geeft u de maximale hoeveelheid opslagruimte op het bestand systeem die beschikbaar is voor de opgegeven gegevens.</span><span class="sxs-lookup"><span data-stu-id="0273c-366">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="0273c-367">De standaardwaarde is 0.</span><span class="sxs-lookup"><span data-stu-id="0273c-367">The default is 0.</span></span>|  
|<span data-ttu-id="0273c-368">**scheduledTransferLogLevelFilterr**</span><span class="sxs-lookup"><span data-stu-id="0273c-368">**scheduledTransferLogLevelFilterr**</span></span>|<span data-ttu-id="0273c-369">**tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="0273c-369">**string**</span></span>|<span data-ttu-id="0273c-370">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="0273c-370">Optional.</span></span> <span data-ttu-id="0273c-371">Hiermee geeft u het minimale ernstniveau van logboekvermeldingen die worden overgedragen.</span><span class="sxs-lookup"><span data-stu-id="0273c-371">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="0273c-372">De standaardwaarde is **Undefined**, die alle logboeken overdraagt.</span><span class="sxs-lookup"><span data-stu-id="0273c-372">The default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="0273c-373">Andere mogelijke waarden (in volgorde van meest naar minst informatie) zijn **uitgebreid**, **informatie**, **waarschuwing**, **fout**, en **Kritiek**.</span><span class="sxs-lookup"><span data-stu-id="0273c-373">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="0273c-374">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="0273c-374">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="0273c-375">**duur**</span><span class="sxs-lookup"><span data-stu-id="0273c-375">**duration**</span></span>|<span data-ttu-id="0273c-376">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="0273c-376">Optional.</span></span> <span data-ttu-id="0273c-377">Hiermee geeft u het interval tussen geplande de overdracht van gegevens, afgerond naar het dichtstbijzijnde aantal minuten.</span><span class="sxs-lookup"><span data-stu-id="0273c-377">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="0273c-378">De standaardwaarde is PT0S.</span><span class="sxs-lookup"><span data-stu-id="0273c-378">The default is PT0S.</span></span>|  
|<span data-ttu-id="0273c-379">**sinks** toegevoegd in 1.5</span><span class="sxs-lookup"><span data-stu-id="0273c-379">**sinks** Added in 1.5</span></span>|<span data-ttu-id="0273c-380">**tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="0273c-380">**string**</span></span>|<span data-ttu-id="0273c-381">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="0273c-381">Optional.</span></span> <span data-ttu-id="0273c-382">Verwijst naar een locatie sink ook diagnostische gegevens verzenden.</span><span class="sxs-lookup"><span data-stu-id="0273c-382">Points to a sink location to also send diagnostic data.</span></span> <span data-ttu-id="0273c-383">Bijvoorbeeld, Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0273c-383">For example, Application Insights.</span></span>|  

## <a name="dockersources"></a><span data-ttu-id="0273c-384">DockerSources</span><span class="sxs-lookup"><span data-stu-id="0273c-384">DockerSources</span></span>
 <span data-ttu-id="0273c-385">*Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources-*</span><span class="sxs-lookup"><span data-stu-id="0273c-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span></span>

 <span data-ttu-id="0273c-386">In 1,9 toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="0273c-386">Added in 1.9.</span></span>

|<span data-ttu-id="0273c-387">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="0273c-387">Element Name</span></span>|<span data-ttu-id="0273c-388">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-388">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="0273c-389">**Statistieken**</span><span class="sxs-lookup"><span data-stu-id="0273c-389">**Stats**</span></span>|<span data-ttu-id="0273c-390">Geeft het systeem voor het verzamelen van statistieken voor Docker-containers</span><span class="sxs-lookup"><span data-stu-id="0273c-390">Tells the system to collect stats for Docker containers</span></span>|  

## <a name="sinksconfig-element"></a><span data-ttu-id="0273c-391">SinksConfig Element</span><span class="sxs-lookup"><span data-stu-id="0273c-391">SinksConfig Element</span></span>  
 <span data-ttu-id="0273c-392">*Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span><span class="sxs-lookup"><span data-stu-id="0273c-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span></span>

 <span data-ttu-id="0273c-393">Een lijst met locaties voor het verzenden van diagnostische gegevens naar en de configuratie die is gekoppeld aan deze locaties.</span><span class="sxs-lookup"><span data-stu-id="0273c-393">A list of locations to send diagnostics data to and the configuration associated with those locations.</span></span>  

|<span data-ttu-id="0273c-394">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="0273c-394">Element Name</span></span>|<span data-ttu-id="0273c-395">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-395">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="0273c-396">**Sink**</span><span class="sxs-lookup"><span data-stu-id="0273c-396">**Sink**</span></span>|<span data-ttu-id="0273c-397">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="0273c-397">See description elsewhere on this page.</span></span>|  

## <a name="sink-element"></a><span data-ttu-id="0273c-398">Sink-Element</span><span class="sxs-lookup"><span data-stu-id="0273c-398">Sink Element</span></span>
 <span data-ttu-id="0273c-399">*Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink-*</span><span class="sxs-lookup"><span data-stu-id="0273c-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span></span>

 <span data-ttu-id="0273c-400">In versie 1.5 toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="0273c-400">Added in version 1.5.</span></span>  

 <span data-ttu-id="0273c-401">Locaties voor het verzenden van diagnostische gegevens naar definieert.</span><span class="sxs-lookup"><span data-stu-id="0273c-401">Defines locations to send diagnostic data to.</span></span> <span data-ttu-id="0273c-402">De Application Insights-service.</span><span class="sxs-lookup"><span data-stu-id="0273c-402">For example, the Application Insights service.</span></span>  

|<span data-ttu-id="0273c-403">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="0273c-403">Attribute</span></span>|<span data-ttu-id="0273c-404">Type</span><span class="sxs-lookup"><span data-stu-id="0273c-404">Type</span></span>|<span data-ttu-id="0273c-405">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-405">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="0273c-406">**naam**</span><span class="sxs-lookup"><span data-stu-id="0273c-406">**name**</span></span>|<span data-ttu-id="0273c-407">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0273c-407">string</span></span>|<span data-ttu-id="0273c-408">Een tekenreeks die de sinkname te identificeren.</span><span class="sxs-lookup"><span data-stu-id="0273c-408">A string identifying the sinkname.</span></span>|  

|<span data-ttu-id="0273c-409">Element</span><span class="sxs-lookup"><span data-stu-id="0273c-409">Element</span></span>|<span data-ttu-id="0273c-410">Type</span><span class="sxs-lookup"><span data-stu-id="0273c-410">Type</span></span>|<span data-ttu-id="0273c-411">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-411">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="0273c-412">**Application Insights**</span><span class="sxs-lookup"><span data-stu-id="0273c-412">**Application Insights**</span></span>|<span data-ttu-id="0273c-413">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0273c-413">string</span></span>|<span data-ttu-id="0273c-414">Alleen gebruikt wanneer het verzenden van gegevens naar Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0273c-414">Used only when sending data to Application Insights.</span></span> <span data-ttu-id="0273c-415">De Instrumentatiesleutel voor een actieve Application Insights-account dat u toegang tot hebt bevatten.</span><span class="sxs-lookup"><span data-stu-id="0273c-415">Contain the Instrumentation Key for an active Application Insights account that you have access to.</span></span>|  
|<span data-ttu-id="0273c-416">**Kanalen**</span><span class="sxs-lookup"><span data-stu-id="0273c-416">**Channels**</span></span>|<span data-ttu-id="0273c-417">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0273c-417">string</span></span>|<span data-ttu-id="0273c-418">Één voor elke extra filteren die u stream</span><span class="sxs-lookup"><span data-stu-id="0273c-418">One for each additional filtering that stream that you</span></span>|  

## <a name="channels-element"></a><span data-ttu-id="0273c-419">Kanalen Element</span><span class="sxs-lookup"><span data-stu-id="0273c-419">Channels Element</span></span>  
 <span data-ttu-id="0273c-420">*Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - kanalen*</span><span class="sxs-lookup"><span data-stu-id="0273c-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span></span>

 <span data-ttu-id="0273c-421">In versie 1.5 toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="0273c-421">Added in version 1.5.</span></span>  

 <span data-ttu-id="0273c-422">Hiermee definieert u filters voor stromen van logboekgegevens een sink te doorlopen.</span><span class="sxs-lookup"><span data-stu-id="0273c-422">Defines filters for streams of log data passing through a sink.</span></span>  

|<span data-ttu-id="0273c-423">Element</span><span class="sxs-lookup"><span data-stu-id="0273c-423">Element</span></span>|<span data-ttu-id="0273c-424">Type</span><span class="sxs-lookup"><span data-stu-id="0273c-424">Type</span></span>|<span data-ttu-id="0273c-425">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-425">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="0273c-426">**Kanaal**</span><span class="sxs-lookup"><span data-stu-id="0273c-426">**Channel**</span></span>|<span data-ttu-id="0273c-427">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0273c-427">string</span></span>|<span data-ttu-id="0273c-428">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="0273c-428">See description elsewhere on this page.</span></span>|  

## <a name="channel-element"></a><span data-ttu-id="0273c-429">Kanaal-Element</span><span class="sxs-lookup"><span data-stu-id="0273c-429">Channel Element</span></span>
 <span data-ttu-id="0273c-430">*Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - kanalen - kanaal*</span><span class="sxs-lookup"><span data-stu-id="0273c-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span></span>

 <span data-ttu-id="0273c-431">In versie 1.5 toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="0273c-431">Added in version 1.5.</span></span>  

 <span data-ttu-id="0273c-432">Locaties voor het verzenden van diagnostische gegevens naar definieert.</span><span class="sxs-lookup"><span data-stu-id="0273c-432">Defines locations to send diagnostic data to.</span></span> <span data-ttu-id="0273c-433">De Application Insights-service.</span><span class="sxs-lookup"><span data-stu-id="0273c-433">For example, the Application Insights service.</span></span>  

|<span data-ttu-id="0273c-434">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="0273c-434">Attributes</span></span>|<span data-ttu-id="0273c-435">Type</span><span class="sxs-lookup"><span data-stu-id="0273c-435">Type</span></span>|<span data-ttu-id="0273c-436">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-436">Description</span></span>|  
|----------------|----------|-----------------|  
|<span data-ttu-id="0273c-437">**logLevel**</span><span class="sxs-lookup"><span data-stu-id="0273c-437">**logLevel**</span></span>|<span data-ttu-id="0273c-438">**tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="0273c-438">**string**</span></span>|<span data-ttu-id="0273c-439">Hiermee geeft u het minimale ernstniveau van logboekvermeldingen die worden overgedragen.</span><span class="sxs-lookup"><span data-stu-id="0273c-439">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="0273c-440">De standaardwaarde is **Undefined**, die alle logboeken overdraagt.</span><span class="sxs-lookup"><span data-stu-id="0273c-440">The default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="0273c-441">Andere mogelijke waarden (in volgorde van meest naar minst informatie) zijn **uitgebreid**, **informatie**, **waarschuwing**, **fout**, en **Kritiek**.</span><span class="sxs-lookup"><span data-stu-id="0273c-441">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="0273c-442">**naam**</span><span class="sxs-lookup"><span data-stu-id="0273c-442">**name**</span></span>|<span data-ttu-id="0273c-443">**tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="0273c-443">**string**</span></span>|<span data-ttu-id="0273c-444">Een unieke naam van het kanaal om te verwijzen naar</span><span class="sxs-lookup"><span data-stu-id="0273c-444">A unique name of the channel to refer to</span></span>|  


## <a name="privateconfig-element"></a><span data-ttu-id="0273c-445">PrivateConfig Element</span><span class="sxs-lookup"><span data-stu-id="0273c-445">PrivateConfig Element</span></span> 
 <span data-ttu-id="0273c-446">*Structuur: Basis - DiagnosticsConfiguration - PrivateConfig*</span><span class="sxs-lookup"><span data-stu-id="0273c-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span></span>

 <span data-ttu-id="0273c-447">In versie 1.3 toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="0273c-447">Added in version 1.3.</span></span>  

 <span data-ttu-id="0273c-448">Optioneel</span><span class="sxs-lookup"><span data-stu-id="0273c-448">Optional</span></span>  

 <span data-ttu-id="0273c-449">Slaat de persoonlijke gegevens van het opslagaccount (naam, sleutel en -eindpunt).</span><span class="sxs-lookup"><span data-stu-id="0273c-449">Stores the private details of the storage account (name, key, and endpoint).</span></span> <span data-ttu-id="0273c-450">Deze informatie wordt verzonden naar de virtuele machine, maar kan niet worden opgehaald uit.</span><span class="sxs-lookup"><span data-stu-id="0273c-450">This information is sent to the virtual machine, but cannot be retrieved from it.</span></span>  

|<span data-ttu-id="0273c-451">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="0273c-451">Child Elements</span></span>|<span data-ttu-id="0273c-452">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0273c-452">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0273c-453">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="0273c-453">**StorageAccount**</span></span>|<span data-ttu-id="0273c-454">Het storage-account te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0273c-454">The storage account to use.</span></span> <span data-ttu-id="0273c-455">De volgende kenmerken zijn vereist</span><span class="sxs-lookup"><span data-stu-id="0273c-455">The following attributes are required</span></span><br /><br /> <span data-ttu-id="0273c-456">- **naam** -de naam van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="0273c-456">- **name** - The name of the storage account.</span></span><br /><br /> <span data-ttu-id="0273c-457">- **sleutel** -de sleutel tot het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="0273c-457">- **key** - The key to the storage account.</span></span><br /><br /> <span data-ttu-id="0273c-458">- **eindpunt** -het eindpunt voor toegang tot het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="0273c-458">- **endpoint** - The endpoint to access the storage account.</span></span> <br /><br /> <span data-ttu-id="0273c-459">-**sasToken** (toegevoegd 1.8.1)-kunt u een SAS-token in plaats van de sleutel van een opslagaccount in de persoonlijke configuratie.</span><span class="sxs-lookup"><span data-stu-id="0273c-459">-**sasToken** (added 1.8.1)- You can specify an SAS token instead of a storage account key in the private config.</span></span> <span data-ttu-id="0273c-460">Indien opgegeven, wordt de sleutel van het opslagaccount wordt genegeerd.</span><span class="sxs-lookup"><span data-stu-id="0273c-460">If provided, the storage account key is ignored.</span></span> <br /><span data-ttu-id="0273c-461">Vereisten voor de SAS-Token:</span><span class="sxs-lookup"><span data-stu-id="0273c-461">Requirements for the SAS Token:</span></span> <br /><span data-ttu-id="0273c-462">-Ondersteunt alleen account SAS-token</span><span class="sxs-lookup"><span data-stu-id="0273c-462">- Supports account SAS token only</span></span> <br /><span data-ttu-id="0273c-463">- *b*, *t* servicetypen zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="0273c-463">- *b*, *t* service types are required.</span></span> <br /> <span data-ttu-id="0273c-464">- *een*, *c*, *u*, *w* machtigingen zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="0273c-464">- *a*, *c*, *u*, *w* permissions are required.</span></span> <br /> <span data-ttu-id="0273c-465">- *c*, *o* brontypen die zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="0273c-465">- *c*, *o* resource types are required.</span></span> <br /> <span data-ttu-id="0273c-466">-Ondersteunt alleen het HTTPS-protocol</span><span class="sxs-lookup"><span data-stu-id="0273c-466">- Supports the HTTPS protocol only</span></span> <br /> <span data-ttu-id="0273c-467">-Starten en het verlooptijdstip moet geldig zijn.</span><span class="sxs-lookup"><span data-stu-id="0273c-467">- Start and expiry time must be valid.</span></span>|  


## <a name="isenabled-element"></a><span data-ttu-id="0273c-468">IsEnabled Element</span><span class="sxs-lookup"><span data-stu-id="0273c-468">IsEnabled Element</span></span>  
 <span data-ttu-id="0273c-469">*Structuur: Basis - DiagnosticsConfiguration - IsEnabled*</span><span class="sxs-lookup"><span data-stu-id="0273c-469">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span></span>

 <span data-ttu-id="0273c-470">Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="0273c-470">Boolean.</span></span> <span data-ttu-id="0273c-471">Gebruik `true` de diagnostische gegevens inschakelen of `false` uitschakelen van de diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="0273c-471">Use `true` to enable the diagnostics or `false` to disable the diagnostics.</span></span>
