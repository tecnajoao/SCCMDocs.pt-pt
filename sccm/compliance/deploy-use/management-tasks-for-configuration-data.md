---
title: Gerir dados de configuração
titleSuffix: Configuration Manager
description: Depois de criar itens de configuração e linhas de base no System Center Configuration Manager, pode utilizar outros comandos para efetuar diversas ações.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b48c693c-d2b0-4707-a5dd-fe92172c49fe
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: d4602a2dbee04259d5953873485cdbccdc58167d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32333665"
---
# <a name="manage-configuration-data-in-system-center-configuration-manager"></a>Gerir os dados de configuração no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Depois de criar itens de configuração e linhas de base de configuração no System Center Configuration Manager, são disponibilizados mais comandos para o ajudar a realizar várias ações.  

## <a name="manage-configuration-items"></a>Gerir itens de configuração  

-   No **ativos e compatibilidade** área de trabalho, expanda **as definições de compatibilidade** > **itens de configuração**, selecione o item de configuração para gerir e, em seguida, selecione uma tarefa de gestão.  

|Tarefa de gestão|Detalhes|  
|---------------------|-------------|  
|**Criar um item de configuração subordinado**|Abre o **Assistente de Criação de Item de Configuração Subordinado** onde pode criar um item de configuração subordinado a partir do item de configuração selecionado.<br /><br /> Não é possível criar um item de configuração subordinado a partir de um item de configuração do dispositivo móvel.<br /><br /> Para obter mais informações, consulte [criar itens de configuração subordinados](../../compliance/deploy-use/create-child-configuration-items.md).|  
|**Histórico de Revisão**|Abre a caixa de diálogo **Histórico de Revisão do Item de Configuração** onde pode ver e gerir as revisões anteriores do item de configuração selecionado.|  
|**Ver Definição XML**|Apresenta o ficheiro de definição de XML para o item de configuração selecionado numa nova janela. Estas informações podem ser úteis quando pretende criar manualmente os dados de configuração.|  
|**Exportarar**|Exporta um item de configuração num formato de ficheiro cabinet (.cab), desde que tenha sido criado nesse site. Pode, em seguida, importá-lo para o mesmo ou outro site do Configuration Manager. Os dados de configuração são convertidos para Resumo DCM.|  
|**Copiar**|Cria uma cópia do item de configuração selecionado com o nome que especificar. O novo item de configuração não mantém qualquer relação com o item de configuração original. Isto significa que o item de configuração duplicado não continua a herdar as informações de configuração do item de configuração original.|  
|**Eliminar**|Abre a caixa de diálogo **Eliminar Item de Configuração** onde poderá consultar quaisquer referências a este item de configuração.<br /><br /> Deve remover todas as referências a um item de configuração antes de poder eliminá-lo.|  

## <a name="manage-configuration-baselines"></a>Gerir linhas de base de configuração  

-   No **ativos e compatibilidade** área de trabalho, expanda **as definições de compatibilidade** > **linhas de base de configuração**, selecione a linha de base de configuração para gerir e, em seguida, selecione uma tarefa de gestão.  


|Tarefa de gestão|Detalhes|  
|---------------------|-------------|  
|**Mostrar Membros**|Apresenta todos os itens de configuração referidos pela linha de base de configuração.|  
|**Agendar Resumo**|Configura o agendamento através do qual os dados apresentados a **linhas de base de configuração** nó na consola do Configuration Manager é atualizado com as informações mais recentes da base de dados do site.|  
|**Executar o Resumo**|O resumo faz com que os dados no nó **Linhas de Base de Configuração** sejam atualizados com os dados mais recentes a partir da base de dados do site. Esta ação pode demorar vários minutos a ser concluída. Poderá ter de clicar em **Atualizar** para visualizar os dados mais recentes na consola.|  
|**Ver Definição XML**|Apresenta o ficheiro de definição de XML da linha de base de configuração selecionada numa nova janela. Estas informações podem ser úteis quando pretende criar manualmente os dados de configuração.|  
|**Ativar**|Permite uma linha de base de configuração para monitorização de compatibilidade.|  
|**Desativar**|Desativa uma linha de base de configuração para que já não seja avaliada relativamente a compatibilidade em computadores cliente. As linhas de base de configuração que referem esta linha de base de configuração também serão desativadas.|  
|**Exportarar**|Exporta uma linha de base de configuração num formato de ficheiro cabinet (.cab), desde que tenha sido criado nesse site. Pode, em seguida, importá-lo para o mesmo ou outro site do Configuration Manager. Os dados de configuração são convertidos para Resumo DCM.<br /><br /> Para obter informações sobre como importar dados de configuração, consulte [importar dados de configuração](../../compliance/deploy-use/import-configuration-data.md).|  
|**Copiar**|Cria uma cópia da linha de base de configuração selecionada com o nome que especificar. A nova linha de base de configuração não mantém qualquer relação com a linha de base de configuração original.|  
|**Eliminar**|Abre a caixa de diálogo **Eliminar Linha de Base de Configuração** onde pode consultar quaisquer referências a esta linha de base de configuração.<br /><br /> Deve remover todas as referências a uma linha de base de configuração antes de poder eliminá-la.|  
|**Implementar**|Abre a caixa de diálogo **Implementar Baseline da Configuração** para poder implementar uma ou mais linhas de base de configuração para dispositivos na sua hierarquia.<br /><br /> Para obter mais informações, consulte [implementar linhas de base de configuração](../../compliance/deploy-use/deploy-configuration-baselines.md).|  
