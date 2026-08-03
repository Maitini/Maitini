<meta charset="utf-8">
<title>Cabecera Maitini</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">

<style>
  :root{
    --base:#07070C;
    --panel:#12121C;
    --key:#16161F;
    --violeta:#B026FF;
    --cian:#00E5FF;
    --claro:#F2F0FF;
    --apagado:#6A6A85;
  }

  *{box-sizing:border-box;margin:0;padding:0}

  body{
    background:#22222B;
    min-height:100vh;
    display:flex;
    flex-direction:column;
    align-items:center;
    justify-content:center;
    gap:28px;
    padding:40px 20px;
    font-family:'Space Grotesk',system-ui,sans-serif;
  }

  .escala{
    transform-origin:top center;
  }

  /* ── el lienzo que vas a capturar ───────────────── */
  .cabecera{
    position:relative;
    width:1200px;
    height:420px;
    background:var(--base);
    border-radius:20px;
    overflow:hidden;
    display:grid;
    grid-template-columns:1fr 520px;
    align-items:center;
  }

  .rejilla{
    position:absolute;
    inset:0;
    background-image:
      linear-gradient(rgba(255,255,255,.028) .5px,transparent .5px),
      linear-gradient(90deg,rgba(255,255,255,.028) .5px,transparent .5px);
    background-size:60px 60px;
    pointer-events:none;
  }

  .borde-sup{
    position:absolute;top:0;left:0;right:0;height:2px;
    background:linear-gradient(90deg,var(--cian),var(--violeta));
    transform:scaleX(0);transform-origin:left;
  }
  .go .borde-sup{animation:barrer .9s cubic-bezier(.2,.8,.2,1) forwards}
  @keyframes barrer{to{transform:scaleX(1)}}

  /* ── columna izquierda ──────────────────────────── */
  .texto{padding:0 0 0 72px;position:relative;z-index:2}

  .eyebrow{
    font-family:'JetBrains Mono',monospace;
    font-size:13px;letter-spacing:.14em;
    color:var(--cian);
    opacity:0;
  }
  .go .eyebrow{animation:entrar .6s ease .15s forwards}

  .nombre{
    font-size:88px;font-weight:700;letter-spacing:-.035em;
    color:var(--claro);line-height:1;
    margin:18px 0 0;
    opacity:0;
  }
  .go .nombre{animation:entrar .7s cubic-bezier(.2,.8,.2,1) .3s forwards}

  .subrayado{
    height:3px;width:0;
    background:var(--violeta);
    margin:20px 0 22px;
  }
  .go .subrayado{animation:crecer .8s cubic-bezier(.2,.8,.2,1) 1.9s forwards}
  @keyframes crecer{to{width:210px}}

  .rol{
    font-size:19px;font-weight:400;color:var(--claro);
    letter-spacing:-.01em;opacity:0;
  }
  .rol span{color:var(--apagado)}
  .go .rol{animation:entrar .6s ease .5s forwards}

  .pie{
    font-family:'JetBrains Mono',monospace;
    font-size:12.5px;color:var(--apagado);
    margin-top:14px;opacity:0;
  }
  .go .pie{animation:entrar .6s ease .65s forwards}

  @keyframes entrar{
    from{opacity:0;transform:translateY(10px)}
    to{opacity:1;transform:none}
  }

  /* ── el deck ────────────────────────────────────── */
  .deck{
    display:grid;
    grid-template-columns:repeat(3,148px);
    grid-template-rows:repeat(2,92px);
    gap:16px;
    position:relative;z-index:2;
  }

  .tecla{
    background:var(--key);
    border:1px solid rgba(255,255,255,.07);
    border-radius:14px;
    display:flex;flex-direction:column;
    justify-content:flex-end;
    padding:14px;
    font-family:'JetBrains Mono',monospace;
    font-size:11.5px;
    color:var(--apagado);
    opacity:.35;
  }
  .tecla i{
    display:block;width:9px;height:9px;border-radius:50%;
    background:#2A2A3A;margin-bottom:auto;
  }

  .go .tecla{animation:encender .5s ease forwards}
  .go .tecla:nth-child(1){animation-delay:.75s}
  .go .tecla:nth-child(2){animation-delay:.88s}
  .go .tecla:nth-child(3){animation-delay:1.01s}
  .go .tecla:nth-child(4){animation-delay:1.14s}
  .go .tecla:nth-child(5){animation-delay:1.27s}
  .go .tecla:nth-child(6){animation-delay:1.40s}

  @keyframes encender{
    0%{opacity:.35;transform:translateY(0)}
    45%{opacity:1;transform:translateY(3px)}
    100%{opacity:1;transform:translateY(0);
      color:var(--claro);
      border-color:var(--violeta);
      background:#1A1426;}
  }
  .go .tecla:nth-child(2n) {animation-name:encender-cian}
  @keyframes encender-cian{
    0%{opacity:.35;transform:translateY(0)}
    45%{opacity:1;transform:translateY(3px)}
    100%{opacity:1;transform:translateY(0);
      color:var(--claro);
      border-color:var(--cian);
      background:#0E1E24;}
  }
  .go .tecla:nth-child(1) i,.go .tecla:nth-child(3) i,.go .tecla:nth-child(5) i{
    animation:puntoV .4s ease 1.5s forwards}
  .go .tecla:nth-child(2) i,.go .tecla:nth-child(4) i,.go .tecla:nth-child(6) i{
    animation:puntoC .4s ease 1.5s forwards}
  @keyframes puntoV{to{background:var(--violeta)}}
  @keyframes puntoC{to{background:var(--cian)}}

  /* ── el pulso: del deck al nombre ───────────────── */
  .cable{
    position:absolute;
    left:72px;right:520px;
    top:236px;height:1px;
    background:rgba(255,255,255,.08);
    z-index:1;
  }
  .pulso{
    position:absolute;top:0;right:0;
    width:70px;height:1px;
    background:linear-gradient(90deg,transparent,var(--cian));
    opacity:0;
  }
  .go .pulso{animation:viajar .9s cubic-bezier(.4,0,.2,1) 1.55s forwards}
  @keyframes viajar{
    0%{opacity:1;transform:translateX(0)}
    99%{opacity:1;transform:translateX(calc(-100% - 540px))}
    100%{opacity:0}
  }

  /* ── controles fuera del lienzo ─────────────────── */
  .controles{display:flex;gap:10px;align-items:center}
  button{
    font-family:'JetBrains Mono',monospace;font-size:12.5px;
    color:#D9D9E6;background:#2E2E3A;
    border:1px solid #43434F;border-radius:8px;
    padding:9px 16px;cursor:pointer;
  }
  button:hover{background:#3A3A48}
  button:focus-visible{outline:2px solid var(--cian);outline-offset:2px}
  .nota{
    font-family:'JetBrains Mono',monospace;
    font-size:12px;color:#8A8A99;text-align:center;max-width:640px;
    line-height:1.7;
  }

  @media (prefers-reduced-motion:reduce){
    .go *{animation-duration:.01ms!important;animation-delay:0ms!important}
  }
</style>

<div class="escala" id="escala">
  <div class="cabecera go" id="lienzo">
    <div class="rejilla"></div>
    <div class="borde-sup"></div>
    <div class="cable"><div class="pulso"></div></div>

    <div class="texto">
      <p class="eyebrow">DESDE ESPAÑA</p>
      <h1 class="nombre">Maitini</h1>
      <div class="subrayado"></div>
      <p class="rol">Construyo herramientas <span>y las diseño yo mismo</span></p>
      <p class="pie">java · php · javascript · after effects</p>
    </div>

    <div class="deck">
      <div class="tecla"><i></i>keyforge</div>
      <div class="tecla"><i></i>centinela</div>
      <div class="tecla"><i></i>serverguard</div>
      <div class="tecla"><i></i>custommobs</div>
      <div class="tecla"><i></i>overlays</div>
      <div class="tecla"><i></i>motion</div>
    </div>
  </div>
</div>

<div class="controles">
  <button id="repetir">Repetir animación</button>
  <button id="congelar">Congelar al final</button>
</div>

<p class="nota">Lienzo de 1200 × 420 px. Captura solo el rectángulo negro.</p>

<script>
  const lienzo = document.getElementById('lienzo');
  const escala = document.getElementById('escala');

  document.getElementById('repetir').onclick = () => {
    lienzo.classList.remove('go');
    void lienzo.offsetWidth;
    lienzo.classList.add('go');
  };

  document.getElementById('congelar').onclick = () => {
    lienzo.getAnimations({subtree:true}).forEach(a => a.finish());
  };

  const ajustar = () => {
    const s = Math.min(1, (window.innerWidth - 60) / 1200);
    escala.style.transform = `scale(${s})`;
    escala.style.height = `${420 * s}px`;
  };
  ajustar();
  window.addEventListener('resize', ajustar);
</script>


<br>

### Proyectos

| | |
|---|---|
| **[KeyForge](https://github.com/Maitini/keyforge)** | Tu móvil como mando del PC. Macros, atajos, OBS, Spotify y luces. Más de 19 integraciones y emparejamiento por QR |
| **[Centinela-WP](https://github.com/Maitini/Centinela-WP)** | Seguridad todo en uno para WordPress: antivirus, cortafuegos, 2FA y copias de seguridad |
| **[ServerGuard](https://github.com/Maitini/ServerGuard)** | Anticheat para Minecraft 1.21.1 |
| **[custommobs](https://github.com/Maitini/custommobs)** | Mobs personalizados para Minecraft 1.21.1 |


<br>

### Hablamos

[Instagram](https://www.instagram.com/maitini1812/)
