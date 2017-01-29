---
title: Sincronizar directivas en dispositivos inscritos con Intune de manera remota | Microsoft Docs
description: "Obtener información sobre cómo sincronizar directivas en dispositivos inscritos con Intune desde la consola de Configuration Manager"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b3731ad0-2a24-4042-994e-5e4c1230e3fe
caps.latest.revision: 18
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dcdccc34fa55ce3d3e4459d209c7aeb74752214b
ms.openlocfilehash: c6496e9694314f1910ca944f6c083a9f3fd2bf79

---
# <a name="remotely-synchronize-policy-on-intune-enrolled-devices-from-the-configuration-manager-console"></a>Sincronizar directivas en dispositivos inscritos con Intune de manera remota desde la consola de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


Puede solicitar una sincronización de directivas en un dispositivo inscrito con Intune desde la consola de Configuration Manager, en lugar de solicitar una sincronización desde la aplicación de portal de empresa en el propio dispositivo. 

Para realizar esta tarea:

1.  Seleccione un dispositivo en **Activos y compatibilidad** > **Información general** > **Dispositivos**.
2.  Haga clic en **Send Sync Request (Enviar solicitud de sincronización)** en el menú **Acciones de dispositivo remoto**.


Después de cinco a diez minutos, cualquier cambio en la directiva se sincronizará con el dispositivo. Puede ver la información del estado de la solicitud de sincronización en una nueva columna en las vistas del dispositivo denominada **Remote Sync State (Estado de la sincronización remota)**, así como en la sección de datos de detección del cuadro de diálogo **Propiedades** de cada dispositivo.



<!--HONumber=Dec16_HO3-->

