---
title: Manual do utilizador do Centro de Software
titleSuffix: Configuration Manager
description: Saiba mais sobre os recursos e funcionalidades do Centro de Software
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.collection: M365-identity-device-management
ms.openlocfilehash: da01c741107d4eb4a707f7f0d8ada5d82706f292
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56119896"
---
# <a name="software-center-user-guide"></a>Manual do utilizador do Centro de Software

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Da sua organização utiliza o administrador de TI Centro de Software para instalar aplicativos, atualizações de software e atualizar o Windows. Este guia de utilizador explica a funcionalidade do Centro de Software para usuários do computador.

### <a name="general-notes-about-software-center-functionality"></a>Observações gerais sobre a funcionalidade do Centro de Software
- Este artigo descreve as funcionalidades mais recentes do Centro de Software. Se sua organização está a utilizar mais antigo, mas ainda uma versão suportada do Centro de Software, nem todas as funcionalidades estão disponíveis. Para obter mais informações, contacte o administrador de TI.
- O administrador de TI pode desabilitar alguns aspectos do Centro de Software. Sua experiência específica pode variar.
<!-- - Your IT admin may change the color of Software Center, and add your organization's logo. The images in this article show the default experience. -->



## <a name="how-to-open-software-center"></a>Como abrir o Centro de Software

Para o método mais simples iniciar o Centro de Software num computador Windows 10, prima **começar** e escreva `Software Center`. 

Se navegar do menu Iniciar, procure no **Microsoft System Center** grupo para o **Centro de Software** ícone.



## <a name="applications"></a>Aplicações

Clique nas **aplicativos** separador para localizar e instalar aplicações que o administrador de TI implementa a si ou neste computador.
- **Todos os**: Mostra todas as aplicações que é possível instalar
- **Necessário**: O administrador de TI impõe esses aplicativos. Se desinstalar um desses aplicativos, o Centro de Software irá reinstalá-lo.
- **Filtros**: O administrador de TI pode criar categorias de aplicativos. Se estiver disponível, clique na lista pendente para filtrar a vista para apenas para as aplicações numa categoria específica. Selecione **todos os** para mostrar todas as aplicações.
- **Ordenar por**: Reorganizar a lista de aplicações. Por predefinição, esta lista ordena por **mais recente**.
- **Pesquisa**: Ainda não é possível localizar o que está procurando? Introduza palavras-chave na caixa de pesquisa para encontrá-lo!
-  **Alterne a exibição**: Clique nos ícones para mudar o modo de exibição entre a vista de lista e o mosaico da vista. Por predefinição, a lista de aplicativos mostra como mosaicos do gráficos. 
    - Vista de mosaico: O administrador de TI pode personalizar os ícones. Veja a seguir cada mosaico mostra o nome da aplicação, publicador e versão. 
    - Vista de lista: Esta vista apresenta o ícone de aplicação, nome, publicador, versão e o estado. 


### <a name="install-multiple-applications"></a>Instalar várias aplicações 
<!-- 1357126 --> Instale mais de um aplicativo ao mesmo tempo, em vez de aguardar que uma seja concluída antes de iniciar a próxima. Nem todos os aplicativos qualificam:
- A aplicação está visível para si
- A aplicação não estiver instalado ou transferir
- O administrador de TI não requer a aprovação para instalar a aplicação

Para instalar mais de um aplicativo por vez:
 1. Para entrar no modo de seleção múltipla na vista de lista, clique no ícone de seleção múltipla ![Ícone de seleção múltipla de centro de software](media/software-center-multi-select-apps.png) no canto superior direito.
 2. Selecione duas ou mais aplicações para instalar clicando na caixa de verificação à esquerda das aplicações na lista.
 3. Clique nas **instalar selecionadas** botão.

As aplicações instalam normalmente, apenas agora consecutivas.




## <a name="updates"></a>Atualizações

Clique nas **atualizações** separador para ver e instalar atualizações de software que implementa o seu administrador de TI neste computador.  
- **Todos os**: Mostra todas as atualizações que é possível instalar
- **Necessário**: O administrador de TI aplica essas atualizações.
- **Ordenar por**: Reorganizar a lista de atualizações. Por predefinição, esta lista ordena por **nome da aplicação: À Z**.

Para instalar atualizações, clique em **instalar todos os**.

Para instalar apenas atualizações específicas, clique no ícone para entrar no modo de seleção múltipla. Verificar as atualizações a instalar e, em seguida, clique em **instalar selecionadas**.



## <a name="operating-systems"></a>Sistemas Operativos

Clique nas **sistemas operativos** separador para ver e instalar as versões do Windows que implementa o seu administrador de TI neste computador.  
- **Todos os**: Mostra todas as versões do Windows que pode instalar
- **Necessário**: O administrador de TI aplica essas atualizações.
- **Ordenar por**: Reorganizar a lista de atualizações. Por predefinição, esta lista ordena por **nome da aplicação: À Z**.



## <a name="installation-status"></a>Estado da instalação

Clique nas **estado de instalação** separador para ver o estado das aplicações. Pode ver os seguintes Estados:
- **Instalado**: Centro de software já instalado esta aplicação neste computador.
- **Baixar o**: Centro de software está a transferir o software a ser instalado neste computador.
- **Falha ao**: Centro de software encontrou um erro em tentar instalar o software.
- **Agendado para instalar após**: Mostra a data e hora da próxima janela de manutenção do dispositivo para instalar software futura. Janelas de manutenção são definidas pelo administrador de TI.<!--1358131-->
    - O estado pode ser visto na **todos os** e o **futuras** separador. 
    - Pode instalar antes da hora de janela de manutenção ao clicar o **instalar agora** botão. 

O administrador de TI permite-lhe ver as aplicações a partir do site do catálogo de aplicações. Para ver o site, clique em **abrir o web site do catálogo de aplicações** no canto superior direito. <!--1358214-->

## <a name="device-compliance"></a>Conformidade do dispositivo

Clique nas **conformidade do dispositivo** separador para ver o estado de conformidade deste computador.

Clique em **verificação de conformidade** para avaliar as definições deste dispositivo com as diretivas de segurança definidas pelo administrador de TI.



## <a name="options"></a>Opções

Clique nas **opções** separador para ver as definições adicionais para este computador.

### <a name="work-information"></a>Informação de trabalho

Indica as horas que normalmente de trabalhar. O administrador de TI pode agendar instalações de software fora das horas de expediente. Permita tarefas de manutenção, pelo menos, quatro horas diárias para o sistema. O administrador de TI ainda pode instalar aplicações críticas e atualizações de software durante o horário comercial.

- Clique nas listas pendentes para selecionar as horas de primeiras e mais recente que utilize este computador. Por predefinição, estes valores são partir **5 AM** através de **10 PM**

- Selecione a caixa de verificação junto aos dias da semana, geralmente usa neste computador. Centro de software seleciona apenas os dias da semana por padrão.  


### <a name="power-management"></a>Gestão de energia

O administrador de TI pode definir políticas de gestão de energia. Estas políticas ajudam a sua organização economizar eletricidade quando este computador não está em utilização. 

Para tornar este computador excluídos destas políticas, selecione a caixa de verificação **não se aplicam as definições de energia do departamento de TI a este computador**. Esta definição estiver desativada por padrão. o computador aplica-se as definições de energia. 


### <a name="computer-maintenance"></a>Manutenção do computador

Especifique como o Centro de Software aplica as alterações ao software antes do prazo
- **Instalar ou desinstalar o software obrigatório e automaticamente reiniciar o computador apenas fora da horas de expediente especificadas**: Esta definição está desativada por predefinição.
- **Suspender as atividades do Centro de Software quando o computador estiver em modo de apresentação**: Esta definição está ativada por predefinição.
- **Sincronizar política**: clicar neste botão quando instruído pelo seu administrador de TI. Neste computador verifica com os servidores de qualquer coisa nova, como aplicações, atualizações de software ou sistemas operativos.

## <a name="custom-tab-in-software-center"></a>Guia personalizada no Centro de Software
O administrador de TI pode ter adicionado uma guia adicional ao centro de Software. Este separador é chamado pelo seu administrador e leva a um web site que especificam. Por exemplo, pode ter uma guia chamada "Técnico" que leva ao site de web de suporte técnico de ajuda da sua organização. <!--1358132-->
