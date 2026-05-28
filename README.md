# PersonChat - Multistream Chat Overlay

Um overlay de chat moderno, leve e totalmente personalizável para transmissões ao vivo. Projetado para funcionar com OBS Studio via Streamlabs, ele é focado em alta performance (ideal para Subathons) e suporte simultâneo a múltiplas plataformas.

## ✨ Principais Recursos

- **🌐 Suporte Multistream Nativo:** Identificação visual automática de espectadores da Twitch, YouTube e Kick com ícones e contornos personalizados.
- **🚀 Otimizado para Subathons:** Sistema inteligente de cache de avatares no navegador (LocalStorage) com limites e autolimpeza para evitar consumo excessivo de memória em lives longas.
- **🎨 Multitemas Integrados:** Troque o visual do chat alterando apenas uma linha de código. Temas inclusos: `dark-purple` (Padrão), `pink-gold`, `kick-green`, `youtube-red` e `clean-white`.
- **✨ Destaque de Eventos e Primeira Mensagem:** Animações CSS avançadas (como ondas de brilho e estrelas) para destacar de forma luxuosa os *First-Time Chatters*, além de banners iluminados para Super Chats, Doações, Raids, Subs e Follows.
- **💬 Respostas (Replies) Inteligentes:** Suporte visual para respostas diretas no chat ou via menção direta (`@usuario`), incluindo pílulas flutuantes informativas.
- **📱 Design Responsivo e Compacto:** Layout flexível que se adapta a telas verticais (Shorts/TikTok) e agrupa mensagens seguidas do mesmo usuário para manter a tela limpa.

## ⚙️ Como Instalar

1. Acesse o seu painel do **Streamlabs** e adicione um widget de **Chat Box**.
2. Ative a opção para usar **HTML/CSS/JS Customizado**.
3. Baixe os arquivos da última versão (Release) deste repositório e substitua os códigos:
   - Cole o conteúdo do arquivo `HTML.txt` na aba **HTML**.
   - Cole o conteúdo do arquivo `CSS.txt` na aba **CSS**.
   - Cole o conteúdo do arquivo `JS.txt` na aba **JS**.
4. Copie a URL do widget e adicione como uma **Fonte de Navegador** no seu OBS Studio.
5. **Tamanho recomendado no OBS:** `Largura: 400` x `Altura: 700` (O chat é flexível e se adaptará caso você altere as proporções).

## 🛠️ Como Configurar

Você não precisa mexer no CSS para personalizar as opções básicas! Toda a configuração é feita de forma simples no topo do arquivo **JS**. 

Procure pelo bloco `CONFIG` nas primeiras linhas do script para ajustar o chat ao seu gosto:

```javascript
const CONFIG = {
    THEME: "dark-purple", // Opções: pink-gold, dark-purple, kick-green, youtube-red, clean-white
    MESSAGE_LINE_LENGTH: "50ch", // Largura do balão de texto
    MAX_MESSAGES: 15, // Limite de mensagens simultâneas na tela
    HIDE_AFTER: 45, // Segundos para a mensagem sumir
    SHOW_PLATFORM_BADGE: true, // Mostrar ícone de Twitch/YouTube/Kick
    SHOW_ROLE_PILLS: false, // Mostrar tags como MOD, VIP e SUB
    // ... e muito mais!
};
```

📞 Contato / Suporte
Em caso de dúvidas sobre a instalação ou para relatar bugs, entre em contato via Discord: miyzuuu_
