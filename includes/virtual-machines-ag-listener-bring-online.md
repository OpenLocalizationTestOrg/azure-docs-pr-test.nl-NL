1. <span data-ttu-id="533ce-101">Vouw in Failoverclusterbeheer **rollen**, en selecteer vervolgens de beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="533ce-101">In Failover Cluster Manager, expand **Roles**, and then highlight your availability group.</span></span>  

2. <span data-ttu-id="533ce-102">Op de **Resources** tabblad en klik vervolgens op met de rechtermuisknop op de naam van de listener **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="533ce-102">On the **Resources** tab, right-click the listener name, and then click **Properties**.</span></span>

3. <span data-ttu-id="533ce-103">Klik op de **afhankelijkheden** tabblad.</span><span class="sxs-lookup"><span data-stu-id="533ce-103">Click the **Dependencies** tab.</span></span> <span data-ttu-id="533ce-104">Controleer of de IP-adressen hebt of niet als meerdere resources worden weergegeven, en afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="533ce-104">If multiple resources are listed, verify that the IP addresses have OR, not AND, dependencies.</span></span>  

4. <span data-ttu-id="533ce-105">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="533ce-105">Click **OK**.</span></span>

5. <span data-ttu-id="533ce-106">Met de rechtermuisknop op de naam van de listener en klik vervolgens op **Online brengen**.</span><span class="sxs-lookup"><span data-stu-id="533ce-106">Right-click the listener name, and then click **Bring Online**.</span></span>

6. <span data-ttu-id="533ce-107">Nadat de listener is online op het **Resources** tabblad en klik vervolgens op met de rechtermuisknop op de beschikbaarheidsgroep **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="533ce-107">After the listener is online, on the **Resources** tab, right-click the availability group, and then click **Properties**.</span></span>
   
    ![De beschikbaarheidsgroepresource configureren](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. <span data-ttu-id="533ce-109">Een afhankelijkheid voor de listener naambron (niet de naam IP-adres resources) maken en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="533ce-109">Create a dependency on the listener name resource (not the IP address resources name), and then click **OK**.</span></span>
   
    ![Afhankelijkheid van de naam van de listener toevoegen](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. <span data-ttu-id="533ce-111">Start SQL Server Management Studio en maak verbinding met de primaire replica.</span><span class="sxs-lookup"><span data-stu-id="533ce-111">Start SQL Server Management Studio, and then connect to the primary replica.</span></span>

9. <span data-ttu-id="533ce-112">Ga naar **AlwaysOn hoge beschikbaarheid** > **beschikbaarheidsgroepen** > **\<AvailabilityGroupName\>**   >  **Beschikbaarheidsgroep-Listeners**.</span><span class="sxs-lookup"><span data-stu-id="533ce-112">Go to **AlwaysOn High Availability** > **Availability Groups** > **\<AvailabilityGroupName\>** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="533ce-113">De naam van de listener die u hebt gemaakt in Failoverclusterbeheer moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="533ce-113">The listener name that you created in Failover Cluster Manager should be displayed.</span></span>

10. <span data-ttu-id="533ce-114">Met de rechtermuisknop op de naam van de listener en klik vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="533ce-114">Right-click the listener name, and then click **Properties**.</span></span>

11. <span data-ttu-id="533ce-115">In de **poort** vak het poortnummer opgeven voor de beschikbaarheidsgroep-listener met behulp van de $EndpointPort die u eerder hebt gebruikt (in deze zelfstudie is 1433 de standaardinstelling), en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="533ce-115">In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort that you used earlier (in this tutorial, 1433 was the default), and then click **OK**.</span></span>

