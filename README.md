# GymOS

> Aplicativo web estático para visualização de planos de treino organizados por nível e grupo muscular.
>
> Static web app for visualizing workout plans organized by level and muscle group.

---

## 🇧🇷 Português

### Sobre

O GymOS é uma aplicação web estática que exibe planos de treino de academia de forma visual e organizada. Os treinos são agrupados por **nível de dificuldade** e **grupo muscular**, com suporte a exercícios avulsos, bisets e trisets. O nível e o treino selecionados são persistidos localmente no navegador.

### Estrutura do Projeto

```
gymos/
├── index.html          # Aplicação principal
├── training-plan.json  # Dados dos treinos (fonte única de verdade)
└── README.md           # Este arquivo
```

### Como Executar Localmente

O aplicativo usa `fetch()` para carregar o JSON, o que requer um servidor HTTP. Abrir o `index.html` diretamente pelo sistema de arquivos (`file://`) não funcionará.

**Opção 1 — Node.js**
```bash
cd gymos
npx serve .
```
Acesse: `http://localhost:3000`

**Opção 2 — Python**
```bash
cd gymos
python3 -m http.server 8080
```
Acesse: `http://localhost:8080`

**Opção 3 — VS Code**

Instale a extensão [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) e clique em **Go Live** no canto inferior direito.

### Como Hospedar

O projeto é totalmente estático — basta colocar os dois arquivos (`index.html` e `training-plan.json`) na mesma pasta raiz de qualquer servidor ou serviço de hospedagem estática.

**Netlify Drop (mais rápido)**
1. Acesse [app.netlify.com/drop](https://app.netlify.com/drop)
2. Arraste a pasta `gymos/` para a página
3. Receba uma URL pública instantaneamente

**GitHub Pages**
1. Crie um repositório no GitHub
2. Faça upload dos arquivos
3. Vá em Settings → Pages → Branch: main → Save

### Como Adicionar Novos Níveis ou Treinos

Edite apenas o arquivo `training-plan.json`. A UI se adapta automaticamente.

**Adicionar um novo nível:**
```json
{
  "level": 3,
  "name": "Nível 3",
  "workouts": [
    {
      "name": "Nome do Treino",
      "groups": [ ... ]
    }
  ]
}
```

**Tipos de grupo suportados:**

| Tipo | Descrição | Visual |
|------|-----------|--------|
| `single` | Exercício avulso ou seção | Fundo escuro padrão |
| `biset` | Dois exercícios em sequência | Fundo verde escuro |
| `triset` | Três exercícios em sequência | Fundo azul-escuro/roxo |

Grupos cujo `label` contenha `aquec` ou `ativa` são tratados como aquecimento (destaque azul, sem emoji).

### Lógica de Imagens

- Exercícios com tags de **membros inferiores** (`Glúteo`, `Quadríceps`, `Posterior`, etc.) exibem o emoji 🦵
- Exercícios de **aquecimento/ativação** exibem um bloco escuro neutro
- Demais exercícios carregam fotos do [Unsplash](https://unsplash.com) baseadas nas tags, com emoji 💪 como fallback

---

## 🇺🇸 English

### About

GymOS is a static web app that displays gym workout plans in a clean, visual layout. Workouts are organized by **difficulty level** and **muscle group**, supporting single exercises, bisets, and trisets. The selected level and workout are persisted locally in the browser.

### Project Structure

```
gymos/
├── index.html          # Main application
├── training-plan.json  # Workout data (single source of truth)
└── README.md           # This file
```

### Running Locally

The app uses `fetch()` to load the JSON, which requires an HTTP server. Opening `index.html` directly from the filesystem (`file://`) will not work.

**Option 1 — Node.js**
```bash
cd gymos
npx serve .
```
Open: `http://localhost:3000`

**Option 2 — Python**
```bash
cd gymos
python3 -m http.server 8080
```
Open: `http://localhost:8080`

**Option 3 — VS Code**

Install the [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) extension and click **Go Live** in the bottom-right corner.

### Hosting

The project is fully static — just place both files (`index.html` and `training-plan.json`) in the same root folder of any static hosting service.

**Netlify Drop (fastest)**
1. Go to [app.netlify.com/drop](https://app.netlify.com/drop)
2. Drag the `gymos/` folder onto the page
3. Get a public URL instantly

**GitHub Pages**
1. Create a GitHub repository
2. Upload both files
3. Go to Settings → Pages → Branch: main → Save

### Adding New Levels or Workouts

Edit only `training-plan.json`. The UI adapts automatically.

**Adding a new level:**
```json
{
  "level": 3,
  "name": "Level 3",
  "workouts": [
    {
      "name": "Workout Name",
      "groups": [ ... ]
    }
  ]
}
```

**Supported group types:**

| Type | Description | Visual |
|------|-------------|--------|
| `single` | Standalone exercise or section | Default dark background |
| `biset` | Two exercises in sequence | Dark green background |
| `triset` | Three exercises in sequence | Dark blue/purple background |

Groups whose `label` contains `aquec` or `ativa` are treated as warm-up sections (blue highlight, no emoji).

### Image Logic

- Exercises tagged as **lower body** (`Glúteo`, `Quadríceps`, `Posterior`, etc.) show the 🦵 emoji
- **Warm-up/activation** exercises show a plain dark block with no emoji
- All other exercises load photos from [Unsplash](https://unsplash.com) based on their tags, with 💪 as fallback