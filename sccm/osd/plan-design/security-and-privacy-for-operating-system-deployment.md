---
title: "Segurança e privacidade para implementação do sistema operativo | Documentos do Microsoft"
description: "Saiba mais sobre segurança e privacidade melhores práticas para a implementação de sistemas operativos no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
caps.latest.revision: 6
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: 5632a753fc565312a80b2ed69ce438335b3fad50
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="security-and-privacy-for-operating-system-deployment-in-system-center-configuration-manager"></a>Problemas de segurança e privacidade na implementação do sistema operativo no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico contém informações de privacidade para implementação do sistema operativo no System Center Configuration Manager e segurança.  

##  <a name="BKMK_Security_HardwareInventory"></a>Melhores práticas de segurança para a implementação do sistema operativo  
 Utilize os seguintes procedimentos recomendados de segurança para a implementação de sistemas operativos com o Configuration Manager:  

-   **Implementar controlos de acesso para proteger os suportes de dados**  

     Ao criar suportes de dados de arranque, atribua sempre uma palavra-passe para ajudar a proteger os suportes de dados. No entanto, mesmo com uma palavra-passe, apenas os ficheiros que contêm informações sensíveis são encriptados, e todos os ficheiros podem ser substituídos.  

     Controle o acesso físico ao suporte de dados para impedir que um atacante utilize ataques criptográficos para obter o certificado de autenticação de cliente.  

     Para ajudar a impedir que um cliente instale conteúdo ou adultere a política de cliente, o conteúdo é protegido por hash e tem de ser utilizado com a política original.  Se o hash de conteúdo ou a verificação de que o conteúdo corresponde à política falharem, o cliente não utilizará o suporte de dados de arranque. Só o conteúdo é protegido por hash: a política não é, mas é encriptada e protegida se especificar uma palavra-passe, o que dificulta a modificação da política por um atacante.  

-   **Utilizar uma localização protegida ao criar suportes de dados para imagens do sistema operativo**  

     Se utilizadores não autorizados tiverem acesso à localização, poderão adulterar os ficheiros que criar. Além disso, poderão utilizar todo o espaço disponível no disco, provocando a falha da criação dos suportes de dados.  

-   **Proteja os ficheiros de certificado (. pfx) com uma palavra-passe e se os armazenar na rede, proteja o canal de rede ao importá-los para o Configuration Manager**  

     Exigir uma palavra-passe ao importar o certificado de autenticação de cliente utilizado para os suportes de dados de arranque ajuda a proteger o certificado contra eventuais atacantes.  

     Utilize a assinatura SMB ou IPsec entre a localização de rede e o servidor de site para impedir que um atacante adultere o ficheiro de certificado.  

-   **Se o certificado de cliente for comprometido, bloqueie o certificado do Configuration Manager e revogue-o se se tratar de um certificado PKI**  

     Para implementar um sistema operativo utilizando suportes de dados de arranque e arranque PXE, terá de possuir um certificado de autenticação de cliente com uma chave privada. Se esse certificado for comprometido, bloqueie o certificado no nó **Certificados** da área de trabalho de **Administração**, nó **Segurança**.  

-   **Quando o fornecedor de SMS se encontrar num computador ou computadores que não seja o servidor do site, proteja o canal de comunicação para proteger as imagens de arranque**  

     Quando as imagens de arranque são modificadas e o Fornecedor de SMS se encontra em execução num servidor que não seja o servidor de site, as imagens de arranque estão vulneráveis a ataques. Proteja o canal de rede entre estes computadores utilizando a assinatura SMB ou IPsec.  

-   **Ativar pontos de distribuição para comunicação de cliente PXE apenas em segmentos de rede seguros**  

     Quando um cliente envia um pedido de arranque PXE, não tem nenhuma forma de garantir que o pedido é servido por um ponto de distribuição PXE ativado. Este cenário apresenta os seguintes riscos de segurança:  

    -   Um ponto de distribuição não autorizado que responda a pedidos PXE poderia fornecer uma imagem adulterada aos clientes.  

    -   Um atacante poderia lançar um ataque "man-in-the-middle" contra o protocolo TFTP utilizado pelo PXE e enviar código malicioso juntamente com os ficheiros do sistema operativo, ou criar um cliente não autorizado para fazer pedidos TFTP diretamente ao ponto de distribuição.  

    -   Um atacante poderia utilizar um cliente malicioso para lançar um ataque denial-of-service contra o ponto de distribuição.  

     Utilize defesa em profundidade para proteger os segmentos de rede onde os clientes acederão aos pontos de distribuição para pedidos PXE.  

    > [!WARNING]  
    >  Devido a estes riscos de segurança, não ative um ponto de distribuição para comunicação PXE quando este se encontrar numa rede não fidedigna, tal como uma rede de perímetro.  

-   **Configurar pontos de distribuição com PXE ativado para responder a pedidos PXE apenas em interfaces de rede especificadas**  

     Se permitir que o ponto de distribuição responda a pedidos PXE em todas as interfaces de rede, esta configuração poderá expor o serviço PXE a redes não fidedignas  

-   **Exigir uma palavra-passe para efetuar o arranque PXE**  

     Ao exigir uma palavra-passe para o arranque PXE, esta configuração adiciona um nível de segurança extra ao processo de arranque PXE, para ajudar a salvaguardar contra a adesão de clientes da hierarquia do Configuration Manager.  

-   **Não incluir a linha de aplicações empresariais ou com software que contenham dados confidenciais numa imagem que será utilizada para arranque PXE ou multicast**  

     Dados os riscos de segurança inerentes ao arranque PXE e multicast, reduza os riscos se o computador não autorizado transferir a imagem do sistema operativo.  

-   **Não incluir a linha de aplicações empresariais ou com software que contenha dados confidenciais em pacotes de software que sejam instalados utilizando variáveis de sequências de tarefas**  

     Se implementar pacotes de software utilizando variáveis de sequência de tarefas, o software poderá ser instalado em computadores e para utilizadores que não estejam autorizados a recebê-lo.  

-   **Ao migrar o estado do utilizador, proteger o canal de rede entre o cliente e o ponto de migração de estado utilizando a assinatura SMB ou IPsec**  

     Após a ligação inicial através de HTTP, os dados da migração de estado de utilizador são transferidos utilizando SMB.  Se não proteger o canal de rede, um atacante poderá ler e modificar esses dados.  

-   **Utilizar a versão mais recente do utilizador State Migration Tool (USMT) que suporte do Configuration Manager**  

     A versão mais recente do USMT fornece melhoramentos de segurança e um maior controlo ao migrar dados de estado do utilizador.  

-   **Eliminar manualmente as pastas no ponto de migração de estado quando estas forem desativadas**  

     Quando remove uma pasta de ponto de migração de estado na consola do Configuration Manager no propriedades do ponto de migração de estado, a pasta física não é eliminada. Para proteger os dados da migração de estado de utilizador contra divulgação de informações, terá de remover manualmente a partilha de rede e eliminar a pasta.  

-   **Não configure a política de eliminação para eliminar imediatamente o estado do utilizador**  

     Se configurar a política de eliminação no ponto de migração de estado para remover os dados marcados para eliminação imediata e se um atacante conseguir obter os dados de estado do utilizador antes do computador válido, os dados de estado do utilizador poderão ser imediatamente eliminados. Defina o **Eliminar depois de**  intervalo de modo a ser suficientemente longo para verificar o sucesso do restauro dos dados de estado de utilizador.  

-   **Eliminar manualmente as associações de computadores quando o restauro de dados de migração de estado de utilizador estiver concluído e verificado**  

     Gestor de configuração não remove automaticamente as associações de computadores. Ajude a proteger a identidade dos dados de estado de utilizador eliminando manualmente as associações de computadores que já não sejam necessárias.  

-   **Segurança de copiar manualmente os dados de migração de estado de utilizador no ponto de migração de estado**  

     Cópia de segurança do Configuration Manager não inclui dados de migração de estado do utilizador.  

-   **Lembre-se ativar o BitLocker depois do sistema operativo está instalado**  

     Se um computador suportar o BitLocker, terá de o desativar utilizando um passo de sequência de tarefas, se pretender instalar o sistema operativo em modo automático. O Configuration Manager não ativa o BitLocker depois do sistema operativo está instalado, pelo que tem o reativar manualmente.  

-   **Implementar controlos de acesso para proteger os suportes de dados**  

     Controle o acesso físico ao suporte de dados para impedir que um atacante utilize ataques criptográficos para obter o certificado de autenticação de cliente e dados confidenciais.  

-   **Implementar controlos de acesso para proteger o computador de referência processo de processamento de imagens**  

     Certifique-se de que o computador de referência utilizado para capturar as imagens do sistema operativo se encontra num ambiente seguro, com controlos de acesso adequados, para que não seja possível instalar nem incluir software inesperado ou malicioso na imagem capturada. Ao capturar a imagem, certifique-se de que a localização de partilha de ficheiros na rede de destino é segura, para que não seja possível adulterar a imagem após a respetiva captura.  

-   **Instalar sempre as atualizações de segurança mais recentes no computador de referência**  

     Se o computador de referência tiver as atualizações de segurança mais recentes, isso ajudará a reduzir a janela de vulnerabilidade dos novos computadores durante o primeiro arranque.  

-   **Se tiver de implementar sistemas operativos num computador desconhecido, implemente controlos de acesso para impedir a ligação à rede de computadores não autorizados**  

     Embora o aprovisionamento de computadores desconhecidos constitua um método cómodo para implementar novos computadores a pedido, poderá permitir que um atacante se torne, de forma eficiente, num cliente fidedigno na rede. Limite o acesso físico à rede e monitorize os clientes para detetar computadores não autorizados. Além disso, os computadores que respondam a implementações de sistema operativo iniciadas por PXE poderão ver todos os seus dados destruídos durante a implementação do sistema operativo, o que poderá resultar na redução da disponibilidade dos sistemas que sejam reformatados de forma inadvertida.  

-   **Ativar a encriptação de pacotes multicast**  

     Para cada pacote de implementação do sistema operativo, tem a opção para ativar a encriptação quando o Configuration Manager transfere o pacote utilizando multicast. Esta configuração ajuda a impedir a adesão de computadores não autorizados à sessão multicast e a impedir atacantes de adulterarem a transmissão.  

-   **Monitorizar pontos de distribuição preparados para multicast não autorizados**  

     Se os atacantes conseguirem aceder à rede, poderão configurar servidores multicast não autorizados para falsificar a implementação do sistema operativo.  

-   **Ao exportar sequências de tarefas para uma localização de rede, proteja a localização e o canal de rede**  

     Limite quem pode aceder à pasta de rede.  

     Utilize a assinatura SMB ou IPsec entre a localização de rede e o servidor de site para impedir que um atacante adultere a sequência de tarefas exportada.  

-   **Proteja o canal de comunicação ao carregar um disco rígido virtual no Virtual Machine Manager.**  

     Para impedir a adulteração dos dados quando é transferido através da rede, utilize Internet Protocol security (IPsec) ou bloco de mensagem de servidor (SMB) entre o computador que executa a consola do Configuration Manager e o computador a executar o Virtual Machine Manager.  

-   **Se tiver de utilizar a sequência de conta Run As tarefas, tome precauções de segurança adicionais**  

     Implemente as seguintes medidas de precaução se utilizar a Conta Run As de Sequência de Tarefas:  

    -   Utilize uma conta com o mínimo de permissões necessárias.  

    -   Não utilize a conta de Acesso à Rede para esta conta.  

    -   Nunca torne a conta num administrador do domínio.  

     Além disso:  

    -   Nunca configure perfis itinerantes para essa conta. Quando a sequência de tarefas for executada, transferirá o perfil itinerante para a conta, o que deixará o perfil vulnerável a acesso no computador local.  

    -   Limite o âmbito da conta. Por exemplo, crie Contas Run As de Sequência de Tarefas diferentes para cada sequência de tarefas, de modo a que, se uma conta for comprometida, apenas sejam comprometidos os computadores cliente a que essa conta tenha acesso. Se a linha de comandos exigir acesso administrativo no computador, considere a criação de uma conta de administrador local apenas para a Conta Run As de Sequência de Tarefas em todos os computadores que executarão a sequência de tarefas, eliminando-a assim que deixar de ser necessária.  

-   **Restrinja e monitorize os utilizadores administrativos a quem são concedidos a função de segurança de Gestor de implementação do sistema operativo**  

     Utilizadores administrativos a quem são concedidos a função de segurança de Gestor de implementação do sistema operativo podem criar certificados autoassinados, que podem ser utilizados para representar um cliente e obter a política de cliente do Configuration Manager.  

### <a name="security-issues-for-operating-system-deployment"></a>Problemas de segurança na implementação do sistema operativo  
 Embora a implementação do sistema operativo possa constituir uma forma cómoda de implementar os sistemas operativos e configurações mais seguras em computadores da rede, apresenta os seguintes riscos de segurança:  

-   Divulgação de informações e denial-of-service  

     Se um intruso obtiver o controlo da infraestrutura do Configuration Manager, poderá executar quaisquer sequências de tarefas, que poderão incluir a formatação das unidades de disco rígidas dos computadores cliente. As sequências de tarefas podem ser configuradas para conter informações confidenciais, tais como contas que tenham permissões para aderir ao domínio e chaves de licenciamento em volume.  

-   Representação e elevação de privilégios  

     As sequências de tarefas permitem associar um computador ao domínio, o que poderá fornecer acesso autenticado de rede a um computador não autorizado. Outra consideração de segurança importante na implementação do sistema operativo é a proteção do certificado de autenticação de cliente utilizado para suportes de dados de sequências de tarefas de arranque e para implementação de arranque PXE. Ao capturar um certificado de autenticação de cliente, está a dar oportunidade a um atacante de obter a chave privada do certificado, passando a representar um cliente válido na rede.  

     Se um intruso obtiver o certificado de cliente que é utilizado para suportes de dados de sequência de tarefas de arranque e para implementação de arranque PXE, este certificado pode ser utilizado para representar um cliente válido do Configuration Manager. Neste cenário, o computador não autorizado pode transferir a política, que pode conter dados confidenciais.  

     Se os clientes utilizarem a Conta de Acesso à Rede para aceder a dados armazenados no ponto de migração de estado, estes clientes partilham efetivamente a mesma identidade e podem aceder aos dados de migração de estado de outro cliente que utilize a Conta de Acesso à Rede. Os dados são encriptados para poderem ser lidos apenas pelo cliente original, mas podem ser adulterados ou eliminados.  

-   Autenticação de cliente para o ponto de migração de estado é efetuada através de um token do Configuration Manager que é emitido pelo ponto de gestão.  

     Além disso, o Configuration Manager não limita nem gere o volume de dados que estão armazenados no ponto de migração de estado e um intruso poderia preencher o espaço em disco disponível e causar uma recusa de serviço.  

-   Se utilizar variáveis de coleção, os administradores locais podem ler informações potencialmente confidenciais  

     Embora as variáveis de coleção ofereçam um método flexível de implementar sistemas operativos, isto pode resultar em divulgação de informações.  

##  <a name="BKMK_Privacy_HardwareInventory"></a>Informações de privacidade para implementação do sistema operativo  
 Além de implementar sistemas operativos em computadores sem sistema operativo, Configuration Manager pode ser utilizado para migrar ficheiros e definições de utilizadores de um computador para outro. O administrador configura as informações para transferência, incluindo ficheiros de dados pessoais, definições de configuração e cookies do browser.  

 As informações são armazenadas num ponto de migração de estado e encriptadas durante a transmissão e o armazenamento. As informações podem ser obtidas pelo novo computador associado às informações de estado. Se o novo computador perder a chave para obter as informações, um administrador do Configuration Manager com direito para Ver Informações de Recuperação em objetos de instância da associação do computador pode aceder às informações e associá-las a um novo computador. Depois do restauro das informações de estado pelo computador novo, por predefinição, este elimina os dados ao fim de um dia. Pode configurar o momento de remoção dos dados marcados para eliminação pelo ponto de migração de estado. As informações de migração de estado não são armazenadas na base de dados do site e não são enviadas à Microsoft.  

 Se utilizar o suporte de dados de arranque para implementar imagens do sistema operativo, utilize sempre a opção predefinida para proteger por palavra-passe o suporte de dados de arranque. A palavra-passe encripta todas as variáveis armazenadas na sequência de tarefas, mas informações não armazenadas numa variável poderão ficar sujeitas a divulgação.  

 A implementação do sistema operativo pode utilizar sequências de tarefa para executar muitas tarefas diferentes durante o processo de implementação, que inclui a instalação de aplicações e atualizações de software. Quando configurar sequências de tarefas, também deve estar ciente das implicações de privacidade da instalação de software.  

 Se carregar um disco rígido virtual para o Virtual Machine Manager sem primeiro utilizar o Sysprep para limpar a imagem, o disco rígido virtual carregado pode conter dados pessoais da imagem original.  

 Configuration Manager não implementa a implementação do sistema operativo por predefinição e requer vários passos de configuração para poder recolher informações do Estado de utilizador ou criar sequências de tarefas ou imagens de arranque.  

 Antes de configurar a implementação do sistema operativo, considere os requisitos de privacidade.  

