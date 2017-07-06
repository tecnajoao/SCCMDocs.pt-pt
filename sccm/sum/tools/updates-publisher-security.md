---
title: "Certificados e segurança | Documentos do Microsoft"
description: "Gerir certificados e segurança para o System Center Updates Publisher"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7f91e63-4750-402e-9970-dd14be7f76a3
caps.latest.revision: 1
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.translationtype: Machine Translation
ms.sourcegitcommit: 31819a1df4e63e1114682490a9b3c3b4e5c99cfa
ms.openlocfilehash: c43af95a539a9284e4e49822b284783e02f9fa21
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="manage-certificates-and-security-for-updates-publisher"></a>Gerir certificados e segurança para o Updates Publisher

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Os procedimentos seguintes podem ajudá-lo a configurar o arquivo de certificados no servidor de atualização, configurar um certificado autoassinado no computador cliente e configurar a política de grupo para permitir que o Windows Update Agent nos computadores para verificar a existência de atualizações publicados.

## <a name="configure-the-certificate-store-on-the-update-server"></a>Configurar o arquivo de certificados no servidor de atualização
 Updates Publisher utiliza um certificado digital para assinar as atualizações de catálogos publica. Antes de um catálogo pode ser publicado para o servidor de atualização, esse certificado tem de ser no arquivo de certificados no servidor de atualização e, no arquivo de certificados do computador publicador de atualizações se for remoto relativamente ao servidor de atualização desse computador.

O procedimento seguinte é um dos vários métodos possíveis para adicionar o certificado ao arquivo de certificados no servidor de atualização.

### <a name="to-configure-the-certificate-store"></a>Para configurar o arquivo de certificados
1.  Num computador que pode aceder ao computador Updates Publisher e o servidor de atualização, clique em **iniciar**, clique em **executar**, tipo **MMC** na caixa de texto e, em seguida, clique em **OK** para abrir a consola de gestão da Microsoft (MMC).

2.  Clique em **ficheiro**, clique em **Adicionar/Remover Snap-in**, clique em **adicionar**, clique em **certificados**, clique em **adicionar**, selecione **conta de computador**e, em seguida, clique em **seguinte**.

3.  Selecione **noutro computador**, escreva o nome do servidor de atualização ou clique em **procurar** para localizar o computador do servidor de atualização, clique em **concluir**, clique em **fechar**e, em seguida, clique em **OK**.

4.  Expanda  **certificados (*nome do servidor de atualização*) * *, expanda **WSUS**e, em seguida, clique em **certificados**.

5.  No painel de resultados, faça duplo clique no certificado pretendido, clique em **todas as tarefas**e, em seguida, clique em **exportar**.

6.  No Assistente para exportar certificados, utilize as predefinições para criar um ficheiro de exportação com o nome e a localização especificada no assistente. Este ficheiro tem de estar disponível para o servidor de atualização antes de prosseguir para o passo seguinte.

7.  Com o botão direito **fabricantes fidedignos**, clique em **todas as tarefas**e, em seguida, clique em **importação**. Conclua o Assistente de importação de certificados utilizando o ficheiro exportado a partir do passo 6.

8.  Se for utilizado um certificado autoassinado, tais como **WSUS Publishers assinados**, com o botão direito **autoridades de certificação de raiz fidedigna**, clique em **todas as tarefas**e, em seguida, clique em **importação**. Conclua o Assistente de importação de certificados utilizando o ficheiro exportado a partir do passo 6.

9.  Com o botão direito  **certificados (*nome do servidor de atualização*) * *, clique em **ligar para outro computador**, introduza o nome do computador para computador publicador de atualizações e clique em **OK**.

10. Se for remoto relativamente ao servidor de atualização Updates Publisher, repita os passos 7 a 9 para importar o certificado ao arquivo de certificados no computador do Updates Publisher.



## <a name="configure-a-self-signing-certificate-on-client-computers"></a>Configurar um certificado autoassinado nos computadores cliente
Em computadores cliente, o Windows Update Agent (WUA) analisarão para as atualizações do catálogo. Este processo irá falhar instalar atualizações quando o agente não é possível localizar o certificado digital no arquivo fabricantes fidedignos no computador local. Se tiver sido utilizado um certificado autoassinado para publicar as atualizações do catálogo, tais como **WSUS Publishers assinados**, o certificado também tem de ser no arquivo de certificados de autoridades de certificação de raiz fidedigna no computador local, para que o agente pode verificar a validade do certificado.

Pode utilizar um dos vários métodos para configurar certificados nos computadores cliente, semelhante à utilização de política de grupo e o **Assistente para importar certificados** ou ao utilizar a distribuição de software e a ferramenta de Certutil.

É fornecido o seguinte como um exemplo de como configurar o certificado de assinatura em computadores cliente.

### <a name="to-configure-a-self-signing-certificate-on-client-computers"></a>Para configurar um certificado autoassinado nos computadores cliente
1.  Num computador com acesso ao servidor de atualização, clique em **iniciar**, clique em **executar**, tipo **MMC** na caixa de texto e, em seguida, clique em **OK** para abrir a consola de gestão da Microsoft (MMC).

2.  Clique em **ficheiro**, clique em **Adicionar/Remover Snap-in**, clique em **adicionar**, clique em **certificados**, clique em **adicionar**, selecione **conta de computador**e, em seguida, clique em **seguinte**.

3.  Selecione **noutro computador**, escreva o nome do servidor de atualização ou clique em **procurar** para localizar o computador do servidor de atualização, clique em **concluir**, clique em **fechar**e, em seguida, clique em **OK**.

4.  Expanda  **certificados (*nome do servidor de atualização*) * *, expanda **WSUS**e, em seguida, clique em **certificados**.

5.  Faça duplo clique no certificado no painel de resultados, clique em **todas as tarefas**e, em seguida, clique em **exportar**. Concluir o **Assistente para exportar certificados** utilizando as predefinições para criar um ficheiro de exportação de certificado com o nome e a localização especificada no assistente.

6.  Utilize um dos seguintes métodos para adicionar o certificado utilizado para assinar o catálogo de atualizações para cada computador cliente que irá utilizar o WUA para analisar as atualizações no catálogo. Adicione o certificado no computador cliente da seguinte forma:

    -   Para certificados autoassinados: Adicionar o certificado para o **autoridades de certificação de raiz fidedigna** e **fabricantes fidedignos** arquivos de certificados.

    -   Para a autoridade de certificação (AC) emitido certificados: Adicionar o certificado para o **fabricantes fidedignos** arquivo de certificados.

    > [!NOTE]
    > O WUA também verifica se o **permitir conteúdo assinado da localização de serviço de atualização de Microsoft na intranet** definição de política de grupo está ativada no computador local. Esta definição de política tem de estar ativada para que o WUA procure atualizações criadas e publicadas com o Updates Publisher. Para obter mais informações sobre a ativação desta definição de política de grupo, consulte [como configurar a política de grupo nos computadores cliente] (https://technet.microsoft.com/library/bb530967.aspx(d=robot).



## <a name="configuring-group-policy-to-allow-wua-on-computers-to-scan-for-published-updates"></a>Configurar a política de grupo para permitir que o WUA em computadores para verificar a existência de atualizações publicadas
Antes do Windows Update Agent (WUA) em computadores verificar existência de atualizações que foram criadas e publicadas com o Updates Publisher, uma definição de política tem de estar ativada para permitir conteúdo assinado a partir de uma localização de serviço de atualização de Microsoft na intranet. Quando a definição de política está ativada, o WUA aceita as atualizações recebidas através de uma localização de intranet se as atualizações forem assinadas **fabricantes fidedignos** arquivo de certificados no computador local. Existem vários métodos para configurar a política de grupo nos computadores no ambiente.

Para computadores que não estão no domínio, é possível configurar uma definição de chave de registo que permite conteúdo assinado da localização do serviço Microsoft Update intranet.

Os procedimentos seguintes fornecem os passos básicos que podem ser utilizados para configurar a política de grupo de computadores no domínio e um valor de chave de registo em computadores que não estão no domínio.

### <a name="to-configure-group-policy-to-allow-wua-to-scan-for-published-updates"></a>Configurar a política de grupo para permitir que o WUA procure publicados atualizações
1.  Abra o snap-in do grupo política objeto Editor gestão consola Microsoft (MMC) com um utilizador que tem os direitos de segurança apropriados para configurar a política de grupo.

2.  Clique em **procurar** e selecione o domínio, UO ou GPOs ligados para o site onde a política de grupo configurada propagará nos computadores cliente pretendido. Clique em **OK**, clique em **concluir**, clique em **fechar**e, em seguida, clique em **OK**.

3.  Expanda a definição de política selecionada na árvore da consola, expanda **configuração do computador**, expanda **modelos administrativos**, expanda **componentes do Windows**e, em seguida, clique em **Windows Update**.

4.  No painel de resultados, faça duplo clique **permitir conteúdo assinado da localização de serviço de atualização de Microsoft na intranet**, clique em **propriedades**, clique em **ativado**e, em seguida, clique em **OK**.
