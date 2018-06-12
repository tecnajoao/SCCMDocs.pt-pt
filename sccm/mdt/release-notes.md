---
title: Notas de versão do MDT
description: Compreenda as plataformas suportadas, pré-requisitos e limitações da Microsoft Deployment Toolkit.
ms.date: 06/04/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 6e32ce6d-585d-4801-a345-ff0f6f2d90ad
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7cb287a17322af8069708268a18d638bd04dddcf
ms.sourcegitcommit: 10b3a571e2a822bbd7b58a25840ee1e6f703a7a2
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34814285"
---
# <a name="microsoft-deployment-toolkit-release-notes"></a>Notas de versão do Microsoft Deployment Toolkit  

Este artigo fornece detalhes sobre a versão mais recente do Microsoft Deployment Toolkit (MDT). Estes detalhes incluem as plataformas suportadas, pré-requisitos e quaisquer limitações. Pressupõe familiaridade com conceitos de versão do MDT, funcionalidades e capacidades.



## <a name="latest-release"></a>Versão mais recente

**MDT criar 8450** é a versão mais recente disponível no [Microsoft Download Center](https://aka.ms/mdtdownload). 

Esta atualização começa suporte para o Windows Assessment and Deployment Kit (ADK) para Windows 10, versão 1709. 

***Atualização***: A partir de Maio de 2018, este compilação também suporta a versão 1803 do Windows 10.

Para obter mais informações, consulte o [plataformas suportadas](#supported-platforms) secção.


### <a name="significant-changes"></a>Alterações significativas
Eis um resumo das alterações significativas neste compilação do MDT.

#### <a name="supported-configuration-updates"></a>Suportado atualizações de configuração
- Windows ADK para Windows 10, versão 1709
- Windows 10, versão 1709
- Versão 1710 do Configuration Manager

#### <a name="quality-updates"></a>Qualidade de atualizações
Seguem-se os títulos de correções nesta versão:
- Dependências de aplicações de Sideload Win10 e a licença não instalado
- Sequência de tarefas CaptureOnly não permite capturar uma imagem
- Erro recebido quando iniciar uma sequência de tarefas do MDT: Valor inválido de DeploymentType "" especificado. A implementação não será possível proceder
- ZTIMoveStateStore procura para a pasta de arquivo de estado na localização errada fazendo com que a falhar movê-lo
- XML contém um erro de digitação simple que causou o comportamento indesejável
- Instalar funções e funcionalidades não funciona para a funcionalidade de consola de gestão do IIS do Windows Server 2016
- Navegar para imagens de SO na sequência de tarefas de atualização não funciona ao utilizar pastas
- Ferramenta de MDT incorretamente Aprovisiona o TPM para um Estado de funcionalidade Reduced. Para obter mais informações, consulte [KB 4018657](https://support.microsoft.com/help/4018657/tpm-is-in-reduced-functionality-mode-after-successful-deployment-of-wi).
- As atualizações à ZTIGather chassis escrever a lógica de deteção
- Atualização de SO de passo deixa atrás SetupComplete.cmd, interrompendo as implementações futuras
- Windows 10 ADK 1607 e a UEFI posterior de arranque problema algum hardware
- Inclui os binários de sequência de tarefas do Configuration Manager atualizado



## <a name="supported-platforms"></a>Plataformas suportadas

Versões do MDT já não são etiquetadas com a versão de ano ou atualização. Para melhor alinhar com as sucursais atuais do Windows 10 e o Configuration Manager e para simplificar a imagem corporativa e processo de versão, agora é simplesmente **Microsoft Deployment Toolkit**. O número de compilação é utilizado para distinguir cada versão. Por exemplo, a compilação mais recente disponível para transferência é 8450.

Ao contrário do Configuration Manager com uma agenda predeterminada versão, MDT apenas versões conforme necessário para suportar novas versões do Windows 10, o Windows ADK ou ramo atual do Configuration Manager. Quaisquer problemas conhecidos com estes componentes serão documentados neste artigo, conforme necessário.

São suportadas as seguintes versões de SO para a implementação com o MDT:
- Windows 10, versão 1803
- Windows 10, versão 1709
- Outros [versões](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet) do Windows 10
- Windows 8,1
- Windows 7
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2



## <a name="prerequisites"></a>Pré-requisitos

MDT requer os seguintes componentes que estão incluídos no Windows:
- Microsoft .NET Framework 4.0
- O Windows PowerShell versão 3.0

Utilizar a versão mais recente [Windows ADK para Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install). 

> [!Note]  
> Windows recomenda utilizar o Windows ADK que corresponde à versão do Windows estiver a implementar. Por exemplo, utilizar o Windows ADK para Windows 10 versão 1703 quando implementar o Windows 10 versão 1703. Para obter mais informações sobre o suporte de componentes do Windows ADK, consulte [DISM plataformas suportadas](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) e [requisitos USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1).

Quando a integração do MDT com o Configuration Manager para cenários ZTI e UDI, utilize a versão mais recente do ramo atual do Configuration Manager.



## <a name="upgrading-mdt"></a>Atualizar o MDT

O processo de instalação do MDT remove quaisquer instâncias existentes do MDT instalado no mesmo computador. Partilhas de implementação, pontos de distribuição e as bases de dados existentes são preservados durante este processo. Tem de ser atualizados quando a instalação estiver concluída.

A versão atual do MDT suporta as seguintes versões do MDT a atualizar:
- MDT compilação 8443

> [!Tip]  
> Crie uma cópia de segurança da infraestrutura existente do MDT antes de tentar uma atualização.

### <a name="lti"></a>LTI
Após a instalação do MDT, atualizar uma partilha de implementação existente executando o **aberto Assistente de partilha de implementação** partir do nó de partilhas de implementação no Deployment Workbench. Especifique o caminho para o diretório de partilha de implementação existente e, em seguida, selecione o **atualizar** caixa de verificação. Este processo também atualiza as partilhas de implementação de rede existente e partilhas de implementação de suportes de dados, pelo que estas partilhas devem ser acessíveis. Não execute esta atualização ao efetuar implementações, porque os ficheiros em utilização podem causar problemas a atualização.

### <a name="zti"></a>ZTI
Existentes sequências de tarefas de MDT presente no Configuration Manager não são modificadas durante o processo de instalação do MDT. Eles devem continuar a funcionar sem qualquer problema. Não foi fornecido nenhum mecanismo para atualizar estas sequências de tarefas. Se pretender utilizar qualquer uma das novas funcionalidades do MDT, crie novos sequências de tarefas MDT integrado no Configuration Manager.

Quando o processo de atualização está concluído:  

- Execute o **configurar Assistente de integração do ConfigMgr** após a atualização. Regista os componentes novos e instala os modelos de sequência de tarefas ZTI atualizados.  

- Crie um novo **Microsoft implementação Toolkit ficheiros** pacote para qualquer nova ZTI as sequências de tarefas que cria. Pode utilizar o pacote de ficheiros de Toolkit do Microsoft implementação existente para sequências de tarefas ZTI criadas antes da atualização, mas tem de criar um novo pacote de ficheiros do Microsoft implementação Toolkit para sequências de tarefas do novo ZTI.



<!--
## Known issues
-->



## <a name="frequently-asked-questions"></a>Perguntas mais frequentes

#### <a name="whats-the-mdt-support-life-cycle"></a>O que é o ciclo de vida de suporte do MDT?  
Para obter mais informações, consulte [ciclo de vida de suporte do Microsoft Deployment Toolkit](https://support.microsoft.com/help/2872000/microsoft-deployment-toolkit-support-life-cycle).

#### <a name="is-this-release-only-supported-with-windows-10-windows-adk-or-configuration-manager-version-x"></a>Esta versão do só é suportada com a versão do Windows 10, o Windows ADK ou o Configuration Manager *X*?
Testamos principalmente este compilação do MDT com a configuração listada acima. Exceto se existem quaisquer problemas conhecidos explícitos, nada fora configuração acima tem uma elevada probabilidade de continuam a funcionar. O mileage pode variar devido às que ainda não testámos explicitamente outras combinações.

#### <a name="how-do-i-get-help-with-mdt"></a>Como posso obter ajuda com o MDT?
Utilize um dos seguintes métodos para obter ajuda com o MDT (por ordem prioritários):

1. Publicar o [fórum do MDT](https://social.technet.microsoft.com/Forums/en/home?forum=mdt). Most e outros utilizadores na Comunidade veja e respondem a mensagens não existe. Provavelmente, a forma mais eficiente para obter ajuda.
2. Contacte o suporte da Microsoft. Obter um incidente de suporte aberta e obter ajuda profissionais.
3. Se consistentemente pode reproduzir um problema e considerar é um erro de produto, ficheiros no Windows 10 [comentários Hub](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app). A equipa de produto investiga tudo o que é comunicada. Utilize o **gestão empresarial** categoria e **implementação do SO** subcategoria quando a apresentação de comentários. Esta categorização ajuda a classificar e encaminhar os seus comentários para a equipa do MDT.
     - O Hub de comentários também pode ser utilizado para submeter sugestões (design pedidos de alteração ou DCRs) no produto.
     - Se anteriormente registada comentários através do Connect, não precisa de refile no Hub comentários.