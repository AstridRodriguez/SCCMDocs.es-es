---
title: Servicios de componentes y comandos de cliente UNIX/Linux | Microsoft Docs
description: "Obtenga información acerca de los servicios de componentes y comandos de clientes Linux y UNIX en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
caps.latest.revision: 6
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: 4a10d3a59aa6417857abc163dd5416f167049f65


---
# <a name="linux-and-unix-clients-component-services-and-commands-for-system-center-configuration-manager"></a>Servicios de componentes y comandos de clientes Linux y UNIX en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


 En la tabla siguiente se identifican los servicios del componente del cliente de Configuration Manager para Linux y UNIX.  

|Nombre del archivo|Más información|  
|---------------|----------------------|  
|ccmexec.bin|Este servicio es equivalente al servicio ccmexc en un cliente basado en Windows. Es responsable de todas las comunicaciones con los roles de sistema de sitio de Configuration Manager, y también se comunica con el servicio omiserver.bin para recopilar el inventario de hardware desde el equipo local.<br /><br /> Para obtener una lista de los argumentos de línea de comandos admitidos, ejecute **ccmexec -h**.|  
|omiserver.bin|Este servicio es el servidor CIM. El servidor CIM proporciona un marco para los módulos de software conectables denominados proveedores. Los proveedores interactúan con los recursos de equipos Linux y UNIX y recopilan los datos del inventario de hardware. Por ejemplo, el **proveedor proceso** para Linux equipo recopila datos asociados a los procesos del sistema operativo Linux.|  

 Los siguientes comandos de lista de tablas que se pueden usar para iniciar, detener o reiniciar los servicios de cliente (ccmexec.bin y omiserver.bin) en cada versión de Linux o UNIX. Al iniciar o detener el servicio ccmexec, el servicio omiserver también se inicia o se detiene.  

|Sistema operativo|Comandos:|  
|----------------------|--------------|  
|Universal Agent<br /><br /> RHEL 4 y SLES 9|Iniciar: **/etc/init d/ccmexecd start**<br /><br /> Detener: **/etc/init d/ccmexecd stop**<br /><br /> Reiniciar: **/etc/init d/ccmexecd restart**|  
|Solaris 9|Iniciar: **/etc/init d/ccmexecd start**<br /><br /> Detener: **/etc/init d/ccmexecd stop**<br /><br /> Reiniciar: **/etc/init d/ccmexecd restart**|  
|Solaris 10|Iniciar:<br /><br /> **svcadm enable -s svc:/application/management/omiserver**<br /><br /> **svcadm enable -s svc:/application/management/ccmexecd**<br /><br /> Detener:<br /><br /> **svcadm disable -s svc:/application/management/ccmexecd**<br /><br /> **svcadm disable -s svc:/application/management/omiserver**|  
|Solaris 11|Iniciar:<br /><br /> **svcadm enable -s svc:/application/management/omiserver**<br /><br /> **svcadm enable -s svc:/application/management/ccmexecd**<br /><br /> Detener:<br /><br /> **svcadm disable -s svc:/application/management/ccmexecd**<br /><br /> **svcadm disable -s svc:/application/management/omiserver**|  
|AIX|Iniciar:<br /><br /> **startsrc -s omiserver**<br /><br /> **startsrc -s ccmexec**<br /><br /> Detener:<br /><br /> **stopsrc -s ccmexec**<br /><br /> **stopsrc -s omiserver**|  
|HP-UX|Iniciar: **/sbin/init.d/ccmexecd start**<br /><br /> Detener: **/sbin/init.d/ccmexecd stop**<br /><br /> Reiniciar: **/sbin/init.d/ccmexecd restart**|  



<!--HONumber=Dec16_HO3-->

