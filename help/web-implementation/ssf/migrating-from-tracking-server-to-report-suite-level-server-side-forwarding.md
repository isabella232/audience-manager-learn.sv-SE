---
title: Migrera från spårningsserver till rapportservervidarebefordran på servernivå
description: I den här artikeln och videon visas hur du aktiverar vidarebefordran av analysdata på serversidan till Audience Manager på rapportsvitnivå i stället för på en spårningsservernivå.
product: audience manager, analytics
feature: integration with analytics
topics: null
audience: implementer
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1776
translation-type: tm+mt
source-git-commit: dfd549508cc223714bdb07ac6fd2aa31e6ca5586
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# Migrera från [!UICONTROL Tracking Server] till [!UICONTROL Report Suite]nivå [!UICONTROL Server-Side Forwarding] {#migrating-from-tracking-server-to-report-suite-level-server-side-forwarding}

I den här artikeln och videon visas hur du aktiverar [!UICONTROL server-side forwarding] data [!DNL Analytics] för Audience Manager på en [!UICONTROL report suite] nivå i stället för på en [!UICONTROL tracking server] nivå.

## Introduktion {#introduction}

Om du har Adobe Audience Manager OCH Adobe Analytics kan du implementera&quot;[!UICONTROL Server-side Forwarding]&quot; av [!DNL Analytics] data för Audience Manager. Det innebär att i stället för att sidan skickar 2 träffar (ett till [!DNL Analytics] och ett till Audience Manager) kan den bara skicka en träff till [!DNL Analytics]och [!DNL Analytics] vidarebefordra data till Audience Manager. Om du redan har detta i drift och om du hade det aktiverat/implementerat före oktober 2017 [!UICONTROL server-side forwarding] kan det bero på ditt&quot;[!UICONTROL Tracking Server]&quot;, som måste aktiveras av Adobe Customer Care eller Adobe Consulting. Från och med oktober 2017 kan du nu konfigurera [!UICONTROL server-side forwarding] dig själv och göra det på en [!UICONTROL Report Suite] nivå (vidarebefordran PER ER [!UICONTROL Report Suite]). Det finns viktiga fördelar med detta, som diskuteras nedan.

## [!UICONTROL Tracking Server] Vidarebefordra {#tracking-server-forwarding}

Ditt [!UICONTROL tracking server] är den plats dit du skickar dina [!DNL Analytics] data och den domän där bildbegäran och cookie-filen skrivs. Den ska ställas in i DTM eller [!DNL Experience Platform Launch], eller i [!DNL AppMeasurement.js] filen, och ska vanligtvis se ut så här, med din webbplats eller ditt företagsnamn som ersätter &quot;minwebbplats&quot;:

`s.trackingServer = "mysite.sc.omtrdc.net";`

Om [!UICONTROL server-side forwarding] är inställt för att vidarebefordra på [!UICONTROL tracking server] nivån vidarebefordras alla träffar som skickas till den här [!UICONTROL tracking server] (OM även Experience Cloud ID-tjänsten är aktiverad) till Audience Manager. Detta måste möjliggöras av Adobe kundtjänst eller Adobe Consulting. Det är också de som kan inaktivera det, EFTER att du har gått över till [!UICONTROL report suite] vidarebefordran enligt beskrivningen nedan.

Om du är osäker på om [!DNL tracking server forwarding] är aktiverat för dig kan du kontakta Adobe kundtjänst eller Adobe Consulting så att du kan få veta det.

## [!UICONTROL Report Suite]-Level [!UICONTROL Server-Side Forwarding] {#report-suite-level-server-side-forwarding}

En av de största fördelarna med att gå över till [!UICONTROL report suite] vidarebefordran från [!UICONTROL tracking server] vidarebefordran är att du nu kan använda &quot;Audience Analytics&quot;, som är möjligheten att vidarebefordra Audience Manager [!UICONTROL segments] tillbaka till Adobe Analytics för detaljerad [!UICONTROL segment] analys. Den här suveräna funktionen stöds INTE om du fortfarande [!UICONTROL tracking server] vidarebefordrar och inte [!UICONTROL report suite] vidarebefordrar. Mer information om Audience Analytics finns i [dokumentationen](https://marketing.adobe.com/resources/help/en_US/analytics/audiences/).

>[!VIDEO](https://video.tv.adobe.com/v/23701/?quality=12)

## Viktigt tips {#additional-resources}

Som framgår av videon ovan bör du kontakta Adobe kundtjänst eller Adobe Consulting och be dem inaktivera [!UICONTROL report suites] vidarebefordran när du har alla [!UICONTROL tracking server] planer på att vidarebefordra till Audience Manager. Det är inte akut för dig att göra detta, eftersom både [!UICONTROL tracking server] vidarebefordran och [!UICONTROL report suite] vidarebefordran INTE leder till dubbla träffar. Det är dock bäst att bara ha [!UICONTROL report suite] vidarebefordran aktiverat. Om du låter [!UICONTROL tracking server] vidarebefordran vara aktiverat kan det inte bara vidarebefordra data från [!UICONTROL report suites] som du inte vill vidarebefordra, utan i framtiden, när du (och alla på ditt företag) har glömt att [!UICONTROL tracking server] vidarebefordra data, kan du tro att data inte vidarebefordras för en specifik [!UICONTROL report suite] (eftersom den inte är aktiverad på rapportsvitnivå), men att data fortfarande vidarebefordras på grund av [!UICONTROL tracking server]. Sedan kommer du att slösa tid och pengar på att ta reda på varför det vidarebefordras och även betala för AAM serversamtal som du inte hade väntat dig. Så det är bara en bra idé att inaktivera [!UICONTROL tracking server] vidarebefordran så fort du har alla de [!UICONTROL report suites] alternativ som behövs för att utveckla ditt företag.
