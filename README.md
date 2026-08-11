# Voice Code

**Voice Code** é um aplicativo de ditado por voz com IA, feito em **Tauri v2** e **React**, que roda em **Windows** e **Linux**. Pressione uma tecla, fale, e o texto é transcrito e digitado automaticamente no aplicativo que estiver em foco — com modos especializados para **código** e **chat**.

Este repositório é o canal de **distribuição** da aplicação: os instaladores, pacotes e o manifest de atualização automática (`latest.json`) são publicados aqui via **GitHub Releases**.

---
<img width="982" height="743" alt="image" src="https://github.com/user-attachments/assets/c9baf606-99ed-4577-98f2-896d2550a83d" />

---

## ⚡ Por que ditado por voz?

Pesquisas da **Universidade de Stanford** mostram que a velocidade média de fala é de cerca de **130 a 150 palavras por minuto**, enquanto a digitação atinge apenas **40 a 60 palavras por minuto** — ou seja, ditado é aproximadamente **3x mais rápido** que digitar ([fonte](https://www.productivitygladiator.com/blog/dictating-is-3x-faster-than-typing-start-talking)).

Com o **Voice Code**, essa velocidade se traduz em produtividade real: você fala no seu ritmo natural e o texto aparece instantaneamente em qualquer aplicativo, sem perder tempo com digitação, correção de erros ou distrações.

---

## 🌐 Por que traduzir de Português para Inglês no modo Code?

O modo **Code** traduz automaticamente sua fala do português para o inglês antes de digitar. Essa decisão tem uma base técnica sólida, com dois grandes benefícios:

1. **Economia de tokens.** Modelos de linguagem (LLMs) e ferramentas de IA generativa funcionam de forma significativamente mais eficiente em inglês — o idioma principal de seus dados de treinamento. Código, comandos, prompts e documentação escritos em inglês consomem **menos tokens** e produzem respostas mais precisas, reduzindo custos e latência.

2. **Melhor qualidade de código.** O código-fonte é escrito em inglês (identificadores, funções, bibliotecas, convenções). Traduzir sua fala diretamente para inglês evita a "tradução mental" na hora de programar e garante que nomes de variáveis, métodos e comandos sejam gerados de forma idiomática e consistente com o ecossistema — resultando em código mais limpo, legível e compatível com as ferramentas do mercado.

---

## ✨ Funcionalidades

- **Ditado com push-to-talk** — segure a tecla (ou alterne liga/desliga) para gravar; solte para transcrever e digitar automaticamente.
- **Modo Code** — a fala é **traduzida para inglês** antes de ser digitada, ideal para escrever código.
- **Modo Chat** — transcreve no **idioma que você falou** (português, inglês, espanhol, francês ou detecção automática).
- **Atalhos globais configuráveis** — funciona em qualquer aplicativo, mesmo em segundo plano na bandeja.
- **Dicionário personalizado** — adicione termos técnicos e nomes de produtos para melhorar a precisão.
- **Feedback sonoro** — bip ao iniciar/parar a gravação, com **controle de volume**.
- **Captura de região e visão** — selecione uma região da tela e capture frames dela.
- **Histórico** — todas as transcrições ficam salvas e podem ser copiadas.
- **Backup** — exporte/importe configurações, dicionário e histórico em um arquivo JSON.
- **Autostart e bandeja** — inicia com o sistema e fica minimizado na bandeja.
- **Atualização automática** — o app verifica e instala novas versões automaticamente.

---

## 🚀 Instalação

Baixe o instalador da **última versão** na página de [Releases](https://github.com/jorgebrunetto/voicecode-release/releases):

| Sistema | Pacote |
| --- | --- |
| **Windows** | `.msi` ou `.exe` (NSIS) |
| **Linux** | `.deb`, `.rpm` ou `.AppImage` |

Depois de instalar:

1. **Abra o aplicativo** — a primeira tela pede a sua **Groq API Key**.
2. **Crie uma chave gratuita** em [console.groq.com](https://console.groq.com) (o plano gratuito já é suficiente).
3. Cole a chave e clique em **Salvar API Key**.
4. Pronto! Pressione **F8** em qualquer aplicativo e fale.

> A API key é armazenada com segurança no **keyring** do sistema operacional (Windows Credential Manager / libsecret no Linux), nunca em arquivos de texto.

---

## 🎮 Como usar

### Teclas padrão

| Tecla | Ação |
| --- | --- |
| **F8** | Gravar/transcrever (segurar ou alternar, conforme o modo configurado) |
| **F9** | Alternar entre modo **Chat** e **Code** |
| **F10** | Capturar um frame da região de tela selecionada |
| **F11** | Abrir o seletor de região de captura |

Todas as teclas podem ser **reconfiguradas** na aba **Atalhos**.

### Modos de transcrição

| Modo | Comportamento |
| --- | --- |
| **Code** | Traduz tudo para **inglês** e digita — perfeito para código e comandos. |
| **Chat** | Transcreve no **idioma falado** selecionado (ou auto-detect). |

- **Modo de fala** (aba Atalhos): **Segurar** (push-to-talk clássico) ou **Alternar** (aperte F8 para ligar, aperte de novo para desligar).

### Abas do aplicativo

- **Status** — estado atual, API key, preferências (autostart, bandeja, som), volume do bip e backup.
- **Atalhos** — configuração das teclas globais e do modo de fala.
- **Microfone** — seleção e teste do dispositivo de entrada.
- **Idioma** — idioma da interface, idioma falado e modelo de transcrição.
- **Dicionário** — termos técnicos personalizados (prompt para o Whisper).
- **Histórico** — transcrições passadas, com cópia e limpeza.
- **Gravação** — captura de região de tela.

---

## 🔧 Tecnologia

- **Tauri v2** — aplicação desktop leve (nativa Rust + WebView).
- **React 19 + TypeScript + Vite** — interface.
- **Groq API (Whisper)** — transcrição/audição por IA.
- **cpal** — captura de áudio e feedback sonoro.
- **enigo** — digitação automática via teclado virtual.
- **xcap** — captura de tela e seleção de região.
- **Tauri updater** — atualização automática via `latest.json`.

---

## 📦 Estrutura do repositório

```
latest.json          # Manifesto do updater (gerado automaticamente pelo CI)
```

Os instaladores e assinaturas (`.sig`) ficam nas **Releases** deste repositório, não no código-fonte.

---

## 🔄 Atualizações

O aplicativo verifica atualizações na aba Status (botão de versão na barra lateral) e automaticamente na inicialização. Quando há uma versão nova, o updater baixa e instala de forma transparente.

O processo é gerenciado por CI no repositório de código-fonte ([voicecode-source](https://github.com/jorgebrunetto/voicecode-source)), que publica aqui:
1. Build **Windows** (`.msi` + `.exe`, com assinaturas de updater).
2. Build **Linux** (`.deb`, `.rpm`, `.AppImage`, com assinaturas).
3. Manifesto `latest.json` com as URLs e assinaturas de cada plataforma.

---

## 🤝 Feedback e suporte

Encontrou um bug ou tem uma sugestão? Abra uma **issue** no repositório [voicecode-source](https://github.com/jorgebrunetto/voicecode-source/issues).
