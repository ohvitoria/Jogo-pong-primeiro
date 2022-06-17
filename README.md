# Jogo-pong-primeiro

//variaveis da bolinha
let xBolinha = 300;
let yBolinha = 200;
let diametro = 21;
let raio = diametro / 2 ;

//velocidade da bolinha
let velocidadeXBolinha = 8;
let velocidadeYBolinha = 8;

//variaveis da minha raquete
let xRaquete = 5 ;
let yRaquete = 150;
let raqueteComprimento =15;
let raqueteAltura = 96;

//variáveis do oponente
let xRaqueteOponente = 580;
let yRaqueteOponente = 150;
let velocidadeYOponente;

function setup() { 
 
  createCanvas (600,400);
}

let colidiu = false;

function draw() {
  background(0);
    mostraBolinha();
    movimentaBolinha();
    verificaColisaoBorda();
    mostraRaquete(xRaquete, yRaquete);
    movimentaMinhaRaquete();
    //verificaColisaoRaquete();
    verificaColisaoRaquete(xRaquete,yRaquete);
    mostraRaquete(xRaqueteOponente, yRaqueteOponente);
   movimentaRaqueteOponente();
   verificaColisaoRaquete(xRaqueteOponente, yRaqueteOponente);
  incluiPlacar();
  marcaPonto();
}

function mostraBolinha(){
  circle (xBolinha,yBolinha,diametro);
}

function movimentaBolinha(){
  xBolinha += velocidadeXBolinha;
  yBolinha += velocidadeYBolinha;
}

function verificaColisaoBorda(){
  if (xBolinha + raio > width || 
     xBolinha - raio < 0){
velocidadeXBolinha *= -1;
  }

if (yBolinha + raio > height || yBolinha - raio < 0){
  velocidadeYBolinha *= -1;
}
}

function mostraRaquete(x,y) {
    rect(x, y, raqueteComprimento, raqueteAltura);
}

function mostraRaquete(xRaqueteOponente,yRaqueteOponente) {
    rect(xRaqueteOponente, yRaqueteOponente, raqueteComprimento, raqueteAltura);
}

function movimentaMinhaRaquete (){
  if(keyIsDown(UP_ARROW)){
    yRaquete -= 10;
  }
if(keyIsDown(DOWN_ARROW)){
  yRaquete += 10;
}
}

function verificaColisaoRaquete(){
  if(xBolinha - raio < xRaquete + raqueteComprimento && yBolinha - raio < yRaquete && yBolinha + raio > yRaquete){
    velocidadeXBolinha *= -1;
  }
}

function colisaoMinhaRaqueteBiblioteca() {
    colidiu = collideRectCircle(xRaquete, yRaquete, raqueteComprimento, raqueteAltura, xBolinha, yBolinha, raio);
    if (colidiu) {
        velocidadeXBolinha *= -1;
    }
}

function movimentaRaqueteOponente() {
    velocidadeYOponente = yBolinha - yRaqueteOponente - raqueteComprimento / 2 - 30;
    yRaqueteOponente += velocidadeYOponente
}

function verificaColisaoRaquete(x, y){
  colidiu = collideRectCircle(x,y,raqueteComprimento,raqueteAltura,xBolinha,yBolinha,raio);
  if (colidiu){
    velocidadeXBolinha *= -1;
  }
}


function marcaPonto() {
    if (xBolinha > 590) {
        meusPontos += 1;
    }
    if (xBolinha < 10) {
        pontosDoOponente += 1;
    }

    velocidadeYOponente = yBolinha - yRaqueteOponente - raqueteComprimento / 2 - 30;
    yRaqueteOponente += velocidadeYOponente
  
}

//placarJogo
let meusPontos = 0;
let pontosDoOponente = 0;

function incluiPlacar(){
  stroke(255);
  textAlign(CENTER);
  textSize(20);
    fill(color(218,112,214));
  rect(150,10,40,20);
  fill(255);
    text(meusPontos, 170, 26);
  fill(color(218,112,214));
  rect(450,10,40,20);
  fill(255);
    text(pontosDoOponente, 470, 26);
}

function marcarPontos(){
  if(xBolinha > 590){
    meusPontos += 1;
  }
 if(xBolinha < 10){
  pontosDoOPonente += 1;
}
}









