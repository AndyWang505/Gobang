<!DOCTYPE html>
<html>
    <head>
        <meta content="text/html; charset=UTF-8" http-equiv="Content-Type" />
        <title>兒童/青少年/初學者程式設計線上課程</title>
        <meta name="csrf-param" content="authenticity_token" />
        <meta name="csrf-token" content="y6ip8QfuFQkPuHq7mn+Fl4ubhq+P0PSBM51F7vFSEfgMQ3swXoJT81NFz9z6Py7A61lduM1/EDxwN5wJABzhIA==" />
        </head>
        <body style="margin:0px">
        <div id="container" style="width:100vw; height: 100vh; display:flex; align-items:center; justify-content:center;">
        <div id="stagebox" style="position: relative;">
        <canvas height="480" id="stage" style="background-color:#006980; display:block;" width="640"></canvas>
        <div id="gamepad_arrow" style="transform: rotate(45deg); position: absolute; bottom: 0; right: 70px;">
        <img class="gamepad-btn" id="key_down" style="transform: rotate(135deg); bottom: 0; right: 0;" src="https://cdn3.koding.school/assets/gamepad/arrow-c2dcda3fd8057f62fff9241e03e7f3b06666451049999d4ed2b3632b91f92646.svg" alt="Arrow" /><img class="gamepad-btn" id="key_right" style="transform: rotate(45deg); bottom: 55px; right: 0;" src="https://cdn3.koding.school/assets/gamepad/arrow-c2dcda3fd8057f62fff9241e03e7f3b06666451049999d4ed2b3632b91f92646.svg" alt="Arrow" /><img class="gamepad-btn" id="key_left" style="transform: rotate(-135deg); bottom: 0; right: 55px;" src="https://cdn3.koding.school/assets/gamepad/arrow-c2dcda3fd8057f62fff9241e03e7f3b06666451049999d4ed2b3632b91f92646.svg" alt="Arrow" /><img class="gamepad-btn" id="key_up" style="transform: rotate(-45deg); bottom: 55px; right: 55px;" src="https://cdn3.koding.school/assets/gamepad/arrow-c2dcda3fd8057f62fff9241e03e7f3b06666451049999d4ed2b3632b91f92646.svg" alt="Arrow" /></div><div id="gamepad_wasd" style="transform: rotate(45deg); position: absolute; bottom: 0; right: calc(100% - 70px);"><img class="gamepad-btn" id="key_s" style="transform: rotate(-45deg); bottom: 0; right: 0;" src="https://cdn7.koding.school/assets/gamepad/key_s-e0d41d68d299e1fafb641796b923f237f30ad696a5ee12ef64a61a3723445b3c.svg" alt="Key s" /><img class="gamepad-btn" id="key_d" style="transform: rotate(-45deg); bottom: 55px; right: 0;" src="https://cdn7.koding.school/assets/gamepad/key_d-dfc8fe5801e48f9ac08719e2a5fe980d8cbeece164092254a346a81fb667feb3.svg" alt="Key d" /><img class="gamepad-btn" id="key_a" style="transform: rotate(-45deg); bottom: 0; right: 55px;" src="https://cdn1.koding.school/assets/gamepad/key_a-1602901ced445e05ed887d6da6970e091bf086a18d7d8fffbd6786a59fa40eda.svg" alt="Key a" /><img class="gamepad-btn" id="key_w" style="transform: rotate(-45deg); bottom: 55px; right: 55px;" src="https://cdn7.koding.school/assets/gamepad/key_w-467c96ce07af2e3f0c3f99d1da8dedc832758b8083f7ca2eb185b76129b5f6c8.svg" alt="Key w" /></div><img class="gamepad-btn" id="toggle_gamepad" style="top: 5px; right: 5px; width: 30px; height: 30px;" src="https://cdn1.koding.school/assets/gamepad/gamepad-f162bdefa53838fed4d91e02bf7276c0f9cac356b4e631759c62a555cafa8055.svg" alt="Gamepad" /><img class="gamepad-btn" id="toggle_sound" style="top: 40px; right: 5px; width: 30px; height: 30px;" src="https://cdn0.koding.school/assets/gamepad/note-06f5103c2355b5ccde538cb0f94907296fefb867e11e3b5c395897389e9f355b.svg" alt="Note" />
        </div>
        </div>
        <script>var TOKEN = "s8mzbvsuoku15dhvdv3mlmnrwcbyzy68",
        PROJECT_ID = 'd5ms59qg',
        PROJECT_LANGUAGE = 'javascript',
        USER_ID = 14203,
        USER_NAME = "Chengwei",
        ENV = "production";
        </script>
        <script src="/assets/sandbox/game-eee82796364a2db6a8977d028e83134aa47b80598e6c9c2d39865cf15b4706c3.js"></script>
        <textarea id="mainCode" style="display: none;"></textarea>
        <textarea id="pluginCode" style="display: none;">setBackdrop(&#39;bg.png&#39;);
    
    const BLACK = &#39;b&#39;;
    const WHITE = &#39;w&#39;;
    const ZZ = [0, 0, 0, 0, 0, 0, 0, 0, 0];
    const V1 = [4, 3, 2, 1, 0, -1, -2, -3, -4];
    const V2 = [-4, -3, -2, -1, 0, 1, 2, 3, 4];
    
    
    var game = (function () {
    
        let grid = {};
        for (let x = -14; x &lt;= 29; x++) {
            grid[x] = {};
            for (let y = -14; y &lt;= 29; y++) {
                grid[x][y] = &#39;&#39;;
            }
        }
    
        function isWin (x, y, vx, vy) {
            var re = grid[x + vx*0][y + vy*0] +
                     grid[x + vx*1][y + vy*1] +
                     grid[x + vx*2][y + vy*2] +
                     grid[x + vx*3][y + vy*3] +
                     grid[x + vx*4][y + vy*4];
    
            if (re == &#39;bbbbb&#39;) {
                drawText(&#39;黑方獲勝&#39;);
                stop();
            }
            if (re == &#39;wwwww&#39;) {
                drawText(&#39;白方獲勝&#39;);
                stop();
            }
        }
        
        //當玩家點擊格子時
        function onclick () {
            var x = Math.floor((cursor.x - 97)/30);
            var y = Math.floor((cursor.y - 17)/30);
    
            if (x &lt; 0 || x &gt;= 15 || y &lt; 0 || y &gt;= 15) return;
            
            place(x, y) &amp;&amp; AI();
        }
    
        //繪製棋子
        function render () {
            for (var x = 0; x &lt; 15; x++) {
                for (var y = 0; y &lt; 15; y++) {
                    pen.size = 0;
                    if (grid[x][y] == &#39;&#39;) continue;
                    if (grid[x][y] == BLACK) pen.fillColor = &#39;black&#39;;
                    if (grid[x][y] == WHITE) pen.fillColor = &#39;white&#39;;
                    pen.drawCircle(x*30 + 110, y*30 + 30, 14);
                }
            }
            for (var x = 0; x &lt; 15; x++) {
                for (var y = 0; y &lt; 15; y++) {
                    isWin(x, y, 1, 0);
                    isWin(x, y, -1, 0);
                    isWin(x, y, 0, 1);
                    isWin(x, y, 0, -1);
                    isWin(x, y, 1, 1);
                    isWin(x, y, -1, 1);
                    isWin(x, y, 1, -1);
                    isWin(x, y, -1, -1);
                }
            }
        }
    
        function place (x, y) {
    
            if (grid[x][y] !== &#39;&#39;) return false;
    
            var count = 0;
            for (var xx = 0; xx &lt; 15; xx++) {
                for (var yy = 0; yy &lt; 15; yy++) {
                    if (grid[xx][yy] !== &#39;&#39;) count++;
                }
            }
            grid[x][y] = count%2 === 0 ? BLACK: WHITE;
            
            return true;
        }
    
        function check(color, x, y) {
    
            if (color == &#39;white&#39; || color == BLACK) color = WHITE;
            if (color == &#39;black&#39; || color == WHITE) color = BLACK;
    
            var temp = grid[x][y];
            grid[x][y] = color;
            var result = [0, 1, 0, 0, 0, 0];
            var a, b, c;
            var start, len;
            for (len = 5; len &gt;= 2; len--) {
                for (start = 5 - len; start &lt;= 4; start++) {
                    z = ZZ.slice(start, start + len);
                    d = V1.slice(start, start + len);
                    i = V2.slice(start, start + len);
                    if (checkLine(grid, x, y, d, z, color)) result[len]++;
                    if (checkLine(grid, x, y, z, d, color)) result[len]++;
                    if (checkLine(grid, x, y, d, d, color)) result[len]++;
                    if (checkLine(grid, x, y, d, i, color)) result[len]++;
                }
            }
    
            grid[x][y] = temp;
    
            return result;
        }
    
        function checkLine(grid, x, y, vx, vy, who) {
            for (var i = 0; i &lt; vx.length; i++) {
                var xx = x + vx[i];
                var yy = y + vy[i];
                if (grid[xx][yy] != who) return false;
            }
            return true;
        }
    
        when(&#39;click&#39;, onclick);
        forever(render);
    
        return {
            place: place,
            current: BLACK,
            grid: grid,
        };
    })();
    
    grid = game.grid;
    
    // 黑子(電腦)先下
    grid[7][7] = &#39;b&#39;;
    
    forever(update);
    
    // 印出評估函式計算的分數在每個格子上
    function update () {
        for (var x = 0; x &lt; 15; x++) {
            for (var y = 0; y &lt; 15; y++) {
                if (grid[x][y] == &#39;&#39;) {
                    grid[x][y] = &#39;b&#39;;
                    var score = evaluate(x, y, grid);
                    grid[x][y] = &#39;w&#39;;
                    score += evaluate(x, y, grid);
                    grid[x][y] = &#39;&#39;;
                    drawText(score, 115 + x*30, 35 + y*30, &#39;black&#39;, 10);
                }
            }
        }
    }
    
    // 當玩家下完會觸發 AI 函式換電腦下棋
    function AI() {
        var bestScore = 0;
        var bestX;
        var bestY;
        for (var x = 0; x &lt; 15; x++) {
            for (var y = 0; y &lt; 15; y++) {
                if (grid[x][y] == &#39;&#39;) {
                    grid[x][y] = &#39;b&#39;;
                    var score = evaluate(x, y, grid)*1.1;
                    grid[x][y] = &#39;w&#39;;
                    score += evaluate(x, y, grid);
                    grid[x][y] = &#39;&#39;;
                    if (score &gt; bestScore) {
                        bestScore = score;
                        bestX = x;
                        bestY = y;
                    }
                }
            }
        }
        grid[bestX][bestY] = &#39;b&#39;;
    }
    
    // 評估函式，組合八個方向的分數
    // top(上)、bottom(下)、right(右)、left(左)
    // topRight(上右)、topLeft(上左)、bottomRight(下右)、bottomLeft(下左)
    function evaluate (x, y) {
        var G = grid;
        var t  = getScore(G[x][y], G[x][y-1], G[x][y-2], G[x][y-3], G[x][y-4]);
        var b  = getScore(G[x][y], G[x][y+1], G[x][y+2], G[x][y+3], G[x][y+4]);
        var r  = getScore(G[x][y], G[x+1][y], G[x+2][y], G[x+3][y], G[x+4][y]);
        var l  = getScore(G[x][y], G[x-1][y], G[x-2][y], G[x-3][y], G[x-4][y]);
        var tr = getScore(G[x][y], G[x+1][y-1], G[x+2][y-2], G[x+3][y-3], G[x+4][y-4]);
        var bl = getScore(G[x][y], G[x-1][y+1], G[x-2][y+2], G[x-3][y+3], G[x-4][y+4]);
        var tl = getScore(G[x][y], G[x-1][y-1], G[x-2][y-2], G[x-3][y-3], G[x-4][y-4]);
        var br = getScore(G[x][y], G[x+1][y+1], G[x+2][y+2], G[x+3][y+3], G[x+4][y+4]);
        
        return t*b + r*l + tr*bl + tl*br;
    }
    
    // 傳入五個格子內容，計算連成幾個
    function getScore (a, b, c, d, e) {
        if (b != a) return 1;
        if (c != a) return 10;
        if (d != a) return 100;
        if (e != a) return 1000;
        return 10000;
    }</textarea><script>function htmlDecode(input){
        var doc = new DOMParser().parseFromString(input, "text/html");
      return doc.documentElement.textContent;
    }
    
    Game.preload(["bg.png"], function() {
        DB.ready(function(){
            var pluginCode = htmlDecode(document.getElementById('pluginCode').innerHTML);
            var mainCode = htmlDecode(document.getElementById('mainCode').innerHTML);
            eval.call(window, pluginCode);
            eval.call(window, mainCode);
            Game.start();
        });
    });</script><style type="text/css">.gamepad-btn {
      display: none;
      position: absolute;
      width: 50px;
      height: 50px;
      opacity: .3;
    }</style></body></html>