# quiz-app
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz App</title>
    <style>
        /* Add your CSS styles here */
    </style>
</head>
<body>
    <div id="quiz-container">
        <h1>Quiz App</h1>
        <p id="question">Question goes here</p>
        <div id="options">
            <!-- Options will be populated using JavaScript -->
        </div>
        <button id="next-button">Next</button>
        <p id="result"></p>
    </div>

    <script>
        // Quiz questions and answers
        const quizData = [
            {
                question: "What is the capital of France?",
                options: ["London", "Madrid", "Paris", "Berlin"],
                correctAnswer: "Paris"
            },
            {
                question: "What is 2 + 2?",
                options: ["3", "4", "5", "6"],
                correctAnswer: "4"
            },
            {
                question: "What is the largest planet in our solar system?",
                options: ["Earth", "Mars", "Jupiter", "Venus"],
                correctAnswer: "Jupiter"
            }
        ];

        let currentQuestionIndex = 0;
        let score = 0;

        const questionElement = document.getElementById("question");
        const optionsElement = document.getElementById("options");
        const nextButton = document.getElementById("next-button");
        const resultElement = document.getElementById("result");

        function loadQuestion() {
            const currentQuestion = quizData[currentQuestionIndex];
            questionElement.textContent = currentQuestion.question;

            optionsElement.innerHTML = '';
            for (let i = 0; i < currentQuestion.options.length; i++) {
                const option = document.createElement("button");
                option.textContent = currentQuestion.options[i];
                option.addEventListener("click", checkAnswer);
                optionsElement.appendChild(option);
            }
        }

        function checkAnswer(event) {
            const userAnswer = event.target.textContent;
            const currentQuestion = quizData[currentQuestionIndex];

            if (userAnswer === currentQuestion.correctAnswer) {
                score++;
            }

            currentQuestionIndex++;

            if (currentQuestionIndex < quizData.length) {
                loadQuestion();
            } else {
                showResult();
            }
        }

        function showResult() {
            resultElement.textContent = `Your score: ${score} out of ${quizData.length}`;
            optionsElement.innerHTML = '';
            nextButton.style.display = 'none';
        }

        nextButton.addEventListener("click", () => {
            if (currentQuestionIndex < quizData.length) {
                loadQuestion();
            } else {
                showResult();
            }
        });

        loadQuestion();
    </script>
</body>
</html>
