---
title: "Gerir ficheiros de instalação rápida para atualizações do Windows 10 | Documentos do Microsoft"
description: "O Configuration Manager suporta ficheiros de instalação rápida para o Windows 10, que fornece transfere mais pequeno e tempos mais rápidos de instalação em clientes."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 03/24/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.translationtype: Machine Translation
ms.sourcegitcommit: d7b13f3dea5a3ae413ca6b8150ec24e1632a4d4d
ms.openlocfilehash: fcdcbcde61402b47871d51deba32d23867a78370
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---

## <a name="manage-express-installation-files-for-windows-10-updates"></a>Gerir ficheiros de instalação rápida de atualizações do Windows 10
A partir do Configuration Manager versão 1702, o Configuration Manager suporta ficheiros de instalação rápida para atualizações do Windows 10. Quando utiliza uma versão suportada do Windows 10, pode utilizar definições do Configuration Manager para transferir apenas as alterações entre Windows 10 atualização o mês atual cumulativa e a atualização do mês anterior. Sem ficheiros de instalação expressa do Configuration Manager transfere a completo Windows 10 atualização cumulativa (incluindo todas as atualizações de meses anteriores) por mês. Utilizar ficheiros de instalação rápida fornece para transferências mais pequenas e tempos mais rápidos de instalação em clientes.

> [!IMPORTANT]
> Enquanto as definições para suportar a utilização de ficheiros de instalação rápida está disponível no Configuration Manager versão 1702, o suporte de clientes do sistema operativo está disponível no Windows 10 versão 1607 com uma atualização de agente do Windows Update. Esta atualização está incluída com as atualizações publicadas no 11 de Abril de 2017 (Patch Terça-feira). Para mais informações sobre estas atualizações, consulte o artigo [suporta artigo 4015217](http://support.microsoft.com/kb/4015217). Atualizações futuras serão partido rápida para as transferências mais pequenas. Windows 10 versão 1607 sem a atualização e as versões anteriores não suportam ficheiros de instalação rápida.


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates-on-the-server"></a>Para permitir a transferência de ficheiros de instalação rápida para atualizações do Windows 10 no servidor do
Para iniciar a sincronização dos metadados para ficheiros de instalação expressa do Windows 10, terá de a ativar nas propriedades do ponto de atualização de Software.
1.    Na consola do Configuration Manager, navegue para **administração** > **configuração do Site** > **Sites**.
2.    Selecione o site de administração central ou site primário autónomo.
3.    No separador **Home Page** , no grupo **Definições** , clique em **Configurar Componentes do Site**e clique em **Ponto de Atualização de Software**. No **ficheiros de atualização** separador, selecione **transferir ficheiros completos de todas as atualizações aprovadas e rápida de ficheiros de instalação para o Windows 10**.

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>Para ativar o suporte para os clientes transferir e instalar ficheiros de instalação rápida
Para ativar o suporte de ficheiros de instalação rápida nos clientes, tem de ativar os ficheiros de instalação rápida nos clientes na secção de atualizações de Software de definições de cliente. Isto cria um serviço de escuta HTTP novo que escuta pedidos transferir ficheiros de instalação rápida na porta que especificar. Depois de implementar as definições de cliente para ativar esta funcionalidade no cliente, irá tentar transferir as diferenças entre Windows 10 atualização o mês atual cumulativa e a atualização do mês anterior (clientes tem de executar uma versão do Windows 10 que suporta express ficheiros de instalação).
1.    Ative o suporte para ficheiros de instalação rápida nas propriedades do componente de ponto de atualização de Software (procedimento anterior).
2.    Na consola do Configuration Manager, navegue para **administração** > **definições de cliente**.
3.    Selecione as definições de cliente apropriada, em seguida, no **base** separador, clique em **propriedades**.
4.    Selecione o **atualizações de Software** página, configure **Sim** para o **ativar a instalação das atualizações rápida nos clientes** definir e configurar a porta utilizada pelo serviço de escuta de HTTP no cliente para o **porta utilizada para transferir conteúdo para atualizações rápidas** definição.

