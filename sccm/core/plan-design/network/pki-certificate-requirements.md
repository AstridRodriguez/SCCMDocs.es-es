---
title: Requisitos de certificados PKI | Microsoft Docs
description: "Encuentre los requisitos de certificados PKI que podría necesitar para System Center Configuration Manager."
ms.custom: na
ms.date: 12/07/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d6a73e68-57d8-4786-842b-36669541d8ff
caps.latest.revision: 17
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: db0642e95bbd7e704d2052aa1e0f5c27cd7bf568
ms.openlocfilehash: 00c3c355fc43eff18b86112b0b9272cbcdf38e85


---
# <a name="pki-certificate-requirements-for-system-center-configuration-manager"></a>Requisitos de certificados PKI para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

En las tablas siguientes se enumeran los certificados de infraestructura de clave pública (PKI) que pueda necesitar para System Center Configuration Manager. Esta información supone un conocimiento básico de los certificados PKI. Para obtener una guía paso a paso de una implementación, vea [Ejemplo paso a paso de implementación de los certificados PKI para Configuration Manager: Entidad de certificación de Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates). Para obtener más información acerca de los servicios de certificados de Active Directory, consulte la siguiente documentación:  

-   Para Windows Server 2012: [Información general de Servicios de certificados de Active Directory](http://go.microsoft.com/fwlink/p/?LinkId=286744)  

-   Para Windows Server 2008: [Servicios de certificados de Active Directory en Windows Server 2008](http://go.microsoft.com/fwlink/p/?LinkId=115018)  

> [!IMPORTANT]  
>  Windows dejará de confiar en los certificados firmados con SHA-1 a partir del 1 de enero de 2017.  Se recomienda emitir nuevos certificados de autenticación de cliente y servidor firmados con SHA-2 (lo que incluye SHA-256).  
>   
>  Para obtener más información sobre este cambio y las posibles actualizaciones hasta la fecha límite, siga esta entrada de blog: [Windows Enforcement of Authenticode Code Signing and Timestamping (Cumplimiento de la firma de código y la marca de tiempo con Authenticode de Windows](http://social.technet.microsoft.com/wiki/contents/articles/32288.windows-enforcement-of-authenticode-code-signing-and-timestamping.aspx)  

 Excepto los certificados de cliente que System Center Configuration Manager inscribe en dispositivos móviles y equipos Mac, los certificados que Microsoft Intune crea automáticamente para administrar dispositivos móviles y los certificados que System Center Configuration Manager instala en equipos basados en AMT, puede usar cualquier PKI para crear, implementar y administrar los certificados siguientes. Sin embargo, cuando utilice Servicios de certificados de Active Directory y plantillas de certificado, esta solución PKI de Microsoft puede facilitar la administración de los certificados. Use la columna **Plantilla de certificado de Microsoft para usar** en las tablas siguientes para identificar la plantilla de certificado que mejor satisfaga sus requisitos de certificado. Los certificados basados en plantilla solo los puede emitir una entidad de certificación (CA) empresarial que se ejecute en las ediciones Enterprise o Datacenter del sistema operativo del servidor, como Windows Server 2008 Enterprise y Windows Server 2008 Datacenter.  

> [!IMPORTANT]  
>  Cuando utilice una empresa entidad emisora de certificados y plantillas de certificados, no utilice las plantillas de la versión 3. Estas plantillas de certificado crean certificados que no son compatibles con System Center Configuration Manager. En su lugar, utilice las plantillas de versión 2 siguiendo las instrucciones siguientes:  
>   
>  -   Para una CA en Windows Server 2012: en la pestaña **Compatibilidad** de las propiedades de la plantilla de certificados, especifique **Windows Server 2003** para la opción **Entidad de certificación** y **Windows XP/Server 2003** para la opción **Destinatario del certificado** .  
> -   Para una CA en Windows Server 2008: cuando duplique una plantilla de certificado, mantenga la selección predeterminada de **Windows Server 2003 Enterprise** cuando se le solicite en el cuadro de diálogo emergente **Plantilla duplicada** . No seleccione **Windows Server 2008, Enterprise Edition**.  

 Consulte las secciones siguientes para ver los requisitos de certificado.  

##  <a name="a-namebkmkpkicertificatesforserversa-pki-certificates-for-servers"></a><a name="BKMK_PKIcertificates_for_servers"></a> Certificados PKI para servidores  

|Componente de System Center Configuration Manager|Propósito del certificado|Plantilla de certificado de Microsoft para usar|Información específica en el certificado|Cómo se usa el certificado en System Center Configuration Manager|  
|-------------------------------------|-------------------------|-------------------------------------------|---------------------------------------------|----------------------------------------------------------|  
|Sistemas de sitio que ejecutan Internet Information Services (IIS) y que están configurados para conexiones de cliente HTTPS:<br /><br /> - Punto de administración<br /><br /> - Punto de distribución<br /><br /> - Punto de actualización de software<br /><br /> - Punto de migración de estado<br /><br /> - Punto de inscripción<br /><br /> - Punto de proxy de inscripción<br /><br /> - Punto de servicio web del catálogo de aplicaciones<br /><br /> - Punto de sitios web del catálogo de aplicaciones<br /><br /> - Punto de registro de certificado|Autenticación de servidor|**Servidor web**|**El valor Uso mejorado de clave** debe contener **Autenticación del servidor (1.3.6.1.5.5.7.3.1)**.<br /><br /> Si el sistema de sitio acepta conexiones de Internet, el nombre del firmante o nombre alternativo del firmante debe contener el nombre de dominio completo (FQDN) de Internet.<br /><br /> Si el sistema de sitio acepta conexiones de la intranet, el nombre del firmante o nombre alternativo del firmante debe contener el FQDN de la intranet (recomendado) o el nombre del equipo, dependiendo de cómo esté configurado el sistema de sitio.<br /><br /> Si el sistema de sitio acepta conexiones tanto de Internet como de la intranet, deberá especificar el FQDN de Internet y el FQDN de la intranet (o nombre del equipo) con el símbolo de y comercial (&) como delimitador entre los dos nombres.<br /><br /> **Nota:** Cuando el punto de actualización de software acepte conexiones de cliente solo de Internet, el certificado deberá contener el FQDN de Internet y el FQDN de la intranet.<br /><br /> Se admite el algoritmo hash SHA-2.<br /><br /> System Center Configuration Manager no especifica una longitud máxima de la clave para este certificado. Consulte la documentación de IIS y PKI en caso de problemas relacionados con el tamaño de la clave de este certificado.|Este certificado debe encontrarse en el almacén personal del almacén de certificados del equipo.<br /><br /> Este certificado de servidor web se usa para autenticar estos servidores en el cliente y para cifrar todos los datos transferidos entre el cliente y estos servidores mediante Capa de sockets seguros (SSL).|  
|Punto de distribución basado en la nube|Autenticación de servidor|**Servidor web**|**El valor Uso mejorado de clave** debe contener **Autenticación del servidor (1.3.6.1.5.5.7.3.1)**.<br /><br /> El nombre del firmante debe contener un nombre de servicio definido por el cliente y un nombre de dominio en un formato de FQDN como el nombre común para la instancia específica del punto de distribución basado en la nube.<br /><br /> La clave privada debe ser exportable.<br /><br /> Se admite el algoritmo hash SHA-2.<br /><br /> Longitudes de clave compatibles: 2048 bits.|Este certificado de servicio se usa para autenticar el servicio de punto de distribución basado en la nube a los clientes de Configuration Manager y para cifrar todos los datos transferidos entre ellos mediante la capa de sockets seguros (SSL). Este certificado debe exportarse en un formato Public Key Certificate Standard (PKCS #12) y la contraseña debe conocerse para que pueda importarse al crear un punto de distribución basado en la nube.<br /><br /> **Nota:** Este certificado se utiliza junto con el certificado de administración de Windows Azure. Para más información acerca de este certificado, consulte [Crear un certificado de administración para Windows Azure](http://go.microsoft.com/fwlink/p/?LinkId=220281) y [Agregar un certificado de administración a una suscripción de Windows Azure](http://go.microsoft.com/fwlink/?LinkId=241722) en la sección Plataforma Windows Azure de MSDN Library.|  
|Servidores de sistema de sitio que ejecutan Microsoft SQL Server|Autenticación de servidor|**Web server**|**El valor Uso mejorado de clave** debe contener **Autenticación del servidor (1.3.6.1.5.5.7.3.1)**.<br /><br /> El nombre del firmante debe contener el nombre de dominio completo (FQDN) de la intranet.<br /><br /> Se admite el algoritmo hash SHA-2.<br /><br /> La longitud de clave compatible máxima es de 2048 bits.|Este certificado debe encontrarse en el almacén personal del almacén de certificados del equipo, y System Center Configuration Manager lo copia automáticamente en el almacén de usuarios de confianza de los servidores de la jerarquía de System Center Configuration Manager que puedan tener que establecer confianza con el servidor.<br /><br /> Estos certificados se utilizan para la autenticación de servidor a servidor.|  
|Clúster de SQL Server: servidores de sistema de sitio que ejecutan Microsoft SQL Server|Autenticación de servidor|**Web server**|**El valor Uso mejorado de clave** debe contener **Autenticación del servidor (1.3.6.1.5.5.7.3.1)**.<br /><br /> El nombre del firmante debe contener el nombre de dominio completo (FQDN) de la intranet del clúster.<br /><br /> La clave privada debe ser exportable.<br /><br /> El certificado debe tener un período de validez de al menos dos años cuando configure System Center Configuration Manager para que use el clúster de SQL Server.<br /><br /> Se admite el algoritmo hash SHA-2.<br /><br /> La longitud de clave compatible máxima es de 2048 bits.|Una vez que haya solicitado e instalado este certificado en un nodo del clúster, exporte el certificado e impórtelo en cada nodo adicional en el clúster de SQL Server.<br /><br /> Este certificado debe encontrarse en el almacén personal del almacén de certificados del equipo, y System Center Configuration Manager lo copia automáticamente en el almacén de usuarios de confianza de los servidores de la jerarquía de System Center Configuration Manager que puedan tener que establecer confianza con el servidor.<br /><br /> Estos certificados se utilizan para la autenticación de servidor a servidor.|  
|Supervisión del sistema de sitio para los siguientes roles de sistema de sitio:<br /><br /> Punto de administración<br /><br /> Punto de migración de estado|Autenticación de cliente|**Autenticación de estación de trabajo**|**El valor Uso mejorado de clave** debe contener **Autenticación del cliente (1.3.6.1.5.5.7.3.2)**.<br /><br /> Los equipos deben tener un valor único en el campo de nombre del firmante o nombre alternativo del firmante.<br /><br /> **Nota:** Si se usan varios valores para el nombre alternativo del sujeto, se utilizará solo el primer valor.<br /><br /> Se admite el algoritmo hash SHA-2.<br /><br /> La longitud de clave compatible máxima es de 2048 bits.|Este certificado es necesario en los servidores de sistema de sitio enumerados, incluso si no está instalado el cliente de System Center Configuration Manager, por lo que se puede supervisar el estado de mantenimiento de estos roles de sistema de sitio y se puede informar sobre ellos al sitio.<br /><br /> El certificado para estos sistemas de sitio debe encontrarse en el almacén personal del almacén de certificados del equipo.|  
|Servidores que ejecutan el módulo de directivas de System Center Configuration Manager con el servicio de rol Servicio de inscripción de dispositivos de red.|Autenticación de cliente|Autenticación de estación de trabajo|**El valor Uso mejorado de clave** debe contener **Autenticación del cliente (1.3.6.1.5.5.7.3.2)**.<br /><br /> No hay requisitos específicos para el nombre del firmante o el nombre alternativo del firmante (SAN) del certificado, y puede utilizar el mismo certificado para varios servidores que ejecutan el Servicio de inscripción de dispositivos de red.<br /><br /> Se admiten los algoritmos hash SHA-2 y SHA-3.<br /><br /> Longitudes de clave compatibles: 1024 bits y 2048 bits.||  
|Sistemas de sitio que tienen instalado un punto de distribución|Autenticación de cliente|**Autenticación de estación de trabajo**|**El valor Uso mejorado de clave** debe contener **Autenticación del cliente (1.3.6.1.5.5.7.3.2)**.<br /><br /> No hay requisitos específicos para el nombre del firmante o el nombre alternativo del firmante (SAN) del certificado, y puede utilizar el mismo certificado para varios puntos de distribución. Sin embargo, se recomienda un certificado diferente para cada punto de distribución.<br /><br /> La clave privada debe ser exportable.<br /><br /> Se admite el algoritmo hash SHA-2.<br /><br /> La longitud de clave compatible máxima es de 2048 bits.|Este certificado tiene dos propósitos:<br /><br /> - Autentica el punto de distribución en un punto de administración habilitado para HTTPS antes de que el punto de distribución envíe mensajes de estado.<br /><br /> - Cuando se selecciona la opción de punto de distribución **Habilitar compatibilidad de PXE para clientes**, el certificado se envía a los equipos. De esta forma, si las secuencias de tareas en el proceso de implementación de sistema operativo incluyen acciones de cliente tales como la recuperación de directiva de cliente o el envío de información del inventario, los equipos cliente se pueden conectar a un punto de administración habilitado para HTTPS durante la implementación del sistema operativo.<br /><br /> Este certificado solo se utiliza durante el tiempo que dure el proceso de implementación del sistema operativo y no se instala en el cliente. Debido a este uso temporal, puede utilizarse el mismo certificado para cada implementación del sistema operativo si no desea usar varios certificados de cliente.<br /><br /> Este certificado debe exportarse en un formato Public Key Certificate Standard (PKCS #12) y la contraseña debe conocerse para que se pueda importar en las propiedades del punto de distribución.<br /><br /> **Nota:** Los requisitos de este certificado son los mismos que los del certificado de cliente para imágenes de arranque cuando se implementan sistemas operativos. Debido a que los requisitos son los mismos, puede utilizar el mismo archivo de certificado.|  
|Servidor que ejecuta Internet Information Services (IIS)|Aprovisionamiento de AMT|**Servidor web** (modificado)|El valor**Uso mejorado de clave** debe contener **Autenticación de servidor (1.3.6.1.5.5.7.3.1)** y el identificador de objeto siguiente: **2.16.840.1.113741.1.2.3**.<br /><br /> El campo de nombre del firmante debe contener el FQDN del servidor que hospeda el punto de servicio fuera de banda.<br /><br /> **Nota:** Si solicita un certificado de aprovisionamiento de AMT desde una CA externa en lugar de desde su propia CA interna y no es compatible con el identificador de objeto de aprovisionamiento de AMT 2.16.840.1.113741.1.2.3, tiene la opción de especificar la cadena de texto siguiente como un atributo de unidad organizativa (OU) en el nombre del sujeto del certificado: **Certificado de instalación del cliente de Intel(R)**. Debe usar esta cadena de texto exacta en inglés, en el mismo caso, sin punto, y junto con el FQDN del servidor que hospeda el punto de servicio fuera de banda.<br /><br /> Longitudes de clave compatibles: 1024 y 2048. Para AMT 6.0 y versiones posteriores, también se admite la longitud de clave de 4096 bits.|Este certificado se encuentra en el almacén personal del almacén de certificados del equipo del servidor de sistema de sitio del punto de servicio fuera de banda.<br /><br /> Este certificado de aprovisionamiento de AMT se utiliza para preparar los equipos para la administración fuera de banda.<br /><br /> Debe solicitar este certificado a una CA que suministre certificados de aprovisionamiento de AMT, y debe configurar la extensión BIOS de los equipos basados en Intel AMT para que usen la huella digital del certificado raíz (también llamada hash del certificado) para este certificado de aprovisionamiento.<br /><br /> VeriSign es un ejemplo típico de una CA externa que proporciona certificados de aprovisionamiento de AMT, pero también puede utilizar su propia CA interna.<br /><br /> Instale el certificado en el servidor que hospeda el punto de servicio fuera de banda, que debe ser capaz de vincularse correctamente a la CA raíz del certificado. (De forma predeterminada, el certificado de CA raíz y el certificado de CA intermedio de VeriSign se instalan cuando se instala Windows).|  
|Servidor de sistema de sitio que ejecuta el conector de Microsoft Intune|Autenticación de cliente|No aplicable: Intune crea automáticamente este certificado.|El valor Uso mejorado de clave contiene Autenticación de cliente (1.3.6.1.5.5.7.3.2).<br /><br /> Existen 3 extensiones personalizadas que identifican de forma exclusiva la suscripción a Intune de los clientes.<br /><br /> El tamaño de clave es de 2048 bits y se utiliza el algoritmo hash SHA-1.<br /><br /> **Nota:** No se puede cambiar esta configuración: esta información se proporciona únicamente para fines informativos.|Este certificado se solicita y se instala automáticamente en la base de datos de Configuration Manager al suscribirse a Microsoft Intune. Cuando se instala el conector de Microsoft Intune, este certificado se instala en el servidor de sistema de sitio que ejecuta el conector de Microsoft Intune. Se instala en el almacén de certificados del equipo.<br /><br /> Este certificado se usa para autenticar la jerarquía de Configuration Manager para Microsoft Intune mediante el conector de Microsoft Intune. Todos los datos que se transfieren entre ellos utilizan la capa de sockets seguros (SSL).|  

###  <a name="a-namebkmkpkicertificatesforproxyserversa-proxy-web-servers-for-internet-based-client-management"></a><a name="BKMK_PKIcertificates_for_proxyservers"></a> Servidores proxy web para la administración de cliente basada en Internet  
 Si el sitio admite la administración de cliente basada en Internet y, además, se utiliza un servidor proxy web con la terminación SSL (puente) para las conexiones entrantes de Internet, el servidor proxy web reúne los requisitos de certificado enumerados en la siguiente tabla.  

> [!NOTE]  
>  Si se utiliza un servidor proxy web sin terminación SSL (tunelización), no se requieren certificados adicionales en el servidor proxy web.  

|Componente de la infraestructura de red|Propósito del certificado|Plantilla de certificado de Microsoft para usar|Información específica en el certificado|Cómo se usa el certificado en System Center Configuration Manager|  
|--------------------------------------|-------------------------|-------------------------------------------|---------------------------------------------|----------------------------------------------------------|  
|Servidor proxy web que acepta conexiones de cliente a través de Internet|Autenticación de servidor y cliente|1. <br />                        **Servidor web**<br /><br /> 2. <br />                        **Autenticación de estación de trabajo**|FQDN de Internet en los campos Nombre de sujeto o Nombre alternativo del sujeto (si se utilizan plantillas de certificado de Microsoft, el nombre alternativo del sujeto sólo está disponible con la plantilla de estación de trabajo).<br /><br /> Se admite el algoritmo hash SHA-2.|Este certificado se utiliza para autenticar los siguientes servidores para los clientes de Internet y para cifrar mediante SSL todos los datos transferidos entre el cliente y este servidor:<br /><br /> - Punto de administración basado en Internet<br /><br /> - Punto de distribución basado en Internet<br /><br /> - Punto de actualización de software basado en Internet<br /><br /> La autenticación de cliente se usa para enlazar las conexiones de cliente entre los clientes de System Center Configuration Manager y los sistemas de sitio basados en Internet.|  

##  <a name="a-namebkmkpkicertificatesforclientsa-pki-certificates-for-clients"></a><a name="BKMK_PKIcertificates_for_clients"></a> Certificados PKI para clientes  

|Componente de System Center Configuration Manager|Propósito del certificado|Plantilla de certificado de Microsoft para usar|Información específica en el certificado|Cómo se usa el certificado en System Center Configuration Manager|  
|-------------------------------------|-------------------------|-------------------------------------------|---------------------------------------------|----------------------------------------------------------|  
|Equipos cliente de Windows|Autenticación de cliente|**Autenticación de estación de trabajo**|**El valor Uso mejorado de clave** debe contener **Autenticación del cliente (1.3.6.1.5.5.7.3.2)**.<br /><br /> Los equipos cliente deben tener un valor único en el campo de Nombre de sujeto o Nombre alternativo del sujeto.<br /><br /> **Nota:** Si se usan varios valores para el nombre alternativo del sujeto, se utilizará solo el primer valor.<br /><br /> Se admite el algoritmo hash SHA-2.<br /><br /> La longitud de clave compatible máxima es de 2048 bits.|De forma predeterminada, System Center Configuration Manager busca los certificados de equipo en el almacén personal del almacén de certificados del equipo.<br /><br /> A excepción del punto de actualización de software y el punto de sitios web del catálogo de aplicaciones, este certificado autentica el cliente para los servidores de sistema de sitio en que se ejecuta IIS y que están configurados para utilizar HTTPS.|  
|Clientes de dispositivos móviles|Autenticación de cliente|**Sesión autenticada**|**El valor Uso mejorado de clave** debe contener **Autenticación del cliente (1.3.6.1.5.5.7.3.2)**.<br /><br /> SHA-1<br /><br /> La longitud de clave compatible máxima es de 2048 bits.<br /><br /> **Notas:**<br /><br /> - Estos certificados deben tener el formato de reglas de codificación distinguida (DER) binario codificado X.509.<br /><br /> - No se admite el formato X.509 codificado con Base64.|Este certificado autentica el cliente de dispositivo móvil para los servidores de sistema de sitio con que se comunica, como los puntos de administración y distribución.|  
|Imágenes de arranque para la implementación de sistemas operativos|Autenticación de cliente|**Autenticación de estación de trabajo**|**El valor Uso mejorado de clave** debe contener **Autenticación del cliente (1.3.6.1.5.5.7.3.2)**.<br /><br /> No hay requisitos específicos para los campos Nombre de sujeto o Nombre alternativo del sujeto del certificado, y puede utilizar el mismo certificado para todas las imágenes de arranque.<br /><br /> La clave privada debe ser exportable.<br /><br /> Se admite el algoritmo hash SHA-2.<br /><br /> La longitud de clave compatible máxima es de 2048 bits.|El certificado se utiliza si las secuencias de tareas del proceso de implementación del sistema operativo incluyen acciones de cliente tales como la obtención de la directiva de cliente o el envío de información de inventario de cliente.<br /><br /> Este certificado solo se utiliza durante el tiempo que dure el proceso de implementación del sistema operativo y no se instala en el cliente. Debido a este uso temporal, puede utilizarse el mismo certificado para cada implementación del sistema operativo si no desea usar varios certificados de cliente.<br /><br /> Este certificado debe exportarse en un formato Public Key Certificate Standard (PKCS #12) y debe conocerse la contraseña para que se pueda importar en las imágenes de arranque de System Center Configuration Manager.<br /><br /> Este certificado es temporal para la secuencia de tareas y no se utiliza para instalar el cliente. Si tiene un entorno con HTTPS exclusivamente, el cliente debe tener un certificado válido para el cliente para comunicarse con el sitio y para que la implementación continúe. El cliente genera automáticamente el certificado de cliente cuando se conecta a Active Directory, o puede instalar un certificado de cliente mediante otro método.<br /><br /> **Nota:** Los requisitos para este certificado son los mismos que para el certificado de servidor para los sistemas de sitio que tienen instalado un punto de distribución. Debido a que los requisitos son los mismos, puede utilizar el mismo archivo de certificado.|  
|Equipos cliente Mac|Autenticación de cliente|Para la inscripción de System Center Configuration Manager:**Sesión autenticada**<br /><br /> Para la instalación de certificados independiente de System Center Configuration Manager: **Autenticación de estación de trabajo**|**El valor Uso mejorado de clave** debe contener **Autenticación del cliente (1.3.6.1.5.5.7.3.2)**.<br /><br /> Cuando System Center Configuration Manager crea un certificado de usuario, el valor del sujeto del certificado se rellena automáticamente con el nombre de usuario de la persona inscrita en el equipo Mac.<br /><br /> Para la instalación de certificados en que no se usa la inscripción en System Center Configuration Manager, sino que se implementa un certificado de equipo independiente de System Center Configuration Manager, el valor del sujeto del certificado debe ser único. Por ejemplo, especifique el FQDN del equipo.<br /><br /> No se admite el campo Nombre alternativo del sujeto.<br /><br /> Se admite el algoritmo hash SHA-2.<br /><br /> La longitud de clave compatible máxima es de 2048 bits.|Este certificado autentica el equipo cliente Mac para los servidores de sistema de sitio con que se comunica, como los puntos de administración y distribución.|  
|Equipos cliente Linux y UNIX|Autenticación de cliente|**Autenticación de estación de trabajo**|**El valor Uso mejorado de clave** debe contener **Autenticación del cliente (1.3.6.1.5.5.7.3.2)**.<br /><br /> No se admite el campo Nombre alternativo del sujeto.<br /><br /> La clave privada debe ser exportable.<br /><br /> El algoritmo hash SHA-2 se admite si el sistema operativo del cliente admite SHA-2. Para obtener más información, vea la sección [Acerca de los sistemas operativos Linux y UNIX que no admiten SHA-256](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256) del tema [Planear la implementación de cliente para servidores Linux y UNIX](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md).<br /><br /> Longitudes de clave compatibles: 2048 bits.<br /><br /> **Nota:** Estos certificados deben tener el formato de reglas de codificación distinguida (DER) binario codificado X.509. No se admite el formato X.509 codificado base 64.|Este certificado autentica el equipo cliente Mac para los servidores de sistema de sitio con que se comunica, como los puntos de administración y distribución. Este certificado debe exportarse en un formato Public Key Certificate Standard (PKCS #12) y la contraseña debe conocerse para que se pueda indicar al cliente al especificar el certificado PKI.<br /><br /> Para obtener más información, vea la sección [Planeamiento de seguridad y certificados para servidores Linux y UNIX](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_SecurityforLnU) de [Planear la implementación de cliente para servidores Linux y UNIX](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md).|  
|- La entidad de certificación (CA) raíz certifica en los siguientes casos:<br /><br /> - Implementación de sistema operativo<br /><br /> - Inscripción de dispositivo móvil<br /><br /> - Autenticación de servidor RADIUS para equipos basados en Intel AMT<br /><br /> - Autenticación de certificado de cliente|Cadena de certificados a una fuente de confianza|No aplicable.|Certificado de CA raíz estándar.|El certificado de CA raíz se debe proporcionar cuando los clientes tienen que establecer una cadena de certificados desde el servidor de comunicación hasta la fuente de confianza. Esto se aplica en los casos siguientes:<br /><br /> - Al implementar un sistema operativo y cuando las secuencias de tareas se ejecutan de manera que conectan el equipo cliente con un punto de administración configurado para utilizar HTTPS.<br /><br /> - Cuando se inscribe un dispositivo móvil para que lo administre System Center Configuration Manager.<br /><br /> - Si usa la autenticación 802.1X para equipos basados en AMT y desea especificar un archivo para el certificado raíz del servidor RADIUS.<br /><br /> Además, el certificado de CA raíz para clientes debe concederse si los certificados clientes los emite una jerarquía de CA distinta a la que ha emitido el certificado del punto de administración.|  
|Equipos basados en Intel AMT|Autenticación de servidor.|**Servidor web** (modificado)<br /><br /> Configure el nombre de sujeto en **Construido a partir de esta información de Active Directory**y, a continuación, seleccione **Nombre común** para el **Formato de nombre de sujeto**.<br /><br /> Debe conceder los permisos **Leer** e **Inscribir** al grupo de seguridad universal que especifique en las propiedades de componente de administración fuera de banda.|**El valor Uso mejorado de clave** debe contener **Autenticación del servidor (1.3.6.1.5.5.7.3.1)**.<br /><br /> El nombre de sujeto debe contener el FQDN del equipo basado en AMT, proporcionado automáticamente por Active Directory Domain Services.|Este certificado se encuentra en la memoria de acceso aleatorio permanente del controlador de administración del equipo y no se encuentra visible en la interfaz de usuario de Windows.<br /><br /> Cada equipo basado en Intel AMT solicita este certificado durante el aprovisionamiento de AMT y para las actualizaciones posteriores. Si quita de estos equipos la información acerca del aprovisionamiento de AMT, estos revocarán el certificado.<br /><br /> Cuando este certificado se instala en equipos basados en Intel AMT, también se instalará la cadena de certificados a la CA raíz. Los equipos basados en AMT no admiten certificados de CA con una longitud de clave mayor que 2048 bits.<br /><br /> Tras la instalación del certificado en equipos basados en Intel AMT, este certificado autentica los equipos basados en AMT en el servidor de sistema de sitio de punto de servicio fuera de banda y en equipos que ejecutan la consola de administración fuera de banda y, además, el certificado cifra todos los datos transferidos entre ellos mediante Seguridad de la capa de transporte (TLS, por sus siglas en inglés).|  
|Certificado de cliente Intel AMT 802.1 X|Autenticación de cliente|**Autenticación de estación de trabajo**<br /><br /> Configure el nombre de sujeto en **Construido a partir de esta información de Active Directory**y, a continuación, seleccione **Nombre común** para el **Formato de nombre de sujeto**, desactive la casilla Nombre de DNS y seleccione Nombre principal del usuario (UPN) como nombre alternativo del sujeto.<br /><br /> Para esta plantilla de certificado, debe conceder los permisos **Leer** e **Inscribir** al grupo de seguridad universal que especifique en las propiedades de componente de administración fuera de banda.|**El valor Uso mejorado de clave** debe contener **Autenticación del cliente (1.3.6.1.5.5.7.3.2)**.<br /><br /> El campo Nombre de sujeto debe contener el FQDN del equipo basado en AMT y el nombre alternativo del sujeto debe contener el UPN.<br /><br /> Longitud de clave compatible máxima: 2048 bits.|Este certificado se encuentra en la memoria de acceso aleatorio permanente del controlador de administración del equipo y no se encuentra visible en la interfaz de usuario de Windows.<br /><br /> Cada equipo basado en Intel AMT puede solicitar este certificado durante el aprovisionamiento de AMT, pero los equipos no revocan este certificado cuando se quita de ellos la información sobre el aprovisionamiento de AMT.<br /><br /> Tras la instalación del certificado en equipos basados en AMT, este certificado autentica los equipos basados en AMT en el servidor RADIUS, a fin de que se le pueda autorizar el acceso a la red.|  
|Dispositivos móviles que están inscritos por Microsoft Intune|Autenticación de cliente|No aplicable: Intune crea automáticamente este certificado.|El valor Uso mejorado de clave contiene Autenticación de cliente (1.3.6.1.5.5.7.3.2).<br /><br /> Existen 3 extensiones personalizadas que identifican de forma exclusiva la suscripción a Intune de los clientes.<br /><br /> Los usuarios pueden proporcionar el valor de sujeto del certificado durante la inscripción. Pero Intune no usa este valor para identificar el dispositivo.<br /><br /> El tamaño de clave es de 2048 bits y se utiliza el algoritmo hash SHA-1.<br /><br /> **Nota:** No se puede cambiar esta configuración: esta información se proporciona únicamente para fines informativos.|Este certificado se solicita e instala automáticamente cuando los usuarios autenticados se inscriben en los dispositivos móviles mediante Microsoft Intune. El certificado creado para el dispositivo se encuentra en el almacén del equipo y autentica el dispositivo móvil inscrito en Intune para que se pueda administrar.<br /><br /> Las extensiones personalizadas del certificado hacen que la autenticación se limite a la suscripción a Intune establecida para la organización.|



<!--HONumber=Dec16_HO3-->

