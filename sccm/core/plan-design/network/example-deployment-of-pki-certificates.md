---
title: "Implementación de certificados PKI | System Center Configuration Manager"
description: "Siga un ejemplo detallado para aprender el proceso de creación e implementación de certificados PKI que usa System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
caps.latest.revision: 11
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 49dfa303453b26a64c1495a1259674e0d8a6bde2


---
# <a name="step-by-step-example-deployment-of-the-pki-certificates-for-system-center-configuration-manager-windows-server-2008-certification-authority"></a>Ejemplo paso a paso de la implementación de los certificados PKI para System Center Configuration Manager: entidad de certificación de Windows Server 2008

*Se aplica a: System Center Configuration Manager (rama actual)*

Esta implementación de ejemplo detallada, que usa una entidad de certificación (CA) de Windows Server 2008, contiene procedimientos para guiarle por el proceso de creación e implementación de los certificados de infraestructura de clave pública (PKI) que usa System Center Configuration Manager. Estos procedimientos utilizan una entidad de certificación (CA) empresarial y plantillas de certificado. Los pasos son adecuados solo para una red de prueba, como una prueba de concepto.  

 Al no haber un único método de implementación de los certificados requeridos, debe consultar su documentación de implementación de PKI específica para obtener información sobre los procedimientos requeridos y las prácticas recomendadas a la hora de implementar los certificados necesarios en un entono de producción. Para obtener más información sobre los requisitos de certificados, consulte [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md) (Requisitos de certificados PKI para System Center Configuration Manager).  

> [!TIP]  
>  Las instrucciones de este tema se puede adaptar fácilmente para los sistemas operativos que no son los que se documentan en la sección Requisitos de la red de prueba. Sin embargo, si se ejecuta la CA emisora en Windows Server 2012, no se le solicitará la versión de la plantilla de certificado. En su lugar, especifíquela en la ficha **Compatibilidad** de las propiedades de la plantilla, de la siguiente manera:  
>   
>  -   **Entidad de certificación**: **Windows Server 2003**  
> -   **Destinatario del certificado**: **Windows XP / Server 2003**  

## <a name="in-this-section"></a>En esta sección  
 Las secciones siguientes incluyen instrucciones detalladas de ejemplo para crear e implementar los siguientes certificados que pueden usarse con System Center Configuration Manager:  

 [Requisitos de la red de prueba](#BKMK_testnetworkenvironment)  

 [Información general acerca de los certificados](#BKMK_overview2008)  

 [Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS](#BKMK_webserver2008_cm2012)  

 [Implementación del certificado de servicio para puntos de distribución basados en la nube](#BKMK_clouddp2008_cm2012)  

 [Implementación del certificado de cliente para equipos Windows](#BKMK_client2008_cm2012)  

 [Implementación del certificado de cliente para puntos de distribución](#BKMK_clientdistributionpoint2008_cm2012)  

 [Implementación del certificado de inscripción para dispositivos móviles](#BKMK_mobiledevices2008_cm2012)  

 [Implementación de los certificados para AMT](#BKMK_AMT2008_cm2012)  

 [Implementación del certificado de cliente para equipos Mac](#BKMK_MacClient_SP1)  

##  <a name="a-namebkmktestnetworkenvironmenta-test-network-requirements"></a><a name="BKMK_testnetworkenvironment"></a> Requisitos de la red de prueba  
 Las instrucciones paso a paso tienen los siguientes requisitos:  

-   La red de prueba ejecuta Servicios de dominio de Active Directory con Windows Server 2008 y se instala como un único dominio, un único bosque.  

-   Dispone de un servidor miembro que ejecuta Windows Server 2008 Enterprise Edition, que tiene instalado el rol Servicios de certificados de Active Directory, y está configurado como una entidad de certificación raíz (CA) empresarial.  

-   Dispone de un equipo que tiene Windows Server 2008 (Standard Edition o Enterprise Edition, R2 o posterior) instalado y está designado como servidor miembro, y en el que se instaló Internet Information Services (IIS). Este equipo será el servidor de sistema de sitio de System Center Configuration Manager que configurará con un FQDN de intranet (para admitir conexiones de cliente en la intranet) y un FQDN de Internet en caso de que sea necesario admitir dispositivos móviles inscritos por System Center Configuration Manager y clientes de Internet.  

-   Dispone de un cliente de Windows Vista con el service pack más reciente instalado, y el equipo está configurado con un nombre de equipo en caracteres ASCII y está unido al dominio. Este equipo será un equipo cliente de System Center Configuration Manager.  

-   Puede iniciar sesión con una cuenta de administrador de dominio raíz o una cuenta de administrador de dominio de empresa y utilizar esta cuenta para todos los procedimientos en esta implementación de ejemplo.  

##  <a name="a-namebkmkoverview2008a-overview-of-the-certificates"></a><a name="BKMK_overview2008"></a> Información general acerca de los certificados  
 En la tabla siguiente se enumeran los tipos de certificados PKI que podrían ser necesarios para System Center Configuration Manager y se describe cómo se usan.  

|Requisito de certificado|Descripción del certificado|  
|-----------------------------|-----------------------------|  
|Certificado de servidor web para los sistemas de sitio que ejecutan IIS|Este certificado se utiliza para cifrar los datos y autenticar el servidor en los clientes. Se debe instalar externamente desde System Center Configuration Manager en servidores de sistemas de sitio que ejecutan IIS y que están configurados en System Center Configuration Manager para usar HTTPS.<br /><br /> Para obtener información sobre los pasos necesarios para configurar e instalar este certificado, consulte [Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS](#BKMK_webserver2008_cm2012) en este tema.|  
|Certificado de servicio para clientes que se conectan a puntos de distribución basados en la nube|Para conocer los pasos necesarios para configurar e instalar este certificado, vea [Implementación del certificado de servicio para puntos de distribución basados en la nube](#BKMK_clouddp2008_cm2012) en este tema.<br /><br /> **Importante:** Este certificado se usa junto con el certificado de administración de Microsoft Azure. Para obtener más información sobre el certificado de administración, consulte [Crear un certificado de administración para Windows Azure](http://go.microsoft.com/fwlink/p/?LinkId=220281) y [Agregar un certificado de administración a una suscripción de Windows Azure](http://go.microsoft.com/fwlink/?LinkId=241722) en la sección Plataforma Windows Azure de MSDN Library.|  
|Certificado de cliente para equipos Windows|Este certificado se usa para autenticar equipos cliente de System Center Configuration Manager en sistemas de sitio que están configurados para usar HTTPS. También puede utilizarse para puntos de administración y puntos de migración de estado, a fin de supervisar su estado de funcionamiento cuando están configurados para usar HTTPS. Se debe instalar externamente en los equipos desde System Center Configuration Manager.<br /><br /> Para conocer los pasos para configurar e instalar este certificado, vea [Implementación del certificado de cliente para equipos Windows](#BKMK_client2008_cm2012) en este tema.|  
|Certificado de cliente para puntos de distribución|Este certificado tiene dos propósitos:<br /><br /> El certificado se utiliza para autenticar el punto de distribución en un punto de administración habilitado para HTTPS antes de que el punto de distribución envíe mensajes de estado.<br /><br /> Cuando está seleccionada la opción de punto de distribución **Habilitar compatibilidad de PXE para clientes** , el certificado se envía a equipos con arranque PXE para que puedan conectarse a un punto de administración habilitado para HTTPS durante la implementación del sistema operativo.<br /><br /> Para obtener información sobre los pasos necesarios para configurar e instalar este certificado, consulte [Implementación del certificado de cliente para puntos de distribución](#BKMK_clientdistributionpoint2008_cm2012) en este tema.|  
|Certificado de inscripción para dispositivos móviles|Este certificado se usa para autenticar clientes de dispositivos móviles de System Center Configuration Manager en sistemas de sitio que están configurados para usar HTTPS. Debe instalarse como parte de la inscripción de dispositivos móviles en System Center Configuration Manager y se debe seleccionar la plantilla de certificado configurada como un valor de cliente de dispositivo móvil.<br /><br /> Para conocer los pasos para configurar este certificado, vea [Deploying the Enrollment Certificate for Mobile Devices](#BKMK_mobiledevices2008_cm2012) en este tema.|  
|Certificados para Intel AMT|Hay tres certificados relacionados con administración fuera de banda para equipos basados en Intel AMT: Un certificado de aprovisionamiento de AMT; un certificado de servidor web AMT; y, opcionalmente, un certificado de autenticación de cliente para redes cableadas o inalámbricas 802.1X.<br /><br /> El certificado de aprovisionamiento de AMT debe instalarse externamente desde System Center Configuration Manager en el equipo del punto de servicio fuera de banda y, después, se debe seleccionar el certificado instalado en las propiedades del punto de servicio fuera de banda. El certificado de servidor web AMT y el certificado de autenticación de cliente se instalan durante el aprovisionamiento y la administración de AMT, por lo que se deben seleccionar las plantillas de certificado configuradas en las propiedades del componente de administración fuera de banda.<br /><br /> Para obtener información sobre los pasos necesarios para configurar estos certificados, consulte [Implementación de los certificados para AMT](#BKMK_AMT2008_cm2012) en este tema.|  
|Certificado de cliente para equipos Mac|Puede solicitar e instalar este certificado desde un equipo Mac al usar la inscripción de System Center Configuration Manager y seleccionar la plantilla de certificado configurada como un valor de cliente de dispositivo móvil.<br /><br /> Para conocer los pasos para configurar este certificado, vea [Deploying the Client Certificate for Mac Computers](#BKMK_MacClient_SP1) en este tema.|  

##  <a name="a-namebkmkwebserver2008cm2012a-deploying-the-web-server-certificate-for-site-systems-that-run-iis"></a><a name="BKMK_webserver2008_cm2012"></a> Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS  
 Esta implementación de certificado consta de los siguientes procedimientos:  

-   Creación y emisión de la plantilla de certificado de servidor web en la entidad de certificación  

-   Solicitud del certificado de servidor web  

-   Configuración de IIS para utilizar el certificado de servidor web  

###  <a name="a-namebkmkwebserver22008a-creating-and-issuing-the-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_webserver22008"></a> Creación y emisión de la plantilla de certificado de servidor web en la entidad de certificación  
 Mediante este procedimiento se crea una plantilla de certificado para sistemas de sitio de System Center Configuration Manager y se agrega a la entidad de certificación.  

##### <a name="to-create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a>Para crear y emitir la plantilla de certificado de servidor web en la entidad de certificación  

1.  Cree un grupo de seguridad llamado **Servidores IIS de Configuration Manager** que contenga los servidores miembro para instalar sistemas de sitio de System Center Configuration Manager que ejecutarán IIS.  

2.  En el servidor miembro que tenga instalados los Servicios de servidor de certificados, en la consola de entidad de certificación, haga clic con el botón secundario en **Plantillas de certificado** y haga clic en **Administrar** para cargar la consola de **Plantillas de certificado** .  

3.  En el panel de resultados, haga clic con el botón secundario en la entrada que muestra **Servidor web** en la columna **Nombre para mostrar plantilla**y, a continuación, haga clic en **Duplicar plantilla**.  

4.  En el cuadro de diálogo **Duplicar plantilla** , asegúrese de que se haya seleccionado **Windows 2003 Server, Enterprise Edition** y, a continuación, haga clic en **Aceptar**.  

    > [!IMPORTANT]  
    >  No seleccione **Windows 2008 Server, Enterprise Edition**.  

5.  En el cuadro de diálogo **Propiedades de plantilla nueva** , en la pestaña **General** , escriba el nombre de la plantilla para generar los certificados web que se utilizarán en los sistemas de sitio de Configuration Manager, como por ejemplo **Certificado de servidor web de Configuration Manager**.  

6.  Haga clic en la pestaña **Nombre de sujeto** y asegúrese de que se haya seleccionado **Proporcionado por el solicitante** .  

7.  Haga clic en la pestaña **Seguridad** y elimine el permiso **Inscribir** de los grupos de seguridad **Admins. del dominio** y **Administradores de organización**.  

8.  Haga clic en **Agregar**, escriba **Servidores IIS de Configuration Manager** en el cuadro de texto y, a continuación, haga clic en **Aceptar**.  

9. Seleccione el permiso **Inscribir** para este grupo y no desactive el permiso **Leer** .  

10. Haga clic en **Aceptar**y cierre la **Consola de plantillas de certificado**.  

11. En la consola de entidad de certificación, haga clic con el botón secundario en **Plantillas de certificado**, haga clic en **Nueva**y, a continuación, haga clic en **Plantilla de certificado que se va a emitir**.  

12. En el cuadro de diálogo **Habilitar plantillas de certificados** , seleccione la nueva plantilla que acaba de crear, **Certificado de servidor web de Configuration Manager**, y, a continuación, haga clic en **Aceptar**.  

13. Si no necesita crear y emitir más certificados, cierre la **Entidad emisora de certificados**.  

###  <a name="a-namebkmkwebserver32008a-requesting-the-web-server-certificate"></a><a name="BKMK_webserver32008"></a> Solicitud del certificado de servidor web  
 Este procedimiento le permite especificar los valores de FQDN de la intranet y de Internet que se configurarán en las propiedades del servidor de sistema de sitio y, a continuación, instala el certificado de servidor web en el servidor miembro que ejecuta IIS.  

##### <a name="to-request-the-web-server-certificate"></a>Para solicitar el certificado de servidor web  

1.  Reinicie el servidor miembro que ejecuta IIS para asegurarse de que el equipo pueda acceder a la plantilla de certificado creada mediante los permisos **Leer** e **Inscribir** que configuró.  

2.  Haga clic en **Inicio**, haga clic en **Ejecutar**, y escriba **mmc.exe.** En la consola vacía, haga clic en **Archivo**y, a continuación, haga clic en **Agregar o quitar complemento**.  

3.  En el cuadro de diálogo **Agregar o quitar complementos** , seleccione **Certificados** en la lista de **Complementos disponibles**y, a continuación, haga clic en **Agregar**.  

4.  En el cuadro de diálogo **Complemento Certificado** , seleccione **Cuenta de equipo**y, a continuación, haga clic en **Siguiente**.  

5.  En el cuadro de diálogo **Seleccionar equipo** , asegúrese de que está seleccionado **Equipo local: (el equipo en el que se está ejecutando esta consola)** y, a continuación, haga clic en **Finalizar**.  

6.  En el cuadro de diálogo **Agregar o quitar complementos** , haga clic en **Aceptar**.  

7.  En la consola, expanda **Certificados (equipo local)**y, a continuación, haga clic en **Personal**.  

8.  Haga clic con el botón secundario en **Certificados**, haga clic en **Todas las tareas**y, a continuación, haga clic en **Solicitar un nuevo certificado**.  

9. En la página **Antes de empezar** , haga clic en **Siguiente**.  

10. Si ve la página **Seleccionar directiva de inscripción de certificados** , haga clic en **Siguiente**.  

11. En la página **Solicitar certificados**, identifique el **Certificado de servidor web de Configuration Manager** en la lista de certificados que aparecen y, a continuación, haga clic en **Se necesita más información para inscribir este certificado. Haga clic aquí para configurar los valores**.  

12. En el cuadro de diálogo **Propiedades de certificado** , en la pestaña **Sujeto** , no realice cambios en el **Nombre de sujeto**. Esto significa que el cuadro **Valor** de la sección **Nombre de sujeto** permanece en blanco. En su lugar, en la sección **Nombre alternativo** , haga clic en la lista desplegable **Tipo** y, a continuación, seleccione **DNS**.  

13. En el cuadro **Valor**, especifique los valores de FQDN que especificará en las propiedades de sistema de sitio de System Center Configuration Manager y, después, haga clic en **Aceptar** para cerrar el cuadro de diálogo **Propiedades de certificado**.  

     Ejemplos:  

    -   Si el sistema de sitio sólo va a aceptar conexiones de cliente de la intranet y el FQDN de la intranet del servidor de sistema de sitio es **server1.internal.contoso.com**: Escriba **server1.internal.contoso.com**y, a continuación, haga clic en **Agregar**.  

    -   Si el sistema de sitio va a aceptar conexiones de cliente desde la intranet e Internet, y el FQDN de la intranet del servidor de sistema de sitio es **server1.internal.contoso.com** y el FQDN de Internet del servidor de sistema de sitio es **server.contoso.com**:  

        1.  Escriba **server1.internal.contoso.com**y, a continuación, haga clic en **Agregar**.  

        2.  Escriba **server.contoso.com**y, a continuación, haga clic en **Agregar**.  

        > [!NOTE]  
        >  No importa en qué orden especifique los FQDN para System Center Configuration Manager. Sin embargo, compruebe que todos los dispositivos que van a utilizar el certificado, como por ejemplo dispositivos móviles y servidores proxy web, puedan utilizar un SAN de certificado y varios valores en el SAN. Si los dispositivos tienen compatibilidad limitada con los valores de SAN en los certificados, tendrá que cambiar el orden de los FQDN o utilizar el valor Sujeto en su lugar.  

14. En la página **Solicitar certificados** , seleccione el **Certificado de servidor web de Configuration Manager** en la lista de certificados que aparecen y, a continuación, haga clic en **Inscribir**.  

15. En la página **Resultados de la instalación de certificados** , espere hasta que se instale el certificado y, a continuación, haga clic en **Finalizar**.  

16. Cierre **Certificados (equipo local)**.  

###  <a name="a-namebkmkwebserver42008a-configuring-iis-to-use-the-web-server-certificate"></a><a name="BKMK_webserver42008"></a> Configuración de IIS para utilizar el certificado de servidor web  
 Este procedimiento permite enlazar el certificado instalado con el **Sitio web predeterminado**de IIS.  

##### <a name="to-configure-iis-to-use-the-web-server-certificate"></a>Para configurar IIS para utilizar el certificado de servidor web  

1.  En el servidor miembro que tiene IIS instalado, haga clic en **Inicio**, **Programas**, **Herramientas administrativas**y, finalmente, en **Administrador de Internet Information Services (IIS)**.  

2.  Expanda **Sitios**, haga clic con el botón secundario en **Sitio web predeterminado**y, a continuación, seleccione **Modificar enlaces**.  

3.  Haga clic en la entrada **https** y, a continuación, en **Editar**.  

4.  En el cuadro de diálogo **Modificar enlace de sitio** , seleccione el certificado que solicitó mediante la plantilla de certificados de servidor web de Configuration Manager y, a continuación, haga clic en **Aceptar**.  

    > [!NOTE]  
    >  Si no está seguro de cuál es el certificado correcto, seleccione uno y, a continuación, haga clic en **Ver**. Esto permite comparar los detalles del certificado seleccionado con los certificados que se muestran con el complemento Certificados. Por ejemplo, el complemento Certificados muestra la plantilla de certificado que se usó para solicitar el certificado. A continuación podrá comparar la huella digital del certificado que se solicitó con la plantilla de certificados de servidor web de Configuration Manager con la huella digital del certificado actualmente seleccionado en el cuadro de diálogo **Modificar enlace de sitio** .  

5.  Haga clic en **Aceptar** en el cuadro de diálogo **Modificar enlace de sitio** y, a continuación, haga clic en **Cerrar**.  

6.  Cierre el **Administrador de Internet Information Services (IIS)**.  

 El servidor miembro cuenta ahora con un certificado de servidor web de System Center Configuration Manager.  

> [!IMPORTANT]  
>  Al instalar el servidor de sistema de sitio de System Center Configuration Manager en este equipo, asegúrese de especificar los mismos FQDN en las propiedades del sistema de sitio que especificó al solicitar el certificado.  

##  <a name="a-namebkmkclouddp2008cm2012a-deploying-the-service-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddp2008_cm2012"></a> Implementación del certificado de servicio para puntos de distribución basados en la nube  

> [!NOTE]  
>  El certificado de servicio para puntos de distribución basados en la nube se aplica a System Center Configuration Manager SP1 y versiones posteriores.  

 Esta implementación de certificado consta de los siguientes procedimientos:  

-   [Creación y emisión de una plantilla de certificado de servidor web personalizado en la entidad de certificación](#BKMK_clouddpcreating2008)  

-   [Solicitud del certificado de servidor web personalizado](#BKMK_clouddprequesting2008)  

-   [Exportación del certificado de servidor web personalizado para puntos de distribución basados en la nube](#BKMK_clouddpexporting2008)  

###  <a name="a-namebkmkclouddpcreating2008a-creating-and-issuing-a-custom-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_clouddpcreating2008"></a> Creación y emisión de una plantilla de certificado de servidor web personalizado en la entidad de certificación  
 Este procedimiento permite crear una plantilla de certificado personalizado que se basa en la plantilla de certificado de servidor web. Se trata de un certificado para puntos de distribución basados en la nube de System Center Configuration Manager y la clave privada debe ser exportable. La plantilla de certificado, una vez creada, se agrega a la entidad de certificación.  

> [!NOTE]  
>  Este procedimiento utiliza una plantilla de certificado diferente de la plantilla de certificado de servidor web creada para sistemas de sitio que ejecutan IIS, ya que, aunque ambos certificados requieren capacidad de autenticación de servidor, en el caso del certificado para puntos de distribución basados en la nube es necesario que usted escriba un valor personalizado para el Nombre de sujeto y la clave privada debe exportarse. Por motivos de seguridad, se recomienda no configurar plantillas de certificado que permitan la exportación de la clave privada a menos que se requiera esta configuración. El punto de distribución basado en la nube requiere esta configuración porque usted debe importar el certificado como un archivo, en lugar de seleccionarlo en el almacén de certificados.  
>   
>  Al crear una nueva plantilla de certificado para este certificado, puede restringir qué equipos solicitan un certificado que permite la exportación de la clave privada. En una red de producción, también podría agregar las siguientes modificaciones para este certificado:  
>   
>  -   Solicitar aprobación para instalar el certificado, para mayor seguridad.  
> -   Incrementar el periodo de validez del certificado. Como debe exportar e importar el certificado siempre antes de que expire, al incrementar el período de validez se reduce la frecuencia con la que debe repetir este procedimiento. Sin embargo, al incrementar el periodo de validez se reduce la seguridad del certificado, porque un atacante tendría más tiempo para descifrar la clave privada y robar el certificado.  
> -   Utilice un valor personalizado en el Nombre alternativo del sujeto (SAN) del certificado para ayudar a distinguir este certificado de los certificados de servidor web estándar que utiliza con IIS.  

##### <a name="to-create-and-issue-the-custom-web-server-certificate-template-on-the-certification-authority"></a>Para crear y emitir la plantilla de certificado de servidor web personalizado en la entidad de certificación  

1.  Cree un grupo de seguridad denominado **Servidores de sitio de Configuration Manager** que contenga los servidores miembro para instalar los servidores de sitio primario de System Center Configuration Manager que administrarán los puntos de distribución basados en la nube.  

2.  En el servidor miembro que ejecuta la consola de entidad de certificación, haga clic con el botón secundario en **Plantillas de certificado**y, a continuación, haga clic en **Administrar** para cargar la consola de administración de las plantillas de certificado.  

3.  En el panel de resultados, haga clic con el botón secundario en la entrada que muestra **Servidor web** en la columna **Nombre para mostrar plantilla**y, a continuación, haga clic en **Duplicar plantilla**.  

4.  En el cuadro de diálogo **Duplicar plantilla** , asegúrese de que se haya seleccionado **Windows 2003 Server, Enterprise Edition** y, a continuación, haga clic en **Aceptar**.  

    > [!IMPORTANT]  
    >  No seleccione **Windows 2008 Server, Enterprise Edition**.  

5.  En el cuadro de diálogo **Propiedades de plantilla nueva** , en la pestaña **General** , escriba el nombre de la plantilla para generar el certificado de servidor web para puntos de distribución basados en la nube, como por ejemplo **Certificado de puntos de distribución basados en la nube de Configuration Manager**.  

6.  Haga clic en la pestaña **Tratamiento de la petición** y seleccione **Permitir que la clave privada se pueda exportar**.  

7.  Haga clic en la pestaña **Seguridad** y elimine el permiso **Inscribir** del grupo de seguridad **Administradores de organización** .  

8.  Haga clic en **Agregar**, escriba **Servidores de sitio de Configuration Manager** en el cuadro de texto y, a continuación, haga clic en **Aceptar**.  

9. Seleccione el permiso **Inscribir** para este grupo y no desactive el permiso **Leer** .  

10. Haga clic en **Aceptar** y cierre la **Consola de plantillas de certificado**.  

11. En la consola de entidad de certificación, haga clic con el botón secundario en **Plantillas de certificado**, haga clic en **Nueva**y, a continuación, haga clic en **Plantilla de certificado que se va a emitir**.  

12. En el cuadro de diálogo **Habilitar plantillas de certificados** , seleccione la nueva plantilla que acaba de crear, **Certificado de puntos de distribución basados en la nube de Configuration Manager**, y, a continuación, haga clic en **Aceptar**.  

13. Si no tiene que crear y emitir más certificados, cierre la **Entidad de certificación**.  

###  <a name="a-namebkmkclouddprequesting2008a-requesting-the-custom-web-server-certificate"></a><a name="BKMK_clouddprequesting2008"></a> Solicitud del certificado de servidor web personalizado  
 Este procedimiento permite solicitar y, a continuación, instalar el certificado de servidor web personalizado en el servidor miembro que ejecutará el servidor de sitio.  

##### <a name="to-request-the-custom-web-server-certificate"></a>Para solicitar el certificado de servidor web personalizado  

1.  Reinicie el servidor miembro después de crear y configurar el grupo de seguridad **Servidores de sitio de Configuration Manager** para asegurarse de que el equipo puede acceder a la plantilla de certificado creada, mediante los permisos **Leer** e **Inscribir** configurados.  

2.  Haga clic en **Inicio**, haga clic en **Ejecutar**, y escriba **mmc.exe.** En la consola vacía, haga clic en **Archivo**y, a continuación, haga clic en **Agregar o quitar complemento**.  

3.  En el cuadro de diálogo **Agregar o quitar complementos** , seleccione **Certificados** en la lista de **Complementos disponibles**y, a continuación, haga clic en **Agregar**.  

4.  En el cuadro de diálogo **Complemento Certificado** , seleccione **Cuenta de equipo**y, a continuación, haga clic en **Siguiente**.  

5.  En el cuadro de diálogo **Seleccionar equipo** , asegúrese de que está seleccionado **Equipo local: (el equipo en el que se está ejecutando esta consola)** y, a continuación, haga clic en **Finalizar**.  

6.  En el cuadro de diálogo **Agregar o quitar complementos** , haga clic en **Aceptar**.  

7.  En la consola, expanda **Certificados (equipo local)**y, a continuación, haga clic en **Personal**.  

8.  Haga clic con el botón secundario en **Certificados**, haga clic en **Todas las tareas**y, a continuación, haga clic en **Solicitar un nuevo certificado**.  

9. En la página **Antes de empezar** , haga clic en **Siguiente**.  

10. Si ve la página **Seleccionar directiva de inscripción de certificados** , haga clic en **Siguiente**.  

11. En la página **Solicitar certificados**, identifique el **Certificado de puntos de distribución basados en la nube de Configuration Manager** en la lista de certificados que aparecen y, a continuación, haga clic en **Se necesita más información para inscribir este certificado. Haga clic aquí para configurar los valores**.  

12. En el cuadro de diálogo **Propiedades de certificado** , en la pestaña **Sujeto** , para el **Nombre de sujeto**, seleccione **Nombre común** como **Tipo**.  

13. En el cuadro **Valor** , especifique el nombre de servicio que desee y su nombre de dominio con un formato FQDN. Por ejemplo: **clouddp1.contoso.com**.  

    > [!NOTE]  
    >  No importa qué nombre de servicio especifique, siempre y cuando sea único en su espacio de nombres. Utilizará DNS para crear un alias (registro CNAME) para asignar este nombre de servicio a un identificador generado automáticamente (GUID) y una dirección IP de Windows Azure.  

14. Haga clic en **Agregar**, y haga clic en **Aceptar** para cerrar el cuadro de diálogo **Propiedades de certificado** .  

15. En la página **Solicitar certificados** , seleccione el **Certificado de puntos de distribución basados en la nube de Configuration Manager** en la lista de certificados que aparecen y, a continuación, haga clic en **Inscribir**.  

16. En la página **Resultados de la instalación de certificados** , espere hasta que se instale el certificado y, a continuación, haga clic en **Finalizar**.  

17. Cierre **Certificados (equipo local)**.  

###  <a name="a-namebkmkclouddpexporting2008a-exporting-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddpexporting2008"></a> Exportación del certificado de servidor web personalizado para puntos de distribución basados en la nube  
 Este procedimiento permite exportar el certificado de servidor web personalizado a un archivo, de modo que se pueda importar al crear el punto de distribución basado en la nube.  

##### <a name="to-export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a>Para exportar el certificado de servidor web personalizado para puntos de distribución basados en la nube  

1.  En la consola **Certificados (equipo local)** , haga clic con el botón secundario en el certificado que acaba de instalar, seleccione **Todas las tareas**y, a continuación, haga clic en **Exportar**.  

2.  En el Asistente para exportación de certificados, haga clic en **Siguiente**.  

3.  En la página **Exportar la clave privada** , seleccione **Exportar la clave privada**y, a continuación, haga clic en **Siguiente**.  

    > [!NOTE]  
    >  Si esta opción no está disponible, significa que el certificado se creó sin la opción de exportar la clave privada. En este escenario, no se puede exportar el certificado en el formato requerido. Debe volver a configurar la plantilla de certificado para que permita la exportación de la clave privada y, a continuación, solicitar el certificado de nuevo.  

4.  En la página **Formato de archivo de exportación** , asegúrese de que está seleccionada la opción **Intercambio de información personal: PKCS #12 (.PFX)** .  

5.  En la página **Contraseña** , especifique una contraseña segura para proteger el certificado exportado con su clave privada y, a continuación, haga clic en **Siguiente**.  

6.  En la página **Archivo para exportar** , especifique el nombre del archivo que desea exportar y, a continuación, haga clic en **Siguiente**.  

7.  Para cerrar el Asistente, haga clic en **Finalizar** en la página **Asistente para exportación de certificados** , y haga clic en **Aceptar** en el cuadro de diálogo de confirmación.  

8.  Cierre **Certificados (equipo local)**.  

9. Almacene el archivo de forma segura y asegúrese de que puede acceder al mismo desde la consola de System Center Configuration Manager.  

 El certificado ya está listo para importarse al crear un punto de distribución basado en la nube.  

##  <a name="a-namebkmkclient2008cm2012a-deploying-the-client-certificate-for-windows-computers"></a><a name="BKMK_client2008_cm2012"></a> Implementación del certificado de cliente para equipos Windows  
 Esta implementación de certificado consta de los siguientes procedimientos:  

-   Creación y emisión de la plantilla de certificado de autenticación de estación de trabajo en la entidad de certificación  

-   Configuración de la inscripción automática de la plantilla de autenticación de estación de trabajo mediante una directiva de grupo  

-   Inscripción automática del certificado de autenticación de estación de trabajo y comprobación de su instalación en los equipos  

###  <a name="a-namebkmkclient02008a-creating-and-issuing-the-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_client02008"></a> Creación y emisión de la plantilla de certificado de autenticación de estación de trabajo en la entidad de certificación  
 Mediante este procedimiento se crea una plantilla de certificado para equipos cliente de System Center Configuration Manager y se agrega a la entidad de certificación.  

##### <a name="to-create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a>Para crear y emitir la plantilla de certificado de autenticación de estación de trabajo en la entidad de certificación  

1.  En el servidor miembro que ejecuta la consola de entidad de certificación, haga clic con el botón secundario en **Plantillas de certificado**y, a continuación, haga clic en **Administrar** para cargar la consola de administración de las plantillas de certificado.  

2.  En el panel de resultados, haga clic con el botón secundario en la entrada que muestra **Autenticación de estación de trabajo** en la columna **Nombre para mostrar plantilla**y, a continuación, haga clic en **Duplicar plantilla**.  

3.  En el cuadro de diálogo **Duplicar plantilla** , asegúrese de que se haya seleccionado **Windows 2003 Server, Enterprise Edition** y, a continuación, haga clic en **Aceptar**.  

    > [!IMPORTANT]  
    >  No seleccione **Windows 2008 Server, Enterprise Edition**.  

4.  En el cuadro de diálogo **Propiedades de plantilla nueva** , en la pestaña **General** , escriba el nombre de la plantilla para generar los certificados de cliente que se utilizarán en los equipos cliente de Configuration Manager, como por ejemplo **Certificado de cliente de Configuration Manager**.  

5.  Haga clic en la pestaña **Seguridad** , seleccione el grupo **Equipos del dominio** y seleccione los permisos adicionales **Leer** e **Inscripción automática**. No desactive **Inscribir**.  

6.  Haga clic en **Aceptar** y cierre la **Consola de plantillas de certificado**.  

7.  En la consola de entidad de certificación, haga clic con el botón secundario en **Plantillas de certificado**, haga clic en **Nueva**y, a continuación, haga clic en **Plantilla de certificado que se va a emitir**.  

8.  En el cuadro de diálogo **Habilitar plantillas de certificados** , seleccione la nueva plantilla que acaba de crear, **Certificado de cliente de Configuration Manager**, y, a continuación, haga clic en **Aceptar**.  

9. Si no necesita crear y emitir más certificados, cierre la **Entidad emisora de certificados**.  

###  <a name="a-namebkmkclient12008a-configuring-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a><a name="BKMK_client12008"></a> Configuración de la inscripción automática de la plantilla de autenticación de estación de trabajo mediante una directiva de grupo  
 Este procedimiento permite configurar una directiva de grupo para la inscripción automática del certificado de cliente en los equipos.  

##### <a name="to-configure-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a>Para configurar la inscripción automática de la plantilla de autenticación de estación de trabajo mediante una directiva de grupo  

1.  En el controlador de dominio, haga clic en **Inicio**, en **Herramientas administrativas**y, finalmente, en **Administración de directivas de grupo**.  

2.  Vaya a su dominio, haga clic con el botón secundario en el dominio y, a continuación, seleccione **Crear un GPO en este dominio y vincularlo aquí**.  

    > [!NOTE]  
    >  En este paso se utiliza el procedimiento recomendado de crear una nueva directiva de grupo para la configuración personalizada en lugar de modificar la directiva predeterminada de dominios que se instala con Servicios de dominio de Active Directory. Mediante la asignación de esta directiva de grupo a nivel de dominio, se aplicará a todos los equipos del dominio. Sin embargo, en un entorno de producción, puede restringir la inscripción automática de modo que se inscriba solo en equipos seleccionados mediante la asignación de la directiva de grupo a nivel de unidad organizativa, o puede filtrar la directiva de grupo de dominio con un grupo de seguridad para que se aplique solo a los equipos del grupo. Si restringe la inscripción automática, no olvide incluir el servidor que está configurado como el punto de administración.  

3.  En el cuadro de diálogo **Nuevo GPO** , escriba un nombre para la directiva de grupo nueva, como **Certificados de inscripción automática**, y haga clic en **Aceptar**.  

4.  En el panel de resultados, en la pestaña **Objetos de directiva de grupo vinculados** , haga clic con el botón secundario en la directiva de grupo nueva y, a continuación, haga clic en **Editar**.  

5.  En el cuadro de diálogo **Editor de administración de directivas de grupo**, expanda **Directivas** bajo **Configuración del equipo**y, a continuación, navegue a **Configuración de Windows** / **Configuración de seguridad** / **Public Key Directivas**.  

6.  Haga clic con el botón derecho en el tipo de objeto **Cliente de Servicios de Certificate Server - Inscripción automática** y, después, haga clic en **Propiedades**.  

7.  En la lista desplegable **Modelo de configuración** , seleccione **Habilitado**, seleccione **Renovar certificados expirados, actualizar certificados pendientes y quitar certificados revocados**, seleccione **Actualizar certificados que usan plantillas de certificado**y, a continuación, haga clic en **Aceptar**.  

8.  Cierre **Administración de directivas de grupo**.  

###  <a name="a-namebkmkclient22008a-automatically-enrolling-the-workstation-authentication-certificate-and-verifying-its-installation-on-computers"></a><a name="BKMK_client22008"></a> Inscripción automática del certificado de autenticación de estación de trabajo y comprobación de su instalación en los equipos  
 Este procedimiento instala el certificado de cliente en los equipos y comprueba la instalación.  

##### <a name="to-automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-the-client-computer"></a>Para inscribir automáticamente el certificado de autenticación de estación de trabajo y comprobar su instalación en el equipo cliente  

1.  Reinicie el equipo de estación de trabajo, y espere unos minutos antes de iniciar sesión.  

    > [!NOTE]  
    >  Reiniciar un equipo es el método más fiable para realizar correctamente la inscripción automática de certificados.  

2.  Inicie sesión con una cuenta que tenga privilegios administrativos.  

3.  En el cuadro de búsqueda, escriba **mmc.exe.**y, a continuación, presione **Intro**.  

4.  En la consola de administración vacía, haga clic en **Archivo**y, a continuación, haga clic en **Agregar o quitar complemento**.  

5.  En el cuadro de diálogo **Agregar o quitar complementos** , seleccione **Certificados** en la lista de **Complementos disponibles**y, a continuación, haga clic en **Agregar**.  

6.  En el cuadro de diálogo **Complemento Certificado** , seleccione **Cuenta de equipo**y, a continuación, haga clic en **Siguiente**.  

7.  En el cuadro de diálogo **Seleccionar equipo** , asegúrese de que está seleccionado **Equipo local: (el equipo en el que se está ejecutando esta consola)** y, a continuación, haga clic en **Finalizar**.  

8.  En el cuadro de diálogo **Agregar o quitar complementos** , haga clic en **Aceptar**.  

9. En la consola, expanda **Certificados (equipo local)**, expanda **Personal**y, a continuación, haga clic en **Certificados**.  

10. En el panel de resultados, confirme que existe un certificado que muestre **Autenticación de cliente** en la columna **Propósito planteado** , y que aparece **Certificado de cliente de Configuration Manager** en la columna **Plantilla de certificado** .  

11. Cierre **Certificados (equipo local)**.  

12. Repita los pasos del 1 al 11 para el servidor miembro para comprobar que el servidor que se va a configurar como punto de administración también tiene un certificado de cliente.  

 El equipo cuenta ahora con un certificado cliente de System Center Configuration Manager.  

##  <a name="a-namebkmkclientdistributionpoint2008cm2012a-deploying-the-client-certificate-for-distribution-points"></a><a name="BKMK_clientdistributionpoint2008_cm2012"></a> Implementación del certificado de cliente para puntos de distribución  

> [!NOTE]  
>  Este certificado también se puede utilizar para imágenes de medios que no utilicen el arranque PXE porque los requisitos del certificado son los mismos.  

 Esta implementación de certificado consta de los siguientes procedimientos:  

-   Creación y emisión de una plantilla de certificado de autenticación de estación de trabajo personalizada en la entidad de certificación  

-   Solicitud del certificado de autenticación de estación de trabajo personalizado  

-   Exportación del certificado de cliente para puntos de distribución  

###  <a name="a-namebkmkclientdistributionpoint02008a-creating-and-issuing-a-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_clientdistributionpoint02008"></a> Creación y emisión de una plantilla de certificado de autenticación de estación de trabajo personalizada en la entidad de certificación  
 Mediante este procedimiento se crea una plantilla de certificado personalizado para puntos de distribución de System Center Configuration Manager que permite exportar la clave privada y se agrega la plantilla de certificado a la entidad de certificación.  

> [!NOTE]  
>  La plantilla de certificado que se utiliza para este procedimiento no es la misma que creó para los equipos cliente porque, aunque ambos certificados requieren la capacidad de autenticación de cliente, el certificado para puntos de distribución requiere la exportación de la clave privada. Por motivos de seguridad, se recomienda no configurar plantillas de certificado que permitan la exportación de la clave privada a menos que se requiera esta configuración. El punto de distribución requiere esta configuración porque se debe importar el certificado como un archivo, en lugar de seleccionarlo en el almacén de certificados.  
>   
>  Al crear una nueva plantilla de certificado para este certificado, puede restringir qué equipos solicitan un certificado que permite la exportación de la clave privada. En nuestra implementación de ejemplo, se tomará el grupo de seguridad que creó anteriormente para los servidores de sistema de sitio de System Center Configuration Manager que ejecutan IIS. En una red de producción que distribuye los roles del sistema de sitio de IIS, considere la creación de un grupo de seguridad nuevo para los servidores que ejecuten puntos de distribución; así, podrá restringir el certificado específicamente a estos servidores de sistema de sitio. También podría agregar las siguientes modificaciones para este certificado:  
>   
>  -   Solicitar aprobación para instalar el certificado, para mayor seguridad.  
> -   Incrementar el periodo de validez del certificado. Como debe exportar e importar el certificado siempre antes de que expire, al incrementar el período de validez se reduce la frecuencia con la que debe repetir este procedimiento. Sin embargo, al incrementar el periodo de validez se reduce la seguridad del certificado, porque un atacante tendría más tiempo para descifrar la clave privada y robar el certificado.  
> -   Utilice un valor personalizado en el campo Sujeto del certificado, o el nombre alternativo del sujeto (SAN, por sus siglas en inglés) para facilitar la identificación de este certificado entre los certificados de cliente estándar. Esto puede resultar especialmente útil si va a utilizar el mismo certificado para varios puntos de distribución.  

##### <a name="to-create-and-issue-the-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a>Para crear y emitir la plantilla de certificado de autenticación de estación de trabajo personalizada en la entidad de certificación  

1.  En el servidor miembro que ejecuta la consola de entidad de certificación, haga clic con el botón secundario en **Plantillas de certificado**y, a continuación, haga clic en **Administrar** para cargar la consola de administración de las plantillas de certificado.  

2.  En el panel de resultados, haga clic con el botón secundario en la entrada que muestra **Autenticación de estación de trabajo** en la columna **Nombre para mostrar plantilla**y, a continuación, haga clic en **Duplicar plantilla**.  

3.  En el cuadro de diálogo **Duplicar plantilla** , asegúrese de que se haya seleccionado **Windows 2003 Server, Enterprise Edition** y, a continuación, haga clic en **Aceptar**.  

    > [!IMPORTANT]  
    >  No seleccione **Windows 2008 Server, Enterprise Edition**.  

4.  En el cuadro de diálogo **Propiedades de plantilla nueva** , en la pestaña **General** , escriba un nombre para la plantilla para generar el certificado de autenticación de cliente para puntos de distribución, como, por ejemplo **Certificado de punto de distribución de cliente de Configuration Manager**.  

5.  Haga clic en la pestaña **Tratamiento de la petición** y seleccione **Permitir que la clave privada se pueda exportar**.  

6.  Haga clic en la pestaña **Seguridad** y elimine el permiso **Inscribir** del grupo de seguridad **Administradores de organización** .  

7.  Haga clic en **Agregar**, escriba **Servidores IIS de Configuration Manager** en el cuadro de texto y, a continuación, haga clic en **Aceptar**.  

8.  Seleccione el permiso **Inscribir** para este grupo y no desactive el permiso **Leer** .  

9. Haga clic en **Aceptar** y cierre la **Consola de plantillas de certificado**.  

10. En la consola de entidad de certificación, haga clic con el botón secundario en **Plantillas de certificado**, haga clic en **Nueva**y, a continuación, haga clic en **Plantilla de certificado que se va a emitir**.  

11. En el cuadro de diálogo **Habilitar plantillas de certificados** , seleccione la nueva plantilla que acaba de crear, **Certificado de punto de distribución de cliente de Configuration Manager**, y, a continuación, haga clic en **Aceptar**.  

12. Si no tiene que crear y emitir más certificados, cierre la **Entidad de certificación**.  

###  <a name="a-namebkmkclientdistributionpoint12008a-requesting-the-custom-workstation-authentication-certificate"></a><a name="BKMK_clientdistributionpoint12008"></a> Solicitud del certificado de autenticación de estación de trabajo personalizado  
 Este procedimiento solicita y, a continuación, instala el certificado de cliente personalizado en el servidor miembro que ejecuta IIS y que se configurará como punto de distribución.  

##### <a name="to-request-the-custom-workstation-authentication-certificate"></a>Para solicitar el certificado de autenticación de estación de trabajo personalizado  

1.  Haga clic en **Inicio**, haga clic en **Ejecutar**, y escriba **mmc.exe.** En la consola vacía, haga clic en **Archivo**y, a continuación, haga clic en **Agregar o quitar complemento**.  

2.  En el cuadro de diálogo **Agregar o quitar complementos** , seleccione **Certificados** en la lista de **Complementos disponibles**y, a continuación, haga clic en **Agregar**.  

3.  En el cuadro de diálogo **Complemento Certificado** , seleccione **Cuenta de equipo**y, a continuación, haga clic en **Siguiente**.  

4.  En el cuadro de diálogo **Seleccionar equipo** , asegúrese de que está seleccionado **Equipo local: (el equipo en el que se está ejecutando esta consola)** y, a continuación, haga clic en **Finalizar**.  

5.  En el cuadro de diálogo **Agregar o quitar complementos** , haga clic en **Aceptar**.  

6.  En la consola, expanda **Certificados (equipo local)**y, a continuación, haga clic en **Personal**.  

7.  Haga clic con el botón secundario en **Certificados**, haga clic en **Todas las tareas**y, a continuación, haga clic en **Solicitar un nuevo certificado**.  

8.  En la página **Antes de empezar** , haga clic en **Siguiente**.  

9. Si ve la página **Seleccionar directiva de inscripción de certificados** , haga clic en **Siguiente**.  

10. En la página **Solicitar certificados** , seleccione el **Certificado de punto de distribución de cliente de Configuration Manager** en la lista de certificados que aparecen y, a continuación, haga clic en **Inscribir**.  

11. En la página **Resultados de la instalación de certificados** , espere hasta que se instale el certificado y, a continuación, haga clic en **Finalizar**.  

12. En el panel de resultados, confirme que existe un certificado que muestre **Autenticación de cliente** en la columna **Propósito planteado** , y que aparece **Certificado de punto de distribución de cliente de Configuration Manager** en la columna **Plantilla de certificado** .  

13. No cierre **Certificados (equipo local)**.  

###  <a name="a-namebkmkexportclientdistributionpoint22008a-exporting-the-client-certificate-for-distribution-points"></a><a name="BKMK_exportclientdistributionpoint22008"></a> Exportación del certificado de cliente para puntos de distribución  
 Este procedimiento exporta el certificado de autenticación de estación de trabajo personalizado a un archivo para que, así, se pueda importar en las propiedades del punto de distribución.  

##### <a name="to-export-the-client-certificate-for-distribution-points"></a>Para exportar el certificado de cliente para puntos de distribución  

1.  En la consola **Certificados (equipo local)** , haga clic con el botón secundario en el certificado que acaba de instalar, seleccione **Todas las tareas**y, a continuación, haga clic en **Exportar**.  

2.  En el Asistente para exportación de certificados, haga clic en **Siguiente**.  

3.  En la página **Exportar la clave privada** , seleccione **Exportar la clave privada**y, a continuación, haga clic en **Siguiente**.  

    > [!NOTE]  
    >  Si esta opción no está disponible, significa que el certificado se creó sin la opción de exportar la clave privada. En este escenario, no se puede exportar el certificado en el formato requerido. Debe volver a configurar la plantilla de certificado para que permita la exportación de la clave privada y, a continuación, solicitar el certificado de nuevo.  

4.  En la página **Formato de archivo de exportación** , asegúrese de que está seleccionada la opción **Intercambio de información personal: PKCS #12 (.PFX)** .  

5.  En la página **Contraseña** , especifique una contraseña segura para proteger el certificado exportado con su clave privada y, a continuación, haga clic en **Siguiente**.  

6.  En la página **Archivo para exportar** , especifique el nombre del archivo que desea exportar y, a continuación, haga clic en **Siguiente**.  

7.  Para cerrar el Asistente, haga clic en **Finalizar** en la página **Asistente para exportación de certificados** , y haga clic en **Aceptar** en el cuadro de diálogo de confirmación.  

8.  Cierre **Certificados (equipo local)**.  

9. Almacene el archivo de forma segura y asegúrese de que puede acceder al mismo desde la consola de System Center Configuration Manager.  

 El certificado está ahora preparado para su importación cuando configure el punto de distribución.  

> [!TIP]  
>  Puede utilizar el mismo archivo de certificado cuando configure imágenes de medios para una implementación de sistema operativo que no utilice arranque PXE, y cuya secuencia de tareas de instalación de imagen deba ponerse en contacto con un punto de administración que requiera conexiones de cliente HTTPS.  

##  <a name="a-namebkmkmobiledevices2008cm2012a-deploying-the-enrollment-certificate-for-mobile-devices"></a><a name="BKMK_mobiledevices2008_cm2012"></a> Implementación del certificado de inscripción para dispositivos móviles  
 Esta implementación de certificado consta de un único procedimiento para crear y emitir la plantilla de certificado de inscripción en la entidad de certificación.  

### <a name="creating-and-issuing-the-enrollment-certificate-template-on-the-certification-authority"></a>Creación y emisión de la plantilla de certificado de inscripción en la entidad de certificación  
 Mediante este procedimiento se crea una plantilla de certificado de inscripción para dispositivos móviles de System Center Configuration Manager y se agrega a la entidad de certificación.  

##### <a name="to-create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Para crear y emitir la plantilla de certificado de inscripción en la entidad de certificación  

1.  Cree un grupo de seguridad que contenga los usuarios que inscribirán dispositivos móviles en System Center Configuration Manager.  

2.  En el servidor miembro que tenga Servicios de servidor de certificados instalados, en la consola de entidad de certificación, haga clic con el botón secundario en **Plantillas de certificado**y, a continuación, haga clic en **Administrar** para cargar la consola de administración de las plantillas de certificado.  

3.  En el panel de resultados, haga clic con el botón secundario en la entrada que muestra **Sesión autenticada** en la columna **Nombre para mostrar plantilla**y, a continuación, haga clic en **Duplicar plantilla**.  

4.  En el cuadro de diálogo **Duplicar plantilla** , asegúrese de que se haya seleccionado **Windows 2003 Server, Enterprise Edition** y, a continuación, haga clic en **Aceptar**.  

    > [!IMPORTANT]  
    >  No seleccione **Windows 2008 Server, Enterprise Edition**.  

5.  En el cuadro de diálogo **Propiedades de plantilla nueva**, en la pestaña **General**, escriba el nombre de la plantilla para generar los certificados de inscripción para los dispositivos móviles que va a administrar System Center Configuration Manager, como **Certificado de inscripción de dispositivos móviles de Configuration Manager**.  

6.  Haga clic en la pestaña **Nombre de sujeto** , asegúrese de que está seleccionado **Construido a partir de esta información de Active Directory** , seleccione **Nombre común** para el **Formato de nombre de sujeto** y desactive **Nombre principal del usuario (UPN)** en **Incluir esta información en un nombre de sujeto alternativo**.  

7.  Haga clic en la pestaña **Seguridad** , seleccione el grupo de seguridad que contiene los usuarios que van a inscribir dispositivos móviles, y seleccione el permiso adicional de **Inscribir**. No desactive **Leer**.  

8.  Haga clic en **Aceptar** y cierre la **Consola de plantillas de certificado**.  

9. En la consola de entidad de certificación, haga clic con el botón secundario en **Plantillas de certificado**, haga clic en **Nueva**y, a continuación, haga clic en **Plantilla de certificado que se va a emitir**.  

10. En el cuadro de diálogo **Habilitar plantillas de certificados** , seleccione la nueva plantilla que acaba de crear, **Certificado de inscripción de dispositivos móviles de Configuration Manager**, y, a continuación, haga clic en **Aceptar**.  

11. Si no necesita crear y emitir más certificados, cierre la consola de entidad de certificación.  

 La plantilla de certificado de inscripción de dispositivos móviles se podrá seleccionar ahora cuando configure un perfil de inscripción de dispositivo móvil en la configuración de cliente.  

##  <a name="a-namebkmkamt2008cm2012a-deploying-the-certificates-for-amt"></a><a name="BKMK_AMT2008_cm2012"></a> Implementación de los certificados para AMT  
 Esta implementación de certificado consta de los siguientes procedimientos:  

-   Creación, emisión e instalación del certificado de aprovisionamiento de AMT  

-   Creación y emisión del certificado de servidor web para equipos basados en AMT  

-   Creación y emisión de los certificados de autenticación del cliente para equipos basados en AMT 802.1X  

###  <a name="a-namebkmkamtprovisioning2008a-creating-issuing-and-installing-the-amt-provisioning-certificate"></a><a name="BKMK_AMTprovisioning2008"></a> Creating, Issuing, and Installing the AMT Provisioning Certificate  
 Cree el certificado de aprovisionamiento con la CA interna al configurar los equipos basados en AMT con la huella digital del certificado de la CA raíz interna. Si este no es el caso y debe usar una entidad de certificación externa, use las instrucciones de la compañía que emite el certificado de aprovisionamiento de AMT, para lo que con frecuencia necesitará solicitar el certificado del sitio web público de la compañía. También podría encontrar instrucciones detalladas para la CA externa de su elección en el Intel vPro Expert Center: Sitio web de manejabilidad de vPro de Microsoft ([http://go.microsoft.com/fwlink/?LinkId=132001](http://go.microsoft.com/fwlink/?LinkId=132001)).  

> [!IMPORTANT]  
>  Las CA externas podrían no admitir el identificador de objetos de aprovisionamiento de Intel AMT. Si este es el caso, utilice el método alternativo de proporcionar el atributo OU del **certificado de instalación del cliente de Intel (R)**.  

 Cuando solicite un certificado de aprovisionamiento de AMT de una CA externa, instale el certificado en el almacén de certificados personal del equipo del servidor miembro que hospedará el punto de servicio fuera de banda.  

##### <a name="to-request-and-issue-the-amt-provisioning-certificate"></a>Para solicitar y emitir el certificado de aprovisionamiento de AMT  

1.  Cree un grupo de seguridad que contenga las cuentas de equipo de los servidores de sistema de sitio que ejecutarán el punto de servicio fuera de banda.  

2.  En el servidor miembro que tenga Servicios de servidor de certificados instalados, en la consola de entidad de certificación, haga clic con el botón secundario en **Plantillas de certificado**y, a continuación, haga clic en **Administrar** para cargar la consola **Plantillas de certificado** .  

3.  En el panel de resultados, haga clic con el botón secundario en la entrada que muestra **Servidor web** en la columna **Nombre para mostrar plantilla** y, a continuación, haga clic en **Duplicar plantilla**.  

4.  En el cuadro de diálogo **Duplicar plantilla** , asegúrese de que se haya seleccionado **Windows 2003 Server, Enterprise Edition** y, a continuación, haga clic en **Aceptar**.  

    > [!IMPORTANT]  
    >  No seleccione **Windows 2008 Server, Enterprise Edition**.  

5.  En el cuadro de diálogo **Propiedades de plantilla nueva** , en la pestaña **General** , escriba el nombre de la plantilla del certificado de aprovisionamiento de AMT, como por ejemplo **Aprovisionamiento de AMT de Configuration Manager**.  

6.  Haga clic en la pestaña **Nombre de sujeto** , seleccione **Construido a partir de esta información de Active Directory**y, a continuación, seleccione **Nombre común**.  

7.  Haga clic en la pestaña **Extensiones** , asegúrese de que está seleccionado **Directivas de aplicación** y, a continuación, haga clic en **Editar**.  

8.  En el cuadro de diálogo **Editar extensión de directivas de aplicación** , haga clic en **Agregar**.  

9. En el cuadro de diálogo **Agregar directivas de aplicación** , haga clic en **Nueva**.  

10. En el cuadro de diálogo **Nueva directiva de aplicación** , escriba **Aprovisionamiento de AMT** en el campo **Nombre** y, a continuación, escriba el siguiente número para el **Identificador de objetos**: **2.16.840.1.113741.1.2.3**.  

11. Haga clic en **Aceptar**y, a continuación, haga clic en **Aceptar** en el cuadro de diálogo **Agregar directivas de aplicación** .  

12. Haga clic en **Aceptar** en el cuadro de diálogo **Editar extensión de directivas de aplicación** .  

13. En el cuadro de diálogo **Propiedades de plantilla nueva** , ahora debería aparecer lo siguiente como la descripción de las **Directivas de aplicación** : **Autenticación del servidor** y **Aprovisionamiento de AMT**.  

14. Haga clic en la pestaña **Seguridad** y elimine el permiso **Inscribir** de los grupos de seguridad **Admins. del dominio** y **Administradores de organización**.  

15. Haga clic en **Agregar**, escriba el nombre de un grupo de seguridad que contenga la cuenta de equipo del rol de sistema de sitio del punto de servicio fuera de banda y, a continuación, haga clic en **Aceptar**.  

16. Seleccione el permiso **Inscribir** para este grupo y no desactive el permiso **Leer** .  

17. Haga clic en **Aceptar**y cierre la consola **Plantillas de certificado** .  

18. En la **Entidad emisora de certificados**, haga clic con el botón secundario en **Plantillas de certificado**, haga clic en **Nueva**y, a continuación, haga clic en **Plantilla de certificado que se va a emitir**.  

19. En el cuadro de diálogo **Habilitar plantillas de certificados** , seleccione la nueva plantilla que acaba de crear, **Aprovisionamiento de AMT de Configuration Manager**, y, a continuación, haga clic en **Aceptar**.  

    > [!NOTE]  
    >  Si no puede completar los pasos 18 o 19, compruebe que está usando la versión Enterprise Edition de Windows Server 2008. Aunque puede configurar plantillas con Windows Server Standard Edition y Servicios de servidor de certificados, no puede implementar certificados con plantillas de certificado modificadas a menos que use la versión Enterprise Edition de Windows Server 2008.  

20. No cierre la **Entidad emisora de certificados**.  

 El certificado de aprovisionamiento de AMT de la CA interna ya está listo para instalarse en el equipo del punto de servicio fuera de banda.  

##### <a name="to-install-the-amt-provisioning-certificate"></a>Para instalar el certificado de aprovisionamiento de AMT  

1.  Reinicie el servidor miembro que ejecuta IIS, para asegurarse de que puede acceder a la plantilla de certificado con el permiso configurado.  

2.  Haga clic en **Inicio**, haga clic en **Ejecutar**, y escriba **mmc.exe.** En la consola vacía, haga clic en **Archivo**y, a continuación, haga clic en **Agregar o quitar complemento**.  

3.  En el cuadro de diálogo **Agregar o quitar complementos** , seleccione **Certificados** en la lista de **Complementos disponibles**y, a continuación, haga clic en **Agregar**.  

4.  En el cuadro de diálogo **Complemento Certificado** , seleccione **Cuenta de equipo**y, a continuación, haga clic en **Siguiente**.  

5.  En el cuadro de diálogo **Seleccionar equipo** , asegúrese de que está seleccionado **Equipo local: (el equipo en el que se está ejecutando esta consola)** y, a continuación, haga clic en **Finalizar**.  

6.  En el cuadro de diálogo **Agregar o quitar complementos** , haga clic en **Aceptar**.  

7.  En la consola, expanda **Certificados (equipo local)**y, a continuación, haga clic en **Personal**.  

8.  Haga clic con el botón secundario en **Certificados**, haga clic en **Todas las tareas**y, a continuación, haga clic en **Solicitar un nuevo certificado**.  

9. En la página **Antes de empezar** , haga clic en **Siguiente**.  

10. Si ve la página **Seleccionar directiva de inscripción de certificados** , haga clic en **Siguiente**.  

11. En la página **Solicitar certificados** , seleccione **Aprovisionamiento de AMT** en la lista de certificados que aparecen y, a continuación, haga clic en **Inscribir**.  

12. En la página **Resultados de la instalación de certificados** , espere hasta que se instale el certificado y, a continuación, haga clic en **Finalizar**.  

13. Cierre **Certificados (equipo local)**.  

 El certificado de aprovisionamiento de AMT de la CA interna ya está instalado y está listo para seleccionarse en las propiedades del punto de servicio de fuera de banda.  

### <a name="creating-and-issuing-the-web-server-certificate-for-amt-based-computers"></a>Creación y emisión del certificado de servidor web para equipos basados en AMT  
 Utilice el siguiente procedimiento para preparar los certificados de servidor web para equipos basados en AMT.  

##### <a name="to-create-and-issue-the-web-server-certificate-template"></a>Para crear y emitir una plantilla de certificado de servidor web  

1.  Cree un grupo de seguridad vacío para que contenga las cuentas de equipo AMT que System Center Configuration Manager crea durante el aprovisionamiento de AMT.  

2.  En el servidor miembro que tenga Servicios de servidor de certificados instalados, en la consola de entidad de certificación, haga clic con el botón secundario en **Plantillas de certificado**y, a continuación, haga clic en **Administrar** para cargar la consola **Plantillas de certificado** .  

3.  En el panel de resultados, haga clic con el botón secundario en la entrada que muestra **Servidor web** en la columna **Nombre para mostrar plantilla**y, a continuación, haga clic en **Duplicar plantilla**.  

4.  En el cuadro de diálogo **Duplicar plantilla** , asegúrese de que se haya seleccionado **Windows 2003 Server, Enterprise Edition** y, a continuación, haga clic en **Aceptar**.  

    > [!IMPORTANT]  
    >  No seleccione **Windows 2008 Server, Enterprise Edition.**  

5.  En el cuadro de diálogo **Propiedades de plantilla nueva** , en la pestaña **General** , escriba el nombre de la plantilla para generar los certificados web que se utilizarán para la administración fuera de banda en los equipos AMT, como por ejemplo **Certificado de servidor web AMT de Configuration Manager**.  

6.  Haga clic en la pestaña **Nombre de sujeto** , haga clic en **Construido a partir de esta información de Active Directory**, seleccione **Nombre común** para el **Formato de nombre de sujeto**y, a continuación, desactive **Nombre principal del usuario (UPN)** para el nombre de sujeto alternativo.  

7.  Haga clic en la pestaña **Seguridad** y elimine el permiso **Inscribir** de los grupos de seguridad **Admins. del dominio** y **Administradores de organización**.  

8.  Haga clic en **Agregar** y escriba el nombre del grupo de seguridad creado para el aprovisionamiento de AMT. A continuación, haga clic en **Aceptar**.  

9. Seleccione los siguientes permisos de **Permitir** para este grupo de seguridad: **Leer** e **Inscribir**.  

10. Haga clic en **Aceptar**y cierre la consola **Plantillas de certificado** .  

11. En la consola **Entidad emisora de certificados** , haga clic con el botón secundario en **Plantillas de certificado**, haga clic en **Nueva**y, a continuación, haga clic en **Plantilla de certificado que se va a emitir**.  

12. En el cuadro de diálogo **Habilitar plantillas de certificados** , seleccione la nueva plantilla que acaba de crear, **Certificado de servidor web AMT de Configuration Manager**, y, a continuación, haga clic en **Aceptar**.  

13. Si no tiene que crear y emitir más certificados, cierre la **Entidad de certificación**.  

 La plantilla de servidor web de AMT ya está lista para el aprovisionamiento de equipos basados en AMT con certificados de servidor web. Seleccione esta plantilla de certificado en las propiedades del componente de administración fuera de banda.  

### <a name="creating-and-issuing-the-client-authentication-certificates-for-8021x-amt-based-computers"></a>Creación y emisión de los certificados de autenticación del cliente para equipos basados en AMT 802.1X  
 Utilice el procedimiento siguiente si los equipos basados en AMT van a utilizar certificados de cliente para redes cableadas o inalámbricas con autenticación 802.1X.  

##### <a name="to-create-and-issue-the-client-authentication-certificate-template-on-the-ca"></a>Para crear y emitir la plantilla de certificado de autenticación del cliente en la CA  

1.  En el servidor miembro que tenga Servicios de servidor de certificados instalados, en la consola de entidad de certificación, haga clic con el botón secundario en **Plantillas de certificado**y, a continuación, haga clic en **Administrar** para cargar la consola **Plantillas de certificado** .  

2.  En el panel de resultados, haga clic con el botón secundario en la entrada que muestra **Autenticación de estación de trabajo** en la columna **Nombre para mostrar plantilla**y, a continuación, haga clic en **Duplicar plantilla**.  

    > [!IMPORTANT]  
    >  No seleccione **Windows 2008 Server, Enterprise Edition.**  

3.  En el cuadro de diálogo **Propiedades de plantilla nueva** , en la pestaña **General** , escriba el nombre de la plantilla para generar los certificados de cliente que se utilizarán para la administración fuera de banda en los equipos AMT, como por ejemplo **Certificado de autenticación del cliente 802.1X AMT de Configuration Manager**.  

4.  Haga clic en la pestaña **Nombre de sujeto** , haga clic en **Construido a partir de esta información de Active Directory** y seleccione **Nombre común** para el **Formato de nombre de sujeto**. Desactive **Nombre DNS** para el nombre de sujeto alternativo y, a continuación, seleccione **Nombre principal del usuario (UPN)**.  

5.  Haga clic en la pestaña **Seguridad** y elimine el permiso **Inscribir** de los grupos de seguridad **Admins. del dominio** y **Administradores de organización**.  

6.  Haga clic en **Agregar** y escriba el nombre del grupo de seguridad que va a especificar en las propiedades del componente de administración fuera de banda, para que contenga las cuentas de equipo de los equipos basados en AMT. A continuación, haga clic en **Aceptar**.  

7.  Seleccione los siguientes permisos de **Permitir** para este grupo de seguridad: **Leer** e **Inscribir**.  

8.  Haga clic en **Aceptar** y cierre la consola de administración **Plantillas de certificado**, **certtmpl - [Plantillas de certificado]**.  

9. En la consola de administración **Entidad emisora de certificados** , haga clic con el botón secundario en **Plantillas de certificado**, haga clic en **Nueva**y, a continuación, haga clic en **Plantilla de certificado que se va a emitir**.  

10. En el cuadro de diálogo **Habilitar plantillas de certificados** , seleccione la nueva plantilla que acaba de crear, **Certificado de autenticación del cliente 802.1X AMT de Configuration Manager**, y, a continuación, haga clic en **Aceptar**.  

11. Si no necesita crear y emitir más certificados, cierre la **Entidad emisora de certificados**.  

 La plantilla de certificado de autenticación del cliente ya está lista para emitir certificados para equipos basados en AMT que se pueden utilizar para la autenticación del cliente 802.1X. Seleccione esta plantilla de certificado en las propiedades del componente de administración fuera de banda.  

##  <a name="a-namebkmkmacclientsp1a-deploying-the-client-certificate-for-mac-computers"></a><a name="BKMK_MacClient_SP1"></a> Implementación del certificado de cliente para equipos Mac  

> [!NOTE]  
>  El certificado de cliente para equipos Mac se aplica a System Center Configuration Manager SP1 y versiones posteriores.  

 Esta implementación de certificado consta de un único procedimiento para crear y emitir la plantilla de certificado de inscripción en la entidad de certificación.  

###  <a name="a-namebkmkmacclientcreatingissuinga-creating-and-issuing-a-mac-client-certificate-template-on-the-certification-authority"></a><a name="BKMK_MacClient_CreatingIssuing"></a> Creación y emisión de una plantilla de certificado de cliente Mac en la entidad de certificación  
 Mediante este procedimiento se crea una plantilla de certificado personalizado para equipos Mac de System Center Configuration Manager y se agrega la plantilla de certificado a la entidad de certificación.  

> [!NOTE]  
>  Este procedimiento utiliza una plantilla de certificado diferente de la plantilla de certificado que podría haber creado para los equipos cliente Windows o para puntos de distribución.  
>   
>  Al crear una nueva plantilla de certificado para este certificado, puede restringir la solicitud de certificado a los usuarios autorizados.  

##### <a name="to-create-and-issue-the-mac-client-certificate-template-on-the-certification-authority"></a>Para crear y emitir la plantilla de certificado de cliente Mac en la entidad de certificación  

1.  Cree un grupo de seguridad que contenga cuentas de usuario para los usuarios administrativos que vayan a inscribir el certificado en el equipo Mac mediante System Center Configuration Manager.  

2.  En el servidor miembro que ejecuta la consola de entidad de certificación, haga clic con el botón secundario en **Plantillas de certificado**y, a continuación, haga clic en **Administrar** para cargar la consola de administración de las plantillas de certificado.  

3.  En el panel de resultados, haga clic con el botón secundario en la entrada que muestra **Sesión autenticada** en la columna **Nombre para mostrar plantilla**y, a continuación, haga clic en **Duplicar plantilla**.  

4.  En el cuadro de diálogo **Duplicar plantilla** , asegúrese de que se haya seleccionado **Windows 2003 Server, Enterprise Edition** y, a continuación, haga clic en **Aceptar**.  

    > [!IMPORTANT]  
    >  No seleccione **Windows 2008 Server, Enterprise Edition**.  

5.  En el cuadro de diálogo **Propiedades de plantilla nueva** , en la pestaña **General** , escriba el nombre de la plantilla para generar el certificado de cliente Mac, como por ejemplo **Certificado de cliente Mac de Configuration Manager**.  

6.  Haga clic en la pestaña **Nombre de sujeto** , asegúrese de que está seleccionado **Construido a partir de esta información de Active Directory** , seleccione **Nombre común** para el **Formato de nombre de sujeto** y desactive **Nombre principal del usuario (UPN)** en **Incluir esta información en un nombre de sujeto alternativo**.  

7.  Haga clic en la pestaña **Seguridad** y elimine el permiso **Inscribir** de los grupos de seguridad **Admins. del dominio** y **Administradores de organización** .  

8.  Haga clic en **Agregar**, especifique el grupo de seguridad creado en el paso uno y, a continuación, haga clic en **Aceptar**.  

9. Seleccione el permiso **Inscribir** para este grupo y no desactive el permiso **Leer** .  

10. Haga clic en **Aceptar** y cierre la **Consola de plantillas de certificado**.  

11. En la consola de entidad de certificación, haga clic con el botón secundario en **Plantillas de certificado**, haga clic en **Nueva**y, a continuación, haga clic en **Plantilla de certificado que se va a emitir**.  

12. En el cuadro de diálogo **Habilitar plantillas de certificados** , seleccione la nueva plantilla que acaba de crear, **Certificado de cliente Mac de Configuration Manager**, y, a continuación, haga clic en **Aceptar**.  

13. Si no tiene que crear y emitir más certificados, cierre la **Entidad de certificación**.  

 La plantilla de certificado de cliente Mac ya está lista para seleccionarse al configurar el cliente para la inscripción.



<!--HONumber=Nov16_HO1-->

