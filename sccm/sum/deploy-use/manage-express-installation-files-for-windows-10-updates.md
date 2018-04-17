---
title: Gerir ficheiros de instalação rápida para atualizações do Windows 10
titleSuffix: Configuration Manager
description: O Configuration Manager suporta ficheiros de instalação rápida para o Windows 10, que fornece transferências mais pequenas e de instalação mais rápidas nos clientes.
keywords: ''
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 03/24/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology:
- configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.openlocfilehash: 80ff608ca0e8270fc004995f861a0ccb312a6f34
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/16/2018
---
# <a name="manage-express-installation-files-for-windows-10-updates"></a>Gerir ficheiros de instalação rápida para atualizações do Windows 10
A partir do Configuration Manager versão 1702, o Configuration Manager suporta ficheiros de instalação rápida para atualizações do Windows 10. Quando utiliza uma versão suportada do Windows 10, pode utilizar as definições de cliente do Configuration Manager para configurar o cliente para transferir apenas as alterações entre Windows 10 atualização o mês atual cumulativa e a atualização do mês anterior. Sem ficheiros de instalação rápida, clientes do Configuration Manager transferirem a completa Windows 10 atualização cumulativa (incluindo todas as atualizações de meses anteriores) por mês. A utilização de ficheiros de instalação rápida fornece para transferências mais pequenas e tempos de instalação mais rápidos nos clientes.

> [!IMPORTANT]
> Enquanto as definições para suportar a utilização de ficheiros de instalação rápida está disponível no Configuration Manager versão 1702, o suporte de cliente do sistema operativo está disponível no Windows 10 versão 1607 com uma atualização de agente do Windows Update. Esta atualização está incluída com as atualizações publicadas no 11 de Abril de 2017 (Patch Terça-feira). Para mais informações sobre estas atualizações, consulte [suporta artigo 4015217](http://support.microsoft.com/kb/4015217). As atualizações futuras irão tirar partido da rápida para transferências mais pequenas. Windows 10 versão 1607 sem a atualização e as versões anteriores não suportam a ficheiros de instalação rápida.


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates"></a>Para permitir a transferência de ficheiros de instalação rápida para atualizações do Windows 10
Para iniciar a sincronizar os metadados para ficheiros de instalação rápida do Windows 10, tem de ativá-la nas propriedades do ponto de atualização de Software.
1.  Na consola do Configuration Manager, navegue até à **administração** > **configuração do Site** > **Sites**.
2.  Selecione o site de administração central ou site primário autónomo.
3.  No separador **Home Page** , no grupo **Definições** , clique em **Configurar Componentes do Site**e clique em **Ponto de Atualização de Software**. No **ficheiros de atualização** separador, selecione **transfira ambos os ficheiros de completos para todos os aprovados atualizações e ficheiros de instalação rápida para Windows 10**.

> [!NOTE]    
> Não é possível configurar o componente de ponto de atualização de Software para transferir apenas atualizações rápidas.  Transferir a instalação rápida de ficheiros serão além dos ficheiros completos e, por conseguinte, irão aumentar a quantidade de conteúdo distribuído para e armazenados em pontos de distribuição.

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>Para ativar o suporte para os clientes transferir e instalar ficheiros de instalação rápida
Para ativar o suporte de ficheiros de instalação rápida nos clientes, tem de ativar os ficheiros de instalação rápida na secção de definições de cliente de atualizações de Software. Esta ação cria um serviço de escuta HTTP novo que escuta pedidos transferir ficheiros de instalação rápida na porta que especificar.

> [!NOTE]    
> Esta é uma porta local que os clientes utilizarão para escutar os pedidos de otimização de entrega (siga) ou o serviço de transferência inteligente em segundo plano (BITS) para transferir conteúdo rápido do ponto de distribuição. Não é necessário abrir esta portas nas firewalls porque todo o tráfego no computador local.

Depois de implementar as definições de cliente para ativar esta funcionalidade no cliente, a tentativa de transferir as diferenças entre Windows 10 atualização o mês atual cumulativa e a atualização do mês anterior (os clientes têm de executar uma versão do Windows 10 que suporta ficheiros de instalação rápida).
1.  Ative o suporte para ficheiros de instalação rápida nas propriedades do componente de ponto de atualização de Software (procedimento anterior).
2.  Na consola do Configuration Manager, navegue até à **administração** > **as definições de cliente**.
3.  Selecione as definições de cliente adequado, em seguida, no **home page** separador, clique em **propriedades**.
4.  Selecione o **atualizações de Software** página, configure **Sim** para o **ativar instalação de atualizações rápida nos clientes** definir e configurar a porta utilizada pelo serviço de escuta HTTP no cliente para o **porta utilizada para transferir conteúdo para atualizações de Express** definição.
