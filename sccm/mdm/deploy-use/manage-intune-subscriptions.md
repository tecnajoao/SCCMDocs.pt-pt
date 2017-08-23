---
title: "Управление подпиской Intune, связанной с System Center Configuration Manager | Документация Майкрософт"
description: "Управление подпиской Intune, связанной с System Center Configuration Manager."
ms.custom: na
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b494767-68c1-47b1-9a86-591bff0ad491
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 2cb4d724c8b78657458a30c0bb020f67c6b62795
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="manage-an-intune-subscription-associated-with-system-center-configuration-manager"></a>Управление подпиской Intune, связанной с System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Если вы добавили Microsoft Intune (пробную или платную подписку) в Configuration Manager и затем возникла необходимость переключиться на другую подписку Intune, необходимо удалить **подписку Microsoft Intune** и **точку подключения службы** из консоли Configuration Manager, прежде чем добавлять новую подписку.

> [!NOTE]
> В гибридном управлении мобильными устройствами можно одновременно настроить только одну подписку Intune.

## <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>Удаление подписки Intune из Configuration Manager

> [!IMPORTANT]
>  При удалении подписки удаляется все содержимое, включая пользовательские регистрации, политики и развертывания приложений, настроенные для устройств под управлением этой подписки Intune.

1.  В консоли Configuration Manager последовательно выберите **Администрирование** > **Обзор** > **Облачные службы** > **Подписки Microsoft Intune**.

2.  Щелкните **подписку Windows Intune** в списке правой кнопкой мыши и выберите пункт **Удалить**.

3.   В мастере щелкните **Удалить подписку Microsoft Intune из Configuration Manager**, нажмите кнопку **Далее**, а затем еще раз нажмите кнопку **Далее**, чтобы удалить подписку.


## <a name="how-to-remove-the-service-connection-point-role"></a>Удаление роли точки подключения службы

1.  Выберите **Администрирование** > **Обзор** > **Конфигурация сайта** > **Серверы и роли системы сайта**.

2.  Выберите сервер, на котором размещена роль **Точка подключения службы**.

3.  Из списка **Роли системы сайта** выберите **Точка подключения службы**, а затем на ленте щелкните **Удалить роль**. Подтвердите удаление роли. Точка подключения службы будет удалена.

Теперь можно создать новую точку подключения службы, добавить новую подписку Intune в Configuration Manager и задать Configuration Manager в качестве центра управления мобильными устройствами.

## <a name="how-to-change-mdm-authority-to-intune"></a>Изменение Центра MDM на Intune
Начиная с версий Configuration Manager 1610 и Microsoft Intune 1705 можно изменять Центр MDM. Для этого вам не нужно обращаться в службу поддержки Майкрософт, отменять регистрацию или повторно регистрировать существующие управляемые устройства. См. дополнительные сведения об [изменении Центра MDM](/sccm/mdm/deploy-use/change-mdm-authority).
