---
title: Twitter gegevens analyseren met Apache Hive - Azure HDInsight | Microsoft Docs
description: Informatie over het gebruik van gebruik Hive en Hadoop in HDInsight voor het transformeren van onbewerkte gegevens van TWitter in een doorzoekbare Hive-tabel.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1e249ed-5f57-40d6-b3bc-a1b4d9a871d3
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: b8656123fa9c5158f366872ab050f370080ec18a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="analyze-twitter-data-using-hive-and-hadoop-on-hdinsight"></a><span data-ttu-id="c7a99-103">Twitter-gegevens met Hive en Hadoop op HDInsight analyseren</span><span class="sxs-lookup"><span data-stu-id="c7a99-103">Analyze Twitter data using Hive and Hadoop on HDInsight</span></span>

<span data-ttu-id="c7a99-104">Informatie over het gebruik van Apache Hive om gegevens van Twitter te verwerken.</span><span class="sxs-lookup"><span data-stu-id="c7a99-104">Learn how to use Apache Hive to process Twitter data.</span></span> <span data-ttu-id="c7a99-105">Het resultaat is een lijst met Twitter-gebruikers die de meeste tweets met een bepaald woord verzonden.</span><span class="sxs-lookup"><span data-stu-id="c7a99-105">The result is a list of Twitter users who sent the most tweets that contain a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7a99-106">De stappen in dit document zijn getest op HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="c7a99-106">The steps in this document were tested on HDInsight 3.6.</span></span>
>
> <span data-ttu-id="c7a99-107">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="c7a99-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c7a99-108">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c7a99-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="get-the-data"></a><span data-ttu-id="c7a99-109">De gegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="c7a99-109">Get the data</span></span>

<span data-ttu-id="c7a99-110">Twitter kunt u voor het ophalen van de [gegevens voor elke tweet](https://dev.twitter.com/docs/platform-objects/tweets) als een document notatie JSON (JavaScript Object) via een REST-API.</span><span class="sxs-lookup"><span data-stu-id="c7a99-110">Twitter allows you to retrieve the [data for each tweet](https://dev.twitter.com/docs/platform-objects/tweets) as a JavaScript Object Notation (JSON) document through a REST API.</span></span> <span data-ttu-id="c7a99-111">[OAuth](http://oauth.net) is vereist voor verificatie van de API.</span><span class="sxs-lookup"><span data-stu-id="c7a99-111">[OAuth](http://oauth.net) is required for authentication to the API.</span></span>

### <a name="create-a-twitter-application"></a><span data-ttu-id="c7a99-112">Een Twitter-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="c7a99-112">Create a Twitter application</span></span>

1. <span data-ttu-id="c7a99-113">Vanuit een webbrowser, moet u zich aanmelden bij [https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="c7a99-113">From a web browser, sign in to [https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="c7a99-114">Klik op de **nu aanmelden** koppelen als u een Twitter-account niet hebt.</span><span class="sxs-lookup"><span data-stu-id="c7a99-114">Click the **Sign-up now** link if you don't have a Twitter account.</span></span>

2. <span data-ttu-id="c7a99-115">Klik op **nieuwe App maken**.</span><span class="sxs-lookup"><span data-stu-id="c7a99-115">Click **Create New App**.</span></span>

3. <span data-ttu-id="c7a99-116">Voer **naam**, **beschrijving**, **Website**.</span><span class="sxs-lookup"><span data-stu-id="c7a99-116">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="c7a99-117">U kunt maken van een URL op voor de **Website** veld.</span><span class="sxs-lookup"><span data-stu-id="c7a99-117">You can make up a URL for the **Website** field.</span></span> <span data-ttu-id="c7a99-118">De volgende tabel ziet u enkele voorbeeldwaarden te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="c7a99-118">The following table shows some sample values to use:</span></span>

   | <span data-ttu-id="c7a99-119">Veld</span><span class="sxs-lookup"><span data-stu-id="c7a99-119">Field</span></span> | <span data-ttu-id="c7a99-120">Waarde</span><span class="sxs-lookup"><span data-stu-id="c7a99-120">Value</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="c7a99-121">Naam</span><span class="sxs-lookup"><span data-stu-id="c7a99-121">Name</span></span> |<span data-ttu-id="c7a99-122">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="c7a99-122">MyHDInsightApp</span></span> |
   | <span data-ttu-id="c7a99-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c7a99-123">Description</span></span> |<span data-ttu-id="c7a99-124">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="c7a99-124">MyHDInsightApp</span></span> |
   | <span data-ttu-id="c7a99-125">Website</span><span class="sxs-lookup"><span data-stu-id="c7a99-125">Website</span></span> |<span data-ttu-id="c7a99-126">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="c7a99-126">http://www.myhdinsightapp.com</span></span> |

4. <span data-ttu-id="c7a99-127">Controleer **Ja, ik ga akkoord**, en klik vervolgens op **uw Twitter-toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="c7a99-127">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>

5. <span data-ttu-id="c7a99-128">Klik op de **machtigingen** tabblad. Standaard de machtiging is **alleen-lezen**.</span><span class="sxs-lookup"><span data-stu-id="c7a99-128">Click the **Permissions** tab. The default permission is **Read only**.</span></span>

6. <span data-ttu-id="c7a99-129">Klik op de **sleutels en toegangstokens** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c7a99-129">Click the **Keys and Access Tokens** tab.</span></span>

7. <span data-ttu-id="c7a99-130">Klik op **maken van mijn toegangstoken**.</span><span class="sxs-lookup"><span data-stu-id="c7a99-130">Click **Create my access token**.</span></span>

8. <span data-ttu-id="c7a99-131">Klik op **Test OAuth** in de rechterbovenhoek van de pagina.</span><span class="sxs-lookup"><span data-stu-id="c7a99-131">Click **Test OAuth** in the upper-right corner of the page.</span></span>

9. <span data-ttu-id="c7a99-132">Noteer **consumentsleutel**, **consumentgeheim**, **toegangstoken**, en **Access token geheim**.</span><span class="sxs-lookup"><span data-stu-id="c7a99-132">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span>

### <a name="download-tweets"></a><span data-ttu-id="c7a99-133">Tweets downloaden</span><span class="sxs-lookup"><span data-stu-id="c7a99-133">Download tweets</span></span>

<span data-ttu-id="c7a99-134">De volgende Python-code downloadt 10.000 tweets van Twitter en sla ze naar een bestand met de naam **tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="c7a99-134">The following Python code downloads 10,000 tweets from Twitter and save them to a file named **tweets.txt**.</span></span>

> [!NOTE]
> <span data-ttu-id="c7a99-135">De volgende stappen worden uitgevoerd op het HDInsight-cluster omdat Python al is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="c7a99-135">The following steps are performed on the HDInsight cluster, since Python is already installed.</span></span>

1. <span data-ttu-id="c7a99-136">Maak verbinding met het HDInsight-cluster via SSH:</span><span class="sxs-lookup"><span data-stu-id="c7a99-136">Connect to the HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="c7a99-137">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c7a99-137">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="c7a99-138">Gebruik de volgende opdrachten voor het installeren van [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2), en andere vereiste pakketten:</span><span class="sxs-lookup"><span data-stu-id="c7a99-138">Use the following commands to install [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2), and other required packages:</span></span>

   ```bash
   sudo apt install python-dev libffi-dev libssl-dev
   sudo apt remove python-openssl
   pip install virtualenv
   mkdir gettweets
   cd gettweets
   virtualenv gettweets
   source gettweets/bin/activate
   pip install tweepy progressbar pyOpenSSL requests[security]
   ```

4. <span data-ttu-id="c7a99-139">Gebruik de volgende opdracht voor het maken van een bestand met de naam **gettweets.py**:</span><span class="sxs-lookup"><span data-stu-id="c7a99-139">Use the following command to create a file named **gettweets.py**:</span></span>

   ```bash
   nano gettweets.py
   ```

5. <span data-ttu-id="c7a99-140">Gebruik de volgende tekst als de inhoud van de **gettweets.py** bestand:</span><span class="sxs-lookup"><span data-stu-id="c7a99-140">Use the following text as the contents of the **gettweets.py** file:</span></span>

   ```python
   #!/usr/bin/python

   from tweepy import Stream, OAuthHandler
   from tweepy.streaming import StreamListener
   from progressbar import ProgressBar, Percentage, Bar
   import json
   import sys

   #Twitter app information
   consumer_secret='Your consumer secret'
   consumer_key='Your consumer key'
   access_token='Your access token'
   access_token_secret='Your access token secret'

   #The number of tweets we want to get
   max_tweets=10000

   #Create the listener class that receives and saves tweets
   class listener(StreamListener):
       #On init, set the counter to zero and create a progress bar
       def __init__(self, api=None):
           self.num_tweets = 0
           self.pbar = ProgressBar(widgets=[Percentage(), Bar()], maxval=max_tweets).start()

       #When data is received, do this
       def on_data(self, data):
           #Append the tweet to the 'tweets.txt' file
           with open('tweets.txt', 'a') as tweet_file:
               tweet_file.write(data)
               #Increment the number of tweets
               self.num_tweets += 1
               #Check to see if we have hit max_tweets and exit if so
               if self.num_tweets >= max_tweets:
                   self.pbar.finish()
                   sys.exit(0)
               else:
                   #increment the progress bar
                   self.pbar.update(self.num_tweets)
           return True

       #Handle any errors that may occur
       def on_error(self, status):
           print status

   #Get the OAuth token
   auth = OAuthHandler(consumer_key, consumer_secret)
   auth.set_access_token(access_token, access_token_secret)
   #Use the listener class for stream processing
   twitterStream = Stream(auth, listener())
   #Filter for these topics
   twitterStream.filter(track=["azure","cloud","hdinsight"])
   ```

    > [!IMPORTANT]
    > <span data-ttu-id="c7a99-141">Vervang de tijdelijke aanduiding voor de volgende items met de gegevens van twitter-toepassing:</span><span class="sxs-lookup"><span data-stu-id="c7a99-141">Replace the placeholder text for the following items with the information from your twitter application:</span></span>
    >
    > * `consumer_secret`
    > * `consumer_key`
    > * `access_token`
    > * `access_token_secret`

6. <span data-ttu-id="c7a99-142">Gebruik **Ctrl + X**, klikt u vervolgens **Y** het bestand wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="c7a99-142">Use **Ctrl + X**, then **Y** to save the file.</span></span>

7. <span data-ttu-id="c7a99-143">Gebruik de volgende opdracht voor het uitvoeren van het bestand en tweets downloaden:</span><span class="sxs-lookup"><span data-stu-id="c7a99-143">Use the following command to run the file and download tweets:</span></span>

    ```bash
    python gettweets.py
    ```

    <span data-ttu-id="c7a99-144">Er verschijnt een voortgangsindicator.</span><span class="sxs-lookup"><span data-stu-id="c7a99-144">A progress indicator appears.</span></span> <span data-ttu-id="c7a99-145">De functie telt tot wel 100% terwijl de tweets worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="c7a99-145">It counts up to 100% as the tweets are downloaded.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c7a99-146">Als het duurt lang voordat de voortgangsbalk om door te gaan, moet u het filter om bij te houden van trends onderwerpen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c7a99-146">If it is taking a long time for the progress bar to advance, you should change the filter to track trending topics.</span></span> <span data-ttu-id="c7a99-147">Wanneer er veel tweets over het onderwerp in het filter, krijgt u snel de 10000 tweets nodig.</span><span class="sxs-lookup"><span data-stu-id="c7a99-147">When there are many tweets about the topic in your filter, you can quickly get the 10000 tweets needed.</span></span>

### <a name="upload-the-data"></a><span data-ttu-id="c7a99-148">De gegevens uploaden</span><span class="sxs-lookup"><span data-stu-id="c7a99-148">Upload the data</span></span>

<span data-ttu-id="c7a99-149">Als u wilt de gegevens uploaden naar HDInsight-opslag, gebruikt u de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="c7a99-149">To upload the data to HDInsight storage, use the following commands:</span></span>

   ```bash
   hdfs dfs -mkdir -p /tutorials/twitter/data
   hdfs dfs -put tweets.txt /tutorials/twitter/data/tweets.txt
```

<span data-ttu-id="c7a99-150">Deze opdrachten worden de gegevens opslaan op een locatie die toegankelijk is voor alle knooppunten in het cluster.</span><span class="sxs-lookup"><span data-stu-id="c7a99-150">These commands store the data in a location that all nodes in the cluster can access.</span></span>

## <a name="run-the-hiveql-job"></a><span data-ttu-id="c7a99-151">Voer de taak HiveQL</span><span class="sxs-lookup"><span data-stu-id="c7a99-151">Run the HiveQL job</span></span>

1. <span data-ttu-id="c7a99-152">Gebruik de volgende opdracht voor het maken van een bestand met HiveQL-instructies:</span><span class="sxs-lookup"><span data-stu-id="c7a99-152">Use the following command to create a file containing HiveQL statements:</span></span>

   ```bash
   nano twitter.hql
   ```

    <span data-ttu-id="c7a99-153">Gebruik de volgende tekst als de inhoud van het bestand:</span><span class="sxs-lookup"><span data-stu-id="c7a99-153">Use the following text as the contents of the file:</span></span>

   ```hiveql
   set hive.exec.dynamic.partition = true;
   set hive.exec.dynamic.partition.mode = nonstrict;
   -- Drop table, if it exists
   DROP TABLE tweets_raw;
   -- Create it, pointing toward the tweets logged from Twitter
   CREATE EXTERNAL TABLE tweets_raw (
       json_response STRING
   )
   STORED AS TEXTFILE LOCATION '/tutorials/twitter/data';
   -- Drop and recreate the destination table
   DROP TABLE tweets;
   CREATE TABLE tweets
   (
       id BIGINT,
       created_at STRING,
       created_at_date STRING,
       created_at_year STRING,
       created_at_month STRING,
       created_at_day STRING,
       created_at_time STRING,
       in_reply_to_user_id_str STRING,
       text STRING,
       contributors STRING,
       retweeted STRING,
       truncated STRING,
       coordinates STRING,
       source STRING,
       retweet_count INT,
       url STRING,
       hashtags array<STRING>,
       user_mentions array<STRING>,
       first_hashtag STRING,
       first_user_mention STRING,
       screen_name STRING,
       name STRING,
       followers_count INT,
       listed_count INT,
       friends_count INT,
       lang STRING,
       user_location STRING,
       time_zone STRING,
       profile_image_url STRING,
       json_response STRING
   );
   -- Select tweets from the imported data, parse the JSON,
   -- and insert into the tweets table
   FROM tweets_raw
   INSERT OVERWRITE TABLE tweets
   SELECT
       cast(get_json_object(json_response, '$.id_str') as BIGINT),
       get_json_object(json_response, '$.created_at'),
       concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
       substr (get_json_object(json_response, '$.created_at'),27,4)),
       substr (get_json_object(json_response, '$.created_at'),27,4),
       case substr (get_json_object(json_response,    '$.created_at'),5,3)
           when "Jan" then "01"
           when "Feb" then "02"
           when "Mar" then "03"
           when "Apr" then "04"
           when "May" then "05"
           when "Jun" then "06"
           when "Jul" then "07"
           when "Aug" then "08"
           when "Sep" then "09"
           when "Oct" then "10"
           when "Nov" then "11"
           when "Dec" then "12" end,
       substr (get_json_object(json_response, '$.created_at'),9,2),
       substr (get_json_object(json_response, '$.created_at'),12,8),
       get_json_object(json_response, '$.in_reply_to_user_id_str'),
       get_json_object(json_response, '$.text'),
       get_json_object(json_response, '$.contributors'),
       get_json_object(json_response, '$.retweeted'),
       get_json_object(json_response, '$.truncated'),
       get_json_object(json_response, '$.coordinates'),
       get_json_object(json_response, '$.source'),
       cast (get_json_object(json_response, '$.retweet_count') as INT),
       get_json_object(json_response, '$.entities.display_url'),
       array(
           trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
       array(
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
       trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
       trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
       get_json_object(json_response, '$.user.screen_name'),
       get_json_object(json_response, '$.user.name'),
       cast (get_json_object(json_response, '$.user.followers_count') as INT),
       cast (get_json_object(json_response, '$.user.listed_count') as INT),
       cast (get_json_object(json_response, '$.user.friends_count') as INT),
       get_json_object(json_response, '$.user.lang'),
       get_json_object(json_response, '$.user.location'),
       get_json_object(json_response, '$.user.time_zone'),
       get_json_object(json_response, '$.user.profile_image_url'),
       json_response
   WHERE (length(json_response) > 500);
   ```

2. <span data-ttu-id="c7a99-154">Druk op **Ctrl + X**, drukt u vervolgens op **Y** het bestand wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="c7a99-154">Press **Ctrl + X**, then press **Y** to save the file.</span></span>
3. <span data-ttu-id="c7a99-155">Gebruik de volgende opdracht om uit te voeren van de HiveQL opgenomen in het bestand:</span><span class="sxs-lookup"><span data-stu-id="c7a99-155">Use the following command to run the HiveQL contained in the file:</span></span>

   ```bash
   beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i twitter.hql
   ```

    <span data-ttu-id="c7a99-156">Met deze opdracht wordt uitgevoerd de de **twitter.hql** bestand.</span><span class="sxs-lookup"><span data-stu-id="c7a99-156">This command runs the the **twitter.hql** file.</span></span> <span data-ttu-id="c7a99-157">Nadat de query is voltooid, ziet u een `jdbc:hive2//localhost:10001/>` prompt.</span><span class="sxs-lookup"><span data-stu-id="c7a99-157">Once the query completes, you see a `jdbc:hive2//localhost:10001/>` prompt.</span></span>

4. <span data-ttu-id="c7a99-158">Gebruik de volgende query om te controleren dat de gegevens zijn geïmporteerd achter de opdrachtprompt beeline:</span><span class="sxs-lookup"><span data-stu-id="c7a99-158">From the beeline prompt, use the following query to verify that data was imported:</span></span>

   ```hiveql
   SELECT name, screen_name, count(1) as cc
       FROM tweets
       WHERE text like "%Azure%"
       GROUP BY name,screen_name
       ORDER BY cc DESC LIMIT 10;
   ```

    <span data-ttu-id="c7a99-159">Deze query retourneert maximaal 10 tweets met het woord **Azure** in de berichttekst.</span><span class="sxs-lookup"><span data-stu-id="c7a99-159">This query returns a maximum of 10 tweets that contain the word **Azure** in the message text.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7a99-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c7a99-160">Next steps</span></span>

<span data-ttu-id="c7a99-161">U hebt geleerd hoe u een niet-gestructureerde JSON-gegevensset transformeren naar een gestructureerde Hive-tabel.</span><span class="sxs-lookup"><span data-stu-id="c7a99-161">You have learned how to transform an unstructured JSON dataset into a structured Hive table.</span></span> <span data-ttu-id="c7a99-162">Zie de volgende documenten voor meer informatie over Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c7a99-162">To learn more about Hive on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="c7a99-163">Aan de slag met HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7a99-163">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="c7a99-164">Vertraging vluchtgegevens met HDInsight analyseren</span><span class="sxs-lookup"><span data-stu-id="c7a99-164">Analyze flight delay data using HDInsight</span></span>](hdinsight-analyze-flight-delay-data-linux.md)

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter
