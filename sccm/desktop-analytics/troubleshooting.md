---
title: Solución de problemas de análisis de escritorio
titleSuffix: Configuration Manager
description: Detalles técnicos para ayudarle a solucionar problemas relacionados con el análisis de escritorio.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6bebf4065a4db1c45ee7eaa0a5b04b8d1533f29f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755548"
---
# <a name="troubleshooting-desktop-analytics"></a>Solución de problemas de análisis de escritorio

Use los detalles de este artículo para ayudarle a solucionar problemas con Analytics escritorio integrado con Configuration Manager.



## <a name="confirm-prerequisites"></a>Confirme los requisitos previos

Muchos problemas comunes están provocados por los requisitos previos que faltan. En primer lugar, confirme las siguientes configuraciones:

- [Requisitos previos](/sccm/desktop-analytics/overview#prerequisites)  

- [Actualizaciones de componentes de Windows](/sccm/desktop-analytics/enroll-devices#update-devices)  

- [Cómo habilitar el uso compartido de datos](/sccm/desktop-analytics/enable-data-sharing), que tratan los temas siguientes:  

    - Puntos de conexión de Internet a la que los clientes necesitan para conectarse  

    - Autenticación del servidor proxy  

    - Niveles de datos de diagnóstico  



## <a name="monitor-connection-health"></a>Supervisión de estado de conexión

Use la **mantenimiento de la conexión** panel en Configuration Manager para profundizar en categorías por estado de dispositivos. En la consola de Configuration Manager, vaya a la **biblioteca de Software** área de trabajo, expanda el **mantenimiento de Microsoft 365** nodo y seleccione el **mantenimiento de la conexión** panel.  

![Captura de pantalla del panel de mantenimiento de conexión de Configuration Manager](media/connection-health-dashboard.png)

Si piensa que algunos dispositivos no están visibles en el escritorio de análisis, compruebe primero el porcentaje de **dispositivos conectados**. Si es inferior al 100%, asegúrese de que los dispositivos son compatibles con análisis de escritorio. Para obtener más información, consulte [Requisitos previos](/sccm/desktop-analytics/overview#prerequisites).


### <a name="connection-health-states"></a>Estados de mantenimiento de conexión

A continuación, revisar el **mantenimiento de la conexión** gráfico. Muestra el número de dispositivos en las siguientes categorías de mantenimiento:  

- [Correctamente inscrito](#properly-enrolled)  
- [Problemas de configuración](#configuration-issues)  
- [Cliente no instalado](#client-not-installed)  
- [Esperando para la inscripción](#waiting-for-enrollment)  
- [Requisitos previos que faltan](#missing-prerequisites)  
- [Datos que faltan](#missing-data)  

Seleccione el nombre de categoría para quitar o agregarlo en el gráfico. Esta acción ayuda a acercar el gráfico para que pueda ver los tamaños relativos de segmentos más pequeños. 

#### <a name="properly-enrolled"></a>Correctamente inscrito
El dispositivo tiene los siguientes atributos:  
- Una versión 1810 o posterior del cliente de Configuration Manager  
- No hay ningún error de configuración  
- Escritorio Analytics recibe datos de diagnóstico completados de este dispositivo en los últimos 28 días  
- Escritorio Analytics tiene un inventario completo de la configuración del dispositivo y las aplicaciones instaladas  

#### <a name="configuration-issues"></a>Problemas de configuración
Configuration Manager detecta uno o varios problemas con la configuración necesaria para el análisis de escritorio. Para obtener más información, consulte la lista de [propiedades de dispositivo de escritorio Analytics en Configuration Manager](#bkmk_config-issues).  

#### <a name="client-not-installed"></a>Cliente no instalado
El dispositivo está destinado a análisis de escritorio, pero no es un cliente de Configuration Manager. 

Se requiere el cliente de Configuration Manager para configurar y administrar el dispositivo para el análisis de escritorio. Para obtener más información, vea [Métodos de instalación de cliente en System Center Configuration Manager](/sccm/core/clients/deploy/plan/client-installation-methods).  

#### <a name="waiting-for-enrollment"></a>Esperando para la inscripción
Análisis de escritorio no tienen datos de diagnóstico para este dispositivo. Este problema puede ser porque el dispositivo se agregó recientemente a la colección de destino y aún no envió los datos. También puede significar el dispositivo no se están comunicando correctamente con el servicio y los datos de diagnóstico más recientes tiene más de 28 días de antigüedad. 

Asegúrese de que el dispositivo es capaz de comunicarse con el servicio. Para obtener más información, consulte [extremos](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

#### <a name="missing-prerequisites"></a>Requisitos previos que faltan
El cliente de Configuration Manager no es de al menos la versión 1810 (5.0.8740). 

Actualice al cliente a la versión más reciente. Considere la posibilidad de habilitar la actualización automática del cliente para el sitio de Configuration Manager. Para obtener más información, vea [Actualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  

#### <a name="missing-data"></a>Datos que faltan
Análisis de escritorio no pueden crear una evaluación de compatibilidad. No tiene un conjunto de datos completo para la configuración del dispositivo (del censo) o instalar aplicaciones (inventario). 

A menudo, este problema se corrige automáticamente cuando el dispositivo intenta enviar. Si persiste, asegúrese de que el dispositivo es capaz de comunicarse con el servicio. Para obtener más información, consulte [extremos](/sccm/desktop-analytics/enable-data-sharing#endpoints).  


### <a name="device-list"></a>Lista de dispositivos

Para ver una lista específica de dispositivos por estado, comience con la **mantenimiento de la conexión** panel. Seleccione uno de los segmentos de la **mantenimiento de la conexión** icono y explorar en profundidad una lista de dispositivos de esta categoría. Esta vista personalizada del dispositivo muestra las siguientes columnas de análisis de escritorio de forma predeterminada:
- Configuración de Id. comercial
- Actualización de compatibilidad mínimo
- Opción datos de diagnóstico de Windows
- Participación datos comerciales en Windows
- Conectividad de punto de conexión de diagnóstico de Windows
- Conectividad de punto de conexión de diagnóstico de Office

Estas columnas corresponden a la clave [requisitos previos](/sccm/desktop-analytics/overview#prerequisites) los dispositivos para comunicarse con el análisis de escritorio. 

![Lista de dispositivos de captura de pantalla de correctamente inscrito](media/sccm-device-list-properly-enrolled.png)

Seleccione un dispositivo para ver la lista completa de las propiedades disponibles en el panel de detalles. También puede agregar cualquiera de estas propiedades como columnas a la lista de dispositivos. 


### <a name="bkmk_config-issues"></a> Propiedades de dispositivo de escritorio Analytics en Configuration Manager

Las columnas siguientes están disponibles en la lista de dispositivos:
- [Configuración de Appraiser](#appraiser-configuration)  
- [Actualización de compatibilidad mínimo](#minimum-compatibility-update)  
- [Versión Appraiser](#appraiser-version)  
- [Última ejecución completa correcta de Appraiser](#last-successful-full-run-of-appraiser)  
- [Recopilación de datos Appraiser](#appraiser-data-collection)  
- [Última ejecución completa correcta del censo](#last-successful-full-run-of-census)  
- [Recopilación de datos del censo](#census-data-collection)  
- [Conectividad de punto de conexión de diagnóstico de Windows](#windows-diagnostic-endpoint-connectivity)  
- [Comprobar los datos de diagnóstico para el usuario final](#check-end-user-diagnostic-data)  
- [Comprobar el proxy de usuario](#check-user-proxy)  
- [Configuración de Id. comercial](#commercial-id-configuration)  
- [Participación datos comerciales en Windows](#windows-commercial-data-opt-in)  
- [Compruebe el nombre del dispositivo en los datos de diagnóstico](#check-device-name-in-diagnostic-data)  
- [Configuración del servicio DiagTrack](#diagtrack-service-configuration)  
- [Versión DiagTrack](#diagtrack-version)  
- [Recuperación de Id. de SQM](#sqm-id-retrieval)  
- [Recuperación del identificador de dispositivo único](#unique-device-identifier-retrieval)  
- [Opción datos de diagnóstico de Windows](#windows-diagnostic-data-opt-in)  
- [Conectividad de punto de conexión de diagnóstico de Office](#office-diagnostic-endpoint-connectivity)  

#### <a name="appraiser-configuration"></a>Configuración de Appraiser
<!--20,21--> Appraiser es el componente de Windows que se corresponde con el [actualizaciones de compatibilidad](/sccm/desktop-analytics/enroll-devices#update-devices). Evalúa las aplicaciones y los controladores del dispositivo para la compatibilidad con la versión más reciente de Windows. 

Si esta comprobación se realiza correctamente, el componente appraiser está configurado correctamente en el dispositivo. 

En caso contrario, es posible que aparezca uno de los errores siguientes:

- No se puede configurar la recopilación de datos de compatibilidad de aplicación de dispositivo (SetRequestAllAppraiserVersions). Compruebe los registros para obtener los detalles de excepción  

- No se puede configurar la recopilación de datos de compatibilidad de aplicación de dispositivo (SetRequestAllAppraiserVersions). Compruebe los registros para obtener los detalles de excepción  

- No se puede escribir la clave RequestAllAppraiserVersions a la clave del registro `HKLM:\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Appraiser`. Compruebe los permisos  

Compruebe los permisos de esta clave del registro. Asegúrese de que la cuenta sistema local puede tener acceso a esta clave para el cliente de Configuration Manager establecer.  

Para obtener más información, revise M365AHandler.log en el cliente.  


#### <a name="minimum-compatibility-update"></a>Actualización de compatibilidad mínimo
<!--18,19,32--> La actualización de compatibilidad (appraiser.dll) no está instalado o no está actualizada en el dispositivo. Es más antigua que el requisito mínimo para el análisis de escritorio, 10.0.17763. 

Instale la actualización de compatibilidad más reciente. Para obtener más información, consulte [actualizaciones de compatibilidad](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser).


#### <a name="appraiser-version"></a>Versión Appraiser
Esta propiedad muestra la versión actual del componente Appraiser en el dispositivo. Muestra la versión del archivo en `%windir%\System32\appraiser.dll`, sin las decimales. Por ejemplo, la versión del archivo 10.0.17763 muestra como 10017763. 


#### <a name="last-successful-full-run-of-appraiser"></a>Última ejecución completa correcta de Appraiser
Esta propiedad muestra la fecha y hora en que el dispositivo correctamente ejecutó por última Appraiser.


#### <a name="appraiser-data-collection"></a>Recopilación de datos Appraiser
<!--Appraiser run status-->
<!--22,33--> Esta propiedad muestra el resultado más reciente de Windows que ejecuta el componente appraiser. 

Si no se realiza correctamente, puede que aparezca uno de los errores siguientes: 

- No se pueden recopilar datos de compatibilidad de aplicaciones (RunAppraiser). Compruebe los registros para obtener más información  

- Colección de datos de compatibilidad de aplicaciones (CompatTelRunner.exe) finalizó con un código de error  

Para obtener más información, revise M365AHandler.log en el cliente. 

Busque el siguiente archivo: `%windir%\System32\CompatTelRunner.exe`. Si no existe, vuelva a instalar los [actualizaciones de compatibilidad](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser). Asegúrese de que ningún otro componente del sistema es eliminar este archivo, como la directiva de grupo o un servicio antimalware. 

Si el archivo M365Handler.log en el cliente incluye uno de los errores siguientes: `RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1`
`RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005`
`RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005`  

Para ayudar a corregir estos errores, ejecute los siguientes comandos desde una consola de Windows PowerShell con privilegios elevados en el cliente afectado:

```PowerShell
# stop associated services
Stop-Service -Name diagtrack #Connected User Experiences and Telemetry
Stop-Service -Name pcasvc #Program Compatibility Assistant Service
Stop-Service -Name dps #Diagnostic Policy Service

# regenerate diagnostic data cache
Remove-Item -Path $Env:WinDir\appcompat\programs\amcache.hve
Remove-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name AmiHivePermissionsCorrect -Force

# set ASL logging level to output log files in %windir%\temp
New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name LogFlags -Value 4 -PropertyType DWord -Force 

# restart services
Start-Service -Name diagtrack
Start-Service -Name pcasvc
Start-Service -Name dps
```

#### <a name="last-successful-full-run-of-census"></a>Última ejecución completa correcta del censo
Esta propiedad muestra la fecha y hora en que el dispositivo por última vez ejecutó correctamente del censo. 

#### <a name="census-data-collection"></a>Recopilación de datos del censo
<!-- Census run status -->
<!--51,52--> Census es el componente de Windows que incluya el dispositivo. Estos datos de inventario se usan para comprender el dispositivo y su configuración. 

Esta propiedad muestra el resultado más reciente de Windows que ejecuta el componente del censo.

Si no se realiza correctamente, puede que aparezca uno de los errores siguientes: 

- No se pueden recopilar datos sobre el dispositivo y su configuración (RunCensus). Compruebe los registros para obtener los detalles de excepción  

- Dispositivos y configuración de herramienta recopilación de datos (devicecensus.exe) no encontrado  

Para obtener más información, revise M365AHandler.log en el cliente. 

Busque el siguiente archivo: `%windir%\System32\DeviceCensus.exe`. Si no existe, vuelva a instalar los [actualizaciones de compatibilidad](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser). Asegúrese de que ningún otro componente del sistema es eliminar este archivo, como la directiva de grupo o un servicio antimalware. 


#### <a name="windows-diagnostic-endpoint-connectivity"></a>Conectividad de punto de conexión de diagnóstico de Windows
<!--12,15--> Si esta comprobación se realiza correctamente, el dispositivo es capaz de conectarse al usuario conectado experiencia y telemetría de punto de conexión (Vortex). 

En caso contrario, puede mostrar uno de los errores siguientes:  

- No se puede conectar al usuario conectado experiencia y telemetría de punto de conexión (Vortex). Compruebe la configuración de red o proxy  

- No se puede comprobar la conectividad con el usuario conectado experiencia y telemetría de punto de conexión (CheckVortexConnectivity). Compruebe los registros para obtener los detalles de excepción  

Dispositivos comprueban la conectividad con una solicitud GET al punto de conexión siguiente en función de la versión del sistema operativo:

| Versión de SO | punto de conexión |
|------------|----------|
| Windows 10, versión 1803 o posterior con la actualización acumulativa más reciente | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Actualización de la versión 1803 o posterior sin el 09 de 2018 o posterior acumulativa de Windows 10 | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10, versión 1709 o versiones anterior | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 o Windows 8.1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

Asegúrese de que el dispositivo es capaz de comunicarse con el servicio. Esta comprobación valida algunos pero no todos los puntos de conexión necesarios. Para obtener más información, consulte [extremos](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

Para obtener más información, revise M365AHandler.log en el cliente.  


#### <a name="check-end-user-diagnostic-data"></a>Comprobar los datos de diagnóstico para el usuario final
<!--1004-->

Si esta comprobación no se realiza correctamente, un usuario seleccionó una menor datos de diagnóstico de Windows en el dispositivo.

Dependiendo de sus requisitos empresariales, puede deshabilitar la elección del usuario a través de la directiva de grupo. Use la configuración para **interfaz de usuario de participación en la configuración de telemetría configurar**. Para obtener más información, consulte [Configurar los datos de diagnóstico de Windows en la organización](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).


#### <a name="check-user-proxy"></a>Comprobar el proxy de usuario
<!--30,35-->

La configuración de DisableEnterpriseAuthProxy está habilitada de forma predeterminada para Windows 7. Para equipos Windows 8.1, Configuration Manager establece el valor de DisableEnterpriseAuthProxy en 0 (no está deshabilitado).

Esta propiedad puede mostrar los errores siguientes:

- Autenticación proxy está habilitado. Establezca DisableEnterpriseAuthProxy en 0 en `HKLM\Software\Policies\Microsoft\Windows\DataCollection` 

- No puede comprobar el estado de autenticación proxy. Compruebe los registros para obtener los detalles de excepción

Para obtener más información, revise M365AHandler.log en el cliente.  

Compruebe los permisos de esta clave del registro. Asegúrese de que la cuenta sistema local puede tener acceso a esta clave para el cliente de Configuration Manager establecer.  


#### <a name="commercial-id-configuration"></a>Configuración de Id. comercial
<!--9, 11, 53--> Microsoft usa un único identificador comercial para asignar la información de dispositivos al área de trabajo de análisis de escritorio. Al integrar Configuration Manager con análisis de escritorio, consulta automáticamente el servicio para este identificador. Administrador de configuración debe aplicar automáticamente este identificador a los clientes que sean destinatarios configuración de análisis de escritorio. 

Si esta comprobación es correcta, a continuación, el dispositivo está configurado correctamente con un Id. comercial.

En caso contrario, puede mostrar uno de los errores siguientes:

- No se puede escribir el CommercialId a la clave del registro `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`. Compruebe los permisos  

- No se puede actualizar el CommercialId en la clave del registro `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`. Compruebe los registros para obtener los detalles de excepción   

- Proporcione el valor correcto de CommercialId en `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`  

Para obtener más información, revise M365AHandler.log en el cliente.  

Compruebe los permisos de esta clave del registro. Asegúrese de que la cuenta sistema local puede tener acceso a esta clave para el cliente de Configuration Manager establecer.  

Hay un identificador distinto para el dispositivo. Esta clave del registro está usando la directiva de grupo. Tiene prioridad sobre el identificador proporcionado por el Administrador de configuración.  


Para ver el identificador comercial en el portal de análisis de escritorio, use el procedimiento siguiente: 

1. Vaya al portal de Analytics de escritorio y seleccione **servicios conectados** en el grupo de configuración Global.  

2. En el **servicios conectados** panel, el **inscribir dispositivos** panel está activado de forma predeterminada. En el panel de dispositivos de inscripción, la sección de información muestra la clave de Id. comercial.  

![Captura de pantalla de identificador comercial en el portal de análisis de escritorio](media/commercial-id.png)

> [!Important]  
> Solo **clave de Id. nuevo Get** cuando no se puede usar actual. Si regenera el identificador comercial, implementar el nuevo identificador en los dispositivos. Este proceso podría provocar la pérdida de datos de diagnóstico durante la transición.  


#### <a name="windows-commercial-data-opt-in"></a>Participación datos comerciales en Windows
<!--64-->

Esta propiedad es específica de los dispositivos que ejecutan Windows 7 o Windows 8.1. Ejecute pruebas similares como [opción datos de diagnóstico de Windows](#windows-diagnostic-data-opt-in), excepto para el CommercialDataOptIn de valor.


#### <a name="check-device-name-in-diagnostic-data"></a>Compruebe el nombre del dispositivo en los datos de diagnóstico
<!--56,58-->

Si esta comprobación se realiza correctamente, el dispositivo está configurado correctamente para compartir el nombre del dispositivo.

En caso contrario, puede mostrar uno de los errores siguientes:

- No puede comprobar el nombre del dispositivo para enviarse a Microsoft como parte de los datos de diagnóstico de Windows. Compruebe los registros para obtener los detalles de excepción  

- No se puede escribir AllowDeviceNameInTelemetry a la clave del registro `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`. Compruebe los permisos  

Para obtener más información, revise M365AHandler.log en el cliente.  

Compruebe los permisos de esta clave del registro. Asegúrese de que la cuenta sistema local puede tener acceso a esta clave para el cliente de Configuration Manager establecer.  

Asegúrese de que otro mecanismo de directiva, como la directiva de grupo, no es si deshabilita a esta configuración. 


#### <a name="diagtrack-service-configuration"></a>Configuración del servicio DiagTrack
<!--44,45,50--> Si esta comprobación se realiza correctamente, el componente DiagTrack está configurado correctamente en el dispositivo. La versión mínima requerida por el análisis de escritorio es 10010586 (10.0.10586). 

En caso contrario, es posible que aparezca uno de los errores siguientes:

- Conecta la experiencia del usuario y el componente de telemetría (diagtrack.dll) está obsoleto. Comprobar los requisitos  

- No se encuentra el componente de telemetría (diagtrack.dll) y la experiencia del usuario. Comprobar los requisitos  

- Habilitar e iniciar el servicio de telemetría y experiencias del usuario conectado para enviar datos a Microsoft  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

Instale las actualizaciones más recientes. Para obtener más información, consulte [actualizaciones del dispositivo](/sccm/desktop-analytics/enroll-devices#update-devices).

Asegúrese de que el **telemetría y experiencias del usuario conectado** se está ejecutando el servicio en el dispositivo.

#### <a name="diagtrack-version"></a>Versión DiagTrack
Esta propiedad muestra la versión actual del componente experiencia del usuario y telemetría en el dispositivo. Muestra la versión del archivo en `%windir%\System32\diagtrack.dll`, sin las decimales. Por ejemplo, la versión del archivo 10.0.10586 muestra como 10010586. 

#### <a name="sqm-id-retrieval"></a>Recuperación de Id. de SQM
<!--38-->

Esta propiedad es principalmente para los dispositivos de Windows 7. Se puede usar con versiones posteriores de sistema operativo como un identificador de reserva para el dispositivo. 

Si no se realiza correctamente, puede mostrar el siguiente error:

- No se puede recuperar el identificador de dispositivo antiguo de la telemetría (SQM Id.)

Para obtener más información, revise M365AHandler.log en el cliente.  

Asegúrese de que no tiene identificadores duplicados en su entorno. Por ejemplo, si se han implementado los dispositivos con una imagen de sistema operativo que no se ha generalizado. 


#### <a name="unique-device-identifier-retrieval"></a>Recuperación del identificador de dispositivo único
<!--54--> Análisis de escritorio usa el servicio de Microsoft Account para una identidad de dispositivo más confiable. 

Asegúrese de que el **cuenta de inicio de sesión de Ayudante de Microsoft** el servicio no está deshabilitado. El tipo de inicio debe ser **Manual (desencadenador de inicio)**.

Para deshabilitar el acceso de cuenta de Microsoft del usuario final, use la configuración de directiva en lugar de bloquear este punto de conexión. Para obtener más información, consulte [cuenta Microsoft en la empresa](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication).


#### <a name="windows-diagnostic-data-opt-in"></a>Opción datos de diagnóstico de Windows
<!--8,40,55,62--> Esta propiedad comprueba que Windows está configurado correctamente para permitir que los datos de diagnóstico. Comprueba el valor de AllowTelemetry en las siguientes claves del registro:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

Compruebe los permisos de estas claves del registro. Asegúrese de que la cuenta sistema local puede tener acceso a estas claves para el cliente de Configuration Manager establecer.  

Para obtener más información, revise M365AHandler.log en el cliente.  


#### <a name="office-diagnostic-endpoint-connectivity"></a>Conectividad de punto de conexión de diagnóstico de Office
<!-- 1001,1002,1003 -->

Si esta comprobación se realiza correctamente, el dispositivo es capaz de conectarse a los puntos de conexión de diagnóstico de Office. 

En caso contrario, puede mostrar uno de los errores siguientes:

- No se puede conectar al punto de conexión diagnóstico de Office (Aria). Compruebe la configuración de red o proxy  

- No se puede conectar al punto de conexión diagnóstico de Office (Nexusrules). Compruebe la configuración de red o proxy  

- No se puede conectar al punto de conexión diagnóstico de Office (Nexus). Compruebe la configuración de red o proxy  

Asegúrese de que el dispositivo es capaz de comunicarse con el servicio. Para obtener más información, consulte [extremos](/sccm/desktop-analytics/enable-data-sharing#endpoints).  



## <a name="log-files"></a>Archivos de registro

Use los siguientes archivos de registro para ayudar a solucionar problemas con Analytics escritorio integrado con Configuration Manager. 


### <a name="service-connection-point"></a>Punto de conexión de servicio

Los siguientes archivos de registro están en el punto de conexión de servicio en el siguiente directorio: `C:\Program Files\Configuration Manager\Logs\M365A`:

| Registro | Descripción |
|---------|---------|
| **M365ADeploymentPlanWorker.log** | Información acerca de la sincronización del plan de implementación de análisis de escritorio en la nube de servicio en el Administrador de configuración local |
| **M365ADeviceHealthWorker.log** | Información sobre el estado del dispositivo se cargue desde el Administrador de configuración para la nube de Microsoft |
| **M365AUploadWorker.log** | Información sobre la recopilación y el dispositivo se cargue desde el Administrador de configuración para la nube de Microsoft |


### <a name="configuration-manager-client"></a>Cliente de Configuration Manager

Los siguientes archivos de registro se encuentran en el cliente de Configuration Manager en el siguiente directorio: `C:\Windows\CCM\logs`:

| Registro | Descripción |
|---------|---------|
| **M365Handler.log** | Información sobre la configuración de directiva de análisis de escritorio |


### <a name="enable-verbose-logging"></a>Habilitar el registro detallado 

1. En el punto de conexión de servicio, vaya a la siguiente clave del registro: `HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Establecer el **LogLevel** valor `0`  
3. Ejecute el siguiente comando SQL en la base de datos de sitio:  

    ```SQL
    DELETE FROM M365AProperties WHERE Name = 'M365ATenantUpdateInfo_LastUpdateTime'
    ```

4. Reinicie el **SMS_EXECUTIVE** servicio del servidor de sitio



## <a name="bkmk_MALogAnalyticsReader"></a> Rol de aplicación MALogAnalyticsReader

Al configurar el análisis de escritorio, acepte un consentimiento en nombre de su organización. Este consentimiento consiste en asignar el rol de lector de Log Analytics para el área de trabajo de la aplicación de MALogAnalyticsReader. Este rol de aplicación es necesario por el análisis de escritorio. 

Si hay un problema con este proceso durante el conjunto de copia, utilice el siguiente proceso para agregar manualmente este permiso:

1. Vaya a la [portal Azure](http://portal.azure.com)y seleccione **todos los recursos**. Seleccione el área de trabajo de tipo **Log Analytics**.  

2. En el menú del área de trabajo, seleccione **control de acceso (IAM)**, a continuación, seleccione **agregar**.  

3. En el **agregar permisos** del panel, configure las siguientes opciones:  

    - **Role**: **Lector de log Analytics**  

    - **Asignar acceso a**: **Usuario, grupo o aplicación de AD Azure**  

    - **Seleccione**: **MALogAnalyticsReader**  
  
4. Seleccione **Guardar**. 

El portal muestra una notificación que agrega la asignación de roles.

