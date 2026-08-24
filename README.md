# PersonChat v7.7.0 — Caixa de Chat Interativa para Streamlabs

Tema de chat moderno e responsivo para Twitch, YouTube e Kick, desenvolvido especificamente para a **Caixa de chat nativa da Streamlabs**.

## 🎛️ Demonstração interativa

[▶ Abrir demonstração ao vivo](https://miyzuu.github.io/PersonChat/docs/)

Teste os temas, animações, efeitos de texto, avatares e dimensões antes de instalar. A página também reproduz exemplos de streamer, moderador, raider, reply, mensagens somente com emotes, efeitos de palavras, onda coletiva de GG e Modo Clímax.

A demonstração usa diretamente os três arquivos oficiais do repositório, não acessa chats reais e não solicita conta ou token.

> A demonstração é apenas uma ferramenta de visualização. Para instalar na Streamlabs, continuam sendo necessários somente `HTML.txt`, `CSS.txt` e `JS.txt`.

<details>
<summary>Como ativar o GitHub Pages deste repositório</summary>

1. Abra **Settings > Pages** no GitHub.
2. Em **Build and deployment**, selecione **Deploy from a branch**.
3. Escolha a branch **main** e a pasta **/(root)**.
4. Salve e aguarde a publicação.
5. A demonstração ficará disponível em `https://miyzuu.github.io/PersonChat/docs/`.

A publicação precisa usar **/(root)** porque a demonstração carrega `HTML.txt`, `CSS.txt` e `JS.txt` diretamente da raiz.

</details>

## 📦 Somente três arquivos

A implementação completa está dentro destes arquivos:

- **HTML.txt** — estrutura visual da mensagem;
- **CSS.txt** — temas, avatar, caixa de reply e animações;
- **JS.txt** — configuração, integração com as plataformas e todos os fallbacks.

Nenhum outro arquivo é necessário para instalar ou executar o PersonChat.

## 🧩 Campos personalizados

O PersonChat **não utiliza o botão Adicionar Campos personalizados**.

Não é necessário criar JSON, formulário ou arquivo extra. Todas as opções ficam no objeto **PERSONCHAT_CONFIG**, nas primeiras linhas de **JS.txt**.

## ⚙️ Instalação

1. Abra **Todos os widgets > Caixa de chat** no painel da Streamlabs.
2. Ative **HTML/CSS personalizado**.
3. Cole o conteúdo de **HTML.txt** na aba HTML.
4. Cole o conteúdo de **CSS.txt** na aba CSS.
5. Cole o conteúdo de **JS.txt** na aba JS.
6. Clique em **Salvar configurações**.
7. Envie uma mensagem de teste.
8. No OBS, adicione a URL da Caixa de chat como **Fonte de navegador**.

Substitua sempre os três arquivos juntos.

## ✨ Recursos

- Dezesseis temas visuais com opções claras, escuras, neon, pastel e monocromáticas.
- Cores pessoais de nick escolhidas pelo público com o comando **!cor**.
- Preferências de cor persistidas com expiração e limite seguro de usuários.
- Opção para o streamer mostrar ou ocultar as fotos dos usuários.
- Avatar real do usuário quando a plataforma disponibiliza a foto.
- Busca controlada de avatar da Twitch e Kick quando necessário.
- Avatar local por iniciais se a foto falhar ou não existir.
- Indicador compacto de resposta acima do nick, com `@usuário` e sem texto redundante.
- Trecho da mensagem original dentro da caixa de reply quando fornecido pela plataforma.
- Fallback de reply para mensagens iniciadas por `@usuário`.
- Badges e emotes inseridos pela própria Streamlabs.
- Agrupamento de mensagens consecutivas.
- Mensagens formadas somente por emotes em tamanho ampliado.
- Agrupamento de mensagens iguais com contador visual.
- Degradê animado para streamer, moderadores e raids.
- Animações de entrada e texto selecionáveis.
- Efeitos configuráveis ativados por palavras e frases.
- Confete para **Briar**, onda coletiva para **GG**, pulso para **Hype**, estrelas para **Boa noite** e chuva monocromática para **F**.
- Modo Clímax ativado automaticamente quando o chat fica muito movimentado.
- Destaque para mensagens do streamer e para quem mencionar o canal.
- Compatibilidade com exclusões feitas pela moderação.
- Limites, timeout, cache e cancelamento para requisições externas.
- Animações com suporte a movimento reduzido.

## 🖼️ Como o avatar funciona

No topo de **JS.txt**, use:

```js
"SHOW_USER_AVATAR": "yes"
```

- **yes** — mostra foto real ou avatar por iniciais;
- **no** — remove a foto, expande a mensagem e evita as buscas externas de avatar.

O JavaScript identifica mensagens nos formatos usados pela Caixa de chat:

- Twitch: eventos **PRIVMSG** e **CHAT**;
- YouTube: **youtube#liveChatMessage** e **CHAT**;
- Kick: **chat.message.sent** e **CHAT**.

A ordem utilizada é:

1. foto entregue pelo evento da plataforma;
2. foto salva no cache local;
3. busca controlada na Twitch ou Kick;
4. avatar SVG com as iniciais.

A mensagem nunca é escondida se uma foto não carregar.

## ↩️ Como o reply funciona

Quando Twitch ou Kick enviam os dados estruturados do reply, o PersonChat mostra:

- uma faixa compacta acima do cabeçalho com o usuário respondido;
- o texto original, quando disponível;
- a resposta atual sem duplicar a menção inicial.

Visualmente, a faixa usa apenas o ícone de reply, `@usuário` e o trecho original; a expressão **Em resposta a** permanece somente na descrição acessível para leitores de tela.

Quando esses dados não chegam, uma mensagem iniciada por `@usuário` ativa o fallback visual de reply.

## 🎨 Temas

Edite **THEME** no topo de **JS.txt**:

- **dark-purple** — padrão;
- **pink-gold**;
- **kick-green**;
- **youtube-red**;
- **clean-white**;
- **ocean-blue**;
- **neon-cyber**;
- **sunset-orange**;
- **emerald-night**;
- **royal-blue**;
- **cherry-black**;
- **lavender-dream**;
- **gold-black**;
- **ice-blue**;
- **pastel-candy**;
- **black-white** — preto, branco e cinzas, incluindo `#2e2e2e`.

### Cores escolhidas pelo público

Com **VIEWER_COLORS_ENABLED** ativado, cada pessoa pode escolher o degradê do próprio nick. O comando é ocultado automaticamente e a escolha aparece nas próximas mensagens.

```text
!cor roxo
!cor azul
!cor rosa
!cor verde
!cor dourado
!cor oceano
!cor fogo
!cor pastel
!cor preto
!cor reset
```

As preferências ficam no armazenamento local do widget por 30 dias, com limite padrão de 1.000 usuários. O sistema mantém Twitch, YouTube e Kick separados e reconhece nome exibido, login e ID mesmo quando esses metadados chegam em momentos diferentes.

Por segurança, o público só pode usar os nomes existentes em **VIEWER_COLOR_PALETTE**. Códigos CSS, URLs e cores arbitrárias enviados pelo chat são ignorados. Broadcaster real, moderador, raider, staff, eventos, primeiras mensagens e o destaque habilitado do streamer continuam tendo prioridade visual sobre a cor pessoal.

O streamer pode trocar o comando em **VIEWER_COLOR_COMMAND**, desativar o recurso ou editar os valores hexadecimais seguros da paleta no início de **JS.txt**. Nenhum Campo personalizado é necessário.

### Animações

Edite **MESSAGE_ANIMATION** para escolher a entrada das mensagens:

- **soft-slide** — deslizamento suave;
- **float-up** — subida leve;
- **pop** — expansão curta;
- **minimal** — apenas fade;
- **none** — sem animação.

Edite **TEXT_EFFECT** para usar **none**, **soft-glow** ou **color-pulse**.

## 🎉 Efeitos interativos

Cada regra de **WORD_EFFECTS** possui:

- **trigger** — palavra ou frase observada;
- **effect** — efeito visual executado;
- **match** — correspondência por palavra, frase ou mensagem exata;
- **cooldown** — intervalo mínimo em milissegundos;
- **particles** — quantidade de partículas, quando aplicável;
- **threshold**, **window** e **uniqueUsers** — usados em efeitos coletivos como o combo de GG.

O efeito de **GG** exige três usuários diferentes dentro de dez segundos. Cada GG válido mostra a carga `GG 1/3`, `GG 2/3` e `GG 3/3`; no terceiro, a onda atravessa o chat. A carga desaparece quando a janela vence. Um único usuário repetindo GG não completa o combo. O matcher também reconhece GG recebido como emote. Mensagens antigas e comandos não disparam efeitos.

Se o sistema operacional estiver configurado para reduzir movimento, o contador continua visível, mas a onda animada é substituída pelo estado estático por acessibilidade.

Configuração padrão:

```js
"WORD_EFFECTS": [
    { "trigger": "Briar", "effect": "confetti", "match": "word", "cooldown": 6000, "particles": 44 },
    { "trigger": "GG", "effect": "energy-wave", "match": "word", "cooldown": 8000, "threshold": 3, "window": 10000, "uniqueUsers": true },
    { "trigger": "Hype", "effect": "hype-pulse", "match": "word", "cooldown": 4000 },
    { "trigger": "Boa noite", "effect": "stars", "match": "phrase", "cooldown": 6000, "particles": 28 },
    { "trigger": "F", "effect": "mono-rain", "match": "exact", "cooldown": 5000, "particles": 34 }
]
```

Para reconhecer menções antes de o streamer enviar sua primeira mensagem, preencha **STREAMER_NAMES** com o nome do canal sem `@`. O nome precisa ficar entre aspas:

    "STREAMER_NAMES": "SeuCanal"

Para mais de um nome, também é aceita uma lista: `"STREAMER_NAMES": ["SeuCanal", "OutroNome"]`. Não use `[SeuCanal]` sem aspas: isso é JavaScript inválido e interrompe todo o widget.

Quando o cargo de broadcaster é recebido pela Streamlabs, o PersonChat também aprende o nome automaticamente.

**STREAMER_HIGHLIGHT_ENABLED** controla o destaque do nome informado manualmente. Avatar e efeitos de palavras continuam ativos nos dois modos. Com `true`, esse nome usa o degradê especial; com `false`, também pode usar cor pessoal e agrupamento normal. Um cargo real de broadcaster continua tendo prioridade de cargo. Informar o nome não cria artificialmente esse cargo.

## 🔧 Configuração

Exemplo do bloco encontrado no início de **JS.txt**:

    globalThis.PERSONCHAT_CONFIG = {
        THEME: "dark-purple",
        MESSAGE_ANIMATION: "soft-slide",
        TEXT_EFFECT: "soft-glow",
        MESSAGE_LINE_LENGTH: "25ch",
        MAX_MESSAGES: 50,
        HIDE_AFTER: 0,
        HIDE_COMMANDS: true,
        SHOW_PLATFORM_BADGE: false,
        SHOW_ROLE_PILLS: false,
        SHOW_EVENT_BANNERS: false,
        ROLE_GRADIENTS_ENABLED: true,
        SHOW_USER_AVATAR: "yes",
        VIEWER_COLORS_ENABLED: true,
        VIEWER_COLOR_COMMAND: "!cor",
        VIEWER_COLOR_EXPIRY: 2592000000,
        VIEWER_COLOR_MAX_USERS: 1000,
        EMOTE_ONLY_MODE: true,
        GROUP_REPEATED_MESSAGES: true,
        HIDE_REPEATED_AVATAR_AND_NAME: true,
        FETCH_TWITCH_AVATAR_WHEN_PLATFORM_UNKNOWN: true,
        FETCH_KICK_AVATAR: true,
        REPLY_FALLBACK_FROM_LEADING_MENTION: true,
        WORD_EFFECTS_ENABLED: true,
        CLIMAX_ENABLED: true,
        STREAMER_HIGHLIGHT_ENABLED: true,
        STREAMER_MENTION_ENABLED: true,
        STREAMER_NAMES: "SeuCanal",
        EMBED_IMAGES: false,
        IMAGE_ALLOWED_HOSTS: []
    };

### Opções principais

| Opção                                     | Função                                                                    |
| ----------------------------------------- | ------------------------------------------------------------------------- |
| THEME                                     | Escolhe o tema visual.                                                    |
| MESSAGE_ANIMATION                         | Escolhe a animação de entrada das mensagens.                              |
| TEXT_EFFECT                               | Escolhe o efeito curto aplicado ao texto.                                 |
| MESSAGE_LINE_LENGTH                       | Controla a largura aproximada do texto.                                   |
| MAX_MESSAGES                              | Limita as mensagens mantidas na tela.                                     |
| HIDE_AFTER                                | Use 0 para deixar o tempo sob controle da Streamlabs.                     |
| HIDE_REPEATED_AVATAR_AND_NAME             | Agrupa mensagens consecutivas do mesmo usuário.                           |
| GROUP_REPEATED_MESSAGES                   | Une mensagens iguais e mostra um contador.                                |
| EMOTE_ONLY_MODE                           | Amplia mensagens compostas somente por emotes.                            |
| ROLE_GRADIENTS_ENABLED                    | Ativa degradês animados por cargo.                                        |
| SHOW_USER_AVATAR                         | Use yes para mostrar fotos ou no para ocultá-las e poupar requisições.    |
| VIEWER_COLORS_ENABLED                     | Permite ao público escolher a cor do próprio nick com !cor.               |
| VIEWER_COLOR_COMMAND                      | Define o comando reservado para selecionar uma cor pessoal.               |
| VIEWER_COLOR_EXPIRY                       | Define por quanto tempo a preferência permanece salva, em milissegundos.  |
| VIEWER_COLOR_MAX_USERS                    | Limita quantas preferências de pessoas ficam armazenadas.                  |
| VIEWER_COLOR_PALETTE                      | Define a lista segura de degradês disponíveis ao público.                  |
| WORD_EFFECTS_ENABLED                      | Ativa os gatilhos de palavras e frases.                                   |
| CLIMAX_ENABLED                            | Ativa o modo visual para períodos de alta atividade.                      |
| STREAMER_HIGHLIGHT_ENABLED                | Ativa o degradê especial sem alterar o cargo real da pessoa.              |
| STREAMER_NAMES                            | Informa os nomes usados para detectar o streamer e suas menções.          |
| FETCH_TWITCH_AVATAR_WHEN_PLATFORM_UNKNOWN | Tenta recuperar foto Twitch quando faltam metadados.                      |
| FETCH_KICK_AVATAR                         | Permite recuperar foto pela API pública da Kick.                          |
| REPLY_FALLBACK_FROM_LEADING_MENTION       | Cria reply visual para mensagens iniciadas por `@usuário`.                |
| EMBED_IMAGES                              | Converte links autorizados em imagens; permanece desligado por segurança. |

## 🩺 Solução rápida de problemas

- **GG não criou a onda:** o combo precisa de três pessoas diferentes em até dez segundos. Confira o contador `GG 1/3` até `GG 3/3`. Com redução de movimento ativa, o contador permanece, mas a onda não anima.
- **!cor foi ocultado, mas a cor não apareceu:** substitua os três arquivos pela mesma versão e envie uma nova mensagem. A correção para a troca tardia entre nome, login, plataforma e ID está incluída na v7.7.0.
- **Recursos pararam após preencher o streamer:** use `"STREAMER_NAMES": "SeuCanal"`, sempre com aspas. Na v7.7.0, esse nome identifica o destaque do streamer sem transformá-lo em cargo de broadcaster.
- **Alteração não apareceu no preview da Streamlabs:** clique em **Salvar configurações** no painel da Streamlabs. O bloco da v7.7.0 é reaplicado a cada execução e não reutiliza a configuração antiga.

## 🌐 Plataformas e emotes

Selecione Twitch, YouTube e Kick no próprio painel da Streamlabs.

BetterTTV, FrankerFaceZ, 7TV, palavras ocultas, usuários silenciados, atraso e tempo de permanência também devem ser configurados no painel. O PersonChat não duplica essas configurações.

## 🔒 Segurança

- Links do chat não viram imagens por padrão.
- Endereços locais, IPs privados, literais IPv6 e URLs não HTTPS são bloqueados.
- Requisições de avatar possuem timeout, limite de concorrência, fila e cooldown.
- Eventos sem comando de chat reconhecido são ignorados.
- Falhas de API ou CORS sempre retornam ao avatar por iniciais.

## 📐 Tamanho recomendado no OBS

Use aproximadamente **400 × 700** como ponto de partida. O layout se adapta a outras dimensões.

## 📞 Contato

Discord: **miyzuuu_**
