---
title: Ativos no ambiente de trabalho Analytics
titleSuffix: Configuration Manager
description: Saiba mais sobre dispositivos, aplicações, aplicações do Office, os suplementos do Office e macros do Office no Analytics de ambiente de trabalho.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b397c4f1a58ed0683e4704d1c484b108c5357717
ms.sourcegitcommit: ad25a7bdd983c5a0e4c95bffdc61c9a1ebcbb765
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/26/2019
ms.locfileid: "55073382"
---
# <a name="assets-in-desktop-analytics"></a>Ativos no ambiente de trabalho Analytics 

> [!Note]  
> Estas informações se relaciona com o serviço de pré-visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft faz não oferece quaisquer garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Depois de dispositivos comunicam dados para análise de ambiente de trabalho, ele fornece um inventário dos ativos seguintes:
- Dispositivos  
- Drivers de hardware  
- Aplicações instaladas  
- Aplicações do Office  
- Suplementos do Office  
- Macros do Office  

No portal do serviço, selecione **ativos** no menu da área de trabalho de análise.


## <a name="devices"></a>Dispositivos

O **dispositivos** separador apresenta informações chave sobre todos os dispositivos da sua organização que se inscreve para análise de ambiente de trabalho. Pode classificar por qualquer coluna ou filtro para valores específicos.

> [!NOTE]  
> Se o dashboard não está a comunicar o número de dispositivos esperado para o seu ambiente, consulte [resolução de problemas de análise de ambiente de trabalho](/sccm/desktop-analytics/troubleshooting).  



## <a name="apps"></a>Aplicações

O **aplicações** separador mostra todas as instaladas aplicações que o serviço Deteta nos seus dispositivos Windows.

**Digno de nota** as aplicações são instaladas em mais de 2% dos dispositivos inscritos. <!--You can change the threshold of "noteworthy" by {doing something}.--> 

Configurar o **importância** de aplicações através da definição de uma das seguintes categorias:

- Crítico
- Importante
- Ignorar
- Não revisto

Selecione a aplicação a partir da lista e selecione **editar**. Esta ação apresenta os detalhes para a aplicação. Selecione o **importância** menu pendente e define um valor. Também pode atribuir um **proprietário**. Se fizer alterações, selecione **guardar**. 


## <a name="office-apps"></a>Aplicações do Office

O **aplicações do Office** separador é semelhante ao separador aplicações. Apenas mostra aplicações como o Microsoft Word ou Excel, e não existe categorização ou contagem digno de nota. Defina o importância e o proprietário para aplicações do Office da mesma forma que com outras aplicações.


## <a name="office-add-ins"></a>Suplementos do Office

O **suplementos do Office** separador mostra ferramentas de suporte, por exemplo, Microsoft Azure Information Protection ou o as de análise. Este separador é semelhante para o separador de aplicações e inclui a contagem de digno de nota. Defina a importância e o proprietário tal como acontece com as aplicações. 


## <a name="office-macros"></a>Macros do Office

O **macros do Office** separador mostra se todos os dispositivos recentemente acederam a todos os ficheiros que podem incluir as macros. 

<!-- (For a detailed list of these file types, see [File formats supported in the 2007 Office system (corrected)](https://blogs.technet.microsoft.com/office_resource_kit/2009/04/04/file-formats-supported-in-the-2007-office-system-corrected/) at the Office IT Pro blog.)
 -->

> [!NOTE]  
> Se também de utilizar o [Readiness Toolkit](https://aka.ms/readinesstoolkit) para os suplementos do Office e o Visual Basic para macros Applications (VBA), essa guia também apresenta os dados adicionais a partir desses dispositivos. 
> 
> Não precisa de utilizar o Kit de ferramentas de preparação para utilizar a análise de ambiente de trabalho.  



## <a name="next-steps"></a>Passos seguintes

- [Saiba mais sobre os planos de implantação de área de trabalho de análise](/sccm/desktop-analytics/about-deployment-plans)  

- [Saiba mais sobre as atualizações de segurança e funcionalidade](/sccm/desktop-analytics/about-updates)  

