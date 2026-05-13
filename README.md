<h1 align="center">Headbutt Berserker</h1>

<p align="center">
Jogo VR/WebXR de reflexos em que o jogador enfrenta inimigos usando movimentos de cabeça, histórico de desempenho e um assistente inteligente baseado em regras.
</p>

<hr>

## 🎮 Conceito

**Headbutt Berserker** é um jogo em realidade virtual no qual o jogador controla um viking sem braços que luta contra inimigos usando cabeçadas, esquivas laterais e agachamentos.

O protótipo atual usa **A-Frame/WebXR** para rastrear a câmera/cabeça do jogador. Também há suporte a teclado para testes no desktop:

- `↑` atacar;
- `←` esquivar para a esquerda;
- `→` esquivar para a direita;
- `↓` agachar;
- `Esc` abrir/fechar menu de pausa no desktop.

> Observação: a visão computacional aparece como evolução futura do projeto. A versão atual usa rastreamento de cabeça pelo WebXR/A-Frame.

<hr>

## ⚡ Treinamento de reflexos

Durante as partidas, o jogo registra métricas como:

- tempo médio de reação;
- acertos e erros;
- precisão por ação;
- timeouts;
- desempenho por fase;
- histórico das últimas partidas.

Essas informações são salvas no arquivo `db.json` e exibidas no menu de histórico.

<hr>

## 🧠 Assistente IA

A aba **Assistente IA** já possui uma primeira versão funcional baseada em regras. Ela analisa o histórico recente e gera recomendações como:

- aumentar dificuldade quando a precisão e o tempo de reação estão bons;
- reduzir dificuldade quando há muitos erros;
- treinar ações específicas com menor precisão;
- ajustar o modo customizado quando há muitos timeouts.

Essa abordagem não usa machine learning ainda, mas já funciona como um assistente inteligente baseado em métricas de desempenho.

<hr>

## 🧰 Tecnologias utilizadas

- **Node.js** para o servidor HTTP;
- **A-Frame 1.5.0** para a cena VR/WebXR;
- **aframe-environment-component** para ambiente 3D;
- **JavaScript puro** no front-end;
- **JSON local (`db.json`)** para histórico de desempenho.

<hr>

## 🚀 Como rodar localmente

Requisitos:

- Node.js 18 ou superior;
- navegador moderno;
- headset compatível com WebXR para jogar em VR, ou teclado para teste em desktop.

Instale e rode:

```bash
npm install
npm start
```

Acesse:

```text
http://localhost:3000
```

Para validar sintaxe dos arquivos principais:

```bash
npm run check
```

<hr>

## 🌐 Servidor público / deploy

O projeto já está preparado para hospedagem pública com:

- `HOST=0.0.0.0`;
- `PORT` por variável de ambiente;
- rota de saúde em `/api/health`;
- `Dockerfile`;
- `render.yaml`;
- `.env.example`.

### Opção rápida: Render

1. Suba este projeto para o GitHub.
2. Crie um novo **Web Service** no Render.
3. Selecione o repositório.
4. Use:
   - Build Command: `npm install`
   - Start Command: `npm start`
5. Configure as variáveis:
   - `HOST=0.0.0.0`
   - `NODE_ENV=production`
   - `CORS_ORIGIN=*`
6. Abra a URL gerada pelo Render.

### Opção com Docker

```bash
docker build -t headbutt-berserker .
docker run -p 3000:3000 -e HOST=0.0.0.0 headbutt-berserker
```

Depois acesse:

```text
http://localhost:3000
```

### Persistência em produção

Por padrão, o histórico fica em `db.json`. Em hospedagens gratuitas, esse arquivo pode ser apagado quando o serviço reiniciar.

Para produção real, use uma destas opções:

- disco persistente e variável `DB_PATH`, por exemplo `/data/db.json`;
- banco externo como PostgreSQL, MongoDB ou Firebase.

<hr>

## 📁 Estrutura principal

```text
server.js
package.json
db.json
public/
  index.html
  style.css
  scripts/
    state.js
    ui.js
    gameplay.js
    components.js
```

<hr>

## 🔮 Melhorias futuras

- integrar visão computacional real com câmera;
- substituir o assistente por modelo de IA/ML;
- salvar usuários separados;
- usar banco externo em produção;
- adicionar ranking e estatísticas por sessão;
- melhorar calibração VR inicial.

<hr>

## Referência

- A-Frame Environment Component: https://github.com/supermedium/aframe-environment-component
