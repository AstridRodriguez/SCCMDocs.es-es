---
title: Inscribir dispositivos iOS con Apple Configurator en Configuration Manager | Microsoft Docs
descriptions: Pre-enroll iOS devices by using Apple Configurator with Configuration Manager.
ms.custom: na
ms.date: 12/16/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
caps.latest.revision: 5
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 991eff171dce95590a7f050e0d3b07f98c0224b3
ms.openlocfilehash: 6c6e9edbc7b2fca3d1be4feabb238efab80465fa


---
# <a name="ios-hybrid-enrollment-using-apple-configurator-with-configuration-manager"></a>Inscripción híbrida de iOS híbrido con Apple Configurator con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Las compañías que compran dispositivos iOS destinados para su uso por los empleados pueden administrarlos mediante Microsoft Intune. Para preparar los dispositivos iOS corporativos para la inscripción, configure un perfil de inscripción en la consola de Configuration Manager y, después, exporte la dirección URL del perfil para que Apple Configurator la use. Prepare el dispositivo iOS para la inscripción conectándolo a un equipo Mac con un cable USB y use Apple Configurator para configurarlo. Apple Configurator restablece la configuración de fábrica del dispositivo y agrega el perfil de inscripción de manera que el dispositivo pueda inscribirse cuando el usuario lo encienda por primera vez y se desplace a través del proceso del Asistente de configuración.

El siguiente procedimiento está recomendado para dispositivos iOS dedicados que tendrán un único usuario que emplea el dispositivo para tener acceso al correo electrónico de la empresa y a recursos corporativos, como aplicaciones y datos.  

## <a name="prerequisites"></a>Requisitos previos  

-   Acceso físico a dispositivos iOS  

-   Números de serie del dispositivo: [cómo obtener un número de serie de iOS](https://support.apple.com/en-us/HT204308)  

-   Equipo Mac con [Apple Configurator 2.0](http://go.microsoft.com/fwlink/?LinkId=518017)  

-   Cables USB para conectar los dispositivos al equipo Mac  

## <a name="step-1-add-a-corporate-owned-device-enrollment-profile"></a>Paso 1: Agregar un perfil de inscripción de dispositivos corporativos

1.  En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Información general** > **Todos los dispositivos corporativos** > **iOS** > **Perfiles de inscripción**. Haga clic en **Crear perfil** para abrir el Asistente para crear el perfil. Establezca la configuración en las siguientes páginas:  

2.  En la página **General** , especifique la siguiente información:  

    -   **Nombre** (No es visible para los usuarios)  

    -   **Descripción** (No es visible para los usuarios)  

    -   **Afinidad de usuario** : especifica cómo se inscriben los dispositivos. En la mayoría de los escenarios del Asistente de configuración, use **Solicitar afinidad de usuarios**.  

        -   **Solicitar afinidad de usuario**: el dispositivo debe estar afiliado a un usuario durante la instalación inicial y, a continuación, se le puede permitir el acceso a los datos y al correo electrónico de la compañía como dicho usuario.  

        -   **Sin afinidad de usuario**: el dispositivo no está afiliado a ningún usuario. Utilice esta afiliación para dispositivos que realizan tareas sin tener acceso a datos de usuario local. Las aplicaciones que requieren la afiliación de un usuario no funcionarán.

    Haga clic en **Siguiente** para continuar.  

3.  En la página **Programa de inscripción de dispositivos**, deje la casilla **Configurar ajustes del programa de inscripción de dispositivos de este perfil** desactivada y haga clic en **Siguiente**.  

4.  Revise el resumen y, después, haga clic en **Siguiente** para crear el perfil de inscripción. Para finalizar el asistente, haga clic en **Cerrar**. Ahora está listo para agregar números IMEI o números de serie a los dispositivos que quiere inscribir.  

## <a name="step-2-predeclare-devices-to-enroll-with-setup-assistant"></a>Paso 2: Predeclarar los dispositivos para su inscripción con el Asistente de configuración

En este paso, predeclare los dispositivos como corporativos proporcionando una lista de identificadores de hardware (IMEI o números de serie).

Para obtener más información, consulte [Predeclare devices with IMEI and iOS serial number (Predeclarar dispositivos con IMEI y números de serie de iOS)](predeclare-devices-with-hardware-id.md). Cuando haya terminado con esa tarea, vuelva a la página para seguir con el siguiente paso.

## <a name="step-3-export-the-profile-to-deploy-to-ios-devices"></a>Paso 3: Exportar el perfil que se va a implementar en dispositivos iOS

1.  En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Información general** > **Todos los dispositivos corporativos** > **iOS** > **Perfiles de inscripción**.

2.  Seleccione el perfil de inscripción que se va a implementar en los dispositivos móviles y haga clic en **Exportar...**.

3.  Copie y guarde la **URL de perfil** en un archivo que pueda editar.   

4.  Para admitir Apple Configurator 2, se debe editar la URL de perfil 2.0. Reemplace la siguiente parte de la dirección URL:  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     por  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```

5.  Guarde la dirección URL de perfil editada. La usará para agregar la dirección URL de perfil de inscripción en Apple Configurator en la [siguiente sección](#step-4-prepare-the-device-with-apple-configurator).  

> [!NOTE]
> La dirección URL del perfil de inscripción es válida durante dos semanas desde que se exporta. Después de dos semanas, debe exportar una nueva dirección URL para inscribir dispositivos iOS.

## <a name="step-4-prepare-the-device-with-apple-configurator"></a>Paso 4: Preparación del dispositivo con Apple Configurator

Para preparar los dispositivos iOS para la inscripción, conecte cada dispositivo a un equipo Mac y cargue el perfil de inscripción en este.  

> [!WARNING]  
>  Apple Configurator borra y restablece los dispositivos a la configuración de fábrica.  

1.  En un equipo Mac, abra **Apple Configurator 2**.  

2.  En la barra de menús, haga clic en **Apple Configurator 2** > **Preferencias**.  

2.  En el panel de preferencias, seleccione **Servers** (Servidores) y haga clic en el símbolo "+" debajo del panel izquierdo para iniciar el asistente del servidor MDM. Haga clic en **Siguiente**.  

3.  Escriba el **Nombre** y la **URL de inscripción** que ha guardado [antes](#step-3-export-the-profile-to-deploy-to-ios-devices). Haga clic en **Siguiente**.  

   > [!NOTE]
   > Si recibe una advertencia sobre los requisitos de perfil de confianza para Apple TV, puede cancelar con seguridad la opción **Trust Profile (Perfil de confianza)** haciendo clic en la "X" de color gris. También de forma segura, puede omitir cualquier advertencia de marcador de certificado.

   Para continuar, haga clic en **Next** (Siguiente) hasta que finalice el asistente.  

4.  En el panel **Servers** (Servidores), haga clic en "Edit" (Editar) junto a perfil del nuevo servidor. Asegúrese de que la dirección URL de inscripción coincide exactamente con la dirección URL que ha especificado anteriormente. Vuelva a escribir la dirección URL si es diferente y haga clic en **Guardar**.  

5.  Con un cable USB, conecte un dispositivo iOS al equipo Mac.  

  > [!WARNING]  
  >  Este proceso restablece los dispositivos a la configuración de fábrica. Antes de conectar el dispositivo, restablezca el dispositivo y enciéndalo. Como procedimiento recomendado, en el dispositivo debe aparecer la pantalla Hello antes de continuar.  

6.  Haga clic en **Prepare** (Preparar). En el panel **Prepare iOS Device (Preparar dispositivo iOS)**, seleccione **Manual** y, después, haga clic en **Siguiente**.  

7.  En el panel **Enroll in MDM Server (Inscribir en servidor MDM)**, seleccione el nombre del servidor que ha creado y haga clic en **Siguiente**.  

9. En el panel **Create an Organization** (Crear una organización), elija la **organización** o cree una nueva y luego haga clic en **Next** (Siguiente).  

10. En el panel **Configure iOS Setup Assistant (Configurar Asistente de configuración de iOS)**, elija los pasos que se van a presentar al usuario y, después, haga clic en **Preparar**. Si se le solicita, autentíquese para actualizar la configuración de confianza.  

11. Cuando termine, puede desconectar el cable USB.  

Repita estos pasos en todos los dispositivos que quiera preparar para la inscripción.

## <a name="step-5-distribute-devices"></a>Paso 5: Distribución de los dispositivos

Los dispositivos ya están listos para la inscripción corporativa. Apague los dispositivos y distribúyalos a los usuarios. Cuando el dispositivo se encienda, se iniciará el Asistente de configuración y se solicitará al usuario su cuenta profesional o educativa para comenzar la inscripción.



<!--HONumber=Jan17_HO4-->

