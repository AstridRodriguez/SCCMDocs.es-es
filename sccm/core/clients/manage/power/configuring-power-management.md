---
title: "Configuración de la administración de energía | System Center Configuration Manager"
description: "Configure la administración de energía en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ca1277ba0c2be68a393da930769151e25e997210


---
# <a name="configuring-power-management-in-system-center-configuration-manager"></a>Configuración de la administración de energía en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Para poder usar la administración de energía en System Center Configuration Manager, debe realizar los siguientes pasos de configuración.  

## <a name="enable-and-configure-power-management-client-settings"></a>Habilitar y configurar opciones de administración de energía  
 Este procedimiento configura las opciones de cliente predeterminadas para la administración de energía y se aplicará a todos los equipos de la jerarquía. Si quiere que esta configuración solo se aplique a algunos equipos, cree una configuración de cliente de dispositivo personalizada y asígnela a una recopilación que contenga los equipos en los que quiere usar la administración de energía. Para más información sobre cómo crear configuraciones de dispositivo personalizadas, vea [Cómo establecer la configuración del cliente en Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

#### <a name="to-enable-power-management-and-configure-client-settings"></a>Para habilitar y configurar opciones de administración de energía  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , haga clic en **Configuración de cliente**.  

3.  Haga clic en **Configuración de cliente predeterminada**.  

4.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

5.  En el cuadro de diálogo **Configuración de cliente predeterminada** , haga clic en **Administración de energía**.  

6.  Configure el siguiente valor para la configuración de cliente de administración de energía:  

    -   **Permitir la administración de energía de dispositivos** : en la lista desplegable, seleccione **Verdadero** para habilitar la administración de energía.  

7.  Configure las opciones de cliente que necesite. Para obtener una lista de las opciones de cliente de administración de energía que puede configurar, vea la sección [Administración de energía](../../../../core/clients/deploy/about-client-settings.md#BKMK_PowMgmtDeviceSettings) del tema [Acerca de la configuración de cliente en Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).  

8.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Configuración de cliente predeterminada** .  

 Los equipos cliente se configurarán con estas opciones la próxima vez que descarguen directivas de cliente. Para iniciar la recuperación de directivas para un solo cliente, vea [How to manage clients in System Center Configuration Manager (Cómo administrar clientes en System Center Configuration Manager)](../../../../core/clients/manage/manage-clients.md).  

## <a name="exclude-computers-from-power-management"></a>Excluir equipos de la administración de energía  
 Puede impedir que las recopilaciones de equipos reciban la configuración de administración de energía. Si un equipo es miembro de alguna recopilación que se excluye de la configuración de administración de energía, ese equipo no aplica la configuración de administración de energía, incluso si es miembro de otra recopilación que aplica la configuración de administración de energía.  

 Puede que quiera excluir equipos de la administración de energía por cualquiera de los siguientes motivos:  

-   Existe un requisito empresarial de que los equipos estén encendidos en todo momento.  

-   Ha creado una recopilación de control de los equipos en los que no quiere aplicar la configuración de administración de energía.  

-   Algunos de los equipos no tienen la capacidad para aplicar la configuración de administración de energía.  

-   Quiere excluir los equipos que ejecutan Windows Server de la administración de energía.  

> [!NOTE]  
>  Si se ha configurado la opción **Permitir a los usuarios excluir su dispositivo de la administración de energía** en la configuración de cliente, los usuarios pueden excluir sus propios equipos de la administración de energía mediante el Centro de software.  

 Para averiguar qué equipos se han excluido de la administración de energía, ejecute el informe **Equipos excluidos**. Para más información sobre este informe, vea [Equipos excluidos](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Excluded) en el tema [Cómo supervisar y planear la administración en el Administrador de configuración de energía](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

> [!IMPORTANT]  
>  La configuración de energía que se aplica a los equipos que ejecutan Windows XP o Windows Server 2003 no revierte a sus valores originales, aunque se excluya el equipo de la administración de energía. En versiones posteriores de Windows, la exclusión de un equipo de la administración de energía hace que toda la configuración de energía revierta a sus valores originales. No puede revertir una configuración de energía individual a sus valores originales.  

#### <a name="to-exclude-a-collection-of-computers-from-power-management"></a>Para excluir una recopilación de equipos de la administración de energía  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Recopilaciones de dispositivos**.  

3.  En la lista **Recopilaciones de dispositivos** , seleccione la recopilación que quiere excluir de la administración de energía y, a continuación, en la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

4.  En la pestaña **Administración de energía** del cuadro de diálogo *<Nombre de la colección>\>***Propiedades**, seleccione **No aplicar nunca la configuración de administración de energía en equipos de esta recopilación**.  

5.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo *<Nombre de la colección>\>***Propiedades** y guardar la configuración.  



<!--HONumber=Nov16_HO1-->

