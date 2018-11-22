---
title: 'Instalar um site utilizando o suporte de dados de linha de base de 1606 '
titleSuffix: Configuration Manager
description: Instalar ou atualizar para o LTSB para o System Center Configuration Manager.
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d6b957ebcc19dfe8c14dd781f71678db8e160af
ms.sourcegitcommit: 1a1bac2d5ee0f20ce565d29798ee4dd99aaca044
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/21/2018
ms.locfileid: "52281911"
---
# <a name="install-and-upgrade-with-the-version-1606-baseline-media-for-system-center-configuration-manager"></a>Instalar e atualizar com a versão 1606 suporte de dados de linha de base para o System Center Configuration Manager

*Aplica-se a:  O System Center Configuration Manager (ramo atual), (Long term Servicing Branch)*

Quando executar a configuração do suporte de dados de linha de base do versão 1606 para o Configuration Manager, pode instalar o term Servicing Branch ou um site do ramo atual do System Center Configuration Manager.

O suporte de dados de linha de base está disponível no DVD como parte do Microsoft System Center 2016 ou de versão do System Center Configuration Manager (ramo atual e longo prazo de manutenção ramo 1606). Para saber mais sobre o suporte de dados de linha de base, veja [versões de linha de base e atualização](../servers/manage/updates.md#bkmk_Baselines).


Quando utiliza o suporte de dados de linha de base do versão 1606, é o site instalar ou atualizar para:
- R *site do Current Branch* isto é equivalente a um site que foi a primeira instalado usando o suporte de dados de linha de base do 1511 e, em seguida, atualizado para a versão 1606, bem como a versão 1606 hotfix rollup - KB3186654.
-   Uma *LTSB site* isto é equivalente ao site do ramo atual que executa a versão 1606, bem como a versão 1606 kumulativní oprava hotfix - KB3186654. O suporte de dados de linha de base já inclui o rollup de correções.  No entanto, o LTSB não suporta todas as funcionalidades ou capacidades disponíveis com o ramo atual, conforme detalhado no [introdução para a longo prazo de manutenção ramo do System Center Configuration Manager](introduction-to-the-ltsb.md).

Se não estiver familiarizado com as ramificações diferentes do System Center Configuration Manager, veja [o ramo do Configuration Manager devo utilizar](which-branch-should-i-use.md).




## <a name="changes-to-setup-with-the-1606-baseline-media"></a>Alterações à configuração com suporte de dados de linha de base da versão 1606
O suporte de dados de linha de base de 1606 apresenta as seguintes alterações à configuração do Configuration Manager.

### <a name="branch-and-edition"></a>Ramo e edição
Quando executar a configuração, será apresentada uma página de licenciamento, onde pode selecionar o ramo do Configuration Manager que pretende instalar. Pode escolher o Current Branch ou LTSB como uma instalação licenciada, ou pode escolher uma edição de avaliação do ramo atual como uma instalação não licenciado.

Para obter mais informações, consulte [ramificações para o System Center Configuration Manager e de licenciamento](learn-more-editions.md).

### <a name="software-assurance-expiration"></a>Expiração do Software Assurance
Durante a configuração, tem a opção para introduzir os **data de expiração do Software Assurance** valor. Este é um valor opcional que pode ser especificado como um lembrete conveniente.

> [!NOTE]
> Microsoft não valida a data de expiração introduzir e não irá utilizar esta data para validação da licença.  Em vez disso, pode usá-lo como um lembrete da data de validade. Isto é útil porque o Configuration Manager periodicamente verifica a existência de novas atualizações de software disponibilizado online e o estado de licença do software assurance deve ser atual para ser elegível para utilizar estas atualizações adicionais.    

- Pode especificar o valor de data sobre o **chave de produto** página do Assistente de configuração ao executar a configuração da System Center Configuration Manager versão 1606 suporte de dados de linha de base.
- Também pode especificar esta data, selecionando **propriedades de definições de hierarquia** > **licenciamento** na consola do Configuration Manager.

Para obter mais informações, consulte "Contratos de Software Assurance" no [ramificações para o System Center Configuration Manager e de licenciamento](learn-more-editions.md).


### <a name="additional-pre-upgrade-configurations"></a>Configurações de pré-atualização adicionais
Antes de iniciar uma atualização do System Center 2012 Configuration Manager para o LTSB, tem de executar os seguintes passos adicionais como parte da lista de verificação de pré-atualização.  
Desinstale as funções de sistema de sites que não suporta o LTSB:
- Ponto de sincronização do Asset Intelligence
- Conector do Microsoft Intune
- Pontos de distribuição baseados na nuvem

Para obter mais informações, consulte [atualizar para o System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).


### <a name="new-scripted-installation-options"></a>Novas opções de instalação com script
O suporte de dados de linha de base do versão 1606 suporta uma nova chave de ficheiro de script automático para instalações com script de um novo site de nível superior. Isto aplica-se para instalar um novo site primário autónomo ou a adição de um site de administração central como parte de um cenário de expansão do site.

Quando utilizar um script automático para instalar um ramo licenciado, tem de adicionar a secção seguinte, nomes de chaves e valores para a secção de opções do seu script. Não precisa de utilizar estes valores para a instalação de uma edição de avaliação do ramo atual do script:  

 **SABranchOptions**
-   **Nome da chave: SAActive**
  - Valores: 0 ou 1.  
  - Detalhes:  0 instala uma edição de avaliação não licenciado do Current Branch e 1 instala uma edição licenciada.   

- **CurrentBranch**
  - Valores: 0 ou 1.  
  - Detalhes:  0 instala term Servicing Branch e 1 é instalado o ramo atual.  

Por exemplo, para instalar uma edição licenciada do ramo atual, que usaria:

  **Nome da chave: SABranchOptions**
   -    **SAActive = 1**
   - **CurrentBranch = 1**


> [!IMPORTANT]  
> **SABranchOptions** só funciona com a configuração do suporte de dados de linha de base. Não é aplicável quando executar a configuração do CD. Pasta mais recente de um site tiver instalado anteriormente com suportes de dados de linha de base da versão 1606.
>
> **SABranchOptions** não se aplicam a atualizações com scripts do System Center 2012 Configuration Manager e sempre resulta no ramo atual.

Para obter mais informações, consulte [utilizar uma linha de comando para instalar sites do System Center Configuration Manager](/sccm/core/servers/deploy/install/use-a-command-line-to-install-sites).


## <a name="install-a-new-site"></a>Instalar um novo site
Quando utilizar a versão 1606 da linha de base de dados para instalar um novo site de qualquer uma das filiais, utilize o site de planeamento, preparação, e procedimentos de instalação documentados no [sites de instalação do System Center Configuration Manager](/sccm/core/servers/deploy/install/installing-sites) tópico com o adição as seguintes considerações para a configuração:

- Durante a configuração tem de escolher o ramo do Configuration Manager que pretende instalar e especifique os detalhes para o seu contrato de Software Assurance.
- Todos os sites na mesma hierarquia tem de executar o ramo do mesmo. Não é suportado para ter uma hierarquia com uma combinação de LTSB e o ramo atual em sites diferentes.
-   Nova instalação com script. Para obter mais informações, consulte "New convertidos em script opções de instalação" no início deste artigo.

## <a name="expand-a-stand-alone-primary-site"></a>Expandir um site primário autónomo
Pode expandir um site primário autónomo que executa o LTSB.  O processo não é diferente do que a usada para um site do ramo atual com uma limitação:

- Ao instalar o novo site de administração central tem de utilizar a configuração da mídia de origem original que utilizou para instalar o site LTSB. Executar a configuração do CD. Pasta mais recente para este cenário não é suportada.

Para obter mais informações sobre a expansão de um site, consulte "Expandir um site primário autónomo" na [instalar um site utilizando o Assistente de configuração](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).

## <a name="upgrade-from-system-center-2012-configuration-manager"></a>Atualização do System Center 2012 Configuration Manager
Ao atualizar do System Center 2012 Configuration Manager, utilize o planejamento do site, preparação e procedimentos, conforme documentado no [atualizar para o System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) tópico, mas com as seguintes alterações:

**Atualizar para o ramo atual:**
- Durante a configuração, tem de escolher o ramo atual e pode especificar os detalhes para o seu contrato de Software Assurance.
-   Nova instalação com script. Para obter mais informações, consulte "New convertidos em script opções de instalação" no início deste artigo.

**Atualizar para o LTSB:**  
- Passos adicionais para seguinte da lista de verificação de pré-atualização.
- Durante a configuração tem de escolher o LTSB e pode especificar os detalhes para o seu contrato de Software Assurance.
- Só é possível atualizar um site com o System Center 2012 Configuration Manager com Service Pack 1, o System Center 2012 Configuration Manager com Service Pack 2, o System Center 2012 R2 Configuration Manager com Service Pack 1 ou o System Center 2012 R2 Configuration Manager sem service pack.

### <a name="in-place-upgrade-paths-for-the-1606-baseline-media"></a>Caminhos de atualização para o suporte de dados de linha de base de 1606 in-loco
Pode utilizar o suporte de dados de linha de base de 1606 para atualizar os seguintes para uma edição licenciada do System Center Configuration Manager:
- System Center 2012 R2 Configuration Manager com Service Pack 1
- System Center 2012 R2 Configuration Manager sem service Pack (requer o uso do suporte de linha de base para a versão 1606 que foi relançadas de 15 de Dezembro de 2016.)
- System Center 2012 Configuration Manager com Service Pack 2
- System Center 2012 Configuration Manager com Service Pack 1 (Isto requer a utilização do suporte de dados de linha de base para a versão 1606, que foi relançada de 15 de Dezembro de 2016).


Também pode utilizar este suporte de dados para atualizar uma edição de avaliação não licenciado do ramo atual para uma versão totalmente licenciada do ramo atual.

Este suporte de dados não suporta a atualização do:
- Outras versões do System Center 2012 Configuration Manager.
- Configuration Manager 2007 ou anterior.
- Uma instalação de Release candidate do lançamento do System Center Configuration Manager.

## <a name="about-the-cdlatest-folder-and-the-ltsb"></a>Sobre o CD. Pasta mais recente e o LTSB
Seguem-se limitações sobre como utilizar o suporte de dados do Configuration Manager cria no CD. Pasta mais recente no servidor do site. Estes limites aplicam-se para sites que executam o LTSB:

Suporte de dados no CD. Pasta mais recente é suportada para:
- Recuperação de sites.
- Manutenção do site.
- Instalar sites primários subordinados adicionais.

Suporte de dados no CD. Pasta mais recente não é suportada para:  
- A instalar um site de administração central como parte de um cenário de expansão do site.

Para obter mais informações, consulte [o CD. Pasta mais recente](/sccm/core/servers/manage/the-cd.latest-folder).

## <a name="backup-recovery-and-site-maintenance-for-the-ltsb"></a>Cópia de segurança, recuperação e manutenção do site para o LTSB
Para criar cópias de segurança, recuperar ou executar a manutenção do site num site que executa o LTSB, utilize as orientações e procedimentos [cópia de segurança e recuperação para o System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).  

Utilize o Gestor de configuração de configuração a partir do CD. Pasta mais recente da cópia de segurança do seu site LTSB.
