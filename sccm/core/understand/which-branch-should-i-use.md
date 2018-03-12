---
title: O ramo devo utilizar
titleSuffix: Configuration Manager
description: "Saber as diferenças entre ramos disponíveis do System Center Configuration Manager."
ms.custom: na
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
caps.latest.revision: 
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: d762cf5e6932e17d8dfb0dd6c442c452028b5228
ms.sourcegitcommit: b653342fb5d69a16e71b3548a7e9a2e47e54bf88
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/12/2018
---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>O ramo do Configuration Manager devo utilizar?

*Aplica-se a: O System Center Configuration Manager (ramo atual, ramo de manutenção longo prazo e pré-visualização técnica)*


A partir de Outubro de 2016, existem três ramos do System Center Configuration Manager está disponível. Utilize este tópico para ajudar a escolher o ramo correto para si.

> [!TIP]  
> Todos os sites numa hierarquia tem de executar o ramo do mesmo. Não é suportado para ter uma hierarquia com ramos diferentes em sites diferentes.

## <a name="current-branch-of-system-center-configuration-manager"></a>Ramo atual do System Center Configuration Manager
Este é um ramo licenciado para utilização num ambiente de produção onde pretende que a opção para obter as mais recentes e funcionalidades. Este é o ramo a utilizar se tiver um dos seguintes: Centro de dados do System Center, System Center, System Center Configuration Manager ou padrão direitos equivalentes de subscrição. Para obter mais informações sobre Software Assurance e opções de licenciamento, consulte [licenciamento e ramos para o System Center Configuration Manager](learn-more-editions.md).


>  [!TIP]
> O ramo atual pode ser instalado como uma edição de avaliação não é necessária uma licença. Pode ser utilizada uma edição de avaliação de 180 dias e suporta a atualização para uma edição licenciada da filial atual.

O ramo atual é atualizado várias vezes um ano com as novas funcionalidades. Cada versão de atualização é suportada para um ano depois da versão. Tem de atualizar para uma versão mais recente do Current Branch no ou antes da expiração desse período de um ano. Atualizações para versões mais recentes estão disponíveis como atualizações na consola.

Para instalar o ramo atual como um novo site ou como uma atualização do System Center 2012 Configuration Manager com Service Pack 2 ou System Center 2012 R2 Configuration Manager com Service Pack 1, pode utilizar [suporte de dados de linha de base](/sccm/core/servers/manage/updates#baseline-and-update-versions) do System Center Configuration Manager que é fornecido como um DVD com o System Center 2016 ou que está disponível como parte da versão autónoma do System Center Configuration Manager. Acesso a este suporte de dados depende de como tiver licenciado System Center Configuration Manager. Instalar versões posteriores de linha de base, como 1702 não suportam o LTSB.

Também pode utilizar o suporte de dados de linha de base para instalar um novo site que é uma edição de avaliação da filial atual. Se pretender instalar apenas uma edição de avaliação, pode obter o software a partir de [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) Web site.

>  [!NOTE]
> Utilize suportes de dados de linha de base para instalar sites para uma nova hierarquia do Configuration Manager. Se anteriormente tiver instalado uma versão de linha de base como a versão 1511, utilize as atualizações na consola para atualizar os sites para uma nova versão, como 1606.
>
> Os sites que são atualizadas utilizando o resultado de atualizações de sites que são os mesmos que o novo site instalado utilizando o suporte de dados de linha de base na consola.
>
> Para obter mais informações consulte [atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).

**Funcionalidades do ramo atual**
- Recebe [atualizações na consola](/sccm/core/servers/manage/install-in-console-updates) que tornam as novas funcionalidades disponíveis para utilização.
- Recebe atualizações na consola que fornecem a segurança e correções de qualidade a funcionalidades existentes.
- Suporta atualizações fora de banda quando for necessário. Consulte [utilizar a ferramenta de registo de atualização](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes) ou [utilizar o instalador de correções](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates).
- Pode interagir com o Microsoft Intune e outros serviços baseados na nuvem e infraestrutura.
- Suporta [migração dos dados](/sccm/core/migration/migrate-data-between-hierarchies) de e para outras instalações do Configuration Manager.
- Suporta a atualização de versões anteriores do Configuration Manager.
- Suporta a instalação como uma edição de avaliação, a partir da qual pode posteriormente atualizar para uma instalação totalmente licenciada.

A edição inicial do ramo atual tinha a versão 1511. As atualizações subsequentes incluem as versões 1602, 1606 e assim sucessivamente. Cada versão permanece no suporte durante um ano, e a Microsoft recomenda que Atualize para a versão mais recente logo após a versão. Pode aguardar até um ano antes de atualizar para uma versão mais recente, e também pode ignorar uma atualização para instalar a versão mais recente disponível. Porque cada versão for cumulativa, se ignorar através de uma atualização e instalar a versão mais recente, ainda, irá obter acesso a todas as funcionalidades e melhoramentos de versões anteriores.

Para obter mais informações, consulte [suporte para versões de Current Branch](/sccm/core/servers/manage/current-branch-versions-supported).

**Opções de atualização**
- Com o Active Directory Software Assurance, poderá instalar atualizações na consola para as versões do ramo atual.  
- Não há nenhuma opção para converter o ramo atual para uma versão de pré-visualização técnica. Pré-visualizações técnicas são instalações separadas que não necessitam de uma licença.
- Não há nenhuma opção para converter o ramo atual para a longo prazo Servicing Branch (LTSB). Tem de desinstalar o ramo atual e, em seguida, instalar o LTSB como uma instalação de novo.

##  <a name="long-term-servicing-branch-of-system-center-configuration"></a>Ramo de manutenção longo prazo de configuração do System Center
Este é um ramo licenciado para utilização em produção para que os clientes do Configuration Manager que estiver a utilizar o ramo atual e que tenham permitido respetivo Configuration Manager Software Assurance (SA) ou direitos de subscrição equivalente para expirar após 1 de Outubro de 2016. Para obter mais informações sobre Software Assurance e opções de licenciamento, consulte [licenciamento e ramos para o System Center Configuration Manager](learn-more-editions.md).

O LTSB baseiam-se a versão 1606. Este ramo não receber atualizações na consola que fornecem novas funcionalidades ou capacidades existentes de atualização. No entanto, são fornecidas correções de segurança críticas. Para instalar o LTSB, tem de utilizar a versão 1606 [suporte de dados de linha de base](/sccm/core/servers/manage/updates#baseline-and-update-versions) que obtém como um DVD com o System Center 2016 ou o System Center Configuration Manager.

Para instalar o LTSB como um novo site ou como uma atualização de um site suportado do Configuration Manager 2012, utilize a versão 1606 [suporte de dados de linha de base](/sccm/core/servers/manage/updates#baseline-and-update-versions) que obtém como um DVD com o lançamento do System Center Configuration Manager (ramo atual e 1606 de sucursal de manutenção longo prazo) ou o System Center 2016. Pode utilizar suportes de dados de linha de base para instalar um novo site que executa a versão 1606 do ramo atual, ou um novo site que executa o ramo de manutenção de longo prazo.

> [!TIP]  
> Para saber mais sobre o System Center 2016, consulte [documentação do System Center 2016](https://docs.microsoft.com/system-center/index). Esta documentação também identifica como obter o System Center 2016, o que necessita de um contrato de licença da Microsoft ou direitos semelhantes.

> Para localizar o System Center Configuration Manager versão 1606 no Volume Licensing Service Center (VLSC), vá para o **transfere e chaves** separador do [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), procure "configuração de centro de sistema" e, em seguida, selecione **System Center Config Mgr (ramo atual e LTSB)**.

> Também pode obter uma edição de avaliação do System Center 2016 do [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview).

**Funcionalidades do LTSB**
-   Recebe atualizações na consola que fornecem correções de segurança críticas
- Fornece uma opção de instalação quando os direitos de contrato ou equivalente SA para o Configuration Manager expiraram
- Suporta a atualização (conversão) para o ramo atual quando tem um contrato de SA atual ou os direitos equivalentes para o Configuration Manager

**Limitações**  
O LTSB baseia-se na versão 1606 de Current Branch e tem as seguintes limitações:
- O LTSB é suportada para 10 anos de atualizações de segurança críticas após a respetiva disponibilidade geral (Outubro de 2016), após o qual, suporte para este ramo expira. Para mais informações sobre o ciclo de vida de suporte, consulte [Microsoft Lifecycle Policy](https://support.microsoft.com/lifecycle).
- Suporta uma lista de conjunto limitado de servidor e sistemas operativos cliente e as tecnologias relacionadas, como as versões do SQL Server. Para mais informações sobre o que é suportado com este ramo, consulte [configurações suportadas para o ramo de manutenção de longo prazo](supported-configurations-for-ltsb.md).
- Não recebe atualizações para as novas funcionalidades.
- Não suporta a adição de uma subscrição do Microsoft Intune, que impede que a utilização de:
  - Intune numa configuração de MDM híbrida
 - MDM no local
-   Não suporta a utilização do Dashboard de manutenção do Windows 10, planos de manutenção, Windows 10 Current Branch (CB) ou Current Branch for Business (CBB).
- Não suporta versões futuras do Windows 10 LTSB e o Windows Server.
-   Sem suporte para o Asset Intelligence.
-   Não existe suporte para pontos de distribuição baseado na nuvem.
-   Sem suporte para obter suporte para o Exchange Online como um conector do Exchange.
-   Não suporta todas as funcionalidades de pré-lançamento.



**Opções de atualização**
- Pode converter a instalação LTSB para uma instalação do ramo atual. A conversão para o ramo atual é suportada antes ou depois do suporte para o LTSB expira.

  Para converter, tem de ter um contrato de Software Assurance Active Directory com a Microsoft. Para obter mais informações, consulte as seguintes ligações:
  - [Atualizar o Long Term Servicing Branch para o Current Branch](convert-to-current-branch.md)
  - [Licenciamento e ramos para o System Center Configuration Manager](learn-more-editions.md)
  - [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#baseline-and-update-versions) no [atualizações para o Configuration Manager](/sccm/core/servers/manage/updates)
- Não há nenhuma opção para converter o LTSB para uma versão de pré-visualização técnica. Pré-visualizações técnicas são instalações separadas que não necessitam de uma licença.
-   Não é possível atualizar uma edição de avaliação do ramo atual para uma instalação de LTSB.


## <a name="technical-preview-for-system-center-configuration-manager"></a>Pré-visualização técnica do System Center Configuration Manager
O Technical Preview destina-se a utilização num ambiente de laboratório em que pretende saber mais sobre e experimentar as funcionalidades mais recentes que está a ser desenvolvidas para o Configuration Manager. O Technical Preview não é suportado num ambiente de produção e não necessita de ter um contrato de licença do Software Assurance.

Para instalar um novo site que executa o Technical Preview, utilize a versão mais recente [suportes de dados de linha de base para o System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview#install-and-update-the-technical-preview). Depois de instalar a pré-visualização técnica, existem novas versões como atualizações na consola cada mês.

**Funcionalidades do Technical Preview**
-  Com base em recente versões de linha de base do Current Branch
-  Recebe atualizações na consola que a instalação da atualização para a versão mais recente do Technical Preview
-  Inclui novas funcionalidades que estão a ser desenvolvidas e para os quais os nossos programadores gostaria que os seus comentários
-  Recebe atualizações que se aplicam apenas para o ramo do Technical Preview

**Limitações**
-  [O suporte está limitado](/sccm/core/get-started/technical-preview#requirements-and-limitatins-for-the-techincal-preview), incluindo apenas um único site primário e até 10 clientes.  
-  Não é possível atualizar a um ramo atual ou LTSB.
-  Não suporta a utilização de migração para importar ou exportar dados para outra instalação do Configuration Manager.
-  Não suporta a atualização a partir de uma versão anterior do Configuration Manager.
-  Não suporta a instalação como uma edição de avaliação.

Funcionalidades que foram primeiro introduzidas numa versão de pré-visualização técnica, muitas vezes, são adicionadas para o ramo atual, numa atualização posterior. Cada nova versão de pré-visualização técnica inclui as funcionalidades de pré-visualizações técnicas anteriores, mesmo depois dessas funcionalidades foram adicionadas para o ramo atual.

Para obter mais informações, consulte [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview).

**Opções de atualização**
-   Pode instalar qualquer atualização na consola para uma nova versão de pré-visualização técnica.
-   Não há nenhuma opção para converter uma versão de pré-visualização técnica para o ramo atual ou LTSB.


## <a name="identify-your-branch-and-version"></a>Identificar o ramo e versão
Ao visualizar informações de versão para um site do Configuration Manager, também confirmar o ramo.

**Versão**   
Para verificar a versão do seu site, além da consola, aceda a **sobre o System Center Configuration Manager** no canto superior esquerdo da consola onde a **versão do Site** aparece. Consulte [versões de linha de base e atualização](/sccm/core/servers/manage/updates#bkmk_Baselines) para uma lista de versões de sites.

**Branch**  
Para confirmar o ramo do seu site (como o LTSB ou o ramo atual), na consola, aceda a **administração** > **configuração do Site** > **Sites**e abra **definições de hierarquia**. Se existir uma opção para converter para o ramo atual e este está ativo, o site executa a versão LTSB. Quando o site é executado o ramo atual, esta opção está desativada. Para obter informações sobre as diferentes versões do Configuration Manager, consulte "versões de linha de base e a atualização" no [atualizações para o Configuration Manager](/sccm/core/servers/manage/updates).
