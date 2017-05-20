---
title: "Contas para aceder ao conteúdo no System Center Configuration Manager | Documentos do Microsoft"
description: "Saiba mais sobre as contas de onde os clientes aos conteúdos do System Center Configuration Manager."
ms.custom: na
ms.date: 2/6/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7df9d0f-fbde-47eb-97e7-3d29536424fa
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: e592a732259147ee71d404a68982c28e5138e243
ms.openlocfilehash: 0e982d08d54af39b13f553fc531a200f921e94a6
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="manage-accounts-to-access-content-in-system-center-configuration-manager"></a>Gerir contas para aceder ao conteúdo no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de implementar o conteúdo no System Center Configuration Manager, considere a forma como os clientes acederão desse conteúdo a partir de pontos de distribuição. Este artigo descreve as seguintes contas para este efeito:

-   **Conta de acesso de rede**. Utilizada pelos clientes para ligar a um ponto de distribuição e aceder ao conteúdo. Por predefinição, os clientes tentam primeiro respetiva conta de computador.

     Esta conta também é utilizada pelos pontos de distribuição de solicitação para obter conteúdos a partir de um ponto de distribuição de origem localizado numa floresta remota.  

-   **Conta de acesso do pacote**. Por predefinição, o Configuration Manager concede acesso ao conteúdo de um ponto de distribuição para as contas incorporadas com o nome **utilizadores** e **administradores**. Pode configurar permissões adicionais para restringir o acesso.  

-   **Conta de ligação de multicast**. Utilizado para implementações do sistema operativo.  

##  <a name="bkmk_NAA"></a>Conta de acesso à rede  
 Computadores cliente utilizam a conta de acesso à rede quando estes não é possível utilizar a respetiva conta de computador local para aceder ao conteúdo em pontos de distribuição. Por exemplo, isto aplica-se a clientes e computadores de grupo de trabalho de domínios não fidedignos. Esta conta também pode ser utilizada durante a implementação do sistema operativo quando o computador a instalar o sistema operativo ainda não possui uma conta de computador no domínio.  

-   Os clientes utilizam apenas a conta de acesso à rede para aceder a recursos na rede.  

-   Em cada site primário, pode configurar várias contas para utilização como uma conta de acesso à rede.  

-   Os clientes tentam pela primeira vez aceder ao conteúdo num ponto de distribuição utilizando os respetivos *computername*conta $. Se esta conta falhar, os clientes tentam, em seguida utilizar uma conta de acesso de rede. Os clientes continuam a tentativa de utilizar a conta de acesso à rede, mesmo que tenha falhado anteriormente.  

### <a name="permissions"></a>Permissões
Conceda a esta conta as permissões mínimas adequadas para aceder ao software para o conteúdo que o cliente requer.  

-   A conta deve ter o **aceder a este computador a partir da rede** à direita no ponto de distribuição.  

-   Crie a conta em qualquer domínio que forneça o acesso necessário a recursos. A Conta de Acesso à Rede tem de incluir sempre um nome de domínio. Segurança pass-through não é suportada para esta conta. Se existirem pontos de distribuição em vários domínios, crie a conta num domínio fidedigno.  

> [!TIP]  
>  Para evitar bloqueios de conta, não altere a palavra-passe de uma Conta de Acesso à Rede existente. Em vez disso, crie uma nova conta e configurar a conta de novo no Configuration Manager. Quando tiver passado o tempo suficiente para todos os clientes receberem os detalhes da nova conta, remova a conta antiga das pastas partilhadas na rede da e eliminar a conta.  

> [!IMPORTANT]  
>  Não conceda a esta conta interativos direitos de início de sessão.  
>   
>  Não conceda a esta conta o direito de associar computadores ao domínio. Se tiver de associar computadores ao domínio durante uma sequência de tarefas, utilize a Conta de Adesão ao Domínio do Editor de Sequência de Tarefas.  

### <a name="to-configure-the-network-access-account"></a>Para configurar a conta de acesso à rede  

1.  Na consola do Configuration Manager, escolha **administração** >   **configuração do Site** >  **Sites**e, em seguida, selecione o site.  

2.  No **definições** grupo, selecione **configurar componentes do Site** > **distribuição de Software**.  

3.  Escolha o **conta de acesso à rede** separador. Configurar uma ou mais contas e, em seguida, escolha **OK**.  

##  <a name="bkmk_Paa"></a>Contas de acesso a pacote  
 Contas de acesso a pacote permitem-lhe definir permissões do sistema de ficheiros NTFS para especificar os utilizadores e grupos de utilizadores que podem aceder ao conteúdo de pacote em pontos de distribuição. Por predefinição, o Configuration Manager concede acesso apenas às genérica **utilizadores** e **administradores** contas. Pode controlar o acesso para computadores cliente, no entanto, utilizando as contas do Windows ou grupos adicionais. Dispositivos móveis não utilizam contas de acesso a pacote, porque estes dispositivos obtêm sempre o conteúdo do pacote de forma anónima.  

 Por predefinição, quando o Configuration Manager copia os ficheiros de conteúdo de um pacote para um ponto de distribuição, concede acesso **leitura** acesso local **utilizadores** grupo e **controlo total** local **administradores** grupo. As permissões reais que são necessárias dependem do pacote. Se tiver clientes localizados em grupos de trabalho ou em florestas não fidedignas, esses clientes utilizam a Conta de Acesso à Rede para aceder ao conteúdo dos pacotes. Certifique-se de que a conta de acesso à rede possui permissões para o pacote utilizando as contas de acesso do pacote definidas.  

 Utilize contas de um domínio que tenham acesso aos pontos de distribuição. Se criar ou alterar a conta após a criação do pacote, necessitará de redistribuir o pacote. A atualização do pacote não altera as permissões do sistema de ficheiros NTFS no pacote.  

 Não é necessário adicionar a conta de acesso à rede como uma conta de acesso do pacote, pois a associação a **utilizadores** grupo adiciona-a automaticamente. Restringir a Contas de Acesso a Pacotes Apenas à Conta de Acesso à Rede não impedirá o acesso dos clientes ao pacote.  

### <a name="to-manage-access-accounts"></a>Para gerir contas de acesso  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software**.  

2.  No **biblioteca de Software** área de trabalho, determinar o tipo de conteúdo para o qual pretende gerir contas de acesso e siga os passos fornecidos:  

    -   **Aplicações**: Expanda **gestão de aplicações**, escolha **aplicações**e, em seguida, selecione as aplicações cujas contas de acesso pretende gerir.  

    -   **Pacotes**: Expanda **gestão de aplicações**, escolha **pacotes**e, em seguida, selecione os pacotes cujas contas de acesso pretende gerir.  

    -   **Pacotes de implementação**: Expanda **atualizações de Software**, escolha **pacotes de implementação**e, em seguida, selecione os pacotes de implementação cujas contas de acesso pretende gerir.  

    -   **Pacotes de controladores**: Expanda **sistemas operativos**, escolha **pacotes de controladores**e, em seguida, selecione os pacotes de controladores cujas contas de acesso pretende gerir.  

    -   **Imagens do sistema operativo**: Expanda **sistemas operativos**, escolha **imagens do sistema operativo**e, em seguida, selecione as imagens de sistemas operativos para cujas contas de acesso pretende gerir.  

    -   **Instaladores do sistema operativo**: Expanda **sistemas operativos**, escolha **instaladores do sistema operativo**e, em seguida, selecione os instaladores do sistema operativo para cujas contas de acesso pretende gerir.  

    -   **Imagens de arranque**: Expanda **sistemas operativos**, escolha **imagens de arranque**e, em seguida, selecione as imagem de arranque cujas contas de acesso pretende gerir.  

3.  O objeto selecionado com o botão direito e, em seguida, selecione **gerir contas de acesso**.  

4.  No **adicionar conta** diálogo caixa, especifique o tipo de conta que será concedido acesso ao conteúdo e, em seguida, especifique os direitos de acesso associados a conta.  

    > [!NOTE]  
    >  Quando adicionar um nome de utilizador para a conta e do Configuration Manager localiza uma conta de utilizador local e uma conta de utilizador de domínio com esse nome, o Configuration Manager Define direitos de acesso para a conta de utilizador de domínio.  

##  <a name="bkmk_multi"></a>Conta de ligação de multicast  
 A conta de ligação de Multicast é utilizada pelos pontos de distribuição que estão configurados para o multicast ler informações da base de dados do site.  

-   Especifique uma conta a utilizar quando configurar ligações de base de dados do Configuration Manager para multicast.  

-   Por predefinição, é utilizada a conta de computador do ponto de distribuição, mas pode configurar uma conta de utilizador em vez disso.  

-   Tem de especificar uma conta de utilizador sempre que a base de dados do site estiver numa floresta não fidedigna.  

-   A conta deve ter **leitura** permissões para a base de dados do site.  

Por exemplo, se o seu centro de dados possuir uma rede de perímetro numa floresta que não é o servidor do site e a base de dados do site, pode utilizar esta conta para ler as informações de multicast da base de dados do site.

Se criar esta conta, crie-a como uma conta de direitos restritos, local no computador que executa o Microsoft SQL Server.  

> [!IMPORTANT]  
>  Não conceda a esta conta interativos direitos de início de sessão.  

