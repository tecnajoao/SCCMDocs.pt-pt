---
title: Como criar planos de implantação
titleSuffix: Configuration Manager
description: Um guia de procedimentos para criar planos de implantação no ambiente de trabalho de análise.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4b56fac3060acc16fe46221464ddc6535b478399
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124454"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>Como criar planos de implantação no ambiente de trabalho de análise 

> [!Note]  
> Estas informações se relaciona com o serviço de pré-visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft faz não oferece quaisquer garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Este artigo fornece os passos para criar um plano de implantação no ambiente de trabalho de análise. Antes de começar, primeiro [Saiba mais sobre os planos de implantação](/sccm/desktop-analytics/about-deployment-plans).

Siga os passos neste artigo para utilizar a análise de ambiente de trabalho para criar um plano para implantar o Windows 10 e Office 365 ProPlus. Crie planos de implantação para o Windows 10, do Office 365 ProPlus ou ambos.

1. Abra o [do portal da análise de ambiente de trabalho](https://aka.ms/m365aprod). Utilize as credenciais que têm, pelo menos, **contribuidores de área de trabalho** permissões.  

2. Selecione **planos de implantação** no grupo gerenciar.  

3. Na **planos de implementação** painel, selecione **criar**.  

4. Na **criar plano de implantação** painel, configure as seguintes definições:  

    - **Nome**: Um nome exclusivo para o plano de implantação  

    - **Produtos e versões**: Escolha quais os produtos e versões para implementar. A Microsoft recomenda a criação de planos de implantação do Office e do Windows em conjunto e utilizar as versões mais recentes.  

    - **Grupos de dispositivos**: Selecione um ou mais grupos e, em seguida, selecione **definido como grupos de destino**. Grupos com **SCCM** como a origem são coleções sincronizadas a partir do Configuration Manager.  

    - **Regras de preparação**: Estas regras ajudam a determinar quais os dispositivos que está qualificado para atualização. 

    - **Data de conclusão**: Escolha a data através do qual Windows e do Office devem ser totalmente implementadas em todos os dispositivos visados.  

5. Selecione **Criar**. O novo plano é apresentada na lista de planos de implantação ao seu a ser processado. Processamento pode demorar até 48 horas antes de poder prosseguir para o passo seguinte.   

6. Abra o plano de implantação, selecionando o seu nome.  

7. No menu de plano de implementação, na **Prepare** grupo, selecione **identificar importância**.  

    1. Sobre o **aplicações** separador, selecione para mostrar apenas **não revisto** ativos.  

    2. Selecione todas as aplicações e, em seguida, selecione **editar**. Pode selecionar mais do que uma aplicação para editar ao mesmo tempo.   

    3. Escolha um nível de importância do **importância** lista. Se pretender que o ambiente de trabalho de análise para validar o suplemento durante o piloto, selecione **crítico** ou **importante**. Ele não será validado suplementos marcados como **não importante**. Considere o risco de compatibilidade e outras informações de plano ao atribuir níveis de importância.  

        Ao atribuir níveis de importância, também pode escolher o decisão de atualização.  

    4. Selecione **guardar** quando terminar.  

    5. Repita estes passos para o **suplementos do Office**.  

8. No menu de plano de implementação, na **Prepare** grupo, selecione **identificar piloto**.  

    1. Reveja os dispositivos recomendados para o piloto.  

    2. Selecione cada dispositivo e selecione **adicionar ao projeto-piloto**. Se discordar com a recomendação, selecione **substitua**.  

        Para obter mais informações sobre como o ambiente de trabalho de análise torna estas recomendações, selecione o ícone de informações no canto superior direito do **identificar piloto** painel.



### <a name="next-steps"></a>Passos seguintes

Avance para o artigo seguinte para implementar em dispositivos pilotos.
> [!div class="nextstepaction"]  
> [Implementar para piloto](/sccm/desktop-analytics/deploy-pilot)  
