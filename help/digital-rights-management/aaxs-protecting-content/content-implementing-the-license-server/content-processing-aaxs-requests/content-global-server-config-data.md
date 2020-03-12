---
seo-title: Konfigurationsdata för global server
title: Konfigurationsdata för global server
uuid: f6d6cb01-2645-4cd2-83ec-0272323a67cd
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Konfigurationsdata för global server{#global-server-configuration-data}

Förutom den konfiguration som används av licensservern `HandlerConfiguration` lagrar konfigurationsinformation som kan skickas till klienten för att styra hur licenser upprätthålls. Detta gör du genom att skapa en `ServerConfigData` klass och anropa `HandlerConfiguration.setServerConfigData()` (dessa inställningar gäller endast för licenser som utfärdas av den här licensservern). Toleransen för klocktillbakaspolning är en egenskap som kan ställas in av licensservern för att styra hur klienten verkställer licenser. Som standard kan användare ställa in datorklockan fyra timmar tillbaka utan att göra licenserna ogiltiga. Om en licensserveroperator vill använda en annan inställning kan det nya värdet anges i `ServerConfigData` klassen. När du ändrar värdet för någon av dessa inställningar måste du öka versionsnumret genom att anropa `setVersion()`. De nya värdena skickas endast till klienten om klientversionen är mindre än den aktuella `ServerConfigData` versionen.
