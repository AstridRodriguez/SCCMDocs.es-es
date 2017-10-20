---
title: "Prueba de la actualización de la base de datos | Microsoft Docs"
description: "Pruebe la actualización de la base de datos de sitio al instalar actualizaciones para Configuration Manager."
ms.custom: na
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: abb696f3-a816-4f12-a9f1-0503a81e1976
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 6b76c97cd205bb02683a7bfa1eb378471a75551d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="test-the-database-upgrade-when-installing-an-update"></a>Prueba de la actualización de la base de datos al instalar una actualización

*Se aplica a: System Center Configuration Manager (rama actual)*

La información de este tema le ayudará a ejecutar una actualización de la base de datos de prueba antes de instalar una actualización en la consola de la Rama actual de Configuration Manager. Sin embargo, la actualización de prueba ya no es un paso necesario o recomendado a menos que la base de datos sea sospechosa o se haya modificado mediante personalizaciones no admitidas explícitamente por Configuration Manager.

## <a name="do-i-need-to-run-a-test-upgrade"></a>¿Es necesario ejecutar una actualización de prueba?
Esta actualización de prueba está en desuso debido a los cambios introducidos con System Center Configuration Manager. Estos cambios simplifican y aceleran el proceso por el que se puede actualizar un entorno de producción a las versiones más recientes. Este nuevo diseño se realizó para ayudar a los clientes a mantenerse al día con menos riesgos y reducir la sobrecarga operativa que implica la instalación de una nueva actualización.

Los cambios afectan al modo de instalar actualizaciones, como la lógica que revierte automáticamente una actualización con errores sin necesidad de ejecutar una recuperación del sitio. Estos cambios habilitan el uso de la consola para administrar las instalaciones de actualizaciones e incluyen una opción para [reintentar la instalación de una actualización con errores](/sccm/core/servers/manage/install-in-console-updates#bkmk_retry).

> [!TIP]
> Cuando se actualiza a System Center Configuration Manager desde un producto anterior, como System Center 2012 Configuration Manager, [se sigue recomendando la ejecución de actualizaciones de base de datos de prueba](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager#a-namebkmktesta-test-the-site-database-upgrade).

Si aún tiene previsto probar la actualización de una base de datos de sitio cuando instala una actualización en la consola, la información siguiente complementa las [instrucciones para instalar una actualización en la consola](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).

## <a name="prepare-to-run-a-test-database-upgrade"></a>Preparación de la ejecución de una actualización de la base de datos de prueba  
Antes de instalar una actualización nueva en la jerarquía, como la 1702, puede probar la actualización de la base de datos de sitio.

Para ejecutar la prueba de actualización, utilice el programa de instalación de Configuration Manager desde los archivos de origen, en la [carpeta CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder) de un sitio que ejecuta la versión de Configuration Manager a la que está actualizando. Este requisito implica que para probar la actualización de base de datos a la versión 1702 se necesita lo siguiente:
-   Debe tener al menos un sitio que ejecute la versión 1702 desde el que pueda obtener esa carpeta CD.Latest.
-   Si no tiene un sitio que ejecute la versión necesaria, considere la posibilidad de instalar un sitio en un entorno de laboratorio y, a continuación, actualice el sitio a la nueva versión. De este modo se crea la carpeta CD.Latest con la versión correcta de los archivos de origen.

La prueba de actualización se ejecuta en una copia de seguridad de la base de datos de sitio que restauró en una instancia independiente de SQL Server.  Ejecute el programa de instalación desde la carpeta **CD.Latest** con el conmutador de línea de comandos **testdbupgrade** para probar la actualización que restauró la copia de la base de datos. Una vez finalizada la actualización de prueba, se descarta la base de datos actualizada. Un sitio de Configuration Manager no puede utilizarla.

Si se produce un error de instalación de una actualización, no es necesario recuperar el sitio. En su lugar, puede intentar instalar de nuevo la actualización desde la consola.

##  <a name="run-the-test-upgrade"></a>Ejecución de la actualización de prueba    
1.  Utilice el programa de instalación de Configuration Manager y los archivos de origen de la carpeta **CD.Latest** de un sitio que ejecuta la versión a la que pretende actualizar.  

2.  Copie la carpeta **CD.Latest** en una ubicación de una instancia de SQL Server que vaya a usar para ejecutar la actualización de la base de datos de prueba.

3.  Cree una copia de seguridad de la base de datos de sitio cuya actualización desea probar. A continuación, restaure una copia de la base de datos de sitio en una instancia de SQL Server que no hospede un sitio de Configuration Manager. La instancia de SQL Server debe usar la misma edición de SQL Server que la base de datos de sitio.  

4.  Después de restaurar la copia de la base de datos, ejecute **el programa de instalación** desde la carpeta CD.Latest que contiene los archivos de origen de la versión a la que está actualizando. Cuando ejecute el programa de instalación, use la opción de línea de comandos **/TESTDBUPGRADE** . Si la instancia de SQL Server que hospeda la copia de la base de datos no es la instancia predeterminada, indique los argumentos de la línea de comandos para identificar la instancia que hospeda la copia de la base de datos del sitio.   

  Por ejemplo, tiene una base de datos de sitio con el nombre *SMS_ABC*. Restaura una copia de esta base de datos de sitio a una instancia compatible de SQL Server con el nombre de instancia *DBTest*. Para probar una actualización de esta copia de la base de datos del sitio, use la siguiente línea de comandos: **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**.  

  Puede encontrar Setup.exe en la siguiente ubicación del medio de origen de System Center Configuration Manager: **SMSSETUP\BIN\X64**.  

5.  En la instancia de SQL Server donde se ejecuta la prueba de la actualización, supervise el archivo *ConfigMgrSetup.log* en la raíz de la unidad del sistema para ver el progreso y si se completa correctamente.  

     En caso de que se produzca un error en la actualización de prueba, corrija los problemas relacionados con el error de actualización de la base de datos de sitio. A continuación, cree una nueva copia de seguridad de la base de datos de sitio y pruebe la actualización de la nueva copia de la base de datos.  



## <a name="next-steps"></a>Pasos siguientes
Cuando la actualización de la base de datos de prueba se haya completado correctamente, descarte la base de datos actualizada. Un sitio de Configuration Manager no puede utilizarla. A continuación, puede volver a su sitio activo y [comenzar la instalación de la actualización](/sccm/core/servers/manage/install-in-console-updates).