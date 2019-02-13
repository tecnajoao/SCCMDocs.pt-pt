---
title: O ramo devo utilizar
titleSuffix: Configuration Manager
description: Aprenda as diferenças entre ramos disponíveis do System Center Configuration Manager.
ms.date: 05/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0bb478eb875e97d8e3088e50daab8538113b40c5
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139590"
---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>O ramo do Configuration Manager devo utilizar?

*Aplica-se a: O System Center Configuration Manager (ramo atual, Long term Servicing Branch e pré-visualização técnica)*


Existem três ramos do System Center Configuration Manager disponíveis: ramo atual, Long term servicing branch e pré-visualização técnica. Utilize este tópico para ajudar a escolher o ramo certo para.

> [!TIP]  
> Todos os sites numa hierarquia tem de executar o ramo do mesmo. Não é suportada para ter uma hierarquia com ramificações diferentes em sites diferentes.


## <a name="current-branch"></a>Ramo atual
Este ramo é licenciado para utilização num ambiente de produção. Utilize este ramo para obter as funções e funcionalidades mais recentes. Se tiver uma das seguintes licenças, pode utilizar este ramo:  
- Centro de dados do System Center
- System Center Standard
- O System Center Configuration Manager
- Direitos de equivalente de subscrição  

Para obter mais informações sobre o Software Assurance e opções de licenciamento, consulte [ramificações para o System Center Configuration Manager e de licenciamento](learn-more-editions.md) e [perguntas mais frequentes sobre ramos do Configuration Manager e licenciamento](/sccm/core/understand/product-and-licensing-faq).

A Microsoft planeja lançar atualizações para o ramo atual do System Center Configuration Manager algumas vezes por ano. Para versões do Configuration Manager lançado antes do 1710, o suporte é de 12 meses. Cada versão de atualização a partir da versão 1710, permanece no suporte de 18 meses a partir da data de lançamento de disponibilidade geral (GA). É fornecido suporte técnico para o período de inteiro de suporte. No entanto, a nossa estrutura de suporte é dinâmica, tendo evoluído para duas fases de manutenção distintas que dependem da disponibilidade da versão do ramo atual mais recente. (Para obter mais informações, consulte o tópico intitulado [suporte para versões de ramo atual do System Center Configuration Manager](https://docs.microsoft.com/sccm/core/servers/manage/current-branch-versions-supported). Atualizações para versões mais recentes estão disponíveis como atualizações na consola.

Para instalar o ramo atual como um novo site, utilize [suporte de dados de linha de base](/sccm/core/servers/manage/updates#baseline-and-update-versions). Também utilize suportes de dados de linha de base para atualizar a partir do System Center 2012 Configuration Manager com Service Pack 2 ou o System Center 2012 R2 Configuration Manager com Service Pack 1. Acesso a este suporte de dados depende de como a sua organização licenciados System Center Configuration Manager. 

Também pode utilizar o suporte de dados de linha de base para instalar um novo site que é uma edição de avaliação do current branch. A edição de avaliação não requer uma licença. Pode usar a edição de avaliação de 180 dias. Suporta a atualização para uma edição licenciada do ramo atual. Para instalar apenas uma edição de avaliação, obtê-lo a partir da [Centro de avaliação TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection).

> [!NOTE]
> Utilize suportes de dados de linha de base para instalar sites para uma nova hierarquia do Configuration Manager. Se instalou anteriormente uma versão de linha de base, utilize atualizações na consola para atualizar seus sites para uma nova versão.  
> 
> Sites que são atualizados com o resultado de atualizações em sites que são os mesmos que o novo site instalado com o suporte de dados de linha de base na consola.
> 
> Para obter mais informações, veja [Atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).  


### <a name="features-of-the-current-branch"></a>Funcionalidades do ramo atual
- Recebe [atualizações na consola](/sccm/core/servers/manage/install-in-console-updates) que tornam as novas funcionalidades disponíveis para utilização.
- Recebe atualizações na consola, que proporcionam segurança e correções de qualidade para os recursos existentes.
- Suporta atualizações fora de banda quando necessário. Para obter mais informações, consulte [utilizar a ferramenta de registo de atualização](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes) ou [utilize o instalador de correções](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates).
- Integra-se com o Microsoft Intune e outros serviços com base na cloud.
- Suporta [migração de dados](/sccm/core/migration/migrate-data-between-hierarchies) de e para outras instalações do Configuration Manager.
- Suporta a atualização de versões anteriores do Configuration Manager.
- Suporta a instalação como uma edição de avaliação, a partir da qual mais tarde pode atualizar para uma instalação totalmente licenciada.

A versão inicial do ramo atual era a versão 1511. As atualizações subsequentes incluem versões 1602, versão 1606 e assim por diante. Cada versão permaneça no suporte durante um ano e a Microsoft recomenda que Atualize para a versão mais recente logo após seu lançamento. Pode esperar até um ano antes de atualizar para uma versão mais recente, e também pode ignorar uma atualização para instalar a versão mais recente disponível. Porque cada versão é cumulativo, se Pular uma atualização e instalar a versão mais recente, ainda obtém acesso a todos os recursos e aprimoramentos de versões anteriores.

Para obter mais informações, consulte [suporte para versões atuais do ramo](/sccm/core/servers/manage/current-branch-versions-supported).


### <a name="update-options"></a>Opções de atualização
- Com Software Assurance ativo, pode instalar atualizações na consola para as versões atuais do ramo.  
- Não existe nenhuma opção para converter o ramo atual para um ramo de pré-visualização técnica. Os ramos de pré-visualização técnica são instalações separadas que não requerem uma licença.
- Não existe nenhuma opção para converter o ramo atual para o Long term servicing branch (LTSB). Tem de desinstalar o ramo atual e, em seguida, instalar o LTSB como uma nova instalação.



##  <a name="long-term-servicing-branch"></a>Long term servicing branch 
Este ramo está licenciado para uso na produção para os clientes de Configuration Manager que estiver a utilizar o ramo atual e que tenham permitido seus Configuration Manager Software Assurance (SA) ou direitos de subscrição equivalente para expirar após 1 de Outubro de 2016. Para mais informações sobre o Software Assurance e opções de licenciamento, consulte [ramificações para o System Center Configuration Manager e de licenciamento](learn-more-editions.md) e [perguntas mais frequentes para ramos do Configuration Manager e o licenciamento](/sccm/core/understand/product-and-licensing-faq).

O LTSB baseia-se a versão 1606. Este ramo não recebe atualizações na consola que ofereça novas funcionalidades ou atualizar as capacidades existentes. No entanto, as correções de segurança críticas são fornecidas. Para instalar o LTSB, tem de utilizar a versão 1606 [suporte de dados de linha de base](/sccm/core/servers/manage/updates#baseline-and-update-versions) que obtém com o System Center 2016. Versões posteriores da linha de base não suportam a instalação do LTSB.

Para instalar o LTSB como um novo site ou como uma atualização a partir de um site suportado do Configuration Manager 2012, utilize a versão 1606 [suporte de dados de linha de base](/sccm/core/servers/manage/updates#baseline-and-update-versions) que obtém com o System Center 2016. Pode utilizar suportes de dados de linha de base para instalar um novo site que executa a versão 1606 do ramo atual, ou um novo site que executa o Long term servicing branch.

> [!TIP]  
> Para saber mais sobre o System Center 2016, veja [documentação do System Center 2016](https://docs.microsoft.com/system-center/index). Esta documentação também identifica como obter o System Center 2016, o que necessita de um contrato de licença da Microsoft ou semelhante direitos.  
>  
> Para encontrar o System Center Configuration Manager versão 1606 no Volume Licensing Service Center (VLSC), vá para o **Downloads e chaves** separador da [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), procurar `System Center 2016`e, em seguida, selecione **System Center 2016 Datacenter** ou **padrão do System Center 2016**.  
>  
> Também pode obter uma edição de avaliação do System Center 2016 a partir da [Centro de avaliação TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview).  


### <a name="features-of-the-ltsb"></a>Recursos do LTSB
-   Recebe atualizações na consola que fornecem correções de segurança críticas.
- Fornece uma opção de instalação quando seus direitos de contrato ou o equivalente do SA para o Configuration Manager tem expirado.
- Suporta a atualização (conversão) para o current branch quando tiver um contrato SA atual ou os direitos equivalentes para o Configuration Manager.


### <a name="limitations"></a>Limitações  
O LTSB baseia-se a versão atual do ramo 1606 e tem as seguintes limitações:
- O LTSB é suportado pelos 10 anos de atualizações críticas de segurança após sua disponibilidade geral (Outubro de 2016), após o qual, suporte para este ramo expira. Para obter mais informações sobre o ciclo de vida de suporte, consulte [Microsoft Lifecycle Policy](https://support.microsoft.com/lifecycle).
- Oferece suporte a uma lista de conjunto limitado de sistemas operativos cliente e servidor e tecnologias relacionadas, como versões do SQL Server. Para mais informações sobre o que é suportado com este ramo, consulte [configurações suportadas do Long term servicing branch](supported-configurations-for-ltsb.md).
- Não recebe atualizações para novas funcionalidades
- Não suporta as seguintes capacidades: 
   - Adicionar uma subscrição do Microsoft Intune, que impede a utilização de:
     -  Intune numa configuração de MDM híbrida
     - MDM no local
   -    O Windows 10, dashboard de manutenção, manutenção planos ou canal semianual do Windows 10
   - Versões futuras do Windows 10 LTSB e no Windows Server
   -    Do Asset intelligence
   -    Pontos de distribuição baseados na nuvem
   -    Exchange Online como um conector do Exchange
   -    Quaisquer funcionalidades de pré-lançamento


### <a name="update-options"></a>Opções de atualização
- Pode converter a instalação LTSB para uma instalação do ramo atual. A conversão para o current branch é suportada antes ou depois de suporte para o LTSB expira.

  Para converter, tem de ter um contrato de Software Assurance ativo com a Microsoft. Para obter mais informações, consulte as seguintes ligações:
  - [Atualizar o Long Term Servicing Branch para o Current Branch](convert-to-current-branch.md)
  - [Licenciamento e ramificações do System Center Configuration Manager](learn-more-editions.md)
  - [Versões de linha de base e de atualização](/sccm/core/servers/manage/updates#baseline-and-update-versions) 
- Não existe nenhuma opção para converter o LTSB para um ramo de pré-visualização técnica. Os ramos de pré-visualização técnica são instalações separadas que não requerem uma licença.
-   Não é possível atualizar uma edição de avaliação do ramo atual para uma instalação de LTSB.



## <a name="technical-preview-branch"></a>Pré-visualização técnica
O ramo de pré-visualização técnica é para utilização num ambiente de laboratório. Saiba mais sobre e experimentar as funcionalidades mais recentes que estão sendo desenvolvidas para o Configuration Manager. Não é suportada num ambiente de produção e não exige que tem um contrato de licença do Software Assurance.

Para instalar um novo site que executa o ramo de pré-visualização técnica, utilize a versão mais recente [suporte de dados de linha de base para o ramo de pré-visualização técnica](/sccm/core/get-started/technical-preview#install-and-update-the-technical-preview). Depois de instalar o ramo de pré-visualização técnica, novas versões estão disponíveis como atualizações na consola de cada mês.


### <a name="features-of-the-technical-preview-branch"></a>Funcionalidades do ramo de pré-visualização técnica
-  Com base em versões recentes de linha de base do current branch
-  Recebe atualizações na consola que atualizarem a instalação para a última versão do ramo de pré-visualização técnica
-  Inclui novos recursos que estão a ser desenvolvidas e para o qual a Microsoft quer os seus comentários
-  Recebe atualizações que se aplicam apenas para o ramo de pré-visualização técnica


### <a name="limitations"></a>Limitações
-  [O suporte é limitado](/sccm/core/get-started/technical-preview#requirements-and-limitatins-for-the-techincal-preview), incluindo apenas um único site primário e até 10 clientes.  
-  Não é possível atualizar para um ramo atual ou LTSB.
-  Não suporta os seguintes comportamentos:
   - Utilizar a migração para importar ou exportar dados para outra instalação do Configuration Manager
   - Atualizar de uma versão anterior do Configuration Manager
   - Instalação como uma edição de avaliação

Funcionalidades que são introduzidas pela primeira vez numa ramificação de pré-visualização técnica, muitas vezes, são adicionadas para o current branch numa atualização posterior. Cada nova versão do ramo de pré-visualização técnica inclui as funcionalidades de ramos de pré-visualização técnica anterior, mesmo depois dessas funcionalidades foram adicionadas para o current branch.

Para obter mais informações, consulte a [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview).


### <a name="update-options"></a>Opções de atualização
-   Pode instalar qualquer atualização na consola para uma nova versão do ramo de pré-visualização técnica.
-   Não existe nenhuma opção para converter um ramo de pré-visualização técnica para o current branch ou LTSB.



## <a name="identify-your-version-and-branch"></a>Identificar a sua versão e o ramo

### <a name="version"></a>Versão   
Para verificar a versão do seu site, além da consola, aceda a **sobre o System Center Configuration Manager** no canto superior esquerdo da consola. Esta caixa de diálogo apresenta os **versão do Site**. Para obter uma lista das versões de site, consulte [versões de linha de base e atualização](/sccm/core/servers/manage/updates#bkmk_Baselines).

### <a name="branch"></a>Ramo
Para confirmar o ramo do seu site, na consola, aceda a **Administration** > **configuração do Site** > **Sites**e abra **Definições de hierarquia**. Se existir uma opção para converter para current branch e estiver ativo, o site executa a versão LTSB. Quando o site é executado o ramo atual, esta opção está a cinzento.

Para obter mais informações sobre as diferentes versões do Configuration Manager, consulte [versões de linha de base e atualização](/sccm/core/servers/manage/updates#bkmk_Baselines).
