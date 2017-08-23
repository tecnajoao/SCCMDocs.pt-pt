---
title: "Использование многоадресной рассылки для развертывания Windows по сети | Документы Майкрософт"
description: "С помощью многоадресной рассылки в среде System Center Configuration Manager можно обеспечить одновременное скачивание образа операционной системы несколькими компьютерами."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
caps.latest.revision: "13"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 55266696aa7340fddda3a57ff90e20222ff665a5
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Использование многоадресной рассылки для развертывания Windows по сети с помощью System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Многоадресная рассылка — это метод оптимизации сети, который можно использовать в средах System Center Configuration Manager, где высока вероятность того, что несколько клиентов будут одновременно загружать один образ операционной системы. Когда используется многоадресная рассылка, несколько компьютеров могут одновременно загружать образ операционной системы, рассылаемый точкой распространения. Этот механизм заменяет сценарий отправки точкой распространения копии данных на каждый клиентский компьютер через отдельное подключение.  

 Вы можете развертывать операционные системы по сети с использованием многоадресной рассылки в следующих сценариях развертывания операционной системы:  

-   [Обновление существующего компьютера до новой версии Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Установка новой версии Windows на новом компьютере (без операционной системы)](install-new-windows-version-new-computer-bare-metal.md)  

 Выполните действия, указанные для одного из сценариев развертывания операционной системы, а затем используйте сведения из приведенных ниже разделов для обеспечения поддержки многоадресной рассылки.  

##  <a name="BKMK_Configure"></a> Настройка точки распространения для обеспечения поддержки многоадресной рассылки  
 Перед использованием многоадресной рассылки при развертывании операционной системы необходимо настроить точку распространения на поддержку такой рассылки. Дополнительные сведения см. в разделе [Настройка точек распространения для поддержки многоадресной рассылки](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast).  

## <a name="prepare-an-operating-system-image-for-multicast-deployments"></a>Подготовка образа операционной системы для многоадресных развертываний  
 Сведения о настройке пакета образа операционной системы для поддержки многоадресной рассылки см. в разделе [Подготовка образа операционной системы для многоадресных развертываний](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).  

##  <a name="BKMK_Deploy"></a> Развертывание последовательности задач  
 Выполните развертывание операционной системы в целевой коллекции. Дополнительные сведения см. в статье [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  
