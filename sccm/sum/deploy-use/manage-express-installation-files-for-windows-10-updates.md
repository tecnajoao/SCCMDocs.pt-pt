---
title: Gerir atualizações do Windows 10 express
titleSuffix: Configuration Manager
description: O Configuration Manager suporta ficheiros de instalação rápida para o Windows 10, que fornece transferências mais pequenas e da instalação mais rápida nos clientes.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/15/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.openlocfilehash: 54e91c729739d7bf1f0417a80a0143cc4969ed74
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383139"
---
# <a name="manage-express-installation-files-for-windows-10-updates"></a>Gerir ficheiros de instalação rápida para atualizações do Windows 10

O Configuration Manager suporta ficheiros de instalação rápida para atualizações do Windows 10. Configurar o cliente para transferir apenas as alterações entre com o Windows 10 o mês atual atualização cumulativa de qualidade e a atualização deste mês anterior. Sem ficheiros de instalação rápida, os clientes do Configuration Manager transferem a atualização completa para Windows 10 cumulative todos os meses, incluindo todas as atualizações dos meses anteriores. A utilização de ficheiros de instalação rápida fornece para transferências mais pequenas e tempos de instalação mais rápidos nos clientes.

Para saber como utilizar o Configuration Manager para gerir o conteúdo da atualização para se manter atualizado com o Windows 10, veja [entrega de atualização do Windows 10 otimizar](/sccm/sum/deploy-use/optimize-windows-10-update-delivery).  


> [!IMPORTANT]  
> O suporte de cliente do sistema operacional está disponível no Windows 10, versão 1607, com a atualização do Windows Update Agent. Esta atualização está incluída com as atualizações publicadas no dia 11 de Abril de 2017. Para obter mais informações sobre estas atualizações, consulte [4015217 do artigo de suporte](http://support.microsoft.com/kb/4015217). As atualizações futuras tirar partido do express para transferências mais pequenas. Em versões anteriores do Windows 10 e Windows 10 versão 1607 sem essa atualização não suportam ficheiros de instalação rápida.  


### <a name="enable-the-site-to-download-express-installation-files-for-windows-10-updates"></a>Permitir que o site transferir ficheiros de instalação rápida para atualizações do Windows 10
Para começar a sincronizar os metadados para ficheiros de instalação rápida do Windows 10, tem de ativá-la nas propriedades do ponto de atualização de software.  

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó.  

2. Selecione o site de administração central ou site primário autónomo.  

3. No Friso, clique em **configurar componentes do Site**e, em seguida, clique em **ponto de atualização de Software**. Mude para o **ficheiros de atualização** separador e selecione **transfira ambos os ficheiros completos para todas as aprovadas as atualizações e os ficheiros de instalação rápida para o Windows 10**.

> [!NOTE]    
> Não é possível configurar o componente de ponto de atualização de software para *apenas* transferir atualizações de express.  O site transfere os ficheiros de instalação rápida além dos ficheiros completos. Isso aumenta a quantidade de conteúdo armazenados na biblioteca de conteúdos e distribuídos e armazenados em pontos de distribuição.

> [!Tip]  
> Para determinar o espaço real a ser utilizado no disco pelo ficheiro, verifique os **tamanho no disco** propriedade do ficheiro. O tamanho na propriedade do disco deve ser consideravelmente menor do que o valor de tamanho. Para obter mais informações, consulte [FAQs para otimizar a entrega de atualização do Windows 10](/sccm/sum/deploy-use/optimize-windows-10-update-delivery#bkmk_faq).  


### <a name="enable-clients-to-download-and-install-express-installation-files"></a>Permitir que os clientes transferir e instalar ficheiros de instalação rápida
Para ativar o suporte de ficheiros de instalação rápida nos clientes, permitir que os ficheiros de instalação rápida no **atualizações de Software** grupo de definições de cliente. Esta definição cria um novo ouvinte HTTP que escuta pedidos transferir ficheiros de instalação rápida na porta que especificar.

> [!NOTE]    
> Esta é uma porta local que os clientes utilizam para escutar os pedidos de Otimização da entrega ou o serviço de transferência inteligente em segundo plano (BITS) para transferir o conteúdo express a partir do ponto de distribuição. Não precisa abrir esta porta nos firewalls, porque todo o tráfego está no computador local.  

Depois de implementar as definições de cliente para ativar esta funcionalidade no cliente, ele tenta transferir o delta entre a atualização cumulativa do Windows 10 do mês atual e a atualização deste mês anterior. Os clientes têm de executar uma versão do Windows 10 que suporta ficheiros de instalação rápida.  

1. Ative o suporte para ficheiros de instalação rápida nas propriedades de componente de ponto de atualização de software (procedimento anterior).  

2. Na consola do Configuration Manager, vá para o **Administration** área de trabalho e selecione **definições de cliente**.  

3. Selecione as definições de cliente adequado e clique em **propriedades** da faixa de opções.  

4. Selecione o **atualizações de Software** grupo. Configurar para **Sim** a definição **ativar a instalação de atualizações de Express em clientes**. Configurar o **porta utilizada para transferir conteúdo para atualizações de Express** com a porta utilizada pelo serviço de escuta HTTP no cliente.
