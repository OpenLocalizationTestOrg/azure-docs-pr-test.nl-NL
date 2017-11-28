---
title: aaaUse automatisch schalen acties toosend e-mail en -webhook waarschuwingsmeldingen. | Microsoft Docs
description: 'Zie hoe toouse automatisch schalen acties toocall web-URL''s of verzenden van e-mailmeldingen in de Azure-Monitor. '
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: eb9a4c98-0894-488c-8ee8-5df0065d094f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: ancav
ms.openlocfilehash: f611a18f5a808412fbdd0c89e3addb36437064c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-autoscale-actions-toosend-email-and-webhook-alert-notifications-in-azure-monitor"></a><span data-ttu-id="aef46-104">Gebruik voor automatisch schalen acties toosend e-mail en -webhook waarschuwingsmeldingen in de Azure-Monitor</span><span class="sxs-lookup"><span data-stu-id="aef46-104">Use autoscale actions toosend email and webhook alert notifications in Azure Monitor</span></span>
<span data-ttu-id="aef46-105">Dit artikel ziet u hoe u triggers hebt instelt, zodat u kunt specifieke web-URL's aanroepen of verzenden van e-mailberichten op basis van de acties voor automatisch schalen in Azure.</span><span class="sxs-lookup"><span data-stu-id="aef46-105">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span></span>  

## <a name="webhooks"></a><span data-ttu-id="aef46-106">Webhooks.</span><span class="sxs-lookup"><span data-stu-id="aef46-106">Webhooks</span></span>
<span data-ttu-id="aef46-107">Webhooks kunt u tooroute hello Azure waarschuwingsmeldingen tooother systemen voor na verwerking of aangepaste meldingen.</span><span class="sxs-lookup"><span data-stu-id="aef46-107">Webhooks allow you tooroute hello Azure alert notifications tooother systems for post-processing or custom notifications.</span></span> <span data-ttu-id="aef46-108">Bijvoorbeeld een team chat gebruiken of messaging-services de hoogte stellen routering Hallo waarschuwing tooservices dat een binnenkomende web aanvraag toosend SMS, meld bugs kan verwerken, enz. Hallo webhook URI moet een geldige HTTP of HTTPS-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="aef46-108">For example, routing hello alert tooservices that can handle an incoming web request toosend SMS, log bugs, notify a team using chat or messaging services, etc. hello webhook URI must be a valid HTTP or HTTPS endpoint.</span></span>

## <a name="email"></a><span data-ttu-id="aef46-109">E-mail</span><span class="sxs-lookup"><span data-stu-id="aef46-109">Email</span></span>
<span data-ttu-id="aef46-110">E-mail kan worden verstuurd tooany geldig e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="aef46-110">Email can be sent tooany valid email address.</span></span> <span data-ttu-id="aef46-111">Beheerders en medebeheerders van Hallo abonnement waarbij Hallo-regel wordt uitgevoerd, wordt ook gewaarschuwd.</span><span class="sxs-lookup"><span data-stu-id="aef46-111">Administrators and co-administrators of hello subscription where hello rule is running will also be notified.</span></span>

## <a name="cloud-services-and-web-apps"></a><span data-ttu-id="aef46-112">Cloudservices en Web-Apps</span><span class="sxs-lookup"><span data-stu-id="aef46-112">Cloud Services and Web Apps</span></span>
<span data-ttu-id="aef46-113">U kunt aanmelden van hello Azure-portal voor Cloudservices en serverfarms (Web-Apps).</span><span class="sxs-lookup"><span data-stu-id="aef46-113">You can opt-in from hello Azure portal for Cloud Services and Server Farms (Web Apps).</span></span>

* <span data-ttu-id="aef46-114">Kies Hallo **schalen door** metriek.</span><span class="sxs-lookup"><span data-stu-id="aef46-114">Choose hello **scale by** metric.</span></span>

![schalen door](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="aef46-116">Virtuele-machineschaalsets</span><span class="sxs-lookup"><span data-stu-id="aef46-116">Virtual Machine scale sets</span></span>
<span data-ttu-id="aef46-117">Voor nieuwere virtuele Machines met Resource Manager (virtuele-machineschaalsets) gemaakt, kunt u dit met behulp van REST-API, Resource Manager-sjablonen, PowerShell en CLI.</span><span class="sxs-lookup"><span data-stu-id="aef46-117">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span></span> <span data-ttu-id="aef46-118">De interface van de portal is nog niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="aef46-118">A portal interface is not yet available.</span></span>
<span data-ttu-id="aef46-119">Wanneer u Hallo REST-API of Resource Manager-sjabloon, neemt u Hallo meldingen element Hello opties te volgen.</span><span class="sxs-lookup"><span data-stu-id="aef46-119">When using hello REST API or Resource Manager template, include hello notifications element with hello following options.</span></span>

```
"notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": false,
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
| <span data-ttu-id="aef46-120">Veld</span><span class="sxs-lookup"><span data-stu-id="aef46-120">Field</span></span> | <span data-ttu-id="aef46-121">Verplichte?</span><span class="sxs-lookup"><span data-stu-id="aef46-121">Mandatory?</span></span> | <span data-ttu-id="aef46-122">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="aef46-122">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="aef46-123">bewerking</span><span class="sxs-lookup"><span data-stu-id="aef46-123">operation</span></span> |<span data-ttu-id="aef46-124">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-124">yes</span></span> |<span data-ttu-id="aef46-125">de waarde moet 'Schaal'</span><span class="sxs-lookup"><span data-stu-id="aef46-125">value must be "Scale"</span></span> |
| <span data-ttu-id="aef46-126">sendToSubscriptionAdministrator</span><span class="sxs-lookup"><span data-stu-id="aef46-126">sendToSubscriptionAdministrator</span></span> |<span data-ttu-id="aef46-127">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-127">yes</span></span> |<span data-ttu-id="aef46-128">waarde moet 'true' of 'false'</span><span class="sxs-lookup"><span data-stu-id="aef46-128">value must be "true" or "false"</span></span> |
| <span data-ttu-id="aef46-129">sendToSubscriptionCoAdministrators</span><span class="sxs-lookup"><span data-stu-id="aef46-129">sendToSubscriptionCoAdministrators</span></span> |<span data-ttu-id="aef46-130">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-130">yes</span></span> |<span data-ttu-id="aef46-131">waarde moet 'true' of 'false'</span><span class="sxs-lookup"><span data-stu-id="aef46-131">value must be "true" or "false"</span></span> |
| <span data-ttu-id="aef46-132">customEmails</span><span class="sxs-lookup"><span data-stu-id="aef46-132">customEmails</span></span> |<span data-ttu-id="aef46-133">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-133">yes</span></span> |<span data-ttu-id="aef46-134">mogelijke waarden zijn null [] of string-matrix van e-mailberichten</span><span class="sxs-lookup"><span data-stu-id="aef46-134">value can be null [] or string array of emails</span></span> |
| <span data-ttu-id="aef46-135">Webhooks.</span><span class="sxs-lookup"><span data-stu-id="aef46-135">webhooks</span></span> |<span data-ttu-id="aef46-136">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-136">yes</span></span> |<span data-ttu-id="aef46-137">mogelijke waarden zijn null of geldig Uri</span><span class="sxs-lookup"><span data-stu-id="aef46-137">value can be null or valid Uri</span></span> |
| <span data-ttu-id="aef46-138">serviceUri</span><span class="sxs-lookup"><span data-stu-id="aef46-138">serviceUri</span></span> |<span data-ttu-id="aef46-139">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-139">yes</span></span> |<span data-ttu-id="aef46-140">een geldige https Uri</span><span class="sxs-lookup"><span data-stu-id="aef46-140">a valid https Uri</span></span> |
| <span data-ttu-id="aef46-141">properties</span><span class="sxs-lookup"><span data-stu-id="aef46-141">properties</span></span> |<span data-ttu-id="aef46-142">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-142">yes</span></span> |<span data-ttu-id="aef46-143">waarde moet leeg {} opzoeken of sleutel-waardeparen kan bevatten</span><span class="sxs-lookup"><span data-stu-id="aef46-143">value must be empty {} or can contain key-value pairs</span></span> |

## <a name="authentication-in-webhooks"></a><span data-ttu-id="aef46-144">Verificatie in webhooks.</span><span class="sxs-lookup"><span data-stu-id="aef46-144">Authentication in webhooks</span></span>
<span data-ttu-id="aef46-145">Hallo webhook kunt verifiëren met behulp van verificatie op basis van tokens opslaglocatie Hallo webhook URI met een token ID als een queryparameter.</span><span class="sxs-lookup"><span data-stu-id="aef46-145">hello webhook can authenticate using token-based authentication, where you save hello webhook URI with a token ID as a query parameter.</span></span> <span data-ttu-id="aef46-146">Bijvoorbeeld: https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span><span class="sxs-lookup"><span data-stu-id="aef46-146">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span></span>

## <a name="autoscale-notification-webhook-payload-schema"></a><span data-ttu-id="aef46-147">Schema voor automatisch schalen melding webhook nettolading</span><span class="sxs-lookup"><span data-stu-id="aef46-147">Autoscale notification webhook payload schema</span></span>
<span data-ttu-id="aef46-148">Wanneer Hallo automatisch schalen melding wordt gegenereerd, is hello volgende metagegevens opgenomen in de nettolading van de webhook Hallo:</span><span class="sxs-lookup"><span data-stu-id="aef46-148">When hello autoscale notification is generated, hello following metadata is included in hello webhook payload:</span></span>

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' toocapacity '2'",
                "subscriptionId": "s1",
                "resourceGroupName": "rg1",
                "resourceName": "MyCSRole",
                "resourceType": "microsoft.classiccompute/domainnames/slots/roles",
                "resourceId": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService/slots/Production/roles/MyCSRole",
                "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService",
                "oldCapacity": "3",
                "newCapacity": "2"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```


| <span data-ttu-id="aef46-149">Veld</span><span class="sxs-lookup"><span data-stu-id="aef46-149">Field</span></span> | <span data-ttu-id="aef46-150">Verplichte?</span><span class="sxs-lookup"><span data-stu-id="aef46-150">Mandatory?</span></span> | <span data-ttu-id="aef46-151">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="aef46-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="aef46-152">status</span><span class="sxs-lookup"><span data-stu-id="aef46-152">status</span></span> |<span data-ttu-id="aef46-153">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-153">yes</span></span> |<span data-ttu-id="aef46-154">Hallo-status die aangeeft dat een actie voor automatisch schalen die is gegenereerd</span><span class="sxs-lookup"><span data-stu-id="aef46-154">hello status that indicates that an autoscale action was generated</span></span> |
| <span data-ttu-id="aef46-155">bewerking</span><span class="sxs-lookup"><span data-stu-id="aef46-155">operation</span></span> |<span data-ttu-id="aef46-156">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-156">yes</span></span> |<span data-ttu-id="aef46-157">Voor een verhoging van exemplaren zal moeten 'Scale Out' en voor een afname in exemplaren, deze 'Schaal In'</span><span class="sxs-lookup"><span data-stu-id="aef46-157">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span></span> |
| <span data-ttu-id="aef46-158">Context</span><span class="sxs-lookup"><span data-stu-id="aef46-158">context</span></span> |<span data-ttu-id="aef46-159">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-159">yes</span></span> |<span data-ttu-id="aef46-160">Hallo automatisch schalen actie context</span><span class="sxs-lookup"><span data-stu-id="aef46-160">hello autoscale action context</span></span> |
| <span data-ttu-id="aef46-161">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="aef46-161">timestamp</span></span> |<span data-ttu-id="aef46-162">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-162">yes</span></span> |<span data-ttu-id="aef46-163">Tijdstempel wanneer Hallo automatisch schalen actie is geactiveerd</span><span class="sxs-lookup"><span data-stu-id="aef46-163">Time stamp when hello autoscale action was triggered</span></span> |
| <span data-ttu-id="aef46-164">id</span><span class="sxs-lookup"><span data-stu-id="aef46-164">id</span></span> |<span data-ttu-id="aef46-165">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-165">Yes</span></span> |<span data-ttu-id="aef46-166">Bronnenbeheerder-ID van het Hallo-instelling voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="aef46-166">Resource Manager ID of hello autoscale setting</span></span> |
| <span data-ttu-id="aef46-167">naam</span><span class="sxs-lookup"><span data-stu-id="aef46-167">name</span></span> |<span data-ttu-id="aef46-168">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-168">Yes</span></span> |<span data-ttu-id="aef46-169">Hallo-naam van het Hallo-instelling voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="aef46-169">hello name of hello autoscale setting</span></span> |
| <span data-ttu-id="aef46-170">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="aef46-170">details</span></span> |<span data-ttu-id="aef46-171">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-171">Yes</span></span> |<span data-ttu-id="aef46-172">Uitleg van Hallo-actie die automatisch schalen service Hallo heeft ondernomen en Hallo in Hallo-exemplaren wijzigen</span><span class="sxs-lookup"><span data-stu-id="aef46-172">Explanation of hello action that hello autoscale service took and hello change in hello instance count</span></span> |
| <span data-ttu-id="aef46-173">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="aef46-173">subscriptionId</span></span> |<span data-ttu-id="aef46-174">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-174">Yes</span></span> |<span data-ttu-id="aef46-175">Abonnement-ID van de doelbron Hallo die wordt geschaald</span><span class="sxs-lookup"><span data-stu-id="aef46-175">Subscription ID of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="aef46-176">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="aef46-176">resourceGroupName</span></span> |<span data-ttu-id="aef46-177">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-177">Yes</span></span> |<span data-ttu-id="aef46-178">Naam van de resourcegroep van Hallo doelresource die wordt geschaald</span><span class="sxs-lookup"><span data-stu-id="aef46-178">Resource Group name of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="aef46-179">resourceName</span><span class="sxs-lookup"><span data-stu-id="aef46-179">resourceName</span></span> |<span data-ttu-id="aef46-180">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-180">Yes</span></span> |<span data-ttu-id="aef46-181">Naam van de doelbron Hallo die wordt geschaald</span><span class="sxs-lookup"><span data-stu-id="aef46-181">Name of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="aef46-182">resourceType</span><span class="sxs-lookup"><span data-stu-id="aef46-182">resourceType</span></span> |<span data-ttu-id="aef46-183">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-183">Yes</span></span> |<span data-ttu-id="aef46-184">Hallo drie ondersteunde waarden: 'microsoft.classiccompute/domainnames/slots/roles' - functies, 'microsoft.compute/virtualmachinescalesets' - virtuele Machine-Schaalsets, en 'Microsoft.Web/serverfarms' - Web-App Service in de Cloud</span><span class="sxs-lookup"><span data-stu-id="aef46-184">hello three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span></span> |
| <span data-ttu-id="aef46-185">resourceId</span><span class="sxs-lookup"><span data-stu-id="aef46-185">resourceId</span></span> |<span data-ttu-id="aef46-186">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-186">Yes</span></span> |<span data-ttu-id="aef46-187">Bronnenbeheerder-ID van Hallo doelresource die wordt geschaald</span><span class="sxs-lookup"><span data-stu-id="aef46-187">Resource Manager ID of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="aef46-188">portalLink</span><span class="sxs-lookup"><span data-stu-id="aef46-188">portalLink</span></span> |<span data-ttu-id="aef46-189">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-189">Yes</span></span> |<span data-ttu-id="aef46-190">Azure portal-koppeling toohello overzichtspagina van Hallo doelbron</span><span class="sxs-lookup"><span data-stu-id="aef46-190">Azure portal link toohello summary page of hello target resource</span></span> |
| <span data-ttu-id="aef46-191">oldCapacity</span><span class="sxs-lookup"><span data-stu-id="aef46-191">oldCapacity</span></span> |<span data-ttu-id="aef46-192">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-192">Yes</span></span> |<span data-ttu-id="aef46-193">Hallo huidige (oude) aantal exemplaren wanneer automatisch schalen een schaalactie heeft</span><span class="sxs-lookup"><span data-stu-id="aef46-193">hello current (old) instance count when Autoscale took a scale action</span></span> |
| <span data-ttu-id="aef46-194">newCapacity</span><span class="sxs-lookup"><span data-stu-id="aef46-194">newCapacity</span></span> |<span data-ttu-id="aef46-195">Ja</span><span class="sxs-lookup"><span data-stu-id="aef46-195">Yes</span></span> |<span data-ttu-id="aef46-196">Hallo nieuwe aantal exemplaren dat automatisch schalen Hallo resource te geschaald</span><span class="sxs-lookup"><span data-stu-id="aef46-196">hello new instance count that Autoscale scaled hello resource too</span></span>|
| <span data-ttu-id="aef46-197">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="aef46-197">Properties</span></span> |<span data-ttu-id="aef46-198">Nee</span><span class="sxs-lookup"><span data-stu-id="aef46-198">No</span></span> |<span data-ttu-id="aef46-199">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="aef46-199">Optional.</span></span> <span data-ttu-id="aef46-200">Reeks < sleutel, waarde > paren (bijvoorbeeld woordenlijst < String, String >).</span><span class="sxs-lookup"><span data-stu-id="aef46-200">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span></span> <span data-ttu-id="aef46-201">Hallo eigenschappenveld is optioneel.</span><span class="sxs-lookup"><span data-stu-id="aef46-201">hello properties field is optional.</span></span> <span data-ttu-id="aef46-202">In een aangepaste gebruikersinterface of Logic app op basis van werkstroom, kunt u sleutels en waarden die kunnen worden doorgegeven met Hallo nettolading.</span><span class="sxs-lookup"><span data-stu-id="aef46-202">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using hello payload.</span></span> <span data-ttu-id="aef46-203">Aangepaste eigenschappen toopass toohello uitgaande webhook aanroep back andere manier is toouse hello webhook URI zelf (als queryparameters)</span><span class="sxs-lookup"><span data-stu-id="aef46-203">An alternate way toopass custom properties back toohello outgoing webhook call is toouse hello webhook URI itself (as query parameters)</span></span> |
