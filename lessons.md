# 📘 Compilado Geral – Alpha EdTech
**Autor:** Mauricio Machado.

**Temas:** Redes e Git.

## 🌐 Parte 1: Redes, Segurança e Infraestrutura

Esta seção cobre desde a estrutura física e lógica das redes até protocolos avançados de segurança e tecnologias emergentes.

### 1. Topologias de Rede
* **Backbone da Internet (Malha/Mesh):**
    * Foco em **alta redundância** e múltiplos caminhos.
    * Evita falhas por rota única (se um link cai, outro assume).
* **Rede Doméstica (Estrela):**
    * Conecta todos os dispositivos a um **roteador central**.
    * Simples, barata e de fácil manutenção.

### 2. Escopo e Classificação de Redes
| Tipo | Definição |
| :--- | :--- |
| **Internet** | Rede global e pública. |
| **Intranet** | Rede interna e privada (ex: rede corporativa). |
| **Extranet** | Rede privada com acesso externo controlado (ex: parceiros/fornecedores). |

**Classificação Geográfica:**
* **PAN (Personal Area Network):** Área pessoal (Bluetooth).
* **LAN (Local Area Network):** Local, alta velocidade (casa/escritório).
* **MAN (Metropolitan Area Network):** Área metropolitana (cidade).
* **WAN (Wide Area Network):** Longas distâncias (países/continentes).

### 3. Performance: QoS e Latência
* **QoS (Quality of Service):** Garante a priorização de tráfego crítico (voz, vídeo, jogos, telemedicina) sobre tráfego menos urgente.
* **Latência:** Tempo que um pacote leva para percorrer a rede.
    * *Impacto:* Prejudica jogos, chamadas de vídeo e transações em tempo real.
    * *Ferramentas:* `Ping` (mede latência), `Traceroute` (mostra os saltos).

### 4. Protocolos de Comunicação

#### Transporte
* **TCP (Transmission Control Protocol):** Confiável, ordenado, orientado à conexão. Garante a entrega.
* **UDP (User Datagram Protocol):** Rápido, não garante entrega. Usado em streaming, VoIP e jogos.

#### Aplicação e Infraestrutura
* **HTTP vs HTTPS:**
    * HTTP: Texto claro, sem segurança.
    * HTTPS: HTTP + TLS (Criptografia, Integridade e Autenticação).
* **DNS (Domain Name System):**
    * Converte nomes (google.com) em IPs.
    * *Vulnerabilidade:* Cache Poisoning.
    * *Mitigação:* DNSSEC, 0x20 encoding, randomização de portas.

### 5. Wi-Fi e Segurança Wireless
* **WEP:** Inseguro (facilmente quebrável).
* **WPA:** Obsoleto.
* **WPA2 / WPA3:** Padrões recomendados atualmente (utilizam criptografia **AES**).

### 6. Endereçamento IP
* **IPv4:** Esgotado. Usa **NAT** para mascarar IPs privados em um IP público único.
    * *Máscaras comuns:* `255.255.255.0` (/24 - 254 hosts), `255.255.0.0` (/16 - redes maiores).
* **IPv6:** Elimina a necessidade de NAT, suporta trilhões de dispositivos e possui IPSec nativo.

### 7. Segurança da Informação

#### Criptografia
* **Simétrica:** Mesma chave para cifrar e decifrar. Rápida (ex: AES).
* **Assimétrica:** Par de chaves (Pública/Privada). Usada em assinaturas digitais e troca de chaves.

#### TLS/SSL e Certificados
* **Handshake TLS:**
    1.  Cliente envia "ClientHello".
    2.  Servidor envia certificado.
    3.  Troca de chaves (ex: ECDHE) e geração de chave simétrica.
    4.  Início da comunicação segura.
* **Certificado Digital:** Contém Subject, Chave Pública, Issuer (CA), Validade e Assinatura da CA.

#### Ameaças e Defesa
* **DDoS (Distributed Denial of Service):** Ataque massivo para esgotar banda ou recursos.
    * *Mitigação:* Anycast, Scrubbing centers, Rate limiting, WAF (Cloudflare/Akamai).
* **Firewalls:**
    * *Packet Filter:* Analisa cabeçalho.
    * *Stateful:* Analisa estado da conexão.
    * *NGFW (Next-Gen):* Inspeção profunda, IDS/IPS, antimalware.
* **Malware:** Vírus, worms, ransomware. Combatido com patches, updates e conscientização (Engenharia Social).

### 8. Cloud, IoT e Tecnologias Avançadas
* **CDN & Cloudflare:** Oferecem WAF, mitigação DDoS, TLS 1.3 e cache distribuído.
* **VPN:** Cria túnel criptografado, protege em Wi-Fi público e contorna bloqueios geográficos.
* **IoT (Internet of Things):** Desafios incluem hardware limitado e segurança fraca. Protocolos leves: MQTT, CoAP.
* **SDN (Software Defined Networking):** Separa Plano de Controle (inteligência) do Plano de Dados (switches).
* **Blockchain:** Blocos encadeados por hashes. Garante imutabilidade e consenso (PoW, PoS).
* **AWS S3:** Armazenamento de objetos.
    * Foco em durabilidade (99.999999999%) e disponibilidade.

---

## 🐙 Parte 2: Git e Controle de Versão

Esta seção foca no uso do Git, desde comandos básicos até fluxos de trabalho colaborativos (Code Review e PRs).

### 1. Fundamentos do Git
* **Configuração:**
    * Global: `.gitconfig` (usuário).
    * Local: `.git/config` (repositório específico).
* **Estados:**
    * `Working tree`: Arquivos atuais sendo editados.
    * `Index` (Staging Area): Área de preparação.
    * `HEAD`: Ponteiro para o commit/branch atual.
    * Tudo fica armazenado na pasta oculta `.git/`.

### 2. Branches, Commits e Hashes
* **Branch:** Não é uma sequência física de commits, mas um **ponteiro móvel** para o commit mais recente.
* **Hash (SHA-1):** Identificador único gerado com base em:
    * Árvore de arquivos (Tree).
    * Commits pais (Parents).
    * Autor, data e mensagem.
    * *Nota:* O comando `git commit --amend` altera esses dados, gerando um **novo hash**.

### 3. Merge e Resolução de Conflitos
| Tipo de Merge | Descrição |
| :--- | :--- |
| **Fast-Forward** | A branch local apenas "anda" para frente até o commit da remota (sem commit de merge). |
| **Merge Normal** | Cria um novo commit específico de união ("merge commit"). |

**Fluxo de Resolução de Conflitos:**
1.  `git switch branch-destino`
2.  `git merge branch-origem` (Conflito detectado)
3.  Editar arquivos manualmente para resolver as diferenças.
4.  `git add .`
5.  `git commit` (Finaliza o merge).

### 4. Git Remoto e Colaboração
* **Comandos Essenciais:**
    * `git remote add origin URL`: Vincula ao repositório remoto.
    * `git fetch`: Baixa referências e objetos, mas não altera seus arquivos.
    * `git pull`: Equivalente a `git fetch` + `git merge`.
* **Regra de Ouro:** Se houver divergência (Non-fast-forward), você deve **atualizar** (pull) antes de enviar (push).

### 5. Pull Requests (PR) e Code Review

**Estrutura do PR:**
* **Source branch:** Onde você fez as alterações.
* **Target branch:** Onde as alterações serão aplicadas (geralmente `main` ou `develop`).

**Estados do Review:**
* **Comment:** Dúvidas ou observações gerais.
* **Approve:** Código pronto para merge.
* **Request changes:** Bloqueia o merge até que correções sejam feitas.

**Conflitos dentro do PR (Workflow):**
Se aparecer "Can't automatically merge":
1.  Vá para sua branch local (`checkout`).
2.  Faça merge da branch de destino (`git merge main`).
3.  Resolva os conflitos localmente.
4.  Faça o `git push` para atualizar o PR automaticamente.
