---
title: aaaAzure Diagnostics 1.3 en hoger configuratieschema uitbreiding | Microsoft Docs
description: Schemaversie 1.3 en hoger Azure diagnostische gegevens verzonden als onderdeel van Hallo Microsoft Azure SDK 2,4 en hoger.
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
ms.openlocfilehash: bd15d3a79ea818fcb3235854717e58d5da36518e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a><span data-ttu-id="66172-103">Azure Diagnostics 1.3 en hoger configuratieschema</span><span class="sxs-lookup"><span data-stu-id="66172-103">Azure Diagnostics 1.3 and later configuration schema</span></span>
> [!NOTE]
> <span data-ttu-id="66172-104">Hello Azure Diagnostics-extensie is Hallo onderdeel gebruikt toocollect prestatiemeteritems en andere statistieken van:</span><span class="sxs-lookup"><span data-stu-id="66172-104">hello Azure Diagnostics extension is hello component used toocollect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="66172-105">Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="66172-105">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="66172-106">Schaalsets voor virtuele machines</span><span class="sxs-lookup"><span data-stu-id="66172-106">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="66172-107">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="66172-107">Service Fabric</span></span> 
> - <span data-ttu-id="66172-108">Cloudservices</span><span class="sxs-lookup"><span data-stu-id="66172-108">Cloud Services</span></span> 
> - <span data-ttu-id="66172-109">Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="66172-109">Network Security Groups</span></span>
> 
> <span data-ttu-id="66172-110">Deze pagina is alleen relevant als u een van deze services.</span><span class="sxs-lookup"><span data-stu-id="66172-110">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="66172-111">Deze pagina is ongeldig voor versies 1.3 en nieuwere (Azure SDK 2,4 en hoger).</span><span class="sxs-lookup"><span data-stu-id="66172-111">This page is valid for versions 1.3 and newer (Azure SDK 2.4 and newer).</span></span> <span data-ttu-id="66172-112">Nieuwere configuratiesecties zijn opmerkingen tooshow in welke versie ze zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="66172-112">Newer configuration sections are commented tooshow in what version they were added.</span></span>  

<span data-ttu-id="66172-113">Hallo-configuratiebestand hier beschreven is gebruikte tooset diagnostische configuratie-instellingen wanneer Hallo diagnostics wordt gestart bewaken.</span><span class="sxs-lookup"><span data-stu-id="66172-113">hello configuration file described here is used tooset diagnostic configuration settings when hello diagnostics monitor starts.</span></span>  

<span data-ttu-id="66172-114">Hallo-uitbreiding wordt gebruikt in combinatie met andere Microsoft-producten voor diagnostische gegevens zoals Azure Monitor, Application Insights en Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="66172-114">hello extension is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>



<span data-ttu-id="66172-115">Hallo openbare configuratie bestand schemadefinitie downloaden door het uitvoeren van Hallo volgende PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="66172-115">Download hello public configuration file schema definition by executing hello following PowerShell command:</span></span>  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

<span data-ttu-id="66172-116">Zie voor meer informatie over het gebruik van Azure Diagnostics [Azure-extensie voor diagnostische gegevens](azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="66172-116">For more information about using Azure Diagnostics, see [Azure Diagnostics Extension](azure-diagnostics.md).</span></span>  

## <a name="example-of-hello-diagnostics-configuration-file"></a><span data-ttu-id="66172-117">Voorbeeld van een configuratiebestand voor Hallo diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="66172-117">Example of hello diagnostics configuration file</span></span>  
 <span data-ttu-id="66172-118">Hallo volgende voorbeeld ziet u een configuratiebestand typische diagnostische gegevens:</span><span class="sxs-lookup"><span data-stu-id="66172-118">hello following example shows a typical diagnostics configuration file:</span></span>  

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

<span data-ttu-id="66172-119">JSON-equivalent van Hallo vorige XML-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="66172-119">JSON equivalent of hello previous XML configuration file.</span></span> 

<span data-ttu-id="66172-120">Hallo PublicConfig en PrivateConfig worden gescheiden omdat in de meeste gevallen voor json-gebruik, de als verschillende variabelen worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="66172-120">hello PublicConfig and PrivateConfig are separated because in most json usage cases, they are passed as different variables.</span></span> <span data-ttu-id="66172-121">Deze gevallen zijn onder andere Resource Manager-sjablonen, virtuele-machineschaalset PowerShell en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="66172-121">These cases include Resource Manager templates, Virtual Machine Scale set PowerShell, and Visual Studio.</span></span> 

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

## <a name="reading-this-page"></a><span data-ttu-id="66172-122">Deze pagina lezen</span><span class="sxs-lookup"><span data-stu-id="66172-122">Reading this page</span></span>  
 <span data-ttu-id="66172-123">Hallo zijn labels te volgen ongeveer in volgorde van Hallo voorgaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="66172-123">hello tags following are roughly in order shown in hello preceding example.</span></span>  <span data-ttu-id="66172-124">Als u niet een volledige beschrijving waar u verwacht ziet, zoekpagina Hallo voor Hallo element of kenmerk.</span><span class="sxs-lookup"><span data-stu-id="66172-124">If you don't see a full description where you expect it, search hello page for hello element or attribute.</span></span>  

## <a name="common-attribute-types"></a><span data-ttu-id="66172-125">Algemene kenmerktypen</span><span class="sxs-lookup"><span data-stu-id="66172-125">Common Attribute Types</span></span>  
 <span data-ttu-id="66172-126">**scheduledTransferPeriod** kenmerk wordt weergegeven in verschillende elementen.</span><span class="sxs-lookup"><span data-stu-id="66172-126">**scheduledTransferPeriod** attribute appears in several elements.</span></span> <span data-ttu-id="66172-127">Is het Hallo-interval tussen geplande overdrachten toostorage toohello dichtstbijzijnde minuut afgerond.</span><span class="sxs-lookup"><span data-stu-id="66172-127">It is hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="66172-128">Hallo-waarde is een [XML "Duur van het gegevenstype."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="66172-128">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span>


## <a name="diagnosticsconfiguration-element"></a><span data-ttu-id="66172-129">DiagnosticsConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="66172-129">DiagnosticsConfiguration Element</span></span>  
 <span data-ttu-id="66172-130">*Structuur: Root - DiagnosticsConfiguration*</span><span class="sxs-lookup"><span data-stu-id="66172-130">*Tree: Root - DiagnosticsConfiguration*</span></span>

<span data-ttu-id="66172-131">In versie 1.3 toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="66172-131">Added in version 1.3.</span></span>  

<span data-ttu-id="66172-132">op het hoogste niveau element Hallo van Hallo diagnostics-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="66172-132">hello top-level element of hello diagnostics configuration file.</span></span>  

<span data-ttu-id="66172-133">**Kenmerk** xmlns - Hallo XML-naamruimte voor Hallo diagnostics-configuratiebestand is:</span><span class="sxs-lookup"><span data-stu-id="66172-133">**Attribute**  xmlns - hello XML namespace for hello diagnostics configuration file is:</span></span>  
<span data-ttu-id="66172-134">http://schemas.Microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="66172-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span></span>  


|<span data-ttu-id="66172-135">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="66172-135">Child Elements</span></span>|<span data-ttu-id="66172-136">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-136">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="66172-137">**PublicConfig**</span><span class="sxs-lookup"><span data-stu-id="66172-137">**PublicConfig**</span></span>|<span data-ttu-id="66172-138">Vereist.</span><span class="sxs-lookup"><span data-stu-id="66172-138">Required.</span></span> <span data-ttu-id="66172-139">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="66172-139">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="66172-140">**PrivateConfig**</span><span class="sxs-lookup"><span data-stu-id="66172-140">**PrivateConfig**</span></span>|<span data-ttu-id="66172-141">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="66172-141">Optional.</span></span> <span data-ttu-id="66172-142">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="66172-142">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="66172-143">**IsEnabled**</span><span class="sxs-lookup"><span data-stu-id="66172-143">**IsEnabled**</span></span>|<span data-ttu-id="66172-144">Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="66172-144">Boolean.</span></span> <span data-ttu-id="66172-145">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="66172-145">See description elsewhere on this page.</span></span>|  

## <a name="publicconfig-element"></a><span data-ttu-id="66172-146">PublicConfig Element</span><span class="sxs-lookup"><span data-stu-id="66172-146">PublicConfig Element</span></span>  
 <span data-ttu-id="66172-147">*Structuur: Basis - DiagnosticsConfiguration - PublicConfig*</span><span class="sxs-lookup"><span data-stu-id="66172-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span></span>

 <span data-ttu-id="66172-148">Beschrijft de configuratie van de openbare diagnostische Hallo.</span><span class="sxs-lookup"><span data-stu-id="66172-148">Describes hello public diagnostics configuration.</span></span>  

|<span data-ttu-id="66172-149">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="66172-149">Child Elements</span></span>|<span data-ttu-id="66172-150">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-150">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="66172-151">**WadCfg**</span><span class="sxs-lookup"><span data-stu-id="66172-151">**WadCfg**</span></span>|<span data-ttu-id="66172-152">Vereist.</span><span class="sxs-lookup"><span data-stu-id="66172-152">Required.</span></span> <span data-ttu-id="66172-153">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="66172-153">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="66172-154">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="66172-154">**StorageAccount**</span></span>|<span data-ttu-id="66172-155">Hallo-naam van hello Azure Storage-account toostore Hallo gegevens in.</span><span class="sxs-lookup"><span data-stu-id="66172-155">hello name of hello Azure Storage account toostore hello data in.</span></span> <span data-ttu-id="66172-156">Kan ook worden opgegeven als parameter bij het uitvoeren van de cmdlet Set-AzureServiceDiagnosticsExtension Hallo.</span><span class="sxs-lookup"><span data-stu-id="66172-156">May also be specified as a parameter when executing hello Set-AzureServiceDiagnosticsExtension cmdlet.</span></span>|  
|<span data-ttu-id="66172-157">**StorageType**</span><span class="sxs-lookup"><span data-stu-id="66172-157">**StorageType**</span></span>|<span data-ttu-id="66172-158">Kan *tabel*, *Blob*, of *TableAndBlob*.</span><span class="sxs-lookup"><span data-stu-id="66172-158">Can be *Table*, *Blob*, or *TableAndBlob*.</span></span> <span data-ttu-id="66172-159">De tabel is standaard.</span><span class="sxs-lookup"><span data-stu-id="66172-159">Table is default.</span></span> <span data-ttu-id="66172-160">Wanneer TableAndBlob is gekozen, diagnostische gegevens worden geschreven tweemaal--eenmaal tooeach type.</span><span class="sxs-lookup"><span data-stu-id="66172-160">When TableAndBlob is chosen, diagnostic data is written twice -- once tooeach type.</span></span>|  
|<span data-ttu-id="66172-161">**LocalResourceDirectory**</span><span class="sxs-lookup"><span data-stu-id="66172-161">**LocalResourceDirectory**</span></span>|<span data-ttu-id="66172-162">Hallo-map op Hallo virtuele machine waar hello Monitoring Agent gebeurtenisgegevens opslaat.</span><span class="sxs-lookup"><span data-stu-id="66172-162">hello directory on hello virtual machine where hello Monitoring Agent stores event data.</span></span> <span data-ttu-id="66172-163">Als dat niet wordt is ingesteld, Hallo standaarddirectory gebruikt:</span><span class="sxs-lookup"><span data-stu-id="66172-163">If not, set, hello default directory is used:</span></span><br /><br /> <span data-ttu-id="66172-164">Voor een functie Worker/webservice:`C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span><span class="sxs-lookup"><span data-stu-id="66172-164">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span></span><br /><br /> <span data-ttu-id="66172-165">Voor een virtuele Machine:`C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span><span class="sxs-lookup"><span data-stu-id="66172-165">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span></span><br /><br /> <span data-ttu-id="66172-166">Vereiste kenmerken zijn:</span><span class="sxs-lookup"><span data-stu-id="66172-166">Required attributes are:</span></span><br /><br /> <span data-ttu-id="66172-167">- **pad** - hello directory op Hallo system toobe die wordt gebruikt door Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="66172-167">- **path** - hello directory on hello system toobe used by Azure Diagnostics.</span></span><br /><br /> <span data-ttu-id="66172-168">- **expandEnvironment** -Hiermee wordt bepaald of omgevingsvariabelen in de padnaam Hallo worden uitgevouwen.</span><span class="sxs-lookup"><span data-stu-id="66172-168">- **expandEnvironment** - Controls whether environment variables are expanded in hello path name.</span></span>|  

## <a name="wadcfg-element"></a><span data-ttu-id="66172-169">WadCFG Element</span><span class="sxs-lookup"><span data-stu-id="66172-169">WadCFG Element</span></span>  
 <span data-ttu-id="66172-170">*Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG-*</span><span class="sxs-lookup"><span data-stu-id="66172-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span></span>
 
 <span data-ttu-id="66172-171">Identificeert en configureert u Hallo telemetrie gegevens toobe verzameld.</span><span class="sxs-lookup"><span data-stu-id="66172-171">Identifies and configures hello telemetry data toobe collected.</span></span>  


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="66172-172">DiagnosticMonitorConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="66172-172">DiagnosticMonitorConfiguration Element</span></span> 
 <span data-ttu-id="66172-173">*Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span><span class="sxs-lookup"><span data-stu-id="66172-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span></span>

 <span data-ttu-id="66172-174">Vereist</span><span class="sxs-lookup"><span data-stu-id="66172-174">Required</span></span> 

|<span data-ttu-id="66172-175">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="66172-175">Attributes</span></span>|<span data-ttu-id="66172-176">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-176">Description</span></span>|  
|----------------|-----------------|  
| <span data-ttu-id="66172-177">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="66172-177">**overallQuotaInMB**</span></span> | <span data-ttu-id="66172-178">maximale hoeveelheid lokale schijfruimte die kan worden gebruikt door Hallo Hallo verschillende soorten diagnostische gegevens verzameld door Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="66172-178">hello maximum amount of local disk space that may be consumed by hello various types of diagnostic data collected by Azure Diagnostics.</span></span> <span data-ttu-id="66172-179">de standaardinstelling Hallo is 5120 MB.</span><span class="sxs-lookup"><span data-stu-id="66172-179">hello default setting is 5120 MB.</span></span><br />
|<span data-ttu-id="66172-180">**useProxyServer**</span><span class="sxs-lookup"><span data-stu-id="66172-180">**useProxyServer**</span></span> | <span data-ttu-id="66172-181">Azure Diagnostics toouse Hallo proxyserverinstellingen configureren zoals in de instellingen van Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="66172-181">Configure Azure Diagnostics toouse hello proxy server settings as set in IE settings.</span></span>|  

<br /> <br />

|<span data-ttu-id="66172-182">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="66172-182">Child Elements</span></span>|<span data-ttu-id="66172-183">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-183">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="66172-184">**CrashDumps**</span><span class="sxs-lookup"><span data-stu-id="66172-184">**CrashDumps**</span></span>|<span data-ttu-id="66172-185">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="66172-185">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="66172-186">**DiagnosticInfrastructureLogs**</span><span class="sxs-lookup"><span data-stu-id="66172-186">**DiagnosticInfrastructureLogs**</span></span>|<span data-ttu-id="66172-187">Inschakelen van verzamelen van logboeken die worden gegenereerd door Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="66172-187">Enable collection of logs generated by Azure Diagnostics.</span></span> <span data-ttu-id="66172-188">Hallo infrastructuur diagnostische logboeken zijn handig voor het oplossen van Hallo diagnostics systeem zelf.</span><span class="sxs-lookup"><span data-stu-id="66172-188">hello diagnostic infrastructure logs are useful for troubleshooting hello diagnostics system itself.</span></span> <span data-ttu-id="66172-189">Optionele kenmerken zijn:</span><span class="sxs-lookup"><span data-stu-id="66172-189">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="66172-190">- **scheduledTransferLogLevelFilter** -configureert Hallo minimale ernstniveau Hallo-logboeken die worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="66172-190">- **scheduledTransferLogLevelFilter** - Configures hello minimum severity level of hello logs collected.</span></span><br /><br /> <span data-ttu-id="66172-191">- **scheduledTransferPeriod** -hello-interval tussen geplande overdrachten toostorage toohello dichtstbijzijnde minuut afgerond.</span><span class="sxs-lookup"><span data-stu-id="66172-191">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="66172-192">Hallo-waarde is een [XML "Duur van het gegevenstype."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="66172-192">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="66172-193">**Mappen**</span><span class="sxs-lookup"><span data-stu-id="66172-193">**Directories**</span></span>|<span data-ttu-id="66172-194">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="66172-194">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="66172-195">**EtwProviders**</span><span class="sxs-lookup"><span data-stu-id="66172-195">**EtwProviders**</span></span>|<span data-ttu-id="66172-196">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="66172-196">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="66172-197">**Metrische gegevens**</span><span class="sxs-lookup"><span data-stu-id="66172-197">**Metrics**</span></span>|<span data-ttu-id="66172-198">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="66172-198">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="66172-199">**PerformanceCounters**</span><span class="sxs-lookup"><span data-stu-id="66172-199">**PerformanceCounters**</span></span>|<span data-ttu-id="66172-200">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="66172-200">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="66172-201">**WindowsEventLog**</span><span class="sxs-lookup"><span data-stu-id="66172-201">**WindowsEventLog**</span></span>|<span data-ttu-id="66172-202">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="66172-202">See description elsewhere on this page.</span></span>| 
|<span data-ttu-id="66172-203">**DockerSources**</span><span class="sxs-lookup"><span data-stu-id="66172-203">**DockerSources**</span></span>|<span data-ttu-id="66172-204">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="66172-204">See description elsewhere on this page.</span></span> | 



## <a name="crashdumps-element"></a><span data-ttu-id="66172-205">CrashDumps Element</span><span class="sxs-lookup"><span data-stu-id="66172-205">CrashDumps Element</span></span>  
 <span data-ttu-id="66172-206">*Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps-*</span><span class="sxs-lookup"><span data-stu-id="66172-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span></span>
 
 <span data-ttu-id="66172-207">Hallo-verzameling van crashdumps inschakelen.</span><span class="sxs-lookup"><span data-stu-id="66172-207">Enable hello collection of crash dumps.</span></span>  

|<span data-ttu-id="66172-208">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="66172-208">Attributes</span></span>|<span data-ttu-id="66172-209">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-209">Description</span></span>|  
|----------------|-----------------|  
|<span data-ttu-id="66172-210">**containerName**</span><span class="sxs-lookup"><span data-stu-id="66172-210">**containerName**</span></span>|<span data-ttu-id="66172-211">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="66172-211">Optional.</span></span> <span data-ttu-id="66172-212">Hallo-naam van de blob-container in uw Azure Storage-account toobe hello toostore crashdumps gebruikt.</span><span class="sxs-lookup"><span data-stu-id="66172-212">hello name of hello blob container in your Azure Storage account toobe used toostore crash dumps.</span></span>|  
|<span data-ttu-id="66172-213">**crashDumpType**</span><span class="sxs-lookup"><span data-stu-id="66172-213">**crashDumpType**</span></span>|<span data-ttu-id="66172-214">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="66172-214">Optional.</span></span>  <span data-ttu-id="66172-215">Azure Diagnostics toocollect mini of volledige crashdumps configureert.</span><span class="sxs-lookup"><span data-stu-id="66172-215">Configures Azure Diagnostics toocollect mini or full crash dumps.</span></span>|  
|<span data-ttu-id="66172-216">**directoryQuotaPercentage**</span><span class="sxs-lookup"><span data-stu-id="66172-216">**directoryQuotaPercentage**</span></span>|<span data-ttu-id="66172-217">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="66172-217">Optional.</span></span>  <span data-ttu-id="66172-218">Hiermee configureert u Hallo percentage **overallQuotaInMB** toobe gereserveerd voor crashdumps op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="66172-218">Configures hello percentage of **overallQuotaInMB** toobe reserved for crash dumps on hello VM.</span></span>|  

|<span data-ttu-id="66172-219">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="66172-219">Child Elements</span></span>|<span data-ttu-id="66172-220">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-220">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="66172-221">**CrashDumpConfiguration**</span><span class="sxs-lookup"><span data-stu-id="66172-221">**CrashDumpConfiguration**</span></span>|<span data-ttu-id="66172-222">Vereist.</span><span class="sxs-lookup"><span data-stu-id="66172-222">Required.</span></span> <span data-ttu-id="66172-223">Hiermee definieert u configuratiewaarden voor elk proces.</span><span class="sxs-lookup"><span data-stu-id="66172-223">Defines configuration values for each process.</span></span><br /><br /> <span data-ttu-id="66172-224">Hallo na kenmerk is ook vereist:</span><span class="sxs-lookup"><span data-stu-id="66172-224">hello following attribute is also required:</span></span><br /><br /> <span data-ttu-id="66172-225">**Procesnaam** - hello naam van het gewenste Azure Diagnostics toocollect een crashdump voor Hallo-proces.</span><span class="sxs-lookup"><span data-stu-id="66172-225">**processName** - hello name of hello process you want Azure Diagnostics toocollect a crash dump for.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="66172-226">Mappen Element</span><span class="sxs-lookup"><span data-stu-id="66172-226">Directories Element</span></span> 
 <span data-ttu-id="66172-227">*Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - mappen*</span><span class="sxs-lookup"><span data-stu-id="66172-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span></span>

 <span data-ttu-id="66172-228">Hiermee Hallo verzameling Hallo inhoud van een map, IIS kan de logboeken voor het aanvragen van toegang en/of de IIS-logboeken.</span><span class="sxs-lookup"><span data-stu-id="66172-228">Enables hello collection of hello contents of a directory, IIS failed access request logs and/or IIS logs.</span></span>  

 <span data-ttu-id="66172-229">Optionele **scheduledTransferPeriod** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="66172-229">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="66172-230">Zie eerder uitleg.</span><span class="sxs-lookup"><span data-stu-id="66172-230">See explanation earlier.</span></span>  

|<span data-ttu-id="66172-231">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="66172-231">Child Elements</span></span>|<span data-ttu-id="66172-232">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-232">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="66172-233">**IISLogs**</span><span class="sxs-lookup"><span data-stu-id="66172-233">**IISLogs**</span></span>|<span data-ttu-id="66172-234">Dit element in configuratie Hallo inclusief kunt Hallo-verzameling van IIS-logboeken:</span><span class="sxs-lookup"><span data-stu-id="66172-234">Including this element in hello configuration enables hello collection of IIS logs:</span></span><br /><br /> <span data-ttu-id="66172-235">**containerName** -Hallo-naam van blob-container in uw Azure Storage-account toobe hello toostore Hallo IIS-logboeken gebruikt.</span><span class="sxs-lookup"><span data-stu-id="66172-235">**containerName** - hello name of hello blob container in your Azure Storage account toobe used toostore hello IIS logs.</span></span>|   
|<span data-ttu-id="66172-236">**FailedRequestLogs**</span><span class="sxs-lookup"><span data-stu-id="66172-236">**FailedRequestLogs**</span></span>|<span data-ttu-id="66172-237">Dit element in configuratie Hallo inclusief kunt verzamelen van logboeken over mislukte aanvragen tooan ISS-site of toepassing.</span><span class="sxs-lookup"><span data-stu-id="66172-237">Including this element in hello configuration enables collection of logs about failed requests tooan IIS site or application.</span></span> <span data-ttu-id="66172-238">U moet ook de traceringsopties onder inschakelen **system. WebServer** in **Web.config**.</span><span class="sxs-lookup"><span data-stu-id="66172-238">You must also enable tracing options under **system.WebServer** in **Web.config**.</span></span>|  
|<span data-ttu-id="66172-239">**Gegevensbronnen**</span><span class="sxs-lookup"><span data-stu-id="66172-239">**DataSources**</span></span>|<span data-ttu-id="66172-240">Een lijst met mappen toomonitor.</span><span class="sxs-lookup"><span data-stu-id="66172-240">A list of directories toomonitor.</span></span>| 




## <a name="datasources-element"></a><span data-ttu-id="66172-241">Gegevensbronnen Element</span><span class="sxs-lookup"><span data-stu-id="66172-241">DataSources Element</span></span>  
 <span data-ttu-id="66172-242">*Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - mappen - gegevensbronnen*</span><span class="sxs-lookup"><span data-stu-id="66172-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span></span>

 <span data-ttu-id="66172-243">Een lijst met mappen toomonitor.</span><span class="sxs-lookup"><span data-stu-id="66172-243">A list of directories toomonitor.</span></span>  

|<span data-ttu-id="66172-244">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="66172-244">Child Elements</span></span>|<span data-ttu-id="66172-245">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-245">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="66172-246">**DirectoryConfiguration**</span><span class="sxs-lookup"><span data-stu-id="66172-246">**DirectoryConfiguration**</span></span>|<span data-ttu-id="66172-247">Vereist.</span><span class="sxs-lookup"><span data-stu-id="66172-247">Required.</span></span> <span data-ttu-id="66172-248">Vereist kenmerk:</span><span class="sxs-lookup"><span data-stu-id="66172-248">Required attribute:</span></span><br /><br /> <span data-ttu-id="66172-249">**containerName** - hello naam van het Hallo blob-container in uw Azure Storage-account dat toobe toostore Hallo logboekbestanden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="66172-249">**containerName** - hello name of hello blob container in your Azure Storage account that toobe used toostore hello log files.</span></span>|  





## <a name="directoryconfiguration-element"></a><span data-ttu-id="66172-250">DirectoryConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="66172-250">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="66172-251">*Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - mappen - gegevensbronnen - DirectoryConfiguration-*</span><span class="sxs-lookup"><span data-stu-id="66172-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span></span>

 <span data-ttu-id="66172-252">Beide hello, omvat mogelijk **Absolute** of **LocalResource** element, maar niet beide.</span><span class="sxs-lookup"><span data-stu-id="66172-252">May include either hello **Absolute** or **LocalResource** element but not both.</span></span>  

|<span data-ttu-id="66172-253">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="66172-253">Child Elements</span></span>|<span data-ttu-id="66172-254">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-254">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="66172-255">**Absolute**</span><span class="sxs-lookup"><span data-stu-id="66172-255">**Absolute**</span></span>|<span data-ttu-id="66172-256">Hallo absoluut pad toohello directory toomonitor.</span><span class="sxs-lookup"><span data-stu-id="66172-256">hello absolute path toohello directory toomonitor.</span></span> <span data-ttu-id="66172-257">Hallo na kenmerken zijn vereist:</span><span class="sxs-lookup"><span data-stu-id="66172-257">hello following attributes are required:</span></span><br /><br /> <span data-ttu-id="66172-258">- **Pad** -Hallo absoluut pad toohello directory toomonitor.</span><span class="sxs-lookup"><span data-stu-id="66172-258">- **Path** - hello absolute path toohello directory toomonitor.</span></span><br /><br /> <span data-ttu-id="66172-259">- **expandEnvironment** -configureert u of omgevingsvariabelen in pad worden uitgevouwen.</span><span class="sxs-lookup"><span data-stu-id="66172-259">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span></span>|  
|<span data-ttu-id="66172-260">**LocalResource**</span><span class="sxs-lookup"><span data-stu-id="66172-260">**LocalResource**</span></span>|<span data-ttu-id="66172-261">Hallo pad relatief tooa lokale resource toomonitor.</span><span class="sxs-lookup"><span data-stu-id="66172-261">hello path relative tooa local resource toomonitor.</span></span> <span data-ttu-id="66172-262">Vereiste kenmerken zijn:</span><span class="sxs-lookup"><span data-stu-id="66172-262">Required attributes are:</span></span><br /><br /> <span data-ttu-id="66172-263">- **Naam** -Hallo lokale resource die Hallo directory toomonitor bevat</span><span class="sxs-lookup"><span data-stu-id="66172-263">- **Name** - hello local resource that contains hello directory toomonitor</span></span><br /><br /> <span data-ttu-id="66172-264">- **relativePath** -pad relatief tooName met Hallo directory toomonitor Hallo</span><span class="sxs-lookup"><span data-stu-id="66172-264">- **relativePath** - hello path relative tooName that contains hello directory toomonitor</span></span>|  



## <a name="etwproviders-element"></a><span data-ttu-id="66172-265">EtwProviders Element</span><span class="sxs-lookup"><span data-stu-id="66172-265">EtwProviders Element</span></span>  
 <span data-ttu-id="66172-266">*Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders-*</span><span class="sxs-lookup"><span data-stu-id="66172-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span></span>

 <span data-ttu-id="66172-267">Hiermee configureert u de verzameling van ETW-gebeurtenissen van EventSource en/of ETW Manifest op basis van providers.</span><span class="sxs-lookup"><span data-stu-id="66172-267">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span></span>  

|<span data-ttu-id="66172-268">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="66172-268">Child Elements</span></span>|<span data-ttu-id="66172-269">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-269">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="66172-270">**EtwEventSourceProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="66172-270">**EtwEventSourceProviderConfiguration**</span></span>|<span data-ttu-id="66172-271">Hiermee configureert u de verzameling van gebeurtenissen die worden gegenereerd op basis van [EventSource klasse](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="66172-271">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span> <span data-ttu-id="66172-272">Vereist kenmerk:</span><span class="sxs-lookup"><span data-stu-id="66172-272">Required attribute:</span></span><br /><br /> <span data-ttu-id="66172-273">**provider** -Hallo klassenaam van Hallo EventSource gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="66172-273">**provider** - hello class name of hello EventSource event.</span></span><br /><br /> <span data-ttu-id="66172-274">Optionele kenmerken zijn:</span><span class="sxs-lookup"><span data-stu-id="66172-274">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="66172-275">- **scheduledTransferLogLevelFilter** -Hallo minimale ernst niveau tootransfer tooyour storage-account.</span><span class="sxs-lookup"><span data-stu-id="66172-275">- **scheduledTransferLogLevelFilter** - hello minimum severity level tootransfer tooyour storage account.</span></span><br /><br /> <span data-ttu-id="66172-276">- **scheduledTransferPeriod** -hello-interval tussen geplande overdrachten toostorage toohello dichtstbijzijnde minuut afgerond.</span><span class="sxs-lookup"><span data-stu-id="66172-276">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="66172-277">Hallo-waarde is een [XML "Duur van het gegevenstype."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="66172-277">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="66172-278">**EtwManifestProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="66172-278">**EtwManifestProviderConfiguration**</span></span>|<span data-ttu-id="66172-279">Vereist kenmerk:</span><span class="sxs-lookup"><span data-stu-id="66172-279">Required attribute:</span></span><br /><br /> <span data-ttu-id="66172-280">**provider** -GUID van het Hallo-gebeurtenisprovider Hallo</span><span class="sxs-lookup"><span data-stu-id="66172-280">**provider** - hello GUID of hello event provider</span></span><br /><br /> <span data-ttu-id="66172-281">Optionele kenmerken zijn:</span><span class="sxs-lookup"><span data-stu-id="66172-281">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="66172-282">- **scheduledTransferLogLevelFilter** -Hallo minimale ernst niveau tootransfer tooyour storage-account.</span><span class="sxs-lookup"><span data-stu-id="66172-282">- **scheduledTransferLogLevelFilter** - hello minimum severity level tootransfer tooyour storage account.</span></span><br /><br /> <span data-ttu-id="66172-283">- **scheduledTransferPeriod** -hello-interval tussen geplande overdrachten toostorage toohello dichtstbijzijnde minuut afgerond.</span><span class="sxs-lookup"><span data-stu-id="66172-283">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="66172-284">Hallo-waarde is een [XML "Duur van het gegevenstype."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="66172-284">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="etweventsourceproviderconfiguration-element"></a><span data-ttu-id="66172-285">EtwEventSourceProviderConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="66172-285">EtwEventSourceProviderConfiguration Element</span></span>  
 <span data-ttu-id="66172-286">*Structuur: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwEventSourceProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="66172-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span></span>

 <span data-ttu-id="66172-287">Hiermee configureert u de verzameling van gebeurtenissen die worden gegenereerd op basis van [EventSource klasse](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="66172-287">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span>  

|<span data-ttu-id="66172-288">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="66172-288">Child Elements</span></span>|<span data-ttu-id="66172-289">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-289">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="66172-290">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="66172-290">**DefaultEvents**</span></span>|<span data-ttu-id="66172-291">Het optionele kenmerk:</span><span class="sxs-lookup"><span data-stu-id="66172-291">Optional attribute:</span></span><br/><br/> <span data-ttu-id="66172-292">**eventDestination** - hello naam van het Hallo tabel toostore Hallo gebeurtenissen in</span><span class="sxs-lookup"><span data-stu-id="66172-292">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  
|<span data-ttu-id="66172-293">**Gebeurtenis**</span><span class="sxs-lookup"><span data-stu-id="66172-293">**Event**</span></span>|<span data-ttu-id="66172-294">Vereist kenmerk:</span><span class="sxs-lookup"><span data-stu-id="66172-294">Required attribute:</span></span><br /><br /> <span data-ttu-id="66172-295">**id** -Hallo Hallo-gebeurtenis-id.</span><span class="sxs-lookup"><span data-stu-id="66172-295">**id** - hello id of hello event.</span></span><br /><br /> <span data-ttu-id="66172-296">Het optionele kenmerk:</span><span class="sxs-lookup"><span data-stu-id="66172-296">Optional attribute:</span></span><br /><br /> <span data-ttu-id="66172-297">**eventDestination** - hello naam van het Hallo tabel toostore Hallo gebeurtenissen in</span><span class="sxs-lookup"><span data-stu-id="66172-297">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  



## <a name="etwmanifestproviderconfiguration-element"></a><span data-ttu-id="66172-298">EtwManifestProviderConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="66172-298">EtwManifestProviderConfiguration Element</span></span>  
 <span data-ttu-id="66172-299">*Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="66172-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span></span>

|<span data-ttu-id="66172-300">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="66172-300">Child Elements</span></span>|<span data-ttu-id="66172-301">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-301">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="66172-302">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="66172-302">**DefaultEvents**</span></span>|<span data-ttu-id="66172-303">Het optionele kenmerk:</span><span class="sxs-lookup"><span data-stu-id="66172-303">Optional attribute:</span></span><br /><br /> <span data-ttu-id="66172-304">**eventDestination** - hello naam van het Hallo tabel toostore Hallo gebeurtenissen in</span><span class="sxs-lookup"><span data-stu-id="66172-304">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  
|<span data-ttu-id="66172-305">**Gebeurtenis**</span><span class="sxs-lookup"><span data-stu-id="66172-305">**Event**</span></span>|<span data-ttu-id="66172-306">Vereist kenmerk:</span><span class="sxs-lookup"><span data-stu-id="66172-306">Required attribute:</span></span><br /><br /> <span data-ttu-id="66172-307">**id** -Hallo Hallo-gebeurtenis-id.</span><span class="sxs-lookup"><span data-stu-id="66172-307">**id** - hello id of hello event.</span></span><br /><br /> <span data-ttu-id="66172-308">Het optionele kenmerk:</span><span class="sxs-lookup"><span data-stu-id="66172-308">Optional attribute:</span></span><br /><br /> <span data-ttu-id="66172-309">**eventDestination** - hello naam van het Hallo tabel toostore Hallo gebeurtenissen in</span><span class="sxs-lookup"><span data-stu-id="66172-309">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  



## <a name="metrics-element"></a><span data-ttu-id="66172-310">Element van de metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="66172-310">Metrics Element</span></span>  
 <span data-ttu-id="66172-311">*Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - metrische gegevens*</span><span class="sxs-lookup"><span data-stu-id="66172-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span></span>

 <span data-ttu-id="66172-312">Hiermee kunt u toogenerate een prestaties teller tabel die is geoptimaliseerd voor snelle query's.</span><span class="sxs-lookup"><span data-stu-id="66172-312">Enables you toogenerate a performance counter table that is optimized for fast queries.</span></span> <span data-ttu-id="66172-313">Elk prestatiemeteritem dat is gedefinieerd in Hallo **PerformanceCounters** element in Hallo metrische gegevens tabel in de toevoeging toohello prestatiemeteritem is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="66172-313">Each performance counter that is defined in hello **PerformanceCounters** element is stored in hello Metrics table in addition toohello Performance Counter table.</span></span>  

 <span data-ttu-id="66172-314">Hallo **resourceId** kenmerk is vereist.</span><span class="sxs-lookup"><span data-stu-id="66172-314">hello **resourceId** attribute is required.</span></span>  <span data-ttu-id="66172-315">Hallo resource-ID van de virtuele Machine die u om Azure Diagnostics implementeert Hallo.</span><span class="sxs-lookup"><span data-stu-id="66172-315">hello resource ID of hello Virtual Machine you are deploying Azure Diagnostics to.</span></span> <span data-ttu-id="66172-316">Hallo ophalen **resourceID** van Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="66172-316">Get hello **resourceID** from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="66172-317">Selecteer **Bladeren** -> **resourcegroepen** -> **< naam\>**.</span><span class="sxs-lookup"><span data-stu-id="66172-317">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span></span> <span data-ttu-id="66172-318">Klik op Hallo **eigenschappen** tegel en Hallo-waarde van de Hallo kopiëren **ID** veld.</span><span class="sxs-lookup"><span data-stu-id="66172-318">Click hello **Properties** tile and copy hello value from hello **ID** field.</span></span>  

|<span data-ttu-id="66172-319">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="66172-319">Child Elements</span></span>|<span data-ttu-id="66172-320">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-320">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="66172-321">**MetricAggregation**</span><span class="sxs-lookup"><span data-stu-id="66172-321">**MetricAggregation**</span></span>|<span data-ttu-id="66172-322">Vereist kenmerk:</span><span class="sxs-lookup"><span data-stu-id="66172-322">Required attribute:</span></span><br /><br /> <span data-ttu-id="66172-323">**scheduledTransferPeriod** -hello-interval tussen geplande overdrachten toostorage toohello dichtstbijzijnde minuut afgerond.</span><span class="sxs-lookup"><span data-stu-id="66172-323">**scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="66172-324">Hallo-waarde is een [XML "Duur van het gegevenstype."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="66172-324">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="performancecounters-element"></a><span data-ttu-id="66172-325">PerformanceCounters Element</span><span class="sxs-lookup"><span data-stu-id="66172-325">PerformanceCounters Element</span></span>  
 <span data-ttu-id="66172-326">*Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters-*</span><span class="sxs-lookup"><span data-stu-id="66172-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span></span>

 <span data-ttu-id="66172-327">Hiermee bepaalt u Hallo van prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="66172-327">Enables hello collection of performance counters.</span></span>  

 <span data-ttu-id="66172-328">Het optionele kenmerk:</span><span class="sxs-lookup"><span data-stu-id="66172-328">Optional attribute:</span></span>  

 <span data-ttu-id="66172-329">Optionele **scheduledTransferPeriod** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="66172-329">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="66172-330">Zie eerder uitleg.</span><span class="sxs-lookup"><span data-stu-id="66172-330">See explanation earlier.</span></span>

|<span data-ttu-id="66172-331">Onderliggend Element</span><span class="sxs-lookup"><span data-stu-id="66172-331">Child Element</span></span>|<span data-ttu-id="66172-332">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-332">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="66172-333">**PerformanceCounterConfiguration**</span><span class="sxs-lookup"><span data-stu-id="66172-333">**PerformanceCounterConfiguration**</span></span>|<span data-ttu-id="66172-334">Hallo na kenmerken zijn vereist:</span><span class="sxs-lookup"><span data-stu-id="66172-334">hello following attributes are required:</span></span><br /><br /> <span data-ttu-id="66172-335">- **counterSpecifier** - hello naam van het prestatiemeteritem Hallo.</span><span class="sxs-lookup"><span data-stu-id="66172-335">- **counterSpecifier** - hello name of hello performance counter.</span></span> <span data-ttu-id="66172-336">Bijvoorbeeld `\Processor(_Total)\% Processor Time`.</span><span class="sxs-lookup"><span data-stu-id="66172-336">For example, `\Processor(_Total)\% Processor Time`.</span></span> <span data-ttu-id="66172-337">tooget een lijst van de prestaties van prestatiemeteritems op uw host, voert u de opdracht Hallo `typeperf`.</span><span class="sxs-lookup"><span data-stu-id="66172-337">tooget a list of performance counters on your host, run hello command `typeperf`.</span></span><br /><br /> <span data-ttu-id="66172-338">- **sampleRate** -hoe vaak hello teller moet actieve.</span><span class="sxs-lookup"><span data-stu-id="66172-338">- **sampleRate** - How often hello counter should be sampled.</span></span><br /><br /> <span data-ttu-id="66172-339">Het optionele kenmerk:</span><span class="sxs-lookup"><span data-stu-id="66172-339">Optional attribute:</span></span><br /><br /> <span data-ttu-id="66172-340">**eenheid** -eenheid Hallo van Hallo teller.</span><span class="sxs-lookup"><span data-stu-id="66172-340">**unit** - hello unit of measure of hello counter.</span></span>|  




## <a name="windowseventlog-element"></a><span data-ttu-id="66172-341">WindowsEventLog Element</span><span class="sxs-lookup"><span data-stu-id="66172-341">WindowsEventLog Element</span></span>
 <span data-ttu-id="66172-342">*Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog-*</span><span class="sxs-lookup"><span data-stu-id="66172-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span></span>
 
 <span data-ttu-id="66172-343">Hallo-verzameling van het Windows-gebeurtenislogboeken kunt.</span><span class="sxs-lookup"><span data-stu-id="66172-343">Enables hello collection of Windows Event Logs.</span></span>  

 <span data-ttu-id="66172-344">Optionele **scheduledTransferPeriod** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="66172-344">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="66172-345">Zie eerder uitleg.</span><span class="sxs-lookup"><span data-stu-id="66172-345">See explanation  earlier.</span></span>  

|<span data-ttu-id="66172-346">Onderliggend Element</span><span class="sxs-lookup"><span data-stu-id="66172-346">Child Element</span></span>|<span data-ttu-id="66172-347">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-347">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="66172-348">**Gegevensbron**</span><span class="sxs-lookup"><span data-stu-id="66172-348">**DataSource**</span></span>|<span data-ttu-id="66172-349">Hallo Windows-gebeurtenislogboeken toocollect.</span><span class="sxs-lookup"><span data-stu-id="66172-349">hello Windows Event logs toocollect.</span></span> <span data-ttu-id="66172-350">Vereist kenmerk:</span><span class="sxs-lookup"><span data-stu-id="66172-350">Required attribute:</span></span><br /><br /> <span data-ttu-id="66172-351">**naam** -Hallo XPath-query met een beschrijving van Hallo windows gebeurtenissen toobe verzameld.</span><span class="sxs-lookup"><span data-stu-id="66172-351">**name** - hello XPath query describing hello windows events toobe collected.</span></span> <span data-ttu-id="66172-352">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="66172-352">For example:</span></span><br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> <span data-ttu-id="66172-353">toocollect alle gebeurtenissen opgeven ' * '</span><span class="sxs-lookup"><span data-stu-id="66172-353">toocollect all events, specify "*"</span></span>|  




## <a name="logs-element"></a><span data-ttu-id="66172-354">Logboeken Element</span><span class="sxs-lookup"><span data-stu-id="66172-354">Logs Element</span></span>  
 <span data-ttu-id="66172-355">*Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logboeken*</span><span class="sxs-lookup"><span data-stu-id="66172-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span></span>

 <span data-ttu-id="66172-356">Aanwezig zijn op versie 1.0 en 1.1.</span><span class="sxs-lookup"><span data-stu-id="66172-356">Present in version 1.0 and 1.1.</span></span> <span data-ttu-id="66172-357">1.2 ontbreken.</span><span class="sxs-lookup"><span data-stu-id="66172-357">Missing in 1.2.</span></span> <span data-ttu-id="66172-358">Terug in 1.3 toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="66172-358">Added back in 1.3.</span></span>  

 <span data-ttu-id="66172-359">Definieert Hallo buffer configuratie voor basic-Azure Logboeken.</span><span class="sxs-lookup"><span data-stu-id="66172-359">Defines hello buffer configuration for basic Azure logs.</span></span>  

|<span data-ttu-id="66172-360">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="66172-360">Attribute</span></span>|<span data-ttu-id="66172-361">Type</span><span class="sxs-lookup"><span data-stu-id="66172-361">Type</span></span>|<span data-ttu-id="66172-362">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-362">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="66172-363">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="66172-363">**bufferQuotaInMB**</span></span>|<span data-ttu-id="66172-364">**unsignedInt**</span><span class="sxs-lookup"><span data-stu-id="66172-364">**unsignedInt**</span></span>|<span data-ttu-id="66172-365">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="66172-365">Optional.</span></span> <span data-ttu-id="66172-366">Hallo maximum hoeveelheid system bestandsopslag die beschikbaar is voor Hallo opgegeven gegevens.</span><span class="sxs-lookup"><span data-stu-id="66172-366">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="66172-367">Hallo standaardwaarde is 0.</span><span class="sxs-lookup"><span data-stu-id="66172-367">hello default is 0.</span></span>|  
|<span data-ttu-id="66172-368">**scheduledTransferLogLevelFilterr**</span><span class="sxs-lookup"><span data-stu-id="66172-368">**scheduledTransferLogLevelFilterr**</span></span>|<span data-ttu-id="66172-369">**tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="66172-369">**string**</span></span>|<span data-ttu-id="66172-370">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="66172-370">Optional.</span></span> <span data-ttu-id="66172-371">Hiermee geeft u een minimale ernstniveau Hallo voor logboekvermeldingen die worden overgedragen.</span><span class="sxs-lookup"><span data-stu-id="66172-371">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="66172-372">de standaardwaarde Hallo is **Undefined**, die alle logboeken overdraagt.</span><span class="sxs-lookup"><span data-stu-id="66172-372">hello default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="66172-373">Andere mogelijke waarden (in volgorde van de meeste tooleast gegevens) zijn **uitgebreid**, **informatie**, **waarschuwing**, **fout**, en **Kritieke**.</span><span class="sxs-lookup"><span data-stu-id="66172-373">Other possible values (in order of most tooleast information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="66172-374">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="66172-374">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="66172-375">**duur**</span><span class="sxs-lookup"><span data-stu-id="66172-375">**duration**</span></span>|<span data-ttu-id="66172-376">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="66172-376">Optional.</span></span> <span data-ttu-id="66172-377">Hiermee geeft u hello-interval tussen de geplande overdrachten van gegevens, afgerond toohello dichtstbijzijnde minuut.</span><span class="sxs-lookup"><span data-stu-id="66172-377">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="66172-378">Hallo standaardwaarde is PT0S.</span><span class="sxs-lookup"><span data-stu-id="66172-378">hello default is PT0S.</span></span>|  
|<span data-ttu-id="66172-379">**sinks** toegevoegd in 1.5</span><span class="sxs-lookup"><span data-stu-id="66172-379">**sinks** Added in 1.5</span></span>|<span data-ttu-id="66172-380">**tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="66172-380">**string**</span></span>|<span data-ttu-id="66172-381">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="66172-381">Optional.</span></span> <span data-ttu-id="66172-382">Punten tooa sink locatie tooalso diagnostische gegevens verzenden.</span><span class="sxs-lookup"><span data-stu-id="66172-382">Points tooa sink location tooalso send diagnostic data.</span></span> <span data-ttu-id="66172-383">Bijvoorbeeld, Application Insights.</span><span class="sxs-lookup"><span data-stu-id="66172-383">For example, Application Insights.</span></span>|  

## <a name="dockersources"></a><span data-ttu-id="66172-384">DockerSources</span><span class="sxs-lookup"><span data-stu-id="66172-384">DockerSources</span></span>
 <span data-ttu-id="66172-385">*Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources-*</span><span class="sxs-lookup"><span data-stu-id="66172-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span></span>

 <span data-ttu-id="66172-386">In 1,9 toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="66172-386">Added in 1.9.</span></span>

|<span data-ttu-id="66172-387">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="66172-387">Element Name</span></span>|<span data-ttu-id="66172-388">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-388">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="66172-389">**Statistieken**</span><span class="sxs-lookup"><span data-stu-id="66172-389">**Stats**</span></span>|<span data-ttu-id="66172-390">Geeft Hallo systeem toocollect statistieken voor Docker-containers</span><span class="sxs-lookup"><span data-stu-id="66172-390">Tells hello system toocollect stats for Docker containers</span></span>|  

## <a name="sinksconfig-element"></a><span data-ttu-id="66172-391">SinksConfig Element</span><span class="sxs-lookup"><span data-stu-id="66172-391">SinksConfig Element</span></span>  
 <span data-ttu-id="66172-392">*Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span><span class="sxs-lookup"><span data-stu-id="66172-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span></span>

 <span data-ttu-id="66172-393">Een lijst met locaties toosend diagnostische gegevens tooand Hallo-configuratie die is gekoppeld aan deze locaties.</span><span class="sxs-lookup"><span data-stu-id="66172-393">A list of locations toosend diagnostics data tooand hello configuration associated with those locations.</span></span>  

|<span data-ttu-id="66172-394">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="66172-394">Element Name</span></span>|<span data-ttu-id="66172-395">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-395">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="66172-396">**Sink**</span><span class="sxs-lookup"><span data-stu-id="66172-396">**Sink**</span></span>|<span data-ttu-id="66172-397">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="66172-397">See description elsewhere on this page.</span></span>|  

## <a name="sink-element"></a><span data-ttu-id="66172-398">Sink-Element</span><span class="sxs-lookup"><span data-stu-id="66172-398">Sink Element</span></span>
 <span data-ttu-id="66172-399">*Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink-*</span><span class="sxs-lookup"><span data-stu-id="66172-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span></span>

 <span data-ttu-id="66172-400">In versie 1.5 toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="66172-400">Added in version 1.5.</span></span>  

 <span data-ttu-id="66172-401">Locaties toosend diagnostische gegevens naar definieert.</span><span class="sxs-lookup"><span data-stu-id="66172-401">Defines locations toosend diagnostic data to.</span></span> <span data-ttu-id="66172-402">Bijvoorbeeld: hello Application Insights-service.</span><span class="sxs-lookup"><span data-stu-id="66172-402">For example, hello Application Insights service.</span></span>  

|<span data-ttu-id="66172-403">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="66172-403">Attribute</span></span>|<span data-ttu-id="66172-404">Type</span><span class="sxs-lookup"><span data-stu-id="66172-404">Type</span></span>|<span data-ttu-id="66172-405">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-405">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="66172-406">**naam**</span><span class="sxs-lookup"><span data-stu-id="66172-406">**name**</span></span>|<span data-ttu-id="66172-407">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="66172-407">string</span></span>|<span data-ttu-id="66172-408">Een Hallo van tekenreeks identificerende sinkname.</span><span class="sxs-lookup"><span data-stu-id="66172-408">A string identifying hello sinkname.</span></span>|  

|<span data-ttu-id="66172-409">Element</span><span class="sxs-lookup"><span data-stu-id="66172-409">Element</span></span>|<span data-ttu-id="66172-410">Type</span><span class="sxs-lookup"><span data-stu-id="66172-410">Type</span></span>|<span data-ttu-id="66172-411">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-411">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="66172-412">**Application Insights**</span><span class="sxs-lookup"><span data-stu-id="66172-412">**Application Insights**</span></span>|<span data-ttu-id="66172-413">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="66172-413">string</span></span>|<span data-ttu-id="66172-414">Alleen bij het verzenden van gegevens tooApplication Insights gebruikt.</span><span class="sxs-lookup"><span data-stu-id="66172-414">Used only when sending data tooApplication Insights.</span></span> <span data-ttu-id="66172-415">Hallo Instrumentatiesleutel voor een actieve Application Insights-account dat u toegang tot hebt bevatten.</span><span class="sxs-lookup"><span data-stu-id="66172-415">Contain hello Instrumentation Key for an active Application Insights account that you have access to.</span></span>|  
|<span data-ttu-id="66172-416">**Kanalen**</span><span class="sxs-lookup"><span data-stu-id="66172-416">**Channels**</span></span>|<span data-ttu-id="66172-417">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="66172-417">string</span></span>|<span data-ttu-id="66172-418">Één voor elke extra filteren die u stream</span><span class="sxs-lookup"><span data-stu-id="66172-418">One for each additional filtering that stream that you</span></span>|  

## <a name="channels-element"></a><span data-ttu-id="66172-419">Kanalen Element</span><span class="sxs-lookup"><span data-stu-id="66172-419">Channels Element</span></span>  
 <span data-ttu-id="66172-420">*Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - kanalen*</span><span class="sxs-lookup"><span data-stu-id="66172-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span></span>

 <span data-ttu-id="66172-421">In versie 1.5 toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="66172-421">Added in version 1.5.</span></span>  

 <span data-ttu-id="66172-422">Hiermee definieert u filters voor stromen van logboekgegevens een sink te doorlopen.</span><span class="sxs-lookup"><span data-stu-id="66172-422">Defines filters for streams of log data passing through a sink.</span></span>  

|<span data-ttu-id="66172-423">Element</span><span class="sxs-lookup"><span data-stu-id="66172-423">Element</span></span>|<span data-ttu-id="66172-424">Type</span><span class="sxs-lookup"><span data-stu-id="66172-424">Type</span></span>|<span data-ttu-id="66172-425">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-425">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="66172-426">**Kanaal**</span><span class="sxs-lookup"><span data-stu-id="66172-426">**Channel**</span></span>|<span data-ttu-id="66172-427">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="66172-427">string</span></span>|<span data-ttu-id="66172-428">Zie de beschrijving ergens anders op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="66172-428">See description elsewhere on this page.</span></span>|  

## <a name="channel-element"></a><span data-ttu-id="66172-429">Kanaal-Element</span><span class="sxs-lookup"><span data-stu-id="66172-429">Channel Element</span></span>
 <span data-ttu-id="66172-430">*Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - kanalen - kanaal*</span><span class="sxs-lookup"><span data-stu-id="66172-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span></span>

 <span data-ttu-id="66172-431">In versie 1.5 toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="66172-431">Added in version 1.5.</span></span>  

 <span data-ttu-id="66172-432">Locaties toosend diagnostische gegevens naar definieert.</span><span class="sxs-lookup"><span data-stu-id="66172-432">Defines locations toosend diagnostic data to.</span></span> <span data-ttu-id="66172-433">Bijvoorbeeld: hello Application Insights-service.</span><span class="sxs-lookup"><span data-stu-id="66172-433">For example, hello Application Insights service.</span></span>  

|<span data-ttu-id="66172-434">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="66172-434">Attributes</span></span>|<span data-ttu-id="66172-435">Type</span><span class="sxs-lookup"><span data-stu-id="66172-435">Type</span></span>|<span data-ttu-id="66172-436">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-436">Description</span></span>|  
|----------------|----------|-----------------|  
|<span data-ttu-id="66172-437">**logLevel**</span><span class="sxs-lookup"><span data-stu-id="66172-437">**logLevel**</span></span>|<span data-ttu-id="66172-438">**tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="66172-438">**string**</span></span>|<span data-ttu-id="66172-439">Hiermee geeft u een minimale ernstniveau Hallo voor logboekvermeldingen die worden overgedragen.</span><span class="sxs-lookup"><span data-stu-id="66172-439">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="66172-440">de standaardwaarde Hallo is **Undefined**, die alle logboeken overdraagt.</span><span class="sxs-lookup"><span data-stu-id="66172-440">hello default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="66172-441">Andere mogelijke waarden (in volgorde van de meeste tooleast gegevens) zijn **uitgebreid**, **informatie**, **waarschuwing**, **fout**, en **Kritieke**.</span><span class="sxs-lookup"><span data-stu-id="66172-441">Other possible values (in order of most tooleast information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="66172-442">**naam**</span><span class="sxs-lookup"><span data-stu-id="66172-442">**name**</span></span>|<span data-ttu-id="66172-443">**tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="66172-443">**string**</span></span>|<span data-ttu-id="66172-444">Een unieke naam van Hallo kanaal toorefer naar</span><span class="sxs-lookup"><span data-stu-id="66172-444">A unique name of hello channel toorefer to</span></span>|  


## <a name="privateconfig-element"></a><span data-ttu-id="66172-445">PrivateConfig Element</span><span class="sxs-lookup"><span data-stu-id="66172-445">PrivateConfig Element</span></span> 
 <span data-ttu-id="66172-446">*Structuur: Basis - DiagnosticsConfiguration - PrivateConfig*</span><span class="sxs-lookup"><span data-stu-id="66172-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span></span>

 <span data-ttu-id="66172-447">In versie 1.3 toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="66172-447">Added in version 1.3.</span></span>  

 <span data-ttu-id="66172-448">Optioneel</span><span class="sxs-lookup"><span data-stu-id="66172-448">Optional</span></span>  

 <span data-ttu-id="66172-449">Slaat de details van persoonlijke Hallo van Hallo storage-account (naam, sleutel en -eindpunt).</span><span class="sxs-lookup"><span data-stu-id="66172-449">Stores hello private details of hello storage account (name, key, and endpoint).</span></span> <span data-ttu-id="66172-450">Deze informatie toohello virtuele machine wordt verzonden, maar kan niet worden opgehaald uit.</span><span class="sxs-lookup"><span data-stu-id="66172-450">This information is sent toohello virtual machine, but cannot be retrieved from it.</span></span>  

|<span data-ttu-id="66172-451">Onderliggende elementen</span><span class="sxs-lookup"><span data-stu-id="66172-451">Child Elements</span></span>|<span data-ttu-id="66172-452">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="66172-452">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="66172-453">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="66172-453">**StorageAccount**</span></span>|<span data-ttu-id="66172-454">Hallo storage account toouse.</span><span class="sxs-lookup"><span data-stu-id="66172-454">hello storage account toouse.</span></span> <span data-ttu-id="66172-455">Hallo na kenmerken zijn vereist</span><span class="sxs-lookup"><span data-stu-id="66172-455">hello following attributes are required</span></span><br /><br /> <span data-ttu-id="66172-456">- **naam** - hello naam van het Hallo-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="66172-456">- **name** - hello name of hello storage account.</span></span><br /><br /> <span data-ttu-id="66172-457">- **sleutel** - hello sleutel toohello storage-account.</span><span class="sxs-lookup"><span data-stu-id="66172-457">- **key** - hello key toohello storage account.</span></span><br /><br /> <span data-ttu-id="66172-458">- **eindpunt** -Hallo eindpunt tooaccess Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="66172-458">- **endpoint** - hello endpoint tooaccess hello storage account.</span></span> <br /><br /> <span data-ttu-id="66172-459">-**sasToken** (1.8.1)-kunt u een SAS-token in plaats van de sleutel van een opslagaccount in de persoonlijke configuratie Hallo toegevoegd. Indien opgegeven, wordt de opslagaccountsleutel Hallo genegeerd.</span><span class="sxs-lookup"><span data-stu-id="66172-459">-**sasToken** (added 1.8.1)- You can specify an SAS token instead of a storage account key in hello private config. If provided, hello storage account key is ignored.</span></span> <br /><span data-ttu-id="66172-460">Vereisten voor Hallo SAS-Token:</span><span class="sxs-lookup"><span data-stu-id="66172-460">Requirements for hello SAS Token:</span></span> <br /><span data-ttu-id="66172-461">-Ondersteunt alleen account SAS-token</span><span class="sxs-lookup"><span data-stu-id="66172-461">- Supports account SAS token only</span></span> <br /><span data-ttu-id="66172-462">- *b*, *t* servicetypen zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="66172-462">- *b*, *t* service types are required.</span></span> <br /> <span data-ttu-id="66172-463">- *een*, *c*, *u*, *w* machtigingen zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="66172-463">- *a*, *c*, *u*, *w* permissions are required.</span></span> <br /> <span data-ttu-id="66172-464">- *c*, *o* brontypen die zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="66172-464">- *c*, *o* resource types are required.</span></span> <br /> <span data-ttu-id="66172-465">-Ondersteunt alleen Hallo HTTPS-protocol</span><span class="sxs-lookup"><span data-stu-id="66172-465">- Supports hello HTTPS protocol only</span></span> <br /> <span data-ttu-id="66172-466">-Starten en het verlooptijdstip moet geldig zijn.</span><span class="sxs-lookup"><span data-stu-id="66172-466">- Start and expiry time must be valid.</span></span>|  


## <a name="isenabled-element"></a><span data-ttu-id="66172-467">IsEnabled Element</span><span class="sxs-lookup"><span data-stu-id="66172-467">IsEnabled Element</span></span>  
 <span data-ttu-id="66172-468">*Structuur: Basis - DiagnosticsConfiguration - IsEnabled*</span><span class="sxs-lookup"><span data-stu-id="66172-468">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span></span>

 <span data-ttu-id="66172-469">Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="66172-469">Boolean.</span></span> <span data-ttu-id="66172-470">Gebruik `true` tooenable Hallo diagnostics of `false` toodisable Hallo diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="66172-470">Use `true` tooenable hello diagnostics or `false` toodisable hello diagnostics.</span></span>
