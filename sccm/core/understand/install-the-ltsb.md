---
title: Instalar um site utilizando o suporte de dados de linha de base 1606 | Documentos do Microsoft
description: Instalar ou atualizar para o LTSB para o System Center Configuration Manager.
ms.custom: na
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 31819a1df4e63e1114682490a9b3c3b4e5c99cfa
ms.openlocfilehash: 39653604ba5fd8e1fe9dd4d42889221d983f9bec
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="install-and-upgrade-with-the-version-1606-baseline-media-for-system-center-configuration-manager"></a>Instalar e atualizar com a versão de suportes de dados do 1606 plano base para o System Center Configuration Manager

*Aplica-se a:  System Center Configuration Manager (ramo atual), (ramo longa duração de manutenção)*

Quando executar a configuração a partir do suporte de dados de linha de base de 1606 de versão para o Configuration Manager, pode instalar o ramo de manutenção de longa duração ou um site secundário atual do System Center Configuration Manager.

O suporte de dados de linha de base está disponível no DVD como parte do Microsoft System Center 2016 ou da versão do System Center Configuration Manager (ramo atual e longo prazo manutenção ramo 1606). Para obter informações sobre suportes de dados do plano base, consulte o artigo [versões de linha de base e atualização](/sccm/core/servers/manage/updates#baseline-and-udpate-versions).


Ao utilizar o suporte de dados de linha de base de 1606 versão, é o site que instalar ou atualizar para:
- Um *site atual ramo* ou seja equivalente a um site que foi a primeira instalados utilizando o suporte de dados de linha de base 1511 e, em seguida, atualizar para a versão 1606 plus a 1606 correção agregação - KB3186654.
-    Um *LTSB site* ou seja equivalente para o site secundário atual que executa o rollup de correção versão 1606 plus a 1606 - KB3186654. O suporte de dados de linha de base já inclui o rollup de correção.  Mas, o LTSB não suporta todas as funcionalidades ou capacidades que estão disponíveis com o ramo atual, conforme especificado nas [introdução para a longo prazo manutenção ramo do System Center Configuration Manager](introduction-to-the-ltsb.md).

Se não estiver familiarizado com os ramos diferentes do System Center Configuration Manager, consulte o artigo [o ramo do Configuration Manager devo utilizar](which-branch-should-i-use.md).




## <a name="changes-to-setup-with-the-1606-baseline-media"></a>Alterações à configuração com o suporte de dados de linha de base 1606
O suporte de dados de linha de base 1606 apresenta as seguintes alterações à configuração do Configuration Manager.

### <a name="branch-and-edition"></a>Ramo e edição
Quando executar a configuração, é agora apresentada com uma página de licenciamento onde pode selecionar o ramo do Configuration Manager que pretende instalar. Pode escolher o ramo atual ou LTSB como uma instalação licenciada, ou pode escolher uma edição de avaliação do mesmo atual como uma instalação não licenciado.

Para obter mais informações, consulte o artigo [licenciamento e ramos para o System Center Configuration Manager](learn-more-editions.md).

### <a name="software-assurance-expiration"></a>Expiração do Software Assurance
Durante a configuração, tem a opção para introduzir o **data de expiração de Software Assurance** valor. Este é um valor opcional que pode ser especificado como um lembrete conveniente.

> [!NOTE]
> Microsoft não valida a data de expiração introduza e não irá utilizar esta data para validação de licença.  Em vez disso, pode utilizá-lo como um lembrete da data de validade. Isto é útil porque do Configuration Manager periodicamente verifica a existência de novas atualizações de software oferecidas online e o estado da licença de software assurance deve ser atual para ser elegível para utilizar estas atualizações adicionais.    

- Pode especificar o valor de data no **chave de produto** página no Assistente de configuração ao executar a configuração da versão System Center Configuration Manager 1606 suportes de dados de linha de base.
- Também pode especificar esta data selecionando **propriedades das definições de hierarquia** > **licenciamento** na consola do Configuration Manager.

Para obter mais informações, consulte "Contratos de Software Assurance" em [licenciamento e ramos para o System Center Configuration Manager](learn-more-editions.md).


### <a name="additional-pre-upgrade-configurations"></a>Configurações de pré-atualização adicionais
Antes de iniciar uma atualização do System Center 2012 Configuration Manager para o LTSB, tem de efetuar os seguintes passos adicionais como parte da lista de verificação anterior à atualização.  
Desinstale as funções de sistema de sites que o LTSB não suporta:
- Ponto de sincronização do Asset Intelligence
- Conector do Microsoft Intune
- Pontos de distribuição baseados na nuvem

Para obter mais informações, consulte o artigo [atualizar para o System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).


### <a name="new-scripted-installation-options"></a>Novas opções de instalação com script
O suporte de dados de linha de base de 1606 versão suporta uma nova chave de ficheiro de script automático para instalações com scripts de um novo site de nível superior. Isto aplica-se para instalar um novo site primário autónomo ou a adição de um site de administração central como parte de um cenário de expansão do site.

Quando utilizar um script automático para instalar um ramo licenciado, tem de adicionar a secção seguinte, os nomes de chaves e valores para a secção de opções do script. Não precisa de utilizar estes valores para a instalação de uma edição de avaliação do mesmo atual do script:  

 **SABranchOptions**
-     **Nome da chave: SAActive**
  - Valores: 0 ou 1.  
  - Detalhes:  0 instala uma edição de avaliação não licenciado do ramo atual e, 1 instala uma edição licenciada.   

- **CurrentBranch**
  - Valores: 0 ou 1.  
  - Detalhes:  0 instala o ramo de manutenção de longo prazo e, 1 instala o ramo atual.  

Por exemplo, para instalar uma edição licenciada do ramo atual utilize:

  **Nome da chave: SABranchOptions**
   -    **SAActive = 1**
   - **CurrentBranch = 1**


> [!IMPORTANT]  
> **SABranchOptions** só funciona com a configuração do suporte de dados de linha de base. Não é aplicável ao executar a configuração a partir do CD. Pasta mais recente de um site instalado anteriormente utilizando o suporte de dados de linha de base de versão 1606.
>
> **SABranchOptions** não é aplicável a atualização com script a partir do System Center 2012 Configuration Manager e conserva sempre o ramo atual.

Para obter mais informações, consulte o artigo [utilizar uma linha de comandos para instalar o System Center Configuration Manager sites](/sccm/core/servers/deploy/install/use-a-command-line-to-install-sites).


## <a name="install-a-new-site"></a>Instalar um novo site
Quando utiliza o 1606 plano base suporte de dados para instalar um novo site de um ramo, utilize o site de planeamento, durante a preparação, e procedimentos de instalação documentados na secção de [sites de instalar o System Center Configuration Manager](/sccm/core/servers/deploy/install/installing-sites) tópico com a adição das seguintes considerações para a configuração:

- Durante a configuração tem de escolher o ramo do Configuration Manager que pretende instalar e pode especificar os detalhes para o seu contrato do Software Assurance.
- Todos os sites na mesma hierarquia tem de executar a mesma sucursal. Não é suportada para ter uma hierarquia com uma mistura de LTSB e ramo atual em sites diferentes.
-    Nova instalação com script. Para obter mais informações, consulte "Novo convertidos em script opções de instalação" anteriormente no artigo.

## <a name="expand-a-stand-alone-primary-site"></a>Expandir um site primário autónomo
Pode expandir um site primário autónomo que executa o LTSB.  O processo é não diferente da utilizada para um site secundário atual com um caveat:

- Ao instalar o novo site de administração central tem de utilizar o programa de configuração a partir do suporte de dados do origem original que utilizou para instalar o site LTSB. Executar a configuração a partir do CD. Pasta mais recente para este cenário não é suportada.

Para obter mais informações sobre a expansão de um site, consulte "Expandir um site primário autónomo" em [instalar um site utilizando o Assistente de configuração](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).

## <a name="upgrade-from-system-center-2012-configuration-manager"></a>Atualizar a partir do System Center 2012 Configuration Manager
Ao atualizar a partir do System Center 2012 Configuration Manager, utilizar o planeamento de sites, preparação e procedimentos, conforme documentado no [atualizar para o System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) tópico, mas com as seguintes alterações:

**Atualizar para o ramo atual:**
- Durante a configuração, tem de escolher o ramo atual e pode especificar os detalhes para o seu contrato do Software Assurance.
-     Nova instalação com script. Para obter mais informações, consulte "Novo convertidos em script opções de instalação" anteriormente no artigo.

**Atualizar para o LTSB:**  
- Passos adicionais para a lista de verificação de pré-atualização seguinte.
- Durante a configuração tem de escolher o LTSB e pode especificar os detalhes para o seu contrato do Software Assurance.
- Só é possível atualizar um site que executa o System Center 2012 Configuration Manager com Service Pack 2 ou System Center 2012 R2 Configuration Manager com Service Pack 1.

### <a name="in-place-upgrade-paths-for-the-1606-baseline-media"></a>Caminhos de atualização para o suporte de dados de linha de base 1606 direta
Pode utilizar o suporte de dados de linha de base 1606 para atualizar o seguinte procedimento para uma edição licenciada do System Center Configuration Manager:
- System Center 2012 Configuration Manager sem Service Pack 2.
- System Center 2012 R2 Configuration Manager sem Service Pack 1.

Também pode utilizar este suporte para atualizar uma edição de avaliação não licenciado do ramo atual para uma versão totalmente licenciada do mesmo atual.

Este suporte não suporta a atualização:
- Outras versões do System Center 2012 Configuration Manager.
- Configuration Manager 2007 ou anterior.
- Uma instalação de candidatos de versão do System Center Configuration Manager.

## <a name="about-the-cdlatest-folder-and-the-ltsb"></a>Sobre o CD. Pasta mais recente e a LTSB
Seguem-se algumas limitações sobre utilizando o suporte de dados do Configuration Manager cria no CD. Pasta mais recente no servidor do site. Estes limites aplicam-se aos sites que executam o LTSB:

Suporte de dados no CD. Pasta mais recente é suportada para:
- Recuperação de site.
- Manutenção do site.
- Instalar sites primários subordinados adicionais.

Suporte de dados no CD. Pasta mais recente não é suportada para:  
- Instalação de um site de administração central como parte de um cenário de expansão do site.

Para obter mais informações, consulte o artigo [CD. Pasta mais recente](/sccm/core/servers/manage/the-cd.latest-folder).

## <a name="backup-recovery-and-site-maintenance-for-the-ltsb"></a>Cópia de segurança, recuperação e manutenção do site para o LTSB
Para criar cópias de segurança, recuperar ou executar a manutenção do site num site que executa o LTSB, utilize as orientações e procedimentos do [cópia de segurança e recuperação para o System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).  

Utilize o Gestor de configuração do programa de configuração a partir do CD. Pasta mais recente da cópia de segurança do seu site LTSB.

