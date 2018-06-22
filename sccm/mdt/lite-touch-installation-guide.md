---
title: Início rápido - instalação Lite Touch
titleSuffix: Microsoft Deployment Toolkit
description: 'Um guia de início rápido para o Microsoft Deployment Toolkit lite touch instalação. '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 21bedd68-e925-46e0-a540-df8c0aba2d6c
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 63ddb0c95fe08051dee8e9d003d542307d21b28c
ms.sourcegitcommit: 645cd5a324bdd299906efa27eaca5885eafc9e9c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/16/2018
ms.locfileid: "27821528"
---
# <a name="quick-start-guide-for-lite-touch-installation"></a>Guia de introdução para instalação Lite Touch  
 Microsoft Deployment Toolkit (MDT) 2013 fornece tecnologias para implementar sistemas operativos Windows e Microsoft Office. Este guia ajuda-o a avaliar rapidamente o MDT 2013, fornecendo instruções passo a passo condensed para utilizá-la para instalar o sistema operativo Windows 8.1 através do Lite Touch Installation (LTI) utilizando suportes de dados (DVD ou USB pen). Este guia demonstra como efetuar o cenário de implementação do novo computador a utilizar uma partilha de implementação do MDT 2013. O cenário de implementação do novo computador abrange a implementação do Windows 8.1 para um novo computador. Este cenário pressupõe que não há nenhum perfil para preservar ou dados de utilizador.  

> [!NOTE]     
>  Neste documento, *Windows* aplica-se aos sistemas operativos Windows 8.1, Windows 8, Windows 7, Windows Server® 2012 R2, Windows Server 2012 e Windows Server 2008 R2, exceto indicação em contrário. MDT não suporta ARM processador versões do Windows. Da mesma forma, *MDT* refere-se ao MDT 2013, salvo indicação em contrário.  

 Depois de utilizar este guia para avaliar o MDT, reveja o resto da documentação de orientação do MDT para saber mais sobre as funcionalidades avançadas da tecnologia.  

## <a name="prerequisites"></a>Pré-requisitos  
 Para implementar sistemas operativos e aplicações com o MDT, o ambiente deve satisfazer os seguintes pré-requisitos de configuração do software e o computador.  

### <a name="required-software"></a>Software necessário  
 Para concluir este guia, é necessário o seguinte software:  

-   Windows 8,1  

     Se optar por concluir neste guia num sistema operativo que não sejam de Windows 8.1, o MDT requer os seguintes elementos:  

    -   Microsoft .NET Framework versão 3.5 com Service Pack 1  

    -   Windows PowerShell™ versão 2.0  

     Windows 8.1 inclui estas funcionalidades.  

-   Windows Assessment and Deployment Kit (Windows ADK) para o Windows 8.1  

-   Serviços de rede, incluindo o sistema de nomes de domínio e Dynamic Host Configuration Protocol  

> [!NOTE]   
>  O sequenciador de tarefas utilizados em implementações de MDT requer que criar Global à direita possível atribuir o objeto para as credenciais utilizadas para aceder e executar o Deployment Workbench e o processo de implementação. Este direito está normalmente disponível para contas com permissões ao nível do administrador (a menos que removeu explicitamente). Além disso, a segurança especializada – perfil de segurança da funcionalidade limitada (SSLF) remove o direito de criar a objetos globais e não deve ser aplicada a computadores que está a ser implementada com o MDT até que o processo de MDT esteja concluído.  

### <a name="computer-configuration"></a>Configuração do computador  
 Para concluir este guia, configure os computadores listados na seguinte tabela. Estes computadores podem ser computadores físicos ou máquinas virtuais (VMs) com os recursos de sistema designados.  


|**Nome do computador**|**Descrição**|  
|-|-|  
|WDG-MDT-01|Este computador é executado o MDT e o Windows 8.1 e está instalado num domínio com o nome *mdt2013.corp.woodgrovebank.com* com um nome de sistema de entrada/saída básicos (NetBIOS) de rede de *MDT2013*. Os recursos do sistema do computador são:<br /><br /> -Processador em execução em 1,4 gigahertz (GHz) ou mais rápida.<br />-1 gigabyte (GB) ou superior memória física.<br />-Partição de disco um que tenha de 16 GB ou mais espaço em disco que vai ser a partição da unidade C.<br />-Um CD-ROM ou DVD-ROM unidade que será atribuída a letra de unidade D.|  
|WDG-REF-01|Este é o computador de referência e é executada sem sistema operativo atual. Os recursos do sistema do computador são:<br /><br /> -Processador em execução em 1,4 GHz ou mais rápida.<br />-1 GB ou mais memória física.<br />-16 GB ou mais de espaço em disco disponível.|  
|WDG-CLI-01|Este é o computador de destino e é executada sem sistema operativo atual. Os recursos do sistema do computador são:<br /><br /> -Processador em execução em 1,4 GHz ou mais rápida.<br />-1 GB ou mais memória física.<br />-16 GB ou mais de espaço em disco disponível.|  

> [!NOTE]   
>  Este guia pressupõe que estiver a avaliar o MDT em computadores físicos ou virtuais de 64 bits (x64). Se a avaliar o MDT nas plataformas de 32 bits (x86), transferência e instalação x86 edições do MDT e os componentes que este guia descreve.  

## <a name="step-1-obtain-the-required-software"></a>Passo 1: Obter o Software necessário  
 Este guia pressupõe que a versão de 64 bits do Windows 8.1 está instalada num computador denominado *WDG-MDT-01*. Se o computador estiver a utilizar com um nome diferente, substitua o nome do computador para *WDG-MDT-01*.  

> [!NOTE]   
>  Esta secção assume que está a criar uma nova infraestrutura de mensagens em fila para o MDT.  

 Para executar implementações LTI, é necessário o seguinte software:  

-   MDT 2013  

-   Windows ADK para Windows 8.1  

-   Ficheiros de distribuição do Windows 8.1  

-   Controladores de dispositivo necessários para o computador de destino, WDG-CLI-01  

-   Controladores de dispositivo necessários para o computador de referência, WDG-REF-01  

## <a name="step-2-prepare-the-mdt-environment"></a>Passo 2: Preparar o ambiente do MDT  
 Neste passo, prepare o ambiente do MDT antes de criar o computador de referência e implementar uma imagem capturada do computador de referência para o computador de destino (WDG-CLI-01).  

 Prepare o ambiente do MDT por:  

-   Instalar o MDT conforme descrito em [passo 1 de 2: Instale o MDT](#InstallMDT)  

-   Instalar o Windows ADK, tal como descrito no [passo 2 de 2: Instalar o Windows ADK](#InstallWindowsADK)  

###  <a name="InstallMDT"></a>Passo 1 de 2: Instale o MDT  
 Para instalar o MDT, conclua os seguintes passos:  

1.  Faça duplo clique em **MicrosoftDeploymentToolkit2013_x64.msi** (para sistemas operativos de 64 bits) ou **MicrosoftDeploymentToolkit2013_x86.msi** (para sistemas de operativos de 32 bits) e, em seguida, clique em **Instalar**.  

     Inicia o Assistente de configuração do Microsoft implementação Toolkit 2013.  

2.  Conclua a implementação Toolkit 2013 Assistente de configuração Microsoft com as informações seguintes. Aceite os valores predefinidos exceto indicação em contrário.  

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Bem-vindo ao Microsoft Deployment Toolkit Assistente de configuração de 2013**|Clique em **Seguinte**.|  
    |**Contrato de licença de utilizador final**|Clique em **aceito os termos no contrato de licença**e, em seguida, clique em **seguinte**.|  
    |**Configuração personalizada**|Clique em **Seguinte**.|  
    |**Pronto para instalar o Microsoft implementação Toolkit de 2013**|Clique em **Instalar**.|  
    |**Instalar o Microsoft Deployment Toolkit 2013**|É apresentado o progresso da instalação do MDT.|  
    |**A concluir o Assistente de configuração do Microsoft Deployment Toolkit 2013**|Clique em **Concluir**.|  

 Concluído o Assistente de configuração do Microsoft implementação Toolkit 2013 e instalação do MDT no WDG-MDT-01.  

###  <a name="InstallWindowsADK"></a>Passo 2 de 2: Instalar o Windows ADK  
 Para instalar o Windows ADK, execute os seguintes passos:  

1.  Monte os ficheiros de distribuição do Windows ADK numa unidade de CD-ROM físico ou virtual.  

2.  No Explorador do Windows, vá para a raiz da unidade de CD-ROM e, em seguida, faça duplo clique em **adksetup.exe**.  

     É iniciado o Assistente de configuração de Kit de implementação e avaliação.  

3.  Conclua o Assistente de configuração de Kit de implementação com as seguintes informações e avaliação.

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Especifique a localização**|Clique em **Seguinte**.|  
    |**Associar o programa de melhoramento da experiência do cliente (PMEC)**|Clique em **Sim** se pretende participar ou **não** caso contrário. Em seguida, clique em **seguinte**.|  
    |**Contrato de licença**|Clique em **aceitar**.|  
    |**Selecione as funcionalidades que pretende instalar**|Certifique-se de que apenas as caixas de verificação para as seguintes funcionalidades estão selecionadas e, em seguida, clique em **seguinte**:<br /><br /> -Ferramentas de implementação<br />-Ambiente de pré-instalação do Windows (Windows PE)<br />-Ferramenta de migração de estado de utilizador do Windows **Nota:**  MDT não necessita de outras funcionalidades, mas podem ser instaladas, se assim o desejar.|  
    |**Instalação de funcionalidades**|É apresentado o progresso para instalar as funcionalidades.|  
    |**Bem-vindo ao Assessment and Deployment Kit**|Clique em **Fechar**.|  

4.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

5.  Feche todas as abra windows.  

> [!NOTE]   
>  Depois de instalar o Windows ADK, termine sessão e, em seguida, inicie sessão novamente para o computador para que a variável de ambiente PATH seja atualizada para incluir a pasta % Program Files%\Windows Imaging.  

## <a name="step-3-configure-mdt-to-create-the-reference-computer"></a>Passo 3: Configurar o MDT para criar o computador de referência  
 Quando preparar o ambiente do MDT, crie o computador de referência. O computador de referência é o modelo para implementar novas imagens em computadores de destino. Configure este computador exatamente como os computadores de destino serão configurados. Irá implementar o Windows 8.1 para o computador de referência (WDG-REF-01), capturar uma imagem do computador de referência e, em seguida, implementar a imagem capturada no computador de destino (WDG-CLI-01).  

 Configure o MDT para criar um computador de referência por:  

-   Criar uma partilha de implementação do MDT, conforme descrito em [passo 1 de 3: Criar uma partilha de implementação do MDT](#CreateMDTDeployShare)  

-   Adicionar ficheiros do sistema operativo para a partilha de implementação, conforme descrito em [passo 2 de 3: Adicionar ficheiros do sistema operativo para a partilha de implementação](#AddOSFilestoDeployShare)  

-   Adicionar controladores de dispositivo para a partilha de implementação, conforme descrito em [passo 3 de 3: Adicionar controladores de dispositivo para a partilha de implementação](#AddDriverstoDeployShare)  

-   Criar uma sequência de tarefas para o computador de referência, conforme descrito em [passo 3-4: Criar uma sequência de tarefas para o computador de referência](#CreateTaskSequence)  

-   Ativar a monitorização do processo de implementação LTI, conforme descrito em [passo 3-5: Ativar a implementação LTI monitorização de processos](#EnableLTIDeployMonitor)  

-   A partilha de implementação de atualização, conforme descrito em [passo 3 a 6: Atualize a partilha de implementação](#UpdateDeployShare)  

###  <a name="CreateMDTDeployShare"></a>Passo 1 de 3: Criar uma partilha de implementação do MDT  
 Antes de pode começar a implementação, crie uma partilha de implementação do MDT no Deployment Workbench. Esta partilha de implementação é o repositório de imagens do sistema operativo, pacotes de idiomas, aplicações, controladores de dispositivo e outro software implementado nos computadores de destino.  

 **Para criar uma partilha de implementação no Deployment Workbench**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação de Workbench/implementação.  

3.  No painel ações, clique em **novas partilhas de implementação**.  

     Inicia o Assistente de nova partilha de implementação.  

4.  Conclua o Assistente de partilha de implementação novo com as informações seguintes.

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Path**|No **caminho de partilha de implementação**, tipo **C:\DeploymentShare$** e, em seguida, clique em **seguinte**.|  
    |**Share**|Clique em **Seguinte**.|  
    |**Nome descritivo**|Clique em **Seguinte**.|  
    |**Opções**|Clique em **Seguinte**.|  
    |**Resumo**|Clique em **Seguinte**.|  
    |**Progresso**|O progresso para criar a partilha de implementação é apresentado.|  
    |**Confirmação**|Clique em **Concluir**.|  

 Depois de concluída as implementação Assistente de nova partilha e a nova partilha de implementação — partilha de implementação MDT (C:\DeploymentShare$)—appears no painel de detalhes.  

###  <a name="AddOSFilestoDeployShare"></a>Passo 3-2: Adicionar ficheiros do sistema operativo para a partilha de implementação  
 MDT atua como um repositório para os ficheiros de sistema operativo implementado para o computador de referência (WDG-REF-01) e o computador de destino (WDG-CLI-01). Adicione o sistema operativo no nó sistemas operativos no Deployment Workbench com o Assistente de importação de sistema operativo.  

 **Para adicionar os ficheiros de sistema operativo Windows 8.1 para a partilha de implementação**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para a partilha de implementação de partilhas/MDT implementação Workbench/implementação (C:\DeploymentShare$)/Operating sistemas.  

3.  No painel ações, clique em **sistema de operativo importação**.  

     Inicia o Assistente de importação de sistema operativo.  

4.  Conclua o Assistente de importação de sistema operativo com as informações seguintes.    

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Na página do Assistente**|**Fazê-lo**|  
    |**Tipo de SO**|Clique em **conjunto completo de ficheiros de origem**e, em seguida, clique em **seguinte**.|  
    |**Origem**|No **diretório de origem**, tipo ***source_path*** (onde *source_path* é o caminho completamente qualificado para os ficheiros de distribuição do Windows 8.1) e, em seguida, clique em  **Seguinte**.|  
    |**Destino**|Clique em **Seguinte**.|  
    |**Resumo**|Clique em **Seguinte**.|  
    |**Progresso**|O progresso para importar o sistema operativo é apresentado.|  
    |**Confirmação**|Clique em **Concluir**.|  

 Concluir o Assistente de importação de sistema operativo. Windows 8.1 é adicionado à lista de sistemas operativos no painel de detalhes e copiados para o *deployment_share*\Operating sistemas\\*operating_system* pasta (onde  *deployment_share* é a pasta de rede partilhada que criou anteriormente no processo e *operating_system* é o nome do sistema operativo que adicionou à partilha de implementação).  

###  <a name="AddDriverstoDeployShare"></a>Passo 3 de 3: Adicionar controladores de dispositivo para a partilha de implementação  
 Depois de ter adicionado Windows 8.1 para o Deployment Workbench, adicione os controladores de dispositivo necessários para o computador de referência (WDG-REF-01) e o computador de destino (WDG-CLI-01). Estes controladores de dispositivo serão adicionadas ao Windows PE e implementados com o Windows 8.1. Adicionar os controladores de dispositivo no nó de controladores no Deployment Workbench, utilizando o Assistente de novo controlador, que copia os ficheiros de controlador de dispositivo para a implementação partilham em controladores de Out-of-Box\\*device_driver* ( onde *device_driver* é o nome do controlador de dispositivo que adicionou à partilha de implementação).  

> [!NOTE]   
>  Se os controladores de dispositivo para o computador de referência (WDG-REF-01) e o computador de destino (WDG-CLI-01) são incluídos com o Windows 8.1, ignore este passo e continue com o passo seguinte.  

 **Para adicionar os controladores de dispositivo para os computadores de referência e de destino para a partilha de distribuição**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para a partilha de implementação de partilhas/MDT implementação Workbench/implementação (C:\DeploymentShare$)/Out-of-Box controladores.  

3.  No painel ações, clique em **importar controladores**.  

     Inicia o Assistente de importação de controladores.  

4.  Conclua o Assistente de importação de controladores com as informações seguintes.

    |**Na página do Assistente**|**Fazê-lo**|
    |-|-|  
    |**Especifique o diretório**|No **diretório de origem de controlador**, tipo ***driver_path*** (onde *driver_path* é o caminho completamente qualificado para a pasta que contém os controladores de dispositivo) e, em seguida, clique em  **Seguinte**.|  
    |**Resumo**|Clique em **Seguinte**.|  
    |Progresso|O progresso para importar os controladores de dispositivo é apresentado.|  
    |**Confirmação**|Clique em **Concluir**.|  

 O Assistente para importar controlador é concluída. Os controladores de dispositivo são adicionados à lista de sistemas operativos no painel de detalhes e são copiados para o *deployment_share*pasta de controladores \Out-of-box (onde *deployment_share* é a partilha de implementação criado anteriormente no processo).  

###  <a name="CreateTaskSequence"></a>Passo 3-4: Criar uma sequência de tarefas para o computador de referência  
 Crie sequências de tarefas do MDT no nó sequências de tarefas no Deployment Workbench com o Assistente de nova sequência de tarefas. MDT inclui o modelo de sequência de tarefas de cliente padrão, que pode utilizar para implementar o sistema operativo de destino no computador de referência (WDG-REF-01).  

 **Para criar uma sequência de tarefas para implementar o computador de referência**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, aceda a partilha de implementação de partilhas/MDT implementação Workbench/implementação (C:\DeploymentShare$)/Task sequências  

3.  No painel ações, clique em **nova sequência de tarefas**.  

     Inicia o Assistente de nova sequência de tarefas.  

4.  Conclua o Assistente de sequência de tarefas novo com as seguintes informações. Aceite os valores predefinidos exceto indicação em contrário.

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Definições gerais**|1.  No **ID de sequência de tarefas**, tipo **WIN8_REFERENCE**.<br />2.  No **nome da sequência de tarefas**, tipo **implementar o Windows 8.1 para o computador de referência**.<br />3.  No **comentários de sequência de tarefas**, tipo **sequência para implementar o Windows 8.1 para o computador de referência (WDG-REF-01) de tarefas**.<br />4.  Clique em **Seguinte**.|  
    |**Selecione o modelo**|No **os modelos de sequência de tarefas seguintes estão disponíveis. Selecione a que pretende utilizar como um ponto de partida**, selecione **sequência de tarefas de cliente padrão**e, em seguida, clique em **seguinte**.|  
    |**Selecione o SO**|No **imagens de sistema operativo que se seguem estão disponíveis para implementação com esta sequência de tarefas**. **Selecione um para utilizar**, selecione **Windows 8.1 *edição***  (onde *edição* a edição do Windows 8.1 adicionada ao nó sistemas operativos no Deployment Workbench) e, em seguida, clique em **seguinte**.|  
    |**Especifique a chave de produto**|Clique em **não especificar uma chave de produto neste momento**e, em seguida, clique em **seguinte**.|  
    |**Definições de SO**|1.  No **nome completo**, tipo **Woodgrove Bank empregado**.<br /><br /> 2.  No **organização**, tipo **Banco Woodgrove**.<br /><br /> 3.  No **Home Page do Internet Explorer**, tipo **http://www.woodgrovebank.com**.<br /><br /> 4.  Clique em **Seguinte**.|  
    |**Palavra-passe de administrador**|No **palavra-passe de administrador** e **confirme a palavra-passe de administrador**, tipo  **P@ssw0rd** e, em seguida, clique em **seguinte**.|  
    |**Resumo**|Clique em **Seguinte**.|  
    |**Progresso**|É apresentado o progresso da criação de sequência de tarefas.|  
    |**Confirmação**|Clique em **Concluir**.|  

 O Assistente Importar sequência de tarefas é concluída e o **implementar o Windows 8.1 para o computador de referência** sequência de tarefas é adicionada à lista de sequências de tarefas.  

###  <a name="EnableLTIDeployMonitor"></a>Passo 3-5: Ativar a implementação LTI monitorização de processos  
 Antes de implementar o computador de referência (WDG-REF-01) com LTI suportes de dados que criou anteriormente no processo, ative a monitorização do processo de implementação LTI. Monitorizar o processo de implementação LTI no nó de monitorização na partilha de implementação. Ativar a monitorização de **monitorização** separador da folha de propriedades de partilha de implementação. Posteriormente no processo, irá monitorizar o processo de implementação LTI.  

 **Para ativar a monitorização do processo de implementação LTI**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação de Workbench/implementação.  

3.  No painel de detalhes, clique em **partilha de implementação do MDT (C:\DeploymentShare$)**.  

4.  No painel ações, clique em **propriedades**  

     O **propriedades de partilha de implementação do MDT (C:\DeploymentShare$)** é aberta a caixa de diálogo.  

5.  No **propriedades de partilha de implementação MDT (C:\DeploymentShare$)** caixa de diálogo a **monitorização** separador, selecione o **ativar a monitorização para esta partilha de implementação** caixa de verificação e, em seguida, clique em **aplicar**.  

6.  No **propriedades de partilha de implementação do MDT (C:\DeploymentShare$)** caixa de diálogo a **regras** separador, tenha em atenção que o **EventService** propriedade foi adicionada para o Ficheiro CustomSettings.ini e, em seguida, clique em **OK**.  

7.  Feche todas as janelas abertas e caixas de diálogo.  

###  <a name="UpdateDeployShare"></a>Passo 3 a 6: Atualize a partilha de implementação  
 Depois de configurar a partilha de implementação, atualizá-lo. A atualização da partilha de implementação de atualizações de todos os ficheiros de configuração do MDT e gera uma versão personalizada do Windows PE. Utilize a versão personalizada do Windows PE para iniciar o computador de referência e iniciar a implementação LTI.  

 **Para atualizar a partilha de implementação no Deployment Workbench**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação de Workbench/implementação.  

3.  No painel de detalhes, clique em **partilha de implementação do MDT (C:\DeploymentShare$)**.  

4.  No painel ações, clique em **partilha de implementação de atualização**.  

     Inicia o Assistente de partilha de implementação da atualização.  

5.  Conclua o Assistente de partilha de implementação de atualização utilizando as seguintes informações. Aceite os valores predefinidos exceto indicação em contrário.

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Opções**|Clique em **Seguinte**.|  
    |**Resumo**|Clique em **Seguinte**.|  
    |**Progresso**|O progresso para a partilha de implementação de atualização é apresentado.|  
    |**Confirmação**|Clique em **Concluir**.|  

 Deployment Workbench inicia a atualização da partilha de implementação MDT (C:\DeploymentShare$) de partilha de implementação. Deployment Workbench também cria os ficheiros de ficheiros LiteTouchPE_x64.iso e LiteTouchPE_x64.wim (para computadores de destino de 64 bits) ou os ficheiros litetouchpe_x86.ISO e LiteTouchPE_x86.wim (para computadores de destino de 32 bits) no *deployment_share*\Boot pasta (onde *deployment_share* é a pasta partilhada de rede utilizada como a partilha de implementação).  

## <a name="step-4-deploy-windows-81-and-capture-an-image-of-the-reference-computer"></a>Passo 4: Implementar o Windows 8.1 e capturar uma imagem do computador de referência  
 Depois de criar a sequência de tarefas para implementar o Windows 8.1 para o computador de referência, iniciar a implementação do sistema operativo e da imagem de captura ao iniciar o computador de referência com LTI suportes de dados.  

 Implementar o Windows 8.1 e capturar uma imagem do computador de referência por:  

-   Criar LTI suportes de dados, conforme descrito em [passo 4-1: Criar LTI suportes de dados](#CreateLTIBootable)  

-   Iniciar o computador de referência com LTI suportes de dados e monitorizar o processo de implementação LTI, conforme descrito em [passo 4-2: Iniciar o computador de referência com LTI suportes de dados](#StartRefCompwithLTIBootable)  

###  <a name="CreateLTIBootable"></a>Passo 4-1: Criar LTI suportes de dados  
 Tem de fornecer um método para iniciar o computador com a versão personalizada do Windows PE que criou quando atualizado a partilha de implementação. Deployment Workbench cria os ficheiros de ficheiros LiteTouchPE_x64.iso e LiteTouchPE_x64.wim (para computadores de destino de 64 bits) ou os ficheiros litetouchpe_x86.ISO e LiteTouchPE_x86.wim (para computadores de destino de 32 bits) no *deployment_share*\Boot pasta (onde *deployment_share* é a pasta partilhada de rede utilizada como a partilha de implementação). Crie adequado LTI suportes de dados a partir de uma destas imagens.  

 **Para criar LTI suportes de dados**  

1.  No Explorador do Windows, aceda a C:\DeploymentShare$\Boot.  

2.  Com base no tipo de computador utilizado para o computador de referência (WDG-REF-01), execute uma das seguintes tarefas:  

    -   Se o computador de referência for um computador físico, crie um CD ou DVD do ficheiro ficheiros LiteTouchPE_x64.iso ou LiteTouchPE_x86.iso físico.  

    -   Se o computador de referência é uma VM, inicie a VM diretamente a partir do ficheiro ficheiros LiteTouchPE_x64.iso ou LiteTouchPE_x86.iso ou a partir de um CD ou DVD dos ficheiros internacional padrão organização ISO ().  

###  <a name="StartRefCompwithLTIBootable"></a>Passo 4-2: Iniciar o computador de referência com LTI suportes de dados  
 Inicie o computador de referência (WDG-REF-01) com LTI suportes de dados que criou anteriormente no processo. O suporte de dados de arranque LTI inicia o Windows PE no computador de referência e inicia a implementação. No final do processo de implementação MDT, Windows 8.1 é implementado no computador de referência.  

> [!NOTE]   
>  Pode utilizar uma imagem de arranque de 32 bits para implementar sistemas operativos de 32 bits e 64 bits; No entanto, uma imagem de arranque de 64 bits só pode ser utilizada para implementar sistemas operativos de 64 bits.  

 Também é possível iniciar o processo ao iniciar o computador de destino a partir dos serviços de implementação do Windows. Para obter mais informações, consulte a secção "Preparar serviços de implementação", no documento do MDT, *utilizar o Microsoft Deployment Toolkit*.  

 **Para iniciar o computador de referência com LTI suportes de dados**  

1.  Inicie WDG-REF-01 com LTI suportes de dados que criou anteriormente no processo.  

     Windows PE inicia e, em seguida, inicia o Assistente de implementação do Windows.  

2.  Conclua o Assistente de implementação do Windows com as informações seguintes. Aceite os valores predefinidos exceto indicação em contrário.  

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Welcome**|Clique em **executar o Assistente de implementação para instalar um novo sistema operativo**.|  
    |**Credenciais**|1.  No **nome de utilizador**, tipo **administrador**.<br />2.  No **palavra-passe**, tipo  **P@ssw0rd** .<br />3.  No **domínio**, tipo **MDT2013**.<br />4.  Clique em **OK**.|  
    |**Sequência de tarefas**|Clique em **implementar o Windows 8.1 para o computador de referência**e, em seguida, clique em **seguinte**.|  
    |**Detalhes do Computador**|No **nome do computador**, **escreva WDG-REF-01**e, em seguida, clique em **seguinte**.|  
    |**Mover dados e definições**|Clique em **Seguinte**.|  
    |**Dados de utilizador (recuperação)**|Clique em **Seguinte**.|  
    |**Região e hora**|Clique em **Seguinte**.|  
    |**Captura de imagem**|Clique em **capturar uma imagem deste computador de referência**e, em seguida, clique em **seguinte**.|  
    |**Pronto**|1.  Clique em **detalhes** para ver as informações fornecidas no assistente.<br />2.  Clique em **começar**.|  

 **Para monitorizar o processo de implementação de computador de referência, execute os seguintes passos no WDG-MDT-01**  

1.  No WDG-MDT-01, clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para a partilha de implementação de partilhas/MDT implementação Workbench/implementação (C:\DeploymentShare$)/Monitoring.  

3.  No painel de detalhes, veja o processo de implementação para **WDG-REF-01**.  

4.  No painel de ações, clique periodicamente **atualizar**.  

     O estado do processo de implementação é atualizado no painel de detalhes.  

     Continue a monitorizar o processo de implementação até que o processo esteja concluído.  

5.  No painel de detalhes, clique em **WDG-REF-01**.  

6.  No painel ações, clique em **propriedades**.  

     O **WDG-REF-01 propriedades** é apresentada a caixa de diálogo.  

7.  No **WDG-REF-01 propriedades** caixa de diálogo a **identidade** separador, ver as informações de monitorização fornecidas sobre o processo de implementação, conforme descrito na seguinte tabela.

    |**Informações**|**Descrição**|  
    |-|-|  
    |**ID**|Identificador exclusivo para o computador que está a ser implementado.|  
    |**Nome do computador**|O nome do computador que está a ser implementado.|  
    |**Estado de implementação**|O estado atual do computador que está a ser implementado; o estado pode ser um dos seguintes:<br /><br /> -   **Executar**. A sequência de tarefas é bom estado de funcionamento e em execução.<br />-   **Não foi possível**. A sequência de tarefas falha e o processo de implementação foi bem-sucedido.<br />-   **Concluir**. A sequência de tarefas foi concluída.<br />-   **Responder**. A sequência de tarefas não tiver atualizado o seu estado nas últimas quatro horas e é prestada, tentados.|  
    |**Passo**|O passo de sequência tarefas atual a ser executado.|  
    |**Progresso**|O progresso global da sequência de tarefas. A barra de progresso indica quantos passos de sequência de tarefas terem sido executados fora do número total de passos de sequência de tarefas.|  
    |**Iniciar**|A hora de início do processo de implementação.|  
    |**End**|A hora em que terminou o processo de implementação.|  
    |**Elapsed**|O período de tempo, o processo de implementação tem estado em execução ou demorou a execução se foi concluído o processo de implementação.|  
    |**Erros**|O número de erros encontrados durante o processo de implementação.|  
    |**Avisos**|O número de avisos durante o processo de implementação.|  
    |**Ambiente de trabalho remoto**|Este botão permite-lhe estabelecer uma ligação de ambiente de trabalho remota com o computador que está a ser implementado através da funcionalidade de ambiente de trabalho remoto do Windows. Este método parte do princípio de que:<br /><br /> -O sistema operativo de destino está em execução e tiver ativada de suporte de ambiente de trabalho remoto<br />-   **mstsc.exe** está no caminho do **Nota:**  Este botão é sempre visível, mas pode não ser capaz de estabelecer uma sessão de ambiente de trabalho remoto, se o computador monitorizado está a executar o Windows PE, não foi concluída a instalação do sistema operativo de destino ou não tem ativada a funcionalidade de ambiente de trabalho remoto.|  
    |**Ligação de VM**|Este botão permite-lhe estabelecer uma ligação de ambiente de trabalho remota para uma VM em execução no HyperV®. Este método parte do princípio de que:<br /><br /> -A implementação está a ser efetuada a uma VM em execução no Hyper-V<br />-   **vmconnect.exe** está localizado na pasta %ProgramFiles%\Hyper-V **Nota:**  Este botão aparece quando ZTIGather.wsf Deteta que os componentes de integração do Hyper-V estão em execução no computador monitorizado. Caso contrário, este botão não serão visível.|  
    |**Controlo remoto de daRT**|Este botão permite-lhe estabelecer uma sessão de controlo remoto utilizando a funcionalidade Visualizador remoto na Diagnostics e Recovery Toolkit (DaRT).<br /><br /> Este método parte do princípio de que:<br /><br /> -DaRT ter sido implementado no computador de destino e estiver em execução<br />-   **DartRemoteViewer.exe** está localizado na pasta %ProgramFiles%\Microsoft DaRT 7\v7 **Nota:**  Este botão aparece quando ZTIGather.wsf Deteta que DaRT está em execução no computador monitorizado. Caso contrário, este botão não serão visível.|  
    |**Atualizar automaticamente estas informações a cada 10 segundos**|Caixa de verificação que controla se as informações na caixa de diálogo é automaticamente atualizadas. Se a caixa de verificação:<br /><br /> -Selecionado, as informações são atualizadas cada 10 segundos<br />-Limpo, as informações não são automaticamente atualizadas e têm de ser manualmente atualizadas utilizando o **atualizar agora** botão|  
    |**Atualizar neste momento**|Este botão imediatamente atualiza as informações apresentadas na caixa de diálogo.|  

8.  No **WDG-REF-01 propriedades** caixa de diálogo, clique em **OK**.  

9. Feche o Deployment Workbench.  

 Para concluir o processo de implementação de computador de referência, execute os seguintes passos no WDG-REF-01:  

1.  No WDG-REF-01, no **resumo de implementação** caixa de diálogo, clique em **detalhes**.  

     Se ocorrerem erros ou avisos, reveja os erros ou avisos e registe as informações de diagnóstico.  

2.  No **resumo de implementação** caixa de diálogo, clique em **concluir**.  

 Windows 8.1 está agora instalado no computador de referência e o ficheiro de formato Windows Imaging (WIM) capturada do computador de referência (WIN7_REFERENCE.wim) é armazenado no *deployment_share*\Captures pasta (onde  *deployment_share* é a pasta partilhada utilizada como a partilha de implementação). Se ocorrerem erros ou avisos, consulte o documento de MDT *referência de resolução de problemas*.  

## <a name="step-5-configure-mdt-to-deploy-windows-81-to-the-target-computer"></a>Passo 5: Configurar o MDT para implementar o Windows 8.1 para o computador de destino  
 Quando tiver capturado uma imagem do computador de referência (MDT-REF-01), implementá-la para o computador de destino (MDT-CLI-01). Importe a imagem capturada no Deployment Workbench com o Assistente para importar sistema operativo. Em seguida, crie uma sequência de tarefas para implementar a imagem capturada ao computador de destino.  

 Configure o MDT para implementar o Windows 8.1 para o computador de destino:  

-   Adicionar a imagem do computador de referência capturada ao Deployment Workbench conforme descrito em [passo 5-1: Adicionar a imagem do computador de referência capturada ao Deployment Workbench](#AddCapturedImagetoDeployWB)  

-   Criar uma sequência de tarefas para o computador de destino, conforme descrito em [passo 5-2: Criar uma sequência de tarefas para o computador de destino](#CreateTaskSequenceforTarget)  

###  <a name="AddCapturedImagetoDeployWB"></a>Passo 5-1: Adicionar a imagem do computador de referência capturada ao Deployment Workbench  
 Para implementar a imagem capturada do computador de referência para o computador de destino, adicione a imagem capturada à lista de sistemas operativos no nó sistemas operativos no Deployment Workbench. O Assistente de importação de sistema operativo copia os ficheiros de sistema operativo para o *deployment_share*\Operating sistemas\\*operating_system* pasta (onde *deployment_ partilhar* é a pasta de partilha de implementação criada anteriormente no processo e *operating_system* é o nome do sistema operativo adicionado à partilha de implementação).  

 **Para adicionar a imagem do computador de referência capturada ao Deployment Workbench**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para a partilha de implementação de partilhas/MDT implementação Workbench/implementação (C:\DeploymentShare$)/Operating sistemas.  

3.  No painel ações, clique em **sistema operativo de importação**.  

     Inicia o Assistente de importação de sistema operativo.  

4.  Conclua o Assistente de importação de sistema operativo utilizando as informações na tabela seguinte.

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Tipo de SO**|Clique em **ficheiro de imagem personalizada**e, em seguida, clique em **seguinte**.|  
    |**Image**|No **ficheiro de origem**, tipo **C:\DeploymentShare$\Captures\WIN8_REFERENCE.wim**e, em seguida, clique em **seguinte**.|  
    |**Setup**|Clique em **Seguinte**.|  
    |**Destino**|Clique em **Seguinte**.|  
    |**Resumo**|Clique em **Seguinte**.|  
    |**Progresso**|O progresso para importar o sistema operativo é apresentado.|  
    |**Confirmação**|Clique em **Concluir**.|  

     Concluir o Assistente de importação de sistema operativo. A imagem capturada do sistema de operativo de computador (WDG-REF-01) de referência é adicionada à lista de sistemas operativos no painel de detalhes e é copiada para o *deployment_share*\Operating sistemas\\  *operating_system* pasta (onde *deployment_share* é a pasta de partilha de implementação criada anteriormente no processo e *operating_system* é o nome da funcionar sistema de adicionar a partilha de implementação).  

5.  Feche todas as janelas abertas e caixas de diálogo.  

###  <a name="CreateTaskSequenceforTarget"></a>Passo 5-2: Criar uma sequência de tarefas para o computador de destino  
 Crie uma sequência de tarefas do MDT para o computador de destino no nó sequências de tarefas no Deployment Workbench com o Assistente de nova sequência de tarefas. Esta sequência de tarefas é utilizada para implementar a imagem capturada do computador de referência para o computador de destino.  

 **Para criar uma sequência de tarefas para implementar a imagem capturada ao computador de destino**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Ponto **para o Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, aceda a partilha de implementação (C:DeploymentShare$) do implementação Workbench/implementação partilhas/MDT / sequências de tarefas.  

3.  No painel ações, clique em **nova sequência de tarefas**.  

     Inicia o Assistente de nova sequência de tarefas.  

4.  Conclua o Assistente de sequência de tarefas novo com as seguintes informações. Aceite os valores predefinidos exceto indicação em contrário.

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Definições gerais**|1.  No **ID de sequência de tarefas**, tipo **WIN8_TARGET**.<br />2.  No **nome da sequência de tarefas**, tipo **implementar imagem capturada ao computador de destino**.<br />3.  No **comentários de sequência de tarefas**, tipo **de sequência de tarefas para a imagem capturada do Windows 8.1 do computador de referência (WDG-REF-01) para o computador de destino (WDG-CLI-01)**.<br />4.  Clique em **Seguinte**.|  
    |**Selecione o modelo**|No **os modelos de sequência de tarefas seguintes estão disponíveis**. **Selecione a que pretende utilizar como um ponto de partida**, selecione a opção padrão **sequência de tarefas de cliente**e, em seguida, clique em **seguinte**.|  
    |**Selecione o SO**|No **imagens de sistema operativo que se seguem estão disponíveis para implementação com esta sequência de tarefas**. **Selecione um para utilizar**, selecione **WIN8_RERENCEDrive no "WIN8_REFERENCE\WIN8_REFERENCE.wim"** e, em seguida, clique em **seguinte**.|  
    |**Especifique a chave de produto**|Clique em **não especificar uma chave de produto neste momento**e, em seguida, clique em **seguinte**.|  
    |**Definições de SO**|1.  No **nome completo**, tipo **Woodgrove Bank empregado**.<br />2.  No **organização**, tipo **Banco Woodgrove**.<br />3.  No **Home Page do Internet Explorer**, tipo **http://www.woodgrovebank.com**.<br />4.  Clique em **Seguinte**.|  
    |**Palavra-passe de administrador**|No **palavra-passe de administrador** e **confirme a palavra-passe de administrador**, tipo  **P@ssw0rd** e, em seguida, clique em **seguinte**.|  
    |**Resumo**|Clique em **Seguinte**.|  
    |**Progresso**|É apresentado o progresso da criação de sequência de tarefas.|  
    |**Confirmação**|Clique em **Concluir**.|  

     O Assistente Importar sequência de tarefas é concluída e o **WIN8_TARGET** sequência de tarefas é adicionada à lista de sequências de tarefas.  

5.  Feche todas as janelas abertas e caixas de diálogo.  

## <a name="step-6-deploy-the-captured-image-of-the-reference-computer-to-the-target-computer"></a>Passo 6: Implementar a imagem capturada do computador de referência para o computador de destino  
 Quando tiver capturado uma imagem do computador de referência e criado e configurado a sequência de tarefas adequadas, implementar a imagem capturada. Configure o MDT para fornecer todas as definições de configuração necessárias para a implementação para o computador de destino. Depois de iniciar o processo de implementação, a imagem do computador de referência com o Windows 8.1 é implementada no computador de destino e automaticamente configurada com as definições especificadas.  

 Implemente a imagem capturada do computador de referência para o computador de destino:  

-   A iniciar o computador de destino com LTI suportes de dados e monitorizar o processo de implementação LTI, conforme descrito em [passo 6-1: Iniciar o computador de destino com LTI suportes de dados](#StartTargetwithLTIBootable)  

###  <a name="StartTargetwithLTIBootable"></a>Passo 6-1: Iniciar o computador de destino com LTI suportes de dados  
 Inicie o computador de destino (WDG-CLI-01) com LTI suportes de dados que criou anteriormente no processo. Este CD inicia o Windows PE no computador de destino e inicia a implementação. No final do processo, o Windows 8.1 é implementado no computador de destino.  

> [!NOTE]
>  Também pode iniciar a implementação ao iniciar o computador de destino a partir dos serviços de implementação do Windows. Para obter mais informações, consulte o documento de MDT *utilizar o Microsoft Deployment Toolkit*.  

 **Para iniciar o computador de destino com LTI suportes de dados**  

1.  Inicie WDG-CLI-01 com LTI suportes de dados que criou anteriormente no processo.  

     Windows PE inicia e, em seguida, inicia o Assistente de implementação do Windows.  

2.  Conclua o Assistente de implementação do Windows com as informações seguintes. Aceite os valores predefinidos exceto indicação em contrário.   

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Welcome**|Clique em **executar o Assistente de implementação para instalar um novo sistema operativo**.|  
    |**Credenciais**|1.  No **nome de utilizador**, tipo **administrador**.<br />2.  No **palavra-passe**, tipo  **P@ssw0rd** .<br />3.  No **domínio**, tipo **MDT2013**.<br />4.  Clique em **OK**.|  
    |**Sequência de tarefas**|Clique em **implementar imagem capturada ao computador de destino**e, em seguida, clique em **seguinte**.|  
    |**Detalhes do Computador**|No **nome do computador**, tipo **WDG-CLI-01**e, em seguida, clique em **seguinte**.|  
    |**Mover dados e definições**|Clique em **Seguinte**.|  
    |**Dados de utilizador (recuperação)**|Clique em **Seguinte**.|  
    |**Região e hora**|**Clique em seguinte**.|  
    |**Captura de imagem**|Clique em **Seguinte**.|  
    |**BitLocker**|Clique em **Seguinte**.|  
    |**Pronto**|1.  Clique em **detalhes** para ver as informações fornecidas no assistente.<br />2.  Clique em **começar**.|  

 O assistente for iniciado, e, em seguida, inicia a implementação do sistema operativo.  

 **Para monitorizar o processo de implementação de computador de destino, execute os seguintes passos no WDG-MDT-01**  

1.  No WDG-MDT-01, clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para a partilha de implementação de partilhas/MDT implementação Workbench/implementação (C:\DeploymentShare$)/Monitoring  

3.  No painel de ações, clique periodicamente **atualizar**.  

4.  No painel de detalhes, veja o processo de implementação para **WDG-CLI-01**.  

5.  No painel de ações, clique periodicamente **atualizar**.  

     O estado do processo de implementação é atualizado no painel de detalhes. Continue a monitorizar o processo de implementação até que o processo esteja concluído.  

6.  Feche o Deployment Workbench.  

 **Para concluir o processo de implementação de computador de destino, execute os seguintes passos no WDG-CLI-01**  

1.  No WDG-CLI-01, no **resumo de implementação** caixa de diálogo, clique em **detalhes**.  

     Se ocorrerem erros ou avisos, reveja os erros ou avisos e registe as informações de diagnóstico.  

2.  No **resumo de implementação** caixa de diálogo, clique em **concluir**.  

 No final do processo de implementação MDT, o **resumo de implementação** é apresentada a caixa de diálogo. A imagem do Windows 8.1 capturada do computador de referência está agora instalada no computador de destino. Se ocorrerem erros ou avisos, consulte o documento de MDT *referência de resolução de problemas*.
