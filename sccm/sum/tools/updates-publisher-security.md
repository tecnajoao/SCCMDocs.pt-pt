---
title: Certificados e segurança
titleSuffix: Configuration Manager
description: Gerir certificados e segurança para o System Center Updates Publisher
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: a7f91e63-4750-402e-9970-dd14be7f76a3
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 3632cbf8a512ef39413685f29b769e133fbcee40
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424303"
---
# <a name="manage-certificates-and-security-for-updates-publisher"></a>Gerir certificados e segurança para o Updates Publisher

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Os procedimentos seguintes podem ajudar a configurar o arquivo de certificados no servidor de atualização, configure um certificado autoassinado no computador cliente e configurar a política de grupo para permitir que o Windows Update Agent nos computadores para verificar a existência de atualizações publicadas .

## <a name="configure-the-certificate-store-on-the-update-server"></a>Configurar o arquivo de certificados no servidor de atualização
 Publicador de atualizações utiliza um certificado digital para assinar as atualizações nos catálogos do publica. Antes de um catálogo pode ser publicado para o servidor de atualização, esse certificado tem de ser no arquivo de certificados no servidor de atualização e no arquivo de certificados do computador Updates Publisher se esse computador for remoto a partir do servidor de atualização.

O procedimento seguinte é um dos vários métodos possíveis para adicionar o certificado ao arquivo de certificados no servidor de atualização.

### <a name="to-configure-the-certificate-store"></a>Para configurar o arquivo de certificados
1.  Num computador que pode acessar o computador do Updates Publisher e o servidor de atualização, clique em **começar**, clique em **execute**, tipo **MMC** no texto da caixa e, em seguida, clique em **OK** para abrir a consola de gestão da Microsoft (MMC).

2.  Clique em **arquivo**, clique em **Adicionar/Remover Snap-in**, clique em **Add**, clique em **certificados**, clique em **adicionar**, Selecione **conta de computador**e, em seguida, clique em **próxima**.

3.  Selecione **noutro computador**, escreva o nome do servidor de atualização ou clique em **procurar** para localizar o computador do servidor de atualização, clique em **concluir**, clique em **fechar**e, em seguida, clique em **OK**.

4.  Expanda **certificados (*nome do servidor de atualização*)**, expanda **WSUS**e, em seguida, clique em **certificados**.

5.  No painel de resultados, clique com botão direito do certificado pretendido, clique em **todas as tarefas**e, em seguida, clique em **exportar**.

6.  No Assistente para exportar certificados, utilize as predefinições para criar um ficheiro de exportação com o nome e a localização especificada no assistente. Este ficheiro tem de estar disponível para o servidor de atualização antes de prosseguir para o passo seguinte.

7.  Com o botão direito **fabricantes fidedignos**, clique em **todas as tarefas**e, em seguida, clique em **importar**. Conclua o Assistente de importação de certificado a utilizar o ficheiro exportado no passo 6.

8.  Se for utilizado um certificado autoassinado, tal como **WSUS Publishers autoassinado**, clique com botão direito **autoridades de certificação de raiz fidedigna**, clique em **todas as tarefas**e, em seguida, clique em **Importação**. Conclua o Assistente de importação de certificado a utilizar o ficheiro exportado no passo 6.

9.  Com o botão direito **certificados (*nome do servidor de atualização*)**, clique em **ligar a outro computador**, introduza o nome do computador para o computador do Updates Publisher e clique em  **OK**.

10. Se o Updates Publisher é remoto a partir do servidor de atualização, repita os passos 7 a 9 para importar o certificado ao arquivo de certificados no computador do Updates Publisher.



## <a name="configure-a-self-signing-certificate-on-client-computers"></a>Configurar um certificado autoassinado em computadores cliente
Em computadores cliente, o Windows Update Agent (WUA) irá analisar as atualizações do catálogo. Este processo irá falhar instalar atualizações quando o agente não é possível localizar o certificado digital no arquivo fabricantes fidedignos no computador local. Se um certificado autoassinado foi usado para publicar as atualizações do catálogo, como **WSUS Publishers autoassinado**, o certificado também tem de ser no arquivo de certificados de autoridades de certificação de raiz fidedigna no computador local por isso, que o agente pode verificar a validade do certificado.

Pode utilizar um dos vários métodos para configurar certificados nos computadores de cliente, como usar a diretiva de grupo e o **Assistente para importar certificados** ou utilizando a distribuição de software e a ferramenta de Certutil.

A seguir é fornecida como um exemplo de como configurar o certificado de assinatura em computadores cliente.

### <a name="to-configure-a-self-signing-certificate-on-client-computers"></a>Para configurar um certificado autoassinado em computadores cliente
1. Num computador com acesso ao servidor de atualização, clique em **começar**, clique em **executar**, tipo **MMC** na caixa de texto e clique em **OK** para abrir o Console de gerenciamento Microsoft (MMC).

2. Clique em **arquivo**, clique em **Adicionar/Remover Snap-in**, clique em **Add**, clique em **certificados**, clique em **adicionar**, Selecione **conta de computador**e, em seguida, clique em **próxima**.

3. Selecione **noutro computador**, escreva o nome do servidor de atualização ou clique em **procurar** para localizar o computador do servidor de atualização, clique em **concluir**, clique em **fechar**e, em seguida, clique em **OK**.

4. Expanda **certificados (*nome do servidor de atualização*)**, expanda **WSUS**e, em seguida, clique em **certificados**.

5. Com o botão direito do certificado no painel de resultados, clique em **todas as tarefas**e, em seguida, clique em **exportar**. Concluir o **Assistente para exportar certificados** utilizando as predefinições para criar um ficheiro de exportação de certificado com o nome e a localização especificada no assistente.

6. Utilize um dos seguintes métodos para adicionar o certificado utilizado para assinar o catálogo de atualizações para cada computador cliente que irá utilizar o WUA para analisar as atualizações no catálogo. Adicione o certificado no computador cliente da seguinte forma:

   -   Para certificados autoassinados: Adicionar o certificado para o **autoridades de certificação de raiz fidedigna** e **fabricantes fidedignos** arquivos de certificados.

   -   Para a autoridade de certificação (AC) emitiu certificados: Adicionar o certificado para o **fabricantes fidedignos** arquivo de certificados.

   > [!NOTE]
   > O WUA também verifica se o **permitir conteúdo assinado da localização de serviço de atualização de Microsoft na intranet** definição de política de grupo está ativada no computador local. Esta definição de política tem de estar ativada para que o WUA procure atualizações criadas e publicadas com o Updates Publisher. Para obter mais informações sobre a ativação desta definição de política de grupo, consulte [como configurar a política de grupo nos computadores cliente](<https://technet.microsoft.com/library/bb530967.aspx(d=robot>).



## <a name="configuring-group-policy-to-allow-wuaon-computers-to-scan-for-published-updates"></a>Configurando a diretiva de grupo para permitir que o WUA nos computadores para verificar a existência de atualizações publicadas
Antes de verificar o Windows Update Agent (WUA) em computadores de atualizações que foram criadas e publicadas com o Updates Publisher, uma definição de política tem de estar ativada para permitir conteúdo assinado da localização do serviço intranet Microsoft update. Quando a definição de política está ativada, o WUA aceita as atualizações recebidas através de uma localização de intranet se as atualizações forem assinadas **fabricantes fidedignos** arquivo de certificados no computador local. Existem vários métodos para configurar a política de grupo em computadores no ambiente.

Para computadores que não estão no domínio, pode ser configurada uma definição de chave de registo que permite que o conteúdo assinado da localização de serviço do Microsoft Update intranet.

Os procedimentos seguintes fornecem os passos básicos que podem ser utilizados para configurar a política de grupo para computadores no domínio e um valor de chave de registo nos computadores que não estão no domínio.

### <a name="to-configure-group-policy-to-allow-wua-to-scan-for-published-updates"></a>Para configurar a política de grupo para permitir que o WUA procure publicadas atualizações
1.  Abra o snap-in do grupo política objeto Editor Microsoft Management Console (MMC) com um utilizador que tem os direitos de segurança adequados para configurar a política de grupo.

2.  Clique em **procurar** e selecione o domínio, UO ou GPOs vinculados ao site em que a política de grupo configurada se propagará para os computadores cliente pretendido. Clique em **OK**, clique em **concluir**, clique em **fechar**e, em seguida, clique em **OK**.

3.  Expanda a definição de política selecionado na árvore da consola, expanda **configuração do computador**, expanda **modelos administrativos**, expanda **componentes do Windows**e, em seguida, Clique em **Windows Update**.

4.  No painel de resultados, clique com botão direito **permitir conteúdo assinado da localização de serviço de atualização de Microsoft na intranet**, clique em **propriedades**, clique em **ativado**e, em seguida, clique em  **OK**.
