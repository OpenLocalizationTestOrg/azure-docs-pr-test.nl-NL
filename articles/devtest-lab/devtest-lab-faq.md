---
title: aaaAzure Veelgestelde vragen over het DevTest Labs | Microsoft Docs
description: Hieronder vindt u antwoorden op vragen over Azure DevTest Labs van toocommon
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: afe83109-b89f-4f18-bddd-b8b4a30f11b4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: tarcher
ms.openlocfilehash: 07d4c870eca21856750a472ed503de4a2734a438
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-devtest-labs-faq"></a>Veelgestelde vragen over Azure DevTest Labs
In dit artikel worden enkele veelgestelde vragen over Azure DevTest Labs Hallo beantwoord.

**Algemeen**
## <a name="what-if-my-question-isnt-answered-here"></a>Wat gebeurt er als mijn vraag hier niet wordt beantwoord?
Als uw vraag hier niet wordt weergegeven, laat ons weten zodat je kunt een antwoord vinden.

* Stel een vraag in Hallo [Disqus-thread](#comments) aan Hallo einde van deze Veelgestelde vragen en benaderen hello Azure Cache-team en andere communityleden over dit artikel.
* een breder publiek tooreach een vraag plaatsen op Hallo [Azure DevTest Labs van MSDN-forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureDevTestLabs), en hello Azure DevTest Labs team en andere leden van de community Hallo benaderen.
* toomake een functie-aanvraag indienen uw aanvragen en ideeën toohello [Azure DevTest Labs User Voice](https://feedback.azure.com/forums/320373-azure-devtest-labs).

## <a name="why-should-i-use-azure-devtest-labs"></a>Waarom moet ik Azure DevTest Labs gebruiken?
Azure DevTest Labs uw team tijd en geld bespaart. Ontwikkelaars kunnen hun eigen omgevingen met behulp van verschillende andere databases maken en gebruik van artefacten tooquickly implementeren en configureren van toepassingen. Met behulp van aangepaste installatiekopieën en formules, worden virtuele machines opgeslagen als de sjablonen en eenvoudig kunnen reproduceren. Bovendien bieden labs verschillende configureerbare beleidsregels waarmee beheerders lab tooreduce afval en een team omgevingen beheren. Deze beleidsregels bevatten automatisch afsluiten, kosten drempelwaarde, maximum aantal virtuele machines per gebruiker en de maximale grootte van de virtuele machine. Lees voor een uitgebreidere uitleg van Azure DevTest Labs Hallo [overzicht](devtest-lab-overview.md) of controle Hallo [Introductievideo](/documentation/videos/videos/what-is-azure-devtest-labs).

## <a name="what-does-worry-free-self-service-mean"></a>Wat houdt 'probleemloos, self-service'?
'Probleemloos, self-service' betekent dat ontwikkelaars en testers hun eigen omgevingen maken indien nodig, en beheerders Hallo beveiliging van weten dat Azure DevTest Labs helpt te beperken afval en beheerkosten hebben. Beheerders kunnen opgeven welke VM-grootten zijn toegestaan, Hallo kunt u het maximum aantal virtuele machines, en wanneer de virtuele machines worden gestart en afgesloten. Azure DevTest Labs ook kunt u eenvoudig toomonitor kosten en set waarschuwingen toostay weten hoe resources in de testomgeving hello worden gebruikt.

## <a name="how-can-i-use-azure-devtest-labs"></a>Hoe kan ik Azure DevTest Labs gebruiken?
Azure DevTest Labs is nuttig wanneer u dev vereisen of testomgeving, en u tooreproduce wilt ze snel en/of ze beheren met beleid voor kostenbesparende.

Hier volgen enkele scenario's die gebruikmaken van onze klanten Azure DevTest Labs voor:

* Ontwikkel- en testomgevingen op één plaats beheert, bouwt met behulp van beleid tooreduce kosten en aangepaste installatiekopieën tooshare in Hallo-team.
* Een toepassing met behulp van aangepaste installatiekopieën toosave Hallo schijf staat gedurende Hallo ontwikkeling fasen ontwikkelen.
* Hallo-kosten in relatie tooprogress bijhouden.
* Maken van massaopslag testomgevingen voor kwaliteit zekerheid te testen.
* Met behulp van artefacten en formules tooeasily configureren en een toepassing in verschillende omgevingen reproduceren.
* Distributie van virtuele machines voor hackathons (ontwikkeling of tests samenwerkingsmogelijkheden), en vervolgens gemakkelijk ongedaan inrichting ze wanneer Hallo gebeurtenis eindigt.

## <a name="how-am-i-billed-for-azure-devtest-labs"></a>Hoe ben ik Azure DevTest Labs gefactureerd?
Azure DevTest Labs is een gratis service, wat betekent dat labs maken en configureren van beleidsregels hello, sjablonen en artefacten vrij is. U betaalt alleen voor hello Azure-resources binnen uw labs, zoals virtuele machines, opslagaccounts en virtuele netwerken gebruikt. Voor meer informatie over Hallo kosten van lab resources meer informatie over [prijzen van Azure DevTest Labs](https://azure.microsoft.com/pricing/details/devtest-lab/).


**Beveiliging**
## <a name="what-are-hello-different-security-levels-in-azure-devtest-labs"></a>Wat zijn de verschillende beveiligingsniveaus Hallo in Azure DevTest Labs?
Beveiligingstoegang wordt bepaald door [gebaseerd toegangsbeheer (RBAC)](../active-directory/role-based-access-built-in-roles.md). toounderstand access hoe werkt, het helpt toounderstand Hallo verschillen tussen een machtiging voor een rol en een bereik, zoals gedefinieerd door RBAC.

* **Machtiging** -een machtiging is een gedefinieerde toegang tooa specifieke actie. Een machtiging kan bijvoorbeeld leestoegang tooall virtuele machines.
* **Rol** -een rol is een reeks machtigingen die kunnen worden gegroepeerd en tooa gebruiker toegewezen. Zo heeft een 'abonnement eigenaar' toegang tot tooall bronnen binnen een abonnement.
* **Bereik** -een scope is een niveau binnen de hiërarchie Hallo van Azure-resource. Een scope kan bijvoorbeeld een resourcegroep of een enkele gehele lab of Hallo-abonnement.

Binnen het bereik van de Hallo van Azure DevTest Labs, er zijn twee typen rollen toodefine gebruikersmachtigingen: labeigenaar en lab-gebruiker.

* **Labeigenaar** -labeigenaar van een Hallo toegang tooany resources binnen Hallo lab heeft. Daarom kunnen ze beleid wijzigen, lezen en schrijven van alle virtuele machines, Hallo virtueel netwerk wijzigen, enzovoort.
* **Lab-gebruiker** : een lab-gebruiker alle lab-resources, zoals virtuele machines, beleid en virtuele netwerken kunt bekijken maar niet worden gewijzigd beleid of alle virtuele machines gemaakt door andere gebruikers. Het is ook mogelijk toocreate aangepaste rollen in Azure DevTest Labs en leert u hoe toodo in Hallo artikel [gebruikersmachtigingen verlenen toospecific labbeleidsregels](devtest-lab-grant-user-permissions-to-specific-lab-policies.md).

Aangezien scopes hiërarchische, wanneer een gebruiker machtigingen op een bepaalde scope heeft, krijgen ze automatisch deze machtigingen voor elke laag niveau scope die zijn opgenomen. Bijvoorbeeld, als een gebruiker is toegewezen toohello rol van eigenaar abonnement, hebben vervolgens ze toegang tot tooall bronnen in een abonnement. Deze bronnen omvatten alle virtuele machines, alle virtuele netwerken en alle labs. De eigenaar van een abonnement neemt dus automatisch Hallo-rol van de labeigenaar van het. Hallo tegengestelde is echter niet het geval. Een labeigenaar heeft toegang tooa lab, een lagere bereik dan Hallo-abonnement is. De labeigenaar van een is daarom niet kunnen toosee virtuele machines of virtuele netwerken of alle bronnen die zich buiten het Hallo-testomgeving.

## <a name="how-do-i-create-a-role-tooallow-users-tooperform-a-specific-task"></a>Hoe maak ik een tooperform rol tooallow gebruikers een specifieke taak?
Een uitgebreide artikel over hoe toocreate aangepaste rollen en toewijzen machtigingen toothat rol u hier vindt. Hier volgt een voorbeeld van een script waarmee Hallo rol 'DevTest Labs geavanceerde gebruiker', dat is gemachtigd toostart en stoppen alle virtuele machines in de testomgeving Hallo maakt:

    $policyRoleDef = Get-AzureRmRoleDefinition "DevTest Labs User"
    $policyRoleDef.Actions.Remove('Microsoft.DevTestLab/Environments/*')
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "DevTest Labs Advance User"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("subscriptions/<subscription Id>")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/virtualMachines/Start/action")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/virtualMachines/Stop/action")
    $policyRoleDef = New-AzureRmRoleDefinition -Role $policyRoleDef  


**CI/CD-integratie en automatisering**
## <a name="does-azure-devtest-labs-integrate-with-my-cicd-toolchain"></a>Azure DevTest Labs integreren in mijn toolchain CI/CD?
Als u VSTS gebruikt, is er een [Azure DevTest Labs taken extensie](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks) waarmee u uw release pijplijn in Azure DevTest Labs tooautomate. Hallo maakt gebruik van deze extensie onder andere:

* Maken en implementeren van een virtuele machine automatisch en met de laatste build Hallo met behulp van Azure bestand kopiëren of PowerShell VSTS taken te configureren.
* Hallo-status van een virtuele machine automatisch vast te leggen na een bug tooreproduce testen op dezelfde virtuele machine voor verder onderzoek Hallo.
* Verwijderen van Hallo VM achter Hallo Hallo pijplijn vrijgeven wanneer deze niet langer nodig is.

Hallo bieden volgende blogberichten richtlijnen en informatie over het gebruik van Hallo VSTS extensie:

* [Azure DevTest Labs – VSTS extensie](https://blogs.msdn.microsoft.com/devtestlab/2016/06/15/azure-devtest-labs-vsts-extension/)
* [Een nieuwe virtuele machine in een bestaande AzureDevTestLab van VSTS implementeren](http://www.visualstudiogeeks.com/blog/DevOps/Deploy-New-VM-To-Existing-AzureDevTestLab-From-VSTS)
* [VSTS Release Management gebruiken voor implementaties van continue tooAzureDevTestLabs](http://www.visualstudiogeeks.com/blog/DevOps/Use-VSTS-ReleaseManagement-to-Deploy-and-Test-in-AzureDevTestLabs)

Voor andere toolchains CI/CD alle Hallo genoemde scenario's die kunnen worden bereikt via Hallo VSTS taken extensie op dezelfde manier kan worden bereikt via implementeren [Azure Resource Manager-sjablonen](https://aka.ms/dtlquickstarttemplate) met [ Azure PowerShell-cmdlets](../azure-resource-manager/resource-group-template-deploy.md) en [.NET SDK's](https://www.nuget.org/packages/Microsoft.Azure.Management.DevTestLabs/). U kunt ook [REST-API's voor DevTest Labs](http://aka.ms/dtlrestapis) toointegrate met uw toolchain.  


**Virtuele machines**
## <a name="why-cant-i-see-certain-vms-in-hello-azure-virtual-machines-blade-that-i-see-within-azure-devtest-labs"></a>Waarom zie ik bepaalde virtuele machines in hello Azure Virtual Machines blade die ik Zie in Azure DevTest Labs kan niet?
Wanneer een virtuele machine wordt gemaakt in Azure DevTest Labs, de machtiging is gegeven tooaccess die VM. U kunt tooview worden deze in Hallo labs blade en Hallo **virtuele Machines** blade. Gebruikers in de rol van Hallo DevTest Labs kunnen zien alle virtuele machines die zijn gemaakt in de testomgeving Hallo via Hallo lab van **alle virtuele Machines** blade. Echter, in Hallo DevTest Labs rol automatisch krijgt geen leestoegang tooVM bronnen die anderen hebben gemaakt. Deze virtuele machines worden daarom niet weergegeven in Hallo **virtuele Machines** blade.

## <a name="what-is-hello-difference-between-custom-images-and-formulas"></a>Wat is Hallo verschil tussen aangepaste installatiekopieën en formules?
Een aangepaste installatiekopie is een VHD (virtuele harde schijf), terwijl een formule is een installatiekopie die u kunt configureren met extra instellingen die u kunt opslaan en reproduceren. Een aangepaste installatiekopie wellicht de voorkeur als u wilt dat tooquickly verschillende omgevingen maken met de Hallo dezelfde installatiekopie van een eenvoudige, niet-wijzigbaar. Een formule is mogelijk beter als u wilt dat tooreproduce Hallo configuratie van uw virtuele machine met de meest recente bits hello, een virtueel netwerksubnet of een specifieke grootte. Zie voor een uitgebreidere uitleg Hallo artikel [vergelijken van aangepaste installatiekopieën en formules in DevTest Labs](devtest-lab-comparing-vm-base-image-types.md).

## <a name="how-do-i-create-multiple-vms-from-hello-same-template-at-once"></a>Hoe kan ik meerdere virtuele machines maken uit Hallo in één keer dezelfde sjabloon?
U kunt Hallo [VSTS taken extensie](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks) of [genereren van een Azure Resource Manager-sjabloon](devtest-lab-add-vm.md#save-azure-resource-manager-template) tijdens het maken van een virtuele machine en [hello Azure Resource Manager sjabloon implementeren vanuit Windows PowerShell ](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="how-do-i-move-my-existing-azure-vms-into-my-azure-devtest-labs-lab"></a>Hoe kan ik mijn bestaande Azure VM's in mijn Azure DevTest Labs lab verplaatsen?
Volg onderstaande toocopy Hallo stappen uw bestaande virtuele machines tooAzure DevTest Labs:

1. Kopiëren Hallo VHD-bestand van uw bestaande virtuele machine gebruik van deze [Windows PowerShell-script](https://github.com/Azure/azure-devtestlab/blob/master/Scripts/CopyVHDFromVMToLab.ps1)
2. [Maken van aangepaste installatiekopie Hallo](devtest-lab-create-template.md) in uw testomgeving Azure DevTest Labs.
3. Een virtuele machine in de testomgeving Hallo van uw aangepaste installatiekopie maken

## <a name="can-i-attach-multiple-disks-toomy-vms"></a>Kan ik meerdere schijven toomy VMs koppelen?
Koppelen van meerdere schijven tooVMs wordt ondersteund.  

## <a name="if-i-want-toouse-a-windows-os-image-for-my-testing-do-i-have-toopurchase-an-msdn-subscription"></a>Als ik voor mijn testen toouse een installatiekopie van het Windows-besturingssysteem wilt gebruiken, heb ik toopurchase een MSDN-abonnement?
Als u toouse Windows-clientbesturingssysteem installatiekopieën (Windows 7 of hoger) voor de ontwikkeling of tests in Azure moet, vervolgens moet Ja, u een van:

- [Een MSDN-abonnement aanschaffen](https://www.visualstudio.com/products/how-to-buy-vs).
- Als u een Enterprise Agreement hebt, maakt u een Azure-abonnement met Hallo [Enterprise ontwikkelen en testen aanbieding](https://azure.microsoft.com/en-us/offers/ms-azr-0148p).

Zie voor meer informatie over hello Azure-krediet voor elke aanbieding MSDN [maandelijkse Azure-tegoed voor Visual Studio-abonnees](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/).

## <a name="how-do-i-automate-hello-process-of-uploading-vhd-files-toocreate-custom-images"></a>Hoe ik Hallo-proces van het VHD-bestanden toocreate aangepaste installatiekopieën uploaden automatiseren?
Er zijn twee opties:

* [Azure AzCopy](../storage/common/storage-use-azcopy.md#blob-upload) kan worden gebruikt toocopy of VHD-bestanden toohello storage-account gekoppeld Hallo lab uploaden.
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een zelfstandige app die wordt uitgevoerd op Windows, OSX en Linux.   

toofind hello doelopslagaccount die zijn gekoppeld aan uw testomgeving als volgt te werk:

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecteer **resourcegroepen** van het linkerpaneel Hallo.
3. Zoek en selecteer Hallo resourcegroep die zijn gekoppeld aan uw testomgeving.
4. Op Hallo **overzicht** blade, selecteert u een van de Hallo storage-accounts.
5. Selecteer **Blobs**.
6. Zoek naar uploads in Hallo-lijst. Als er nog geen bestaat, tooStep #4 retourneren en probeer een ander opslagaccount.
7. Gebruik Hallo **URL** als de bestemming in de AzCopy-opdracht.

## <a name="how-can-i-automate-hello-process-of-deleting-all-hello-vms-in-my-lab"></a>Hoe kan ik Hallo proces van het verwijderen van alle Hallo VM's in mijn lab automatiseren?
Bovendien toodeleting virtuele machines uit uw lab in hello Azure-portal, kunt u verwijderen alle Hallo VM's in uw testomgeving met een PowerShell-script. In Hallo Hallo parameterwaarden onder Hallo volgende voorbeeld wijzigt **waarden toochange** opmerking. U kunt ophalen Hallo `subscriptionId`, `labResourceGroup`, en `labName` waarden uit de labblade Hallo in hello Azure-portal.

    # Delete all hello VMs in a lab

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource group here>"
    $labName = "<Enter lab name here>"

    # Login tooyour Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. This step is optional
    # if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Get hello lab that contains hello VMs toodelete.
    $lab = Get-AzureRmResource -ResourceId ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)

    # Get hello VMs from that lab.
    $labVMs = Get-AzureRmResource | Where-Object {
              $_.ResourceType -eq 'microsoft.devtestlab/labs/virtualmachines' -and
              $_.ResourceName -like "$($lab.ResourceName)/*"}

    # Delete hello VMs.
    foreach($labVM in $labVMs)
    {
        Remove-AzureRmResource -ResourceId $labVM.ResourceId -Force
    }

**Artefacten**
## <a name="what-are-artifacts"></a>Wat zijn artefacten?
Artefacten zijn aanpasbare elementen die kunnen worden gebruikt toodeploy uw meest recente bits of uw Developer tools op een virtuele machine. Ze zijn aangesloten tooyour VM tijdens het maken van een paar eenvoudige klikken en eenmaal Hallo VM is ingericht, Hallo artefacten implementeren en configureren van uw virtuele machine. Er zijn verschillende vooraf bestaande artefacten in onze [openbare GitHub-opslagplaats](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts), maar u kunt ook eenvoudig [ontwerpen van uw eigen artefacten](devtest-lab-artifact-author.md).


**Configuratie van het testlab**
## <a name="how-do-i-create-a-lab-from-an-azure-resource-manager-template"></a>Hoe maak ik een testomgeving met een Azure Resource Manager-sjabloon
We hebt opgegeven een [GitHub-opslagplaats met Azure Resource Manager-sjablonen lab](https://aka.ms/dtlquickstarttemplate) die u kunt implementeren als-is of aangepaste sjablonen voor uw labs toocreate wijzigen. Elk van deze sjablonen heeft een koppeling die u kunt klikken op toodeploy Hallo lab als-is onder uw eigen Azure-abonnement of u kunt Hallo sjabloon aanpassen en [implementeren met behulp van PowerShell of Azure CLI](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="why-are-my-vms-created-in-different-resource-groups-with-arbitrary-names-can-i-rename-or-modify-these-resource-groups"></a>Waarom wordt mijn VM's in verschillende resourcegroepen met willekeurige namen gemaakt? Kan ik wijzigen of deze brongroepen wijzigen?
Resourcegroepen zijn op deze manier gemaakt om Azure DevTest Labs toomanage Hallo gebruikersmachtigingen en toegang toovirtual machines. Terwijl u Hallo VM tooanother resourcegroep met de naam van uw gewenste verplaatsen kunt, wordt doen dit niet aanbevolen. We werken op het verbeteren van deze ervaring tooallow meer flexibiliteit.   

## <a name="how-many-labs-can-i-create-under-hello-same-subscription"></a>Hoeveel labs kan ik maken onder Hallo hetzelfde abonnement?
Er is geen specifieke limiet van Hallo aantal labs dat per abonnement kan worden gemaakt. Hallo-resources die worden gebruikt, zijn echter beperkt per abonnement. U kunt meer informatie over Hallo [limieten en quota's die zijn opgelegd voor het Azure-abonnementen](../azure-subscription-service-limits.md) en [hoe tooincrease deze limieten](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests).

## <a name="how-many-vms-can-i-create-per-lab"></a>Hoeveel virtuele machines kan ik per lab maken?
Er is geen specifieke limiet op Hallo aantal virtuele machines die per lab kunnen worden gemaakt. Hallo-resources die worden gebruikt zijn echter beperkt per abonnement (bijvoorbeeld VM kernen, openbare IP-adressen, enz.). U kunt meer informatie over Hallo [limieten en quota's die zijn opgelegd voor het Azure-abonnementen](../azure-subscription-service-limits.md) en [hoe tooincrease deze limieten](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests).

## <a name="how-do-i-share-a-direct-link-toomy-lab"></a>Hoe kan ik een directe koppeling toomy lab delen
een directe koppeling tooshare tooyour lab gebruikers, kunt u Hallo na procedure uitvoeren:

1. Blader toohello lab in hello Azure-portal.
2. Hallo lab-URL van uw browser kopiëren en delen met uw lab-gebruikers.

> [!NOTE]
> Als uw gebruikers lab externe gebruikers met zijn een [Microsoft-account](#what-is-a-microsoft-account) en ze niet deel uit van de Active directory van het bedrijf tooyour, krijgen ze mogelijk een fout opgetreden tijdens het navigeren toohello opgegeven koppeling. Als ze een foutbericht ontvangt, moeten ze hun naam in Hallo rechterbovenhoek van de Azure portal en selecteer Hallo directory waar Hallo lab uit Hallo bestaat Hallo tooclick **Directory** gedeelte van Hallo-menu.
>
>

## <a name="what-is-a-microsoft-account"></a>Wat is een Microsoft-account?
Een Microsoft-account wordt gebruikt voor bijna alles wat die u met Microsoft-apparaten en services doet. Het is e-mailadres en wachtwoord dat u toosign in tooSkype, Outlook.com, OneDrive, Windows Phone en Xbox LIVE – betekent dit uw bestanden, foto's, contactpersonen dat en instellingen u tooany apparaat volgen kunnen.

> [!NOTE]
> Microsoft-account gebruikt toobe 'Windows Live ID' genoemd.
>
>


**Problemen oplossen**
## <a name="my-artifact-failed-during-vm-creation-how-do-i-troubleshoot-it"></a>Mijn artefact is mislukt tijdens het maken van VM. Hoe kan ik oplossen?
Raadpleeg te[hoe toodiagnose artefact fouten in DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md) toolearn hoe tooobtain met betrekking tot uw mislukte artefacten registreert.

## <a name="why-isnt-my-existing-virtual-network-saving-properly"></a>Waarom wordt niet mijn bestaande virtuele netwerk juist opslaan?
Een kans is dat de naam van uw virtuele netwerk punten bevat. Als u dus verwijder Hallo punten of afbreekstreepjes vervangen en probeer het vervolgens Hallo opslaan opnieuw virtueel netwerk.

## <a name="why-do-i-get-a-parent-resource-not-found-error-when-provisioning-a-vm-from-powershell"></a>Waarom krijg ik een 'Bovenliggende bron is niet gevonden'-Fout bij het inrichten van een virtuele machine vanuit PowerShell?
Wanneer een bron een bovenliggende tooanother resource is, moet Hallo bovenliggende resource bestaan voordat u Hallo onderliggende resource maakt. Als deze niet bestaat, ontvangt u een **ParentResourceNotFound** fout. Als u een afhankelijkheid op Hallo bovenliggende resource niet opgeeft, mogelijk Hallo onderliggende resource worden geïmplementeerd voordat Hallo bovenliggende.

Virtuele machines zijn onderliggende resources onder een lab in een resourcegroep. Wanneer u Azure Resource Manager-sjablonen toodeploy via PowerShell gebruikt, moet Hallo Resourcegroepnaam opgegeven in de PowerShell-script Hallo Hallo Resourcegroepnaam Hallo Lab. Zie voor meer informatie [veelvoorkomende fouten van de Azure-implementatie oplossen ](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-common-deployment-errors#parentresourcenotfound).

## <a name="where-can-i-find-more-error-information-if-a-vm-deployment-fails"></a>Waar vind ik meer foutinformatie als de implementatie van een virtuele machine mislukt?
VM-implementatiefouten worden vastgelegd in Hallo activiteitenlogboeken. U vindt lab activiteitenlogboeken VM's via Hallo **controlelogboeken** of **diagnostische gegevens van virtuele machine** Hallo resource menu Hallo lab van VM-blade (Hallo blade wordt weergegeven nadat u hebt geselecteerd Hallo VM van **Mijn virtuele machines** lijst).

Soms Hallo implementatiefout deze gebeurtenis treedt op voordat Hallo VM-implementatie wordt gestart - zoals wanneer de limiet voor het abonnement voor een resource die is gemaakt met de Hallo VM Hallo is overschreden. In dit geval Hallo foutdetails zijn vastgelegd in Hallo lab niveau **activiteitenlogboeken** die kunnen worden zoeken aan de onderkant Hallo Hallo **configuratie en het beleid** instellingen. Zie voor meer informatie over het gebruik van de activiteit geregistreerd in Azure, [weergave activiteit registreert tooaudit bewerkingen op bronnen](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-audit).

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]
