---
title: Guia de utilizador do Centro de software
titleSuffix: Configuration Manager
description: Saiba mais sobre as funções e funcionalidades do Centro de Software
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: ff40af9dd40921b63f8b8bd13ba5c287c3bf9972
ms.sourcegitcommit: e35d07870656eadd29faacc378ecd091ff3bdcfb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 06/07/2018
ms.locfileid: "34848667"
---
# <a name="software-center-user-guide"></a>Guia de utilizador do Centro de software

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Da sua organização administrador de TI utiliza o Centro de Software para instalar aplicações, atualizações de software e atualizar o Windows. Este guia de utilizador explica a funcionalidade do Centro de Software para utilizadores do computador.

### <a name="general-notes-about-software-center-functionality"></a>Notas gerais sobre a funcionalidade do Centro de Software
- Este artigo descreve as funcionalidades mais recentes do Centro de Software. Se a sua organização está a utilizar mais antigo, mas ainda a versão suportada do Centro de Software, nem todas as funcionalidades estão disponíveis. Para obter mais informações, contacte o administrador de TI.
- O administrador de TI pode desativar alguns aspetos do Centro de Software. A experiência específica pode variar.
<!-- - Your IT admin may change the color of Software Center, and add your organization's logo. The images in this article show the default experience. -->



## <a name="how-to-open-software-center"></a>Como abrir o Centro de Software

Para o método mais simples iniciar o Centro de Software num computador Windows 10, prima **iniciar** e tipo `Software Center`. 

Se navegar menu Iniciar, procure no **Microsoft System Center** grupo para o **Centro de Software** ícone.



## <a name="applications"></a>Aplicações

Clique em de **aplicações** separador para localizar e instalar aplicações que implementa o administrador de TI a si ou neste computador.
- **Todos os**: Mostra todas as aplicações que pode instalar o
- **Necessário**: O administrador de TI impõe estas aplicações. Se desinstalar uma destas aplicações, o Centro de Software reinstala-o.
- **Filtros**: O administrador de TI pode criar categorias de aplicações. Se estiver disponível, clique na lista pendente para filtrar a vista para apenas para as aplicações numa categoria específica. Selecione **todos os** para mostrar todas as aplicações.
- **Ordenar por**: Reorganizar a lista de aplicações. Por predefinição, esta lista ordena por **mais recente**.
- **Pesquisa**: Ainda não é possível encontrar aquilo que procura? Introduza as palavras-chave na caixa de pesquisa para encontrá-lo!
-  **A vista de comutador**: Clique nos ícones para mudar a vista entre a vista de lista e o mosaico vista. Por predefinição, a lista de aplicações mostra como mosaicos de gráfico. 
    - Vista em mosaico: O administrador de TI pode personalizar os ícones. A seguir cada mosaico mostra o nome da aplicação, Editor e versão. 
    - Vista de lista: Esta vista apresenta o ícone de aplicação, nome, publicador, versão e o estado. 


### <a name="install-multiple-applications"></a>Instalar várias aplicações 
<!-- 1357126 -->
Instale mais do que uma aplicação numa altura em vez de aguardar um para concluir antes de iniciar a próxima. Nem todas as aplicações qualificam:
- A aplicação está visível para si
- A aplicação não estiver já instalada ou transferir
- O administrador de TI não necessita de aprovação para instalar a aplicação

Para instalar mais do que uma aplicação num momento:
 1. Para introduzir o modo selecionar vários na vista de lista, clique no ícone selecionar vários ![Ícone de seleção múltipla do Centro de software](media/software-center-multi-select-apps.png) no canto superior direito.
 2. Selecione a instalação clicando na caixa de verificação à esquerda das aplicações na lista de dois ou mais aplicações.
 3. Clique em de **instalar selecionado** botão.

As aplicações instalar como normal, apenas agora sucessivamente.




## <a name="updates"></a>Atualizações

Clique em de **atualizações** separador para ver e instalar atualizações de software que implementa o administrador de TI a este computador.  
- **Todos os**: Mostra todas as atualizações que podem instalar
- **Necessário**: O administrador de TI impõe estas atualizações.
- **Ordenar por**: Reorganizar a lista de atualizações. Por predefinição, esta lista ordena por **nome da aplicação: À Z**.

Para instalar atualizações, clique em **instalar todas as**.

Para instalar apenas atualizações específicas, clique no ícone para selecionar vários em modo. Verifique as atualizações a instalar e, em seguida, clique em **instalar selecionado**.



## <a name="operating-systems"></a>Sistemas Operativos

Clique em de **sistemas operativos** separador para ver e instalar as versões do Windows que o administrador de TI implementa neste computador.  
- **Todos os**: Mostra todas as versões do Windows que pode instalar
- **Necessário**: O administrador de TI impõe estas atualizações.
- **Ordenar por**: Reorganizar a lista de atualizações. Por predefinição, esta lista ordena por **nome da aplicação: À Z**.



## <a name="installation-status"></a>Estado da instalação

Clique em de **estado da instalação** separador para ver o estado das aplicações. Poderá ver os seguintes Estados:
- **Instalado**: Centro de software instalados esta aplicação neste computador.
- **Transferir**: Centro de software está a transferir o software para instalar este computador.
- **Não foi possível**: Centro de software encontrou um erro na tentar instalar o software.



## <a name="device-compliance"></a>Conformidade do dispositivo

Clique em de **conformidade do dispositivo** separador para ver o estado de conformidade deste computador.

Clique em **verificar conformidade** para avaliar definições este dispositivo com as políticas de segurança definidas pelo administrador de TI.



## <a name="options"></a>Opções

Clique em de **opções** separador para ver as definições adicionais para este computador.

### <a name="work-information"></a>Informação de trabalho

Indique as horas que trabalha normalmente. O administrador de TI pode agendar instalações de software fora das horas de expediente. Permitir, pelo menos, quatro horas diárias para sistema tarefas de manutenção. O administrador de TI ainda pode instalar aplicações críticas e atualizações de software durante o horário comercial.

- Clique nas listas de lista pendente para selecionar as horas mais antigo e mais recentes que utilize este computador. Por predefinição, estes valores são de **5 AM** através de **as 22: 00**

- Selecione a caixa de verificação junto as dias da semana é normalmente utilizada neste computador. Centro de software apenas seleciona os dias da semana por predefinição.  


### <a name="power-management"></a>Gestão de energia

O administrador de TI pode definir políticas de gestão de energia. Estas políticas ajudam a sua organização poupar eletricidade quando este computador não está em utilização. 

Para tornar este computador excluídos estas políticas, selecione a caixa de verificação **não aplicar as definições de energia do departamento de TI a este computador**. Esta definição está desativada por predefinição; o computador aplica-se as definições de energia. 


### <a name="computer-maintenance"></a>Manutenção do computador

Especifique como o Centro de Software aplica as alterações ao software antes do prazo
- **Instalar ou desinstalar o software necessário e automaticamente reiniciar o computador apenas fora das horas de expediente especificadas**: Esta definição está desativada por predefinição.
- **Suspender as atividades do Centro de Software quando o computador está em modo de apresentação**: Esta definição está ativada por predefinição.
- **Sincronizar política**: clicar neste botão quando indicado pelo seu administrador de TI. Este computador verifica com os servidores para tudo o novo, como aplicações, atualizações de software ou sistemas operativos.

