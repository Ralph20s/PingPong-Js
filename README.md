# PingPong-Js
//boletahchanges
let xBoleta = 300;
let yBoleta = 200;
let diametro = 15;
let raio = diametro/2;

//velocityboleta
let velocidadeXBoleta = 6;
let velocidadeYBoleta = 6;

//variáveis da raquete
let xRaquete = 5;
let yRaquete = 150;
let raquetecomprimento = 10;
let raquetealtura = 90;

//variáveis da raquete oponente
let xRaqueteoponente = 582;
let yRaqueteoponente = 150;
let raquetecomprimentooponente = 10;
let raquetealturaoponente = 90;
let velocidadeYOponente;

//placar do jogo
let meusPontos = 0;
let pontosOponente = 0;

//sons do jogo
let raquetada;
let ponto;
let trilha;

let colidiu = false

function preload(){
  trilha = loadSound("trilha.mp3");
  ponto = loadSound("ponto.mp3");
  raquetada = loadSound("raquetada.mp3");
}

function setup() {
createCanvas(600, 400);
  trilha.loop();
}

function draw() {
  background(0);
  mostraBoleta();
  movimentaBoleta();
  verifybordcolision();
  MostrarRaquete(xRaquete, yRaquete);
  MovimentMinhaRaquete();
 //verificaColisaoRaquete();
  VerificaColisaoRaquete(xRaquete, yRaquete);
  MostrarRaquete(xRaqueteoponente, yRaqueteoponente);
  movimentaoponente();
  VerificaColisaoRaquete(xRaqueteoponente, yRaqueteoponente);
  incluiPlacar();
  marcaPonto();
}

function mostraBoleta(){
circle (xBoleta, yBoleta, diametro)
}

function movimentaBoleta(){
xBoleta += velocidadeXBoleta
yBoleta += velocidadeYBoleta
}

function verifybordcolision(){
if (xBoleta + raio > width ||
xBoleta - raio < 0){
velocidadeXBoleta *= -1
}

if (yBoleta + raio > height ||
yBoleta - raio < 0){
velocidadeYBoleta *= -1
}
}

function MostrarRaquete(x, y){
  rect(x, y, raquetecomprimento, raquetealtura)
}

function MovimentMinhaRaquete(){
  if (keyIsDown(UP_ARROW)){
      yRaquete -= 10;
      }
  if (keyIsDown(DOWN_ARROW)){
      yRaquete += 10;
      }
}

function verificaColisaoRaquete (){
  if (xBoleta - raio < xRaquete + raquetecomprimento
&& yBoleta - raio < yRaquete + raquetealtura && 
yBoleta + raio > yRaquete){
    velocidadeXBoleta *= -1;
    raquetada.play();
  }
}

function VerificaColisaoRaquete(x, y){
   colidiu =
  collideRectCircle(x, y, raquetecomprimento, raquetealtura, xBoleta, yBoleta, raio);
  if (colidiu){
    velocidadeXBoleta *= -1;
    raquetada.play();
  } 
}

function movimentaoponente(){
  if (keyIsDown(87)){
      yRaqueteoponente -= 10;
      }
  if (keyIsDown(83)){
      yRaqueteoponente += 10;
      }
}

function incluiPlacar(){
  stroke(255);
  textAlign(CENTER);
  textSize(16);
  fill(color(255,215,0));
  rect(180, 10, 40, 20);
  fill(255);
  text(meusPontos, 200, 26);
  fill(color(255,215,0));
  rect(380, 10, 40, 20);
  fill(255);
  text(pontosOponente, 400, 26);
}

function marcaPonto(){
  if (xBoleta > 590){
    meusPontos += 1; 
    ponto.play();
  }
  if (xBoleta < 10){
    pontosOponente += 1;
    ponto.play();
  }
}

function bolinhaNaoFicaPresa(){
    if (xBoleta - raio < 0){
    xBoleta = 23
    }
}
