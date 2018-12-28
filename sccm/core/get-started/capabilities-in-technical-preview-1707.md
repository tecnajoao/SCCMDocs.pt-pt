---
title: Pré-visualização técnica versão 1707
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis na versão Technical Preview versão 1707 para o System Center Configuration Manager.
ms.date: 08/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cb405ba0-8792-4ab7-988b-2f835f3a9550
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5500b7458935c83207a5e54f8fd1d4d7f40dc333
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421642"
---
# <a name="capabilities-in-technical-preview-1707-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview versão 1707 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão versão 1707. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md) para se familiarizar com os requisitos gerais e limitações para a utilização de um técnico de pré-visualização, como atualizar entre as versões e como fornecer comentários sobre os recursos de uma technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Problemas conhecidos neste Technical Preview:**
- **Atualização para a versão versão 1707 pré-visualização falha quando tem um servidor de site em modo passivo**. Quando executar a versão de pré-visualização 1706 e ter uma [servidor do site primário em modo passivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), tem de desinstalar o servidor do site de modo passivo antes de poder atualizar o site de pré-visualização com êxito para a versão versão 1707. Pode reinstalar o servidor do site de modo passivo após a versão versão 1707 de execução do seu site.

  Para desinstalar o servidor do site de modo passivo:
  1. Na consola, aceda a **Administration** > **descrição geral** > **configuração do Site** > **servidores e sites Funções do sistema**e, em seguida, selecione o servidor de site de modo passivo.
  2. Na **funções do sistema de sites** painel, clique direito na **servidor do Site** função e, em seguida, escolha **remover função**.
  3. Faça duplo clique no servidor do site de modo passivo e, em seguida, escolha **eliminar**.
  4. Depois de desinstala o servidor do site, no servidor do site primário active reinicie o serviço **CONFIGURATION_MANAGER_UPDATE**.



**Seguem-se os novos recursos, que pode experimentar com esta versão.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Suporte de Cache ponto a ponto do cliente para ficheiros de instalação rápida do Windows 10 e Office 365
<!-- 1352486 --> A partir desta versão, Cache ponto a ponto suporta a distribuição de ficheiros de conteúdo de instalação rápida para o Windows 10 e de ficheiros de atualização para o Office 365. Sem configurações adicionais são necessárias.

## <a name="surface-device-dashboard"></a>Painel do dispositivo Surface
<!--1355788--> Dashboard do dispositivo de superfície fornece informações sobre os dispositivos Surface encontrado no seu ambiente. Na consola, aceda a **monitorização** > **dispositivos Surface**. Pode ver o seguinte:
- Número de Surfaces
- Percentagem de modelos de surfaces
- principais cinco versões de sistema operativo

Clique na secção do **modelos de superfície** gráfico para obter uma lista completa dos dispositivos.  

## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Configurar e implementar políticas do Windows Defender Application Guard
<!-- 1351960 -->

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) é um novo recurso do Windows que ajuda a proteger os seus utilizadores ao abrir sites não confiáveis no contentor isolado seguro que não está acessível por outras partes do sistema operativo. Este technical preview, adicionámos suporte para configurar esta funcionalidade utilizando as definições de compatibilidade do Configuration Manager que configurar e, em seguida, implementar numa coleção. Esta funcionalidade será lançada em pré-visualização para a versão de 64 bits da atualização do criador do Windows 10 Fall (codinome: RS3). Para testar esta funcionalidade, agora, tem de utilizar uma versão de pré-visualização desta atualização.

### <a name="before-you-start"></a>Antes de começar

Para criar e implementar políticas do Windows Defender Application Guard, os dispositivos Windows 10 nos quais implementou a política tem de ser configurados com uma política de isolamento de rede. Para obter mais detalhes, consulte [nesta mensagem de blogue](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Esta funcionalidade funciona apenas com compilações do Windows 10 Insider atuais. Para testá-lo, os clientes devem executar um recente Windows 10 Insider criar.

### <a name="try-it-out"></a>Experimente!

#### <a name="to-create-a-policy-and-to-browse-the-available-settings"></a>Para criar uma política e para procurar as definições disponíveis:

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade**.
2. Na **ativos e compatibilidade** área de trabalho, escolha **descrição geral** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. Na **home page** separador a **Create** , clique em **criar política Windows Defender Application Guard**.
4. Utilizar a mensagem de blogue como referência, pode procurar e configurar as definições disponíveis para experimentar a funcionalidade.
5. Nesta versão, adicionámos o novo **definição de rede** página para o assistente. Nesta página, especifique a identidade empresarial e defina o limite da rede empresarial.<br>Windows 10 PCs armazenar apenas uma lista de isolamento de rede no cliente. Nesta versão, pode criar dois tipos diferentes de listas de isolamento de rede (uma do Windows Information Protection e do Windows Defender Application Guard) e implementá-las para o cliente. Se implementar ambas as políticas, essas listas de isolamento de rede tem de corresponder. Se implementar listas que não correspondem para o mesmo cliente, a implementação irá falhar.
Pode encontrar mais informações sobre como especificar definições de rede na [documentação de Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).
6. Quando tiver terminado, conclua o assistente e implementar a política para um ou mais dispositivos do Windows 10.

### <a name="further-reading"></a>Leitura adicional
Para ler mais sobre o Windows Defender Application Guard, veja [nesta mensagem de blogue](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Além disso, para saber mais sobre o modo autônomo do Windows Defender Application Guard, veja [nesta mensagem de blogue](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).

## <a name="add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Adicionar parâmetros ao implementar scripts do PowerShell do Configuration Manager

<!-- 1236459 --->

No último Technical Preview, introduzimos uma nova funcionalidade que permite que [criar e executar scripts do PowerShell da consola do Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1706#create-and-run-powershell-scripts-from-the-configuration-manager-console).
Esta pré-visualização técnica, Expandimos sobre esta capacidade. Agora, Configuration Manager lê o script do PowerShell e apresenta todos os parâmetros no Assistente de criação de Script. Pode fornecer um valor para o parâmetro no assistente que será utilizado quando o script é executado. Em alternativa, pode deixar o parâmetro em branco. Se o fizer, terá de fornecer um valor para o parâmetro ao executar o script.
Nesta pré-visualização técnica, deve fornecer quaisquer parâmetros que necessita de um script. Numa versão futura, planeamos de tornar a fornecer os parâmetros de script opcionais.

### <a name="try-it-out"></a>Experimente!

1. Siga as instruções para [criar e executar scripts do PowerShell da consola do Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1706#create-and-run-powershell-scripts-from-the-configuration-manager-console).
2. No novo **parâmetros de Script** página do **Assistente de criação de Script**, selecione um parâmetro e, em seguida, clique em **editar**.
3. Fornecer um valor de parâmetro para o parâmetro selecionado e, em seguida, clique em **OK**.
4. Conclua o assistente.

Quando o script é executado, ele usará quaisquer valores de parâmetro que configurou.
