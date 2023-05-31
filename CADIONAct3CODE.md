# CADIONAct3
To be submitted to Sir Rustico
<!DOCTYPE html>
<html>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <style>
        body {
            margin: 0;
            padding: 0;
            overflow: hidden;
            background-color: #87CEEB;
        }
        #game-container {
            position: relative;
            width: 100%;
            height: 100vh;
        }
        .player {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 50px;
            height: 70px;
            background-color: #FF0000;
        }
    </style>
</head>
<body>
    <div id="game-container">
        <div class="player"></div>
    </div>

    <script>
        // Player object
        var player = {
            element: document.querySelector('.player'),
            position: {
                x: 0,
                y: 0
            },
            velocity: {
                x: 0,
                y: 0
            },
            isJumping: false,
            jumpPower: 15,
            gravity: 1
        };

        // Keyboard controls
        var keys = {};
        document.addEventListener('keydown', function(e) {
            keys[e.code] = true;
        });
        document.addEventListener('keyup', function(e) {
            keys[e.code] = false;
        });

        // Game loop
        function gameLoop() {
            // Update player
            updatePlayer();

            // Update game objects
            updateGameObjects();

            // Call the game loop again
            requestAnimationFrame(gameLoop);
        }

        // Update player position based on controls
        function updatePlayer() {
            if (keys['ArrowLeft']) {
                player.velocity.x = -5;
            } else if (keys['ArrowRight']) {
                player.velocity.x = 5;
            } else {
                player.velocity.x = 0;
            }

            if (keys['Space'] && !player.isJumping) {
                player.isJumping = true;
                player.velocity.y = -player.jumpPower;
            }

            // Apply gravity
            player.velocity.y += player.gravity;

            // Update player position
            player.position.x += player.velocity.x;
            player.position.y += player.velocity.y;

            // Limit player position within game container
            if (player.position.x < 0) {
                player.position.x = 0;
            }
            if (player.position.x + player.element.clientWidth > document.getElementById('game-container').clientWidth) {
                player.position.x = document.getElementById('game-container').clientWidth - player.element.clientWidth;
            }
            if (player.position.y < 0) {
                player.position.y = 0;
            }
            if (player.position.y + player.element.clientHeight > document.getElementById('game-container').clientHeight) {
                player.position.y = document.getElementById('game-container').clientHeight - player.element.clientHeight;
                player.isJumping = false;
                player.velocity.y = 0;
            }

            // Update player element position
            player.element.style.left = player.position.x + 'px';
            player.element.style.bottom = player.position.y + 'px';
        }

        // Update other game objects
        function updateGameObjects() {
            // Add code to update other game objects here
        }

        // Start the game loop
        gameLoop();
    </script>
</body>
</html>
