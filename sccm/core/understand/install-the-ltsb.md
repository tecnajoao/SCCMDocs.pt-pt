---
title: Instalar um site utilizando o suporte de dados de linha de base de 1606 | Microsoft Docs
description: Instalar ou atualizar para o LTSB para o System Center Configuration Manager.
ms.custom: na
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 247fbe5313c17be906802acfaa6952ab3358122e
ms.sourcegitcommit: a17f5dece340a70cedbec03d19938dab90ae60b1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-upgrade-with-the-version-1606-baseline-media-for-system-center-configuration-manager"></a>Instalar e atualizar com a versão 1606 suporte de dados de linha de base para o System Center Configuration Manager

*Aplica-se a:  O System Center Configuration Manager (ramo atual), (ramo de manutenção longo prazo)*

Quando executar a configuração do suporte de dados de linha de base do versão 1606 para o Configuration Manager, pode instalar o ramo de manutenção de longo prazo ou um site do ramo atual do System Center Configuration Manager.

O suporte de dados de linha de base está disponível no DVD como parte do Microsoft System Center 2016 ou versão do System Center Configuration Manager (ramo atual e 1606 de sucursal de manutenção longo prazo). Para saber mais sobre o suporte de dados de linha de base, consulte [versões de linha de base e atualização](/sccm/core/servers/manage/updates#baseline-and-udpate-versions).


Quando utiliza os versão 1606 da linha de base de dados, é o site instalar ou atualizar para:
- A *site Current Branch* que é equivalente a um site que foi a primeira instalados utilizando o suporte de dados de linha de base 1511 e, em seguida, atualizar a versão 1606 plus o 1606 de rollup de correção - KB3186654.
-   Um *LTSB site* que é equivalente ao site Current Branch que executa o rollup de correção de versão 1606 plus o 1606 - KB3186654. O suporte de dados de linha de base já inclua o rollup de correção.  No entanto, o LTSB não suporta todas as funcionalidades ou capacidades disponíveis com o ramo atual, conforme detalhado em [introdução para a longo prazo manutenção ramo do System Center Configuration Manager](introduction-to-the-ltsb.md).

Se não estiver familiarizado com os ramos diferentes do System Center Configuration Manager, consulte [o ramo do Configuration Manager devo utilizar](which-branch-should-i-use.md).




## <a name="changes-to-setup-with-the-1606-baseline-media"></a>Alterações à configuração com o suporte de dados de linha de base de 1606
O suporte de dados de linha de base de 1606 apresenta as seguintes alterações à configuração do Configuration Manager.

### <a name="branch-and-edition"></a>Ramo e edição
Quando executar a configuração, é agora apresentada uma página de licenciamento, onde pode selecionar o ramo do Configuration Manager que pretende instalar. Pode escolher o ramo atual ou LTSB como uma instalação licenciada, ou pode escolher uma edição de avaliação da filial atual como uma instalação não licenciado.

Para obter mais informações, consulte [licenciamento e ramos para o System Center Configuration Manager](learn-more-editions.md).

### <a name="software-assurance-expiration"></a>Expiração do Software Assurance
Durante a configuração, tem a opção para introduzir o **data de expiração do Software Assurance** valor. Este é um valor opcional que pode especificar como um lembrete conveniente.

> [!NOTE]
> Microsoft não valida a data de expiração, introduza e não utilize esta data para validação da licença.  Em vez disso, pode utilizá-lo como um lembrete da sua data de expiração. Isto é útil porque o Configuration Manager periodicamente verifica a existência de novas atualizações de software disponibilizadas online e o estado de licença do software assurance deve ser atual para serem elegíveis para utilizar estas atualizações adicionais.    

- Pode especificar o valor de data no **chave de produto** página do Assistente de configuração ao executar a configuração da versão System Center Configuration Manager 1606 suporte de dados de linha de base.
- Também pode especificar esta data selecionando **propriedades de definições de hierarquia** > **licenciamento** na consola do Configuration Manager.

Para obter mais informações, consulte "Contratos de Software Assurance" em [licenciamento e ramos para o System Center Configuration Manager](learn-more-editions.md).


### <a name="additional-pre-upgrade-configurations"></a>Configurações de pré-atualização adicionais
Antes de iniciar uma atualização do System Center 2012 Configuration Manager para o LTSB, tem de colocar os seguintes passos adicionais como parte da lista de verificação de pré-atualização.  
Desinstale as funções de sistema de sites que o LTSB não suporta:
- Ponto de sincronização do Asset Intelligence
- Conector do Microsoft Intune
- Pontos de distribuição baseados na nuvem

Para obter mais informações, consulte [atualizar para o System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).


### <a name="new-scripted-installation-options"></a>Novas opções de instalação com script
O suporte de dados de linha de base do versão 1606 suporta uma nova chave de ficheiro de script automático para instalações com scripts de um novo site de nível superior. Isto aplica-se para instalar um novo site primário autónomo ou a adição de um site de administração central como parte de um cenário de expansão do site.

Quando utilizar um script automático para instalar um ramo licenciado, tem de adicionar a secção seguinte, os nomes de chaves e valores para a secção de opções do seu script. Não precisa de utilizar estes valores para a instalação de uma edição de avaliação do ramo atual do script:  

 **SABranchOptions**
-   **Nome da chave: SAActive**
  - Valores: 0 ou 1.  
  - Detalhes:  0 instala uma edição de avaliação não licenciado do ramo atual, e 1 instala uma edição licenciada.   

- **CurrentBranch**
  - Valores: 0 ou 1.  
  - Detalhes:  0 instala o ramo de manutenção de longo prazo e 1 instala o ramo atual.  

Por exemplo, para instalar uma edição licenciada do ramo atual utilize:

  **Nome da chave: SABranchOptions**
   -    **SAActive = 1**
   - **CurrentBranch = 1**


> [!IMPORTANT]  
> **SABranchOptions** só funciona com a configuração do suporte de dados de linha de base. Não é aplicável quando executar a configuração a partir do CD. Pasta mais recente de um site instalado anteriormente utilizando o suporte de dados de linha de base de versão 1606.
>
> **SABranchOptions** não se aplicam a atualizações com script do System Center 2012 Configuration Manager e sempre resulta no ramo atual.

Para obter mais informações, consulte [utilizar uma linha de comando para instalar sites do System Center Configuration Manager](/sccm/core/servers/deploy/install/use-a-command-line-to-install-sites).


## <a name="install-a-new-site"></a>Instalar um novo site
Quando utiliza o 1606 da linha de base suporte de dados para instalar um novo site de um ramo, utilize o site de planeamento, preparação e procedimentos de instalação documentadas no [sites de instalar o System Center Configuration Manager](/sccm/core/servers/deploy/install/installing-sites) tópico com a adição das seguintes considerações para a configuração:

- Durante a configuração tem de escolher o ramo do Configuration Manager que pretende instalar e pode especificar os detalhes do contrato de Software Assurance.
- Todos os sites na mesma hierarquia tem de executar o ramo do mesmo. Não é suportado para ter uma hierarquia com uma combinação de LTSB e Current Branch em sites diferentes.
-   Nova instalação com script. Para obter mais informações, consulte "Novo convertidos em script opções de instalação" anteriormente no artigo.

## <a name="expand-a-stand-alone-primary-site"></a>Expandir um site primário autónomo
Pode expandir um site primário autónomo que executa o LTSB.  O processo é não diferente da utilizada para um site de Current Branch com uma advertência:

- Ao instalar o novo site de administração central tem de utilizar a configuração do suporte de dados do origem original que utilizou para instalar o site LTSB. Executar a configuração do CD. Pasta mais recente para este cenário não é suportada.

Para obter mais informações sobre a expansão de um site, consulte "Expandir um site primário autónomo" [instalar um site utilizando o Assistente de configuração](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).

## <a name="upgrade-from-system-center-2012-configuration-manager"></a>Atualização do System Center 2012 Configuration Manager
Quando atualizar a partir do System Center 2012 Configuration Manager, utilize o site planeamento, preparação e os procedimentos, conforme documentado no [atualizar para o System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) tópico, but com as seguintes alterações:

**Atualizar para o ramo atual:**
- Durante a configuração, tem de escolher o ramo atual, e pode especificar os detalhes do contrato de Software Assurance.
-   Nova instalação com script. Para obter mais informações, consulte "Novo convertidos em script opções de instalação" anteriormente no artigo.

**Atualizar para o LTSB:**  
- Passos adicionais para seguinte da lista de verificação de pré-atualização.
- Durante a configuração tem de escolher o LTSB e pode especificar os detalhes do contrato de Software Assurance.
- Só é possível atualizar um site que executa o System Center 2012 Configuration Manager com Service Pack 1, o System Center 2012 Configuration Manager com Service Pack 2, o System Center 2012 R2 Configuration Manager com Service Pack 1 ou o System Center 2012 R2 Configuration Gestor de sem nenhum service pack.

### <a name="in-place-upgrade-paths-for-the-1606-baseline-media"></a>Caminhos de atualização para o suporte de dados de linha de base de 1606 no local
Pode utilizar o suporte de dados de linha de base de 1606 para atualizar o seguinte procedimento para uma edição licenciada do System Center Configuration Manager:
- System Center 2012 R2 Configuration Manager sem Service Pack 1
- System Center 2012 R2 Configuration Manager sem service Pack (Isto requer a utilização de suporte de linha de base para versão 1606 de que foi rereleased no dia 15 de Dezembro de 2016.)
- System Center 2012 Configuration Manager sem Service Pack 2
- System Center 2012 Configuration Manager com Service Pack 1 (Isto requer a utilização do suporte de dados de linha de base para a versão 1606 foi rereleased no dia 15 de Dezembro de 2016.)


Também pode utilizar este suporte de dados para atualizar uma edição de avaliação não licenciado do ramo atual para uma versão totalmente licenciada do ramo atual.

Este suporte de dados não suporta a atualização do:
- Outras versões do System Center 2012 Configuration Manager.
- Do Configuration Manager 2007 ou anterior.
- Uma instalação de candidatos de lançamento do System Center Configuration Manager.

## <a name="about-the-cdlatest-folder-and-the-ltsb"></a>Sobre o CD. Pasta mais recente e a LTSB
Seguem-se as limitações utilizando o suporte de dados do Configuration Manager cria no CD. Pasta mais recente no servidor do site. Estes limites se aplicam a sites que executam o LTSB:

Suporte de dados no CD. Pasta mais recente é suportada para:
- Recuperação de sites.
- Manutenção do site.
- Instalar sites primários subordinados adicionais.

Suporte de dados no CD. Pasta mais recente não é suportada para:  
- Instalar um site de administração central como parte de um cenário de expansão do site.

Para obter mais informações, consulte [CD. Pasta mais recente](/sccm/core/servers/manage/the-cd.latest-folder).

## <a name="backup-recovery-and-site-maintenance-for-the-ltsb"></a>Cópia de segurança, recuperação e manutenção do site para o LTSB
Para criar cópias de segurança, recuperar ou executar a manutenção do site num site que executa o LTSB, utilize as orientações e procedimentos do [cópia de segurança e recuperação para o System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).  

Utilize o Gestor de configuração do programa de configuração do CD. Pasta mais recente da cópia de segurança do seu site LTSB.
