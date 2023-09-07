var score = 0;
            var clickingPower = 1

            var cursorcost = 15;
            var cursors = 0;
            var robotcost = 75;
            var robots = 0;
            var dhcost = 150;
            var dh = 0;
            var clonecost = 225;
            var clone= 0;

            function buycursor () {
                if (score >= cursorcost) {
                     score =  score - cursorcost;
                     cursors = cursors + 1;
                     cursorcost = Math.round(cursorcost * 1.15);

                     document.getElementById("score").innerHTML = score;
                     document.getElementById("cursorcost").innerHTML = cursorcost;
                     document.getElementById("cursors").innerHTML = cursors;
                     updatescorepersecond();
                    }
            }
            function buyrobot () {
                if (score >= robotcost) {
                     score =  score - robotcost;
                     robots = robots + 1;
                     robotcost = Math.round(robotcost * 1.15);

                     document.getElementById("score").innerHTML = score;
                     document.getElementById("robotcost").innerHTML = robotcost;
                     document.getElementById("robots").innerHTML = robots;
                     updatescorepersecond();
                    }
            }
            function buydh () {
                if (score >= dhcost) {
                     score =  score - dhcost;
                     dh = dh + 1;
                     dhcost = Math.round(dhcost * 1.15);

                     document.getElementById("score").innerHTML = score;
                     document.getElementById("dhcost").innerHTML = dhcost;
                     document.getElementById("dh").innerHTML = dh;
                     updatescorepersecond();
                    }
            }
            function buyclone () {
                if (score >= clonecost) {
                     score =  score - clonecost;
                     clone = clone + 1;
                     clonecost = Math.round(clonecost * 1.15);

                     document.getElementById("score").innerHTML = score;
                     document.getElementById("clonecost").innerHTML = clonecost;
                     document.getElementById("clone").innerHTML = clone;
                     updatescorepersecond();
                    }
            }


            function addtoscore (amount) {
                score = score + amount;
                document.getElementById("score").innerHTML = score;
            }

            function updatescorepersecond() {
                scorepersecond =  cursors + robots * 5 + dh * 10 + clone * 15;
                document.getElementById("scorepersecond").innerHTML = scorepersecond;
            }

            function loadgame() {
                var savedgame = JSON.parse(localStorage.getItem("gamesave"));
                if (typeof savedgame.score !== "undefined") score = savedgame.score;
                if (typeof savedgame.clickingPower !== "undefined") clickingPower = savedgame.clickingPower;
                if (typeof savedgame.cursorcost !== "undefined") cursorcost = savedgame.cursorcost;
                if (typeof savedgame.cursors !== "undefined") cursors = savedgame.cursors;
                if (typeof savedgame.robotcost !== "undefined") robotcost = savedgame.robotcost;
                if (typeof savedgame.robots !== "undefined") robots = savedgame.robots;
                if (typeof savedgame.dhcost !== "undefined") dhcost = savedgame.dhcost;
                if (typeof savedgame.dh !== "undefined") dh = savedgame.dh;
                if (typeof savedgame.clonecost !== "undefined") clonecost = savedgame.clonecost;
                if (typeof savedgame.clone !== "undefined") clone = savedgame.clone;
            }
            
            function saveGame() {
                var gamesave = {
                    score: score,
                    clickingPower: clickingPower,
                    cursorcost: cursorcost,
                    cursors: cursors,
                    robotcost: robotcost,
                    robots: robots,
                    dhcost: dhcost,
                    dh: dh,
                    clonecost: clonecost,
                    clone: clone,
                };
                localStorage.setItem("gamesave", JSON.stringify(gamesave));
            }

            function resetgame () {
                 if (confirm("Are you sure you want to reset the game?")) {
                    var gamesave = {};
                    localStorage.setItem("gamesave", JSON.stringify(gamesave));
                    location.reload();
                 }
            }
             
           window.onload = function() {
                loadgame();
                updatescorepersecond();
                document.getElementById("score").innerHTML = score;
                    document.getElementById("cursorcost").innerHTML = cursorcost;
                     document.getElementById("cursors").innerHTML = cursors;  
           };       document.getElementById("robotcost").innerHTML = robotcost;
                     document.getElementById("robots").innerHTML = robots;
                     document.getElementById("dhcost").innerHTML = dhcost;
                     document.getElementById("dh").innerHTML = dh;
                     document.getElementById("clonecost").innerHTML = clonecost;
                     document.getElementById("clone").innerHTML = clone;
           
            setInterval(function()  {
                score = score + cursors;
                score = score + robots * 5
                score = score + dh * 10
                score = score + clone * 15
                document.getElementById ("score").innerHTML = score;
                
                document.title = score + " money - roy clicker vAlpha"

            }, 1000); // 1000ms = 1 second 

                setInterval(function() {
                    saveGame();

                }, 30000); //30000ms = 30 seconds
                
                document.addEventListener("keydown", function(event) {
                    if(event.ctrlKey && event.which == 83) { //ctrl + s
                        event.preventDefault();
                        saveGame();
                        alert("saved")
                    }
                }, false);
