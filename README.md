<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <title>Projeto ADS - Snake Game</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #1a1a1a;
            color: white;
            font-family: sans-serif;
            flex-direction: column;
        }
        canvas {
            border: 4px solid #3498db;
            background-color: #000;
        }
    </style>
</head>
<body>

    <h1>Snake Game - ADS 🐍</h1>
    <canvas id="stage" width="400" height="400"></canvas>
    <p>Use as setas do teclado para jogar!</p>

    <script type="text/javascript">
        
        window.onload = function() {
            var stage = document.getElementById('stage');
            var ctx = stage.getContext("2d");
            document.addEventListener("keydown", keyPush);
            
            // Configurações do Jogo
            var velocidade = 80; // ms
            var tp = 20; // Tamanho do ponto (grid)
            var qp = 20; // Quantidade de pontos (400/20 = 20)
            
            var vx = 0; var vy = 0; // Velocidade inicial (parado)
            var px = 10; var py = 10; // Posição inicial da cabeça
            var ax = 15; var ay = 15; // Posição inicial da maçã
            
            var trail = []; // Rastro/Corpo da cobra
            var tail = 5;   // Tamanho da cauda

            setInterval(game, velocidade);

            function game() {
                px += vx;
                py += vy;

                // Lógica de atravessar a parede
                if (px < 0) px = qp - 1;
                if (px > qp - 1) px = 0;
                if (py < 0) py = qp - 1;
                if (py > qp - 1) py = 0;

                // Limpa o fundo
                ctx.fillStyle = "black";
                ctx.fillRect(0, 0, stage.width, stage.height);

                // Desenha a maçã
                ctx.fillStyle = "red";
                ctx.fillRect(ax * tp, ay * tp, tp, tp);

                // Desenha a cobra
                ctx.fillStyle = "lime";
                for (var i = 0; i < trail.length; i++) {
                    ctx.fillRect(trail[i].x * tp, trail[i].y * tp, tp - 1, tp - 1);
                    
                    // Se bater no próprio corpo
                    if (trail[i].x == px && trail[i].y == py && (vx != 0 || vy != 0)) {
                        vx = vy = 0;
                        tail = 5;
                    }
                }

                trail.push({x: px, y: py});
                while (trail.length > tail) {
                    trail.shift();
                }

                // Comer a maçã
                if (ax == px && ay == py) {
                    tail++;
                    ax = Math.floor(Math.random() * qp);
                    ay = Math.floor(Math.random() * qp);
                }
            }

            function keyPush(event) {
                switch (event.keyCode) {
                    case 37: // Esquerda
                        if (vx === 0) { vx = -1; vy = 0; }
                        break;
                    case 38: // Cima
                        if (vy === 0) { vx = 0; vy = -1; }
                        break;
                    case 39: // Direita
                        if (vx === 0) { vx = 1; vy = 0; }
                        break;
                    case 40: // Baixo
                        if (vy === 0) { vx = 0; vy = 1; }
                        break;
                }
            }
        }
    </script>
</body>
</html># Snake-game
Jogo feito em JavaScript, Snake game
