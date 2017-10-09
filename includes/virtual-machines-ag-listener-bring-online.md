1. <span data-ttu-id="98ac7-101">Vouw in Failoverclusterbeheer **rollen**, en selecteer vervolgens de beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="98ac7-101">In Failover Cluster Manager, expand **Roles**, and then highlight your availability group.</span></span>  

2. <span data-ttu-id="98ac7-102">Op Hallo **Resources** tabblad en klik vervolgens op met de rechtermuisknop op de naam van de beschikbaarheidsgroeplistener hello **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="98ac7-102">On hello **Resources** tab, right-click hello listener name, and then click **Properties**.</span></span>

3. <span data-ttu-id="98ac7-103">Klik op Hallo **afhankelijkheden** tabblad. Controleer of Hallo IP-adressen hebt of niet als meerdere resources worden weergegeven, en afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="98ac7-103">Click hello **Dependencies** tab. If multiple resources are listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span>  

4. <span data-ttu-id="98ac7-104">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="98ac7-104">Click **OK**.</span></span>

5. <span data-ttu-id="98ac7-105">Met de rechtermuisknop op de naam van de beschikbaarheidsgroeplistener hello en klik vervolgens op **Online brengen**.</span><span class="sxs-lookup"><span data-stu-id="98ac7-105">Right-click hello listener name, and then click **Bring Online**.</span></span>

6. <span data-ttu-id="98ac7-106">Na het Hallo-listener is online op Hallo **Resources** tabblad en klik vervolgens op met de rechtermuisknop op het Hallo-beschikbaarheidsgroep **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="98ac7-106">After hello listener is online, on hello **Resources** tab, right-click hello availability group, and then click **Properties**.</span></span>
   
    ![Hallo beschikbaarheidsgroepresource configureren](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. <span data-ttu-id="98ac7-108">Maken van een afhankelijkheid Hallo listener bron (niet Hallo IP-adres resources naam) en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="98ac7-108">Create a dependency on hello listener name resource (not hello IP address resources name), and then click **OK**.</span></span>
   
    ![Afhankelijkheid van de naam van de listener Hallo toevoegen](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. <span data-ttu-id="98ac7-110">Start SQL Server Management Studio en maak verbinding toohello primaire replica.</span><span class="sxs-lookup"><span data-stu-id="98ac7-110">Start SQL Server Management Studio, and then connect toohello primary replica.</span></span>

9. <span data-ttu-id="98ac7-111">Ga te**AlwaysOn hoge beschikbaarheid** > **beschikbaarheidsgroepen** > **\<AvailabilityGroupName\>**   >  **Beschikbaarheidsgroep-Listeners**.</span><span class="sxs-lookup"><span data-stu-id="98ac7-111">Go too**AlwaysOn High Availability** > **Availability Groups** > **\<AvailabilityGroupName\>** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="98ac7-112">Hallo-listener-naam die u hebt gemaakt in Failoverclusterbeheer moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="98ac7-112">hello listener name that you created in Failover Cluster Manager should be displayed.</span></span>

10. <span data-ttu-id="98ac7-113">Met de rechtermuisknop op de naam van de beschikbaarheidsgroeplistener hello en klik vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="98ac7-113">Right-click hello listener name, and then click **Properties**.</span></span>

11. <span data-ttu-id="98ac7-114">In Hallo **poort** Geef Hallo-poortnummer voor Hallo beschikbaarheidsgroep-listener met behulp van Hallo $EndpointPort die u eerder hebt gebruikt (in deze zelfstudie is 1433 Hallo standaard), en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="98ac7-114">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort that you used earlier (in this tutorial, 1433 was hello default), and then click **OK**.</span></span>

