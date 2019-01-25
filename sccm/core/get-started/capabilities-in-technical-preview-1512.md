---
title: Funcionalidades no Technical Preview 1512
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1512.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e4d9e414-1346-4ed4-85d0-64d602b68731
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 970f86849572d6b360c5b92a42a3d131a38fe1d7
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54896469"
---
# <a name="capabilities-in-technical-preview-1512-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1512 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1512. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](technical-preview.md), para se familiarizar com os requisitos gerais e limitações para a utilização de um Technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos de uma technical preview.  

 Seguem-se os novos recursos, que pode experimentar com esta versão.  

##  <a name="bkmk_devicehealth"></a> Device Health Attestation  
 A partir do Technical Preview 1512, os administradores podem ver o estado do atestado de estado de funcionamento do dispositivo do Windows 10 na consola do Configuration Manager.  Esta funcionalidade está disponível para o Configuration Manager e o Configuration Manager com o Microsoft Intune. O atestado de estado de funcionamento permite ao administrador garantir que o cliente computadores têm fidedignas de BIOS, TPM e as configurações de software de arranque. Para suportar o atestado de estado de funcionamento do dispositivo, dispositivos de cliente devem ter o Win10 com TPM 2 ativado. Atestado de estado de funcionamento do dispositivo apresenta o número de dispositivos ativados para cada um dos seguintes:  

-   Antimalware de início antecipado  

-   BitLocker  

-   Arranque seguro  

-   Integridade do código  

A consola também apresenta a parte superior em falta as definições de atestado de estado de funcionamento com o número de dispositivos.  

Para pré-visualizar a vista de atestado de estado de funcionamento do dispositivo, na consola do Configuration Manager vá para o **monitorização** área de trabalho, clique em **Security** nó e, em seguida, clique **atestado de estado de funcionamento** .  

##  <a name="bkmk_viewterms"></a> A monitorização de termos e condições na consola  
A partir do Technical Preview 1512, ao integrar o Configuration Manager com o Microsoft Intune, pode utilizar a consola do Configuration Manager para ver que utilizadores aceitaram os termos e condições configurados pelo departamento de TI e quais usuários têm não.  

**Para ver informações de resumo:**  

-   Na consola do Configuration Manager, aceda a **monitorização** > **descrição geral** > **implementações** e selecione os termos e condições implementação que pretende visualizar.  

**Para ver informações detalhadas:**  

1.  Na consola do Configuration Manager, aceda a **ativos e compatibilidade** > **descrição geral** > **as definições de compatibilidade**  >   **Termos e condições**e, em seguida, selecione os termos e condições que pretende visualizar.  

2.  Na parte inferior da consola, selecione o **implementações** separador, selecione a implementação e, em seguida, clique em **ver o estado.**  

##  <a name="bkmk_EPpolicy"></a> Melhoramentos às definições de política do Endpoint Protection  
No 1512 Technical Preview adicionámos as seguintes novas definições de política antimalware do Endpoint Protection:  

-   Proteção em tempo real: **Bloquear Aplicações Potencialmente Indesejáveis ao transferir e antes da instalação**  

    -   PUA (Potential Unwanted Applications) é uma classificação de ameaça baseada em reputação e identificação orientada por pesquisa. Normalmente, trata-se de bundlers de aplicações indesejadas ou das respetivas aplicações agregadas.  

    -   A definição de política de proteção está ativada (definida como "Sim") por predefinição. Quando ativada, esta definição bloqueia PUA no momento da transferência e da instalação. No entanto, pode excluir ficheiros ou pastas para satisfazer as necessidades específicas do seu ambiente específicos.  

-   Definições de análise: **Analisar unidades de rede mapeadas ao executar uma análise completa**  

    -   Esta definição proporciona maior granularidade para que o administrador possa permitir análises a pedido dos ficheiros de rede sem o risco de analisar sempre as unidades de rede mapeadas durante uma análise completa agendada.  

    -   A definição **analisar ficheiros de rede** primeiro tem de ser ativado ("Sim") para esta definição esteja disponível para configuração.  

    -   Por predefinição, esta definição é "Não" que significa que uma análise completa não terão acesso às unidades de rede mapeadas.  

-   Definições de submissão de ficheiros de exemplo automática:  

     O motor antimalware pode solicitar os ficheiros de exemplo para ser enviado à Microsoft para análise adicional. Por predefinição, será sempre apresentado um aviso antes de enviar esses exemplos. Os administradores podem agora gerir as seguintes definições para configurar este comportamento:  

    -   Avançado: **Ativar a submissão de ficheiros de exemplo de automática ajudar a determinar se certos itens detetados são maliciosos**:  Altere esta definição como "Sim" para ativar a submissão automática de ficheiros de exemplo. Por predefinição, esta definição é "Não", o que significa que a submissão automática de ficheiros de exemplo está desativada e os utilizadores serão avisados antes de enviarem exemplos.   (Esta definição foi introduzida inicialmente no System Center 2012 R2 Configuration Manager SP1)  

    -   Avançado: **Permitir aos utilizadores modificar definições de submissão automática de ficheiros de exemplo**: Esta definição determina se um utilizador com direitos administrativos locais num dispositivo pode alterar a definição de submissão de ficheiros de exemplo automática na interface do cliente. Por predefinição, esta definição é "Não", o que significa que as definições só podem ser alteradas de dentro da consola do Configuration Manager e os administradores locais num dispositivo não é possível alterar esta configuração.  

         Por exemplo, o código a seguir mostra a definição do Windows Defender no Windows 10, o administrador definiu como ativada e o utilizador não tem permissão para modificá-lo:  

         ![TechRef&#95;WinDefender](../../core/get-started/media/TechRef_WinDefender.png "TechRef_WinDefender")  

    Além disso, o existente **excluir ficheiros e pastas** política de configuração na secção "Definições de exclusão" antimalware do endpoint protection foi melhorada para permitir exclusões de dispositivos. Por exemplo, agora pode especificar o seguinte como exclusão: **\device\mvfs** (em Sistema de Ficheiros com Múltiplas Versões). A política não valida o caminho do dispositivo; a política do endpoint protection é fornecida ao motor antimalware no cliente, que tem de conseguir interpretar a cadeia do dispositivo.  

**Pré-requisitos para utilizar políticas de proteção de ponto final:**  

Antes de poder utilizar as políticas de proteção de ponto final tem de instalar e gerir o cliente do Endpoint Protection utilizando as definições de cliente do Endpoint Protection. Isso é feito com o cliente do System Center Endpoint Protection para Windows 7, Windows 8, Windows 8.1 ou geridos com o Windows Defender para Windows 10. Ver [Endpoint Protection no System Center Configuration Manager](../../protect/deploy-use/endpoint-protection.md).  
