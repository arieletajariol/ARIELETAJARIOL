let questions = [
  {
    question: "Qual é um alimento típico do campo?",
    options: ["Pizza", "Feijão", "Hambúrguer", "Sushi"],
    answer: 1,
    image: "https://example.com/feijao.jpg"
  },
  {
    question: "Qual festa é famosa nas cidades?",
    options: ["Festa Junina", "Carnaval", "Colheita", "Feriado Rural"],
    answer: 1,
    image: "https://example.com/carnaval.jpg"
  },
  {
    question: "O que representa a conexão entre campo e cidade?",
    options: ["Tecnologia", "Natureza", "Cultura", "Tradição"],
    answer: 2,
    image: "https://example.com/natureza.jpg"
  },
  {
    question: "Qual é um instrumento musical comum no campo?",
    options: ["Guitarra", "Acordeão", "Piano", "Bateria"],
    answer: 1,
    image: "https://example.com/acordeao.jpg"
  },
  {
    question: "Qual destes animais é frequentemente associado ao campo?",
    options: ["Cachorro", "Gato", "Cavalo", "Peixe"],
    answer: 2,
    image: "https://example.com/cavalo.jpg"
  },
  {
    question: "Qual atividade é comum no campo?",
    options: ["Fabricação de móveis", "Agricultura", "Programação", "Design Gráfico"],
    answer: 1,
    image: "https://example.com/agricultura.jpg"
  },
  {
    question: "Qual fruta é típica de áreas rurais?",
    options: ["Maçã", "Banana", "Morango", "Cajá"],
    answer: 3,
    image: "https://example.com/caja.jpg"
  }
];

let currentQuestion = 0;
let score = 0;
let img;

function setup() {
  createCanvas(600, 400);
  displayQuestion();
}

function displayQuestion() {
  background(255, 228, 196);
  let q = questions[currentQuestion];

  // Carregar e exibir a imagem
  loadImage(q.image, (loadedImg) => {
    img = loadedImg;
  });

  // Exibir a imagem se já tiver sido carregada
  if (img) {
    image(img, 20, 100, 100, 100);
  }

  textSize(18);
  fill(34, 139, 34);
  textAlign(CENTER);
  text(q.question, width / 2, 50);

  for (let i = 0; i < q.options.length; i++) {
    fill(255, 165, 0);
    rect(150, 120 + i * 50, 300, 40, 10);
    fill(0);
    textSize(20);
    textAlign(CENTER);
    text(q.options[i], width / 2, 140 + i * 50);
  }
}

function mousePressed() {
  let q = questions[currentQuestion];
  for (let i = 0; i < q.options.length; i++) {
    if (mouseX > 150 && mouseX < 450 && mouseY > 120 + i * 50 && mouseY < 160 + i * 50) {
      checkAnswer(i);
    }
  }
}

function checkAnswer(selected) {
  if (selected === questions[currentQuestion].answer) {
    score++;
    fill(0, 255, 0);
    textSize(32);
    text("Correto!", width / 2, height - 50);
  } else {
    fill(255, 0, 0);
    textSize(32);
    text("Errado!", width / 2, height - 50);
  }
  currentQuestion++;

  setTimeout(() => {
    if (currentQuestion < questions.length) {
      displayQuestion();
    } else {
      displayScore();
    }
  }, 1000);
}

function displayScore() {
  background(255, 228, 196);
  textSize(32);
  fill(0);
  text(`Você acertou ${score} de ${questions.length}`, width / 2, height / 2 - 30);
  
  textSize(20);
  textAlign(LEFT);
  text("A conexão entre campo e cidade é importante porque:", 20, height / 2 + 30);
  text("1. A agricultura fornece alimentos para as cidades.", 20, height / 2 + 60);
  text("2. As cidades oferecem tecnologia e serviços ao campo.", 20, height / 2 + 90);
  text("3. A cultura rural enriquece a vida urbana.", 20, height / 2 + 120);
}
