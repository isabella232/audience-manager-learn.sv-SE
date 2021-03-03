---
title: Identifiera ditt Audience Manager partner-ID eller underdomän
description: När du implementerar vissa Experience Cloud-funktioner måste du veta vad ditt Audience Manager "partner-ID" är (kallas ibland även ditt "klient-ID" eller "underdomän"). I den här videon visar vi två platser där du kan få detta ID i användargränssnittet för Audience Manager.
feature: Implementeringsgrunder
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2359
role: '"Utvecklare, datatekniker"'
level: Mellanliggande
translation-type: tm+mt
source-git-commit: a7dc335e75697a7b1720eccdadbb9605fdeda798
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Identifiera din Audience Manager-underdomän {#how-to-identify-your-audience-manager-partner-id-or-subdomain}

När du implementerar vissa Experience Cloud-funktioner måste du veta vad din Audience Manager `Subdomain` är (kallas ibland `client ID` eller `Partner ID`). I den här videon visar vi två ställen där du kan få den här informationen i användargränssnittet för Audience Manager.

## Tar bort slutet... {#giving-away-the-ending}

Om du hellre vill hoppa in och hitta den utan att titta på den här korta videon kan du hitta din `Partner Subdomain` på två ställen i användargränssnittet:

1. Om du redan har skapat en [!UICONTROL rule-based] [!UICONTROL trait] klickar du på **[!UICONTROL Get Trait URL]**
   [!UICONTROL Get Trait URL] står bredvid  [!UICONTROL trait] i listan över  [!UICONTROL traits] i mappen och URL:en kommer att inkludera din underdomän i URL:en.
1. Om du går in i **[!UICONTROL Tools]** > **[!UICONTROL Tags]**-gränssnittet och klickar på **[!UICONTROL Get code]** för behållaren är underdomänen mot slutet av Akamai-raden

Om du inte snabbt hittar den med de här snabbreferenserna är videon ett kort åtagande. :)

>[!VIDEO](https://video.tv.adobe.com/v/25922/?quality=12)

>[!IMPORTANT]
>
>Varje kund i Adobe Experience Cloud tilldelas ett numeriskt ID, och detta kallas ofta för&quot;PID&quot; eller partner-ID. Detta är inte det ID som vi pratar om i den här artikeln och videon. I stället är &quot;partnerunderdomänen&quot;, som ibland kallas partner-ID, vanligtvis en version av klientnamnet och är underdomänen till servern som data skickas till. Om ditt företag till exempel är&quot;Bob&#39;s Knobs&quot; (alla saker är &quot;haha&quot;) är det troligt att din partnerunderdomän är&quot;bobsknobs&quot;, medan&quot;PID&quot; är något mer som&quot;12345&quot;. Du behöver vanligtvis inte känna till ditt PID, men din underdomän är viktig att känna till så att du kan konfigurera implementeringen av Audience Manager.

