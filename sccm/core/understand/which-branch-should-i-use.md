---
title: "Qual ramificação devo usar | Microsoft Docs"
description: "Aprenda as diferenças entre as ramificações disponíveis do System Center Configuration Manager."
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 662901e850566756759fcfc61c58f3c0e56bc5aa
ms.openlocfilehash: 26356a80bd8c78d4517253bae73e53d8d8f3a73a
ms.contentlocale: pt-pt
ms.lasthandoff: 06/03/2017


---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>Qual ramificação do Configuration Manager deve usar?

*Aplica-se a: System Center Configuration Manager (ramificação atual, o Branch de serviços de longo prazo e Technical Preview)*


A partir de outubro de 2016, há três ramificações do System Center Configuration Manager disponíveis. Use este tópico para ajudar a escolher a ramificação certa para você.

> [!TIP]  
> Todos os sites em uma hierarquia devem executar o mesmo da ramificação. Não há suporte para ter uma hierarquia com ramificações diferentes em sites diferentes.

## <a name="current-branch-of-system-center-configuration-manager"></a>Ramificação atual do System Center Configuration Manager
Este é um branch licenciado para uso em um ambiente de produção em que você deseja que a opção para obter os últimos recursos e funcionalidades. Esta é a ramificação a ser usado se você tiver um dos seguintes: Data Center do System Center, padrão do System Center, o System Center Configuration Manager ou direitos de assinatura equivalente. Para obter mais informações sobre Software Assurance e as opções de licenciamento, consulte [licenciamento e ramificações para o System Center Configuration Manager](learn-more-editions.md).


>  [!TIP]
> O Branch atual pode ser instalado como edição de avaliação que não requer uma licença. Pode ser usada uma edição de avaliação de 180 dias, e dá suporte à atualização para uma edição licenciada do Branch atual.

O Branch atual é atualizado várias vezes por ano com novos recursos. Cada versão de atualização tem suporte para um ano após seu lançamento. Você deve atualizar para uma versão mais recente da ramificação atual em ou antes da expiração do período de um ano. Atualizações para versões mais recentes estão disponíveis como atualizações no console.

Para instalar o Branch atual como um novo site ou uma atualização do System Center 2012 Configuration Manager com Service Pack 2 ou o System Center 2012 R2 Configuration Manager com Service Pack 1, você deve usar [mídia de linha de base](/sccm/core/servers/manage/updates#baseline-and-update-versions) do System Center Configuration Manager que é fornecida como um DVD com o System Center 2016, ou que está disponível como parte de uma versão autônoma do System Center Configuration Manager. Acesso a esta mídia depende de como o System Center Configuration Manager tem licenciado. Linha de base em versões posteriores, como 1702 não dão suporte à instalação do LTSB.

Você também pode usar a mídia de linha de base para instalar um novo site que é uma edição de avaliação do Branch atual. Se você deseja instalar uma edição de avaliação, você pode obter o software a partir de [Centro de avaliação TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) site.

>  [!NOTE]
> Use a mídia de linha de base para instalar sites para uma nova hierarquia do Configuration Manager. Se você instalou anteriormente uma versão de linha de base como a versão 1511, use atualizações no console para atualizar seus sites para uma nova versão, como 1606.
>
> Sites que são atualizados usando o resultado de atualizações em sites que são o mesmo que o novo site instalado usando a mídia de linha de base no console.
>
> Para obter mais informações, consulte [atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).

**Recursos do Branch atual**
- Recebe [atualizações no console](/sccm/core/servers/manage/install-in-console-updates) que tornam os novos recursos disponíveis para uso.
- Recebe atualizações no console que fornecem segurança e correções de qualidade em recursos existentes.
- Oferece suporte a atualizações fora de banda quando necessário. Consulte [usar a ferramenta de registro de atualização](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes) ou [usar o instalador do hotfix](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates).
- Pode interoperar com o Microsoft Intune e outros serviços baseados em nuvem e da infraestrutura.
- Dá suporte a [migração de dados](/sccm/core/migration/migrate-data-between-hierarchies) de e para outras instalações do Configuration Manager.
- Dá suporte à atualização de versões anteriores do Configuration Manager.
- Dá suporte à instalação como uma edição de avaliação, do qual você pode atualizar para uma instalação totalmente licenciada mais tarde.

A versão inicial da ramificação atual foi versão 1511. Atualizações subsequentes incluem versões 1602, 1606 e assim por diante. Cada versão permanece no suporte para um ano, e a Microsoft recomenda que você atualize para a versão mais recente logo após seu lançamento. Você pode esperar um ano antes de atualizar para uma versão mais recente, e você também pode ignorar um update para instalar a versão mais recente disponível. Como cada versão é cumulativo, se você ignorar uma atualização e instale a versão mais recente, você ainda receber acesso a todos os recursos e melhorias de versões anteriores.

Para obter mais informações, consulte [suporte para versões de ramificação atual](/sccm/core/servers/manage/current-branch-versions-supported).

**Opções de atualização**
- Com garantia de Software ativo, você pode instalar as atualizações no console para versões de ramificação atual.  
- Não há nenhuma opção para converter o Branch atual para uma visualização técnica. Visualização técnica está instalações separadas que não exigem uma licença.
- Não há nenhuma opção para converter o Branch atual para a longo prazo manutenção LTSB (Branch). Você deve desinstalar o Branch atual e, em seguida, instale o LTSB como uma nova instalação.

##  <a name="long-term-servicing-branch-of-system-center-configuration"></a>Longo prazo Branch de serviços de configuração do System Center
Este é um branch licenciado para uso em produção para clientes do Configuration Manager que estão usando o Branch atual e permitiu seu Configuration Manager Software Assurance (SA) ou direitos de assinatura equivalente para expirar depois de 1º de outubro de 2016. Para obter mais informações sobre Software Assurance e as opções de licenciamento, consulte [licenciamento e ramificações para o System Center Configuration Manager](learn-more-editions.md).

O LTSB se baseia na versão 1606. A ramificação não recebe atualizações no console que fornecem novos recursos ou atualizar recursos existentes. No entanto, correções de segurança críticas são fornecidas. Para instalar o LTSB, você deve usar a versão 1606 [mídia de linha de base](/sccm/core/servers/manage/updates#baseline-and-update-versions) que você obtém como um DVD com o System Center 2016 ou o System Center Configuration Manager.

Para instalar o LTSB como um novo site ou uma atualização de um site com suporte do Configuration Manager 2012, use a versão 1606 [mídia de linha de base](/sccm/core/servers/manage/updates#baseline-and-update-versions) que você obtém como um DVD com o System Center 2016 ou versão do System Center Configuration Manager (ramificação atual e 1606 de ramificação de manutenção de longo prazo). Você pode usar a mídia de linha de base para instalar um novo site que executa a versão 1606 do Branch atual ou um novo site que executa o Branch de serviços de longo prazo.

> [!TIP]  
> Para saber mais sobre o System Center 2016, consulte [documentação do System Center 2016](https://technet.microsoft.com/system-center-docs/system-center). Esta documentação também identifica como obter o System Center 2016, o que exige um contrato de licença da Microsoft ou direitos semelhantes.

> Para localizar o System Center Configuration Manager versão 1606 no Volume Licensing Service Center (VLSC), vá para o **chaves e Downloads** guia do [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), procure "configuração do Centro de sistema" e, em seguida, selecione **System Center Config Mgr (ramificação atual e LTSB)**.

> Você também pode obter uma edição de avaliação do System Center 2016 do [Centro de avaliação TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview).

**Recursos do LTSB**
-    Recebe atualizações no console que fornecem correções de segurança crítica
- Fornece uma opção de instalação quando os contrato ou equivalente direitos SA para o Configuration Manager expiraram
- Dá suporte à atualização (conversão) para o Branch atual quando você tiver um contrato SA ou direitos equivalentes para o Configuration Manager

**Limitações**  
O LTSB é baseada na versão 1606 do Branch atual e tem as seguintes limitações:
- O LTSB é suportado para 10 anos de atualizações críticas de segurança após sua disponibilidade geral (outubro de 2016), após o qual, suporte para essa ramificação expira. Para obter mais informações sobre o ciclo de vida de suporte, consulte [Microsoft Lifecycle Policy](https://support.microsoft.com/en-us/lifecycle).
- Oferece suporte a uma lista de conjunto limitado de sistemas operacionais cliente e servidor e tecnologias relacionadas, como nas versões do SQL Server. Para obter mais informações sobre o que é compatível com esta ramificação, consulte [configurações com suporte para a ramificação de manutenção de longo prazo](supported-configurations-for-ltsb.md).
- Não recebe atualizações para os novos recursos.
- Não oferece suporte a adição de uma assinatura do Microsoft Intune, que impede o uso de:
  -    Intune em uma configuração de MDM híbrida
 - MDM local
-    Não suporte o uso do painel de serviço do Windows 10, manutenção planos, Windows 10 CB (Branch atual) ou ramificação atual para negócios (CBB).
- Não oferece suporte a versões futuras do Windows 10 LTSB e Windows Server.
-    Não há suporte para o Asset Intelligence.
-    Não há suporte para pontos de distribuição baseado em nuvem.
-    Não há suporte para o suporte para o Exchange Online como um conector do Exchange.
-    Não oferece suporte a quaisquer recursos de pré-lançamento.



**Opções de atualização**
- Você pode converter sua instalação LTSB para uma instalação de ramificação atual. A conversão para a ramificação atual é suportada antes ou depois que o suporte para o LTSB expira.

  Para converter, você deve ter um contrato de Software Assurance ativado com a Microsoft. Para obter mais informações, consulte os links a seguir:
  - [Atualizar o Long Term Servicing Branch para o Current Branch](convert-to-current-branch.md)
  - [Licenciamento e ramificações para o System Center Configuration Manager](learn-more-editions.md)
  - [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#baseline-and-update-versions) na [atualizações do Configuration Manager](/sccm/core/servers/manage/updates)
- Não há nenhuma opção para converter o LTSB em uma visualização técnica. Visualização técnica está instalações separadas que não exigem uma licença.
-    Você não pode atualizar uma edição de avaliação do Branch atual para uma instalação LTSB.


## <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview do System Center Configuration Manager
A visualização técnica é para uso em um ambiente de laboratório em que você deseja conhecer e experimente os recursos mais novos que estão sendo desenvolvidos para o Configuration Manager. A visualização técnica não tem suporte em um ambiente de produção e não exige que você tenha um contrato de licença do Software Assurance.

Para instalar um novo site que executa o Technical Preview, use a versão mais recente [mídia de linha de base para o System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview#install-and-update-the-technical-preview). Depois de instalar o Technical Preview, novas versões estão disponíveis como atualizações no console por mês.

**Recursos da visualização técnica**
-  Com base em versões recentes de linha de base do Branch atual
-  Recebe atualizações no console que atualizam a instalação para a versão mais recente do Technical Preview
-  Inclui novos recursos que estão sendo desenvolvidos e para que nossos desenvolvedores gostaria que os seus comentários
-  Recebe atualizações que se aplicam somente para o Technical Preview

**Limitações**
-  [O suporte é limitado](/sccm/core/get-started/technical-preview#requirements-and-limitatins-for-the-techincal-preview), incluindo apenas um único site primário e até 10 clientes.  
-  Não pode ser atualizada para uma ramificação atual ou LTSB.
-  Não oferece suporte a usar a migração para importar ou exportar dados para outra instalação do Configuration Manager.
-  Não oferece suporte a atualização de uma versão anterior do Configuration Manager.
-  Não dá suporte a instalação como uma edição de avaliação.

Recursos que são introduzidos pela primeira vez em uma visualização técnica geralmente são adicionados para a ramificação atual em uma atualização posterior. Cada nova versão de Technical Preview inclui os recursos de visualização técnica anterior, mesmo depois que esses recursos foram adicionados para a ramificação atual.

Para obter mais informações, consulte [visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview).

**Opções de atualização**
-    Você pode instalar qualquer atualização no console para uma nova versão de Technical Preview.
-    Não há nenhuma opção para converter uma visualização técnica para a ramificação atual ou LTSB.


## <a name="identify-your-branch-and-version"></a>Identificar a ramificação e versão
Quando você exibe informações de versão para um site do Configuration Manager, você também confirmar a ramificação.

**Versão**   
Para verificar a versão do seu site, no console vá para **sobre o System Center Configuration Manager** no canto superior esquerdo do console onde o **versão do Site** é exibida. Consulte [ ]() para obter uma lista de versões do site.

**Ramificação**  
Para confirmar a ramificação do seu site (como o LTSB ou ramificação atual), no console, vá para **administração** > **configuração do Site** > **Sites**e abra **configurações da hierarquia**. Se há uma opção para converter para o Branch atual e ele estiver ativo, o site executa a versão LTSB. Quando o site é executada a ramificação atual, essa opção fica esmaecida.
Para obter informações sobre as diferentes versões do Configuration Manager, consulte "versões de linha de base e atualização" [atualizações do Configuration Manager](/sccm/core/servers/manage/updates).

