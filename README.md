<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<title>Test de Performances PC</title>
<style>
    body { background:#111; color:#fff; font-family:Arial; text-align:center; }
    button { padding: 10px 20px; margin: 10px; font-size:16px; }
    canvas { background:#000; margin-top:20px; }
</style>
</head>
<body>

<h1>Test de Performances du PC</h1>

<button onclick="startCPUTest()">Test CPU</button>
<button onclick="startDOMTest()">Test DOM (RAM)</button>
<button onclick="startGPUTest()">Test GPU</button>

<canvas id="gpuCanvas" width="600" height="400"></canvas>

<script>
// ---------- TEST CPU ----------
function startCPUTest() {
    alert("Le test CPU commence. Le navigateur peut devenir lent.");
    let x = 0;
    function loop() {
        for (let i = 0; i < 5e7; i++) { x += Math.sqrt(i); }
        requestAnimationFrame(loop);
    }
    loop();
}

// ---------- TEST DOM ----------
function startDOMTest() {
    alert("Le test DOM va ajouter énormément d'éléments, ça peut lag.");
    for (let i = 0; i < 50000; i++) {
        const div = document.createElement("div");
        div.textContent = "Élément " + i;
        div.style.color = i % 2 ? "#0f0" : "#f00";
        document.body.appendChild(div);
    }
}

// ---------- TEST GPU ----------
function startGPUTest() {
    alert("Le test GPU commence (Canvas).");
    const canvas = document.getElementById("gpuCanvas");
    const ctx = canvas.getContext("2d");
    let balls = [];

    // Création de 5000 particules
    for (let i = 0; i < 5000; i++) {
        balls.push({
            x: Math.random()*600,
            y: Math.random()*400,
            vx: (Math.random()*2)-1,
            vy: (Math.random()*2)-1
        });
    }

    function animate() {
        ctx.clearRect(0,0,600,400);
        ctx.fillStyle = "white";

        for (let b of balls) {
            b.x += b.vx;
            b.y += b.vy;
            if (b.x < 0 || b.x > 600) b.vx *= -1;
            if (b.y < 0 || b.y > 400) b.vy *= -1;
            ctx.fillRect(b.x, b.y, 2, 2);
        }

        requestAnimationFrame(animate);
    }
    animate();
}
</script>

</body>
</html>
