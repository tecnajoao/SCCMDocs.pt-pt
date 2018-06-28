---
title: O ramo devo utilizar
titleSuffix: Configuration Manager
description: Saber as diferenças entre ramos disponíveis do System Center Configuration Manager.
ms.date: 05/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4331ec4120141ab9aa20301b9a99c3c6ebeef568
ms.sourcegitcommit: 0305e710f634529793ae73e5aac24168ee4fe02f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 06/27/2018
ms.locfileid: "37042750"
---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>O ramo do Configuration Manager devo utilizar?

*Aplica-se a: O System Center Configuration Manager (ramo atual, ramo de manutenção longo prazo e pré-visualização técnica)*


Existem três ramos do System Center Configuration Manager disponíveis: ramo atual, o ramo de manutenção longo prazo e o ramo de pré-visualização técnica. Utilize este tópico para ajudar a escolher o ramo correto para si.

> [!TIP]  
> Todos os sites numa hierarquia tem de executar o ramo do mesmo. Não é suportada para ter uma hierarquia com ramos diferentes em sites diferentes.


## <a name="current-branch"></a>Ramo atual
Este ramo está licenciado para utilização num ambiente de produção. Utilize este ramo para obter as mais recentes e funcionalidades. Se tiver uma das seguintes licenças, pode utilizar este ramo:  
- Centro de dados do System Center
- O System Center padrão
- O System Center Configuration Manager
- Direitos equivalentes de subscrição  

Para obter mais informações sobre Software Assurance e opções de licenciamento, consulte [licenciamento e ramos para o System Center Configuration Manager](learn-more-editions.md) e [perguntas mais frequentes sobre ramos de Configuration Manager e licenciamento](/sccm/core/understand/product-and-licensing-faq).

Microsoft planos de lançamento atualizações para o ramo atual do System Center Configuration Manager algumas vezes por ano. Para versões do Configuration Manager lançadas antes 1710, o suporte está durante 12 meses. Cada versão de atualização a partir do lançamento 1710, permanece no suporte para 18 meses a partir da respetiva data de lançamento de disponibilidade geral (DG). O suporte técnico é fornecido para o período de suporte completo. No entanto, os nossa estrutura de suporte for dinâmica, evolução em duas fases distintas manutenção que dependem da disponibilidade da versão do ramo atual mais recente. (Para obter mais informações, consulte o tópico intitulado [suporte para versões do System Center Configuration Manager current branch](https://docs.microsoft.com/sccm/core/servers/manage/current-branch-versions-supported). Atualizações para versões mais recentes estão disponíveis como atualizações na consola.

Para instalar o ramo atual como um novo site, utilize [suporte de dados de linha de base](/sccm/core/servers/manage/updates#baseline-and-update-versions). Também utilize suportes de dados de linha de base a atualização do System Center 2012 Configuration Manager com Service Pack 2 ou System Center 2012 R2 Configuration Manager com Service Pack 1. Acesso a este suporte de dados depende de como a sua organização licenciado System Center Configuration Manager. 

Também pode utilizar o suporte de dados de linha de base para instalar um novo site que é uma edição de avaliação da filial atual. A edição de avaliação não necessita de uma licença. Pode utilizar a edição de avaliação de 180 dias. Suporta a atualização para uma edição licenciada da filial atual. Para instalar apenas uma edição de avaliação, obtido a partir de [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection).

>  [!NOTE]  
> Utilize suportes de dados de linha de base para instalar sites para uma nova hierarquia do Configuration Manager. Se instalou anteriormente uma versão de linha de base, utilize atualizações na consola para atualizar os sites para uma nova versão.  
>  
> Os sites que são atualizadas utilizando o resultado de atualizações de sites que são os mesmos que o novo site instalado utilizando o suporte de dados de linha de base na consola.
>
> Para obter mais informações, veja [Atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).  


### <a name="features-of-the-current-branch"></a>Funcionalidades do ramo atual
- Recebe [atualizações na consola](/sccm/core/servers/manage/install-in-console-updates) que tornam as novas funcionalidades disponíveis para utilização.
- Recebe atualizações na consola que fornecem a segurança e correções de qualidade a funcionalidades existentes.
- Suporta atualizações fora de banda quando for necessário. Para obter mais informações, consulte [utilizar a ferramenta de registo de atualização](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes) ou [utilizar o instalador de correções](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates).
- Integra-se com o Microsoft Intune e outros serviços baseados na nuvem.
- Suporta [migração dos dados](/sccm/core/migration/migrate-data-between-hierarchies) de e para outras instalações do Configuration Manager.
- Suporta a atualização de versões anteriores do Configuration Manager.
- Suporta a instalação como uma edição de avaliação, a partir da qual pode posteriormente atualizar para uma instalação totalmente licenciada.

A edição inicial do ramo atual tinha a versão 1511. As atualizações subsequentes incluem as versões 1602, 1606 e assim sucessivamente. Cada versão permanece no suporte durante um ano, e a Microsoft recomenda que Atualize para a versão mais recente logo após a versão. Pode aguardar até um ano antes de atualizar para uma versão mais recente, e também pode ignorar uma atualização para instalar a versão mais recente disponível. Porque cada versão for cumulativa, se ignorar através de uma atualização e instalar a versão mais recente, ainda obtiver acesso a todas as funcionalidades e melhoramentos de versões anteriores.

Para obter mais informações, consulte [suporte para versões do current branch](/sccm/core/servers/manage/current-branch-versions-supported).


### <a name="update-options"></a>Opções de atualização
- Com o Active Directory Software Assurance, poderá instalar atualizações na consola para versões do ramo atual.  
- Não há nenhuma opção para converter o ramo atual para um ramo de pré-visualização técnica. Ramos de pré-visualização técnica são instalações separadas que não requerem uma licença.
- Não há nenhuma opção para converter o ramo atual para o ramo de manutenção longo prazo (LTSB). Tem de desinstalar o ramo atual e, em seguida, instalar o LTSB como uma instalação de novo.



##  <a name="long-term-servicing-branch"></a>Ramo de manutenção longo prazo 
Este ramo está licenciado para utilização em produção para que os clientes do Configuration Manager que estiver a utilizar o ramo atual e que tenham permitido respetivo Configuration Manager Software Assurance (SA) ou direitos de subscrição equivalente para expirar após 1 de Outubro de 2016. Para obter mais informações sobre Software Assurance e opções de licenciamento, consulte [licenciamento e ramos para o System Center Configuration Manager](learn-more-editions.md) e [perguntas mais frequentes para o Configuration Manager ramos eLicenciamento](/sccm/core/understand/product-and-licensing-faq).

O LTSB baseiam-se a versão 1606. Este ramo não recebe atualizações na consola que fornecem novas funcionalidades ou capacidades existentes de atualização. No entanto, são fornecidas correções de segurança críticas. Para instalar o LTSB, tem de utilizar a versão 1606 [suporte de dados de linha de base](/sccm/core/servers/manage/updates#baseline-and-update-versions) que obtém com o System Center 2016. Versões de linha de base posteriores não suportam a instalação do LTSB.

Para instalar o LTSB como um novo site ou como uma atualização de um site suportado do Configuration Manager 2012, utilize a versão 1606 [suporte de dados de linha de base](/sccm/core/servers/manage/updates#baseline-and-update-versions) que obtém com o System Center 2016. Pode utilizar suportes de dados de linha de base para instalar um novo site que executa a versão 1606 do ramo atual, ou um novo site que executa o ramo de manutenção longo prazo.

> [!TIP]  
> Para saber mais sobre o System Center 2016, consulte [documentação do System Center 2016](https://docs.microsoft.com/system-center/index). Esta documentação também identifica como obter o System Center 2016, o que necessita de um contrato de licença da Microsoft ou direitos semelhantes.  
>  
> Para localizar o System Center Configuration Manager versão 1606 no Volume Licensing Service Center (VLSC), vá para o **transfere e chaves** separador do [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), procurar `System Center 2016`e, em seguida, selecione **Centro de dados do system Center 2016** ou **padrão do System Center 2016**.  
>  
> Também pode obter uma edição de avaliação do System Center 2016 do [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview).  


### <a name="features-of-the-ltsb"></a>Funcionalidades do LTSB
-   Recebe atualizações na consola que fornecem correções de segurança críticas.
- Fornece uma opção de instalação quando os direitos de contrato ou equivalente SA para o Configuration Manager tem expirado.
- Suporta a atualização (conversão) para o ramo atual quando tem um contrato de SA atual ou os direitos equivalentes para o Configuration Manager.


### <a name="limitations"></a>Limitações  
O LTSB baseia-se na versão do ramo atual 1606 e tem as seguintes limitações:
- O LTSB é suportada para 10 anos de atualizações de segurança críticas após a respetiva disponibilidade geral (Outubro de 2016), após o qual, suporte para este ramo expira. Para mais informações sobre o ciclo de vida de suporte, consulte [Microsoft Lifecycle Policy](https://support.microsoft.com/lifecycle).
- Suporta uma lista de conjunto limitado de servidor e sistemas operativos cliente e as tecnologias relacionadas, como as versões do SQL Server. Para mais informações sobre o que é suportado com este ramo, consulte [as configurações suportadas para o ramo de manutenção longo prazo](supported-configurations-for-ltsb.md).
- Não recebem atualizações para as novas funcionalidades
- Não suporta as seguintes capacidades: 
   - Adicionar uma subscrição do Microsoft Intune, que impede a utilização de:
     -  Intune numa configuração de MDM híbrida
     - MDM no local
   -    O Windows 10 dashboard de manutenção, manutenção planos ou canal por anual do Windows 10
   - Em versões futuras do Windows 10 LTSB e o Windows Server
   -    Do Asset intelligence
   -    Pontos de distribuição baseados na nuvem
   -    Exchange Online como um conector do Exchange
   -    Todas as funcionalidades de pré-lançamento


### <a name="update-options"></a>Opções de atualização
- Pode converter a instalação LTSB para uma instalação do ramo atual. A conversão para o ramo atual é suportada antes ou depois do suporte para o LTSB expira.

  Para converter, tem de ter um contrato de Software Assurance Active Directory com a Microsoft. Para obter mais informações, consulte as seguintes ligações:
  - [Atualizar o Long Term Servicing Branch para o Current Branch](convert-to-current-branch.md)
  - [Licenciamento e ramos para o System Center Configuration Manager](learn-more-editions.md)
  - [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#baseline-and-update-versions) 
- Não há nenhuma opção para converter o LTSB para um ramo de pré-visualização técnica. Ramos de pré-visualização técnica são instalações separadas que não requerem uma licença.
-   Não é possível atualizar uma edição de avaliação do ramo atual para uma instalação de LTSB.



## <a name="technical-preview-branch"></a>Ramo de pré-visualização técnica
O ramo de pré-visualização técnica é para utilização num ambiente de laboratório. Saiba mais sobre e experimentar as funcionalidades mais recentes que está a ser desenvolvidas para o Configuration Manager. Não é suportado num ambiente de produção e não necessita de ter um contrato de licença do Software Assurance.

Para instalar um novo site que executa o ramo de pré-visualização técnica, utilize a versão mais recente [suportes de dados de linha de base para o ramo de pré-visualização técnica](/sccm/core/get-started/technical-preview#install-and-update-the-technical-preview). Depois de instalar o ramo de pré-visualização técnica, existem novas versões como atualizações na consola cada mês.


### <a name="features-of-the-technical-preview-branch"></a>Funcionalidades do ramo de pré-visualização técnica
-  Com base em recente versões de linha de base da filial atual
-  Recebe atualizações na consola que a instalação da atualização para a versão do ramo de pré-visualização técnica mais recente
-  Inclui novas funcionalidades que estão a ser desenvolvidas e para o qual Microsoft pretender que os seus comentários
-  Recebe atualizações que se aplicam apenas para o ramo de pré-visualização técnica


### <a name="limitations"></a>Limitações
-  [O suporte está limitado](/sccm/core/get-started/technical-preview#requirements-and-limitatins-for-the-techincal-preview), incluindo apenas um único site primário e até 10 clientes.  
-  Não é possível atualizar a um ramo atual ou LTSB.
-  Não suporta os comportamentos seguintes:
   - Utilizando a migração para importar ou exportar dados para outra instalação do Configuration Manager
   - Atualizar a partir de uma versão anterior do Configuration Manager
   - Instalação como uma edição de avaliação

Funcionalidades que foram primeiro introduzidas num ramo de pré-visualização técnica, muitas vezes, são adicionadas para o ramo atual, numa atualização posterior. Cada nova versão do ramo de pré-visualização técnica inclui as funcionalidades de ramos de pré-visualização técnica anterior, mesmo depois dessas funcionalidades foram adicionadas para o ramo atual.

Para obter mais informações, consulte o [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview).


### <a name="update-options"></a>Opções de atualização
-   Pode instalar qualquer atualização na consola para uma nova versão do ramo de pré-visualização técnica.
-   Não há nenhuma opção para converter um ramo de pré-visualização técnica para o ramo atual ou LTSB.



## <a name="identify-your-version-and-branch"></a>Identificar a versão e uma sucursal

### <a name="version"></a>Versão   
Para verificar a versão do seu site, além da consola, aceda a **sobre o System Center Configuration Manager** no canto superior esquerdo da consola. Esta caixa de diálogo apresenta o **versão do Site**. Para obter uma lista de versões de sites, consulte [versões de linha de base e atualização](/sccm/core/servers/manage/updates#bkmk_Baselines).

### <a name="branch"></a>Sucursal
Para confirmar o ramo do seu site, na consola, aceda a **administração** > **configuração do Site** > **Sites**e abra **Definições de hierarquia**. Se existir uma opção para converter para o ramo atual e este está ativo, o site executa a versão LTSB. Quando o site é executado o ramo atual, esta opção está desativada.

Para mais informações sobre as diferentes versões do Configuration Manager, consulte [versões de linha de base e atualização](/sccm/core/servers/manage/updates#bkmk_Baselines).
