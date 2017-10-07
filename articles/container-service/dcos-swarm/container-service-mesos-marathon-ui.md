---
title: aaaManage Azure DC/OS-cluster met Marathon-gebruikersinterface | Microsoft Docs
description: Containers tooan Azure Container Service-cluster-service implementeren met behulp van Hallo webgebruikersinterface van Marathon.
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: a90180e1b4763e6d2ddfa699ed4b7269f209f728
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-hello-marathon-web-ui"></a>Een Azure Container Service DC/OS-cluster via Hallo webgebruikersinterface van Marathon beheren
DC/OS biedt een omgeving voor het implementeren en schalen van geclusterde werkbelastingen terwijl het Hallo onderliggende hardware wordt onttrokken. Op de DC/OS ligt een framework dat de planning en uitvoering van rekenworkloads regelt.

Terwijl frameworks er beschikbaar zijn voor veel populaire werkbelastingen, wordt in dit document beschrijft hoe tooget gestart voor het implementeren van containers met Marathon. 


## <a name="prerequisites"></a>Vereisten
Voer het uitvoeren van deze voorbeelden hebt u een DC/OS-cluster nodig dat is geconfigureerd in Azure Container Service. U moet ook toohave externe connectiviteit toothis cluster. Zie voor meer informatie over deze items Hallo artikelen te volgen:

* [Een Azure Container Service-cluster implementeren](container-service-deployment.md)
* [Verbinding maken met tooan Azure Container Service-cluster](../container-service-connect.md)

> [!NOTE]
> In dit artikel wordt ervan uitgegaan dat u toohello DC/OS-cluster via tunneling via uw lokale poort 80.
>

## <a name="explore-hello-dcos-ui"></a>Hallo DC/OS-gebruikersinterface verkennen
Met een tunnel Secure Shell (SSH) [tot stand gebracht](../container-service-connect.md), toohttp://localhost/ bladeren. Dit wordt Hallo DC/OS-webgebruikersinterface geladen en informatie over het Hallo-cluster, zoals gebruikte resources, actieve agents en actieve services.

![DC/OS-webgebruikersinterface](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-hello-marathon-ui"></a>Hallo Marathon-gebruikersinterface verkennen
toosee hello Marathon-gebruikersinterface toohttp://localhost/marathon bladeren. In dit scherm kunt u een nieuwe container of een andere toepassing starten op Hallo Azure Container Service DC/OS-cluster. U ziet ook informatie over actieve containers en toepassingen.  

![Marathon-gebruikersinterface](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a>Een met Docker ingedeelde container implementeren
toodeploy een nieuwe container via Marathon, klikt u op **toepassing maken**, en voer de volgende informatie in Hallo formuliertabbladen Hallo:

| Veld | Waarde |
| --- | --- |
| Id |nginx |
| Geheugen | 32 |
| Installatiekopie |nginx |
| Netwerk |Overbrugd |
| Hostpoort |80 |
| Protocol |TCP |

![Nieuwe toepassingsgebruikersinterface: algemeen](./media/container-service-mesos-marathon-ui/dcos4.png)

![Nieuwe toepassingsgebruikersinterface: Docker-container](./media/container-service-mesos-marathon-ui/dcos5.png)

![Nieuwe toepassingsgebruikersinterface: poort- en servicedetectie](./media/container-service-mesos-marathon-ui/dcos6.png)

Als u wilt dat toostatically kaart Hallo container poort tooa poort op Hallo-agent, moet u toouse JSON-modus. Ja, schakelt de wizard nieuwe toepassing hello te toodo**JSON-modus** met behulp van Hallo in-of uitschakelen. Voer vervolgens de volgende instelling onder Hallo Hallo `portMappings` sectie van de definitie van de toepassing hello. In het volgende voorbeeld wordt poort 80 van Hallo container tooport 80 Hallo DC/OS-agent. Nadat u deze wijziging hebt aangebracht, kunt u deze wizard uit JSON-modus halen.

```none
"hostPort": 80,
```

![Nieuwe toepassingsgebruikersinterface: voorbeeld van poort 80](./media/container-service-mesos-marathon-ui/dcos13.png)

Als u tooenable statuscontroles wilt, stelt u een pad op Hallo **Health controleert** tabblad.

![Nieuwe toepassingsgebruikersinterface: statuscontroles](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

Hallo DC/OS-cluster wordt geïmplementeerd met set persoonlijke en openbare agents. Hallo cluster toobe kunnen tooaccess toepassingen van Hallo Internet moet u toodeploy Hallo toepassingen tooa openbare agent. toodo Selecteer daarom Hallo **optioneel** tabblad van de wizard nieuwe toepassing hello en voer **slave_public** voor Hallo **geaccepteerde resourcerollen**.

Klik vervolgens op **Toepassing maken**.

![Nieuwe toepassingsgebruikersinterface: instellingen openbare agent](./media/container-service-mesos-marathon-ui/dcos14.png)

Terug op Hallo hoofdpagina van Marathon ziet u Hallo Implementatiestatus voor Hallo-container. Eerst wordt de status **Implementeren** weergegeven. Na een geslaagde implementatie Hallo statuswijzigingen te**met**.

![Hoofdpagina van Marathon: implementatiestatus van container](./media/container-service-mesos-marathon-ui/dcos7.png)

Wanneer u overschakelt back toohello DC/OS-webgebruikersinterface (http://localhost/), ziet u dat een taak (in dit geval een met Docker ingedeelde container) wordt uitgevoerd op Hallo DC/OS-cluster.

![DC/OS-webgebruikersinterface: taak uitgevoerd op Hallo-cluster](./media/container-service-mesos-marathon-ui/dcos8.png)

toosee hello clusterknooppunt die taak Hallo op wordt uitgevoerd, klikt u op Hallo **knooppunten** tabblad.

![DC/OS-webgebruikersinterface: clusterknooppunt van taak](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-hello-container"></a>Hallo-container bereiken

In dit voorbeeld wordt Hallo toepassing uitgevoerd op een knooppunt openbare agent. U bereikt Hallo toepassing hello internet door te bladeren toohello agent FQDN-naam van de cluster Hallo: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, waarbij:

* **DNSPREFIX** Hallo DNS-voorvoegsel op dat u hebt opgegeven tijdens de implementatie Hallo-cluster is.
* **REGIO** Hallo regio waarin uw resourcegroep zich bevindt.

    ![Nginx van Internet](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a>Volgende stappen
* [Werken met DC/OS en Marathon API Hallo](container-service-mesos-marathon-rest.md)

* Deep dive op Hallo Azure Container Service met Mesos

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
