---
title: Konfigurationsdata för global server
description: Konfigurationsdata för global server
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Konfigurationsdata för global server{#global-server-configuration-data}

Förutom den konfiguration som används av licensservern, `HandlerConfiguration` lagrar konfigurationsinformation som kan skickas till klienten för att styra hur licenser används. Detta görs genom att skapa en `ServerConfigData` klass och anrop `HandlerConfiguration.setServerConfigData()`. De här inställningarna gäller endast för licenser som utfärdas av den här licensservern.

Toleransen för klocktillbakaspolning är en egenskap som kan ställas in av licensservern för att styra hur klienten verkställer licenser. Som standard kan användare ställa in datorklockan fyra timmar tillbaka utan att göra licenserna ogiltiga. Om en licensserveroperator vill använda en annan inställning kan det nya värdet anges i `ServerConfigData` klassen. När du ändrar värdet för någon av dessa inställningar måste du öka versionsnumret genom att anropa `setVersion()`. De nya värdena skickas bara till klienten om klientversionen är äldre än den aktuella `ServerConfigData` version.
