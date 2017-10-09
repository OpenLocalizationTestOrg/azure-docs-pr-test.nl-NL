---
title: stap aaaGeneric stap door de SQL-Connector | Microsoft Docs
description: Roulatie van dit artikel wordt u via een eenvoudige HR-systeem met behulp van stapsgewijze Hallo algemene SQL-Connector.
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
ms.openlocfilehash: b1b5f89ab588de6f92f173a7bc00f97180067669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="e2e7b-103">Algemene SQL Connector, stap voor stap</span><span class="sxs-lookup"><span data-stu-id="e2e7b-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="e2e7b-104">In dit onderwerp is een stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="e2e7b-105">Deze maakt een eenvoudig voorbeeld HR-database en deze gebruiken voor het importeren van sommige gebruikers en hun groepslidmaatschap.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-hello-sample-database"></a><span data-ttu-id="e2e7b-106">Hallo-voorbeelddatabase voorbereiden</span><span class="sxs-lookup"><span data-stu-id="e2e7b-106">Prepare hello sample database</span></span>
<span data-ttu-id="e2e7b-107">Op een server met SQL Server, voert u Hallo SQL-script is gevonden in [bijlage A](#appendix-a). Dit script maakt een voorbeelddatabase met Hallo naam GSQLDEMO.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-107">On a server running SQL Server, run hello SQL script found in [Appendix A](#appendix-a). This script creates a sample database with hello name GSQLDEMO.</span></span> <span data-ttu-id="e2e7b-108">Hallo-objectmodel voor Hallo gemaakt database lijkt erop deze afbeelding:</span><span class="sxs-lookup"><span data-stu-id="e2e7b-108">hello object model for hello created database looks like this picture:</span></span>  
<span data-ttu-id="e2e7b-109">![Objectmodel](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-109">![Object Model](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="e2e7b-110">Ook een gebruiker die u toouse tooconnect toohello database wilt maken.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-110">Also create a user you want toouse tooconnect toohello database.</span></span> <span data-ttu-id="e2e7b-111">In dit scenario is Hallo gebruiker FABRIKAM\SQLUser genoemd en in Hallo-domein bevinden.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-111">In this walkthrough, hello user is called FABRIKAM\SQLUser and located in hello domain.</span></span>

## <a name="create-hello-odbc-connection-file"></a><span data-ttu-id="e2e7b-112">Hallo ODBC-verbindingsbestand maken</span><span class="sxs-lookup"><span data-stu-id="e2e7b-112">Create hello ODBC connection file</span></span>
<span data-ttu-id="e2e7b-113">Hallo algemene SQL-Connector maakt gebruik van ODBC-tooconnect toohello externe server.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-113">hello Generic SQL Connector is using ODBC tooconnect toohello remote server.</span></span> <span data-ttu-id="e2e7b-114">Eerst moet u een bestand met de Hallo ODBC-verbindingsgegevens toocreate.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-114">First we need toocreate a file with hello ODBC connection information.</span></span>

1. <span data-ttu-id="e2e7b-115">Start Hallo ODBC-management-hulpprogramma op uw server:</span><span class="sxs-lookup"><span data-stu-id="e2e7b-115">Start hello ODBC management utility on your server:</span></span>  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="e2e7b-117">Selecteer Hallo tabblad **DSN-bestand**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-117">Select hello tab **File DSN**.</span></span> <span data-ttu-id="e2e7b-118">Klik op **toevoegen...** .</span><span class="sxs-lookup"><span data-stu-id="e2e7b-118">Click **Add...**.</span></span>  
   <span data-ttu-id="e2e7b-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="e2e7b-120">Hallo out-of-box stuurprogramma werkt fijn, dus te selecteren en op **volgende >**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-120">hello out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="e2e7b-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="e2e7b-122">Hallo-bestand, zoals een naam geven **GenericSQL**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-122">Give hello file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="e2e7b-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="e2e7b-124">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-124">Click **Finish**.</span></span>  
   <span data-ttu-id="e2e7b-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="e2e7b-126">Tijd tooconfigure Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-126">Time tooconfigure hello connection.</span></span> <span data-ttu-id="e2e7b-127">Hallo-gegevensbron een goede beschrijving geven en geef de naam Hallo van Hallo-server met SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-127">Give hello data source a good description and provide hello name of hello server running SQL Server.</span></span>  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="e2e7b-129">Selecteren hoe tooauthenticate met SQL.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-129">Select how tooauthenticate with SQL.</span></span> <span data-ttu-id="e2e7b-130">In dit geval gebruiken we Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="e2e7b-132">Hallo-naam van de voorbeelddatabase Hallo **GSQLDEMO**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-132">Provide hello name of hello sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="e2e7b-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="e2e7b-134">Houd alles op dit scherm standaard.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-134">Keep everything default on this screen.</span></span> <span data-ttu-id="e2e7b-135">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-135">Click **Finish**.</span></span>  
   <span data-ttu-id="e2e7b-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="e2e7b-137">tooverify alles werkt zoals verwacht, klikt u op **gegevensbron testen**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-137">tooverify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="e2e7b-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="e2e7b-139">Zorg ervoor dat het Hallo-test is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-139">Make sure hello test is successful.</span></span>  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="e2e7b-141">Hallo ODBC-configuratiebestand worden nu weergegeven in de DSN-bestand.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-141">hello ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="e2e7b-143">We hebben nu Hallo bestand we moeten en kunt beginnen met het maken van Hallo Connector.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-143">We now have hello file we need and can start creating hello Connector.</span></span>

## <a name="create-hello-generic-sql-connector"></a><span data-ttu-id="e2e7b-144">Hallo algemene SQL-Connector maken</span><span class="sxs-lookup"><span data-stu-id="e2e7b-144">Create hello Generic SQL Connector</span></span>
1. <span data-ttu-id="e2e7b-145">Selecteer in de Hallo Synchronization Service Manager UI, **Connectors** en **maken**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-145">In hello Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="e2e7b-146">Selecteer **algemene SQL (Microsoft)** en wijs hieraan een beschrijvende naam.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="e2e7b-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="e2e7b-148">Hallo u hebt gemaakt in de vorige sectie Hallo DSN-bestand vinden en upload het toohello-server.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-148">Find hello DSN file you created in hello previous section and upload it toohello server.</span></span> <span data-ttu-id="e2e7b-149">Hallo referenties tooconnect toohello database opgeven.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-149">Provide hello credentials tooconnect toohello database.</span></span>  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="e2e7b-151">In dit overzicht we zijn zodat u gemakkelijk voor ons en er zijn twee objecttypen spreken **gebruiker** en **groep**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="e2e7b-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="e2e7b-153">toofind hello kenmerken, willen we Hallo Connector toodetect die kenmerken door te kijken Hallo tabel zelf.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-153">toofind hello attributes, we want hello Connector toodetect those attributes by looking at hello table itself.</span></span> <span data-ttu-id="e2e7b-154">Aangezien **gebruikers** is een gereserveerd woord in SQL, moeten we tooprovide in vierkante haakjes [].</span><span class="sxs-lookup"><span data-stu-id="e2e7b-154">Since **Users** is a reserved word in SQL, we need tooprovide it in square brackets [ ].</span></span>  
   <span data-ttu-id="e2e7b-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="e2e7b-156">Tijd toodefine hello ankerkenmerk en Hallo DN-kenmerk.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-156">Time toodefine hello anchor attribute and hello DN attribute.</span></span> <span data-ttu-id="e2e7b-157">Voor **gebruikers**, gebruiken we Hallo combinatie van Hallo twee kenmerken username en werknemer-id.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-157">For **Users**, we use hello combination of hello two attributes username and EmployeeID.</span></span> <span data-ttu-id="e2e7b-158">Voor **groep**, gebruiken we GroupName (geen realistisch in de praktijk, maar voor dit scenario werkt).</span><span class="sxs-lookup"><span data-stu-id="e2e7b-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="e2e7b-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="e2e7b-160">Niet alle kenmerktypen kunnen worden gedetecteerd in een SQL-database.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="e2e7b-161">kan met name Hallo kenmerk referentietype niet.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-161">hello reference attribute type in particular cannot.</span></span> <span data-ttu-id="e2e7b-162">Voor het objecttype Hallo-groep moeten we toochange Hallo OwnerID en MemberID tooreference.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-162">For hello group object type, we need toochange hello OwnerID and MemberID tooreference.</span></span>  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="e2e7b-164">Hallo kenmerken we geselecteerd als verwijzingskenmerken in de vorige stap Hallo Hallo objecttype dat u deze waarden een verwijzing naar zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-164">hello attributes we selected as reference attributes in hello previous step require hello object type these values are a reference to.</span></span> <span data-ttu-id="e2e7b-165">In ons geval Hallo objecttype van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-165">In our case, hello User object type.</span></span>  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="e2e7b-167">Selecteer op de pagina Hallo globale Parameters **watermerk** als Hallo delta-strategie.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-167">On hello Global Parameters page, select **Watermark** as hello delta strategy.</span></span> <span data-ttu-id="e2e7b-168">Ook in datum-/ tijdnotatie Hallo typen **jjjj-MM-dd: mm: SS**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-168">Also type in hello date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="e2e7b-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="e2e7b-170">Op Hallo **configureren partities en hiërarchieën** pagina, selecteert u beide objecttypen.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-170">On hello **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="e2e7b-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="e2e7b-172">Op Hallo **objecttypen selecteren** en **kenmerken selecteren**, objecttypen en alle kenmerken selecteren.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-172">On hello **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="e2e7b-173">Op Hallo **ankers configureren** pagina, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-173">On hello **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="e2e7b-174">Uitvoeringsprofielen maken</span><span class="sxs-lookup"><span data-stu-id="e2e7b-174">Create Run Profiles</span></span>
1. <span data-ttu-id="e2e7b-175">Selecteer in de Hallo Synchronization Service Manager UI, **Connectors**, en **Uitvoeringsprofielen configureren**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-175">In hello Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="e2e7b-176">Klik op **nieuw profiel**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-176">Click **New Profile**.</span></span> <span data-ttu-id="e2e7b-177">We beginnen met **volledige Import**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="e2e7b-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="e2e7b-179">Selecteer Hallo type **volledige Import (alleen Faseren)**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-179">Select hello type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="e2e7b-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="e2e7b-181">Selecteer Hallo partitie **OBJECT = gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-181">Select hello partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="e2e7b-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="e2e7b-183">Selecteer **tabel** en het type **[gebruikers]**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="e2e7b-184">Schuif naar beneden toohello met meerdere waarden object type sectie en gegevens zoals in de volgende afbeelding Hallo Hallo invoeren.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-184">Scroll down toohello multi-valued object type section and enter hello data as in hello following picture.</span></span> <span data-ttu-id="e2e7b-185">Selecteer **voltooien** toosave Hallo stap.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-185">Select **Finish** toosave hello step.</span></span>  
   <span data-ttu-id="e2e7b-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="e2e7b-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="e2e7b-188">Selecteer **nieuwe stap**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-188">Select **New Step**.</span></span> <span data-ttu-id="e2e7b-189">Selecteer deze keer **OBJECT groep =**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="e2e7b-190">Op de laatste pagina Hallo Hallo-configuratie zoals in de volgende afbeelding hello te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-190">On hello last page, use hello configuration as in hello following picture.</span></span> <span data-ttu-id="e2e7b-191">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-191">Click **Finish**.</span></span>  
   <span data-ttu-id="e2e7b-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="e2e7b-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="e2e7b-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="e2e7b-194">Optioneel: Als u wilt, kunt u extra profielen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="e2e7b-195">Voor dit scenario alleen Hallo volledige Import wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-195">For this walkthrough, only hello Full Import is used.</span></span>
7. <span data-ttu-id="e2e7b-196">Klik op **OK** uitvoeringsprofielen toofinish wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-196">Click **OK** toofinish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-hello-import"></a><span data-ttu-id="e2e7b-197">Sommige test gegevens en test Hallo importeren toevoegen</span><span class="sxs-lookup"><span data-stu-id="e2e7b-197">Add some test data and test hello import</span></span>
<span data-ttu-id="e2e7b-198">Voer enkele testgegevens in de voorbeelddatabase.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="e2e7b-199">Wanneer u klaar bent, selecteert u **uitvoeren** en **volledige import**.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="e2e7b-200">Hier volgt een gebruiker met twee telefoonnummers en een groep met een aantal leden.</span><span class="sxs-lookup"><span data-stu-id="e2e7b-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![CS2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="e2e7b-203">Bijlage A</span><span class="sxs-lookup"><span data-stu-id="e2e7b-203">Appendix A</span></span>
<span data-ttu-id="e2e7b-204">**Hallo voorbeelddatabase voor SQL-script toocreate**</span><span class="sxs-lookup"><span data-stu-id="e2e7b-204">**SQL script toocreate hello sample database**</span></span>

```SQL
---Creating hello Database---------
Create Database GSQLDEMO
Go
-------Using hello Database-----------
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
