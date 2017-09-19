---
title: Atualizar clientes | Microsoft Docs
description: Atualize clientes em computadores com Windows no System Center Configuration Manager.
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6143fd47-48ec-4bca-b53b-5b9b9f067bc3
caps.latest.revision: "11"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 319fbbf8ef70cb9b8a055b610828d1a2503c4689
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/15/2017
---
# <a name="how-to-upgrade-clients-for-windows-computers-in-system-center-configuration-manager"></a>Como atualizar clientes em computadores Windows no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode atualizar o cliente em computadores Windows utilizando métodos de instalação de cliente ou as funcionalidades de atualização automática do cliente no Configuration Manager. Os seguintes métodos de instalação de cliente são formas válidas de atualizar o software de cliente em computadores Windows:  

-   Instalação da política de grupo  

-   Instalação do script de início de sessão  

-   Instalação manual  

-   Instalação de atualização  

 Se estiver interessado em Atualizar o cliente utilizando métodos de instalação de cliente, saiba mais sobre como utilizar esses métodos em [como implementar clientes em computadores Windows no System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).

 A partir da versão 1610, pode excluir os clientes de que está a ser atualizado, especificando um grupo de exclusão. Para obter mais informações, consulte [como excluir atualizar clientes em computadores Windows](exclude-clients-windows.md).  


> [!TIP]  
>  Se estiver a atualizar a infraestrutura do servidor a partir de uma versão anterior do \(como o Configuration Manager 2007 ou o System Center 2012 Configuration Manager\), recomendamos que conclua a atualização do servidor incluindo a instalação de todas as atualizações do current branch, antes de atualizar os clientes do Configuration Manager.   A atualização mais recente do current branch contém a versão mais recente do cliente. Deste modo, é melhor fazer as atualizações de cliente depois de instalar todas as atualizações do Configuration Manager que pretende utilizar.

> [!NOTE]
> Se planeia reatribuir o site para os clientes durante a atualização, pode especificar o novo site utilizando a propriedade de client.msi SMSSITECODE. Se utilizar automática para o SMSSITECODE, também tem de especificar SITEREASSIGN = TRUE para permitir a reatribuição de automática de site ocorrer durante a atualização. Para obter mais informações, consulte [SMSSITECODE](../../deploy/about-client-installation-properties.md#smssitecode).

## <a name="use-automatic-client-upgrade"></a>Utilizar a atualização automática de cliente  
 Também pode configurar o Configuration Manager para atualizar automaticamente o software de cliente para a versão mais recente do cliente do Configuration Manager quando Configuration Manager identifica que um cliente atribuído à hierarquia do Configuration Manager é a versão anterior à utilizada na hierarquia. Este cenário inclui a atualização do cliente para a versão mais recente, quando o mesmo tenta a atribuição a um site do Configuration Manager.  

 Um cliente pode ser atualizado automaticamente nos seguintes cenários:  

-   A versão do cliente é anterior à versão utilizada na hierarquia.  

-   O cliente no site de administração central tem um pacote de idiomas instalado e o cliente existente não.  

-   Um pré-requisito de cliente na hierarquia tem uma versão diferente da instalada no cliente.  

-   Um ou mais dos ficheiros de instalação de cliente têm uma versão diferente.  

> [!NOTE]  
>  Pode executar o relatório **clientes de contagem do Configuration Manager por versões de cliente** na pasta de relatórios **Site - informação de cliente** para identificar as diversas versões do cliente do Configuration Manager na sua hierarquia.  

 Por predefinição que é enviada automaticamente a todos os pontos de distribuição na hierarquia, o Configuration Manager cria um pacote de atualização. Se efetuar alterações ao pacote de cliente no site de administração central, por exemplo, adicionar um pacote de idiomas de cliente do Configuration Manager atualizará automaticamente o pacote e distribuirá o mesmo por todos os pontos de distribuição na hierarquia. Se a atualização automática de cliente estiver ativada, todos os clientes irão instalar o novo pacote de idiomas de cliente automaticamente.  

> [!NOTE]  
>  O Configuration Manager não envia automaticamente a atualização de cliente pacote para pontos de distribuição baseados na nuvem do Configuration Manager.  

 Recomendamos que ative atualizações automáticas de cliente através da hierarquia. Isto irá manter os seus clientes atualizados com minimizando a sobrecarga administrativa.  

 Utilize o procedimento seguinte para configurar a atualização automática de cliente. A atualização automática de cliente tem de ser configurada num site de administração central e esta configuração aplica-se a todos os clientes da hierarquia.  

### <a name="to-configure-automatic-client-upgrades"></a>Para configurar atualizações automáticas de clientes  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  Na área de trabalho **Administração** , expanda **Configuração do Site**e clique em **Sites**.  

3.  No separador **Home Page** , no grupo **Sites** , clique em **Definições de Hierarquia**.  

4.  No separador **Atualização de Cliente** da caixa de diálogo **Propriedades das Definições de Hierarquia** , reveja a versão e a data do cliente de produção e certifique-se de que corresponde à versão que pretende utilizar para a atualização de computadores Windows.  Se não for a versão do cliente que esperava ver, poderá ter de promover o cliente de pré-produção para produção. Para obter mais informações, consulte [como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager](../../../../core/clients/manage/upgrade/test-client-upgrades.md).  

5.  Clique em **Atualizar todos os clientes na hierarquia utilizando o cliente de produção** e clique em **OK** na caixa de diálogo de confirmação.  

6.  Se não pretender que as atualizações de cliente sejam aplicadas a servidores, clique em **Não atualizar os servidores**.  

7.  Especifique o número de dias em que os computadores têm de atualizar o cliente após receberem a política de cliente. O cliente será atualizado num intervalo aleatório dentro deste prazo. Isto impede cenários em que um grande número de computadores cliente é atualizado simultaneamente.

    > [!NOTE]
    > Tem de executar um computador para atualizar o cliente. Se um computador não está em execução quando tem agendada para receber a atualização, a atualização não ocorrer. Em vez disso, quando o computador é reiniciado, outra atualização está agendada para um tempo aleatório num número de dias permitido. Se isto ocorrer depois do número de dias para atualizar tiver expirado, a atualização irá ser agendada para ocorrer num momento aleatórios dentro de 24 horas depois do computador foi reiniciado.
    >     
    > Devido a este comportamento, computadores que regularmente encerrar no final do workday podem um demorar mais tempo a atualizar a que o esperado se a hora de atualização agendada aleatoriamente não se encontra dentro do horário de trabalho normal.

7. A partir de versão 1610, se pretender excluir os clientes da ser atualizado, clique em **excluir especificado de clientes de atualização** e especifique a coleção para excluir.

8.  Se pretender que o pacote de instalação de cliente seja copiado para pontos de distribuição que tenham o conteúdo pré-configurado ativado, clique em **Distribuir automaticamente o pacote de instalação de cliente aos pontos de distribuição que tenham o conteúdo pré-configurado ativado**.  

9. Clique em **OK** para guardar as definições e fechar o caixa de diálogo **Propriedades das Definições de Hierarquia** . Os clientes receberão estas definições da próxima vez que transferirem a política.

>[!NOTE]
>As atualizações de cliente honrar janelas de manutenção do Configuration Manager, que configurou.
