# Criando e Configurando sua Primeira Máquina Virtual na Azure - Guia para Iniciantes (e Além!)
Guia Passo a Passo para Usuários de Azure.
Introdução: Desvendando o Poder das VMs na Nuvem Azure

Se você está começando sua jornada na nuvem ou buscando consolidar seus conhecimentos, entender como criar e configurar máquinas virtuais (VMs) na Azure é um passo fundamental. Uma VM na nuvem é essencialmente um computador virtualizado rodando nos data centers da Microsoft, oferecendo flexibilidade, escalabilidade e uma vasta gama de opções para suas necessidades computacionais. Este guia foi elaborado para te conduzir desde os primeiros cliques até as configurações mais avançadas, garantindo que você compreenda os conceitos chave e as melhores práticas para suas implementações na Azure.

Passo 1: Acesso ao Portal do Azure - Sua Central de Comando

O primeiro passo para criar sua VM é acessar o Portal do Azure. Pense nele como o painel de controle centralizado para todos os seus recursos na Azure.
    Abra seu navegador preferido e navegue até https://portal.azure.com/.
    Faça login com sua conta Microsoft (a mesma que você utiliza para outros serviços Microsoft, como Outlook ou Xbox Live, ou a conta que você criou ao se inscrever na Azure).
    Se esta for sua primeira vez, você verá um painel inicial com diversas opções. Para começar a criar sua VM, procure pelo serviço de Máquinas Virtuais. Você pode encontrá-lo na barra de pesquisa no topo ou no menu de serviços.

Passo 2: Criando sua Primeira Máquina Virtual - O Nascimento da sua VM

Com o serviço de Máquinas Virtuais selecionado, vamos ao processo de criação:
    Clique no botão + Criar e selecione Máquina virtual. Isso abrirá a tela de configuração da sua nova VM.
    Detalhes do Projeto:
        Grupo de recursos: Um grupo de recursos é um contêiner lógico que agrupa seus recursos relacionados na Azure. Se você já tem um, pode selecioná-lo no menu suspenso. Caso contrário, clique em Criar novo e dê um nome descritivo ao seu grupo de recursos (por exemplo, meu-projeto-web). Organizar seus recursos em grupos facilita o gerenciamento, a aplicação de políticas e o controle de custos.
        Nome da máquina virtual: Escolha um nome único e fácil de identificar para sua VM (por exemplo, web-server-01).
    Detalhes da Instância:
        Região: Aqui, você seleciona a localização geográfica onde sua VM será provisionada. Essa escolha é crucial! A região afeta a latência (tempo de resposta) para seus usuários, a disponibilidade de serviços e, em alguns casos, o custo. Escolha uma região que esteja geograficamente próxima aos seus usuários ou a outros serviços que sua VM precisará interagir. Mais adiante, discutiremos as zonas de disponibilidade dentro de algumas regiões.
        Zonas de disponibilidade: Se a região selecionada suportar zonas de disponibilidade, você poderá escolher uma ou mais zonas para aumentar a resiliência da sua aplicação. Zonas de disponibilidade são data centers fisicamente separados dentro de uma região da Azure. Ao distribuir suas VMs por diferentes zonas, você se protege contra falhas em um data center específico. Se você está começando, pode deixar essa opção como padrão, mas lembre-se dela para futuras implementações mais críticas.
        Opções de disponibilidade: Este é um ponto chave para garantir a continuidade do seu serviço. A Azure oferece diferentes opções:
           
  Conjuntos de disponibilidade: Agrupa duas ou mais VMs para proteger sua aplicação contra falhas de hardware planejadas (manutenção da Azure) e não planejadas. As VMs em um conjunto de disponibilidade são distribuídas por diferentes domínios de falha (racks de servidores) e domínios de atualização (grupos de servidores que são reinicializados ao mesmo tempo durante a manutenção). Para cargas de trabalho de produção, é altamente recomendado usar conjuntos de disponibilidade.
          
  Conjuntos de escala de máquinas virtuais: Permitem criar e gerenciar um grupo de VMs idênticas com balanceamento de carga automático. São ideais para cargas de trabalho que precisam escalar dinamicamente (aumentar ou diminuir o número de VMs com base na demanda).
           
  Zonas de disponibilidade (já mencionadas): Oferecem a maior resiliência, protegendo contra falhas em data centers inteiros dentro de uma região.
            Sem redundância de infraestrutura necessária: Opção mais básica, sem proteção adicional contra falhas de hardware. Adequada para ambientes de desenvolvimento ou testes não críticos.
       
  Imagem: Aqui você escolhe o sistema operacional e, opcionalmente, o software pré-instalado para sua VM. A Azure Marketplace oferece uma vasta seleção de imagens, incluindo diversas distribuições Linux (Ubuntu, CentOS, Red Hat), Windows Server e imagens com aplicações populares (como servidores web, bancos de dados, etc.). Para iniciantes, uma imagem popular como "Ubuntu Server LTS" ou "Windows Server Standard" é um bom ponto de partida.
        Tamanho: Define as especificações de hardware da sua VM, como o número de vCPUs, a quantidade de memória RAM e o desempenho da rede. A escolha do tamanho impacta diretamente no custo e no desempenho da sua VM. A Azure oferece uma grande variedade de tamanhos otimizados para diferentes tipos de cargas de trabalho (computação intensiva, memória intensiva, armazenamento otimizado, etc.). Para começar, um tamanho da série "B" (Burstable) ou "D" (General Purpose) pode ser adequado para cargas de trabalho leves ou de desenvolvimento. Clique em "Ver todos os tamanhos" para explorar as opções e seus custos estimados por hora. Preste atenção nas DTUs (Database Transaction Units) ou ACUs (Azure Compute Units) como métricas de desempenho.
   
  Conta de Administrador:
        Tipo de autenticação: Você pode escolher entre autenticação por senha ou por chave SSH (Secure Shell). Para iniciantes em Linux, a senha pode parecer mais familiar, mas a chave SSH é mais segura para ambientes de produção. Para Windows, a senha é o método padrão.
        Nome de usuário: Escolha um nome de usuário para a conta de administrador da sua VM.
        Senha: Se você escolheu autenticação por senha, crie uma senha forte e segura. Guarde essa informação em um local seguro!
        Chave pública SSH: Se você escolheu chave SSH, você precisará fornecer sua chave pública. Se você não tem um par de chaves SSH, precisará gerá-lo (há tutoriais para isso em diversos sistemas operacionais). A chave privada correspondente será usada para se conectar à sua VM via SSH.
    
  Regras de porta de entrada (firewall):
        Aqui, você configura quais portas de rede estarão abertas para acesso externo à sua VM. Por padrão, a porta 3389 (RDP para Windows) e a porta 22 (SSH para Linux) podem ser oferecidas para acesso remoto. É crucial revisar e restringir essas portas por motivos de segurança. Se você pretende hospedar um site na sua VM, precisará abrir as portas 80 (HTTP) e/ou 443 (HTTPS). Você pode configurar essas regras agora ou posteriormente através do Network Security Group (NSG) associado à sua VM. Recomenda-se fortemente configurar um NSG para gerenciar o tráfego de rede.
  
  Discos:
        A Azure cria um disco de sistema operacional para sua VM por padrão. Você pode configurar o tipo de disco (SSD Premium, SSD Standard, HDD Standard). Para cargas de trabalho de produção, SSD Premium oferece o melhor desempenho. SSD Standard é uma opção mais econômica para cargas de trabalho menos exigentes. HDD Standard é adequado para armazenamento de dados não críticos.
        Você também pode adicionar discos de dados adicionais para armazenar seus aplicativos e dados.
   
  Redes:
        A Azure cria uma rede virtual (VNet) e uma sub-rede padrão para você. Você pode usar essas configurações padrão para começar ou personalizar sua rede.
        Endereço IP público: Você pode escolher se sua VM terá um endereço IP público (para acesso direto da internet). Para servidores web ou VMs que precisam ser acessadas publicamente, um IP público é necessário. Você pode escolher entre um IP dinâmico (que pode mudar ao reiniciar a VM) ou um IP estático (que permanece o mesmo). Para serviços que precisam ser consistentemente acessíveis, um IP estático é recomendado.
        Network Security Group (NSG): Como mencionado anteriormente, um NSG atua como um firewall para sua VM, controlando o tráfego de entrada e saída. A Azure pode criar um NSG básico para você com as portas que você abriu na seção de regras de porta de entrada. É fundamental revisar e configurar as regras do seu NSG para garantir a segurança da sua VM.
    Gerenciamento:
        Aqui você pode configurar opções como diagnóstico de inicialização (para ajudar a solucionar problemas de inicialização), identidade gerenciada (para permitir que sua VM se autentique em outros serviços Azure sem precisar gerenciar credenciais), e outras configurações avançadas. Para iniciantes, as configurações padrão geralmente são suficientes.
    Avançado:
        Permite configurações mais específicas, como extensões (para instalar software e configurar sua VM após a criação), dados personalizados (scripts que são executados na primeira inicialização), e configurações de proximidade (para reduzir a latência entre recursos).
    Etiquetas:
        As etiquetas são pares de chave-valor que você pode atribuir aos seus recursos Azure para organização, relatórios de custos e gerenciamento. É uma boa prática usar etiquetas consistentes. Por exemplo, Environment: Production, Application: WebServer.
    Revisar + criar:
        Antes de criar sua VM, revise todas as configurações. A Azure mostrará um resumo e o custo estimado por hora da sua VM.
        Clique em Criar para iniciar o processo de provisionamento. A criação da VM pode levar alguns minutos. Você poderá acompanhar o progresso na seção de notificações do portal.

Passo 3: Conectando-se à sua Máquina Virtual

Após a criação da sua VM, você precisará se conectar a ela para configurá-la e executar seus aplicativos.
    Para VMs Windows: Utilize a Conexão de Área de Trabalho Remota (RDP).
        No portal do Azure, navegue até sua VM.
        Clique em Conectar e selecione RDP.
        Um arquivo .rdp será baixado. Abra este arquivo e siga as instruções. Você será solicitado a inserir o nome de usuário e a senha que você definiu durante a criação da VM.
    Para VMs Linux: Utilize um cliente SSH (como o Terminal no macOS/Linux ou PuTTY no Windows).
        No portal do Azure, navegue até sua VM e anote o endereço IP público.
        Abra seu cliente SSH e conecte-se usando o seguinte comando (substitua <seu-usuario> pelo nome de usuário e <seu-ip-publico> pelo IP da sua VM): 
      
        ssh <seu-usuario>@<seu-ip-publico>

  Se você usou autenticação por senha, será solicitado a inserir sua senha. Se usou chave SSH, a conexão será estabelecida usando sua chave privada.

Passo 4: Considerações Essenciais - SLA, Tempo de Inatividade, Segurança e Mais

Criar a VM é apenas o começo. Para garantir que sua aplicação seja confiável, segura e com bom desempenho, é crucial entender os seguintes aspectos:
Acordo de Nível de Serviço (SLA)

O SLA (Service Level Agreement) é um contrato formal entre você e a Microsoft que define as garantias de desempenho e disponibilidade dos serviços Azure. Para máquinas virtuais, o SLA varia dependendo das opções de disponibilidade que você escolher:

   VM única: Sem nenhuma opção de disponibilidade configurada, o SLA para uma única instância de máquina virtual com pelo menos dois discos de dados anexados é de 99,9% de tempo de atividade. Isso significa que, em um mês, sua VM pode ficar indisponível por aproximadamente 43 minutos.
    Conjuntos de disponibilidade: Ao implantar duas ou mais VMs em um conjunto de disponibilidade, o SLA aumenta para 99,95% de tempo de atividade para todas as VMs no conjunto. Isso reduz o tempo de inatividade potencial para cerca de 21 minutos por mês.
    Zonas de disponibilidade: Ao implantar duas ou mais VMs em diferentes zonas de disponibilidade dentro de uma mesma região, o SLA é de 99,99% de tempo de atividade. Isso representa um tempo de inatividade potencial de menos de 5 minutos por mês.

É fundamental escolher a opção de disponibilidade que se alinha aos requisitos de criticidade da sua aplicação. Para ambientes de produção com alta demanda por disponibilidade, conjuntos de disponibilidade ou zonas de disponibilidade são essenciais.
Tempo de Inatividade (Downtime)

O tempo de inatividade é o período em que sua VM não está disponível. Ele pode ocorrer devido a:

  Manutenção planejada: A Azure ocasionalmente realiza manutenção em sua infraestrutura. Ao usar conjuntos de disponibilidade ou zonas de disponibilidade, a Azure garante que as atualizações não afetem todas as suas VMs simultaneamente.
    Falhas não planejadas: Podem ocorrer falhas de hardware, software ou rede. As opções de alta disponibilidade ajudam a mitigar o impacto dessas falhas.
    Erros de configuração: Configurações incorretas na sua VM ou nos serviços relacionados podem levar a interrupções.

Para minimizar o tempo de inatividade:

  Utilize opções de alta disponibilidade (conjuntos de disponibilidade ou zonas de disponibilidade).
  Implemente balanceamento de carga para distribuir o tráfego entre várias VMs, garantindo que se uma VM falhar, outras possam continuar atendendo às solicitações.
  Configure monitoramento e alertas para detectar problemas proativamente e tomar medidas corretivas antes que causem interrupções. O Azure Monitor é uma ferramenta poderosa para isso.
  Planeje e teste procedimentos de recuperação de desastres, como backups regulares e a capacidade de restaurar suas VMs em outra região em caso de falha regional.

Detalhes da Instância (Tamanho da VM)

A escolha do tamanho da instância da sua VM é crucial para o desempenho e o custo. Considere os seguintes fatores:

  Requisitos da sua carga de trabalho: Qual a demanda de CPU, memória, disco e rede da sua aplicação? Monitore o uso de recursos da sua VM para identificar gargalos e ajustar o tamanho conforme necessário.
    Custo: VMs maiores com mais recursos são mais caras. Otimize o tamanho para atender às suas necessidades sem desperdiçar recursos.
    Tipos de instância: A Azure oferece diversos tipos de instância otimizados para diferentes cargas de trabalho (uso geral, computação intensiva, memória intensiva, armazenamento otimizado, GPUs). Escolha o tipo que melhor se adapta à sua aplicação.
    Escalabilidade: Considere se você precisará escalar sua VM verticalmente (aumentar ou diminuir o tamanho da instância) ou horizontalmente (aumentar ou diminuir o número de instâncias). Para escalabilidade horizontal, conjuntos de escala de máquinas virtuais são ideais.

Opções de Disponibilidade (Revisitando)

Como já discutido, a escolha da opção de disponibilidade é fundamental para a resiliência da sua aplicação. Reforçando:

  Conjuntos de disponibilidade: Proteção contra falhas de hardware planejadas e não planejadas dentro de um único data center.
    Zonas de disponibilidade: Proteção contra falhas em data centers inteiros dentro de uma região. Oferece maior resiliência, mas pode ter um custo ligeiramente superior.
    Conjuntos de escala de máquinas virtuais: Ideal para escalabilidade e alta disponibilidade, permitindo o gerenciamento e o escalonamento automático de várias VMs idênticas.

Zona (Zona de Disponibilidade)

A escolha da zona de disponibilidade (se aplicável na região selecionada) permite distribuir suas VMs por diferentes data centers físicos dentro de uma região. Isso oferece uma camada adicional de proteção contra falhas de infraestrutura localizadas. Para aplicações críticas, distribuir VMs por múltiplas zonas de disponibilidade é uma prática recomendada.

Segurança - Sua Prioridade Máxima

A segurança da sua máquina virtual na Azure é uma responsabilidade compartilhada entre você e a Microsoft. A Microsoft protege a infraestrutura subjacente, mas você é responsável por proteger sua VM e os dados nela contidos. Algumas práticas essenciais de segurança incluem:

  Network Security Groups (NSGs): Configure NSGs para controlar o tráfego de rede de entrada e saída da sua VM. Aplique o princípio do menor privilégio, permitindo apenas o tráfego necessário para sua aplicação funcionar. Revise e ajuste suas regras de NSG regularmente.
    Azure Firewall: Para um controle de segurança de rede mais granular e centralizado, considere usar o Azure Firewall para proteger suas redes virtuais.
    Azure Security Center (Microsoft Defender for Cloud): Utilize o Azure Security Center para obter recomendações de segurança, monitorar ameaças e fortalecer a postura de segurança dos seus recursos Azure, incluindo suas VMs.
    Atualizações e patches: Mantenha seu sistema operacional e aplicativos atualizados com os patches de segurança mais recentes. Utilize serviços como o Azure Update Management para automatizar esse processo.
    Antivírus e antimalware: Instale e configure software antivírus e antimalware na sua VM.
    Gerenciamento de identidades e acesso (IAM): Utilize o Azure Active Directory (Azure AD) para gerenciar identidades e controlar o acesso aos seus recursos Azure, incluindo suas VMs. Aplique o princípio do menor privilégio ao conceder permissões.

  Criptografia:
        Criptografia em repouso: Proteja seus dados armazenados nos discos da sua VM utilizando a criptografia de disco da Azure. Você pode optar por criptografia gerenciada pela plataforma ou gerenciada pelo cliente (usando suas próprias chaves no Azure Key Vault). Para dados confidenciais, a criptografia em repouso é essencial para proteger contra acesso não autorizado caso os discos sejam comprometidos.
        Criptografia em trânsito: Proteja os dados que trafegam para e da sua VM utilizando protocolos seguros como HTTPS (para tráfego web) e SSH (para acesso remoto). Certifique-se de que seus aplicativos e configurações estejam utilizando criptografia para proteger a confidencialidade e a integridade dos dados em movimento.
    Azure Bastion: Em vez de expor a porta RDP (3389) ou SSH (22) diretamente à internet, considere utilizar o Azure Bastion. Ele fornece uma conexão segura e gerenciada via navegador da web ou cliente nativo, reduzindo significativamente a superfície de ataque da sua VM.
    Monitoramento e logs de segurança: Habilite logs de diagnóstico para sua VM e utilize o Azure Monitor e o Azure Security Center para monitorar eventos de segurança, identificar atividades suspeitas e responder a incidentes de segurança.
    Políticas de segurança: Implemente políticas de segurança consistentes em todos os seus recursos Azure, utilizando o Azure Policy para garantir a conformidade e evitar configurações inseguras.
    Backups seguros: Realize backups regulares das suas VMs utilizando o Azure Backup e armazene esses backups em um local seguro e separado da sua VM principal. Considere a replicação dos backups para outra região (Azure paired region) para proteção contra desastres regionais.

Passo 5: Gerenciamento e Monitoramento Contínuo

A criação e configuração inicial da sua VM são apenas o primeiro passo. O gerenciamento e o monitoramento contínuos são essenciais para garantir o desempenho, a disponibilidade e a segurança da sua infraestrutura.

  Azure Monitor: Utilize o Azure Monitor para coletar e analisar métricas de desempenho, logs de atividades e logs de diagnóstico da sua VM. Configure alertas para ser notificado sobre problemas potenciais (alto uso de CPU, falta de espaço em disco, etc.).
  Azure Advisor: O Azure Advisor analisa suas configurações e uso de recursos e fornece recomendações para otimizar seus custos, segurança, confiabilidade e desempenho. Revise as recomendações do Advisor regularmente.
  Azure Resource Manager (ARM) Templates: Para infraestrutura como código (IaC), considere utilizar ARM Templates para definir e implantar sua infraestrutura Azure de forma declarativa e repetível. Isso facilita a criação de ambientes consistentes e o gerenciamento da sua infraestrutura em escala.
  Azure Automation: Utilize o Azure Automation para automatizar tarefas de gerenciamento repetitivas, como aplicação de patches, inicialização/desligamento de VMs em horários específicos e outras tarefas operacionais.
  Azure Cost Management: Monitore os custos associados à sua VM e tome medidas para otimizar seus gastos. Utilize etiquetas para rastrear os custos por projeto ou departamento. Considere o uso de instâncias reservadas para obter descontos em cargas de trabalho de longo prazo.

Conclusão: Dominando o Mundo das VMs na Azure

Parabéns! Você percorreu um longo caminho, desde a criação da sua primeira máquina virtual na Azure até a compreensão das considerações essenciais para garantir sua disponibilidade, segurança e desempenho. Lembre-se que a nuvem Azure é um ambiente em constante evolução, por isso, continue explorando os diversos serviços e recursos disponíveis para aprimorar suas habilidades e otimizar suas soluções.

Este guia serve como um ponto de partida robusto e uma referência para suas futuras consultas. Ao compartilhar este material no seu Git, você não apenas auxilia outros iniciantes, mas também demonstra seu conhecimento e atenção aos detalhes, o que certamente será um diferencial valioso para possíveis empregadores.

Se tiver mais alguma dúvida ou precisar de ajuda com algum tópico específico, pode me perguntar! Estou aqui para continuar te auxiliando nessa jornada.
        
