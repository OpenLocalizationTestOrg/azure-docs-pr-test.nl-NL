---
title: Algemene SQL-Connector stap voor stap | Microsoft Docs
description: In dit artikel wordt u stap voor stap een eenvoudig HR-systeem stapsgewijze met behulp van de algemene SQL-Connector.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 3fdc1b405b95180d031aa4ad45b406f7fc149d8f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="f4043-103">Algemene SQL Connector, stap voor stap</span><span class="sxs-lookup"><span data-stu-id="f4043-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="f4043-104">In dit onderwerp is een stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="f4043-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="f4043-105">Deze maakt een eenvoudig voorbeeld HR-database en deze gebruiken voor het importeren van sommige gebruikers en hun groepslidmaatschap.</span><span class="sxs-lookup"><span data-stu-id="f4043-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-the-sample-database"></a><span data-ttu-id="f4043-106">De voorbeelddatabase voorbereiden</span><span class="sxs-lookup"><span data-stu-id="f4043-106">Prepare the sample database</span></span>
<span data-ttu-id="f4043-107">Op een server met SQL Server, voert de SQL-script gevonden in [bijlage A](#appendix-a). Dit script maakt een voorbeelddatabase met de naam GSQLDEMO.</span><span class="sxs-lookup"><span data-stu-id="f4043-107">On a server running SQL Server, run the SQL script found in [Appendix A](#appendix-a). This script creates a sample database with the name GSQLDEMO.</span></span> <span data-ttu-id="f4043-108">Het objectmodel voor de database is gemaakt, ziet deze afbeelding:</span><span class="sxs-lookup"><span data-stu-id="f4043-108">The object model for the created database looks like this picture:</span></span>  
<span data-ttu-id="f4043-109">![Objectmodel](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-109">![Object Model](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="f4043-110">Ook een gebruiker die u wilt gebruiken om verbinding met de database te maken.</span><span class="sxs-lookup"><span data-stu-id="f4043-110">Also create a user you want to use to connect to the database.</span></span> <span data-ttu-id="f4043-111">In dit scenario wordt de gebruiker FABRIKAM\SQLUser aangeroepen en zich in het domein.</span><span class="sxs-lookup"><span data-stu-id="f4043-111">In this walkthrough, the user is called FABRIKAM\SQLUser and located in the domain.</span></span>

## <a name="create-the-odbc-connection-file"></a><span data-ttu-id="f4043-112">Maken van het ODBC-verbindingsbestand</span><span class="sxs-lookup"><span data-stu-id="f4043-112">Create the ODBC connection file</span></span>
<span data-ttu-id="f4043-113">De algemene SQL-Connector maakt gebruik van ODBC verbinding maken met de externe server.</span><span class="sxs-lookup"><span data-stu-id="f4043-113">The Generic SQL Connector is using ODBC to connect to the remote server.</span></span> <span data-ttu-id="f4043-114">Eerst moet een bestand met de gegevens voor de ODBC-verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="f4043-114">First we need to create a file with the ODBC connection information.</span></span>

1. <span data-ttu-id="f4043-115">Start het ODBC-management-hulpprogramma op uw server:</span><span class="sxs-lookup"><span data-stu-id="f4043-115">Start the ODBC management utility on your server:</span></span>  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="f4043-117">Selecteer het tabblad **DSN-bestand**.</span><span class="sxs-lookup"><span data-stu-id="f4043-117">Select the tab **File DSN**.</span></span> <span data-ttu-id="f4043-118">Klik op **toevoegen...** .</span><span class="sxs-lookup"><span data-stu-id="f4043-118">Click **Add...**.</span></span>  
   <span data-ttu-id="f4043-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="f4043-120">De out-of-box stuurprogramma werkt fijn, dus te selecteren en op **volgende >**.</span><span class="sxs-lookup"><span data-stu-id="f4043-120">The out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="f4043-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="f4043-122">Geef het bestand een naam, zoals **GenericSQL**.</span><span class="sxs-lookup"><span data-stu-id="f4043-122">Give the file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="f4043-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="f4043-124">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="f4043-124">Click **Finish**.</span></span>  
   <span data-ttu-id="f4043-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="f4043-126">Tijd om de verbinding te configureren.</span><span class="sxs-lookup"><span data-stu-id="f4043-126">Time to configure the connection.</span></span> <span data-ttu-id="f4043-127">Geef de gegevensbron een goede beschrijving en geef de naam van de server met SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f4043-127">Give the data source a good description and provide the name of the server running SQL Server.</span></span>  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="f4043-129">Selecteer hoe u verifieert met behulp van SQL.</span><span class="sxs-lookup"><span data-stu-id="f4043-129">Select how to authenticate with SQL.</span></span> <span data-ttu-id="f4043-130">In dit geval gebruiken we Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="f4043-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="f4043-132">Geef de naam van de voorbeelddatabase **GSQLDEMO**.</span><span class="sxs-lookup"><span data-stu-id="f4043-132">Provide the name of the sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="f4043-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="f4043-134">Houd alles op dit scherm standaard.</span><span class="sxs-lookup"><span data-stu-id="f4043-134">Keep everything default on this screen.</span></span> <span data-ttu-id="f4043-135">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="f4043-135">Click **Finish**.</span></span>  
   <span data-ttu-id="f4043-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="f4043-137">Om te controleren of alles werkt zoals verwacht, klikt u op **gegevensbron testen**.</span><span class="sxs-lookup"><span data-stu-id="f4043-137">To verify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="f4043-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="f4043-139">Zorg ervoor dat de test is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="f4043-139">Make sure the test is successful.</span></span>  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="f4043-141">Het ODBC-configuratiebestand worden nu zichtbaar in de DSN-bestand.</span><span class="sxs-lookup"><span data-stu-id="f4043-141">The ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="f4043-143">We hebben nu het bestand we nodig en u kunt beginnen met het maken van de Connector.</span><span class="sxs-lookup"><span data-stu-id="f4043-143">We now have the file we need and can start creating the Connector.</span></span>

## <a name="create-the-generic-sql-connector"></a><span data-ttu-id="f4043-144">De algemene SQL-Connector maken</span><span class="sxs-lookup"><span data-stu-id="f4043-144">Create the Generic SQL Connector</span></span>
1. <span data-ttu-id="f4043-145">Selecteer in de UI Synchronization Service Manager **Connectors** en **maken**.</span><span class="sxs-lookup"><span data-stu-id="f4043-145">In the Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="f4043-146">Selecteer **algemene SQL (Microsoft)** en wijs hieraan een beschrijvende naam.</span><span class="sxs-lookup"><span data-stu-id="f4043-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="f4043-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="f4043-148">Zoek de DSN-bestand dat u in de vorige sectie hebt gemaakt en dit uploaden naar de server.</span><span class="sxs-lookup"><span data-stu-id="f4043-148">Find the DSN file you created in the previous section and upload it to the server.</span></span> <span data-ttu-id="f4043-149">Geef de referenties voor verbinding met de database.</span><span class="sxs-lookup"><span data-stu-id="f4043-149">Provide the credentials to connect to the database.</span></span>  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="f4043-151">In dit overzicht we zijn zodat u gemakkelijk voor ons en er zijn twee objecttypen spreken **gebruiker** en **groep**.</span><span class="sxs-lookup"><span data-stu-id="f4043-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="f4043-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="f4043-153">Ga voor de kenmerken, willen we de Connector voor het detecteren van deze kenmerken door te kijken naar de tabel zelf.</span><span class="sxs-lookup"><span data-stu-id="f4043-153">To find the attributes, we want the Connector to detect those attributes by looking at the table itself.</span></span> <span data-ttu-id="f4043-154">Aangezien **gebruikers** is een gereserveerd woord in SQL, moeten we opgeven in vierkante haken [].</span><span class="sxs-lookup"><span data-stu-id="f4043-154">Since **Users** is a reserved word in SQL, we need to provide it in square brackets [ ].</span></span>  
   <span data-ttu-id="f4043-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="f4043-156">Tijd om het ankerkenmerk en het kenmerk DN te definiëren.</span><span class="sxs-lookup"><span data-stu-id="f4043-156">Time to define the anchor attribute and the DN attribute.</span></span> <span data-ttu-id="f4043-157">Voor **gebruikers**, gebruiken we de combinatie van de twee kenmerken gebruikersnaam en het werknemer-id.</span><span class="sxs-lookup"><span data-stu-id="f4043-157">For **Users**, we use the combination of the two attributes username and EmployeeID.</span></span> <span data-ttu-id="f4043-158">Voor **groep**, gebruiken we GroupName (geen realistisch in de praktijk, maar voor dit scenario werkt).</span><span class="sxs-lookup"><span data-stu-id="f4043-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="f4043-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="f4043-160">Niet alle kenmerktypen kunnen worden gedetecteerd in een SQL-database.</span><span class="sxs-lookup"><span data-stu-id="f4043-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="f4043-161">Kan met name het kenmerk referentietype niet.</span><span class="sxs-lookup"><span data-stu-id="f4043-161">The reference attribute type in particular cannot.</span></span> <span data-ttu-id="f4043-162">Voor het objecttype van de groep moeten we de OwnerID en MemberID om te verwijzen naar wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f4043-162">For the group object type, we need to change the OwnerID and MemberID to reference.</span></span>  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="f4043-164">De kenmerken die we geselecteerd als verwijzingskenmerken in de vorige stap is vereist voor het objecttype deze waarden zijn een verwijzing naar.</span><span class="sxs-lookup"><span data-stu-id="f4043-164">The attributes we selected as reference attributes in the previous step require the object type these values are a reference to.</span></span> <span data-ttu-id="f4043-165">In ons geval typt u het gebruikersobject.</span><span class="sxs-lookup"><span data-stu-id="f4043-165">In our case, the User object type.</span></span>  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="f4043-167">Selecteer op de pagina Algemene Parameters **watermerk** als de delta-strategie.</span><span class="sxs-lookup"><span data-stu-id="f4043-167">On the Global Parameters page, select **Watermark** as the delta strategy.</span></span> <span data-ttu-id="f4043-168">Ook in de datum-/ tijdnotatie typen **jjjj-MM-dd: mm: SS**.</span><span class="sxs-lookup"><span data-stu-id="f4043-168">Also type in the date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="f4043-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="f4043-170">Op de **configureren partities en hiërarchieën** pagina, selecteert u beide objecttypen.</span><span class="sxs-lookup"><span data-stu-id="f4043-170">On the **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="f4043-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="f4043-172">Op de **objecttypen selecteren** en **kenmerken selecteren**, objecttypen en alle kenmerken selecteren.</span><span class="sxs-lookup"><span data-stu-id="f4043-172">On the **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="f4043-173">Op de **ankers configureren** pagina, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="f4043-173">On the **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="f4043-174">Uitvoeringsprofielen maken</span><span class="sxs-lookup"><span data-stu-id="f4043-174">Create Run Profiles</span></span>
1. <span data-ttu-id="f4043-175">Selecteer in de UI Synchronization Service Manager **Connectors**, en **Uitvoeringsprofielen configureren**.</span><span class="sxs-lookup"><span data-stu-id="f4043-175">In the Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="f4043-176">Klik op **nieuw profiel**.</span><span class="sxs-lookup"><span data-stu-id="f4043-176">Click **New Profile**.</span></span> <span data-ttu-id="f4043-177">We beginnen met **volledige Import**.</span><span class="sxs-lookup"><span data-stu-id="f4043-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="f4043-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="f4043-179">Selecteer het type **volledige Import (alleen Faseren)**.</span><span class="sxs-lookup"><span data-stu-id="f4043-179">Select the type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="f4043-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="f4043-181">Selecteer de partitie **OBJECT = gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="f4043-181">Select the partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="f4043-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="f4043-183">Selecteer **tabel** en het type **[gebruikers]**.</span><span class="sxs-lookup"><span data-stu-id="f4043-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="f4043-184">Schuif helemaal naar het gedeelte van het type object met meerdere waarden en voer de gegevens in de volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="f4043-184">Scroll down to the multi-valued object type section and enter the data as in the following picture.</span></span> <span data-ttu-id="f4043-185">Selecteer **voltooien** om op te slaan van de stap.</span><span class="sxs-lookup"><span data-stu-id="f4043-185">Select **Finish** to save the step.</span></span>  
   <span data-ttu-id="f4043-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="f4043-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="f4043-188">Selecteer **nieuwe stap**.</span><span class="sxs-lookup"><span data-stu-id="f4043-188">Select **New Step**.</span></span> <span data-ttu-id="f4043-189">Selecteer deze keer **OBJECT groep =**.</span><span class="sxs-lookup"><span data-stu-id="f4043-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="f4043-190">Gebruik de configuratie zoals in de volgende afbeelding op de laatste pagina.</span><span class="sxs-lookup"><span data-stu-id="f4043-190">On the last page, use the configuration as in the following picture.</span></span> <span data-ttu-id="f4043-191">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="f4043-191">Click **Finish**.</span></span>  
   <span data-ttu-id="f4043-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="f4043-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="f4043-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="f4043-194">Optioneel: Als u wilt, kunt u extra profielen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f4043-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="f4043-195">Voor dit scenario wordt alleen de volledige Import gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f4043-195">For this walkthrough, only the Full Import is used.</span></span>
7. <span data-ttu-id="f4043-196">Klik op **OK** voltooid uitvoeringsprofielen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f4043-196">Click **OK** to finish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-the-import"></a><span data-ttu-id="f4043-197">Sommige gegevens testen en testen van de invoer toevoegen</span><span class="sxs-lookup"><span data-stu-id="f4043-197">Add some test data and test the import</span></span>
<span data-ttu-id="f4043-198">Voer enkele testgegevens in de voorbeelddatabase.</span><span class="sxs-lookup"><span data-stu-id="f4043-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="f4043-199">Wanneer u klaar bent, selecteert u **uitvoeren** en **volledige import**.</span><span class="sxs-lookup"><span data-stu-id="f4043-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="f4043-200">Hier volgt een gebruiker met twee telefoonnummers en een groep met een aantal leden.</span><span class="sxs-lookup"><span data-stu-id="f4043-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![CS2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="f4043-203">Bijlage A</span><span class="sxs-lookup"><span data-stu-id="f4043-203">Appendix A</span></span>
<span data-ttu-id="f4043-204">**SQL-script voor het maken van de voorbeelddatabase**</span><span class="sxs-lookup"><span data-stu-id="f4043-204">**SQL script to create the sample database**</span></span>

```SQL
---Creating the Database---------
Create Database GSQLDEMO
Go
-------Using the Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```
