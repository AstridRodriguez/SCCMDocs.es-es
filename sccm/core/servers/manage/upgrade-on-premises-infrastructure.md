---
title: Actualizar la infraestructura local | System Center Configuration Manager
description: "Obtenga información sobre cómo actualizar la infraestructura, como SQL Server y el sistema operativo de sitio de los sistemas de sitio."
ms.custom: na
ms.date: 10/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c8115fba0722fc902e60ce201d8a9914036c1245
ms.openlocfilehash: 1239bf81991bb233a9640606bb47f598a70d5e50


---
# <a name="upgrade-on-premises-infrastructure-that-supports-system-center-configuration-manager"></a>Actualizar la infraestructura local que es compatible con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use la siguiente información para ayudarle a actualizar la infraestructura que ejecuta System Center Configuration Manager.  

##  <a name="a-namebkmksupconfigupgradesitesrva-upgrade-site-operating-system-of-site-systems"></a><a name="BKMK_SupConfigUpgradeSiteSrv"></a> Actualizar el sistema operativo de sitio de los sistemas de sitio  
 Configuration Manager admite la actualización local del sistema operativo de los servidores que hospedan un servidor de sitio y de los servidores remotos que hospedan cualquier rol de sistema de sitio en las situaciones siguientes:  

-   Actualización local a un Service Pack posterior de Windows Server si el nivel de Service Pack resultante de Windows sigue siendo compatible con Configuration Manager.  
-   Actualización local desde:
    - Windows Server 2012 R2 a Windows Server 2016 ([Ver detalles adicionales](#upgrade-windows-server-2012-r2-to-2016))
    - Windows Server 2012 a Windows Server 2012 R2 ([Ver detalles adicionales](#upgrade-windows-server-2012-to-windows-server-2012-r2))
    - Si usa la versión 1602 de Configuration Manager o una versión posterior, también se puede actualizar Windows Server 2008 R2 a Windows Server 2012 R2 ([Ver detalles adicionales](#upgrade-windows-server-2008-r2-to-windows-server-2012-r2))

    > [!WARNING]  
    >  Antes de actualizar a Windows Server 2012 R2, **debe desinstalar WSUS 3.2** del servidor.  
    >   
    >  Para obtener más información acerca de este paso crítico, consulte la sección Funcionalidad nueva y modificada en [Introducción a Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx) en la documentación de Windows Server.  

Para actualizar un servidor, use los procedimientos de actualización que proporciona el sistema operativo al que se va a actualizar.  Consulte lo siguiente:
  -  [Opciones de actualización para Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) en la documentación de Windows Server.  
  - [Opciones de actualización y conversión para Windows Server 2016](https://technet.microsoft.com/windows-server-docs/get-started/supported-upgrade-paths) en la documentación de Windows Server.

### <a name="upgrade-windows-server-2012-r2-to-2016"></a>Actualizar Windows Server 2012 R2 a 2016  
Este escenario de actualización de sistema operativo tiene las siguientes condiciones:

**Antes de la actualización:**  
-   Quite el cliente de System Center Endpoint Protection (SCEP). Windows Server 2016 tiene Windows Defender integrado, que reemplaza al cliente SCEP. La presencia del cliente SCEP puede impedir la actualización a Windows Server 2016.

**Después de la actualización:**
-   Asegúrese de que Windows Defender está habilitado, establecido para el inicio automático y en ejecución.
-   Asegúrese de que se ejecutan los siguientes servicios de Configuration Manager:
  -     SMS_EXECUTIVE
  -     SMS_SITE_COMPONENT_MANAGER


-   Asegúrese de que los servicios **Activación de proceso de Windows** y **WWW/W3svc** están habilitados, establecidos para el inicio automático y en ejecución en los siguientes roles de sistema de sitio (estos servicios se deshabilitan durante la actualización):
  -     Servidor de sitio
  -     Punto de administración
  -     Punto de servicio web del catálogo de aplicaciones
  -     Punto de sitios web del catálogo de aplicaciones


-   Asegúrese de que todos los servidores que hospedan un rol de sistema de sitio siguen cumpliendo todos los [requisitos previos para roles de sistema de sitio](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) que se ejecutan en ese servidor. Por ejemplo, puede que tenga que volver a instalar BITS, WSUS, o configurar valores específicos de IIS.

  Después de restaurar los requisitos previos que falten, reinicie el servidor una vez más para asegurarse de que los servicios se han iniciado y están operativos.

**Problema conocido de consolas remotas de Configuration Manager:**  
Después de actualizar el servidor de sitio o un servidor que hospeda una instancia de SMS_Provider para Windows Server 2016, es posible que los usuarios administrativos no puedan conectar una consola de Configuration Manager al sitio. Para evitar este problema, debe restaurar de forma manual los permisos del grupo de administradores de SMS en WMI. Los permisos deben establecerse en el servidor de sitio y en cada servidor remoto que hospeda una instancia del proveedor de SMS:

1. En los servidores aplicables, abra Microsoft Management Console (MMC), agregue el complemento de **Control WMI** y seleccione **Equipo local**.
2. En MMC, abra las **Propiedades** de **Control WMI (local)** y seleccione la pestaña **Seguridad**.
3. Expanda el árbol por debajo de la raíz, seleccione el nodo **SMS** y luego haga clic en **Seguridad**.  Asegúrese de que el grupo **Administradores de SMS** tiene los permisos siguientes:
  -     Habilitar cuenta
  -     Llamada remota habilitada
4. Después, en la pestaña **Seguridad**, bajo el nodo SMS, seleccione el nodo **site_<sitecode>** y después haga clic en **Seguridad**. Asegúrese de que el grupo de **administradores de SMS** tiene el permiso siguiente:
  -   Ejecutar métodos
  -   Escritura de proveedor
  -   Habilitar cuenta
  -   Llamada remota habilitada
5. Guarde los permisos para restaurar el acceso de la consola de Configuration Manager.

### <a name="windows-server-2012-to-windows-server-2012-r2"></a>Windows Server 2012 a Windows Server 2012 R2

**Antes de la actualización:**
-  A diferencia de los otros escenarios compatibles, este escenario no requiere consideraciones adicionales antes de la actualización.

**Después de la actualización:**
  - Asegúrese de que los servicios de implementación de Windows están iniciados y en ejecución para los siguientes roles de sistema de sitio (este servicio se detiene durante la actualización):
    - Servidor de sitio
    - Punto de administración
    - Punto de servicio web del catálogo de aplicaciones
    - Punto de sitios web del catálogo de aplicaciones


  -     Asegúrese de que los servicios **Activación de proceso de Windows** y **WWW/W3svc** están habilitados, establecidos para el inicio automático y en ejecución en los siguientes roles de sistema de sitio (estos servicios se deshabilitan durante la actualización):
    -   Servidor de sitio
    -   Punto de administración
    -   Punto de servicio web del catálogo de aplicaciones
    -   Punto de sitios web del catálogo de aplicaciones


  -     Asegúrese de que todos los servidores que hospedan un rol de sistema de sitio siguen cumpliendo todos los [requisitos previos para roles de sistema de sitio](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) que se ejecutan en ese servidor. Por ejemplo, puede que tenga que volver a instalar BITS, WSUS, o configurar valores específicos de IIS.

  Después de restaurar los requisitos previos que falten, reinicie el servidor una vez más para asegurarse de que los servicios se han iniciado y están operativos.

### <a name="upgrade-windows-server-2008-r2-to-windows-server-2012-r2"></a>Actualice Windows Server 2008 R2 a Windows Server 2012 R2
Este escenario de actualización de sistema operativo tiene las siguientes condiciones:  

**Antes de la actualización:**
-   Desinstale WSUS 3.2.  
    Antes de actualizar un sistema operativo de servidor a Windows Server 2012 R2, debe desinstalar WSUS 3.2 del servidor. Para obtener más información sobre este paso crítico, consulte la sección Funcionalidad nueva y modificada en Introducción a Windows Server Update Services en la documentación de Windows Server.

**Después de la actualización:**
  - Asegúrese de que los servicios de implementación de Windows están iniciados y en ejecución para los siguientes roles de sistema de sitio (este servicio se detiene durante la actualización):
    - Servidor de sitio
    - Punto de administración
    - Punto de servicio web del catálogo de aplicaciones
    - Punto de sitios web del catálogo de aplicaciones


  -     Asegúrese de que los servicios **Activación de proceso de Windows** y **WWW/W3svc** están habilitados, establecidos para el inicio automático y en ejecución en los siguientes roles de sistema de sitio (estos servicios se deshabilitan durante la actualización):
    -   Servidor de sitio
    -   Punto de administración
    -   Punto de servicio web del catálogo de aplicaciones
    -   Punto de sitios web del catálogo de aplicaciones


  -     Asegúrese de que todos los servidores que hospedan un rol de sistema de sitio siguen cumpliendo todos los [requisitos previos para roles de sistema de sitio](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) que se ejecutan en ese servidor. Por ejemplo, puede que tenga que volver a instalar BITS, WSUS, o configurar valores específicos de IIS.

  Después de restaurar los requisitos previos que falten, reinicie el servidor una vez más para asegurarse de que los servicios se han iniciado y están operativos.


### <a name="unsupported-upgrade-scenarios"></a>Escenarios de actualización no compatibles
Con frecuencia, se pregunta sobre los siguientes escenarios de actualización de Windows Server, pero no son compatibles con Configuration Manager:  

-   Windows Server 2008 a Windows Server 2012 o posterior  
-   Windows Server 2008 R2 a Windows Server 2012



##  <a name="a-namebkmksupconfigupgradeclienta-upgrade-the-operating-system-of-configuration-manager-clients"></a><a name="BKMK_SupConfigUpgradeClient"></a> Actualizar el sistema operativo de clientes de Configuration Manager  
 Configuration Manager admite una actualización local del sistema operativo para los clientes de Configuration Manager en las situaciones siguientes:  

-   Actualización local a un Service Pack posterior de Windows si el nivel de Service Pack resultante sigue siendo compatible con Configuration Manager.  

-   Actualización inmediata de Windows desde una versión compatible a Windows 10. Para más información, consulte [Actualizar Windows a la versión más reciente con System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   Actualizaciones de mantenimiento desde una compilación a otra de Windows 10.  Para más información, consulte [Administración de Windows como servicio mediante System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md).  

##  <a name="a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server"></a><a name="BKMK_SupConfigUpgradeDBSrv"></a> Actualizar SQL Server en el servidor de base de datos del sitio  
  Configuration Manager admite una actualización local de SQL Server desde una versión compatible de SQL en el servidor de base de datos del sitio. A continuación encontrará detalles sobre los escenarios de actualización de SQL Server compatibles con Configuration Manager y los requisitos para cada escenario.

 Para obtener más información sobre qué versiones de SQL Server son compatibles con Configuration Manager, consulte [Compatibilidad con versiones de SQL Server para System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

 **Actualizar la versión del Service Pack de SQL Server:**    
 Configuration Manager admite la actualización local de SQL Server a un Service Pack posterior si el nivel de Service Pack resultante de SQL Server sigue siendo compatible con Configuration Manager.

 Cuando hay varios sitios de Configuration Manager en una jerarquía, cada sitio puede ejecutar una versión diferente de Service Pack de SQL Server y no hay ninguna limitación para el orden en que los sitios actualizan la versión del Service Pack de SQL Server que se usa para la base de datos del sitio.

 **Actualizar a una nueva versión de SQL Server:**   
 Configuration Manager es compatible con la actualización local de SQL Server a las siguientes versiones:

 - SQL Server 2012  
 - SQL Server 2014  
 - SQL Server 2016  

Al actualizar la versión de SQL Server que hospeda la base de datos de sitio, debe actualizar la versión de SQL Server que se usa en los sitios en el siguiente orden:

 1. Actualice primero SQL Server en el sitio de administración central.
 2. Actualice los sitios secundarios antes de actualizar un sitio primario principal de un sitio secundario.
 3. Actualice los sitios primarios principales en último lugar. Esto incluye tanto los sitios primarios secundarios que dependen de un sitio de administración central como los sitios primarios independientes que están en el sitio de nivel superior de una jerarquía.



**Para obtener más información sobre SQL Server, consulte la documentación de SQL Server en TechNet:**  
-   [Actualización a SQL Server 2014](http://technet.microsoft.com/library/ms143393\(v=sql.120))  
-   [Actualización a SQL Server 2012](http://technet.microsoft.com/library/ms143393\(v=sql.110))
-   [Actualización a SQL Server 2016](https://technet.microsoft.com/library/bb677622(v=sql.130))



### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Para actualizar SQL Server en el servidor de base de datos del sitio  

1.  Detenga todos los servicios de Configuration Manager del sitio.  
2.  Actualice SQL Server a una versión compatible.  
3.  Reinicie los servicios de Configuration Manager.  

> [!NOTE]  
>  Al cambiar la edición de SQL Server en uso en el sitio de administración central desde una edición Standard a la edición Enterprise o Datacenter, la partición de la base de datos que limita el número de clientes que admite la jerarquía no cambia.



<!--HONumber=Nov16_HO1-->

