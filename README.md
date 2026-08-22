# PersonChat v7.3.0 — Caixa de Chat Interativa para Streamlabs

Tema de chat moderno e responsivo para Twitch, YouTube e Kick, desenvolvido especificamente para a **Caixa de chat nativa da Streamlabs**.

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

- Cinco temas visuais.
- Avatar real do usuário quando a plataforma disponibiliza a foto.
- Busca controlada de avatar da Twitch e Kick quando necessário.
- Avatar local por iniciais se a foto falhar ou não existir.
- Caixa **Em resposta a @usuário**.
- Trecho da mensagem original dentro da caixa de reply quando fornecido pela plataforma.
- Fallback de reply para mensagens iniciadas por **@usuário**.
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

- o usuário respondido;
- o texto original, quando disponível;
- a resposta atual sem duplicar a menção inicial.

Quando esses dados não chegam, uma mensagem iniciada por **@usuário** ativa o fallback visual de reply.

## 🎨 Temas

Edite **THEME** no topo de **JS.txt**:

- **dark-purple** — padrão;
- **pink-gold**;
- **kick-green**;
- **youtube-red**;
- **clean-white**.

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

O efeito de **GG** exige três usuários diferentes dentro de seis segundos. Mensagens antigas, comandos e atualizações tardias de badges não disparam efeitos.

Configuração padrão:

```js
"WORD_EFFECTS": [
    { "trigger": "Briar", "effect": "confetti", "match": "word", "cooldown": 6000, "particles": 44 },
    { "trigger": "GG", "effect": "energy-wave", "match": "word", "cooldown": 8000, "threshold": 3, "window": 6000, "uniqueUsers": true },
    { "trigger": "Hype", "effect": "hype-pulse", "match": "word", "cooldown": 4000 },
    { "trigger": "Boa noite", "effect": "stars", "match": "phrase", "cooldown": 6000, "particles": 28 },
    { "trigger": "F", "effect": "mono-rain", "match": "exact", "cooldown": 5000, "particles": 34 }
]
```

Para reconhecer menções antes de o streamer enviar sua primeira mensagem, preencha **STREAMER_NAMES** com o nome do canal sem `@`:

    "STREAMER_NAMES": ["SeuCanal"]

Quando o cargo de broadcaster é recebido pela Streamlabs, o PersonChat também aprende o nome automaticamente.

## 🔧 Configuração

Exemplo do bloco encontrado no início de **JS.txt**:

    globalThis.PERSONCHAT_CONFIG = globalThis.PERSONCHAT_CONFIG || {
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
        STREAMER_NAMES: ["SeuCanal"],
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
| WORD_EFFECTS_ENABLED                      | Ativa os gatilhos de palavras e frases.                                   |
| CLIMAX_ENABLED                            | Ativa o modo visual para períodos de alta atividade.                      |
| STREAMER_NAMES                            | Informa os nomes usados para detectar o streamer e suas menções.          |
| FETCH_TWITCH_AVATAR_WHEN_PLATFORM_UNKNOWN | Tenta recuperar foto Twitch quando faltam metadados.                      |
| FETCH_KICK_AVATAR                         | Permite recuperar foto pela API pública da Kick.                          |
| REPLY_FALLBACK_FROM_LEADING_MENTION       | Cria reply visual para mensagens iniciadas por @usuário.                  |
| EMBED_IMAGES                              | Converte links autorizados em imagens; permanece desligado por segurança. |

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
