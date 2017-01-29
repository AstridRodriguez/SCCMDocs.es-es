---
title: "Jerarquías de origen de migración | Microsoft Docs"
description: "Configure una jerarquía de origen y sitios de origen para poder migrar datos al entorno de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ccce7cb5-e18f-4337-8adf-2018edca3c00
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5e3d3f4194b06442e34c10988a20fe9ca40ac5d7
ms.openlocfilehash: 1ecac05cb7aba822047bbc519d8a0ca316c600a5


---
# <a name="configuring-source-hierarchies-and-source-sites-for-migration-to-system-center-configuration-manager"></a>Configurar jerarquías de origen y sitios de origen para la migración a System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Para habilitar la migración de datos al entorno de System Center Configuration Manager, debe configurar una jerarquía de origen de Configuration Manager compatible y uno o varios sitios de origen de esa jerarquía que contengan los datos que quiere migrar.  

> [!NOTE]  
>  Las operaciones de la migración se ejecutan en el sitio de nivel superior en la jerarquía de destino. Si configura la migración cuando use una consola de Configuration Manager conectada a un sitio primario secundario, debe dejar tiempo para que la configuración se replique en el sitio de administración central, para que se inicie y, luego, replique el estado de vuelta al sitio primario al que está conectado.  

 Utilice la información y los procedimientos de las secciones siguientes para especificar la jerarquía de origen y para agregar sitios de origen adicionales. Después de completar estos procedimientos, puede crear trabajos de migración y empezar a migrar datos de la jerarquía de origen a la jerarquía de destino.  

-   [Especificar una jerarquía de origen para la migración](#BKBM_ConfigSrcHierarchy)  

-   [Identificar sitios de origen adicionales de la jerarquía de origen](#BKBM_ConfigSrcSites)  

##  <a name="a-namebkbmconfigsrchierarchya-specify-a-source-hierarchy-for-migration"></a><a name="BKBM_ConfigSrcHierarchy"></a> Especificar una jerarquía de origen para la migración  
 Para migrar datos a la jerarquía de destino, debe especificar una jerarquía de origen compatible que contenga los datos que desee migrar. De forma predeterminada, el sitio de nivel superior de esa jerarquía se convierte en un sitio de origen de la jerarquía de origen. Si migra desde una jerarquía de Configuration Manager 2007, tras recopilar los datos del sitio de origen inicial, puede configurar sitios de origen adicionales para la migración. Si migra desde una jerarquía de System Center 2012 Configuration Manager o System Center Configuration Manager, no tiene que configurar sitios de origen adicionales para migrar datos desde la jerarquía de origen. Esto se debe a que estas versiones de Configuration Manager usan una base de datos compartida que está disponible en el sitio de nivel superior de la jerarquía de origen. La base de datos compartida contiene toda la información que puede migrar.  

 Use los procedimientos siguientes para especificar una jerarquía de origen para la migración y para identificar sitios de origen adicionales en una jerarquía de Configuration Manager 2007.  

 Realice este procedimiento con una consola de Configuration Manager que esté conectada a la jerarquía de destino.  

#### <a name="to-configure-a-source-hierarchy"></a>Para configurar una jerarquía de origen  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Migración**y, a continuación, haga clic en **Jerarquía de orígenes**.  

3.  En la pestaña **Inicio** , en el grupo **Migración** , haga clic en **Especificar la jerarquía de origen**.  

4.  En el cuadro de diálogo **Especificar la jerarquía de origen** para **Jerarquía de origen**, seleccione **Nueva jerarquía de origen**.  

5.  En **Servidor de sitio de Configuration Manager de nivel superior**, especifique el nombre o la dirección IP del sitio de nivel superior de una jerarquía de origen admitida.  

6.  Especifique cuentas de acceso del sitio de origen que tengan los siguientes permisos:  

    -   Cuenta de sitio de origen: permiso **Leer** del proveedor de SMS para el sitio de nivel superior especificado en la jerarquía de origen.  

    -   Cuenta de base de datos del sitio de origen: permisos **Leer** y **Ejecutar** de la base de datos de SQL Server para el sitio de nivel superior especificado en la jerarquía de origen.  

     Si especifica el uso de la cuenta de equipo, Configuration Manager usa la cuenta de equipo del sitio de nivel superior de la jerarquía de destino. Para esta opción, asegúrese de que esta cuenta sea miembro del grupo de seguridad **Usuarios COM distribuidos** en el dominio en el que reside el sitio de nivel superior de la jerarquía de origen.  

7.  Para compartir puntos de distribución entre las jerarquías de origen y de destino, active la casilla **Habilitar uso compartido del punto de distribución para el servidor de sitio de origen** . Si no habilita el uso compartido del punto de distribución en este momento, podrá hacerlo una vez completada la recopilación de datos mediante la edición de las credenciales del sitio de origen.  

8.  Haga clic en **Aceptar** para guardar la configuración. Se abrirá el cuadro de diálogo **Estado de obtención de datos** y la recopilación de los datos se iniciará automáticamente.  

9. Cuando finalice la obtención de datos, haga clic en **Cerrar** para cerrar el cuadro de diálogo **Estado de obtención de datos** y complete la configuración.  

##  <a name="a-namebkbmconfigsrcsitesa-identify-additional-source-sites-of-the-source-hierarchy"></a><a name="BKBM_ConfigSrcSites"></a> Identificar sitios de origen adicionales de la jerarquía de origen  
 Cuando se configura una jerarquía de origen compatible, el sitio de nivel superior de esa jerarquía se configura automáticamente como un sitio de origen y se recopilan datos automáticamente de ese sitio. La siguiente acción que realice depende de la versión de Configuration Manager que ejecute la jerarquía de origen:  

-   En una jerarquía de origen de Configuration Manager 2007, tras finalizar la recopilación de datos del sitio de origen inicial, puede comenzar la migración solamente desde ese sitio de origen inicial o configurar sitios de origen adicionales desde la jerarquía de origen. Se configurarían sitios de origen adicionales para una jerarquía de Configuration Manager 2007 para migrar datos que solo estuvieran disponibles en un sitio secundario. Por ejemplo, puede configurar sitios de origen adicionales para recopilar datos sobre el contenido que desea migrar cuando ese contenido se ha creado en un sitio secundario en la jerarquía de origen y no está disponible en el sitio superior de la jerarquía de origen.  

-   En una jerarquía de origen de System Center 2012 Configuration Manager o System Center Configuration Manager, no es necesario configurar sitios de origen adicionales. Esto se debe a que estas versiones de Configuration Manager usan una base de datos compartida que está disponible en el sitio de nivel superior de la jerarquía de origen. La base de datos compartida contiene toda la información que puede migrar desde todos los sitios de esa jerarquía de origen. Esto da como resultado que los datos que se pueden migrar estén disponibles desde el sitio de nivel superior de la jerarquía de origen.  

Cuando configure sitios de origen adicionales para una jerarquía de origen de Configuration Manager 2007, deberá configurar los sitios de origen adicionales desde la parte superior de la jerarquía de origen hasta la parte inferior. Debe configurar un sitio primario como un sitio de origen antes de configurar cualquiera de sus sitios secundarios como sitios de origen.  

Use el siguiente procedimiento para configurar sitios de origen adicionales para jerarquías de origen de Configuration Manager 2007.  

#### <a name="to-identify-additional-source-sites-in-the-source-hierarchy"></a>Para identificar sitios de origen adicionales en la jerarquía de origen  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Migración**y, a continuación, haga clic en **Jerarquía de orígenes**.  

3.  Haga clic en el sitio que desee configurar como un sitio de origen.  

4.  En la pestaña **Inicio** , en el grupo **Sitio de origen** , haga clic en **Configurar**.  

5.  En el cuadro de diálogo **Credenciales del sitio de origen** , para las cuentas de acceso del sitio de origen, especifique las cuentas que tengan los permisos siguientes:  

    -   Cuenta de sitio de origen: permiso **Leer** del proveedor de SMS para el sitio de nivel superior especificado en la jerarquía de origen.  

    -   Cuenta de base de datos del sitio de origen: permisos **Leer** y **Ejecutar** de la base de datos de SQL Server para el sitio de nivel superior especificado en la jerarquía de origen.  

    Si especifica el uso de la cuenta de equipo, Configuration Manager usa la cuenta de equipo del sitio de nivel superior de la jerarquía de destino. Para esta opción, asegúrese de que esta cuenta sea miembro del grupo de seguridad **Usuarios COM distribuidos** en el dominio en el que reside el sitio de nivel superior de la jerarquía de origen.  

6.  Para compartir puntos de distribución entre las jerarquías de origen y de destino, active la casilla **Habilitar uso compartido del punto de distribución para el servidor de sitio de origen** . Si no habilita el uso compartido del punto de distribución en este momento, podrá hacerlo una vez completada la recopilación de datos mediante la edición de las credenciales para el sitio de origen.  

7.  Haga clic en **Aceptar** para guardar la configuración. Se abrirá el cuadro de diálogo **Estado de obtención de datos** y la recopilación de los datos se iniciará automáticamente.  

8.  Cuando termine la recopilación de datos, haga clic en **Cerrar** para completar la configuración.  



<!--HONumber=Dec16_HO3-->

