---
title: "Comandos de suporte de dados de sequência de tarefas de Pré-início | Microsoft Docs"
description: "Criar um script para utilizar para o comando de Pré-início, distribuir o conteúdo associado o comando de Pré-início e configurar o comando de Pré-início no suporte de dados."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ccc9f652-2953-4c38-8a90-c799484105ca
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 1c396534425179c6828d48acc578295167c566be
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="prestart-commands-for-task-sequence-media-in-system-center-configuration-manager"></a>Comandos de Pré-início para suportes de dados do sequência de tarefas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode criar um comando de Pré-início no System Center Configuration Manager, para utilizar com suportes de dados de arranque, suportes de dados autónomos e suportes de dados. O comando de pré-início é um script ou executável que é executado antes da seleção da sequência de tarefas e pode interagir com o utilizador no Windows PE. O comando de pré-início pode solicitar informações a um utilizador e guardá-las no ambiente da sequência de tarefas ou consultar uma variável da sequência de tarefas para obter informações. Quando o computador de destino arranca, a linha de comandos é executada antes de a política ser transferida do ponto de gestão. Utilize os procedimentos seguintes para criar um script que será utilizado no comando de pré-início, distribuir o conteúdo associado ao comando de pré-início e configurar o comando de pré-início no suporte de dados.  

## <a name="create-a-script-file-to-use-for-the-prestart-command"></a>Criar um ficheiro de script para utilizar no Comando de Pré-início  
 É possível ler e escrever as variáveis da sequência de tarefas, utilizando o objeto Microsoft.SMS.TSEnvironment COM enquanto a sequência de tarefas está em execução. O exemplo a seguir ilustra um ficheiro de script do Visual Basic que consulta a variável da sequência de tarefas _SMSTSLogPath para obter a localização do registo atual. O script também define uma variável personalizada.  

```  
dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")  
dim logPath  
' You can query the environment to get an existing variable.  
logPath = env("_SMSTSLogPath")  
' You can also set a variable in the OSD environment.  
env("MyCustomVariable") = "varname"  
```  

## <a name="create-a-package-for-the-script-file-and-distribute-the-content"></a>Criar um Pacote para o Ficheiro de Script e Distribuir o Conteúdo  
 Depois de criar o script ou executável para o comando de pré-início, tem de criar uma origem de pacote para alojar os ficheiros para o script ou executável, criar um pacote para os ficheiros (não é necessário nenhum programa) e depois distribuir o conteúdo para um ponto de distribuição.  

 Para obter mais informações sobre como criar um pacote, consulte [pacotes e programas](../../apps/deploy-use/packages-and-programs.md).  

 Para obter mais informações sobre a distribuição de conteúdo, consulte [distribuir conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

## <a name="configure-the-prestart-command-in-media"></a>Configurar o Comando de Pré-início no Suporte de Dados  
 No Assistente de Criação do Suporte de Dados da Sequência de Tarefas, é possível configurar um comando de pré-início para suportes de dados autónomos, suportes de dados de arranque ou suportes de dados de pré-configuração. Para obter mais informações sobre os tipos de suportes de dados, consulte [criar suportes de dados de sequência de tarefas](../deploy-use/create-task-sequence-media.md). Utilize o procedimento seguinte para criar um comando de pré-início no suporte de dados.  

#### <a name="to-create-a-prestart-command-in-media"></a>Para criar um comando de pré-início no suporte de dados  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Suportes de Dados da Sequência de Tarefas** para iniciar o Assistente de Criação de Suporte de Dados da Sequência de Tarefas.  

4.  Na página **Selecionar Tipo de Suporte de Dados** , selecione **Suporte de dados autónomo**, **Suporte de dados de arranque**ou **Suporte de dados de pré-configuração**e, em seguida, clique em **Seguinte**.  

5.  Navegue para a página **Personalização** do assistente. Para obter mais informações sobre a configuração das outras páginas no assistente, consulte [criar suportes de dados de sequência de tarefas](../deploy-use/create-task-sequence-media.md).  

6.  Na página **Personalização** , especifique as seguintes informações e clique em **Seguinte**.  

    -   Selecione **Ativar comando de pré-início**.  

    -   Na caixa de texto **Linha de comandos** , introduza o script ou executável que criou para o comando de pré-início.  

        > [!IMPORTANT]  
        >  Utilize **cmd /C < comando de Pré-início\>**  para especificar o comando de Pré-início. Por exemplo, se tiver utilizado o nome TSScript.vbs para o script do comando de pré-início, deve introduzir **cmd /C TSScript.vbs** na linha de comandos. Se **cmd /C** abrir uma nova janela do interpretador de comandos do Windows e utilizar a variável de ambiente Path para localizar o script ou executável do comando de pré-início. Também é possível especificar o caminho completo para o comando de pré-início, mas a letra da unidade pode ser diferente em computadores com configurações de unidades diferentes.  

    -   Selecione **Incluir ficheiros para o comando de pré-início**.  

    -   Clique em **Definir** para selecionar o pacote que está associado aos ficheiros de comando de pré-início.  

    -   Clique em **Procurar** para selecionar o ponto de distribuição que aloja o conteúdo para o comando de pré-início.  

7.  Conclua o assistente.  
