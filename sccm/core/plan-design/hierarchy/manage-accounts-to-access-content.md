---
title: "As contas para aceder a conteúdo no System Center Configuration Manager | Microsoft Docs"
description: "Saiba mais sobre as contas de onde os clientes acedem aos conteúdos do System Center Configuration Manager."
ms.custom: na
ms.date: 2/6/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7df9d0f-fbde-47eb-97e7-3d29536424fa
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0e982d08d54af39b13f553fc531a200f921e94a6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="manage-accounts-to-access-content-in-system-center-configuration-manager"></a>Gerir contas para aceder a conteúdo no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de implementar o conteúdo no System Center Configuration Manager, considere a forma como os clientes acedem a esse conteúdo de pontos de distribuição. Este artigo descreve as seguintes contas utilizadas para esta finalidade:

-   **Conta de acesso de rede**. Utilizada pelos clientes para ligar a um ponto de distribuição e aceder ao conteúdo. Por predefinição, os clientes tentar primeiro a respetiva conta de computador.

     Esta conta é também utilizada pelos pontos de distribuição de extração para obter conteúdo de um ponto de distribuição de origem numa floresta remota.  

-   **Conta de acesso a pacote**. Por predefinição, o Configuration Manager concede acesso a conteúdo num ponto de distribuição para as contas incorporadas com o nome **utilizadores** e **administradores**. Pode configurar permissões adicionais para restringir o acesso.  

-   **Conta de ligação de multicast**. Utilizado para implementações do sistema operativo.  

##  <a name="bkmk_NAA"></a>Conta de acesso de rede  
 Computadores cliente utilizam a conta de acesso à rede quando estes não podem utilizar a respetiva conta de computador local para aceder ao conteúdo em pontos de distribuição. Por exemplo, isto aplica-se a clientes e computadores de grupo de trabalho de domínios não fidedignos. Esta conta também pode ser utilizada durante a implementação do sistema operativo quando o computador a instalar o sistema operativo ainda não possui uma conta de computador no domínio.  

-   Os clientes utilizam apenas a conta de acesso de rede para aceder a recursos na rede.  

-   Em cada site primário, pode configurar várias contas para utilização como uma conta de acesso à rede.  

-   Os clientes tentam pela primeira vez para aceder ao conteúdo num ponto de distribuição utilizando o respetivo *computername*conta $. Se esta conta falhar, os clientes tentam, em seguida utilizar uma conta de acesso de rede. Os clientes continuam a tentar utilizar a conta de acesso de rede, mesmo que tenha falhado anteriormente.  

### <a name="permissions"></a>Permissões
Conceda a esta conta as permissões mínimas adequadas para aceder ao software para o conteúdo que o cliente requer.  

-   A conta deve ter o **aceder a este computador a partir da rede** à direita no ponto de distribuição.  

-   Crie a conta em qualquer domínio que fornece o acesso necessário a recursos. A Conta de Acesso à Rede tem de incluir sempre um nome de domínio. Segurança pass-through não é suportada para esta conta. Se existirem pontos de distribuição em vários domínios, crie a conta num domínio fidedigno.  

> [!TIP]  
>  Para evitar bloqueios de conta, não altere a palavra-passe de uma Conta de Acesso à Rede existente. Em vez disso, crie uma nova conta e configure a nova conta no Configuration Manager. Quando tiver passado o tempo suficiente para todos os clientes receberem os detalhes da nova conta, remova a conta antiga a partir das pastas partilhadas na rede e eliminar a conta.  

> [!IMPORTANT]  
>  Não conceda a esta conta de direitos interativos ao iniciar sessão.  
>   
>  Não conceda a esta conta o direito de associar computadores ao domínio. Se tiver de associar computadores ao domínio durante uma sequência de tarefas, utilize a Conta de Adesão ao Domínio do Editor de Sequência de Tarefas.  

### <a name="to-configure-the-network-access-account"></a>Para configurar a conta de acesso de rede  

1.  Na consola do Configuration Manager, escolha **administração** >   **configuração do Site** >  **Sites**e, em seguida, selecione o site.  

2.  No **definições** grupo, escolha **configurar componentes do Site** > **distribuição de Software**.  

3.  Escolha o **conta de acesso à rede** separador. Configurar uma ou mais contas e, em seguida, escolha **OK**.  

##  <a name="bkmk_Paa"></a>Contas de acesso do pacote  
 Contas de acesso a pacote permitem-lhe definir permissões do sistema de ficheiros NTFS para especificar os utilizadores e grupos de utilizadores que podem aceder a conteúdo de pacote em pontos de distribuição. Por predefinição, o Configuration Manager concede acesso apenas às genérica **utilizadores** e **administradores** contas. Pode controlar o acesso para computadores cliente, no entanto, através da utilização de contas do Windows ou grupos adicionais. Dispositivos móveis não utilizem as contas de acesso do pacote, porque estes dispositivos sempre obtêm conteúdo do pacote de forma anónima.  

 Por predefinição, quando o Configuration Manager copia os ficheiros de conteúdo de um pacote para um ponto de distribuição, concede acesso **leitura** acesso local **utilizadores** grupo e **controlo total** local **administradores** grupo. As permissões reais que são necessárias dependem do pacote. Se tiver clientes localizados em grupos de trabalho ou em florestas não fidedignas, esses clientes utilizam a Conta de Acesso à Rede para aceder ao conteúdo dos pacotes. Certifique-se de que a conta de acesso de rede tem permissões para o pacote utilizando as contas de acesso do pacote definidas.  

 Utilize contas de um domínio que tenham acesso aos pontos de distribuição. Se criar ou alterar a conta após a criação do pacote, necessitará de redistribuir o pacote. A atualização do pacote não altera as permissões do sistema de ficheiros NTFS no pacote.  

 Não é necessário adicionar a conta de acesso de rede como uma conta de acesso do pacote, porque a associação do **utilizadores** grupo adiciona automaticamente. Restringir a Contas de Acesso a Pacotes Apenas à Conta de Acesso à Rede não impedirá o acesso dos clientes ao pacote.  

### <a name="to-manage-access-accounts"></a>Para gerir contas de acesso  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software**.  

2.  No **biblioteca de Software** área de trabalho, determinar o tipo de conteúdo para o qual pretende gerir contas de acesso e siga os passos fornecidos:  

    -   **Aplicações**: Expanda **gestão de aplicações**, escolha **aplicações**e, em seguida, selecione as aplicações cujas contas de acesso pretende gerir.  

    -   **Pacotes**: Expanda **gestão de aplicações**, escolha **pacotes**e, em seguida, selecione os pacotes cujas contas de acesso pretende gerir.  

    -   **Pacotes de implementação**: Expanda **atualizações de Software**, escolha **pacotes de implementação**e, em seguida, selecione os pacotes de implementação cujas contas de acesso pretende gerir.  

    -   **Pacotes de controladores**: Expanda **sistemas operativos**, escolha **pacotes de controladores**e, em seguida, selecione os pacotes de controladores cujas contas de acesso pretende gerir.  

    -   **Imagens de sistema operativo**: Expanda **sistemas operativos**, escolha **imagens do sistema operativo**e, em seguida, selecione as imagens de sistema operativo para o qual pretende gerir contas de acesso.  

    -   **Instaladores do sistema operativo**: Expanda **sistemas operativos**, escolha **instaladores do sistema operativo**e, em seguida, selecione os instaladores do sistema operativo para o qual pretende gerir contas de acesso.  

    -   **Imagens de arranque**: Expanda **sistemas operativos**, escolha **imagens de arranque**e, em seguida, selecione as imagem de arranque cujas contas de acesso pretende gerir.  

3.  Faça duplo clique o objeto selecionado e, em seguida, escolha **gerir contas de acesso**.  

4.  No **adicionar conta** diálogo caixa, especifique o tipo de conta que será concedido acesso ao conteúdo e, em seguida, especifique os direitos de acesso associados à conta.  

    > [!NOTE]  
    >  Quando adicionar um nome de utilizador para a conta e do Configuration Manager localiza uma conta de utilizador local e uma conta de utilizador de domínio com esse nome, o Configuration Manager Define direitos de acesso da conta de utilizador de domínio.  

##  <a name="bkmk_multi"></a>Conta de ligação de multicast  
 A conta de ligação de Multicast é utilizada pelos pontos de distribuição que estão configurados para o multicast ler informações da base de dados do site.  

-   Especifique uma conta a utilizar quando configurar ligações de base de dados do Configuration Manager para multicast.  

-   Por predefinição, é utilizada a conta de computador do ponto de distribuição, mas pode configurar uma conta de utilizador em vez disso.  

-   Tem de especificar uma conta de utilizador sempre que a base de dados do site estiver numa floresta não fidedigna.  

-   A conta deve ter **leitura** permissões para a base de dados do site.  

Por exemplo, se o seu centro de dados possuir uma rede de perímetro numa floresta que não é o servidor do site e a base de dados do site, pode utilizar esta conta para ler as informações de multicast da base de dados do site.

Se criar esta conta, crie-o como um com direitos restritos, uma conta local no computador que executa o Microsoft SQL Server.  

> [!IMPORTANT]  
>  Não conceda a esta conta de direitos interativos ao iniciar sessão.  
