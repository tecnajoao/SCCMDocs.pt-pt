---
title: Pré-visualização técnica 1710 | Documentos da Microsoft
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis na versão 1710 do Technical Preview do System Center Configuration Manager.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f4706a58-1f11-4eab-b1eb-3d1a0da02d0f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e8f7a8fbdbd52a8f872583cf2237a06ee8c1420e
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53414723"
---
# <a name="capabilities-in-technical-preview-1710-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1710 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1710. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md) para se familiarizar com os requisitos gerais e limitações para a utilização de um técnico de pré-visualização, como atualizar entre as versões e como fornecer comentários sobre os recursos de uma technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemas conhecidos neste Technical Preview:**
- **Suporte para Windows 10, versão 1709 (também conhecido como o Fall Creators Update)**.  Começando com esta versão do Windows, o suporte de dados do Windows inclui várias edições. Ao configurar uma sequência de tarefas para utilizar um pacote de atualização do sistema operativo ou a imagem do sistema operativo, certifique-se de que selecione um [edition que é suportada para utilização pelo Configuration Manager](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).
- **Atualização para uma nova versão de pré-visualização falha quando tem um servidor de site em modo passivo**. Quando executa uma versão de pré-visualização que tem um [servidor do site primário em modo passivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), tem de desinstalar o servidor do site de modo passivo antes de poder atualizar com êxito o site de pré-visualização para esta nova versão de pré-visualização. Pode reinstalar o servidor do site de modo passivo após a atualização do seu site estiver concluída.

  Para desinstalar o servidor do site de modo passivo:
  1. Na consola, aceda a **Administration** > **descrição geral** > **configuração do Site** > **servidores e sites Funções do sistema**e, em seguida, selecione o servidor de site de modo passivo.
  2. Na **funções do sistema de sites** painel, clique direito na **servidor do Site** função e, em seguida, escolha **remover função**.
  3. Faça duplo clique no servidor do site de modo passivo e, em seguida, escolha **eliminar**.
  4. Depois de desinstala o servidor do site, no servidor do site primário active reinicie o serviço **CONFIGURATION_MANAGER_UPDATE**.

**Seguem-se os novos recursos, que pode experimentar com esta versão.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-deploying-powershell-scripts-from-configuration-manager"></a>Melhorias para a implementação de Scripts do PowerShell do Configuration Manager
Com esta versão, scripts do PowerShell que implementa suportam agora a utilização dos seguintes melhoramentos: 
- **Âmbitos de segurança**.  Scripts agora utilizam âmbitos de segurança para os scripts de controle de criação e execução. Isso é feito através da atribuição de etiquetas que representam os grupos de utilizadores. Para obter mais informações sobre como utilizar âmbitos de segurança, consulte [configurar a administração baseada em funções para o System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).
- **Monitorização em tempo real**. Ao monitorizar a execução de um script, está agora em tempo real à medida que o script é executado.
- **Validação de parâmetro**. Cada parâmetro no script tem um **propriedades do parâmetro de Script** caixa de diálogo para adicionar validação para esse parâmetro. Depois de adicionar validação, obterá erros se estiver participando um valor para um parâmetro que não possui a respectiva validação.

Implementação de scripts do PowerShell foi introduzido pela primeira vez no Technical Preview [Tech Preview 1706](/sccm/core/get-started/capabilities-in-technical-preview-1706#create-and-run-powershell-scripts-from-the-configuration-manager-console). Aprimoramentos adicionais foram entregues com [versão 1707 de pré-visualização do Tech](/sccm/core/get-started/capabilities-in-technical-preview-1707#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) e, em seguida [Tech Preview 1708](/sccm/core/get-started/capabilities-in-technical-preview-1708#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager).


### <a name="try-it-out"></a>Experimente!

Para experimentar o usando o recurso de executar Scripts, consulte [criar e executar scripts](../../apps/deploy-use/create-deploy-scripts.md).



## <a name="limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Limitar telemetria avançada do Windows 10 para enviar apenas dados relevantes para o estado de funcionamento de dispositivos do Windows Analytics
<!-- 1356148 -->

Com esta versão, agora pode definir a recolha de dados de telemetria do Windows 10 para **avançado (limitado)**. Esta definição permite-lhe obter informações acionáveis sobre dispositivos no seu ambiente sem dispositivos que reportem todos os dados no **avançado** nível de telemetria com o Windows 10 versão 1709 ou posterior.

O nível de telemetria avançado (limitado) inclui métricas a partir do nível básico, bem como um subconjunto dos dados recolhidos a partir da **avançado** nível relevante para o Windows Analytics. Para obter mais informações sobre os níveis de telemetria, consulte [níveis de telemetria](https://docs.microsoft.com/windows/configuration/configure-windows-telemetry-in-your-organization#telemetry-levels).

### <a name="try-it-out"></a>Experimente!
Para configurar a recolha de telemetria do Windows 10 nos clientes, consulte [como configurar as definições de cliente](/sccm/core/clients/deploy/configure-client-settings). Abra o **serviços Cloud** janela e defina a telemetria do Windows 10 como **avançado**.


## <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Centro de software já não distorçam ícones maiores do que 250 x 250  
<!-- 1356194 -->

Com esta versão, o Centro de Software já não será distorcer os ícones que são maiores do que 250 x 250. Centro de software efetuada esses ícones parecer indistinta. Agora pode definir um ícone com um dimensões de pixel de até 512 x 512 e apresenta ao máximo sem distorção.

### <a name="try-it-out"></a>Experimente!
Adicione um ícone para a sua aplicação no Centro de Software. Para experimentá-lo a ver [criem aplicativos](/sccm/apps/deploy-use/create-applications).


## <a name="check-compliance-from-software-center-for-co-managed-devices"></a>Verificar a conformidade do Centro de Software para dispositivos cogeridos
<!-- 1356374 --> Nesta versão, os utilizadores podem utilizar o Centro de Software para verificar a conformidade dos respetivos dispositivos Windows 10 cogeridos, mesmo quando o acesso condicional é gerido pelo Intune. Para obter detalhes, consulte [cogestão para dispositivos Windows 10](./capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices).


## <a name="support-for-exploit-guard"></a>Suporte do Exploit Guard
Esta versão adiciona suporte para o Windows Defender Exploit Guard. Pode configurar e implementar políticas que gerem a todos os quatro componentes do Exploit Guard. Estes componentes incluem:
-   Redução da Superfície de Ataque
-   Acesso a pastas controladas
-   Proteção de exploração
-   Proteção de rede

Dados de conformidade para a implementação de política do Exploit Guard estão disponíveis a partir da consola do Configuration Manager.

Para obter mais informações sobre a Exploit Guard e componentes específicos e regras, consulte [Windows Defender Exploit Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard) na biblioteca de documentação de Windows.

### <a name="prerequisites"></a>Pré-requisitos
Dispositivos geridos têm de executar o Windows 10 1709 Fall Creators Update ou posterior e cumprir os requisitos seguintes, consoante os componentes e as regras configuradas:

|Componentes do exploit Guard |Pré-requisitos adicionais|
|------------------------|------------------------|
| Redução da Superfície de Ataque  | Dispositivos têm de ter [proteção em tempo real do Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) ativada.  |
| Acesso a pastas controladas  | Dispositivos têm de ter [proteção em tempo real do Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) ativada.   |
| Proteção de exploração  | Nenhum  |
| Proteção de rede  |  Dispositivos têm de ter [proteção em tempo real do Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) ativada.  |

### <a name="create-an-exploit-guard-policy----1355468---"></a>Criar uma política do Exploit Guard  <!--1355468 -->
1. Na consola do Configuration Manager, aceda a **ativos e compatibilidade** > **proteção de ponto final**e, em seguida, clique em **Windows Defender Exploit Guard**.
2. Sobre o **home page** separador a **criar** , clique em **criar política de explorar**.
3. Na página **Geral** do **Assistente de Criação de Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.
4. Em seguida, selecione os componentes do Exploit Guard que pretende gerir com esta política. Para cada componente que selecionar, em seguida, pode configurar detalhes adicionais.
   - **Redução da superfície de ataque:** Configure as ameaças, ameaças de scripts e ameaças de e-mail que pretende bloquear ou de auditoria do Office. Também pode excluir ficheiros ou pastas específicos desta regra.
   - **Acesso a pastas controladas:** Configurar o bloqueio ou a auditoria e, em seguida, adicionar aplicações que podem ignorar esta política.  Também pode especificar pastas adicionais que não estão protegidas por predefinição.
   - **Proteção de exploração:**  Especifique um ficheiro XML que contém definições para mitigar as explorações de aplicações e processos do sistema. Pode exportar estas definições a partir da aplicação do Centro de segurança do Windows Defender num dispositivo Windows 10.
   - **Proteção de rede:** Definir a proteção de rede para bloco ou auditoria o acesso a domínios suspeitos.
5. Conclua o Assistente para criar a política, que posteriormente pode implementar em dispositivos.

### <a name="deploy-an-exploit-guard-policy"></a>Implementar uma política do Exploit Guard     
Depois de criar políticas do Exploit Guard, utilize o assistente implementar política de proteção Exploit para implementá-las. Para tal, abra a consola do Configuration Manager para **ativos e compatibilidade** > **proteção de ponto final**e, em seguida, clique em **implementar política de proteção Exploit**.

## <a name="limited-support-for-cng-certificates"></a>Suporte limitado para certificados CNG
<!-- 1356191 --> Começando com esta versão, pode agora utilizar [API de criptografia: Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) modelos para os seguintes cenários de certificado:

- Registo de clientes e a comunicação com um ponto de gestão HTTPS.   
- Distribuição e aplicação de implementação de software com um ponto de distribuição de HTTPS.   
- Implementação do sistema operativo.  
- Cliente SDK (com a atualização mais recente) e de ISV Proxy de mensagens.   
- Configuração do Gateway de gestão de cloud.  

Para utilizar certificados CNG, a sua autoridade de certificação (AC) tem de fornecer modelos de certificado da CNG para máquinas de destino.  Detalhes do modelo variam de acordo com o cenário. No entanto, as seguintes propriedades são necessárias:

- **Compatibilidade** separador

    - **Autoridade de certificação** tem de ser Windows Server 2008 ou posterior. (O Windows Server 2012 é recomendado.)

    - **Destinatário do certificado** tem de ser Windows Vista/Server 2008 ou posterior. (O Windows 8 e Windows Server 2012 é recomendado.)

- **Criptografia** separador

    - **Categoria de fornecedor** tem de ser **Key Storage Provider**.  (Obrigatório)

Para obter melhores resultados, recomendamos a criação de nome do requerente de informações do Active Directory.  Utilize o nome de DNS para **formato de nome de requerente** e incluir o nome DNS no nome do requerente alternativo.  Caso contrário, terá de fornecer estas informações quando o dispositivo é inscrito para o perfil de certificado.


## <a name="improved-descriptions-for-pending-computer-restarts-----1356283---"></a>Descrições melhoradas para reinícios de computador pendentes   <!--1356283 -->
Na [technical preview 1708](/sccm/core/get-started/capabilities-in-technical-preview-1708#restart-computers-from-the-configuration-manager-console), adicionamos a capacidade de identificar os dispositivos que estão pendentes de uma reinicialização a partir da consola do Configuration Manager.

A partir desta pré-visualização técnica, a consola apresenta os detalhes adicionais que fornecem informações sobre o processo ou ação que está a solicitar a reinicialização.

## <a name="device-guard-policy-changes----1355092---"></a>Alterações de política de proteção do dispositivo <!-- 1355092 -->
Com a compilação de pré-visualização técnica 1710, as seguintes três alterações foram feitas em relação a políticas de Device Guard:

### <a name="device-guard-policies-renamed-to-windows-defender-application-control-policies"></a>O nome mudadas para políticas de controlo de aplicações do Windows Defender de políticas do Device Guard
Políticas do Device Guard foram renomeadas para políticas de controlo de aplicações do Windows Defender. Assim, por exemplo, o **Assistente de política de criar o Device Guard** tem agora o nome **Assistente de política de criar controlo de aplicações do Windows Defender**.

### <a name="restart-is-not-required-to-apply-policies"></a>Não é necessário reiniciar para aplicar políticas
Começando com o Fall Creators Update para Windows versão 1709, dispositivos com a nova versão do Windows não exigem uma reinicialização para aplicar as políticas de controlo de aplicações do Windows Defender.

A predefinição é reiniciar.

#### <a name="try-it-out"></a>Experimente!  

Se pretender desativar a reinícios, siga estes passos:

1.  Abra o **Criar aplicação de controlo de política do Windows Defender** assistente.
2.  Sobre o **gerais** página, desmarque a caixa de verificação **impor um reinício de dispositivos, para que esta política pode ser imposta para todos os processos**.
3.  Clique em **seguinte** até que o assistente ser concluído.

Para versões mais antigas do Windows, ainda é forçado um reinício do automatizada.

### <a name="automatically-run-software-trusted-by-the-intelligent-security-graph"></a>Executar automaticamente software considerado fidedigno pelo gráfico de segurança inteligente

Os administradores agora têm a opção para permitir que os dispositivos bloqueados executar o software de confiança com uma boa reputação, conforme determinado pelo gráfico de segurança inteligente Microsoft (ISG). O ISG é composto por Windows Defender SmartScreen e outros serviços Microsoft.

Os dispositivos devem executar o Windows Defender SmartScreen para o software ser fidedignas.

#### <a name="try-it-out"></a>Experimente!  

Para permitir que um dispositivo a executar o Windows Defender SmartScreen executar software de confiança, siga estes passos:

1.  Abra o **Assistente para criar aplicação controlo política do Windows Defender**.
2.  Sobre o **inclusões** página, marque a caixa **autorizar o software que é considerado fidedigno pelo gráfico de segurança inteligente**.
3.  Na **fidedigno ficheiros ou pasta** caixa, adicione os ficheiros e pastas que pretende que seja confiável.
4.  Clique em **seguinte** até que o assistente ser concluído.

## <a name="configure-and-deploy-windows-defender-application-guard-policies----1351960---"></a>Configurar e implementar políticas do Windows Defender Application Guard <!-- 1351960 -->

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) é um novo recurso do Windows que ajuda a proteger os seus utilizadores ao abrir sites não confiáveis no contentor isolado seguro que não está acessível por outras partes do sistema operativo. Este technical preview, adicionámos suporte para configurar esta funcionalidade utilizando as definições de compatibilidade do Configuration Manager que configurar e, em seguida, implementar numa coleção. Esta funcionalidade será lançada em pré-visualização para a versão de 64 bits da atualização do Windows 10 Creator (codinome: RS2). Para testar esta funcionalidade, agora, tem de utilizar uma versão de pré-visualização desta atualização.

### <a name="before-you-start"></a>Antes de começar
Para criar e implementar políticas do Windows Defender Application Guard, os dispositivos Windows 10 nos quais implementou a política tem de ser configurados com uma política de isolamento de rede. Para obter mais informações, consulte o blog post referenciado mais tarde. Esta funcionalidade funciona apenas com compilações do Windows 10 Insider atuais. Para testá-lo, os clientes devem executar um recente Windows 10 Insider criar.

### <a name="try-it-out"></a>Experimente!

Para compreender as noções básicas sobre o Windows Defender Application Guard, leia [a mensagem de blogue](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97).

Para criar uma política e para procurar as definições disponíveis:
1. Na **Configuration Manager** da consola, escolha **ativos e compatibilidade**.
2. Na **ativos e compatibilidade** área de trabalho, escolha **descrição geral** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. Na **home page** separador a **Create** , clique em **criar política Windows Defender Application Guard**.
4. Utilizar a mensagem de blogue como referência, pode procurar e configurar as definições disponíveis para experimentar a funcionalidade.
5. Nesta versão, adicionámos a nova página de definição de rede para o assistente. Aqui, especifique a identidade empresarial e defina o limite da rede empresarial.

    > [!NOTE]
    > Windows 10 PCs armazenar apenas uma lista de isolamento de rede no cliente. Nesta versão, pode criar dois tipos diferentes de listas de isolamento de rede (uma do Windows Information Protection e do Windows Defender Application Guard) e implementá-las para o cliente. Se implementar ambas as políticas, essas listas de isolamento de rede tem de corresponder. Se implementar listas que não correspondem para o mesmo cliente, a implementação irá falhar.

    Pode encontrar mais informações sobre como especificar definições de rede na [documentação de Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).

6. Quando tiver terminado, conclua o assistente e implementar a política para um ou mais dispositivos do Windows 10.

### <a name="further-reading"></a>Leitura adicional

Para ler mais sobre o Windows Defender Application Guard, veja [nesta mensagem de blogue](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Além disso, para saber mais sobre o modo autônomo do Windows Defender Application Guard, veja [nesta mensagem de blogue](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).

## <a name="next-steps"></a>Passos Seguintes
Para obter informações sobre a instalação ou a atualizar o ramo de pré-visualização técnica, veja [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
