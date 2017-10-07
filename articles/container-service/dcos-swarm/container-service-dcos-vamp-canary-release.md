---
title: aaaCanary release met Vamp op Azure DC/OS-cluster | Microsoft Docs
description: Hoe toouse Vamp toocanary release services en slimme verkeer filteren op een Azure Container Service DC/OS-cluster toe te passen
services: container-service
author: gggina
manager: rasquill
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/17/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: e7b8658a161a7cddcf718e3e1c12a889a330d3d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a>Kokospalm release microservices met Vamp in een Azure Container Service DC/OS-cluster

In dit scenario stelt Vamp op Azure Container Service met een DC/OS-cluster. We kokospalm hello Vamp demoservice 'sava' release en vervolgens incompatibiliteit van Hallo-service met Firefox oplossen door toe te passen smart verkeer gefilterd. 

> [!TIP] 
> In dit overzicht Vamp wordt uitgevoerd op een DC/OS-cluster, maar u kunt ook Vamp met Kubernetes gebruiken als Hallo orchestrator.
>

## <a name="about-canary-releases-and-vamp"></a>Over Canarische vrijgegeven en Vamp


[Vrijgeven van kokospalm](https://martinfowler.com/bliki/CanaryRelease.html) is een strategie voor slimme implementatie door innovatieve organisaties zoals Netflix, Facebook en Spotify vastgesteld. Het is een benadering die logisch, klinkt omdat deze problemen vermindert veiligheid netten introduceert en verhoogt de vernieuwing. Waarom worden niet alle bedrijven met behulp van deze? Uitbreiden van een pijplijn CI/CD tooinclude kokospalm strategieën voegt complexiteit en uitgebreide devops kennis en ervaring vereist. Dat is voldoende tooblock kleinere bedrijfs- en ondernemingsbeheer zowel voordat ze ook aan de slag. 

[Vamp](http://vamp.io/) een open source-systeem tooease deze overgang is en kokospalm geven functies tooyour voorkeur container scheduler te brengen. De vamp kokospalm functionaliteit zich verder uitstrekt dan implementaties op basis van een percentage. Verkeer kan worden gefilterd en splitst bij een breed scala aan de voorwaarden, bijvoorbeeld tootarget specifieke gebruikers, IP-adresbereiken of apparaten. Vamp houdt en maatstaven voor prestaties, zodat voor automatisering op basis van echte gegevens analyseert. U kunt instellen op automatisch herstel op fouten of afzonderlijke service varianten op basis van load of latentie schalen.

## <a name="set-up-azure-container-service-with-dcos"></a>Azure Container Service met DC/OS instellen



1. [Een DC/OS-cluster implementeren](container-service-deployment.md) met één master en twee agents van standaardgrootte. 

2. [Maken van een SSH-tunnel](../container-service-connect.md) tooconnect toohello DC/OS-cluster. In dit artikel wordt ervan uitgegaan dat u een tunnel toohello cluster op de lokale poort 80.


## <a name="set-up-vamp"></a>Vamp instellen

Nu dat u een actieve DC/OS-cluster hebt, kunt u Vamp installeren vanaf Hallo DC/OS-Webgebruikersinterface (http://localhost:80). 

![DC/OS-webgebruikersinterface](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

De installatie wordt uitgevoerd in twee fasen:

1. **Implementeer Elasticsearch**.

2. Vervolgens **Vamp implementeren** door Hallo Vamp DC/OS universe pakket installeert.

### <a name="deploy-elasticsearch"></a>Elasticsearch implementeren

Elasticsearch vereist vamp voor het verzamelen van de metrische gegevens en aggregatie. U kunt Hallo [magneticio Docker installatiekopieën](https://hub.docker.com/r/magneticio/elastic/) toodeploy een compatibel Vamp Elasticsearch-stack.

1. Ga te in Hallo DC/OS-Webgebruikersinterface,**Services** en klik op **Service implementeren**.

2. Selecteer **JSON-modus** van Hallo **nieuwe Service implementeren** pop-upvenster.

  ![Selecteer JSON-modus](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. In de volgende JSON hello te plakken. Deze configuratie wordt uitgevoerd Hallo-container met 1 GB RAM-geheugen en een eenvoudige statuscontrole op Hallo Elasticsearch poort.
  
  ```JSON
  {
    "id": "elasticsearch",
    "instances": 1,
    "cpus": 0.2,
    "mem": 1024.0,
    "container": {
      "docker": {
        "image": "magneticio/elastic:2.2",
        "network": "HOST",
        "forcePullImage": true
      }
    },
    "healthChecks": [
      {
        "protocol": "TCP",
        "gracePeriodSeconds": 30,
        "intervalSeconds": 10,
        "timeoutSeconds": 5,
        "port": 9200,
        "maxConsecutiveFailures": 0
      }
    ]
  }
  ```
  

3. Klik op **implementeren**.

  DC/OS implementeert Hallo Elasticsearch container. U kunt de voortgang volgen op Hallo **Services** pagina.  

  ![e implementeren? Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a>Vamp implementeren

Zodra Elasticsearch als rapporteert **met**, kunt u Hallo Vamp DC/OS Universe pakket toevoegen. 

1. Ga te**Universe** en zoek naar **vamp**. 
  ![Vamp op DC/OS universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)

2. Klik op **installeren** volgende toohello vamp pakket en kies **installatie in de geavanceerde**.

3. Schuif naar beneden en Voer Hallo elasticsearch-url te volgen: `http://elasticsearch.marathon.mesos:9200`. 

  ![Voer de URL Elasticsearch](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. Klik op **Bekijk en installeer**, klikt u vervolgens op **installeren** toostart Hallo-implementatie.  

  DC/OS implementeert alle vereiste Vamp onderdelen. U kunt de voortgang volgen op Hallo **Services** pagina.
  
  ![Vamp als universe pakket implementeren](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. Zodra de implementatie is voltooid, kunt u toegang tot Hallo Vamp gebruikersinterface:

  ![-Service op de DC/OS vamp](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Vamp gebruikersinterface](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a>Uw eerste service implementeren

Nu dat Vamp actief en werkend is, een service implementeren vanuit een blauwdruk. 

In de meest eenvoudige vorm een [Vamp blauwdruk](http://vamp.io/documentation/using-vamp/blueprints/) Hallo eindpunten (gateways), clusters en services toodeploy beschrijft. Vamp maakt gebruik van clusters toogroup verschillende varianten van Hallo dezelfde service in logische groepen voor kokospalm vrijgeven of A / B-tests.  

Dit scenario wordt gebruikt voor een voorbeeldtoepassing monolithische aangeroepen [ **sava**](https://github.com/magneticio/sava), die is op versie 1.0. Hallo monoliet wordt verpakt in een Docker-container in Docker-Hub onder de magneticio/sava:1.0.0 ligt. Hallo-app wordt normaal uitgevoerd op poort 8080, maar u wilt dat tooexpose in 9050 in dit geval poort. Hallo-app via Vamp met behulp van een eenvoudige blauwdruk implementeren.

1. Ga te**implementaties**.

2. Klik op **Add**.

3. Plakken in de volgende Hallo blauwdruk YAML. Deze blauwdruk bevat één cluster met slechts één service-variant, die we in een latere stap wijzigen:

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster toocreate
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. Klik op **Opslaan**. Vamp initieert Hallo-implementatie.

Hallo-implementatie wordt vermeld op Hallo **implementaties** pagina. Klik op Hallo implementatie toomonitor de status ervan.

![UI - sava implementeren vamp](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![de service Sava in Vamp gebruikersinterface](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

Twee gateways worden gemaakt, die worden vermeld op Hallo **Gateways** pagina:

* een stabiele eindpunt tooaccess Hallo-service (poort 9050) uitgevoerd 
* een beheerde Vamp interne gateway (meer informatie over deze gateway later). 

![UI - sava gateways vamp](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

Hallo sava service is nu geïmplementeerd, maar u geen toegang tot deze extern omdat hello Azure Load Balancer tooforward verkeer tooit nog niet weet. tooaccess hello service update hello Azure netwerkconfiguratie.


## <a name="update-hello-azure-network-configuration"></a>Werk de configuratie van hello Azure-netwerk

Hallo sava service vamp geïmplementeerd op Hallo DC/OS-agent knooppunten, een stabiele eindpunt op poort 9050 blootstellen. tooaccess Hallo-service van het buitenste Hallo DC/OS-cluster, moet u Hallo wijzigingen toohello Azure netwerkconfiguratie in uw implementatie van het cluster te volgen: 

1. **Hello Azure Load Balancer configureren** voor Hallo-agents (Hallo resource met de naam **dcos-agent-lb-xxxx**) met een health test en een regel tooforward-verkeer op poort 9050 toohello sava exemplaren. 

2. **Update Hallo netwerkbeveiligingsgroep** voor openbare agents hello (Hallo resource met de naam **XXXX-agent-openbare-nsg-XXXX**) tooallow verkeer op poort 9050.

Voor gedetailleerde stappen toocomplete Hallo deze taken met behulp van Azure portal, Zie [openbare toegang tooan Azure Container Service-toepassing inschakelen](container-service-enable-public-access.md). Poort 9050 voor alle poortinstellingen opgeven.


Zodra u alles is gemaakt, gaat u toohello **overzicht** blade Hallo DC/OS-agent load balancer (Hallo resource met de naam **dcos-agent-lb-xxxx**). Hallo zoeken **openbaar IP-adres**, en Hallo adres tooaccess sava op poort 9050 gebruiken.

![Azure portal - get openbaar IP-adres](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![Sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a>Voer een kokospalm release

Stel dat u hebt een nieuwe versie van deze toepassing die u wilt dat toocanary release in productie. U hebt het beperkte als magneticio/sava:1.1.0 en toogo gereed zijn. Vamp kunt u eenvoudig toevoegen van nieuwe services toohello waarop implementatie wordt uitgevoerd. Deze 'samengevoegde' services worden geïmplementeerd naast Hallo bestaande services in Hallo-cluster en een gewicht van 0% toegewezen. Er is geen verkeer is gerouteerde tooa zojuist samengevoegd service totdat u de distributie van verkeer Hallo aanpassen. Hallo gewicht schuifregelaar in Hallo Vamp gebruikersinterface biedt u volledige controle over Hallo distributie, waardoor het incrementele aanpassingen (kokospalm release) of een directe terugdraaien.

### <a name="merge-a-new-service-variant"></a>Een nieuwe service-variant samenvoegen

toomerge hello nieuwe sava 1.1-service met Hallo waarop implementatie wordt uitgevoerd:

1. Klik in de gebruikersinterface Vamp hello, op **blauwdrukken**.

2. Klik op **toevoegen** en plakken in de volgende Hallo blauwdruk YAML: deze blauwdruk wordt een nieuwe service variant (sava: 1.1.0) toodeploy binnen Hallo bestaand cluster (sava_cluster) beschreven.

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster tooupdate
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint tooupdate
  ```
  
3. Klik op **Opslaan**. Hallo blauwdruk wordt opgeslagen en weergegeven op Hallo **blauwdrukken** pagina.

4. Open Hallo actiemenu op Hallo sava: 1.1 blauwdruk en klikt u op **samenvoegen naar**.

  ![UI - blauwdrukken vamp](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. Selecteer Hallo **sava** implementatie en klik op **samenvoegen**.

  ![Vamp UI - blauwdruk toodeployment samenvoegen](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

Vamp implementeert Hallo nieuwe sava: 1.1.0 service variant beschreven in Hallo blauwdruk naast sava: 1.0.0 in Hallo **sava_cluster** Hallo waarop implementatie wordt uitgevoerd. 

![UI - bijgewerkte sava implementatie vamp](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

Hallo **sava_cluster-sava/webport** gateway (Hallo clustereindpunt) wordt ook bijgewerkt, sava: 1.1.0 toevoegen van een route toohello zojuist geïmplementeerd. Op dit moment geen verkeer wordt gerouteerd hier (Hallo **gewicht** too0% is ingesteld).

![UI - cluster gateway vamp](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a>Kokospalm release

Met beide versies van sava geïmplementeerd in Hallo dezelfde cluster, het Hallo-distributie van verkeer tussen hen door Hallo verplaatsen aanpassen **gewicht** schuifregelaar.

1. Klik op ![Vamp UI - bewerken](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) volgende te**gewicht**.

2. Stel Hallo gewicht distributie too50%/50% en klik op **opslaan**.

  ![UI - gateway gewicht schuifregelaar vamp](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. Ga terug tooyour browser en vernieuw Hallo sava pagina een paar keer. Hallo sava toepassing nu schakelt u tussen een sava: 1.0 en een pagina sava: 1.1.

  ![wisselende sava1.0 en sava1.1 services](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > Deze alternatieven van Hallo pagina werkt het beste met Hallo 'Incognito' of 'Anoniem'-modus van uw browser vanwege Hallo van statische elementen in de cache.
  >

### <a name="filter-traffic"></a>Filteren van verkeer

Stel dat na implementatie dat u een incompatibiliteit in sava: 1.1.0 dat oorzaken problemen worden weergegeven in browsers Firefox gedetecteerd. U kunt Vamp toofilter binnenkomend verkeer en directe back-alle gebruikers van Firefox toohello stabiele sava: 1.0.0 bekend. Dit filter verbeterd direct wordt omgezet Hallo onderbreking voor Firefox gebruikers, terwijl alle andere tooenjoy Hallo voordelen van Hallo blijft sava: 1.1.0.

Maakt gebruik van vamp **voorwaarden** toofilter verkeer tussen routes in een gateway. Het verkeer wordt eerst gefilterd en omgeleid volgens toohello voorwaarden toegepast tooeach route. Alle resterende verkeer wordt verdeeld volgens toohello gateway gewicht-instelling.

U kunt een voorwaarde toofilter alle Firefox gebruikers maken en hen te instrueren toohello oude sava: 1.0.0:

1. Op Hallo sava_cluster-sava/webport **Gateways** pagina, klikt u op ![Vamp UI - bewerken](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd een **voorwaarde** toohello route sava/sava_cluster/sava:1.0.0/webport. 

2. Voer Hallo voorwaarde **gebruikersagent Firefox ==** en klik op ![Vamp UI - opslaan](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).

  Vamp voegt Hallo voorwaarde van een standaard sterkte van 0%. toostart het filteren van het verkeer, moet u tooadjust Hallo voorwaarde sterkte.

3. Klik op ![Vamp UI - bewerken](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **sterkte** toohello voorwaarde wordt toegepast.
 
4. Set Hallo **sterkte** too100% en klik op ![Vamp UI - opslaan](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.

  Vamp verzendt nu al het verkeer die overeenkomt met de Hallo voorwaarde (alle gebruikers voor de Firefox) toosava:1.0.0.

  ![Vamp UI - voorwaarde toogateway toepassen](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. Ten slotte aanpassen Hallo gateway gewicht toosend alle resterende verkeer (alle gebruikers voor de niet-Firefox) toohello nieuwe sava: 1.1.0. Klik op ![Vamp UI - bewerken](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) volgende te**gewicht** en stel de gewichtsverdeling Hallo zodat 100% gerichte toohello route sava/sava_cluster/sava:1.1.0/webport.

  Al het verkeer niet gefilterd door het Hallo-voorwaarde is nu gerichte toohello nieuwe sava: 1.1.0.

6. toosee hello filter in actie, twee verschillende browsers (één Firefox en een andere browser) en openen Hallo sava service van beide. Alle Firefox aanvragen verzonden toosava:1.0.0, terwijl alle andere browsers gerichte toosava:1.1.0 zijn.

  ![UI - filter verkeer vamp](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a>Berekening van het

Dit artikel is een korte inleiding tooVamp op een DC/OS-cluster. Om te beginnen u Vamp up verkregen en uitgevoerd op uw Azure Container Service DC/OS-cluster, een service met een blauwdruk Vamp geïmplementeerd en het heeft geopend op Hallo blootgesteld eindpunt (gateway).

We ook op sommige andere van krachtige functies van Vamp aangeraakt: een nieuwe service variant toohello waarop implementatie wordt uitgevoerd en voor het filteren van verkeer tooresolve een bekend incompatibiliteitsprobleem incrementeel introducing samenvoegen.


## <a name="next-steps"></a>Volgende stappen

* Meer informatie over het beheren van Vamp acties via Hallo [Vamp REST-API](http://vamp.io/documentation/api/api-reference/).

* Vamp automatiseringsscripts in Node.js bouwen en uitvoeren als [Vamp werkstromen](http://vamp.io/documentation/tutorials/create-a-workflow/).

* Zie aanvullende [VAMP zelfstudies](http://vamp.io/documentation/tutorials/overview/).

