# Portfolio
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>João Lucas (JJ) — Portfólio</title>
<meta name="description" content="Portfólio pessoal de João Lucas, técnico em Informática para Internet, com as entregas do módulo Mundo do Trabalho.">

<!-- Única exceção a "sem bibliotecas": fontes do Google Fonts, exatamente as escolhidas -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@500;700&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">

<style>
  /* =========================================================
     VARIÁVEIS DE COR (paleta "Minha própria", exatamente como pedida)
     fundo = rubro-negro | texto = vermelho intenso + preto
     primária = vermelho | secundária = preto | destaque = mistura vermelho+preto
     ========================================================= */
  :root{
    --cor-fundo: #140506;          /* fundo geral: preto puxando pro vermelho ("rubro-negro") */
    --cor-secundaria: #0a0a0a;     /* preto puro: painéis, nav, botões secundários */
    --cor-primaria: #e5162c;       /* vermelho: bordas, títulos grandes, marcações */
    --cor-texto-vermelho: #ff3b47; /* vermelho intenso: cor de texto sobre fundo escuro (parágrafos, links) */
    --cor-texto-preto: #111111;    /* preto: cor de texto sobre superfícies claras (moldura do polaroid) */
    --cor-moldura: #f2f0ec;        /* branco/creme da moldura polaroid — exigido pelo estilo de card escolhido */
    --cor-destaque-a: #e5162c;     /* ponta 1 do gradiente "mistura forte de vermelho e preto" */
    --cor-destaque-b: #5c0e18;     /* ponta do meio (vinho), reforça a mistura */
    --cor-destaque-c: #0a0a0a;     /* ponta 2 do gradiente */

    --fonte-titulo: 'Space Grotesk', sans-serif;
    --fonte-texto: 'Inter', sans-serif;

    --pad-x: clamp(1.25rem, 5vw, 4rem);
    --altura-nav: 4.25rem;
  }

  /* =========================================================
     RESET BÁSICO
     ========================================================= */
  *, *::before, *::after{ box-sizing: border-box; }
  html{ scroll-behavior: smooth; background: var(--cor-fundo); }
  body{
    margin: 0;
    background: var(--cor-fundo);
    color: var(--cor-texto-vermelho);
    font-family: var(--fonte-texto);
    -webkit-font-smoothing: antialiased;
    overflow-x: hidden;
  }
  h1,h2,h3,p,ul{ margin:0; padding:0; }
  ul{ list-style:none; }
  a{ color: inherit; text-decoration: none; }
  img, svg{ max-width: 100%; display:block; }
  h1,h2,h3{ font-family: var(--fonte-titulo); }

  /* estado de foco visível, pra quem navega pelo teclado */
  a:focus-visible, button:focus-visible{
    outline: 2px solid var(--cor-texto-vermelho);
    outline-offset: 3px;
  }

  .container{
    max-width: 1180px;
    margin: 0 auto;
    padding-left: var(--pad-x);
    padding-right: var(--pad-x);
  }

  /* linha fina usada como divisória entre seções */
  .divisoria-fina{
    border-top: 1px solid rgba(229,22,44,0.25);
  }

  /* =========================================================
     BARRA DE PROGRESSO DE LEITURA (detalhe extra escolhido)
     fica fixa no topo e cresce conforme o usuário rola a página
     ========================================================= */
  .barra-progresso{
    position: fixed; top: 0; left: 0;
    height: 4px; width: 0%;
    background: var(--cor-texto-vermelho);
    z-index: 100;
    transition: width 0.15s linear;
  }

  /* =========================================================
     MENU DE NAVEGAÇÃO — barra fixa no topo
     ========================================================= */
  .nav-fixa{
    position: fixed; top: 0; left: 0; right: 0; z-index: 90;
    background: rgba(10,10,10,0.88);
    border-bottom: 1px solid rgba(229,22,44,0.25);
    backdrop-filter: blur(6px);
  }
  .nav-container{
    max-width: 1180px; margin: 0 auto;
    padding: 0.85rem var(--pad-x);
    display: flex; align-items: center; justify-content: space-between;
    gap: 1rem;
  }
  .nav-logo{
    font-family: var(--fonte-titulo); font-weight: 700;
    font-size: 1.1rem; color: var(--cor-texto-vermelho);
  }
  .nav-links{
    display: flex; gap: 1.4rem;
    overflow-x: auto; /* pra não quebrar layout em telas bem estreitas (360px) */
    -webkit-overflow-scrolling: touch;
  }
  .nav-links a{
    font-size: 0.92rem; font-weight: 500; white-space: nowrap;
    color: var(--cor-texto-vermelho);
    padding: 0.3rem 0.1rem;
    border-bottom: 1px solid transparent;
    transition: border-color 0.3s ease;
  }
  .nav-links a:hover{ border-bottom-color: var(--cor-primaria); }

  /* =========================================================
     MANCHAS DE COR DESFOCADAS — fundo decorativo da página inteira
     ========================================================= */
  .manchas{
    position: fixed; inset: 0; z-index: 0; overflow: hidden; pointer-events: none;
  }
  .mancha{
    position: absolute; border-radius: 50%;
    filter: blur(90px);
    opacity: 0.35;
  }
  .mancha-1{ width: 420px; height: 420px; background: var(--cor-primaria); top: -10%; left: -8%; }
  .mancha-2{ width: 380px; height: 380px; background: var(--cor-destaque-b); top: 40%; right: -10%; }
  .mancha-3{ width: 320px; height: 320px; background: var(--cor-primaria); bottom: -8%; left: 20%; opacity: 0.25; }

  /* conteúdo real da página fica acima das manchas */
  main, footer{ position: relative; z-index: 1; }

  /* =========================================================
     1. HERO (TOPO) — centralizado: avatar em cima, nome e frase embaixo
     ========================================================= */
  .hero{
    min-height: 100svh;
    display: flex; align-items: center; justify-content: center;
    text-align: center;
    padding: calc(var(--altura-nav) + 2rem) var(--pad-x) 3rem;
    position: relative; overflow: hidden;
  }
  /* elemento interativo principal: gradiente de fundo que se move devagar */
  .hero-gradiente{
    position: absolute; inset: -20%; z-index: -1;
    background: linear-gradient(120deg, var(--cor-destaque-c), var(--cor-destaque-b), var(--cor-destaque-a), var(--cor-destaque-c));
    background-size: 300% 300%;
    animation: mover-gradiente 22s ease-in-out infinite;
  }
  @keyframes mover-gradiente{
    0%{ background-position: 0% 50%; }
    50%{ background-position: 100% 50%; }
    100%{ background-position: 0% 50%; }
  }

  .hero-conteudo{ display: flex; flex-direction: column; align-items: center; gap: 1.5rem; max-width: 640px; }

  /* avatar circular (placeholder com as iniciais do apelido) */
  .avatar-foto{
    width: clamp(140px, 32vw, 190px);
    aspect-ratio: 1 / 1;
    border-radius: 50%;
    background: linear-gradient(160deg, var(--cor-secundaria), var(--cor-destaque-b));
    border: 3px solid var(--cor-primaria);
    display: flex; align-items: center; justify-content: center;
  }
  .avatar-foto span{
    font-family: var(--fonte-titulo); font-weight: 700;
    font-size: clamp(2rem, 6vw, 2.8rem);
    color: var(--cor-texto-vermelho);
  }

  .hero-nome{
    font-weight: 700; letter-spacing: -0.02em; line-height: 0.98;
    font-size: clamp(2.6rem, 9vw, 5.2rem);
    color: var(--cor-primaria);
  }
  .hero-frase{
    font-size: clamp(1.05rem, 2vw, 1.3rem); line-height: 1.6;
    max-width: 40ch; color: var(--cor-texto-vermelho);
  }
  .hero-pills{ display: flex; flex-wrap: wrap; justify-content: center; gap: 0.6rem; }
  .pill{
    font-size: 0.82rem; font-weight: 500;
    border: 1px solid rgba(255,59,71,0.45);
    border-radius: 100px; padding: 0.4rem 0.9rem;
  }

  /* =========================================================
     DETALHE EXCLUSIVO — coisas que só existem nesta página
     ========================================================= */
  .detalhe-exclusivo{ padding: 3rem 0; }
  .detalhe-exclusivo h2{
    font-size: clamp(1.4rem, 3vw, 1.9rem); color: var(--cor-primaria); margin-bottom: 1.5rem;
  }
  .lista-detalhe{ display: grid; gap: 0.9rem; max-width: 520px; }
  .lista-detalhe li{
    display: flex; justify-content: space-between; gap: 1rem;
    border-bottom: 1px solid rgba(255,59,71,0.18);
    padding-bottom: 0.7rem; font-size: 0.98rem;
  }
  .detalhe-rotulo{ color: var(--cor-texto-vermelho); opacity: 0.9; }
  .detalhe-valor{ font-weight: 600; color: var(--cor-texto-vermelho); text-align: right; }

  /* =========================================================
     SEÇÕES GERAIS
     ========================================================= */
  .section{ padding: clamp(3.5rem, 8vw, 6rem) 0; scroll-margin-top: var(--altura-nav); }
  .section h2{
    font-size: clamp(1.9rem, 4.4vw, 2.6rem); color: var(--cor-primaria);
    letter-spacing: -0.01em; margin-bottom: 1rem;
  }
  .section p{ font-size: 1.02rem; line-height: 1.8; max-width: 62ch; color: var(--cor-texto-vermelho); }
  .sobre p + p{ margin-top: 1.1rem; }

  /* =========================================================
     ANIMAÇÃO AO ROLAR — entram alternando pela esquerda e direita
     ========================================================= */
  [data-reveal]{
    opacity: 0;
    transition: opacity 0.6s ease, transform 0.6s cubic-bezier(.16,.84,.44,1);
  }
  [data-reveal="esquerda"]{ transform: translateX(-40px); }
  [data-reveal="direita"]{ transform: translateX(40px); }
  [data-reveal].revelado{ opacity: 1; transform: none; }

  /* =========================================================
     3. MINHAS ENTREGAS — cards estilo "janela de terminal"
     (barrinha no topo com 3 bolinhas, tipo um editor de código)
     ========================================================= */
  .entregas-intro{ margin-bottom: 2.5rem; }
  .grade-cards{
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1.75rem;
  }

  .card-terminal{
    background: var(--cor-secundaria);
    border: 1px solid rgba(255,59,71,0.22);
    border-radius: 6px;
    overflow: hidden; /* mantém a barrinha e a foto dentro dos cantos arredondados */
    box-shadow: 6px 6px 0 var(--cor-primaria);
    transition: transform 0.4s cubic-bezier(.16,.84,.44,1), box-shadow 0.4s cubic-bezier(.16,.84,.44,1);
  }
  .card-terminal:hover{ transform: translateY(-4px); box-shadow: 9px 9px 0 var(--cor-primaria); }

  /* barrinha do topo da janela, com as 3 bolinhas (só nos tons da paleta) */
  .janela-topo{
    display: flex; align-items: center; gap: 0.4rem;
    background: #050202;
    padding: 0.6rem 0.85rem;
    border-bottom: 1px solid rgba(255,59,71,0.16);
  }
  .ponto{ width: 9px; height: 9px; border-radius: 50%; }
  .ponto-1{ background: var(--cor-primaria); }
  .ponto-2{ background: var(--cor-texto-vermelho); }
  .ponto-3{ background: transparent; border: 1px solid var(--cor-primaria); }
  .janela-nome{ margin-left: auto; font-size: 0.72rem; color: var(--cor-texto-vermelho); opacity: 0.9; }

  .card-foto{
    aspect-ratio: 4 / 3;
    overflow: hidden; /* necessário pro efeito de zoom não vazar da janela */
    background: linear-gradient(150deg, var(--cor-destaque-c), var(--cor-destaque-b));
    display: flex; align-items: center; justify-content: center;
  }
  .card-foto svg{
    width: 46%; height: 46%;
    transition: transform 0.4s ease; /* efeito ao passar o mouse: zoom leve na imagem */
  }
  .card-terminal:hover .card-foto svg{ transform: scale(1.12); }

  .card-corpo{ padding: 1rem 1.1rem 1.2rem; color: var(--cor-texto-vermelho); }
  .card-topo-legenda{ display: flex; align-items: center; justify-content: space-between; }
  .card-numero{ font-family: var(--fonte-titulo); font-weight: 700; font-size: 0.85rem; opacity: 0.9; }

  .selo{
    font-size: 0.7rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.03em;
    padding: 0.25rem 0.6rem; border-radius: 100px;
  }
  .selo-concluida{ background: var(--cor-texto-vermelho); color: var(--cor-texto-preto); }
  .selo-em-breve{ background: rgba(255,59,71,0.08); color: var(--cor-texto-vermelho); border: 1px solid rgba(255,59,71,0.45); }

  .card-titulo{ font-size: 1.08rem; font-weight: 700; margin-top: 0.6rem; color: var(--cor-texto-vermelho); }
  .card-data{ display: block; font-size: 0.78rem; opacity: 0.9; margin-top: 0.15rem; }
  .card-aprendi{ font-size: 0.92rem; line-height: 1.55; margin-top: 0.6rem; }

  .card-link{
    display: inline-block; margin-top: 0.9rem;
    font-size: 0.88rem; font-weight: 700; color: var(--cor-texto-vermelho);
    border-bottom: 2px solid var(--cor-primaria);
  }
  .card-indisponivel{
    display: inline-block; margin-top: 0.9rem;
    font-size: 0.85rem; font-weight: 600; opacity: 0.9;
  }

  /* card "Em breve": aparência apagada e sem link clicável */
  .card-terminal.em-breve{ opacity: 0.55; }
  .card-terminal.em-breve .card-foto{ filter: grayscale(0.6); }

  /* =========================================================
     4. MANIFESTO — recolhido com botão "Ler manifesto completo"
     ========================================================= */
  .manifesto-teaser{ margin-bottom: 1.25rem; }
  .manifesto-corpo{
    max-height: 0; overflow: hidden;
    transition: max-height 0.6s ease, opacity 0.5s ease;
    opacity: 0;
  }
  .manifesto-corpo.aberto{ max-height: 1200px; opacity: 1; margin-bottom: 1.5rem; }
  .manifesto-corpo p{ font-style: italic; opacity: 0.92; }

  /* =========================================================
     BOTÕES / LINKS — quadrado com sombra dura
     ========================================================= */
  .botao{
    display: inline-block;
    font-family: var(--fonte-texto); font-weight: 700; font-size: 0.95rem;
    background: var(--cor-texto-vermelho);
    color: var(--cor-texto-preto);
    padding: 0.85rem 1.6rem;
    border: none; border-radius: 0; /* quadrado */
    box-shadow: 5px 5px 0 var(--cor-secundaria);
    cursor: pointer;
    transition: transform 0.3s cubic-bezier(.16,.84,.44,1), box-shadow 0.3s cubic-bezier(.16,.84,.44,1);
  }
  .botao:hover{ transform: translate(-3px,-3px); box-shadow: 8px 8px 0 var(--cor-secundaria); }
  .botao-secundario{
    background: var(--cor-secundaria); color: var(--cor-texto-vermelho);
    box-shadow: 5px 5px 0 var(--cor-primaria);
  }
  .botao-secundario:hover{ box-shadow: 8px 8px 0 var(--cor-primaria); }

  /* =========================================================
     RODAPÉ
     ========================================================= */
  .rodape{ padding: 3.5rem 0 2.5rem; }
  .rodape h2{ font-size: clamp(1.6rem, 3.6vw, 2.1rem); color: var(--cor-primaria); margin-bottom: 0.8rem; }
  .rodape p{ margin-bottom: 1.75rem; }
  .rodape-links{ display: flex; flex-wrap: wrap; gap: 1rem; }
  .rodape-nota{
    margin-top: 3rem; padding-top: 1.5rem; border-top: 1px solid rgba(255,59,71,0.18);
    font-size: 0.78rem; opacity: 0.9; display: flex; flex-wrap: wrap; gap: 0.5rem; justify-content: space-between;
  }

  /* =========================================================
     RESPONSIVO — testado mentalmente em 360px de largura
     ========================================================= */
  @media (max-width: 480px){
    .nav-links{ gap: 1rem; }
    .card-polaroid{ padding: 0.5rem 0.5rem 0.8rem; }
    .lista-detalhe li{ flex-direction: column; gap: 0.2rem; }
    .detalhe-valor{ text-align: left; }
  }

  /* =========================================================
     RESPEITA "REDUZIR MOVIMENTO" — desliga todas as animações
     ========================================================= */
  @media (prefers-reduced-motion: reduce){
    html{ scroll-behavior: auto; }
    *{ animation-duration: 0.01ms !important; animation-iteration-count: 1 !important; transition-duration: 0.01ms !important; }
    [data-reveal]{ opacity: 1 !important; transform: none !important; }
  }
</style>
</head>
<body>

  <!-- barra de progresso de leitura, atualizada via JS conforme o scroll -->
  <div class="barra-progresso" id="barraProgresso" aria-hidden="true"></div>

  <!-- menu fixo no topo -->
  <header class="nav-fixa">
    <div class="nav-container">
      <a href="#topo" class="nav-logo">JJ</a>
      <nav class="nav-links" aria-label="Navegação principal">
        <a href="#sobre">Sobre</a>
        <a href="#entregas">Entregas</a>
        <a href="#manifesto">Manifesto</a>
        <a href="#contato">Contato</a>
      </nav>
    </div>
  </header>

  <!-- manchas de cor desfocadas atrás de todo o conteúdo -->
  <div class="manchas" aria-hidden="true">
    <span class="mancha mancha-1"></span>
    <span class="mancha mancha-2"></span>
    <span class="mancha mancha-3"></span>
  </div>

  <main id="topo">

    <!-- ===================== 1. TOPO (HERO) ===================== -->
    <section class="hero" id="hero">
      <div class="hero-gradiente" aria-hidden="true"></div>
      <div class="hero-conteudo">
        <!-- avatar circular com as iniciais do apelido (JJ), no lugar de uma foto real -->
        <div class="avatar-foto" role="img" aria-label="Avatar de João Lucas, apelido JJ">
          <span>JJ</span>
        </div>
        <h1 class="hero-nome">João Lucas</h1>
        <p class="hero-frase">Fanático pelo Flamengo, sempre ligado em futebol, outros esportes e games.</p>
        <!-- as três coisas que me definem -->
        <div class="hero-pills">
          <span class="pill">Flamengo</span>
          <span class="pill">Futebol</span>
          <span class="pill">Games</span>
        </div>
      </div>
    </section>

    <div class="divisoria-fina"></div>

    <!-- ===================== DETALHE QUE SÓ EXISTE AQUI ===================== -->
    <section class="detalhe-exclusivo" data-reveal="esquerda">
      <div class="container">
        <h2>Isso aqui só tem na minha página</h2>
        <ul class="lista-detalhe">
          <li><span class="detalhe-rotulo">Time</span><span class="detalhe-valor">Flamengo</span></li>
          <li><span class="detalhe-rotulo">Jogo favorito</span><span class="detalhe-valor">BMPES</span></li>
          <li><span class="detalhe-rotulo">Trilha sonora</span><span class="detalhe-valor">Astrothunder, Travis Scott</span></li>
          <li><span class="detalhe-rotulo">Curiosidade</span><span class="detalhe-valor">Também curto assistir tênis</span></li>
        </ul>
      </div>
    </section>

    <div class="divisoria-fina"></div>

    <!-- ===================== 2. SOBRE MIM ===================== -->
    <section class="section sobre" id="sobre">
      <div class="container">
        <h2 data-reveal="direita">Sobre mim</h2>
        <p data-reveal="direita">Eu, João Lucas, gosto muito de futebol. Não importa o que eu esteja fazendo no meu tempo livre, ou eu tô assistindo futebol ou eu tô jogando futebol. Além do futebol, gosto de jogar GTA, BMPES, Far Cry 3, Garry's Mod e Left 4 Dead 2, com mods e tudo mais.</p>
        <p data-reveal="direita">Falando mais sobre mim, eu sou um cara bem mais sério, mas com os amigos eu sempre acabo me abrindo mais.</p>
      </div>
    </section>

    <div class="divisoria-fina"></div>

    <!-- ===================== 3. MINHAS ENTREGAS ===================== -->
    <section class="section entregas" id="entregas">
      <div class="container">
        <h2 data-reveal="esquerda">Minhas entregas</h2>
        <p class="entregas-intro" data-reveal="esquerda">As atividades do módulo Mundo do Trabalho, uma por uma.</p>

        <div class="grade-cards">

          <!-- Card 1: Capa do Meu Álbum -->
          <article class="card-terminal" data-reveal="esquerda">
            <div class="janela-topo" aria-hidden="true">
              <span class="ponto ponto-1"></span><span class="ponto ponto-2"></span><span class="ponto ponto-3"></span>
              <span class="janela-nome">01-capa-do-album.md</span>
            </div>
            <div class="card-foto">
              <svg viewBox="0 0 32 32" fill="none" aria-hidden="true">
                <circle cx="16" cy="16" r="12" stroke="var(--cor-primaria)" stroke-width="1.6"/>
                <circle cx="16" cy="16" r="4" stroke="var(--cor-primaria)" stroke-width="1.6"/>
                <circle cx="16" cy="16" r="1.3" fill="var(--cor-primaria)"/>
              </svg>
            </div>
            <div class="card-corpo">
              <div class="card-topo-legenda">
                <span class="card-numero">01</span>
                <span class="selo selo-concluida">Concluída</span>
              </div>
              <h3 class="card-titulo">Capa do Meu Álbum</h3>
              <span class="card-data">[DATA DA ENTREGA]</span>
              <p class="card-aprendi">Pensei em como resumir quem eu sou numa capa só, tipo se fosse lançar um álbum de verdade.</p>
              <a class="card-link" href="https://github.com/Jotalucs/SEU-REPOSITORIO/tree/main/01-capa-do-album" target="_blank" rel="noopener">Ver pasta no GitHub</a>
            </div>
          </article>

          <!-- Card 2: Dashboard Quem Sou Eu -->
          <article class="card-terminal" data-reveal="direita">
            <div class="janela-topo" aria-hidden="true">
              <span class="ponto ponto-1"></span><span class="ponto ponto-2"></span><span class="ponto ponto-3"></span>
              <span class="janela-nome">02-dashboard.md</span>
            </div>
            <div class="card-foto">
              <svg viewBox="0 0 32 32" fill="none" aria-hidden="true">
                <rect x="5" y="5" width="9" height="9" rx="1.5" stroke="var(--cor-primaria)" stroke-width="1.6"/>
                <rect x="18" y="5" width="9" height="9" rx="1.5" stroke="var(--cor-primaria)" stroke-width="1.6"/>
                <rect x="5" y="18" width="9" height="9" rx="1.5" stroke="var(--cor-primaria)" stroke-width="1.6"/>
                <rect x="18" y="18" width="9" height="9" rx="1.5" stroke="var(--cor-primaria)" stroke-width="1.6"/>
              </svg>
            </div>
            <div class="card-corpo">
              <div class="card-topo-legenda">
                <span class="card-numero">02</span>
                <span class="selo selo-concluida">Concluída</span>
              </div>
              <h3 class="card-titulo">Dashboard Quem Sou Eu</h3>
              <span class="card-data">[DATA DA ENTREGA]</span>
              <p class="card-aprendi">Organizei um painel com informações sobre mim e treinei como deixar isso visual e fácil de entender.</p>
              <a class="card-link" href="https://github.com/Jotalucs/SEU-REPOSITORIO/tree/main/02-dashboard" target="_blank" rel="noopener">Ver pasta no GitHub</a>
            </div>
          </article>

          <!-- Card 3: Árvore das Profissões 2.0 -->
          <article class="card-terminal" data-reveal="esquerda">
            <div class="janela-topo" aria-hidden="true">
              <span class="ponto ponto-1"></span><span class="ponto ponto-2"></span><span class="ponto ponto-3"></span>
              <span class="janela-nome">03-arvore-das-profissoes.md</span>
            </div>
            <div class="card-foto">
              <svg viewBox="0 0 32 32" fill="none" aria-hidden="true">
                <path d="M16 27V15M16 15L9 8M16 15L23 8M16 20L11 15M16 20L21 15" stroke="var(--cor-primaria)" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/>
              </svg>
            </div>
            <div class="card-corpo">
              <div class="card-topo-legenda">
                <span class="card-numero">03</span>
                <span class="selo selo-concluida">Concluída</span>
              </div>
              <h3 class="card-titulo">Árvore das Profissões 2.0</h3>
              <span class="card-data">[DATA DA ENTREGA]</span>
              <p class="card-aprendi">Vi que dentro de TI dá pra seguir vários caminhos diferentes, não é só uma profissão só.</p>
              <a class="card-link" href="https://github.com/Jotalucs/SEU-REPOSITORIO/tree/main/03-arvore-das-profissoes" target="_blank" rel="noopener">Ver pasta no GitHub</a>
            </div>
          </article>

          <!-- Card 4: Âncoras de Carreira -->
          <article class="card-terminal" data-reveal="direita">
            <div class="janela-topo" aria-hidden="true">
              <span class="ponto ponto-1"></span><span class="ponto ponto-2"></span><span class="ponto ponto-3"></span>
              <span class="janela-nome">04-ancoras-de-carreira.md</span>
            </div>
            <div class="card-foto">
              <svg viewBox="0 0 32 32" fill="none" aria-hidden="true">
                <circle cx="16" cy="7" r="3" stroke="var(--cor-primaria)" stroke-width="1.6"/>
                <path d="M16 10V27M8 19c0 4.4 3.6 8 8 8s8-3.6 8-8M6 15h6m8 0h6" stroke="var(--cor-primaria)" stroke-width="1.6" stroke-linecap="round"/>
              </svg>
            </div>
            <div class="card-corpo">
              <div class="card-topo-legenda">
                <span class="card-numero">04</span>
                <span class="selo selo-concluida">Concluída</span>
              </div>
              <h3 class="card-titulo">Âncoras de Carreira</h3>
              <span class="card-data">[DATA DA ENTREGA]</span>
              <p class="card-aprendi">Parei pra pensar no que realmente me move no trabalho, tipo o que eu não abriria mão.</p>
              <a class="card-link" href="https://github.com/Jotalucs/SEU-REPOSITORIO/tree/main/04-ancoras-de-carreira" target="_blank" rel="noopener">Ver pasta no GitHub</a>
            </div>
          </article>

          <!-- Card 5: Manifesto (ainda não pronto -> selo "Em breve", sem link) -->
          <article class="card-terminal em-breve" data-reveal="esquerda">
            <div class="janela-topo" aria-hidden="true">
              <span class="ponto ponto-1"></span><span class="ponto ponto-2"></span><span class="ponto ponto-3"></span>
              <span class="janela-nome">05-manifesto.md</span>
            </div>
            <div class="card-foto">
              <svg viewBox="0 0 32 32" fill="none" aria-hidden="true">
                <path d="M9 4h11l5 5v19a1 1 0 0 1-1 1H9a1 1 0 0 1-1-1V5a1 1 0 0 1 1-1z" stroke="var(--cor-primaria)" stroke-width="1.6" stroke-linejoin="round"/>
                <path d="M13 15h8M13 20h8M13 10h4" stroke="var(--cor-primaria)" stroke-width="1.6" stroke-linecap="round"/>
              </svg>
            </div>
            <div class="card-corpo">
              <div class="card-topo-legenda">
                <span class="card-numero">05</span>
                <span class="selo selo-em-breve">Em breve</span>
              </div>
              <h3 class="card-titulo">Manifesto</h3>
              <span class="card-data">[DATA DA ENTREGA]</span>
              <p class="card-aprendi">Ainda tô escrevendo, mas vai ser sobre os valores que eu quero levar pra minha carreira.</p>
              <span class="card-indisponivel">Pasta ainda não disponível</span>
            </div>
          </article>

        </div>
      </div>
    </section>

    <div class="divisoria-fina"></div>

    <!-- ===================== 4. MANIFESTO ===================== -->
    <section class="section manifesto" id="manifesto">
      <div class="container">
        <h2 data-reveal="direita">Manifesto</h2>
        <p class="manifesto-teaser" data-reveal="direita">Ainda tô escrevendo essa parte com calma. Dá pra abrir o rascunho aqui embaixo.</p>

        <!-- corpo recolhido por padrão; o JS abre e fecha ao clicar no botão -->
        <div class="manifesto-corpo" id="manifestoCorpo">
          <p>[MANIFESTO AQUI]</p>
        </div>

        <button class="botao botao-secundario" id="botaoManifesto" type="button" aria-expanded="false" aria-controls="manifestoCorpo">
          Ler manifesto completo
        </button>
      </div>
    </section>

  </main>

  <div class="divisoria-fina"></div>

  <!-- ===================== RODAPÉ ===================== -->
  <footer class="rodape" id="contato">
    <div class="container">
      <h2>Cola comigo</h2>
      <p>Time, jogo ou curso de TI, qualquer assunto é motivo pra trocar uma ideia.</p>
      <div class="rodape-links">
        <a class="botao" href="https://github.com/Jotalucs" target="_blank" rel="noopener">GitHub</a>
        <a class="botao botao-secundario" href="https://instagram.com/hitex_fx" target="_blank" rel="noopener">Instagram</a>
      </div>
      <div class="rodape-nota">
        <span>© 2026 João Lucas (JJ)</span>
        <span>Módulo Mundo do Trabalho</span>
      </div>
    </div>
  </footer>

<script>
  // =========================================================
  // BARRA DE PROGRESSO DE LEITURA
  // calcula quanto já foi rolado da página e atualiza a largura da barra
  // =========================================================
  var barra = document.getElementById('barraProgresso');
  function atualizarBarraProgresso(){
    var alturaTotal = document.documentElement.scrollHeight - window.innerHeight;
    var progresso = alturaTotal > 0 ? (window.scrollY / alturaTotal) * 100 : 0;
    barra.style.width = progresso + '%';
  }
  window.addEventListener('scroll', atualizarBarraProgresso, { passive: true });
  window.addEventListener('resize', atualizarBarraProgresso);
  atualizarBarraProgresso();

  // =========================================================
  // ANIMAÇÃO AO ROLAR A PÁGINA
  // observa os elementos com [data-reveal] e adiciona a classe "revelado"
  // quando eles entram na tela (o CSS cuida de vir da esquerda ou da direita)
  // =========================================================
  var elementosParaRevelar = document.querySelectorAll('[data-reveal]');
  if('IntersectionObserver' in window){
    var observador = new IntersectionObserver(function(entradas){
      entradas.forEach(function(entrada){
        if(entrada.isIntersecting){
          entrada.target.classList.add('revelado');
          observador.unobserve(entrada.target);
        }
      });
    }, { threshold: 0.15 });
    elementosParaRevelar.forEach(function(el){ observador.observe(el); });
  } else {
    // navegador sem suporte: mostra tudo direto, sem animação
    elementosParaRevelar.forEach(function(el){ el.classList.add('revelado'); });
  }

  // =========================================================
  // SEÇÃO MANIFESTO RECOLHIDA
  // clique no botão abre/fecha o texto do manifesto
  // =========================================================
  var botaoManifesto = document.getElementById('botaoManifesto');
  var corpoManifesto = document.getElementById('manifestoCorpo');
  botaoManifesto.addEventListener('click', function(){
    var aberto = corpoManifesto.classList.toggle('aberto');
    botaoManifesto.setAttribute('aria-expanded', aberto ? 'true' : 'false');
    botaoManifesto.textContent = aberto ? 'Fechar manifesto' : 'Ler manifesto completo';
  });
</script>

</body>
</html>
