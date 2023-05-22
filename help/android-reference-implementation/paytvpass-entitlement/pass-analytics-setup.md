---
description: Du kan ställa in referensimplementeringen så att den använder Adobe Analytics-rapportering.
title: Konfigurera Adobe Analytics Reporting
exl-id: 3607f9d4-1069-4722-af0b-121223125112
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# Konfigurera Adobe Analytics Reporting {#configure-adobe-analytics-reporting}

Du kan ställa in referensimplementeringen så att den använder Adobe Analytics-rapportering.

Referensimplementeringen är konfigurerad för att skicka händelsedata för Primetime-autentisering till Adobe Analytics med hjälp av Adobe Mobile Library som paketerats i Primetime SDK. Om du vill aktivera och använda händelsedata som skickas från programmet måste du först skapa ett Adobe Analytics-konto. När kontot har skapats:

1. Konfigurera programmet med din kontoinformation; och
1. Skapa bearbetningsregler för att anpassa hur händelsedata visas i dina rapporter.

Tabellen nedan visar de data som skickats till Adobe Analytics:

| Åtgärdsnamn | `a.media.pass.event.MvpdSelection` | Användaren valde en distributör av flerkanalsvideo (MVPD) i en valdialogruta |
|---|---|---|
| Kontextdata | `a.media.pass.MvpdId (String)` | Användarvalt MVPD |
|  | `a.media.pass.ClientType` | (String) Klienttypen är antingen &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; eller &quot;android&quot; |
|  |  |  |
| Åtgärdsnamn | `a.media.pass.event.AuthenticationDetection` | Ett autentiseringsarbetsflöde har slutförts |
| Kontextdata | `a.media.pass.Successful` | (Boolean) Om tokenbegäran lyckades, var true eller false |
|  | `a.media.pass.MvpdId` | (String) Användarvalt MVPD |
|  | `a.media.pass.Guid` | (Sträng) Ett spårnings-ID |
|  | `a.media.pass.Cached` | (Boolean) Token finns redan i cache, true eller false |
|  | `a.media.pass.ClientType` | (String) Klienttypen är antingen &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; eller &quot;android&quot; |
|  |  |  |
| Åtgärdsnamn | `a.media.pass.event.AuthorizationDetection` | Ett auktoriseringsarbetsflöde har slutförts |
| Kontextdata | `a.media.pass.Successful` | (Boolean) Om tokenbegäran lyckades, var true eller false |
|  | `a.media.pass.MvpdId` | (String) Användaren har valt MVPD |
|  | `a.media.pass.Guid` | (Sträng) Ett spårnings-ID |
|  | `a.media.pass.Cached` | (Boolean) Token finns redan i cache, true eller false |
|  | `a.media.pass.Error` | (String) Felet om auktoriseringsförsöket misslyckades |
|  | `a.media.pass.ErrorDetails` | (String) Ytterligare felinformation |
|  | `a.media.pass.ClientType` | (String) Klienttypen är antingen &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; eller &quot;android&quot; |

1. Konfigurera programmet för användning med Adobe Marketing Cloud.

   Om du vill att Primetime Primetime-autentiseringsdata ska kunna skickas till Adobe Analytics kan du [!DNL `ADBMobileConfig.json`] konfigurationsfilen måste läggas till i referensimplementeringen vid kompileringen. Observera att detta är exakt samma konfigurationsfil som används av Primetime SDK för att skicka videoanalysdata till Marketing Cloud. Läs [Adobe Marketing Cloud-dokumentation](https://microsite.omniture.com/t2/help/en_US/reference/) om du vill ha mer information om hur du konfigurerar ett program med ditt Adobe Analytics-konto.
1. Skapa bearbetningsregler.

   De händelsedata för autentisering av Primetime som skickas av referensimplementeringen visas inte automatiskt i dina analysrapporter. Du måste först använda data genom att skapa bearbetningsregler. Läs [Adobe Analytics-dokumentation om hur du skapar bearbetningsregler](https://microsite.omniture.com/t2/help/en_US/reference/processing_rules.html).
