---
title: Identifiera ditt partner-ID eller underdomän
description: Lär dig hur du identifierar ditt partner-ID eller underdomän när du implementerar vissa Experience Cloud-funktioner, och om två platser kan du få detta ID i användargränssnittet för Audience Manager.
feature: Implementation Basics
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2359
role: Developer, Data Engineer
level: Intermediate
exl-id: d3f4a12d-acc5-47b7-a38a-a6a14152bf3a
source-git-commit: 62b43b5627dabf754cf821f974a56c60989ef7ef
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Identifiera din Audience Manager-underdomän {#how-to-identify-your-audience-manager-partner-id-or-subdomain}

När du implementerar vissa Experience Cloud-funktioner måste du veta vad Audience Manager `Subdomain` kallas ibland `client ID` eller `Partner ID`). I den här videon visar vi två ställen där du kan få den här informationen i användargränssnittet för Audience Manager.

## Gav bort slutet.. {#giving-away-the-ending}

Om du hellre vill hitta den utan att titta på den här korta videon hittar du `Partner Subdomain` på två platser i användargränssnittet:

1. Om du redan har skapat en [!UICONTROL rule-based] egenskap, klicka **[!UICONTROL Get Trait URL]**
   [!UICONTROL Get Trait URL] står bredvid egenskapen i listan över egenskaper i den mappen, och URL:en kommer att inkludera din underdomän i URL:en.
1. Om du går in i **[!UICONTROL Tools]** > **[!UICONTROL Tags]** gränssnitt och klicka **[!UICONTROL Get code]** för behållaren är underdomänen mot slutet av Akamai-linjen

Om du inte snabbt hittar den med de här snabbreferenserna är videon ett kort åtagande. :)

>[!VIDEO](https://video.tv.adobe.com/v/25922/?quality=12)

>[!IMPORTANT]
>
>Varje kund i Adobe Experience Cloud tilldelas ett numeriskt ID, och detta kallas ofta för&quot;PID&quot; eller partner-ID. Detta är inte det ID som vi pratar om i den här artikeln och videon. I stället är &quot;partnerunderdomänen&quot;, som ibland kallas partner-ID, vanligtvis en version av klientnamnet och är underdomänen till servern som data skickas till. Om ditt företag till exempel är&quot;Bob&#39;s Knobs&quot; (alla saker är &quot;haha&quot;) är det troligt att din partnerunderdomän är&quot;bobsknobs&quot;, medan&quot;PID&quot; är något mer som&quot;12345&quot;. Du behöver vanligtvis inte känna till ditt PID, men din underdomän är viktig att känna till så att du kan konfigurera implementeringen av Audience Manager.
