---
title: "Создание последовательности задач для развертывания операционных систем | Документы Майкрософт"
description: "Создание последовательности задач, которые не связаны с развертыванием операционных систем, например распространение программного обеспечения, обновление драйверов, изменения пользовательских сред и т. д."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
caps.latest.revision: "6"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: b4b04907f2cd48d81e864e46ca47c14a0b98a9f7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="create-a-task-sequence-for-non-operating-system-deployments-with-system-center-configuration-manager"></a>Создание последовательности задач для развертываний, отличных от операционных систем, в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Последовательности задач в System Center Configuration Manager применяются для автоматизации различных задач в среде. Эти задачи разрабатываются и тестируются главным образом для развертывания операционных систем.  Configuration Manager содержит и многие другие возможности, которые следует применять в качестве основных технологий для таких сценариев, как [установка приложений](../../apps/understand/introduction-to-application-management.md), [установка обновлений программного обеспечения](../../sum/understand/software-updates-introduction.md), [настройка конфигурации](../../compliance/understand/ensure-device-compliance.md) или специализированная автоматизация. Существуют и другие технологии автоматизации Microsoft System Center, такие как [Orchestrator](https://technet.microsoft.com/library/hh237242.aspx) и [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx) , которые следует учитывать.  

Преимущества последовательностей задач заключаются в гибкости, которая позволяет использовать их для настройки параметров клиента, распространения программного обеспечения, обновления драйверов, изменения сведений о пользовательской среде и выполнения других задач независимо от развертывания операционной системы. Можно создать настраиваемую последовательность задач, чтобы добавить любое количество задач. В Configuration Manager поддерживается использование пользовательских последовательностей задач для развертывания программного обеспечения, отличного от операционных систем. Но если выполнение последовательности задач приводит к нежелательным или несогласованным результатам, рассмотрите способы упростить эту операцию. Для этого можно упростить шаги, разделить действия на несколько последовательностей задач или применить поэтапный подход к созданию и тестированию последовательности задач.

 Для пользовательской последовательности задач развертывания ПО, отличного от операционной системы, поддерживаются следующие шаги:  

-   [Проверить готовность](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

-   [Подключить к сетевой папке](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

-   [Скачать содержимое пакета](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

-   [Установить приложение](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

-   [Установить пакет](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

-   [Установить обновления программного обеспечения](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

-   [Перезагрузить компьютер](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer)  

-   [Выполнить из командной строки](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

-   [Запустить сценарий PowerShell](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

-   [Задать динамические переменные](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

-   [Задать переменную последовательности задач](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>Дальнейшие действия
[Развертывание последовательности задач](manage-task-sequences-to-automate-tasks.md#a-namebkmkdeploytsa-deploy-a-task-sequence)
