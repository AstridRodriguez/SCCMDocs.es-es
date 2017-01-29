---
title: "Seguridad y privacidad para la configuración de cumplimiento | Microsoft Docs"
description: "Obtenga información sobre los procedimientos recomendados de seguridad para la configuración de cumplimiento en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1c409244-6778-4970-a99c-d2508c9cf62b
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f9e939d871e95a3248d8e5d96cb73063a81fd5cf
ms.openlocfilehash: e7dc554ffcd23978eed44819b525f6cc239b2135


---
# <a name="security-and-privacy-for-compliance-settings-in-system-center-configuration-manager"></a>Seguridad y privacidad para la configuración de cumplimiento en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


## <a name="security-best-practices-for-compliance-settings"></a>Procedimientos recomendados de seguridad para la configuración de cumplimiento  

|Práctica recomendada de seguridad|Más información|  
|----------------------------|----------------------|  
|No supervise datos confidenciales.|Para evitar la divulgación de información, no configure los elementos de configuración para supervisar información potencialmente confidencial.|  
|No configure reglas de compatibilidad que usen datos que puedan modificar usuarios finales.|Si crea una regla de cumplimiento basada en datos que los usuarios pueden modificar, como la configuración del Registro para opciones de configuración, los resultados de cumplimiento no serán confiables.|  
|Importe paquetes de configuración de Microsoft System Center y otros datos de configuración de orígenes externos solo si tienen una firma digital válida de un editor de confianza.|Los datos de configuración publicados pueden estar firmados digitalmente para que pueda comprobar el origen de la publicación y asegurarse de que los datos no se han alterado. Si la comprobación de firma digital no se completa correctamente, se emitirá una advertencia y se le solicitará confirmación para continuar con la importación. No importe datos sin firmar si no puede comprobar el origen y la integridad de los datos.|  
|Implementar controles de acceso para proteger los equipos de referencia.|Asegúrese de que cuando un usuario administrativo configure el Registro o el sistema de archivos a partir de un equipo de referencia, el equipo de referencia no se ha puesto en peligro.|  
|Proteja el canal de comunicación cuando examine un equipo de referencia.|Para evitar la manipulación de los datos cuando se transfieren por la red, use la seguridad del protocolo de Internet (IPsec) o el bloque de mensajes de servidor (SMB) entre el equipo que ejecuta la consola de Configuration Manager y el equipo de referencia.|  
|Restrinja y supervise los usuarios administrativos a los que se concede el rol de seguridad basado en el rol Administrador de configuración de cumplimiento.|Los usuarios administrativos a los que se concede el rol **Administrador de configuración de cumplimiento** pueden implementar elementos de configuración en todos los dispositivos y todos los usuarios en la jerarquía. Los elementos de configuración pueden ser muy eficaces y pueden incluir, por ejemplo, la reconfiguración del Registro y scripts.|  

## <a name="privacy-information-for-compliance-settings"></a>Información de privacidad para la configuración de cumplimiento  
 Puede usar la configuración de cumplimiento para evaluar si los dispositivos cliente son conformes con los elementos de configuración que se implementan en las líneas base de configuración. Algunas correcciones pueden corregirse automáticamente si no son conformes. El punto de administración envía información de compatibilidad al servidor del sitio y la almacena en la base de datos del sitio. La información se cifra cuando los dispositivos la envían al punto de administración, pero no se almacena en formato cifrado en la base de datos del sitio. La información se guarda en la base de datos hasta que la tarea de mantenimiento del sitio **Eliminar datos antiguos de administración de configuración** la elimina cada 90 días. Puede configurar el intervalo de eliminación. La información de compatibilidad no se envía a Microsoft.  

 De manera predeterminada, los dispositivos no evalúan la configuración de cumplimiento. Además, debe configurar los elementos de configuración y las líneas base de configuración y, a continuación, implementarlos en los dispositivos.  



<!--HONumber=Dec16_HO3-->

