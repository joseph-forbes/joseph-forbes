 \<html>
\
\
    \<head>
\
        <title>Flappy Bird</title>
\
    \</head>
\
    \<body>    
        \<canvas id='game' width=500 height=500>        
        \<script>
          
            let canvas,ctx;
            window.onload = function() {
                canvas = document.getElementById('game');
                ctx = canvas.getContext('2d');
                world.push(new Pipe(0));
                document.addEventListener('keydown',function(e){
                    if(e.keyCode == 32 && !bird.jump) {
                        bird.vv = -15;
                        bird.jump = true;
                    }
                })
                
                setInterval(mainloop,1000/30)
            }
            var framerate = 0;
            var bird = {
                y: 250,
                vv: 0,
                jump: false,
                update: function() {
                    ctx.fillStyle = 'green';
                    ctx.fillRect(100,this.y,50,50);
                    this.vv++;
                    this.y += this.vv;
                    if(this.vv > 0) {
                        this.jump = false;
                    }
                    if(this.y < -50 || this.y > canvas.height) {
                        this.y = canvas.height / 2;
                        this.vv = 0;
                        framerate = 0;
                        world = [new Pipe(0)];
                    }

                }
            };
            var world = [];
            class Pipe {
                constructor(idx) {
                    this.idx = idx;
                    this.x = canvas.width;
                    this.y = Math.random() * (canvas.height-200);
                }
                
                
                update() {
                    this.x -= 10;
                    if(this.x < -25)
                        world.splice(this.idx,1);
                    ctx.fillStyle = 'gray';
                    ctx.fillRect(this.x,0,50,this.y);
                    ctx.fillRect(this.x,this.y + 200,50,canvas.height);
                    if(this.x < 150 && this.x + 50 > 100 && (bird.y < this.y || bird.y + 50 > this.y + 200)) {
                        bird.y = canvas.height / 2;
                        bird.vv = 0;
                        framerate = 0;
                        world = [new Pipe(0)];
                    }
                }
            } 
            function mainloop() {
                framerate++
                if(framerate % 90 == 0) {
                    world.push(new Pipe(world.length));
                    framerate = 0; 
                }
                ctx.clearRect(0,0,canvas.width,canvas.height);
                ctx.fillStyle = 'black';
                ctx.fillRect(0,0,canvas.width,canvas.height);
                ctx.fillStyle = 'green';
                bird.update();
                world.forEach(function(o) {
                    o.update()
                })
            }

\
        </script>
\
    \</body>
    
\</html>

<!---
joseph-forbes/joseph-forbes is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
