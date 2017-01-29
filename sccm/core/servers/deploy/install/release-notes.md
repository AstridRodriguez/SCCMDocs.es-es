---
title: "Notas de la versión | Microsoft Docs"
description: "Consulte estas notas relativas a problemas urgentes que aún no se han corregido en el producto o no se han tratado en un artículo de Microsoft Knowledge Base."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: 41
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: ea723a6694feb2c9584b35498aa9c3519383f08d
ms.openlocfilehash: a9dc046a54c15d9d299664cd1f2a149383f53489


---
# <a name="release-notes-for-system-center-configuration-manager"></a>Notas de la versión de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Con System Center Configuration Manager, las notas de la versión del producto se limitan a problemas urgentes que aún no se han resuelto en el producto (disponible a través de una actualización en la consola) o problemas detallados en el artículo de Microsoft Knowledge Base.  

 Para problemas conocidos que afectan a los escenarios principales, esta información se muestra en la documentación del producto en línea en la biblioteca de documentación de System Center Configuration Manager.  

> [!TIP]  
>  Este tema contiene notas de la versión de la rama actual de System Center Configuration Manager. Para obtener información sobre la vista previa técnica de System Center Configuration Manager, consulte [Technical Preview for System Center Configuration Manager](../../../../core/get-started/technical-preview.md) (Technical Preview de System Center Configuration Manager).  

## <a name="setup-and-upgrade"></a>Instalación y actualización  

### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>Al instalar un sitio de Rama de mantenimiento a largo plazo mediante la versión 1606, se instala un sitio de Rama actual
Al usar el medio de línea base de la versión 1606 incluido en la versión de octubre de 2016 para instalar un sitio de Rama de mantenimiento a largo plazo (LTSB), el programa de instalación instala en su lugar un sitio de Rama actual. Esto ocurre porque no está seleccionada la opción para instalar un punto de conexión de servicio con la instalación del sitio.

 - Aunque no es necesario un punto de conexión de servicio, se debe seleccionar que se instale durante la instalación de un sitio de LTSB.

Una vez completada la instalación, puede desinstalar el punto de conexión de servicio.  Pero debe tener un punto de conexión de servicio en modo sin conexión o en línea para enviar datos de telemetría y obtener actualizaciones de seguridad de los sitios de Rama actual y LTSB.

Si su sitio se instaló como un sitio de Rama actual pero quería instalar la LTSB, puede desinstalarlo y volver a instalarlo. También puede llamar a [Ayuda y soporte de Microsoft](http://go.microsoft.com/fwlink/?LinkId=243064) para obtener ayuda.  

Para confirmar qué rama está instalada, en la consola, vaya a **Administración** > **Configuración de sitio** > **Sitios** y abra **Configuración de jerarquía**. La opción para convertir el sitio a un sitio de Rama actual solo está disponible cuando el sitio ejecuta la LTSB.  

**Solución alternativa:**  ninguna.   





### <a name="the--sql-server-backup-model-in-use-by-configuration-manager-can-change-from-full-to-simple"></a>El modelo de copia de seguridad de SQL Server que se usa en Configuration Manager puede cambiar de completo a simple  
 Al actualizar a System Center Configuration Manager versión 1511, el modelo de copia de seguridad de SQL Server que usa Configuration Manager puede cambiar de completo a simple.  

-   Si usa una tarea de copia de seguridad de SQL Server personalizada con el modelo de copia de seguridad completa (en lugar de la tarea de copia de seguridad integrada para Configuration Manager), la actualización puede cambiar su modelo de copia de seguridad de completa a sencilla.  

**Solución**: después de actualizar a la versión 1511, revise la configuración de SQL Server y restáurela por completo si es necesario.  

### <a name="when-you-add-a-service-window-to-a-new-site-server-service-windows-that-were---configured-for-another-site-server-are-deleted"></a>Al agregar una ventana de servicio a un nuevo servidor de sitio, se eliminan las ventanas de servicio que se habían configurado para otro servidor de sitio  
 Al usar ventanas de servicio con System Center Configuration Manager versión 1511, solo se pueden configurar ventanas de servicio para un único servidor de sitio en una jerarquía. Si después de configurar ventanas de servicio en un servidor, configura una ventana de servicio en un segundo servidor de sitio, las ventanas de servicio del primero se eliminan de forma silenciosa, sin ningún error ni advertencia.  

**Solución alternativa**: instale la revisión que se describe en el [artículo 3142341 de Microsoft Knowledge Base](http://support.microsoft.com/kb/3142341). Este problema también se resuelve al instalar la actualización 1602 de System Center Configuration Manager.  

### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>Una actualización está detenida con un estado Descargando en el nodo Actualizaciones y mantenimiento de la consola de Configuration Manager  
Durante la descarga automática de actualizaciones por un punto de conexión de servicio en línea, una actualización puede bloquearse con un estado Descargando. Cuando se detiene la descarga de una actualización, aparecen entradas similares a las siguientes en los archivos de registro indicados:  

Registro de DMPdownloader:  

-   ERROR: No se pudo descargar el paquete redistribuible para 037cd17e-4d7b-40e1-802b-14bb682364c7 con el comando /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 RedistVersion 112015/NoUI "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"  

ConfigMgrSetup.log:  

-   Error: Error al comprobar 'd: firma de código de autenticación de \ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi'.  

-   Error: Error de comprobación de la forma de archivo para 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi  

**Solución alternativa**: en el servidor de sitio, modifique la siguiente clave del Registro para que coincida con la siguiente y, luego, reinicie el servicio SMS_Executive o espere 24 horas al próximo ciclo de descarga automática.  

-   **Clave para editar**: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **Valor para estado**: establecido en **146944** decimal o **0x00023e00** hexadecimal  

### <a name="pre-release-features-introduced-in-system-center-configuration-manager-1602"></a>Características de versión preliminar introducidas en System Center Configuration Manager 1602  

Se incluyen características de versión preliminar en el producto para la realización de las primeras pruebas en un entorno de producción, pero no se debe considerar que ya estén listas para él.  

A partir de la actualización 1606, debe dar su consentimiento antes de poder utilizar las características de la versión preliminar. Para obtener más información, consulte [Use pre-release features from updates](../../../../core/servers/manage/install-in-console-updates.md) (Uso de características de la versión preliminar a partir de las actualizaciones).

La versión 1602 de System Center Configuration Manager introduce dos características de versión preliminar:  

-   Acceso condicional para equipos administrados por System Center Configuration Manager. Para obtener más información, consulte [Manage access to O365 services for PCs managed by System Center Configuration Manager](../../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md) (Administración del acceso a servicios de Office 365 para equipos administrados por System Center Configuration Manager).
    - Después de instalar la actualización 1602, el tipo de característica aparece como liberado, aunque se trate de una versión preliminar.
    - Si actualiza de la versión 1602 a la 1606, el tipo de característica se muestra como liberado aunque se conserve la versión preliminar.
    - Si actualiza de la versión 1511 directamente a la versión 1606, el tipo de característica se muestra como versión preliminar.


-   Mantenimiento de una recopilación compatible con clústeres. Para obtener más información, consulte [Service a server group](../../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups) (Mantenimiento de un grupo de servidores) en [Capabilities in Technical Preview 1605 for System Center Configuration Manager](../../../../core/get-started/capabilities-in-technical-preview-1605.md) (Capacidades de Technical Preview 1605 para System Center Configuration Manager).  




### <a name="recovery-options-for-a-secondary-site-are-not-available-in-the-console"></a>Las opciones de recuperación para un sitio secundario no están disponibles en la consola  
Después de producirse un error en la recuperación de un sitio secundario, la opción **Recuperar sitio secundario** ya no está disponible en la consola de Configuration Manager.  

Este problema afecta a System Center Configuration Manager versión 1511 y 1602 y previsiblemente se resolverá en una futura actualización.  

**Solución alternativa**: use uno de los métodos siguientes para recuperar (reinstalar) el sitio secundario:  

-   Use **Preinst.exe** y el comando **/delsite** para quitar el sitio secundario y, a continuación, vuelva a instalarlo. Para obtener más información sobre preinst.exe, consulte [Hierarchy Maintenance Tool (Preinst.exe) for System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md) (Herramienta de mantenimiento de jerarquía (Preinst.exe) para System Center Configuration Manager).  

-   Ejecute el script siguiente para iniciar la recuperación del sitio secundario. Ejecute este script en la base de datos en el sitio primario principal del sitio secundario que desea recuperar:  

    ```  
    declare @SiteCode NVARCHAR(3)=N'<replace with secondary site code>'   

    UPDATE Sites SET Status = 9  
                    , DetailedStatus = 3  
    FROM Sites WHERE SiteCode = @SiteCode  

    UPDATE SCP SET SCP.Value1 = 9  
                    , SCP.Value2 = N'3'  
    FROM SC_SiteDefinition_Property SCP INNER JOIN SC_SiteDefinition SC ON SC.SiteNumber = SCP.SiteNumber  
    WHERE SC.SiteCode = @SiteCode AND SCP.[Name] = N'Requested Status'  
  ```  

###  <a name="setup-fails-when-using-redist-files-from-the-cdlatest-folder-with-a-manifest-verification-error"></a>Se produce un error en el programa de instalación cuando se usan archivos de redistribución de la carpeta CD.Latest con un error de comprobación de manifiesto
Al ejecutar el programa de instalación desde la carpeta CD.Latest creada para la versión 1606 y usar los archivos de redistribución incluidos en dicha carpeta, se produce un error en el programa de instalación. Aparecen los siguientes errores en el registro de instalación de Configuration Manager:

  - ERROR: File hash check failed for defaultcategories.dll
  - ERROR: Manifest verification failed. Wrong version of manifest?

**Solución alternativa:** use uno de los siguientes métodos:
 - Durante la instalación, descargue los archivos de redistribución más recientes de Microsoft, en lugar de usar los que se incluyen en la carpeta CD.Latest.
 - Elimine manualmente la carpeta *cd.latest\redist\languagepack\zhh* y, luego, vuelva a ejecutar la instalación.

### <a name="service-connection-tool-throws-an-exception-when-sql-server-is-remote-or-when-shared-memory-is-disabled"></a>La herramienta de conexión de servicio produce una excepción cuando SQL Server está instalado en una ubicación remota o cuando la memoria compartida está deshabilitada
A partir de la versión 1606, la herramienta de conexión de servicio genera una excepción cuando se cumple una de las siguientes condiciones:  
 -  La base de datos del sitio está instalada en una ubicación remota con respecto al equipo que hospeda el punto de conexión de servicio y usa un puerto no estándar (un puerto distinto de 1433).
 -  La base de datos del sitio está en el mismo servidor que el punto de conexión de servicio, pero la **memoria compartida** del protocolo de SQL está deshabilitada.

La excepción es similar a la siguiente:
 - *Excepción no controlada: System.Data.SqlClient.SqlException: Error relacionado con la red o específico de la instancia mientras se establecía una conexión con el servidor SQL Server. No se encontró el servidor o éste no estaba accesible. Compruebe que el nombre de la instancia es correcto y que SQL Server está configurado para admitir conexiones remotas. (proveedor: Proveedor de canalizaciones con nombre, error: 40 - No se pudo abrir una conexión con SQL Server) --*

**Solución alternativa**: mientras usa la herramienta, debe modificar el registro del servidor que hospeda el punto de conexión de servicio para que incluya información sobre el puerto de SQL Server:

   1.   Antes de usar la herramienta, edite la siguiente clave del Registro y agregue el número del puerto que está en uso con el nombre de SQL Server:
    - Clave: HKLM\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\
      - Valor: &lt;nombre de SQL Server>
    - Agregue: **,&lt;PUERTO>**

    Por ejemplo, para agregar el puerto *15001* a un servidor denominado *testserver.test.net*, la clave resultante sería la siguiente: ***HKLM\Software\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\testserver.test.net,15001***

   2.   Después de agregar el puerto al registro, la herramienta debería funcionar con normalidad.  

   3.   Una vez que haya acabado de usar la herramienta, cambie la clave del Registro al valor original para los pasos **-import** y **-connect**.  






## <a name="backup-and-recovery"></a>Copia de seguridad y recuperación
### <a name="pre-production-client-is-not-available-after-a-site-restore"></a>El cliente de preproducción no está disponible después de una restauración del sitio
Con la versión 1602, si utiliza clientes de preproducción y restaura el sitio de nivel superior de la jerarquía desde una copia de seguridad, la versión del cliente de preproducción no está disponible después de que se restaura el sitio.  

**Solución alternativa:** después de restaurar el sitio de nivel superior de la jerarquía debe copiar manualmente los archivos de cliente de preproducción para que Configuration Manager pueda procesarlos y restaurarlos para su utilización:
1. En el equipo del servidor de sitio de nivel superior, copie el contenido de la carpeta *&lt;CM_Install_Location\>\\Client* en la carpeta *&lt;CM_Install_Location\>\\StagingClient*.

2. Cree un archivo vacío denominado **client.acu** y copie o pegue este archivo en la carpeta *&lt;CM_Install_Location\>\\Inboxes\\hman.box* del servidor de sitio. (Este archivo puede ser un archivo de texto al que se ha cambiado de nombre, siempre y cuando ya no tenga la extensión txt). Después de colocar este archivo en la carpeta hman.box, el Administrador de jerarquía en el servidor de sitio iniciará y procesará los archivos de cliente y restaurará los archivos de cliente de preproducción para su uso.

Este problema se resolvió en la versión 1606.


## <a name="client-deployment-and-upgrade"></a>Actualizaciones e implementaciones de cliente  

### <a name="expansion-to-central-administration-site-stops-automatic-client-upgrades"></a>La expansión al sitio de administración central detiene las actualizaciones automáticas del cliente  
Solo en la versión 1511, no podrá ejecutar actualizaciones de cliente automáticas para ningún sitio que se expanda de un sitio primario al sitio de administración central. Cuando se expande el sitio, el sitio autorizado en el paquete de actualización de cliente no está correctamente establecido en el nuevo sitio de administración central, lo que impide que se ejecuten actualizaciones de cliente automáticas de forma satisfactoria. Este problema solo existe en la versión 1511. En la versión 1602 y versiones posteriores, este problema se ha corregido.  

**Solución alternativa:** ejecute el siguiente script SQL en la base de datos del sitio de administración central. Después de ejecutar el script, las actualizaciones de cliente automáticas se deben empezar a ejecutar con normalidad.  

  ```  
  DECLARE @RootSite AS NVARCHAR(3)  
  DECLARE @SourceServer AS NVARCHAR(255)  
  DECLARE @FullClientPkgSource AS NVARCHAR(255)  
  DECLARE @UpgradePkgSource AS NVARCHAR(255)  

  SELECT @RootSite = SiteCode, @SourceServer = SiteServer  
  FROM sites  
  WHERE ISNULL(ReportToSite, N'') = N''  

  SELECT @FullClientPkgSource = N'\\' + @SourceServer + N'\SMS_' + @RootSite + N'\Client'  
  SELECT @UpgradePkgSource = N'\\' + @SourceServer + N'\SMS_' + @RootSite + N'\ClientUpgrade'  

  UPDATE SMSPackages_G  
  SET Source = @FullClientPkgSource, SourceSite = @RootSite  
  WHERE PkgID IN  
      (SELECT FullPackageID FROM ClientDeploymentSettings)  

  UPDATE SMSPackages_G  
  SET Source = @UpgradePkgSource, SourceSite = @RootSite  
  WHERE PkgID IN  
      (SELECT UpgradePackageID FROM ClientDeploymentSettings)  

  UPDATE ProgramOffers_G  
  SET SourceSite = @RootSite  
  WHERE OfferID IN  
      (SELECT UpgradeAdvertisementID FROM ClientDeploymentSettings)  
  ```  

## <a name="operating-system-deployment"></a>Implementación de sistema operativo  

### <a name="issue-with-the-windows-adk-for-windows-10-version-1511"></a>Problema con el Windows ADK para Windows 10, versión 1511  
Si ejecuta una secuencia de tareas desde el Centro de software que usa una imagen de arranque de Windows PE v.10.0.10586 desde Windows ADK 10 (versión 1511) y el equipo se reinicia en Windows PE, se producirá el siguiente error cuando se estén “Inicializando los dispositivos de hardware”: **error de inicialización de Windows PE con el código 0x80220014**.  

**Solución alternativa**: use Windows 10 ADK original. Para obtener más información, consulte el siguiente blog del Equipo de System Center Configuration Manager: [Issue with the Windows ADK for Windows 10](http://blogs.technet.com/b/configmgrteam/archive/2015/11/20/issue-with-the-windows-adk-for-windows-10-version-1511.aspx)(Problema con Windows ADK para Windows 10).  

### <a name="dynamic-application-installation-fails-during-task-sequence-which-successfully-completes"></a>Se produce un error en la instalación de la aplicación dinámica durante la secuencia de tareas que se completa correctamente  
Cuando se implementa una secuencia de tareas que usa la opción **Instalar aplicaciones según la lista de variables dinámicas**, y una de las aplicaciones no se instalan por cualquier motivo, la secuencia de tareas indica que todo se ha realizado correctamente. Esto ocurre independientemente de cómo se configuran las opciones siguientes:  

-   **Continuar después de un error** (en la pestaña Opciones del paso Instalar aplicación)  

-   **Continuar instalando otras aplicaciones en la lista si se produce un error de instalación de aplicación** (en la pestaña Propiedades del paso Instalar aplicación)  

Puede ver el archivo smsts.log, para determinar si una aplicación no se pudo instalar.  

**Solución alternativa**: use la variable **_TSAppInstallStatus** como una condición en un pasos posterior de una secuencia de tareas con una condición de error de la secuencia de tareas si se hubo un error con una de las aplicaciones dinámicas.  

### <a name="smb-might-not-work-properly-after-you-use-a-task-sequence-to-install-windows-10"></a>Puede que SMB no funcione correctamente después de utilizar una secuencia de tareas para instalar Windows 10  
Cuando utiliza una secuencia de tareas para instalar una imagen de Windows 10, SMB podría no funcionar correctamente después de instalar el cliente de Configuration Manager. Por ejemplo, se podrían producir errores en los siguientes pasos de secuencia de tareas:  

-   Restauración del estado de usuario cuando se utiliza con un punto de migración de estado  

-   Conexión a la carpeta de red  

Desde un símbolo del sistema de administrador en F8, se puede seguir haciendo PING al equipo, por ejemplo, pero el tráfico de red de SMB (como NET USE desde un símbolo del sistema) podría producir el error 1231: No es posible el acceso a la ubicación de red.  

**Solución alternativa**:  
Agregue un paso de secuencia de tareas Ejecutar línea de comandos después del paso de secuencia de tareas Instalar Windows y Configuration Manager para detener y luego iniciar el servicio Estación de trabajo de la manera siguiente:    
**net stop workstation /y & net start workstation**  

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>Los planes de mantenimiento crean de forma predeterminada muchos grupos de actualizaciones e muchas implementaciones de software duplicadas  
De forma predeterminada, el asistente para Crear un plan de mantenimiento se ejecuta actualmente después de cada sincronización de actualizaciones de software. Cada vez que se ejecuta el asistente, se crea un nuevo grupo de actualizaciones e implementaciones de software. Si tiene una programación de sincronización de actualizaciones de software que se ejecuta varias veces al día, por ejemplo, el asistente para Crear un plan de mantenimiento creará varios grupos de actualizaciones y varias implementaciones de software, probablemente idénticos, cada día.  

**Solución alternativa**:    
Después de crear un plan de mantenimiento, abra las propiedades, vaya a la pestaña **Programación de evaluación**, seleccione **Ejecutar la regla en una programación**, haga clic en **Personalizar** y cree una programación personalizada. Por ejemplo, puede hacer que el plan de mantenimiento se ejecute cada 60 días.  

## <a name="mobile-device-management"></a>Administración de dispositivos móviles  

### <a name="cannot-create-an-enrollment-profile-on-a-primary-site"></a>No se puede crear un perfil de inscripción de un sitio primario  
Un administrador no puede crear un perfil de inscripción en la consola de administración de System Center Configuration Manager que se conecta a un sitio primario. Al intentar efectuar una inscripción, el administrador verá el error “DEP token has not been updated. Upload a DEP token” en el Asistente para crear perfil de inscripción. Este error se produce aunque se haya cargado un token de DEP válido en el sitio de administración central.  

**Solución alternativa**: crea un perfil de inscripción en la consola de System Center Configuration Manager que se conecta al sitio de administración central.  

### <a name="dep-cannot-use-non-alpha-numeric-characters-in-enrollment-profiles"></a>DEP no puede usar caracteres que no son alfanuméricos en perfiles de inscripción  
Los perfiles de inscripción asociados al perfil de inscripción de dispositivo (DEP) de Apple no pueden usar caracteres no son alfanuméricos en los campos **Nombre**, **Descripción**, **Departamento** y **Número de teléfono** para el perfil de inscripción si DEP está habilitado. El uso de caracteres que no son alfanuméricos en estos campos crea un perfil de inscripción, pero este perfil no puede cargarse en Apple. El servidor de Apple no proporciona ningún mensaje de error o advertencia y los perfiles no se implementarán en dispositivos administrados por DEP.  

**Solución alternativa**: ninguna.

### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>El borrado completo deshabilita los dispositivos de Windows 10 con menos de 4 GB de RAM

Realizar un borrado completo en dispositivos de Windows 10 RTM (versiones anteriores a la 1511) con menos de 4 GB de RAM puede inutilizar el dispositivo. Después de intentar borrar el dispositivo, este no se puede iniciar y no responde.

**Solución alternativa**: asegúrese de que los equipos con Windows 10 RTM tienen al menos 4 GB de RAM disponibles antes de realizar un borrado completo en el dispositivo. Para ver el número de versión de los dispositivos de Windows 10, escriba 'winver' en un símbolo del sistema. Si el dispositivo ya se ha borrado y ya no responde, use una unidad USB de Windows 10 de arranque para iniciar y recuperar el acceso al dispositivo.

### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>Cuando un usuario pertenece a dos o más recopilaciones de usuarios en las que se implementa una directiva de términos y condiciones, el usuario ve varios conjuntos de los mismos términos  

Si un administrador implementa un conjunto de términos en varias recopilaciones de usuarios, y un usuario es miembro de más de una de estas recopilaciones, ese usuario verá varias copias de los mismos términos al abrir el portal de empresa.  Por ejemplo, si un usuario llamado "SampleUser" es miembro de dos recopilaciones de usuarios diferentes, denominadas "CompanyEmployeesFTE" y "CompanyEmployeesNA", y los términos y condiciones denominados "CompanyTerms" se implementan en CompanyEmployeesFTE y CompanyEmployeesNA, SampleUser verá dos conjuntos idénticos de CompanyTerms en la página de aceptación de términos. Puesto que los usuarios solo pueden aceptar o rechazar todos los términos, no existe riesgo de estar en un estado de aceptación ambigua (donde el usuario ha aceptado y rechazado los términos al mismo tiempo). El informe de aceptación de términos y condiciones solo incluirá una fila para cada conjunto de términos de cada usuario, de modo que no hay ningún error en el informe. La única consecuencia es que el usuario verá dos conjuntos de términos en la página de aceptación.  

**Solución alternativa**: asegúrese de que cada usuario solo se incluya en una colección para la que se implementan los términos.  

## <a name="reports-and-monitoring"></a>Informes y supervisión  

### <a name="the-health-attestation-report-is-empty-even-though-health-attestation-data-was-previously-collected"></a>El informe de atestación de estado está vacío aunque anteriormente se han recopilado datos de atestación de estado  
Cuando un usuario administrativo con un rol de seguridad que incluye el permiso de **Lectura** para el grupo de permisos de **Atestación de estado** ve el informe de atestación de estado, este está vacío y no se muestran datos. El motivo es que los permisos para ver los datos en este informe están vinculados al grupo de permisos de **Afinidad entre usuario y dispositivo** en lugar de al grupo de permisos de Atestación de estado.  

Este problema afecta a System Center Configuration Manager con la actualización 1602, y previsiblemente se resolverá en una futura actualización.  

**Solución alternativa**: asigne al usuario administrativo a un grupo de seguridad que incluya el permiso de **Lectura** para el grupo de permisos de **Afinidad entre usuario y dispositivo**.  

### <a name="conditional-access"></a>Acceso condicional  

#### <a name="the-same-user-collection-is-not-blocked-from-being-added-to-both-exempted-and-targeted-collections"></a>No se impide que la misma recopilación de usuario se agregue a las recopilaciones exentas y objetivo.  
Esto solo se produce cuando agrega la misma **recopilación de usuarios** a la página **Recopilaciones exentas** **antes** de agregarla a la página **Colecciones objetivo**.  Si primero agrega una **recopilación de usuarios** a la página **Colecciones objetivo** y luego intenta agregar la misma **recopilación de usuarios** a la página **Recopilaciones exentas**, debería ver el mensaje de bloqueo normal.  

Este problema afecta al acceso condicional de System Center Configuration Manager para **Exchange local** con la actualización 1602 y se espera que se resuelva en una futura actualización.  

**Solución alternativa**: agregue la **recopilación de usuarios** a la página **Colecciones objetivo** antes de seleccionar la **recopilación de usuarios** en la página **Recopilaciones exentas**, o asegúrese de que no agrega la misma **recopilación de usuarios** tanto a las recopilaciones objetivo como exentas.



<!--HONumber=Dec16_HO3-->

