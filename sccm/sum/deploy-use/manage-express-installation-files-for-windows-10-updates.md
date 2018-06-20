---
title: Gerir atualizações do Windows 10 express
titleSuffix: Configuration Manager
description: O Configuration Manager suporta ficheiros de instalação rápida para o Windows 10, que fornece transferências mais pequenas e de instalação mais rápidas nos clientes.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/15/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.openlocfilehash: 5f29b7a5d82b58358bdecd5508391db219b2cedc
ms.sourcegitcommit: 4b8afbd08ecf8fd54950eeb630caf191d3aa4767
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 06/19/2018
ms.locfileid: "36260929"
---
# <a name="manage-express-installation-files-for-windows-10-updates"></a>Gerir ficheiros de instalação rápida para atualizações do Windows 10

O Configuration Manager suporta ficheiros de instalação rápida para atualizações do Windows 10. Configurar o cliente para transferir apenas as alterações entre Windows 10 o mês atual atualização cumulativa qualidade e a atualização deste mês anterior. Sem ficheiros de instalação rápida, clientes do Configuration Manager transferem a completa Windows 10 a atualização cumulativa cada mês, incluindo todas as atualizações de meses anteriores. A utilização de ficheiros de instalação rápida fornece para transferências mais pequenas e tempos de instalação mais rápidos nos clientes.

Para saber como utilizar o Configuration Manager para gerir o conteúdo da atualização para se manter atual com o Windows 10, consulte [entrega de atualização do Windows 10 otimizar](/sccm/sum/deploy-use/optimize-windows-10-update-delivery).  


> [!IMPORTANT]  
> O suporte de cliente do SO está disponível no Windows 10, versão 1607, com uma atualização do Windows Update Agent. Esta atualização está incluída com as atualizações publicadas no 11 de Abril de 2017. Para mais informações sobre estas atualizações, consulte [suporta artigo 4015217](http://support.microsoft.com/kb/4015217). As atualizações futuras tirar partido do express para transferências mais pequenas. Versões anteriores do Windows 10 e Windows 10 versão 1607 sem esta atualização não suportam ficheiros de instalação rápida.  


### <a name="enable-the-site-to-download-express-installation-files-for-windows-10-updates"></a>Permitir que o site transferir ficheiros de instalação rápida para atualizações do Windows 10
Para iniciar a sincronizar os metadados para ficheiros de instalação rápida do Windows 10, ativá-la nas propriedades do ponto de atualização de software.  

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nós.  

2. Selecione o site de administração central ou site primário autónomo.  

3. No Friso, clique em **configurar componentes do Site**e, em seguida, clique em **ponto de atualização de Software**. Mudar para o **ficheiros de atualização** separador e selecione **transfira ambos os ficheiros de completos para todos os aprovados atualizações e ficheiros de instalação rápida para Windows 10**.

> [!NOTE]    
> Não é possível configurar o componente de ponto de atualização de software para *apenas* transferir atualizações rápidas.  O site transfere os ficheiros de instalação rápida para além dos ficheiros completos. Isto aumenta a quantidade de conteúdo armazenado na biblioteca de conteúdos e distribuídos e armazenados em pontos de distribuição.

> [!Tip]  
> Para determinar o espaço real que está a ser utilizado no disco pelo ficheiro, verifique o **tamanho do disco** propriedade do ficheiro. O tamanho na propriedade de disco deve ser significativamente menor do que o valor de tamanho. Para obter mais informações, consulte [perguntas mais frequentes para otimizar a entrega de atualização do Windows 10](/sccm/sum/deploy-use/optimize-windows-10-update-delivery#bkmk_faq).  


### <a name="enable-clients-to-download-and-install-express-installation-files"></a>Permitir que os clientes transferir e instalar ficheiros de instalação rápida
Para ativar o suporte de ficheiros de instalação rápida nos clientes, ative os ficheiros de instalação rápida no **atualizações de Software** grupo de definições de cliente. Esta definição cria um serviço de escuta HTTP novo que escuta pedidos transferir ficheiros de instalação rápida na porta que especificar.

> [!NOTE]    
> Esta é uma porta local que os clientes utilizam para escutar os pedidos de serviço de transferência inteligente em segundo plano (BITS) ou de otimização de entrega transferir conteúdo rápido do ponto de distribuição. Não precisa de abrir este portas nas firewalls porque todo o tráfego no computador local.  

Depois de implementar as definições de cliente para ativar esta funcionalidade no cliente, este tenta transferir as diferenças entre a atualização cumulativa do Windows 10 do mês atual e a atualização deste mês anterior. Os clientes têm de executar uma versão do Windows 10 que suporta ficheiros de instalação rápida.  

1. Ative o suporte para ficheiros de instalação rápida nas propriedades de componente de ponto de atualização de software (procedimento anterior).  

2. Na consola do Configuration Manager, vá para o **administração** área de trabalho e selecione **as definições de cliente**.  

3. Selecione as definições de cliente apropriada e clique em **propriedades** no Friso.  

4. Selecione o **atualizações de Software** grupo. Configurar a **Sim** a definição para **ativar instalação de atualizações rápida nos clientes**. Configurar o **porta utilizada para transferir conteúdo para atualizações de Express** com a porta utilizada pelo serviço de escuta HTTP no cliente.  
