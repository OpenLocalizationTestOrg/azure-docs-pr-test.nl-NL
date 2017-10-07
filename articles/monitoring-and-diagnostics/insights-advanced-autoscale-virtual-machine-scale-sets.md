---
title: aaaAdvanced automatisch schalen met behulp van Azure Virtual Machines | Microsoft Docs
description: Maakt gebruik van Resource Manager en VM-Schaalsets met meerdere regels en -profielen die e-mail verzenden en roept u webhook-URL's met de schaalacties.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 7e3576e2-4a2b-4736-b5ae-98c4689cdd2b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2016
ms.author: ancav
ms.openlocfilehash: ecb01e3094f715837b75ef07a7dbecdf0f2e78f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a><span data-ttu-id="9d0e0-103">Configuratie van geavanceerde automatisch schalen met Resource Manager-sjablonen voor VM-Schaalsets</span><span class="sxs-lookup"><span data-stu-id="9d0e0-103">Advanced autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>
<span data-ttu-id="9d0e0-104">U kunt de schaal in en scale-out in virtuele-Machineschaalsets op basis van drempelwaarden voor prestaties metrische door een terugkerend schema of door een bepaalde datum.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-104">You can scale-in and scale-out in Virtual Machine Scale Sets based on performance metric thresholds, by a recurring schedule, or by a particular date.</span></span> <span data-ttu-id="9d0e0-105">U kunt ook e-mail en -webhook meldingen voor schaalacties configureren.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-105">You can also configure email and webhook notifications for scale actions.</span></span> <span data-ttu-id="9d0e0-106">Dit overzicht toont een voorbeeld van de configuratie van deze objecten die zijn met een Resource Manager-sjabloon op een VM-Schaalset.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-106">This walkthrough shows an example of configuring all these objects using a Resource Manager template on a VM Scale Set.</span></span>

> [!NOTE]
> <span data-ttu-id="9d0e0-107">Tijdens deze procedure worden de Hallo stappen uitgelegd voor VM-Schaalsets, hello dezelfde informatie is van toepassing tooautoscaling [Cloudservices](https://azure.microsoft.com/services/cloud-services/), en [App Service - Web-Apps](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="9d0e0-107">While this walkthrough explains hello steps for VM Scale Sets, hello same information applies tooautoscaling [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span>
> <span data-ttu-id="9d0e0-108">Voor een eenvoudige schaal in/out-instelling op een VM-Schaalset gebaseerd op een eenvoudige prestaties metrische gegevens zoals CPU, Raadpleeg toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) en [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documenten</span><span class="sxs-lookup"><span data-stu-id="9d0e0-108">For a simple scale in/out setting on a VM Scale Set based on a simple performance metric such as CPU, refer toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) and [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents</span></span>
>
>

## <a name="walkthrough"></a><span data-ttu-id="9d0e0-109">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="9d0e0-109">Walkthrough</span></span>
<span data-ttu-id="9d0e0-110">In dit scenario, gebruiken we [Azure Resource Explorer](https://resources.azure.com/) tooconfigure en update Hallo instelling voor automatisch schalen voor een scale-set.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-110">In this walkthrough, we use [Azure Resource Explorer](https://resources.azure.com/) tooconfigure and update hello autoscale setting for a scale set.</span></span> <span data-ttu-id="9d0e0-111">Azure Resource Explorer is een eenvoudige manier toomanage Azure-resources via Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-111">Azure Resource Explorer is an easy way toomanage Azure resources via Resource Manager templates.</span></span> <span data-ttu-id="9d0e0-112">Als u nieuwe tooAzure Resource Explorer hulpprogramma, lezen [deze inleiding](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span><span class="sxs-lookup"><span data-stu-id="9d0e0-112">If you are new tooAzure Resource Explorer tool, read [this introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span></span>

1. <span data-ttu-id="9d0e0-113">Implementeer een nieuwe schaal ingesteld met een instelling voor automatisch schalen die basic.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-113">Deploy a new scale set with a basic autoscale setting.</span></span> <span data-ttu-id="9d0e0-114">Dit artikel wordt Hallo uit de Snelstartgalerie Azure, met een Windows hello schaalset met een sjabloon basic automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-114">This article uses hello one from hello Azure QuickStart Gallery, which has a Windows scale set with a basic autoscale template.</span></span> <span data-ttu-id="9d0e0-115">Linux scale ingesteld werk Hallo dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-115">Linux scale sets work hello same way.</span></span>
2. <span data-ttu-id="9d0e0-116">Na het Hallo-scale set wordt gemaakt, gaat u toohello scale set resource van Azure Resource Explorer.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-116">After hello scale set is created, navigate toohello scale set resource from Azure Resource Explorer.</span></span> <span data-ttu-id="9d0e0-117">U ziet Hallo volgende onder het knooppunt Microsoft.Insights.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-117">You see hello following under Microsoft.Insights node.</span></span>

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    <span data-ttu-id="9d0e0-119">Hallo sjabloon uitvoering een standaardinstelling voor automatisch schalen is gemaakt met de naam van de Hallo **'autoscalewad'**.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-119">hello template execution has created a default autoscale setting with hello name **'autoscalewad'**.</span></span> <span data-ttu-id="9d0e0-120">U kunt aan de rechterkant hello, Hallo volledige definitie van deze instelling voor automatisch schalen weergeven.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-120">On hello right-hand side, you can view hello full definition of this autoscale setting.</span></span> <span data-ttu-id="9d0e0-121">In dit geval de standaardinstelling voor automatisch schalen hello wordt geleverd met een regel CPU % op basis van scale-out en de schaal.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-121">In this case, hello default autoscale setting comes with a CPU% based scale-out and scale-in rule.</span></span>  

3. <span data-ttu-id="9d0e0-122">U kunt nu meer regels op basis van Hallo planning of specifieke vereisten en -profielen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-122">You can now add more profiles and rules based on hello schedule or specific requirements.</span></span> <span data-ttu-id="9d0e0-123">We maken een instelling voor automatisch schalen met drie profielen.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-123">We create an autoscale setting with three profiles.</span></span> <span data-ttu-id="9d0e0-124">toounderstand profielen en regels in voor automatisch schalen, Bekijk [Best Practices voor automatisch schalen](insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="9d0e0-124">toounderstand profiles and rules in autoscale, review [Autoscale Best Practices](insights-autoscale-best-practices.md).</span></span>  

    | <span data-ttu-id="9d0e0-125">Profielen en regels</span><span class="sxs-lookup"><span data-stu-id="9d0e0-125">Profiles & Rules</span></span> | <span data-ttu-id="9d0e0-126">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9d0e0-126">Description</span></span> |
    |--- | --- |
    | <span data-ttu-id="9d0e0-127">**Profiel**</span><span class="sxs-lookup"><span data-stu-id="9d0e0-127">**Profile**</span></span> |<span data-ttu-id="9d0e0-128">**Op basis van metrische gegevens en prestaties**</span><span class="sxs-lookup"><span data-stu-id="9d0e0-128">**Performance/metric based**</span></span> |
    | <span data-ttu-id="9d0e0-129">Regel</span><span class="sxs-lookup"><span data-stu-id="9d0e0-129">Rule</span></span> |<span data-ttu-id="9d0e0-130">Aantal berichten Service Bus-wachtrij > x</span><span class="sxs-lookup"><span data-stu-id="9d0e0-130">Service Bus Queue Message Count > x</span></span> |
    | <span data-ttu-id="9d0e0-131">Regel</span><span class="sxs-lookup"><span data-stu-id="9d0e0-131">Rule</span></span> |<span data-ttu-id="9d0e0-132">Aantal berichten Service Bus-wachtrij < y</span><span class="sxs-lookup"><span data-stu-id="9d0e0-132">Service Bus Queue Message Count < y</span></span> |
    | <span data-ttu-id="9d0e0-133">Regel</span><span class="sxs-lookup"><span data-stu-id="9d0e0-133">Rule</span></span> |<span data-ttu-id="9d0e0-134">CPU-percentage > n</span><span class="sxs-lookup"><span data-stu-id="9d0e0-134">CPU% > n</span></span> |
    | <span data-ttu-id="9d0e0-135">Regel</span><span class="sxs-lookup"><span data-stu-id="9d0e0-135">Rule</span></span> |<span data-ttu-id="9d0e0-136">CPU-percentage < p</span><span class="sxs-lookup"><span data-stu-id="9d0e0-136">CPU% < p</span></span> |
    | <span data-ttu-id="9d0e0-137">**Profiel**</span><span class="sxs-lookup"><span data-stu-id="9d0e0-137">**Profile**</span></span> |<span data-ttu-id="9d0e0-138">**Werkdag ochtend uur (geen regels)**</span><span class="sxs-lookup"><span data-stu-id="9d0e0-138">**Weekday morning hours (no rules)**</span></span> |
    | <span data-ttu-id="9d0e0-139">**Profiel**</span><span class="sxs-lookup"><span data-stu-id="9d0e0-139">**Profile**</span></span> |<span data-ttu-id="9d0e0-140">**Product starten dag (geen regels)**</span><span class="sxs-lookup"><span data-stu-id="9d0e0-140">**Product Launch day (no rules)**</span></span> |

4. <span data-ttu-id="9d0e0-141">Hier volgt een hypothetische vergroten/verkleinen scenario dat we voor deze procedure gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-141">Here is a hypothetical scaling scenario that we use for this walk-through.</span></span>

    * <span data-ttu-id="9d0e0-142">**Op basis van Load** -tooscale of op basis van Hallo belasting van de toepassing die wordt gehost op mijn set.* schaal wilt</span><span class="sxs-lookup"><span data-stu-id="9d0e0-142">**Load based** - I'd like tooscale out or in based on hello load on my application hosted on my scale set.*</span></span>
    * <span data-ttu-id="9d0e0-143">**Grootte van de wachtrij bericht** -ik een Service Bus-wachtrij voor Hallo binnenkomende berichten toomy toepassing gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-143">**Message Queue size** - I use a Service Bus Queue for hello incoming messages toomy application.</span></span> <span data-ttu-id="9d0e0-144">Ik gebruik aantal van de wachtrij van het Hallo-berichten en CPU-percentage en configureren van een standaard profiel tootrigger een schaalactie als het aantal berichten of CPU treffers threshold.* Hallo</span><span class="sxs-lookup"><span data-stu-id="9d0e0-144">I use hello queue's message count and CPU% and configure a default profile tootrigger a scale action if either of message count or CPU hits hello threshold.*</span></span>
    * <span data-ttu-id="9d0e0-145">**Tijd van de week en dag** -ik wil een wekelijks terugkerende 'tijd van de dag Hallo' op basis van profiel 'Hours werkdag ochtend' genoemd.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-145">**Time of week and day** - I want a weekly recurring 'time of hello day' based profile called 'Weekday Morning Hours'.</span></span> <span data-ttu-id="9d0e0-146">Op basis van historische gegevens, weet ik is beter toohave bepaalde aantal VM-exemplaren toohandle laden van mijn toepassingen tijdens deze time.*</span><span class="sxs-lookup"><span data-stu-id="9d0e0-146">Based on historical data, I know it is better toohave certain number of VM instances toohandle my application's load during this time.*</span></span>
    * <span data-ttu-id="9d0e0-147">**Speciale datums** -ik heb een profiel 'Product starten dag' toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-147">**Special Dates** - I added a 'Product Launch Day' profile.</span></span> <span data-ttu-id="9d0e0-148">Ik vooruit te plannen voor specifieke datums zodat de toepassing gereed toohandle Hallo laden vanwege marketing aankondigingen en wanneer er een nieuw product in Hallo application.* plaatsen</span><span class="sxs-lookup"><span data-stu-id="9d0e0-148">I plan ahead for specific dates so my application is ready toohandle hello load due marketing announcements and when we put a new product in hello application.*</span></span>
    * <span data-ttu-id="9d0e0-149">*de laatste twee profielen Hallo kunnen ook andere prestaties metrische gebaseerde regels binnen deze hebben. In dit geval ik niet toohave een besloten en in plaats daarvan toorely op Hallo standaard prestaties metriek op basis van regels. Regels zijn optioneel voor Hallo terugkerende en op basis van datum-profielen.*</span><span class="sxs-lookup"><span data-stu-id="9d0e0-149">*hello last two profiles can also have other performance metric based rules within them. In this case, I decided not toohave one and instead toorely on hello default performance metric based rules. Rules are optional for hello recurring and date-based profiles.*</span></span>

    <span data-ttu-id="9d0e0-150">Prioriteitsaanduiding van Hallo profielen en regels voor automatisch schalen-engine wordt ook vastgelegd in Hallo [aanbevolen procedures voor automatisch schalen](insights-autoscale-best-practices.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-150">Autoscale engine's prioritization of hello profiles and rules is also captured in hello [autoscaling best practices](insights-autoscale-best-practices.md) article.</span></span>
    <span data-ttu-id="9d0e0-151">Raadpleeg voor een lijst met algemene metrische gegevens voor automatisch schalen, [algemene metrische gegevens voor automatisch schalen](insights-autoscale-common-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="9d0e0-151">For a list of common metrics for autoscale, refer [Common metrics for Autoscale](insights-autoscale-common-metrics.md)</span></span>

5. <span data-ttu-id="9d0e0-152">Zorg ervoor dat u zich op Hallo **lezen/schrijven** modus in Resource Explorer</span><span class="sxs-lookup"><span data-stu-id="9d0e0-152">Make sure you are on hello **Read/Write** mode in Resource Explorer</span></span>

    ![Autoscalewad, instelling standaard voor automatisch schalen](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. <span data-ttu-id="9d0e0-154">Klik op bewerken.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-154">Click Edit.</span></span> <span data-ttu-id="9d0e0-155">**Vervang** Hallo 'profielen'-element in de instelling voor automatisch schalen Hello volgende configuratie:</span><span class="sxs-lookup"><span data-stu-id="9d0e0-155">**Replace** hello 'profiles' element in autoscale setting with hello following configuration:</span></span>

    ![Profielen](./media/insights-advanced-autoscale-vmss/profiles.png)

    ```
    {
            "name": "Perf_Based_Scale",
            "capacity": {
              "minimum": "2",
              "maximum": "12",
              "default": "2"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 10
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 3
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 85
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          },
          {
            "name": "Weekday_Morning_Hours_Scale",
            "capacity": {
              "minimum": "4",
              "maximum": "12",
              "default": "4"
            },
            "rules": [],
            "recurrence": {
              "frequency": "Week",
              "schedule": {
                "timeZone": "Pacific Standard Time",
                "days": [
                  "Monday",
                  "Tuesday",
                  "Wednesday",
                  "Thursday",
                  "Friday"
                ],
                "hours": [
                  6
                ],
                "minutes": [
                  0
                ]
              }
            }
          },
          {
            "name": "Product_Launch_Day",
            "capacity": {
              "minimum": "6",
              "maximum": "20",
              "default": "6"
            },
            "rules": [],
            "fixedDate": {
              "timeZone": "Pacific Standard Time",
              "start": "2016-06-20T00:06:00Z",
              "end": "2016-06-21T23:59:00Z"
            }
          }
    ```
    <span data-ttu-id="9d0e0-157">Zie voor ondersteunde velden en hun waarden [automatisch schalen REST API-documentatie](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d0e0-157">For supported fields and their values, see [Autoscale REST API documentation](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span></span> <span data-ttu-id="9d0e0-158">De instelling voor automatisch schalen bevat nu de drie profielen Hallo hierboven is uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-158">Now your autoscale setting contains hello three profiles explained previously.</span></span>

7. <span data-ttu-id="9d0e0-159">Tot slot bekijkt hello automatisch schalen **melding** sectie.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-159">Finally, look at hello Autoscale **notification** section.</span></span> <span data-ttu-id="9d0e0-160">Meldingen over automatisch schalen kunt u de drie dingen toodo wanneer een scale-out of in actie met succes wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-160">Autoscale notifications allow you toodo three things when a scale-out or in action is successfully triggered.</span></span>
   - <span data-ttu-id="9d0e0-161">Hallo beheerder en co-beheerders van uw abonnement</span><span class="sxs-lookup"><span data-stu-id="9d0e0-161">Notify hello admin and co-admins of your subscription</span></span>
   - <span data-ttu-id="9d0e0-162">Een set gebruikers een e-mail</span><span class="sxs-lookup"><span data-stu-id="9d0e0-162">Email a set of users</span></span>
   - <span data-ttu-id="9d0e0-163">Activeren van een webhook-aanroep.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-163">Trigger a webhook call.</span></span> <span data-ttu-id="9d0e0-164">Wanneer deze gebeurtenis wordt gestart, deze webhook stuurt de metagegevens over Hallo automatisch schalen voorwaarde en Hallo schaalset resource.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-164">When fired, this webhook sends metadata about hello autoscaling condition and hello scale set resource.</span></span> <span data-ttu-id="9d0e0-165">toolearn meer informatie over het Hallo-nettolading van de webhook automatisch schalen, Zie [configureren Webhook & e-mailmeldingen voor automatisch schalen](insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="9d0e0-165">toolearn more about hello payload of autoscale webhook, see [Configure Webhook & Email Notifications for Autoscale](insights-autoscale-to-webhook-email.md).</span></span>

   <span data-ttu-id="9d0e0-166">Hallo na toohello automatisch schalen instelling vervangen toevoegen uw **melding** element waarvan de waarde null is</span><span class="sxs-lookup"><span data-stu-id="9d0e0-166">Add hello following toohello Autoscale setting replacing your **notification** element whose value is null</span></span>

   ```
   "notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": true,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]

   ```

   <span data-ttu-id="9d0e0-167">Klik op **plaatsen** knop in Resource Explorer tooupdate Hallo-instelling voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-167">Hit **Put** button in Resource Explorer tooupdate hello autoscale setting.</span></span>

<span data-ttu-id="9d0e0-168">U hebt bijgewerkt een instelling op een VM-Scale set tooinclude meerdere scale profielen voor automatisch schalen en schalen van meldingen.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-168">You have updated an autoscale setting on a VM Scale set tooinclude multiple scale profiles and scale notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d0e0-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9d0e0-169">Next Steps</span></span>
<span data-ttu-id="9d0e0-170">Gebruik deze koppelingen toolearn meer informatie over automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="9d0e0-170">Use these links toolearn more about autoscaling.</span></span>

[<span data-ttu-id="9d0e0-171">Problemen oplossen met virtuele-Machineschaalsets voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="9d0e0-171">TroubleShoot Autoscale with Virtual Machine Scale Sets</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[<span data-ttu-id="9d0e0-172">Algemene metrische gegevens voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="9d0e0-172">Common Metrics for Autoscale</span></span>](insights-autoscale-common-metrics.md)

[<span data-ttu-id="9d0e0-173">Aanbevolen procedures voor Azure automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="9d0e0-173">Best Practices for Azure Autoscale</span></span>](insights-autoscale-best-practices.md)

[<span data-ttu-id="9d0e0-174">Beheren met behulp van PowerShell voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="9d0e0-174">Manage Autoscale using PowerShell</span></span>](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[<span data-ttu-id="9d0e0-175">Beheren met CLI voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="9d0e0-175">Manage Autoscale using CLI</span></span>](insights-cli-samples.md#autoscale)

[<span data-ttu-id="9d0e0-176">Webhook & e-mailmeldingen voor automatisch schalen configureren</span><span class="sxs-lookup"><span data-stu-id="9d0e0-176">Configure Webhook & Email Notifications for Autoscale</span></span>](insights-autoscale-to-webhook-email.md)
