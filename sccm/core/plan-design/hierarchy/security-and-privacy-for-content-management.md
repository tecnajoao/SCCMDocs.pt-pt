---
title: Gestão de conteúdo de segurança e privacidade
titleSuffix: Configuration Manager
description: Otimize a segurança e privacidade para gestão de conteúdos no System Center Configuration Manager.
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d82af132cc6ba60a459d9872cf76f69adc00daa6
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32334655"
---
# <a name="security-and-privacy-for-content-management-for-system-center-configuration-manager"></a>Segurança e privacidade para gestão de conteúdo no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico contém informações de segurança e privacidade para gestão de conteúdos no System Center Configuration Manager. Leia-o em conjunto com os seguintes tópicos:  

-   [Segurança e privacidade para gestão de aplicações no System Center Configuration Manager](../../../apps/plan-design/security-and-privacy-for-application-management.md)  

-   [Segurança e privacidade para atualizações de software no System Center Configuration Manager](/sccm/sum/plan-design/security-and-privacy-for-software-updates)  

-   [Segurança e privacidade para implementação do sistema operativo no System Center Configuration Manager](../../../osd/plan-design/security-and-privacy-for-operating-system-deployment.md)  

##  <a name="BKMK_Security_ContentManagement"></a> Melhores práticas de segurança para gestão de conteúdo  
 Utilize os seguintes procedimentos recomendados de segurança para gestão de conteúdo:  

 **Para pontos de distribuição na intranet, considere as vantagens e desvantagens da utilização de HTTPS e HTTP**: Na maioria dos cenários, a utilização de contas de acesso HTTP e o pacote para autorização fornece mais segurança ao através de HTTPS com encriptação, mas sem autorização. No entanto, se o conteúdo incluir dados confidenciais que pretende encriptar durante a transferência, utilize o HTTPS.  

-   **Quando utilizar o HTTPS para um ponto de distribuição**, o Configuration Manager não utiliza contas de acesso de pacotes para autorizar o acesso ao conteúdo, mas o conteúdo é encriptado quando é transferido através da rede.  

-   **Se utilizar HTTP para um ponto de distribuição**, pode utilizar contas de acesso aos pacotes para autorização, mas o conteúdo não é encriptado quando é transferido através da rede.  


**Se utilizar um certificado de autenticação de cliente PKI em vez de um certificado autoassinado para o ponto de distribuição, proteja o ficheiro de certificado (.pfx) com uma palavra-passe segura. Se armazenar o ficheiro na rede, proteja o canal de rede quando importar o ficheiro para o Configuration Manager**: Ao exigir uma palavra-passe para importar o certificado de autenticação de cliente que o ponto de distribuição utiliza para comunicar com pontos de gestão, ajuda a proteger o certificado de um atacante. Utilize a assinatura de bloco de mensagem de servidor (SMB) ou IPsec entre a localização de rede e o servidor do site para impedir que um atacante adultere o ficheiro de certificado.  

**Remover a função de ponto de distribuição do servidor do site**: Por predefinição, um ponto de distribuição está instalado no mesmo servidor que o servidor do site. Os clientes não precisam de comunicar diretamente com o servidor do site; por conseguinte, para reduzir a superfície de ataque, atribua a função do ponto de distribuição a outros sistemas de sites e remova-a do servidor do site.  

**Proteger o conteúdo ao nível de acesso do pacote**: A partilha do ponto de distribuição permite o acesso de leitura a todos os utilizadores. Para restringir os utilizadores que podem aceder ao conteúdo, utilize contas de acesso aos pacotes quando o ponto de distribuição estiver configurado para HTTP. Não é aplicável aos pontos de distribuição baseados na nuvem, que não suportam contas de acesso do pacote. Para obter mais informações sobre as contas de acesso de pacotes, consulte [gerir contas para aceder ao conteúdo](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).


**Se o Configuration Manager instala o IIS quando adicionar uma função de sistema de sites de ponto de distribuição, remova o redirecionamento de HTTP ou ferramentas e Scripts de gestão do IIS quando a instalação do ponto de distribuição estiver concluída**: O ponto de distribuição não necessita de redirecionamento de HTTP ou ferramentas e Scripts de gestão do IIS. Para reduzir a superfície de ataque, remova estes serviços de função para a função do servidor Web (IIS).  Para obter mais informações sobre os serviços de função para a função de servidor (IIS) web para pontos de distribuição, consulte [Site e os pré-requisitos de sistema de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  

**Definir as permissões de acesso do pacote ao criar o pacote**: Porque as alterações às contas de acesso nos ficheiros do pacote só terão efeitas quando redistribuir o pacote, defina o pacote de permissões de acesso cuidadosamente quando criar primeiro o pacote. Isto é especialmente importante quando o pacote é grande ou está distribuído por muitos pontos de distribuição e quando a capacidade de largura de banda de rede para a distribuição de conteúdo é limitada.  

**Implementar controlos de acesso para proteger os suportes de dados que contém conteúdo pré-configurado**: Conteúdo pré-configurado está comprimido, mas não encriptado. Um atacante poderia ler e modificar os ficheiros que, em seguida, são transferidos para dispositivos. Clientes do Configuration Manager rejeitar conteúdo adulterado, mas ainda o transferem.  

**Importe o conteúdo pré-configurado utilizando apenas a linha de comandos ferramenta ExtractContent (ExtractContent.exe) fornecida com o Configuration Manager e certifique-se de que está assinado pela Microsoft**: Para evitar a adulteração e a elevação de privilégios, utilize apenas a linha de comandos ferramenta autorizada que é fornecida com o Configuration Manager.  

**Proteja o canal de comunicação entre o servidor do site e a localização de origem do pacote**: Utilize IPsec ou assinatura SMB entre o servidor de site e a localização de origem do pacote ao criar aplicações e pacotes. Isto ajuda a impedir que um intruso adultere os ficheiros de origem.  

**Se alterar a opção de configuração do site para utilizar um Web site personalizado em vez de Web site predefinido, depois de instalar quaisquer funções de ponto de distribuição, remova os diretórios virtuais predefinidos**: Quando muda do Web site predefinido para um Web site personalizado, o Configuration Manager não remove os diretórios virtuais antigos. Remova os diretórios virtuais que o Configuration Manager originalmente criado no Web site predefinido:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  

**Para pontos de distribuição baseado na nuvem, proteja os detalhes da subscrição e certificados**: Quando utiliza pontos de distribuição baseado na nuvem, proteja os itens de valor elevado, incluindo o nome de utilizador e palavra-passe da sua subscrição do Azure, o certificado de gestão do Azure e o certificado de serviço do ponto de distribuição baseado na nuvem. Armazene os certificados de forma segura e se os procurar através da rede quando configurar o ponto de distribuição baseado na nuvem, utilize o IPsec ou a assinatura SMB entre o servidor do site e a localização de origem.  

**Para pontos de distribuição baseado na nuvem: Para continuidade do serviço, monitorize a data de expiração dos certificados**: O Configuration Manager não avisar quando os certificados importados para a gestão de distribuição baseado na nuvem ponto dos serviços está prestes a expirar. Tem de monitorizar as datas de expiração independentemente do Configuration Manager e certifique-se de que renova e importa os novos certificados antes da data de expiração. Isto é especialmente importante se adquirir um Gestor de configuração baseado na nuvem do ponto de distribuição certificado do serviço de uma autoridade de certificação externa (AC), pois pode necessitar de mais tempo para obter um certificado renovado.  

 Se um dos certificados expirar, o Gestor de serviços em nuvem gera o ID de mensagem de estado **9425** e o ficheiro de CloudMgr.log contém uma entrada que indica que o certificado **está no estado expirado**, com a data de expiração também registada em UTC.  

## <a name="security-considerations-for-content-management"></a>Considerações de segurança para gestão de conteúdo  
Quando planear a gestão de conteúdo, considere o seguinte:  

-   Os clientes não validam o conteúdo até após a transferência.  

     Clientes do Configuration Manager validam o hash do conteúdo após a transferência para a respetiva cache do cliente. Se um intruso adulterar a lista de ficheiros para transferir ou com o próprio conteúdo, o processo de transferência pode demorar algum tempo considerável largura de banda, apenas para o cliente rejeite o conteúdo quando encontrar o hash inválido.  

-   Quando utiliza pontos de distribuição baseado na nuvem, o acesso ao conteúdo é restringe-se automaticamente à sua empresa e não pode restringi-la utilizadores ou grupos selecionados.  

-   Quando utiliza pontos de distribuição baseado na nuvem, os clientes são autenticados pelo ponto de gestão e, em seguida, utilizam um token do Configuration Manager para aceder a pontos de distribuição baseado na nuvem. O token é válido para oito horas. Isto significa que, se bloquear um cliente porque já não é fidedigno, este pode continuar a transferir conteúdo de um ponto de distribuição baseado na cloud, até que o período de validade do token expirou. Neste momento, o ponto de gestão não irá emitir outro token para o cliente, porque o cliente está bloqueado.  

     Para evitar que um cliente bloqueado Transfira conteúdo durante este período de hora de oito, pode parar o serviço em nuvem no **nuvem** nó, **configuração da hierarquia**, no **administração** área de trabalho na consola do Configuration Manager.  

##  <a name="BKMK_Privacy_ContentManagement"></a> Informações de privacidade da gestão de conteúdo  
 O Configuration Manager não inclui quaisquer dados de utilizador nos ficheiros de conteúdo, embora um utilizador administrativo possa optar por fazê-lo.  

 Antes de configurar a gestão de conteúdo, considere os requisitos de privacidade.  
