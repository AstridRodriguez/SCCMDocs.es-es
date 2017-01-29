---
title: "Cómo inscriben dispositivos los usuarios mediante MDM local en Configuration Manager | Microsoft Docs"
description: "Conozca cómo inscriben dispositivos los usuarios mediante la administración de dispositivos móviles local en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
caps.latest.revision: 9
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 991eff171dce95590a7f050e0d3b07f98c0224b3
ms.openlocfilehash: 43a30709473939829d82d822503537d448159a1c


---
# <a name="how-users-enroll-devices-with-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Cómo inscriben dispositivos los usuarios mediante la administración de dispositivos móviles (MDM) local en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Con la administración local de dispositivos móviles en System Center Configuration Manager, los usuarios pueden inscribir dispositivos si se les ha concedido permiso de inscripción (por medio de la configuración actualizada de cliente) y si sus dispositivos tienen instalado el certificado raíz necesario para establecer comunicaciones de confianza con los servidores que hospedan los roles de sistema de sitio requeridos. Para obtener más información sobre cómo configurar la inscripción, consulte [Configure la inscripción del dispositivo para Administración de dispositivos móviles local en System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md).  

 > [!NOTE]  
>  La rama actual de Configuration Manager admite la inscripción en la administración de dispositivos móviles local para dispositivos con los sistemas operativos siguientes:  
>   
>  -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team \(a partir de la versión 1602 de Configuration Manager\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise

En las tareas siguientes se explica cómo inscribir equipos y dispositivos y comprobar su inscripción para la administración de dispositivos móviles local:  

-   [Inscribir un equipo Windows 10](#bkmk_enrollDesk)  

-   [Inscribir un dispositivo Windows 10 Mobile](#bkmk_enrollMob)  

-   [Comprobar inscripción de dispositivo](#bkmk_verify)  

##  <a name="a-namebkmkenrolldeska-enroll-a-windows-10-computer"></a><a name="bkmk_enrollDesk"></a> Inscribir un equipo Windows 10  

1.  En un equipo Windows 10, vaya a **Configuración**.  

2.  Haga clic en **Cuentas**y luego en **Acceso al trabajo**.  

3.  En Acceso al trabajo, en **Conectarse a la red del trabajo o colegio**, haga clic en **Conectar**, escriba su dirección de correo electrónico y haga clic en **Continuar**.  

4.  Escriba el FQDN del servidor que hospeda el rol de sistema de sitio de punto de proxy de inscripción y haga clic en **Continuar**.  

5.  En Conectando con un servicio, escriba la contraseña de correo electrónico del trabajo y haga clic en **Iniciar sesión**.  

6.  Haga clic en **Omitir** para recordar la información de inicio de sesión y después de unos instantes se conectará el dispositivo.  

##  <a name="a-namebkmkenrollmoba-enroll-a-windows-10-mobile-device"></a><a name="bkmk_enrollMob"></a> Inscribir un dispositivo Windows 10 Mobile  

1.  En un dispositivo Windows 10 Mobile, vaya a **Configuración**.  

2.  Haga clic en **Cuentas**y luego en **Acceso al trabajo**.  

3.  Haga clic en **Conectar**.  

4.  Escriba su dirección de correo electrónico laboral y el FQDN del servidor que hospeda el rol de sistema de sitio de punto de proxy de inscripción. Haga clic en **Conectar**.  

5.  En la siguiente pantalla, escriba su dirección de correo electrónico y contraseña laborales y luego, haga clic en **Iniciar de sesión**. Después de unos minutos, se inscribirá el dispositivo. Haga clic en **Listo**.  

##  <a name="a-namebkmkverifya-verify-device-enrollment"></a><a name="bkmk_verify"></a> Comprobar inscripción de dispositivo  
 Puede comprobar que los dispositivos están inscritos correctamente en la consola de Configuration Manager.  

1.  Inicie la consola de Configuration Manager.  

2.  Haga clic en **Activos y compatibilidad** > **Introducción** > **Dispositivos**. El dispositivo inscrito aparece en la lista.  

## <a name="see-also"></a>Véase también  
 [Enroll devices for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/deploy-use/enroll-devices-on-premises-mdm.md) (Inscribir dispositivos para la administración de dispositivos móviles local en System Center Configuration Manager)



<!--HONumber=Jan17_HO4-->

