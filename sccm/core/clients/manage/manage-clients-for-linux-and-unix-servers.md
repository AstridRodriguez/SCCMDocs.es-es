---
title: "Administración de clientes de UNIX y Linux | System Center Configuration Manager"
description: Administre clientes en servidores Linux y UNIX en System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
caps.latest.revision: 7
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d10b6876058d19d3a9a750a59267913d15793574


---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Cómo administrar clientes para servidores Linux y UNIX en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Cuando se administran los servidores Linux y UNIX con System Center Configuration Manager, se pueden configurar recopilaciones, ventanas de mantenimiento y configuraciones de cliente para ayudar a administrar los servidores. Además, aunque el cliente de Configuration Manager para Linux y UNIX no tiene una interfaz de usuario, puede forzar al cliente a sondear manualmente la directiva de cliente.

##  <a name="a-namebkmkcollectionsforlnua-collections-of-linux-and-unix-servers"></a><a name="BKMK_CollectionsforLnU"></a> Collections of Linux and UNIX servers  
 Se usan recopilaciones para administrar grupos de servidores Linux y UNIX de la misma forma que se usan recopilaciones para administrar otros tipos de cliente. Las recopilaciones pueden ser recopilaciones de pertenencia directa o recopilaciones basadas en consultas que identifican los sistemas operativos cliente, las configuraciones de hardware u otros detalles sobre el cliente que se almacenan en la base de datos del sitio. Por ejemplo, puede usar las recopilaciones que incluyen servidores Linux y UNIX para administrar lo siguiente:  

-   Configuración de cliente  

-   Implementaciones de software  

-   Aplicar ventanas de mantenimiento  

 Antes de poder identificar un cliente Linux o UNIX por su sistema operativo o distribución, debe recopilar el inventario de hardware de correctamente desde el cliente. Para obtener información acerca de la recopilación de inventario de hardware, consulte [Hardware inventory for Linux and UNIX in System Center Configuration Manager](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md) (Inventario de hardware para Linux y UNIX en System Center Configuration Manager).  

 La configuración de cliente predeterminada para el inventario de hardware incluye información sobre el sistema operativo del equipo de cliente. Puede usar la propiedad **Título** de la clase **Sistema operativo** para identificar el sistema operativo de un servidor Linux o UNIX.  

 Puede ver detalles sobre los equipos que ejecutan el cliente de Configuration Manager para Linux y UNIX en el nodo Dispositivos del área de trabajo Activos y compatibilidad en la consola de Configuration Manager. En el área de trabajo Activos y compatibilidad de la consola de Configuration Manager, puede ver el nombre del sistema operativo de cada equipo en la columna **Sistema operativo**.  

 De forma predeterminada, los servidores Linux y UNIX son miembros de la recopilación **Todos los sistemas** . Se recomienda crear recopilaciones personalizadas que incluyan solo servidores Linux y UNIX, o un subconjunto de ellos. Esto permite administrar operaciones como la implementación de software o la asignación de la configuración de cliente a grupos de equipos aplicables. Por ejemplo, si implementa software para equipos RHEL6 x64 en una recopilación que contiene equipos de Windows y Linux, el estado de la implementación aparecerá como parcialmente correcta. En su lugar, al implementar software en una recopilación que contiene solo equipos RHEL6 x64, puede usar mensajes de estado e informes para identificar con precisión el éxito de la implementación.  

 Cuando cree una recopilación personalizada para servidores Linux y UNIX, incluya consultas de regla de pertenencia que contengan el atributo de título para el atributo de sistema operativo. Para obtener más información sobre la creación de recopilaciones, consulte [How to create collections in System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md) (Creación de recopilaciones en System Center Configuration Manager).  

##  <a name="a-namebkmkmaintenancewindowsforlnua-maintenance-windows-for-linux-and-unix-servers"></a><a name="BKMK_MaintenanceWindowsforLnU"></a> Maintenance windows for Linux and UNIX servers  
 El cliente de Configuration Manager para servidores de Linux y UNIX admite el uso de ventanas de mantenimiento. Esta compatibilidad no se ha modificado para los clientes basados en Windows.  

 Para obtener más información sobre las ventanas de mantenimiento, consulte [How to use maintenance windows in System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md) (Uso de ventanas de mantenimiento en System Center Configuration Manager).  

##  <a name="a-namebkmkclientsettingsforlnua-client-settings-for-linux-and-unix-servers"></a><a name="BKMK_ClientSettingsforLnU"></a> Client settings for Linux and UNIX servers  
 Puede configurar las opciones de cliente que se aplican a servidores Linux y UNIX de la misma manera que configura las opciones para otros clientes.  

 De forma predeterminada, la **Configuración predeterminada del agente cliente** se aplica a servidores Linux y UNIX. También puede crear una configuración de cliente personalizada e implementarla en recopilaciones que contienen sistemas operativos cliente específicos, o una combinación de sistemas operativos de cliente.  

 No hay ninguna configuración de cliente adicional que se aplique solo a los clientes de Linux y UNIX. Sin embargo, hay configuración predeterminada de cliente que no se aplica a los clientes de Linux y UNIX. El cliente para Linux y UNIX solo aplica la configuración de funciones que admite y se omiten las configuraciones de funciones que no admite.  

 Por ejemplo, cuando crea una configuración de dispositivo de cliente personalizada que especifica una programación de inventario de hardware y, a continuación, asigna a una recopilación que incluye equipos Linux. El resultado es que la programación de inventario de hardware se aplica en los servidores Linux y UNIX. Luego, crea una configuración de dispositivo de cliente personalizada que se habilita y configura las opciones de control remoto y la asigna a esa misma colección. El resultado es que los servidores Linux y UNIX omiten la configuración de control remoto. Esto es porque el cliente para Linux y UNIX no es compatible con el control remoto en Configuration Manager.  

 Para obtener información acerca de cómo especificar la configuración de cliente, consulte [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md) (Configuración del cliente en System Center Configuration Manager).  

##  <a name="a-namebkmkpolicyforlnua-computer-policy-for-linux-and-unix-servers"></a><a name="BKMK_PolicyforLnU"></a> Computer policy for Linux and UNIX servers  
 El cliente de Configuration Manager para servidores Linux y UNIX sondee periódicamente en su sitio la directiva de equipo para obtener información sobre las configuraciones solicitadas y para comprobar las implementaciones.  

 También puede forzar al cliente en un servidor Linux o UNIX para que sondee inmediatamente la directiva de equipo. Para sondear inmediatamente, use las credenciales de **root** en el servidor para ejecutar el comando siguiente: **/opt/microsoft/configmgr/bin/ccmexec -rs policy**  

 Los detalles sobre el sondeo de la directiva de equipo se escriben en el archivo de registro de cliente compartido **scxcm.log**.  

> [!NOTE]  
>  El cliente de Configuration Manager para Linux y UNIX nunca solicita ni procesa la directiva de usuario.  

##  <a name="a-namebkmkmanagelinuxcertsa-how-to-manage-certificates-on-the-client-for-linux-and-unix"></a><a name="BKMK_ManageLinuxCerts"></a> How to manage certificates on the client for Linux and UNIX  
 Después de instalar el cliente para Linux y UNIX, puede usar la herramienta **certutil** para actualizar el cliente con un nuevo certificado PKI e importar una nueva lista de revocación de certificados (CRL). Al instalar el cliente para Linux y UNIX, esta herramienta se coloca en la siguiente ubicación: **/opt/microsoft/configmgr/bin/certutil**  

 Para administrar certificados, en cada cliente ejecute certutil con una de las siguientes opciones:  

|Opción|Más información|  
|------------|----------------------|  
|importPFX|Use esta opción para especificar un certificado que reemplace el certificado que actualmente usa un cliente.<br /><br /> Cuando use **-importPFX**, también debe usar el parámetro de línea de comandos **–password** para proporcionar la contraseña asociada con el archivo PKCS #12.<br /><br /> Use **-rootcerts** para especificar los requisitos de certificado raíz adicionales.<br /><br /> Ejemplo: **certutil -importPFX &lt;ruta de acceso al certificado PKCS #12> -password &lt;contraseña del certificado\> [-rootcerts&lt;lista separada por comas de certificados>]**|  
|-importsitecert|Use esta opción para actualizar el servidor de sitio que firma el certificado que se encuentra en el servidor de administración.<br /><br /> Ejemplo: **certutil -importsitecert &lt;ruta de acceso al certificado DER\>**|  
|-importcrl|Use esta opción para actualizar la CRL en el cliente con una o varias rutas de archivos CRL.<br /><br /> Ejemplo: **certutil -importcrl &lt;rutas de acceso de archivos CRL separados por comas\>**|  



<!--HONumber=Nov16_HO1-->

