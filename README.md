<title>Jogo da Memória do Amor 💘</title>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(#ffc0cb, #ffe4e1);
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      min-height: 100vh;
      text-align: center; /* Centraliza tudo dentro do body */
    }

    h1 {
      color: #d6336c;
      margin-top: 40px;
    }

    .instrucoes {
      font-size: 1.2rem;
      margin-bottom: 20px;
    }

    .tabuleiro {
      display: grid;
      grid-template-columns: repeat(4, 100px);
      gap: 15px;
      justify-content: center;
      margin-bottom: 30px;
    }

    .carta {
      width: 100px;
      height: 100px;
      background: white;
      border-radius: 12px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      font-size: 2rem;
      transition: transform 0.3s ease;
      user-select: none;
    }

    .carta.virada {
      background-color: #fff0f5;
      transform: rotateY(180deg);
    }

    #vitoria {
      background: #fff0f5;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      max-width: 300px;
    }

    .escondido {
      display: none;
    }
  </style>
</head>
<body>
  <h1>Jogo da Memória do Amor 💘</h1>
  <p class="instrucoes">Encontre todos os pares!</p>

  <div class="tabuleiro" id="tabuleiro"></div>

  <div id="vitoria" class="escondido">
    <h2>Parabéns, amor da minha vida! ❤️</h2>
    <p>Você completou nosso jogo da memória.<br>
    Então queria te convidar para um encontro na quinta-feira, dia 12/06 💕</p>
  </div>

  <script>
    const emojis = ['💕','💜','💛','💙','💚','❤️'];
    let cartas = [...emojis, ...emojis];
    cartas = cartas.sort(() => 0.5 - Math.random());

    const tabuleiro = document.getElementById('tabuleiro');
    let primeiraCarta = null;
    let bloqueado = false;
    let paresEncontrados = 0;

    cartas.forEach((emoji, index) => {
      const carta = document.createElement('div');
      carta.classList.add('carta');
      carta.dataset.valor = emoji;
      carta.dataset.index = index;
      carta.innerHTML = ''; // começa sem mostrar

      carta.addEventListener('click', () => {
        if (bloqueado || carta.classList.contains('virada')) return;

        carta.classList.add('virada');
        carta.innerHTML = emoji;

        if (!primeiraCarta) {
          primeiraCarta = carta;
        } else {
          if (
            primeiraCarta.dataset.valor === carta.dataset.valor &&
            primeiraCarta.dataset.index !== carta.dataset.index
          ) {
            primeiraCarta = null;
            paresEncontrados++;
            if (paresEncontrados === emojis.length) {
              document.getElementById('vitoria').classList.remove('escondido');
            }
          } else {
            bloqueado = true;
            setTimeout(() => {
              primeiraCarta.classList.remove('virada');
              primeiraCarta.innerHTML = '';
              carta.classList.remove('virada');
              carta.innerHTML = '';
              primeiraCarta = null;
              bloqueado = false;
            }, 1000);
          }
        }
      });

      tabuleiro.appendChild(carta);
    });
  </script>
</body>
</html>
