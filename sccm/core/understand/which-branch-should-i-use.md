---
title: O ramo devo utilizar | Documentos do Microsoft
description: "Saiba as diferenças entre ramos disponíveis do System Center Configuration Manager."
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
ms.sourcegitcommit: 90775fcf2549080a43e9c1606caa79d9eb90a89c
ms.openlocfilehash: f791278b0aa8efc734a894da7dab1704bb567ed0
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>O ramo do Configuration Manager devo utilizar?

*Aplica-se a: System Center Configuration Manager (ramo atual, ramo de manutenção de longo prazo e pré-visualização técnica)*


Iniciar em Outubro de 2016, existem três ramos do System Center Configuration Manager está disponível. Utilize este tópico para ajudar a escolher o ramo direita por si.

> [!TIP]  
> Todos os sites numa hierarquia tem de executar a mesma sucursal. Não é suportada para ter uma hierarquia com ramos diferentes em sites diferentes.

## <a name="current-branch-of-system-center-configuration-manager"></a>Ramo atual do System Center Configuration Manager
Este é um ramo licenciado para utilização num ambiente de produção onde pretende que a opção para obter as funcionalidades e remoto através da mais recente. Este é o ramo a utilizar se tiver um dos seguintes procedimentos: Centro de dados do System Center, System Center padrão, System Center Configuration Manager ou direitos de subscrição equivalente. Para mais informações sobre o Software Assurance e opções de licenciamento, consulte o artigo [licenciamento e ramos para o System Center Configuration Manager](learn-more-editions.md).


>  [!TIP]
> O ramo atual pode ser instalado como edição de avaliação que não necessita de uma licença. Pode ser utilizada uma edição de avaliação de 180 dias e suporta a atualização para uma edição licenciada do mesmo atual.

O ramo atual é atualizado várias vezes num ano com novas funcionalidades. Cada versão de atualização é suportada para um ano depois da versão. Tem de atualizar para uma versão mais recente do ramo atual em ou antes da data de expiração desse período de um ano. As atualizações para as versões mais recentes estão disponíveis como atualizações na consola.

Instalar o ramo atual como um novo site ou como uma atualização do System Center 2012 Configuration Manager com Service Pack 2 ou System Center 2012 R2 Configuration Manager com Service Pack 1, que utiliza [suportes de dados de linha de base](/sccm/core/servers/manage/updates#baseline-and-update-versions) para o System Center Configuration Manager que vem como um DVD com o System Center 2016 ou que está disponível como parte de uma versão autónoma do System Center Configuration Manager. Acesso a este suporte depende da forma como tiver licenciado o System Center Configuration Manager. Versões posteriores do plano base, como 1702 não suportam instale o LTSB.

Também pode utilizar o suporte de dados do plano base para instalar um novo site é uma edição de avaliação do mesmo atual. Se pretende instalar apenas uma edição de avaliação, pode obter software a partir de [Centro de avaliação TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) Web site.

>  [!NOTE]
> Utilize suportes de dados do plano base para instalar sites para uma nova hierarquia do Configuration Manager. Se tiver instalado anteriormente uma versão de linha de base como versão 1511, utilize atualizações de na consola para atualizar os sites para uma nova versão, como 1606.
>
> Sites que são atualizados com atualizações resultado em sites que são os mesmos que o novo site instalado utilizando o suporte de dados do plano base na consola.
>
> Para mais informações consulte [atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).

**Funcionalidades do mesmo atual**
- Recebe [na consola atualizações](/sccm/core/servers/manage/install-in-console-updates) que tornam as novas funcionalidades disponíveis para utilização.
- Recebe atualizações numa consola que entrega de segurança e correções de qualidade a das funcionalidades existentes.
- Suporta atualizações fora de banda quando for necessário. Consulte o artigo [utilizar a ferramenta de registo de atualização](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes) ou [utilizar o instalador de correção](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates).
- Pode interagir com o Microsoft Intune e outros serviços baseados na nuvem e infraestrutura.
- Suporta [migração de dados](/sccm/core/migration/migrate-data-between-hierarchies) de e para outras instalações do Configuration Manager.
- Suporta atualizar a partir de versões anteriores do Gestor de configuração.
- Suporta a instalação como uma edição de avaliação, a partir do qual mais tarde pode atualizar para uma instalação completamente licenciada.

A edição inicial do mesmo atual foi versão 1511. As atualizações subsequentes incluem as versões 1602, 1606 e assim sucessivamente. Cada versão permanece no suporte de um ano e, a Microsoft recomenda que Atualize para a versão mais recente logo após a versão. Pode aguardar até um ano antes de atualizar para uma versão mais recente e também pode ignorar uma atualização para instalar a versão mais recente disponível. Uma vez cada versão é cumulativa, se passar de uma atualização e instalar a versão mais recente, ainda irá obter acesso a todas as funcionalidades e melhorias de versões anteriores.

Para obter mais informações, consulte o artigo [suporte das versões do ramo atual](/sccm/core/servers/manage/current-branch-versions-supported).

**Opções de atualização**
- Com o Software Assurance ativo, poderá instalar atualizações de na consola para versões de ramo atual.  
- Não existe nenhuma opção para converter o ramo atual para uma pré-visualização técnica. Técnicas pré-visualizações são separadas instalações que não necessitam de uma licença.
- Não existe nenhuma opção para converter o ramo atual para a longo prazo manutenção ramo (LTSB). Tem de desinstalar o ramo atual e, em seguida, instalar o LTSB como uma nova instalação.

##  <a name="long-term-servicing-branch-of-system-center-configuration"></a>Longa duração ramo de manutenção de configuração do System Center
Este é um ramo licenciado para utilização em produção para os clientes do Configuration Manager que estiver a utilizar o ramo atual e tiver permitido o Configuration Manager Software Assurance (SA) ou direitos de subscrição equivalentes para expirarem após 1 de Outubro de 2016. Para mais informações sobre o Software Assurance e opções de licenciamento, consulte o artigo [licenciamento e ramos para o System Center Configuration Manager](learn-more-editions.md).

O LTSB baseia-se na versão 1606. Este ramo não recebem atualizações na consola fornecer novas funcionalidades ou atualizar capacidades existentes. No entanto, são fornecidas correções de segurança importantes. Para instalar o LTSB, tem de utilizar a versão 1606 [suportes de dados de linha de base](/sccm/core/servers/manage/updates#baseline-and-update-versions) que obtém como um DVD com o System Center 2016 ou o System Center Configuration Manager.

Para instalar o LTSB como um novo site ou como uma atualização a partir de um site suportado do Configuration Manager 2012, utilize a versão 1606 [suportes de dados de linha de base](/sccm/core/servers/manage/updates#baseline-and-update-versions) que obtém como um DVD com o System Center 2016 ou versão do System Center Configuration Manager (ramo atual e longo prazo manutenção ramo 1606). Pode utilizar suportes de dados do plano base para instalar um novo site que executa versão 1606 do mesmo atual, ou um novo site que executa o ramo de manutenção de longo prazo.

> [!TIP]  
> Para saber mais sobre o System Center 2016, consulte o artigo [documentação do System Center 2016](https://technet.microsoft.com/system-center-docs/system-center). Esta documentação também identifica como obter o System Center 2016, que necessita de um contrato de licença da Microsoft ou direitos semelhantes.

> Para encontrar o System Center Configuration Manager versão 1606 no licenciamento em Volume serviço System Center (VLSC), aceda ao **transfere e chaves** separador do [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), procure "configuração do system center" e, em seguida, selecione **System Center Config Mgr (ramo atual e LTSB 1606)**.

> Também pode obter uma edição de avaliação do System Center 2016 a partir de [Centro de avaliação TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview).

**Funcionalidades do LTSB**
-    Recebe atualizações numa consola que correções de segurança importantes
- Fornece uma opção de instalação quando os direitos de contrato ou equivalente SA do Configuration Manager já passaram da validade
- Suporta atualizar (conversão) para o ramo atual quando tem um contrato de SA atual ou direitos equivalentes para o Configuration Manager

**Limitações**  
O LTSB baseia-se na versão atual ramo 1606 e tem as seguintes limitações:
- O LTSB é suportada para 10 anos de atualizações de segurança importantes após a respetiva disponibilidade geral (Outubro de 2016), após o qual, suporte para este ramo expira. Para mais informações sobre o ciclo de vida do suporte, consulte o artigo [Microsoft Lifecycle Policy](https://support.microsoft.com/en-us/lifecycle).
- Suporta uma lista de conjunto limitado de sistemas operativos de servidor e cliente e tecnologias relacionadas, como versões do SQL Server. Para mais informações sobre o que é suportado com este ramo, consulte o artigo [configurações suportadas para o ramo de manutenção de longo prazo](supported-configurations-for-ltsb.md).
- Não receber atualizações sobre as novas funcionalidades.
- Não suporta a adição de uma subscrição do Windows Intune, que impede que a utilização de:
  -    Intune numa configuração híbrida MDM
 - MDM no local
-    Não suporta a utilização do Dashboard de manutenção do Windows 10, planos de manutenção, Windows 10 atual ramo (CB) ou ramo atual para empresas (CBB).
- Não suporta versões futuras do LTSB do Windows 10 e Windows Server.
-    Sem suporte para o Asset Intelligence.
-    Sem suporte para os pontos de distribuição baseado na nuvem.
-    Sem suporte para o suporte para o Exchange Online como um conector do Exchange.
-    Não suporta as funcionalidades da versão de pré-lançamento.



**Opções de atualização**
- Pode converter a instale LTSB para uma instalação de ramo atual. A conversão para o ramo atual é suportada antes ou depois de suporte para o LTSB expira.

  Para converter, tem de ter um contrato de Software Assurance ativo com a Microsoft. Para obter mais informações, consulte as seguintes ligações:
  - [Atualizar o ramo de manutenção de longa duração para o ramo atual](convert-to-current-branch.md)
  - [Licenciamento e ramos para o System Center Configuration Manager](learn-more-editions.md)
  - [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#baseline-and-update-versions) no [atualizações para o Configuration Manager](/sccm/core/servers/manage/updates)
- Não existe nenhuma opção para converter o LTSB para uma pré-visualização técnica. Técnicas pré-visualizações são separadas instalações que não necessitam de uma licença.
-    É possível atualizar uma edição de avaliação do mesmo atual para uma instalação LTSB.


## <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview do System Center Configuration Manager
A pré-visualização técnica é para utilização num ambiente de laboratório onde pretende saber mais sobre e experimentar as funcionalidades mais recentes que está a ser desenvolvidas para o Configuration Manager. A pré-visualização técnica não é suportada num ambiente de produção e não requer que tenha um contrato de licença de Software Assurance.

Para instalar um novo site que executa a pré-visualização técnica, utilize a versão mais recente [suportes de dados de linha de base para o System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview#install-and-update-the-technical-preview). Depois de instalar a pré-visualização técnica, existem novas versões como na consola as atualizações de cada mês.

**Funcionalidades de pré-visualização do técnico**
-  Com base nas versões recentes do plano base do mesmo atual
-  Recebe atualizações numa consola que a instalação de atualizações para a versão mais recente da pré-visualização técnica
-  Inclui novas funcionalidades que estão a ser desenvolvida e para o qual os nossos programadores gostaria que os seus comentários
-  Recebe atualizações que se aplicam apenas para o ramo de pré-visualização técnica

**Limitações**
-  [O suporte está limitado](/sccm/core/get-started/technical-preview#requirements-and-limitatins-for-the-techincal-preview), incluindo um único site primário e até 10 clientes.  
-  Não é possível atualizar a um ramo atual ou LTSB.
-  Não suporta utilizando a migração para importar ou exportar dados para outra instalação do Configuration Manager.
-  Não suporta a atualização a partir de uma versão anterior do Configuration Manager.
-  Não suporta a instalação como uma edição de avaliação.

Funcionalidades que são introduzidas pela primeira vez numa pré-visualização técnica, muitas vezes, são adicionadas para o ramo atual numa atualização posterior. Cada nova versão de pré-visualização técnica inclui as funcionalidades de pré-visualizações técnicas anterior, mesmo depois dessas funcionalidades foram adicionadas para o ramo atual.

Para obter mais informações, consulte o artigo [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview).

**Opções de atualização**
-    É possível instalar qualquer atualização na consola de uma nova versão de pré-visualização técnica.
-    Não existe nenhuma opção para converter uma pré-visualização técnica para o ramo atual ou LTSB.


## <a name="identify-your-branch-and-version"></a>Identificar os ramo e da versão
Ao visualizar informações sobre a versão de um site do Configuration Manager, também confirme a ramificação.

**Versão**   
Para verificar a versão do seu site, na consola do aceda à **sobre o System Center Configuration Manager** no canto superior esquerdo da consola onde o **versão do Site** aparece. Consulte o artigo [ ]() para obter uma lista das versões do site.

**Ramo**  
Para confirmar o ramo do seu site (como o LTSB ou ramo atual), na consola de ir para **administração** > **configuração do Site** > **Sites**, no computador e abra **definições de hierarquia**. Se existir uma opção para converter para o ramo atual e está ativo, o site executa a versão LTSB. Quando o site executa o ramo atual, esta opção a cinzento.
Para obter informações sobre as diversas versões do Configuration Manager, consulte "versões de linha de base e atualização" no [atualizações para o Configuration Manager](/sccm/core/servers/manage/updates).

