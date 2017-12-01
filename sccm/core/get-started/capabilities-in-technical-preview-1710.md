---
title: "Pré-visualização técnica 1710 | Microsoft Docs"
titleSuffix: Configuration Manager
description: "Saiba mais sobre as funcionalidades disponíveis na versão de pré-visualização técnica 1710 para o System Center Configuration Manager."
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4706a58-1f11-4eab-b1eb-3d1a0da02d0f
author: erikje
ms.author: erikje
manager: angrobe
ms.openlocfilehash: ed5f977df79114e1209cd3cc82d2e56e8e728c3d
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="capabilities-in-technical-preview-1710-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1710 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1710. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md) para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemas conhecidos neste Technical Preview:**
-   **Suporte para Windows 10, versão 1709 (também conhecido como a atualização de criadores de reversão)**.  A partir desta versão do Windows, o suporte de dados do Windows inclui várias edições. Quando configurar uma sequência de tarefas para utilizar um pacote de atualização do sistema operativo ou a imagem do sistema operativo, é necessário selecionar um [edição que é suportada para utilização pelo Configuration Manager](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).
-   **Falha de atualização para uma nova versão de pré-visualização quando tiver um servidor de site no modo passivo**. Quando executa uma versão de pré-visualização que tem um [servidor do site primário em modo passivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), tem de desinstalar o servidor do site de modo passivo antes de poder atualizar com êxito o site de pré-visualização para esta nova versão de pré-visualização. Pode reinstalar o servidor do site de modo passivo depois do seu site é concluída a atualização.

  Para desinstalar o servidor do site de modo passivo:
  1. Na consola, aceda a **administração** > **descrição geral** > **configuração do Site** > **servidores e funções de sistema de sites**e, em seguida, selecione o servidor de site de modo passivo.
  2. No **funções do sistema de sites** painel, clique direito no **servidor do Site** função e, em seguida, escolha **remover função**.
  3. Faça duplo clique no servidor do site de modo passivo e, em seguida, escolha **eliminar**.
  4. Depois de desinstala o servidor do site, no servidor do site primário Active Directory reinicie o serviço **CONFIGURATION_MANAGER_UPDATE**.

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-deploying-powershell-scripts-from-configuration-manager"></a>Melhoramentos para a implementação de Scripts do PowerShell do Configuration Manager
Com esta versão, os scripts do PowerShell que implementar suportam agora utilização das seguintes melhorias: 
- **Âmbitos de segurança**.  Scripts agora utilizam âmbitos de segurança para a criação de scripts de controlo e a execução. Isto é feito através da atribuição de etiquetas que representam os grupos de utilizadores. Para obter mais informações sobre como utilizar âmbitos de segurança, consulte [configurar a administração baseada em funções para o System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).
- **A monitorização em tempo real**. Ao monitorizar a execução de um script, está agora em tempo real como o script é executado.
- **Validação do parâmetro**. Cada parâmetro no script tem um **propriedades de parâmetro de Script** caixa de diálogo para adicionar a validação para este parâmetro. Depois de adicionar a validação, deve obter erros se está a introduzir um valor para um parâmetro que não cumprem a respectiva validação.

Implementação de scripts do PowerShell foi introduzida pela primeira vez no Technical Preview [técnico pré-visualização 1706](/sccm/core/get-started/capabilities-in-technical-preview-1706#create-and-run-powershell-scripts-from-the-configuration-manager-console). Melhoramentos adicionais foram fornecidos com [técnico pré-visualização 1707](/sccm/core/get-started/capabilities-in-technical-preview-1707#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) e, em seguida, [técnico pré-visualização 1708](/sccm/core/get-started/capabilities-in-technical-preview-1708#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager).


### <a name="try-it-out"></a>Experimente!

Experimentar a utilizar a funcionalidade de executar Scripts, consulte [criar e executadas scripts](../../apps/deploy-use/create-deploy-scripts.md).



## <a name="limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Limitar a telemetria melhorada do Windows 10 para apenas enviar dados relevantes para o estado de funcionamento de dispositivo de análise de Windows
<!-- 1356148 -->

Com esta versão, agora pode definir a recolha de dados de telemetria do Windows 10 para **avançado (limitado)**. Esta definição permite-lhe ganhar acionável conhecimentos aprofundados sobre os dispositivos no seu ambiente sem dispositivos que reportam a todos os dados no **avançado** nível de telemetria com o Windows 10 versão 1709 ou posterior.

O nível de telemetria avançado (limitado) inclui as métricas de nível básico, bem como um subconjunto dos dados recolhidos a partir de **avançado** nível relevante à análise do Windows. Para obter mais informações sobre níveis de telemetria, consulte [níveis de telemetria](https://docs.microsoft.com/windows/configuration/configure-windows-telemetry-in-your-organization#telemetry-levels).

### <a name="try-it-out"></a>Experimente!
Para configurar a coleção de telemetria do Windows 10 nos clientes, consulte [como configurar as definições de cliente](/sccm/core/clients/deploy/configure-client-settings). Abra o **serviços em nuvem** janela e definir a telemetria do Windows 10 para **avançado**.


## <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Centro de software já não distorts ícones maiores do que 250 x 250  
<!-- 1356194 -->

Com esta versão, o Centro de Software já não será distort ícones que são maiores do que 250 x 250. Centro de software efetuada essas ícones parecer blurry. Agora pode definir um ícone com um dimensões de pixel de até 512 x 512 e apresenta sem distortion.

### <a name="try-it-out"></a>Experimente!
Adicione um ícone para a sua aplicação no Centro de Software. Para experimentar consulte [criar aplicações](/sccm/apps/deploy-use/create-applications).


## <a name="check-compliance-from-software-center-for-co-managed-devices"></a>Verificação de conformidade do Centro de Software para dispositivos geridos conjuntamente
<!-- 1356374 -->
Nesta versão, os utilizadores podem utilizar o Centro de Software para verificar a compatibilidade dos dispositivos Windows 10 conjuntamente geridos mesmo quando o acesso condicional é gerido pelo Intune. Para obter mais informações, consulte [conjunta management para Windows 10 dispositivos](./capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices).


## <a name="support-for-exploit-guard"></a>Suporte para proteção de exploração
Esta versão adiciona suporte para o Windows Defender exploram Guard. Pode configurar e implementar políticas que gerir todos os quatro componentes de proteção Exploit. Estes componentes incluem:
-   Redução da superfície de ataque
-   Controlar o acesso da pasta
-   Proteção exploit
-   Proteção de rede

Dados de conformidade de implementação de política de proteção Exploit estão disponíveis a partir da consola do Configuration Manager.

Para obter mais informações sobre proteção Exploit e componentes específicos e regras, consulte [Windows Defender exploram Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard) na biblioteca de documentação do Windows.

### <a name="prerequisites"></a>Pré-requisitos
Dispositivos geridos tem de executar o Windows 10 1709 Outono criadores Update ou posterior e satisfazer os seguintes requisitos, consoante os componentes e as regras configuradas:

|Componente de proteção de exploração |Pré-requisitos adicionais|
|------------------------|------------------------|
| Redução da superfície de ataque  | Dispositivos têm de ter [proteção em tempo real do Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) ativada.  |
| Controlar o acesso da pasta  | Dispositivos têm de ter [proteção em tempo real do Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) ativada.   |
| Proteção exploit  | Nenhum  |
| Proteção de rede  |  Dispositivos têm de ter [proteção em tempo real do Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) ativada.  |

### <a name="create-an-exploit-guard-policy----1355468---"></a>Criar uma política de proteção Exploit<!--1355468 -->
1.  Na consola do Configuration Manager, vá para **ativos e compatibilidade** > **Endpoint Protection**e, em seguida, clique em **Windows Defender exploram Guard**.
2.  No **home page** separador o **criar** , clique em **criar política exploram**.
3.  Na página **Geral** do **Assistente de Criação de Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.
4.  Em seguida, selecione os componentes de proteção Exploit que pretende gerir com esta política. Para cada componente que selecionar, em seguida, pode configurar detalhes adicionais.
  - **Redução da superfície de ataque:** Configure a ameaça Office, scripts de ameaças e ameaças de e-mail que pretende bloquear ou de auditoria. Também pode excluir ficheiros ou pastas específicos desta regra.
  - **Controlar o acesso da pasta:** Configurar o bloqueio ou auditoria e, em seguida, adicionar as aplicações que podem ignorar esta política.  Também pode especificar as pastas adicionais que não estão protegidas por predefinição.
  - **Proteção exploit:**  Especifique um ficheiro XML que contém definições para mitigar exploits de processos do sistema e de aplicações. Pode exportar estas definições a partir da aplicação do Centro de segurança do Windows Defender num dispositivo Windows 10.
  - **Proteção de rede:** Definir a proteção de rede para bloquear ou auditoria acesso aos domínios suspeitos.
5.  Conclua o Assistente para criar uma política, que pode, posteriormente, implementar em dispositivos.

### <a name="deploy-an-exploit-guard-policy"></a>Implementar uma política de proteção Exploit     
Depois de criar políticas de proteção Exploit, utilize o assistente implementar política de proteção Exploit para implementá-las. Para tal, abra a consola do Configuration Manager para **ativos e compatibilidade** > **Endpoint Protection**e, em seguida, clique em **implementar política de proteção Exploit**.

## <a name="limited-support-for-cng-certificates"></a>Suporte limitado para certificados CNG
<!-- 1356191 -->
A partir desta versão, pode agora utilizar [Cryptography API: Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) modelos para os seguintes cenários de certificado:

- O registo de cliente e comunicação com um ponto de gestão HTTPS.   
- Distribuição e aplicação de implementação de software com um ponto de distribuição de HTTPS.   
- Implementação do sistema operativo.  
- Cliente SDK (com a atualização mais recente) e o ISV Proxy de mensagens.   
- Configuração do Gateway de gestão de nuvem.  

Para utilizar certificados CNG, a sua autoridade de certificação (AC) tem de fornecer modelos de certificado CNG máquinas de destino.  Detalhes de modelo variam de acordo com o cenário; No entanto, as seguintes propriedades são necessárias:

- **Compatibilidade** separador

    - **Autoridade de certificado** tem de ser Windows Server 2008 ou posterior. (Windows Server 2012 é recomendado.)

    - **Destinatário do certificado** tem de ser Windows Vista/Server 2008 ou posterior. (Windows 8/Windows Server 2012 é recomendado.)

- **Criptografia** separador

    - **Categoria de fornecedor** tem de ser **Key Storage Provider**.  (Obrigatório)

Para obter os melhores resultados, recomendamos a criação de nome do requerente de informações do Active Directory.  Utilize o nome de DNS para **formato de nome de requerente** e incluir o nome DNS no nome do requerente alternativo.  Caso contrário, terá de fornecer estas informações quando inscreve o dispositivo para o perfil de certificado.


## <a name="improved-descriptions-for-pending-computer-restarts-----1356283---"></a>Descrições melhoradas para pendentes reinícios de computador<!--1356283 -->
No [pré-visualização técnica 1708](/sccm/core/get-started/capabilities-in-technical-preview-1708#restart-computers-from-the-configuration-manager-console), adicionámos a capacidade para identificar dispositivos que estão pendente um reinício a partir da consola do Configuration Manager.

A partir desta pré-visualização técnica, a consola apresenta detalhes adicionais que fornecem informações sobre o processo ou a ação que está a pedir o reinício.

## <a name="device-guard-policy-changes----1355092---"></a>Alterações de política de proteção de dispositivos<!-- 1355092 -->
Com a compilação de pré-visualização técnica 1710, foram efetuadas as seguintes alterações de três em relação a políticas de proteção de dispositivos:

### <a name="device-guard-policies-renamed-to-windows-defender-application-control-policies"></a>Políticas de proteção de dispositivos mudadas para políticas de controlo de aplicação do Windows Defender
Políticas de proteção de dispositivos cujo nome foi mudadas para políticas de controlo de aplicação do Windows Defender. Sim, por exemplo, o **Assistente de política de criar Device Guard** tem agora o nome **Assistente de política de criar controlo de aplicação do Windows Defender**.

### <a name="restart-is-not-required-to-apply-policies"></a>Não é necessário reiniciar para aplicar políticas
A partir de reversão criadores atualização para Windows versão 1709, dispositivos com a nova versão do Windows não necessitam de um reinício para aplicar as políticas de controlo de aplicação do Windows Defender.

Reiniciar é a predefinição.

#### <a name="try-it-out"></a>Experimente!  

Se pretender desativar reinícios, siga estes passos:

1.  Abra o **criar Windows Defender aplicação de política de controlo** assistente.
2.  No **geral** página, desmarque a caixa de verificação **impor um reinício de dispositivos para que esta política pode ser imposta para todos os processos**.
3.  Clique em **seguinte** até que o assistente ser concluído.

Para versões antigas do Windows, ainda é forçado um reinício automatizado.

### <a name="automatically-run-software-trusted-by-the-intelligent-security-graph"></a>Executar automaticamente software considerado fidedigno pelo gráfico de segurança inteligente

Os administradores têm agora a opção para permitir que os dispositivos de baixo bloqueado executar software fidedigna com uma boa reputação conforme determinado pela gráfico segurança inteligente Microsoft (ISG). O ISG é composta por Windows Defender SmartScreen e outros serviços Microsoft.

Os dispositivos devem estar a executar o Windows Defender SmartScreen para o software para ser considerado confiável.

#### <a name="try-it-out"></a>Experimente!  

Para permitir que um dispositivo com o Windows Defender SmartScreen executar software fidedigna, siga estes passos:

1.  Abra o **assistente criar Windows Defender aplicação política de controlo**.
2.  No **as inclusões** página, marque a caixa de **autorizar software que é considerado fidedigno pelo gráfico de segurança inteligente**.
3.  No **fidedigna ficheiros ou pastas** caixa, adicione os ficheiros e pastas que pretende que sejam fidedignos.
4.  Clique em **seguinte** até que o assistente ser concluído.

## <a name="configure-and-deploy-windows-defender-application-guard-policies----1351960---"></a>Configurar e implementar políticas de proteção de aplicações do Windows Defender<!-- 1351960 -->

[Proteção de aplicações do Windows Defender](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) é uma nova funcionalidade do Windows que ajuda a proteger os seus utilizadores abrindo não fidedignos web sites num contentor isolado seguro que não pode ser acedido por outras partes do sistema operativo. Esta pré-visualização técnica, adicionámos suporte para configurar esta funcionalidade utilizando as definições de compatibilidade do Configuration Manager que configurar e, em seguida, implementar numa coleção. Esta funcionalidade será lançada em pré-visualização para a versão de 64 bits da atualização do Windows 10 Creator (nome: RS2). Para testar esta funcionalidade agora, tem de utilizar uma versão de pré-visualização desta atualização.

### <a name="before-you-start"></a>Antes de começar
Para criar e implementar políticas de proteção de aplicações do Windows Defender, os dispositivos Windows 10 nos quais implementou a política tem de ser configurados com uma política de isolamento de rede. Para obter mais informações, consulte o blogue post referenciado mais tarde. Esta capacidade funciona apenas com atuais compilações do Windows 10 internas. Para testar, os clientes tem de executar um recente Windows 10 Insider criar.

### <a name="try-it-out"></a>Experimente!

Para compreender as noções básicas sobre proteção de aplicações do Windows Defender, leia [a mensagem de blogue](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97).

Para criar uma política e, para procurar as definições disponíveis:
1. No **do Configuration Manager** consola, escolha **ativos e compatibilidade**.
2. No **ativos e compatibilidade** área de trabalho, escolha **descrição geral** > **Endpoint Protection** > **Guard de aplicação do Windows Defender**.
3. No **home page** separador o **criar** , clique em **criar Windows Defender Guard política aplicações**.
4. Utilizar a mensagem de blogue como uma referência, pode procurar e configurar as definições disponíveis para experimentar a funcionalidade.
5. Nesta versão, adicionámos a nova página de definição de rede para o assistente. Aqui, especifique a identidade empresarial e definir o limite da rede empresarial.

    > [!NOTE]
    > Windows 10 PCs armazenar apenas uma lista de isolamento de rede no cliente. Nesta versão, pode criar dois tipos diferentes de listas de isolamento de rede (uma da proteção de informações do Windows e outro da proteção de aplicações do Windows Defender) e implementá-las para o cliente. Se implementar ambas as políticas, estas listas de isolamento de rede tem de corresponder. Se implementar listas não correspondem ao cliente mesmo, a implementação irá falhar.

    Pode encontrar mais informações sobre como especificar definições de rede no [documentação de Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).

6. Quando tiver terminado, conclua o assistente e implementar a política para um ou mais dispositivos do Windows 10.

### <a name="further-reading"></a>Ler mais

Para ler mais informações sobre proteção de aplicações do Windows Defender, consulte [esta mensagem de blogue](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Além disso, para saber mais sobre o modo autónomo de proteção de aplicações do Windows Defender, consulte o artigo [esta mensagem de blogue](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).

## <a name="next-steps"></a>Passos Seguintes
Para obter informações sobre instalar ou atualizar o ramo de pré-visualização técnica, consulte [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
