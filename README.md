<!DOCTYPE html>
<html>
<head>
    <title>Snake Game</title>
    <style>
        #game {
            border: 1px solid black;
            display: block;
            margin: 0 auto;
        }
    </style>
</head>
<body>
    <div id="game"></div>

    <script>
        const canvas = document.getElementById('game');
        const ctx = canvas.getContext('2d');

        const snake = {
            x: 10,
            y: 10,
            dx: 10,
            dy: 0,
            cells: [],
            maxCells: 4
        };

        const food = {
            x: 30,
            y: 30
        };

        const grid = 20;
        const cw = canvas.width = 300;
        const ch = canvas.height = 300;

        function loop() {
            requestAnimationFrame(loop);
            update();
            render();
        }

        function update() {
            snake.x += snake.dx;
            snake.y += snake.dy;

            if (snake.x < 0) {
                snake.x = cw - grid;
            } else if (snake.x >= cw) {
                snake.x = 0;
            }

            if (snake.y < 0) {
                snake.y = ch - grid;
            } else if (snake.y >= ch) {
                snake.y = 0;
            }

            if (snake.x === food.x && snake.y === food.y) {
                snake.maxCells++;
                food.x = getRandomInt(0, (cw / grid) - 1) * grid;
                food.y = getRandomInt(0, (ch / grid) - 1) * grid;
            }

            for (let i = snake.cells.length - 1; i > 0; i--) {
                snake.cells[i] = snake.cells[i - 1];
            }
            snake.cells[0] = { x: snake.x, y: snake.y };

            if (snake.cells.length > snake.maxCells - 1) {
                snake.cells.pop();
            }

            for (let i = 1; i < snake.cells.length; i++) {
                if (snake.cells[i].x === snake.x && snake.cells[i].y === snake.y) {
                    snake.x = 10;
                    snake.y = 10;
                    snake.cells = [];
                    snake.maxCells = 4;
                }
            }
        }

        function render() {
            ctx.fillStyle = 'black';
            ctx.fillRect(0, 0, cw, ch);

            ctx.fillStyle = 'lime';
            ctx.fillRect(food.x, food.y, grid - 1, grid - 1);

            for (let i = 0; i < snake.cells.length; i++) {
                ctx.fillRect(snake.cells[i].x, snake.cells[i].y, grid - 1, grid - 1);
            }
        }

        function getRandomInt(min, max) {
            return Math.floor(Math.random() * (max - min + 1)) + min;
        }

        document.addEventListener('keydown', function (e) {
            switch (e.keyCode) {
                case 37:
                    snake.dx = -grid;
                    snake.dy = 0;
                    break;
                case 38:
                    snake.dx = 0;
                    snake.dy = -grid;
                    break;
                case 39:
                    snake.dx = grid;
                    snake.dy = 0;
                    break;
                case 40:
                    snake.dx = 0;
                    snake.dy = grid;
                    break;
            }
        });

        loop();
    </script>
</body>
</html>
