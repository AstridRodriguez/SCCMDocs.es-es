---
title: "Tareas de administración para aplicaciones de System Center Configuration Manager | System Center Configuration Manager"
description: "Administre tipos de implementación y aplicaciones de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c4041e21-21ff-4d95-ab05-14007e0047cf
caps.latest.revision: 8
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b8ecf5334304f0aaae62b3fa5d6f84da84d97799


---
# <a name="management-tasks-for-system-center-configuration-manager-applications"></a>Tareas de administración de aplicaciones de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Utilice la información de este tema como ayuda para administrar tipos de implementación y aplicaciones de System Center Configuration Manager.  
  
Para obtener más información sobre la creación de aplicaciones y los tipos de implementación, consulte [Create applications](../../apps/deploy-use/create-applications.md) (Creación de aplicaciones).  
  
> [!IMPORTANT]  
>  En función del tipo de aplicación o implementación, algunas de las opciones de administración no están disponibles.  

##  <a name="manage-applications"></a>Administración de aplicaciones  
 En el área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** > **Aplicaciones**, seleccione la aplicación que desea administrar y, a continuación, seleccione una tarea de administración.  
  
|Tarea|Detalles|  
|----------|-------------|  
|**Administrar cuentas de acceso**|Se abre el cuadro de diálogo **Administrar cuentas de acceso** , en el que podrá especificar el nivel de acceso que se permite para el contenido asociado a la aplicación seleccionada.|  
|**Crear archivo de contenido preconfigurado**|Se abre el **Asistente para crear archivos de contenido preconfigurados** que le ayuda a administrar la distribución de contenido en puntos de distribución remotos. Cuando la programación y la limitación no proporcionan una solución válida para el punto de distribución remoto, puede preconfigurar el contenido en el punto de distribución<br /><br /> Consulte [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Administración de contenido e infraestructura de contenido).|  
|**Historial de revisiones**|Abre el cuadro de diálogo **Historial de revisiones de la aplicación** , que le permite visualizar las propiedades de las revisiones realizadas en esta aplicación, eliminar revisiones antiguas y restaurar versiones antiguas de esta aplicación.<br /><br /> Consulte [Revise and supersede applications](../../apps/deploy-use/revise-and-supersede-applications.md) (Revisión y sustitución de aplicaciones).|  
|**Crear tipo de implementación**|Abre el **Asistente para crear tipos de implementación** , que le permite agregar un nuevo tipo de implementación a la aplicación seleccionada.<br /><br /> Consulte [Create applications](../../apps/deploy-use/create-applications.md) (Creación de aplicaciones).|  
|**Actualizar estadísticas**|Actualiza la información que se muestra en el nodo **Implementaciones** del área de trabajo **Supervisión** sobre las implementaciones de esta aplicación.<br /><br /> Consulte [Monitor applications from the System Center Configuration Manager console](../../apps/deploy-use/monitor-applications-from-the-console.md) (Supervisión de aplicaciones desde la consola de System Center Configuration Manager).|  
|**Restablecer**|Esta opción restablece una aplicación retirada anteriormente mediante el uso de la tarea de administración **Retirar** .|  
|**Retirar**|Cuando se retira una aplicación, dejará de estar disponible para la implementación. Sin embargo, la aplicación y sus implementaciones no se eliminan. No se quitarán las copias existentes de la aplicación que se instalaron en equipos cliente. Todos los cambios hechos en la aplicación se eliminarán de Configuration Manager transcurridos 60 días. Sin embargo, las copias instaladas de la aplicación no se eliminan.<br /><br /> Para eliminar una aplicación debe retirarla, eliminar todas las implementaciones, quitar las referencias de otras implementaciones a la aplicación y, a continuación, eliminar todas sus revisiones.<br /><br /> See [Revise and supersede applications](../../apps/deploy-use/revise-and-supersede-applications.md) (Revisión y sustitución de aplicaciones).|  
|**Exportarar**|Abre el **Asistente para exportar aplicaciones** que permite exportar las aplicaciones seleccionadas en un archivo .zip que se puede archivar o instalar en otro sitio. Si decide exportar el contenido de una aplicación, se creará una carpeta con el contenido.<br /><br /> También puede exportar las dependencias de aplicación, las relaciones de sustitución y las condiciones y el contenido de la aplicación y de sus dependencias.<br /><br /> El cmdlet de Windows PowerShell **Export-CMApplication**realiza la misma función. Para obtener más información, consulte [http://go.microsoft.com/fwlink/p/?LinkID=258880](http://go.microsoft.com/fwlink/p/?LinkID=258880) en la documentación de referencia del cmdlet de Microsoft System Center 2012 Configuration Manager SP1.|  
|**Eliminar**|Elimina la aplicación seleccionada.<br /><br /> No se puede eliminar una aplicación si otras aplicaciones dependen de la misma, si tiene una implementación activa o si tiene secuencias de tareas dependientes.|  
|**Simular implementación**|Abre el **Asistente para simular implementación de aplicación** , en el que puede probar el resultado de una implementación de aplicación en equipos sin instalar o desinstalar la aplicación.<br /><br /> Consulte [Simulate application deployments](../../apps/deploy-use/simulate-application-deployments.md) (Simulación de implementaciones de aplicaciones).|  
|**Implementar**|Abre el **Asistente para implementar software** , en el que puede implementar la aplicación seleccionada en recopilaciones de equipos en su jerarquía.<br /><br /> Consulte [Deploy applications](../../apps/deploy-use/deploy-applications.md) (Implementación de aplicaciones).|  
|**Distribuir contenido**|Abre el **Asistente para distribuir contenido** , en el que puede copiar el contenido de la aplicación seleccionada en puntos de distribución en la jerarquía.<br /><br /> Consulte [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Administración de contenido e infraestructura de contenido).|  
|**Ver relaciones**|Permite visualizar un diagrama gráfico que muestra las relaciones de las aplicaciones seleccionadas con otras aplicaciones. Elija una de las siguientes opciones:<br><br> - **Dependencia**: muestra las aplicaciones que dependen de la aplicación seleccionada y las aplicaciones de las que la aplicación seleccionada depende.<br>-                    **Sustitución**: muestra las aplicaciones que el elemento seleccionado sustituye, y las aplicaciones que sustituyen al elemento seleccionado.<br>- **Condiciones globales**: muestra las condiciones globales a las que esta aplicación hace referencia.<br /><br /> Consulte [Revise and supersede applications](../../apps/deploy-use/revise-and-supersede-applications.md) (Revisión y sustitución de aplicaciones) y [Cómo crear condiciones globales](../../apps/deploy-use/create-global-conditions.md).|  
  
##  <a name="manage-deployment-types"></a>Administración de tipos de implementaciones  
 En el área de trabajo **Biblioteca de software** , expanda **Administración de aplicaciones**, seleccione **Aplicaciones**y seleccione la aplicación que contiene el tipo de implementación que desea administrar. En el panel de detalles, haga clic en la ficha **Tipos de implementación** , seleccione el tipo de implementación que desea administrar y, a continuación, seleccione una tarea de administración.  
  
|Tarea|Detalles|  
|----------|-------------|  
|**Aumentar prioridad**|Aumenta la prioridad del tipo de implementación seleccionado. Los tipos de implementación se evalúan en orden. Cuando un tipo de implementación cumple los requisitos especificados se ejecutará y no se evaluarán otros tipos de implementación de la lista de prioridad.|  
|**Reducir prioridad**|Reduce la prioridad del tipo de implementación seleccionado.|  
|**Eliminar**|Elimina el tipo de implementación seleccionado.<br><br>No se puede eliminar un tipo de implementación si un tipo de implementación en otra aplicación hace referencia al mismo.<br>Para eliminar un tipo de implementación debe quitar las dependencias al tipo de implementación contenidas en otros tipos de implementación.<br>Además, también debe quitar revisiones anteriores de aplicaciones que contienen un tipo de implementación que hace referencia al tipo de implementación que desea eliminar.|  
|**Actualizar contenido**|Actualiza el contenido del tipo de implementación seleccionado.<br /><br /> Al iniciar el asistente para un tipo de implementación que contiene una aplicación virtual, se inicia el **Asistente para actualizar contenido** . Este asistente le permite modificar las opciones de publicación y las reglas de requisitos para la aplicación virtual seleccionada. Para obtener más información, consulte [Create applications](../../apps/deploy-use/create-applications.md) (Creación de aplicaciones).<br /><br /> Al actualizar el contenido de un tipo de implementación, se crea una nueva revisión de la aplicación. Esto puede provocar que los dispositivos cliente se actualicen con la nueva aplicación.|  
  




<!--HONumber=Nov16_HO1-->

