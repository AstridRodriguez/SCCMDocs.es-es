---
title: "Declaración de privacidad de System Center Configuration Manager: información adicional | Microsoft Docs"
description: "Conozca cómo Microsoft recopila y usa datos de una implementación de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translation.priority.ht:
- cs-cz
- de-de
- en-gb
- es-es
- fr-fr
- hu-hu
- it-it
- ja-jp
- ko-kr
- nl-nl
- pl-pl
- pt-br
- pt-pt
- ru-ru
- sv-se
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 613b7dbf81de84129e113468d554d8430cbc3182

---
# <a name="additional-information-about-privacy-for-system-center-configuration-manager"></a>Más información sobre la privacidad de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


## <a name="updates-and-servicing"></a>Actualizaciones y mantenimiento
System Center Configuration Manager presenta un nuevo modelo de actualización que ayuda a mantener al día la implementación de Configuration Manager con las actualizaciones y características más recientes. Una vez instalada, esta característica agrega un nuevo rol de sistema de sitio a un servidor de sitio elegido por el administrador denominado punto de conexión de servicio. Para obtener detalles sobre la información que se recopila y su uso, vea la sección Datos de uso de esta declaración.


## <a name="usage-data"></a>Datos de uso
System Center Configuration Manager recopila datos de uso y diagnóstico sobre sí mismo que Microsoft emplea para mejorar la experiencia de instalación, la calidad y la seguridad de las versiones futuras.
Los datos de diagnóstico y uso están habilitados para cada jerarquía de System Center Configuration Manager. Consta de las consultas de SQL Server que se ejecutan de forma semanal en cada sitio primario y en el sitio de administración central. Cuando la jerarquía usa un sitio de administración central, los datos de los sitios primario se replican en ese sitio. En el sitio de nivel superior de la jerarquía, el punto de conexión de servicio envía esta información cuando busca actualizaciones. Si el punto de conexión de servicio está en modo sin conexión, la información se transfiere mediante la herramienta de conexión de servicio.

Configuration Manager solamente recopila datos de la base de datos de SQL Server de sitios y no recopila datos directamente de los clientes ni de los servidores de sitios.

Los administradores pueden cambiar el nivel de datos recopilado en la sección "Datos de uso" de la consola de Configuration Manager.

Para más información, vea el artículo sobre niveles y configuración de datos de uso en [http://go.microsoft.com/fwlink/?LinkID=626566](http://go.microsoft.com/fwlink/?LinkID=626566).


## <a name="customer-experience-improvement-program"></a>Programa para la mejora de la experiencia del usuario
El Programa para la mejora de la experiencia del usuario ("CEIP") recopila información básica de la consola de Configuration Manager sobre la configuración de hardware y el empleo de nuestro software y nuestros servicios con el objeto de identificar tendencias y patrones de uso. CEIP también recopila el tipo y el número de los errores que encuentra, el rendimiento del hardware y el software, y la velocidad de los servicios.  No recopilaremos su nombre, dirección ni ninguna otra información de contacto. No se recopilan datos de CEIP de los equipos cliente.

Usamos esta información para mejorar la calidad, la confiabilidad y el rendimiento del software y los servicios de Microsoft.

Para más información sobre la información recopilada, procesada o transmitida por CEIP, vea la declaración de privacidad de CEIP en [http://go.microsoft.com/fwlink/?LinkID=525211](http://go.microsoft.com/fwlink/?LinkID=525211).

## <a name="oms-connector"></a>Conector de OMS
El conector de Microsoft Operations Management Suite sincroniza datos como colecciones de System Center Configuration Manager con Microsoft Operations Management Suite. El identificador de suscripción de Microsoft Azure y la clave secreta se almacenan en la base de datos de Configuration Manager cuando un administrador configura la característica. El secreto de cliente de Azure Active Directory y la clave compartida del área de trabajo de Microsoft Operations Management Suite se almacenan en la base de datos de System Center Configuration Manager local. Todas las comunicaciones entre System Center Configuration Manager y Microsoft Operations Management Suite usan HTTPS. No se proporciona a Microsoft ninguna información adicional sobre las colecciones más allá de datos de telemetría aleatorios. Para conocer detalles sobre la información recopilada por Microsoft Operations Management Suite, vea el artículo sobre la seguridad de los datos de análisis del registro en [http://go.microsoft.com/fwlink/?LinkId=823545](http://go.microsoft.com/fwlink/?LinkId=823545).

## <a name="asset-intelligence"></a>Asset Intelligence
Asset Intelligence permite a los administradores de TI definir, realizar un seguimiento y administrar de manera proactiva la conformidad con los estándares de configuración. La medición y la creación de informes sobre la implementación y el uso de aplicaciones físicas y virtuales ayuda a las organizaciones a tomar mejores decisiones empresariales acerca de las licencias de software y el cumplimiento con los contratos de licencia. Después de recopilar datos de uso de los clientes de Configuration Manager, los administradores pueden utilizar características distintas para ver los datos, incluidas las recopilaciones, las consultas y los informes.

Durante cada sincronización, se descargará un catálogo de software conocido de Microsoft. El administrador de TI puede enviar información de Microsoft acerca de los títulos de software sin categorizar detectados dentro de su organización que se van a buscar y agregar al catálogo. Antes de cargar esta información, un cuadro de diálogo muestra exactamente los datos que se van a cargar. Los datos cargados no se pueden recuperar. Asset Intelligence no envía información relativa a los usuarios y equipos o el uso de licencias a Microsoft.

Una vez se ha cargado un título de software, los buscadores de Microsoft identifican, categorizan y ponen ese conocimiento a disposición de los demás clientes que usan esta característica y de otros consumidores del catálogo. Cualquier título de software cargado se hace público, en el sentido de que el conocimiento de esa determinada aplicación y su categorización pasan a formar parte del catálogo, y desde ahí se puede descargar a otros consumidores. Antes de configurar la recopilación de datos de Asset Intelligence y decidir si desea enviar información a Microsoft, tenga en cuenta los requisitos de privacidad de su organización.

Asset Intelligence no está habilitado en System Center Configuration Manager de forma predeterminada. La carga de títulos sin categorizar nunca se produce automáticamente y el sistema no está diseñado para que se automatice esta tarea. Debe seleccionar manualmente y aprobar la carga de cada título de software.

## <a name="endpoint-protection"></a>Endpoint Protection
Productos aplicables de Microsoft Cloud Protection Service (anteriormente conocido como Microsoft Active Protection Service o MAPS): System Center Endpoint Protection y la característica Endpoint Protection de System Center Configuration Manager (para la administración de System Center Endpoint Protection y Windows Defender en Windows 10). Esta característica no está implementada para las versiones Linux y Mac de System Center Endpoint Protection.

La comunidad antimalware Microsoft Cloud Protection Service es una comunidad voluntaria internacional en línea que agrupa a los usuarios de System Center Endpoint Protection. Al unirse a Microsoft Cloud Protection Service, System Center Endpoint Protection envía información a Microsoft automáticamente para ayudarle a determinar qué software debe investigar para detectar posibles amenazas así como a mejorar la eficacia de System Center Endpoint Protection. Esta comunidad ayuda a detener la propagación de nuevas infecciones de software malintencionado. Si un informe de Microsoft Cloud Protection Service incluye detalles sobre malware u otro software potencialmente no deseado que el cliente de Endpoint Protection puede quitar, Microsoft Cloud Protection Service descargará la firma más reciente para proceder. Microsoft Cloud Protection Service también puede detectar "falsos positivos" (elementos inicialmente identificados como malware de forma errónea) y corregirlos.

Los informes de Microsoft Cloud Protection Service incluyen información sobre posibles archivos de malware, como nombres de archivo, hash criptográfico, proveedor, tamaño y marcas de fecha. Además, Microsoft Cloud Protection Service podría recopilar direcciones URL completas para indicar el origen del archivo. Estas direcciones URL podrían incluir información personal como términos de búsqueda o datos escritos en formularios. Los informes también podrían incluir las medidas tomadas cuando Endpoint Protection notificó sobre el software no deseado. Los informes de Microsoft Cloud Protection Service incluyen esta información para ayudar a Microsoft a evaluar la eficacia de Endpoint Protection a la hora de detectar y quitar el malware y el software potencialmente no deseado y para intentar identificar nuevo malware.

Es posible unirse a Microsoft Cloud Protection Service con una suscripción básica o avanzada. Los informes de los miembros básicos contienen la información descrita anteriormente. Los informes para un miembro avanzado son más completos y pueden incluir detalles adicionales sobre el software detectado por Endpoint Protection, incluida la ubicación del software, nombres de archivos, cómo funciona el software y el impacto que ha tenido en el equipo. Estos informes, junto con los de otros usuarios de Endpoint Protection que participan en Microsoft Cloud Protection Service, ayudan a los investigadores de Microsoft a detectar las nuevas amenazas con más rapidez. Posteriormente, se crean las definiciones de malware para programas que cumplen los criterios de análisis y las definiciones actualizadas se ponen a disposición de todos los usuarios a través de Microsoft Update.

Para ayudar a detectar y solucionar determinados tipos de infecciones de malware, el producto envía regularmente a Microsoft Cloud Protection Service alguna información sobre el estado de seguridad del equipo. Esta información incluye detalles sobre la configuración de seguridad del equipo y archivos de registro que describen los controladores y otro software que se carga cuando el equipo arranca.
También se envía un número que identifica al equipo de forma exclusiva. Además, Microsoft Cloud Protection Service podría recopilar las direcciones IP a las que se conectan los potenciales archivos de malware.

Los informes de Microsoft Cloud Protection Service se usan para mejorar el software y los servicios de Microsoft. Los informes también podrían usarse para estadísticas o con otros fines de pruebas o analíticos, y para generar definiciones. El acceso a los informes solo se proporciona a los empleados de Microsoft, los contratistas, los partners y los proveedores que tengan la necesidad empresarial de usarlos.

Microsoft Cloud Protection Service no recopila intencionadamente información personal. En la medida en que Microsoft Cloud Protection Service recopila información personal, Microsoft no usa dicha información para identificarle ni ponerse en contacto con usted.

Encontrará más detalles relacionados con los datos recopilados en la documentación del producto en [http://go.microsoft.com/fwlink/?LinkId=823547](http://go.microsoft.com/fwlink/?LinkId=823547).

## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>Jerarquía del sitio – vista geográfica con Bing Maps
La vista geográfica de la jerarquía del sitio le permite ver la topología del servidor físico de Configuration Manager mediante mapas proporcionados por Microsoft Bing Maps. Para habilitar esta característica, se envía información de ubicación proporcionada por usted desde su servidor al servicio web de Bing Maps.

Microsoft utiliza la información para hacer funcionar y mejorar Microsoft Bing Maps y otros sitios y servicios de Microsoft. Para más información, vea la Declaración de privacidad de Microsoft en http://go.microsoft.com/fwlink/?LinkId=823548.
Puede elegir no utilizar la Vista geográfica para la Jerarquía del sitio. La vista Diagrama de jerarquía permite ver la jerarquía y no utiliza el servicio Bing Maps.

## <a name="microsoft-intune-subscription"></a>Suscripción a Microsoft Intune
Los clientes que han adquirido una suscripción a Microsoft Intune pueden usar Configuration Manager para administrar los dispositivos móviles que se conectan a través de Microsoft Intune. La [Declaración de privacidad de Microsoft Online Services](http://go.microsoft.com/fwlink/?LinkId=262214) se aplica a los servicios en línea de Microsoft, incluido Microsoft Intune. Si los clientes además tienen una suscripción de Microsoft Intune, la [Declaración de privacidad de Microsoft Online Services](http://go.microsoft.com/fwlink/?LinkId=262214) debe leerse con la presente declaración de privacidad.

Todas las comunicaciones con Microsoft Intune usan HTTPS. Para configurar la suscripción de Microsoft Intune y descargar la solicitud de firma de certificado (CSR) necesaria para la configuración del soporte de iOS, un administrador debe iniciar sesión en Microsoft Intune mediante la cuenta y la contraseña de su organización. Estas credenciales no se almacenan en Configuration Manager. Todas las demás comunicaciones con Microsoft Intune se autentican mediante certificados PKI generados automáticamente por Microsoft Intune.

Para administrar dispositivos conectados a Microsoft Intune, algunos datos se envían a Microsoft Intune y se reciben de este. Estos datos incluyen el nombre principal de usuario (UPN) de todos los usuarios asignados al servicio e información de inventario de los dispositivos administrados por Microsoft Intune. Los metadatos, como el nombre de la aplicación, el publicador y la versión, del contenido asignado a los puntos de distribución de Manage.Microsoft.com se envían a Microsoft Intune. El contenido binario real asignado a un punto de distribución de Manage.Microsoft.com se cifra antes de cargarse en Microsoft Intune.

Esta característica no está configurada de forma predeterminada. Los administradores tienen control sobre el contenido que se transfiere al punto de distribución de Manage.Microsoft.com y sobre los usuarios que están asignados al servicio. La característica se puede quitar en cualquier momento.



<!--HONumber=Dec16_HO3-->

