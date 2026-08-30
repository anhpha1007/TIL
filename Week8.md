```html
<!-- 1. Trivia -->
             document.addEventListener('DOMContentLoaded', function() {
                let correctButton = document.querySelector('.correct');
                correctButton.addEventListener('click', function() {
                    correctButton.style.backgroundColor = 'Green';
                    document.querySelector('#feedback1').innerHTML = 'Correct!';
                });

                let incorrectButton = document.querySelectorAll('.incorrect');
                for (let i = 0; i < incorrectButton.length; i++) {
                    incorrectButton[i].addEventListener('click', function() {
                        incorrectButton[i].style.backgroundColor = 'Red';
                        document.querySelector('#feedback1').innerHTML = 'Incorrect!';
                    });
                }

                document.querySelector('#check').addEventListener('click', function(){
                    let input = document.querySelector('#answer');
                    if (input.value.trim().toLowerCase() === '1989') {
                        input.style.backgroundColor = 'Green';
                        document.querySelector('#feedback2').innerHTML = 'Correct!';
                    } else {
                        input.style.backgroundColor = 'Red';
                        document.querySelector('#feedback2').innerHTML = 'Incorrect';
                    }
                });
            });

<1-- 2. Homepage -->
<head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <title>My Homepage - About</title>
        <!-- Bootstrap CSS -->
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
        <!-- Custom CSS -->
        <link href="styles.css" rel="stylesheet">
</head>

<!-- Navigation Bar -->
        <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
            <div class="container-fluid">
                <a class="navbar-brand" href="index.html">Melanie's Site</a>
                <div class="navbar-nav">
                    <a class="nav-link" href="index.html">Home</a>
                    <a class="nav-link active" href="about.html">About</a>
                    <a class="nav-link" href="projects.html">Projects</a>
                    <a class="nav-link" href="contact.html">Contact</a>
                </div>
            </div>
        </nav>

<!-- Bootstrap JS Bundle -->
        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
