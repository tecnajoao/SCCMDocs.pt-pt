---
title: "Настройка требований к имени домена с помощью System Center Configuration Manager | Документация Майкрософт"
description: "Настройка требований к имени домена с помощью System Center Configuration Manager."
ms.custom: na
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 522c2e82-20eb-4f38-859b-d55640b24e32
caps.latest.revision: "18"
caps.handback.revision: "0"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 35b24294073956a6bdb14cae07705f56d31e00a9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="confirm-domain-name-requirements-with-system-center-configuration-manager-and-microsoft-intune"></a>Настройка требований к имени домена с помощью System Center Configuration Manager и Microsoft Intune

*Применимо к: System Center Configuration Manager (Current Branch)*

Если вам требуется выполнить условия всех зависимостей, являющихся внешними для Configuration Manager, сделайте следующее:

1. Каждый пользователь должен иметь лицензию Intune для регистрации устройств. Чтобы связать лицензии Intune с пользователями, каждый пользователь должен иметь имя участника-пользователя (UPN), которое может быть разрешено через Интернет (например, johndoe@contoso.com или альтернативный идентификатор входа в Azure Active Directory). Настройка альтернативного идентификатора входа позволяет пользователям выполнять вход с помощью адреса электронной почты, например, даже если их UPN-имена указаны в формате NetBIOS (например, CONTOSO\johndoe).

  - Если ваша компания использует разрешимые, доступные через Интернет имена участников-пользователей (т. е. johndoe@contoso.com), дальнейшая настройка не требуется.
  - Если ваша компания использует неразрешимое имя субъекта-пользователя (например, CONTOSO\johndoe), необходимо [настроить альтернативный идентификатор в Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync).

2.  Разверните и настройте службы федерации Active Directory (AD FS). (Необязательный)

     При настройке единого входа пользователи могут войти в систему, указав корпоративные учетные данные для использования служб в Intune.

     Дополнительные сведения см. в следующих разделах:
    -   [Подготовка к осуществлению единого входа](http://go.microsoft.com/fwlink/?LinkID=271124)
    -   [Планирование и развертывание служб федерации Active Directory 2.0 для использования с единым входом](http://go.microsoft.com/fwlink/?LinkID=271125)

3.  Разверните и настройте синхронизацию службы каталогов.

     Синхронизация службы каталогов позволяет заполнить Intune синхронизированными учетными записями пользователей. Синхронизированные учетные записи пользователей и группы безопасности добавляются в Intune. Ошибка включения синхронизации каталогов является распространенной причиной, по которой устройства не могут выполнить регистрацию при настройке управления мобильными устройствами Configuration Manager с использованием Microsoft Intune.

     Дополнительные сведения см. в статье [Интеграция каталогов](http://go.microsoft.com/fwlink/?LinkID=271120) библиотеки документации Active Directory.

4.  Необязательно, не рекомендуется: если службы федерации Active Directory (AD FS) не используются, сбросьте пароли пользователей Microsoft Online.

     Если вы не используете службы федерации Active Directory, необходимо задать пароль для каждого пользователя Microsoft Online.

> [!div class="button"]
[< Назад](create-mdm-collection.md) [Вперед >](configure-intune-subscription.md)
