---
title: Panel de dispositivos Surface
titleSuffix: System Center Configuration Manager
description: Revise la información sobre los dispositivos Surface mediante el panel.
keywords: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology:
- configmgr-other
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: 8c9171ed5b239091b7f77b534368422575c0f2f4
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="surface-device-dashboard-in-system-center-configuration-manager"></a>Panel de dispositivos Surface en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

A partir de la versión 1802, en el panel de dispositivos Surface se proporciona información sobre los dispositivos Surface que se encuentran en el entorno de un solo vistazo. <!--1355788-->

## <a name="open-the-surface-device-dashboard"></a>Abrir el panel de dispositivos Surface

Para abrir el panel de dispositivos Surface, siga estos pasos: 

1. Abra la consola de Configuration Manager. 
2. Haga clic en el nodo **Supervisión**. 
3. Para cargar el panel, haga clic en **Dispositivos Surface**.

**Panel de dispositivos Surface**
![Surface device dashboard](media\Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>Revisión de la información en el panel de dispositivos Surface

En el panel de dispositivos Surface se muestran tres gráficos para el entorno. 

- **Percent of Surface devices** (Porcentaje de dispositivos Surface): proporciona el porcentaje de los dispositivos Surface en todo el entorno.

    ![Gráfico Porcentaje de dispositivos Surface](media\Percent-Surface-Devices.PNG)
- **Modelos de Surface**: muestra el número de dispositivos por modelo de Surface. 
    - Al mantener el puntero sobre una sección del gráfico se proporciona el porcentaje de los dispositivos Surface en el modelo seleccionado. 

         ![Gráfico Modelos de Surface](media\Surface-Models-Hover.PNG)
    - Al hacer clic en una sección del gráfico se tiene acceso a una lista de dispositivos para el modelo. 
        ![Lista de dispositivos del modelo de Surface](media\Surface-Model-Device-List.PNG)

- **Cinco versiones principales de firmware**: muestra un gráfico con los cinco modelos de firmware principales en el entorno. 
    - Al mantener el puntero sobre una sección del gráfico se proporciona el porcentaje de los dispositivos Surface en la versión de firmware seleccionada. 
       ![Lista de dispositivos del modelo de Surface](media\Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>Más información

Para obtener más información sobre los dispositivos Surface, vea:
 - El sitio web de [Surface]( https://go.microsoft.com/fwlink/?linkid=861998).
    
Para más información sobre cómo implementar actualizaciones de firmware de Surface en Configuration Manager, vea:
 - [How to manage Surface driver updates in Configuration Manager]( https://support.microsoft.com/help/4098906) (Cómo administrar actualizaciones de controladores de Surface en Configuration Manager).



