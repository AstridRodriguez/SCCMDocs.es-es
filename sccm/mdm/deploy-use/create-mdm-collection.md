---
title: "Creación de una colección de MDM mediante System Center Configuration Manager | Microsoft Docs"
description: "Cree una colección de MDM mediante System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d1b4337f-85e8-45e6-8bbe-9f18b49041c7
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: fabbcfd2d5656d4fa8cb87feffe87e17998df145
ms.lasthandoff: 03/06/2017

---
# <a name="create-an-mdm-collection-with-system-center-configuration-manager-and-microsoft-intune"></a>Creación de una colección de MDM con System Center Configuration Manager y Microsoft Intune

*Se aplica a: System Center Configuration Manager (rama actual)*

Se necesita una recopilación de usuarios de Configuration Manager para especificar qué usuarios pueden inscribir dispositivos en la administración. Solo puede usar recopilaciones de usuarios (en lugar de recopilaciones de dispositivos) porque las licencias de Intune se asignan por usuario.

> [!NOTE]
> Para inscribir dispositivos con Intune, no es necesario asignar licencias a los usuarios del portal de Office 365 o el portal de Azure Active Directory. Todo lo que necesita es incluir a los usuarios en una colección que se asocia a la suscripción de Intune (en un [paso posterior](configure-intune-subscription.md)).

Con fines de prueba, puede configurar una **regla directa** y agregar usuarios específicos que pueden inscribir dispositivos. En la consola de Configuration Manager, elija **Activos y compatibilidad** > **Recopilaciones de usuarios**, haga clic en la pestaña **Inicio** > grupo **Crear** y luego haga clic en **Crear recopilación de usuario**. Para una distribución más amplia, debe usar **reglas de consulta** para definir usuarios. Para obtener más información sobre las recopilaciones, consulte [Cómo crear recopilaciones](https://technet.microsoft.com/library/mt629371.aspx).

![Crear una recopilación de usuarios de MDM](../media/mdm-create-user-collection.png)

> [!div class="button"]
[Paso siguiente >](confirm-dns.md)
