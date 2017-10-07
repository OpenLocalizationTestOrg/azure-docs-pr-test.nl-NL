---
title: Java-toepassing op een virtuele machine aaaCompute-intensieve | Microsoft Docs
description: Meer informatie over hoe toocreate Azure een virtuele machine die een rekenintensieve Java-toepassing wordt uitgevoerd door een andere Java-toepassing kan worden bewaakt.
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: ae6f2737-94c7-4569-9913-d871450c2827
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 02a198802a8d78bd444cd5a9197a78cb94f48e3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-compute-intensive-task-in-java-on-a-virtual-machine"></a>Hoe een rekenintensieve toorun taak Java op een virtuele machine
> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

Met Azure, kunt u een virtuele machine toohandle rekenintensieve taken. Bijvoorbeeld: een virtuele machine verwerkt taken en leveren resultaten tooclient computers of mobiele toepassingen. Na het lezen van dit artikel hebt u een goed begrip van hoe toocreate een virtuele machine die een rekenintensieve Java-toepassing wordt uitgevoerd door een andere Java-toepassing kan worden bewaakt.

Deze zelfstudie wordt ervan uitgegaan dat u weet hoe toocreate Java-consoletoepassingen bibliotheken tooyour Java-toepassing kunt importeren en een Java-archief (JAR) kunt genereren. Er is geen kennis van Microsoft Azure wordt verondersteld.

U leert:

* Hoe toocreate een virtuele machine met een Java Development Kit (JDK) al is geïnstalleerd.
* Hoe meld tooremotely in tooyour virtuele machine.
* Hoe toocreate een service bus naamruimte.
* Hoe toocreate een Java-toepassing die een taak rekenintensieve uitvoert.
* Hoe Hallo toocreate een Java-toepassing bewaakt de voortgang van Hallo rekenintensieve taak.
* Hoe Hallo toorun Java-toepassingen.
* Hoe Hallo toostop Java-toepassingen.

Deze zelfstudie gebruikt Hallo Traveling verkoper probleem voor Hallo rekenintensieve taak. Hallo Hieronder volgt een voorbeeld van Hallo Java-toepassing uitgevoerd Hallo rekenintensieve taak.

![Traveling verkoper probleem solver][solver_output]

Hallo Hier volgt een voorbeeld van een Java-toepassing hello rekenintensieve bewakingstaak Hallo.

![Traveling verkoper probleem client][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a>toocreate een virtuele machine
1. Meld u bij toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Klik op **nieuw**, klikt u op **Compute**, klikt u op **virtuele machine**, en klik vervolgens op **uit galerie**.
3. In Hallo **virtuele machine-installatiekopie selecteert** dialoogvenster, **JDK 7 Windows Server 2012**.
   Houd er rekening mee dat **JDK 6 Windows Server 2012** beschikbaar is voor het geval u oudere toepassingen die nog niet klaar toorun in JDK 7 hebt.
4. Klik op **Volgende**.
5. In Hallo **Virtuele-machineconfiguratie** in het dialoogvenster:
   1. Geef een naam voor de Hallo virtuele machine.
   2. Geef Hallo grootte toouse voor Hallo virtuele machine.
   3. Voer een naam voor Hallo beheerder in Hallo **gebruikersnaam** veld. Deze naam en het Hallo-wachtwoord u naast voert, gebruikt u deze wanneer u op afstand toohello virtuele machine aanmelden.
   4. Voer een wachtwoord in Hallo **nieuw wachtwoord** veld en voer deze opnieuw in Hallo **bevestigen** veld. Dit is wachtwoord Hallo Administrator-account.
   5. Klik op **Volgende**.
6. In Hallo volgende **Virtuele-machineconfiguratie** in het dialoogvenster:
   1. Voor **Cloudservice**, standaard-Hallo **Maak een nieuwe cloudservice**.
   2. waarde voor Hallo **Cloud service DNS-naam** uniek zijn binnen cloudapp.net. Indien nodig, wijzigt u deze waarde zodat deze Azure geeft dat deze uniek is.
   3. Geef een regio, een affiniteitsgroep of een virtueel netwerk. Geef voor deze zelfstudie een regio zoals **VS-West**.
   4. Voor **Opslagaccount**, selecteer **een automatisch gegenereerde opslagaccount gebruiken**.
   5. Voor **Beschikbaarheidsset**, selecteer **(geen)**.
   6. Klik op **Volgende**.
7. In de laatste Hallo **Virtuele-machineconfiguratie** in het dialoogvenster:
   1. Hallo eindpunt standaardvermeldingen accepteren.
   2. Klik op **Voltooien**.

## <a name="tooremotely-log-in-tooyour-virtual-machine"></a>tooremotely aanmelden tooyour virtuele machine
1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Klik op **virtuele machines**.
3. Klik op de naam Hallo van Hallo virtuele machine die u wilt toolog in.
4. Klik op **Verbinden**.
5. Reageren op toohello prompts als benodigde tooconnect toohello virtuele machine. Desgevraagd Hallo beheerdersnaam en wachtwoord gebruiken Hallo-waarden die u hebt opgegeven toen u Hallo virtuele machine hebt gemaakt.

Opmerking die hello Azure Service Bus-functionaliteit vereist Hallo Baltimore CyberTrust Root certificate toobe geïnstalleerd als onderdeel van uw Java Runtime Environment **cacerts** opslaan. Dit certificaat wordt automatisch opgenomen in Hallo Java Runtime Environment (JRE) die wordt gebruikt door deze zelfstudie. Als u nog geen dit certificaat in uw JRE **cacerts** opslaat, Zie [toevoegen van een certificaat toohello Java CA-certificaatarchief] [ add_ca_cert] voor meer informatie over deze toe te voegen (evenals informatie over het Hallo-certificaten weergeven in uw archief cacerts).

## <a name="how-toocreate-a-service-bus-namespace"></a>Hoe toocreate een service bus naamruimte
toobegin met Service Bus-wachtrijen in Azure, moet u eerst een Servicenaamruimte maken. Een Servicenaamruimte biedt een scoping container voor het adresseren van Service Bus-resources in uw toepassing.

een Servicenaamruimte toocreate:

1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Klik in het Hallo linksonder navigatiedeelvenster Hallo klassieke Azure-portal op **Service Bus, Access Control & opslaan in cache**.
3. Klik in Hallo linksboven deelvenster Hallo klassieke Azure-portal op Hallo **Service Bus** knooppunt en klik vervolgens op Hallo **nieuw** knop.  
   ![Schermafbeelding van de service Bus-knooppunt][svc_bus_node]
4. In Hallo **maken van een nieuwe Service-Namespace** dialoogvenster Voer een **Namespace**, en klik vervolgens toomake ervoor dat deze uniek zijn, op de **beschikbaarheid controleren** knop.  
   ![Maak een nieuwe Namespace-schermafbeelding][create_namespace]
5. Nadat u ervoor zorgt dat Hallo naamruimtenaam beschikbaar is, kiest u het land of regio waarin uw naamruimte moet worden gehost, en klik vervolgens op Hallo **Namespace maken** knop.  
   
   Hallo-naamruimte die u hebt gemaakt wordt vervolgens in de klassieke Azure-portal Hallo weergegeven en een tooactivate even duurt. Wacht totdat de status Hallo **Active** voordat u doorgaat met de volgende stap Hallo.

## <a name="obtain-hello-default-management-credentials-for-hello-namespace"></a>Hallo standaard Standaardbeheerreferenties voor Hallo-naamruimte ophalen
In de volgorde tooperform beheerbewerkingen, zoals het maken van een wachtrij op de nieuwe naamruimte hello, moet u tooobtain hello beheerreferenties voor de naamruimte.

1. Klik in de Hallo navigatiedeelvenster links op Hallo **Service Bus** knooppunt om Hallo lijst met beschikbare naamruimten weer te geven.
   ![Schermafbeelding met beschikbare naamruimten][avail_namespaces]
2. Selecteer Hallo naamruimte die u zojuist hebt gemaakt in Hallo lijst weergegeven.
   ![Lijst met Namespace-schermafbeelding][namespace_list]
3. Hallo rechter **eigenschappen** deelvenster bevat Hallo-eigenschappen voor de nieuwe naamruimte.
   ![Schermopname van eigenschappen deelvenster][properties_pane]
4. Hallo **standaard sleutel** wordt verborgen. Klik op Hallo **weergave** knop toodisplay Hallo beveiligingsreferenties.
   ![Standaard-sleutel-schermafbeelding][default_key]
5. Maak een notitie van Hallo **verlener standaard** en Hallo **standaard sleutel** als u deze informatie hieronder tooperform operations met de naamruimte gebruiken gaat.

## <a name="how-toocreate-a-java-application-that-performs-a-compute-intensive-task"></a>Hoe toocreate een Java-toepassing die een taak rekenintensieve uitvoert
1. Op uw ontwikkelcomputer (waarvoor geen toobe Hallo virtuele machine die u hebt gemaakt), download Hallo [Azure SDK voor Java](https://azure.microsoft.com/develop/java/).
2. Maak een Java-consoletoepassing met voorbeeldcode Hallo aan Hallo einde van deze sectie. In deze zelfstudie gebruiken we **TSPSolver.java** als Hallo Java-bestandsnaam. Hallo wijzigen **uw\_service\_bus\_naamruimte**, **uw\_service\_bus\_eigenaar**, en **uw\_service\_bus\_sleutel** toouse tijdelijke aanduidingen voor uw servicebus **naamruimte**, **standaard verlener** en  **Standaard sleutel** waarden, respectievelijk.
3. Nadat de codering vereist export Hallo toepassing tooa uitvoerbare Java-archief (JAR) en pakket Hallo bibliotheken in Hallo JAR gegenereerd. In deze zelfstudie gebruiken we **TSPSolver.jar** als de naam van de JAR Hallo gegenereerd.

<p/>

    // TSPSolver.java

    import com.microsoft.windowsazure.services.core.Configuration;
    import com.microsoft.windowsazure.services.core.ServiceException;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import java.io.*;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;

    public class TSPSolver {

        //  Value specifying how often tooprovide an update toohello console.
        private static long loopCheck = 100000000;  

        private static long nTimes = 0, nLoops=0;

        private static double[][] distances;
        private static String[] cityNames;
        private static int[] bestOrder;
        private static double minDistance;
        private static ServiceBusContract service;

        private static void buildDistances(String fileLocation, int numCities) throws Exception{
            try{
                BufferedReader file = new BufferedReader(new InputStreamReader(new DataInputStream(new FileInputStream(new File(fileLocation)))));
                double[][] cityLocs = new double[numCities][2];
                for (int i = 0; i<numCities; i++){
                    String[] line = file.readLine().split(", ");
                    cityNames[i] = line[0];
                    cityLocs[i][0] = Double.parseDouble(line[1]);
                    cityLocs[i][1] = Double.parseDouble(line[2]);
                }
                for (int i = 0; i<numCities; i++){
                    for (int j = i; j<numCities; j++){
                        distances[i][j] = Math.hypot(Math.abs(cityLocs[i][0] - cityLocs[j][0]), Math.abs(cityLocs[i][1] - cityLocs[j][1]));
                        distances[j][i] = distances[i][j];
                    }
                }
            } catch (Exception e){
                throw e;
            }
        }

        private static void permutation(List<Integer> startCities, double distSoFar, List<Integer> restCities) throws Exception {

            try
            {
                nTimes++;
                if (nTimes == loopCheck)
                {
                    nLoops++;
                    nTimes = 0;
                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.print("Current time is " + dateFormat.format(date) + ". ");
                    System.out.println(  "Completed " + nLoops + " iterations of size of " + loopCheck + ".");
                }

                if ((restCities.size() == 1) && ((minDistance == -1) || (distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-1)] < minDistance))){
                    startCities.add(restCities.get(0));
                    newBestDistance(startCities, distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-2)]);
                    startCities.remove(startCities.size()-1);
                }
                else{
                    for (int i=0; i<restCities.size(); i++){
                        startCities.add(restCities.get(0));
                        restCities.remove(0);
                        permutation(startCities, distSoFar + distances[startCities.get(startCities.size()-1)][startCities.get(startCities.size()-2)],restCities);
                        restCities.add(startCities.get(startCities.size()-1));
                        startCities.remove(startCities.size()-1);
                    }
                }
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        private static void newBestDistance(List<Integer> cities, double distance) throws ServiceException, Exception {
            try
            {
                minDistance = distance;
                String cityList = "Shortest distance is "+minDistance+", with route: ";
                for (int i = 0; i<bestOrder.length; i++){
                    bestOrder[i] = cities.get(i);
                    cityList += cityNames[bestOrder[i]];
                    if (i != bestOrder.length -1)
                        cityList += ", ";
                }
                System.out.println(cityList);
                service.sendQueueMessage("TSPQueue", new BrokeredMessage(cityList));
            }
            catch (ServiceException se)
            {
                throw se;
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        public static void main(String args[]){

            try {

                Configuration config = ServiceBusConfiguration.configureWithWrapAuthentication(
                        "your_service_bus_namespace", "your_service_bus_owner",
                        "your_service_bus_key",
                        ".servicebus.windows.net",
                        "-sb.accesscontrol.windows.net/WRAPv0.9");

                service = ServiceBusService.create(config);

                int numCities = 10;  // Use as hello default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing toooccur other than creating hello queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing toooccur other than deleting hello queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume hello value passed in is hello number of cities toosolve.
                    numCities = Integer.valueOf(args[0]);  
                }

                System.out.println("Running for " + numCities + " cities.");

                List<Integer> startCities = new ArrayList<Integer>();
                List<Integer> restCities = new ArrayList<Integer>();
                startCities.add(0);
                for(int i = 1; i<numCities; i++)
                    restCities.add(i);
                distances = new double[numCities][numCities];
                cityNames = new String[numCities];
                buildDistances("c:\\TSP\\cities.txt", numCities);
                minDistance = -1;
                bestOrder = new int[numCities];
                permutation(startCities, 0, restCities);
                System.out.println("Final solution found!");
                service.sendQueueMessage("TSPQueue", new BrokeredMessage("Complete"));
            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }
        }

    }



## <a name="how-toocreate-a-java-application-that-monitors-hello-progress-of-hello-compute-intensive-task"></a>Hoe toocreate een Java-toepassing bewaakt de voortgang van Hallo rekenintensieve taak Hallo
1. Maak een Java-consoletoepassing met voorbeeldcode Hallo op Hallo einde van dit gedeelte op uw ontwikkelcomputer. In deze zelfstudie gebruiken we **TSPClient.java** als Hallo Java-bestandsnaam. Zoals eerder besproken, Hallo wijzigen **uw\_service\_bus\_naamruimte**, **uw\_service\_bus\_eigenaar**, en **uw\_service\_bus\_sleutel** toouse tijdelijke aanduidingen voor uw servicebus **naamruimte**, **standaard verlener**en **standaard sleutel** waarden, respectievelijk.
2. Hallo toepassing tooa exporteren uitvoerbare JAR en pakket Hallo vereist bibliotheken in Hallo JAR gegenereerd. In deze zelfstudie gebruiken we **TSPClient.jar** als de naam van de JAR Hallo gegenereerd.

<p/>

    // TSPClient.java

    import java.util.Date;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import com.microsoft.windowsazure.services.core.*;

    public class TSPClient
    {

        public static void main(String[] args)
        {
                try
                {

                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.println("Starting at " + dateFormat.format(date) + ".");

                    String namespace = "your_service_bus_namespace";
                    String issuer = "your_service_bus_owner";
                    String key = "your_service_bus_key";

                    Configuration config;
                    config = ServiceBusConfiguration.configureWithWrapAuthentication(
                            namespace, issuer, key,
                            ".servicebus.windows.net",
                            "-sb.accesscontrol.windows.net/WRAPv0.9");

                    ServiceBusContract service = ServiceBusService.create(config);

                    BrokeredMessage message;

                    int waitMinutes = 3;  // Use as hello default, if no value is specified at command line.
                    if (args.length != 0)
                    {
                        waitMinutes = Integer.valueOf(args[0]);  
                    }

                    String waitString;

                    waitString = (waitMinutes == 1) ? "minute." : waitMinutes + " minutes.";

                    // This queue must have previously been created.
                    service.getQueue("TSPQueue");

                    int numRead;

                    String s = null;

                    while (true)
                    {

                        ReceiveQueueMessageResult resultQM = service.receiveQueueMessage("TSPQueue");
                        message = resultQM.getValue();

                        if (null != message && null != message.getMessageId())
                        {

                            // Display hello queue message.
                            byte[] b = new byte[200];

                            System.out.print("From queue: ");

                            s = null;
                            numRead = message.getBody().read(b);
                            while (-1 != numRead)
                            {
                                s = new String(b);
                                s = s.trim();
                                System.out.print(s);
                                numRead = message.getBody().read(b);
                            }
                            System.out.println();
                            if (s.compareTo("Complete") == 0)
                            {
                                // No more processing toooccur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // hello queue is empty.
                            System.out.println("Queue is empty. Sleeping for another " + waitString);
                            Thread.sleep(60000 * waitMinutes);
                        }
                    }

            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }

        }

    }

## <a name="how-toorun-hello-java-applications"></a>Hoe toorun Hallo Java-toepassingen
Hallo rekenintensieve toepassing uitvoert, Hallo eerste toocreate Hallo wachtrij vervolgens toosolve onderweg Saleseman probleem, waardoor Hallo huidige beste route toohello service bus-wachtrij wordt toegevoegd. Tijdens het Hallo is rekenintensieve toepassing uitgevoerd (of later), Voer Hallo client toodisplay resultaten van Hallo service bus-wachtrij.

### <a name="toorun-hello-compute-intensive-application"></a>toorun hello rekenintensieve toepassing
1. Meld u aan tooyour virtuele machine.
2. Maak een map waar u uw toepassing wordt uitgevoerd. Bijvoorbeeld: **c:\TSP**.
3. Kopiëren **TSPSolver.jar** te**c:\TSP**,
4. Maak een bestand met de naam **c:\TSP\cities.txt** Hello inhoud te volgen.
   
        City_1, 1002.81, -1841.35
        City_2, -953.55, -229.6
        City_3, -1363.11, -1027.72
        City_4, -1884.47, -1616.16
        City_5, 1603.08, -1030.03
        City_6, -1555.58, 218.58
        City_7, 578.8, -12.87
        City_8, 1350.76, 77.79
        City_9, 293.36, -1820.01
        City_10, 1883.14, 1637.28
        City_11, -1271.41, -1670.5
        City_12, 1475.99, 225.35
        City_13, 1250.78, 379.98
        City_14, 1305.77, 569.75
        City_15, 230.77, 231.58
        City_16, -822.63, -544.68
        City_17, -817.54, -81.92
        City_18, 303.99, -1823.43
        City_19, 239.95, 1007.91
        City_20, -1302.92, 150.39
        City_21, -116.11, 1933.01
        City_22, 382.64, 835.09
        City_23, -580.28, 1040.04
        City_24, 205.55, -264.23
        City_25, -238.81, -576.48
        City_26, -1722.9, -909.65
        City_27, 445.22, 1427.28
        City_28, 513.17, 1828.72
        City_29, 1750.68, -1668.1
        City_30, 1705.09, -309.35
        City_31, -167.34, 1003.76
        City_32, -1162.85, -1674.33
        City_33, 1490.32, 821.04
        City_34, 1208.32, 1523.3
        City_35, 18.04, 1857.11
        City_36, 1852.46, 1647.75
        City_37, -167.44, -336.39
        City_38, 115.4, 0.2
        City_39, -66.96, 917.73
        City_40, 915.96, 474.1
        City_41, 140.03, 725.22
        City_42, -1582.68, 1608.88
        City_43, -567.51, 1253.83
        City_44, 1956.36, 830.92
        City_45, -233.38, 909.93
        City_46, -1750.45, 1940.76
        City_47, 405.81, 421.84
        City_48, 363.68, 768.21
        City_49, -120.3, -463.13
        City_50, 588.51, 679.33
5. Wijzig de mappen tooc:\TSP bij een opdrachtprompt.
6. Zorg ervoor dat Hallo JRE de bin-map in omgevingsvariabele Hallo-PATH.
7. U moet toocreate Hallo service bus-wachtrij voordat u het aantal permutaties Hallo TSP solver uitvoert. Hallo na de opdracht toocreate Hallo service bus-wachtrij worden uitgevoerd.
   
        java -jar TSPSolver.jar createqueue
8. Nu dat hello wachtrij wordt gemaakt, kunt u het aantal permutaties Hallo TSP solver kunt uitvoeren. Bijvoorbeeld: uitvoeren Hallo opdracht toorun Hallo solver voor 8 steden te volgen.
   
        java -jar TSPSolver.jar 8
   
   Als u niet een getal opgeeft, wordt deze uitgevoerd voor 10 steden. Als Hallo solver huidige kortste routes wordt gevonden, wordt deze deze toohello wachtrij toegevoegd.

> [!NOTE]
> Hallo groter Hallo nummer dat u opgeeft, Hallo langer Hallo solver wordt uitgevoerd. Bijvoorbeeld, actief 14 steden kunnen enkele minuten duren, en wordt uitgevoerd voor 15 steden kan enkele uren duren. Verhogen too16 of meer plaatsen kan leiden tot dagen van de runtime (uiteindelijk weken, maanden en jaren). Dit is vanwege toohello snelle toename van het aantal permutaties geëvalueerd door Hallo solver als het aantal steden toeneemt Hallo Hallo.
> 
> 

### <a name="how-toorun-hello-monitoring-client-application"></a>Hoe toorun Hallo bewaking clienttoepassing
1. Meld u aan tooyour computer waar u de clienttoepassing hello wordt uitgevoerd. Dit hoeft geen toobe dezelfde machine uitgevoerd Hallo Hallo **TSPSolver** toepassing, maar het kan zijn.
2. Maak een map waar u uw toepassing wordt uitgevoerd. Bijvoorbeeld: **c:\TSP**.
3. Kopiëren **TSPClient.jar** te**c:\TSP**,
4. Zorg ervoor dat Hallo JRE de bin-map in omgevingsvariabele Hallo-PATH.
5. Wijzig de mappen tooc:\TSP bij een opdrachtprompt.
6. Hallo volgende opdracht worden uitgevoerd.
   
        java -jar TSPClient.jar
   
    Geef desgewenst Hallo aantal minuten toosleep bij het Hallo-wachtrij door door te geven in een opdrachtregelargument controleren. Hallo slaapstand standaardperiode voor het controleren van de wachtrij Hallo is 3 minuten, die wordt gebruikt als er geen opdrachtregelargument wordt doorgegeven, te**TSPClient**. Als u een andere waarde toouse voor hello slaapstand-interval wilt, bijvoorbeeld één minuut Hallo volgende opdracht uitvoeren.
   
        java -jar TSPClient.jar 1
   
    Hallo-client wordt uitgevoerd totdat deze een wachtrijbericht van 'Voltooi' ziet. Houd er rekening mee dat als u meerdere exemplaren van Hallo solver uitvoert zonder het Hallo-client uitvoert, u toorun Hallo client meerdere keren toocompletely leeg Hallo wachtrij moet mogelijk. U kunt ook Hallo wachtrij verwijderen en opnieuw maken. toodelete hello wachtrij op en voer de volgende Hallo **TSPSolver** (geen **TSPClient**) opdracht.
   
        java -jar TSPSolver.jar deletequeue
   
    Hallo solver wordt uitgevoerd totdat het klaar is met het onderzoeken van alle routes.

## <a name="how-toostop-hello-java-applications"></a>Hoe toostop Hallo Java-toepassingen
Voor Hallo solver en clienttoepassingen, drukt u op **Ctrl + C** tooexit als u wilt dat tooend voorafgaande toonormal voltooiing.

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
