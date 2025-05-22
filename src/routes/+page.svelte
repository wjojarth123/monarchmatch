<script>
  import { onMount } from 'svelte';

  // Quiz data structure
  const quizData = [
    {
      question: "How do you prefer to expand your influence?",
      choices: [
        {
          text: "Through military conquest and strategic warfare",
          rulers: [
            { name: "Genghis Khan", points: 10 },
            { name: "Alexander the Great", points: 8 },
            { name: "Julius Caesar", points: 5 }
          ]
        },
        {
          text: "Through diplomacy and political alliances",
          rulers: [
            { name: "Cleopatra", points: 10 },
            { name: "Augustus", points: 7 },
            { name: "Catherine the Great", points: 6 }
          ]
        },
        {
          text: "Through cultural and artistic achievements",
          rulers: [
            { name: "Emperor Ashoka", points: 9 },
            { name: "Queen Elizabeth I", points: 8 },
            { name: "Louis XIV", points: 10 }
          ]
        }
      ]
    },
    {
      question: "How do you handle opposition?",
      choices: [
        {
          text: "Crush them swiftly and completely",
          rulers: [
            { name: "Genghis Khan", points: 10 },
            { name: "Attila the Hun", points: 9 },
            { name: "Ramses II", points: 7 }
          ]
        },
        {
          text: "Convert them to your cause",
          rulers: [
            { name: "Constantine", points: 8 },
            { name: "Emperor Ashoka", points: 10 },
            { name: "Cyrus the Great", points: 6 }
          ]
        },
        {
          text: "Negotiate and find common ground",
          rulers: [
            { name: "Solomon", points: 9 },
            { name: "Queen Elizabeth I", points: 7 },
            { name: "Augustus", points: 8 }
          ]
        }
      ]
    },
    {
      question: "What legacy would you want to leave behind?",
      choices: [
        {
          text: "A vast empire that spans continents",
          rulers: [
            { name: "Alexander the Great", points: 10 },
            { name: "Genghis Khan", points: 9 },
            { name: "Charlemagne", points: 7 }
          ]
        },
        {
          text: "Cultural and architectural wonders",
          rulers: [
            { name: "Emperor Ashoka", points: 8 },
            { name: "Ramses II", points: 10 },
            { name: "Louis XIV", points: 9 }
          ]
        },
        {
          text: "Legal and political systems that last for centuries",
          rulers: [
            { name: "Justinian I", points: 10 },
            { name: "Augustus", points: 9 },
            { name: "Hammurabi", points: 8 }
          ]
        }
      ]
    },
    {
      question: "How do you view religion's role in governance?",
      choices: [
        {
          text: "Religion should be the foundation of the state",
          rulers: [
            { name: "Constantine", points: 9 },
            { name: "Akbar", points: 7 },
            { name: "Saladin", points: 10 }
          ]
        },
        {
          text: "Religion is a useful tool for controlling the population",
          rulers: [
            { name: "Augustus", points: 8 },
            { name: "Catherine the Great", points: 7 },
            { name: "Qin Shi Huang", points: 9 }
          ]
        },
        {
          text: "The state should be secular or tolerant of different religions",
          rulers: [
            { name: "Cyrus the Great", points: 10 },
            { name: "Akbar", points: 9 },
            { name: "Marcus Aurelius", points: 8 }
          ]
        }
      ]
    },
    {
      question: "How would you handle economic policy?",
      choices: [
        {
          text: "Heavy taxation to fund military campaigns and grand projects",
          rulers: [
            { name: "Louis XIV", points: 10 },
            { name: "Qin Shi Huang", points: 8 },
            { name: "Ramses II", points: 7 }
          ]
        },
        {
          text: "Encourage trade and commerce to increase prosperity",
          rulers: [
            { name: "Queen Elizabeth I", points: 9 },
            { name: "Cleopatra", points: 8 },
            { name: "Solomon", points: 10 }
          ]
        },
        {
          text: "Focus on agricultural development and land reforms",
          rulers: [
            { name: "Emperor Ashoka", points: 8 },
            { name: "Charlemagne", points: 7 },
            { name: "Cyrus the Great", points: 9 }
          ]
        }
      ]
    },
    {
      question: "What is your approach to education and knowledge?",
      choices: [
        {
          text: "Focus on practical skills and military training",
          rulers: [
            { name: "Genghis Khan", points: 8 },
            { name: "Sparta's Lycurgus", points: 10 },
            { name: "Julius Caesar", points: 6 }
          ]
        },
        {
          text: "Patronize arts, science, and philosophy",
          rulers: [
            { name: "Augustus", points: 8 },
            { name: "Akbar", points: 9 },
            { name: "Marcus Aurelius", points: 10 }
          ]
        },
        {
          text: "Standardize education to promote unity and loyalty",
          rulers: [
            { name: "Qin Shi Huang", points: 10 },
            { name: "Charlemagne", points: 8 },
            { name: "Catherine the Great", points: 7 }
          ]
        }
      ]
    },
    {
      question: "How do you respond to natural disasters or plagues?",
      choices: [
        {
          text: "See them as divine judgment and offer sacrifices",
          rulers: [
            { name: "Ramses II", points: 9 },
            { name: "Constantine", points: 8 },
            { name: "Montezuma", points: 10 }
          ]
        },
        {
          text: "Organize relief efforts and public works",
          rulers: [
            { name: "Emperor Ashoka", points: 10 },
            { name: "Augustus", points: 8 },
            { name: "Cyrus the Great", points: 9 }
          ]
        },
        {
          text: "Use them as an opportunity to eliminate opponents",
          rulers: [
            { name: "Qin Shi Huang", points: 9 },
            { name: "Catherine the Great", points: 7 },
            { name: "Attila the Hun", points: 8 }
          ]
        }
      ]
    },
    {
      question: "What is your approach to justice and law?",
      choices: [
        {
          text: "Harsh punishments to maintain order",
          rulers: [
            { name: "Qin Shi Huang", points: 10 },
            { name: "Genghis Khan", points: 8 },
            { name: "Hammurabi", points: 9 }
          ]
        },
        {
          text: "Fair and consistent application of laws",
          rulers: [
            { name: "Justinian I", points: 10 },
            { name: "Marcus Aurelius", points: 9 },
            { name: "Solomon", points: 8 }
          ]
        },
        {
          text: "Merciful and focused on rehabilitation",
          rulers: [
            { name: "Emperor Ashoka", points: 10 },
            { name: "Cyrus the Great", points: 9 },
            { name: "Akbar", points: 8 }
          ]
        }
      ]
    },
    {
      question: "How do you view your subjects?",
      choices: [
        {
          text: "They exist to serve the ruler and the state",
          rulers: [
            { name: "Louis XIV", points: 10 },
            { name: "Qin Shi Huang", points: 9 },
            { name: "Ramses II", points: 8 }
          ]
        },
        {
          text: "They are to be protected and cared for",
          rulers: [
            { name: "Emperor Ashoka", points: 10 },
            { name: "Cyrus the Great", points: 9 },
            { name: "Marcus Aurelius", points: 8 }
          ]
        },
        {
          text: "They are valuable resources to be utilized effectively",
          rulers: [
            { name: "Catherine the Great", points: 9 },
            { name: "Augustus", points: 8 },
            { name: "Genghis Khan", points: 7 }
          ]
        }
      ]
    },
    {
      question: "What is your preferred architectural style?",
      choices: [
        {
          text: "Massive monuments to display power",
          rulers: [
            { name: "Ramses II", points: 10 },
            { name: "Qin Shi Huang", points: 9 },
            { name: "Louis XIV", points: 8 }
          ]
        },
        {
          text: "Practical and defensive structures",
          rulers: [
            { name: "Genghis Khan", points: 7 },
            { name: "Charlemagne", points: 8 },
            { name: "Justinian I", points: 9 }
          ]
        },
        {
          text: "Beautiful and culturally significant buildings",
          rulers: [
            { name: "Emperor Ashoka", points: 9 },
            { name: "Augustus", points: 8 },
            { name: "Akbar", points: 10 }
          ]
        }
      ]
    }
  ];

  // Track user answers and scores
  let userAnswers = Array(quizData.length).fill(-1);
  let rulerScores = {};
  let rulerMaxScores = {};
  let selectedAnswers = [];
  let showResults = false;
  let resultData = {
    topRuler: "",
    topPercentage: 0,
    runnerUp: "",
    runnerUpPercentage: 0,
    topAnswers: []
  };

  // Calculate the maximum possible score for each ruler
  onMount(() => {
    // Initialize ruler scores
    quizData.forEach(question => {
      question.choices.forEach(choice => {
        choice.rulers.forEach(ruler => {
          if (!rulerScores[ruler.name]) {
            rulerScores[ruler.name] = 0;
          }
          if (!rulerMaxScores[ruler.name]) {
            rulerMaxScores[ruler.name] = 0;
          }
          // Add to maximum possible score
          rulerMaxScores[ruler.name] += ruler.points;
        });
      });
    });
  });

  // Handle answer selection
  function selectAnswer(questionIndex, choiceIndex) {
    userAnswers[questionIndex] = choiceIndex;
  }

  // Calculate results
  function calculateResults() {
    // Reset scores
    Object.keys(rulerScores).forEach(ruler => {
      rulerScores[ruler] = 0;
    });
    
    selectedAnswers = [];

    // Reset chart animation for new display
    if (showResults) {
      showResults = false;
      setTimeout(() => calculateAndShowResults(), 50);
      return;
    }
    
    calculateAndShowResults();
  }
  
  function calculateAndShowResults() {
    // Calculate scores based on user answers
    quizData.forEach((question, qIndex) => {
      const choiceIndex = userAnswers[qIndex];
      if (choiceIndex >= 0) {
        const choice = question.choices[choiceIndex];
        choice.rulers.forEach(ruler => {
          rulerScores[ruler.name] += ruler.points;
          
          // Store this answer for potential "top answers" display
          selectedAnswers.push({
            question: question.question,
            answer: choice.text,
            ruler: ruler.name,
            points: ruler.points
          });
        });
      }
    });

    // Find the top ruler and runner-up
    let topRulers = Object.keys(rulerScores)
      .map(name => ({
        name,
        score: rulerScores[name],
        maxScore: rulerMaxScores[name],
        percentage: (rulerScores[name] / rulerMaxScores[name]) * 100
      }))
      .sort((a, b) => b.percentage - a.percentage);

    // Get top answers that contributed to the winning ruler's score
    let topAnswers = selectedAnswers
      .filter(answer => answer.ruler === topRulers[0].name)
      .sort((a, b) => b.points - a.points)
      .slice(0, 5);

    resultData = {
      topRuler: topRulers[0].name,
      topPercentage: Math.round(topRulers[0].percentage),
      runnerUp: topRulers[1].name,
      runnerUpPercentage: Math.round(topRulers[1].percentage),
      topAnswers
    };

    showResults = true;
  }

  // Check if all questions are answered
  $: allAnswered = userAnswers.every(answer => answer >= 0);

  // Close the results modal
  function closeResults() {
    showResults = false;
  }
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Libre+Baskerville:ital,wght@0,400;0,700;1,400&display=swap');
  @import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@400;500;700&display=swap');
  
  :global(body) {
    background-color: #f5e9d0;
    background-image: url("https://www.transparenttextures.com/patterns/old-map.png");
    margin: 0;
    padding: 0;
  }
  
  .container {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
    font-family: 'Libre Baskerville', 'Palatino Linotype', serif;
    color: #4e3629;
  }
  
  h1 {
    text-align: center;
    color: #5c3a21;
    margin-bottom: 30px;
    font-size: 2.8rem;
    font-weight: bold;
    text-shadow: 1px 1px 3px rgba(107, 83, 28, 0.3);
    position: relative;
    padding-bottom: 15px;
    font-family: 'Cinzel', serif;
    letter-spacing: 1px;
  }
  
  h1::after {
    content: "";
    position: absolute;
    bottom: 0;
    left: 50%;
    transform: translateX(-50%);
    width: 150px;
    height: 3px;
    background: linear-gradient(90deg, transparent, #8c6b3b, transparent);
  }
  
  .quote {
    text-align: center;
    font-style: italic;
    color: #73583a;
    margin-bottom: 30px;
    font-size: 1.1rem;
    position: relative;
    padding: 0 40px;
  }
  
  .quote::before {
    content: "\201C";
    font-size: 2rem;
    color: #c0a080;
    position: absolute;
    left: 0;
    top: 10px;
    font-family: Georgia, serif;
    line-height: 0.1;
  }
  
  .quote::after {
    content: "\201D";
    font-size: 2rem;
    color: #c0a080;
    position: absolute;
    right: 0;
    bottom: 0;
    font-family: Georgia, serif;
    line-height: 0.1;
  }
  
  .question {
    margin-bottom: 30px;
    padding: 25px;
    border-radius: 8px;
    background-color: #f7f0e2;
    box-shadow: 0 4px 8px rgba(78, 54, 41, 0.15);
    border: 1px solid #d2b48c;
    position: relative;
    overflow: hidden;
  }
  
  .question::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 5px;
    background: linear-gradient(90deg, #8c6b3b, #d2b48c, #8c6b3b);
  }
  
  .question h3 {
    margin-top: 0;
    color: #5c3a21;
    font-size: 1.3rem;
    border-bottom: 1px dotted #c0a080;
    padding-bottom: 10px;
  }
  
  .choices {
    display: flex;
    flex-direction: column;
    gap: 12px;
    margin-top: 15px;
  }
  
  .choice {
    padding: 15px;
    border-radius: 5px;
    background-color: #fffaf0;
    cursor: pointer;
    transition: all 0.3s ease;
    border: 1px solid #d2b48c;
    position: relative;
    font-weight: 500;
    box-shadow: 0 2px 4px rgba(78, 54, 41, 0.1);
    font-family: 'Libre Baskerville', 'Palatino Linotype', serif;
    color: #4e3629;
    text-align: left;
    width: 100%;
    font-size: 1rem;
    display: block;
  }
  
  .choice::before {
    content: "✦";
    margin-right: 10px;
    color: #8c6b3b;
    font-size: 0.9rem;
  }
  
  .choice:hover {
    background-color: #f3e6cf;
    transform: translateY(-2px);
    box-shadow: 0 4px 8px rgba(78, 54, 41, 0.2);
  }
  
  .choice.selected {
    background-color: #e6d2ae;
    border-color: #8c6b3b;
    box-shadow: inset 0 2px 4px rgba(78, 54, 41, 0.2);
    transform: translateY(0);
  }
  
  .choice.selected::before {
    content: "✓";
    color: #5c3a21;
    font-weight: bold;
  }
  
  .submit-btn {
    display: block;
    width: 220px;
    margin: 30px auto;
    padding: 14px;
    background-color: #8c6b3b;
    color: #fffaf0;
    border: none;
    border-radius: 5px;
    font-size: 1rem;
    font-weight: bold;
    cursor: pointer;
    transition: all 0.3s ease;
    font-family: 'Libre Baskerville', 'Palatino Linotype', serif;
    position: relative;
    overflow: hidden;
    z-index: 1;
    box-shadow: 0 4px 8px rgba(78, 54, 41, 0.3);
  }
  
  .submit-btn::before {
    content: "";
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
    transition: 0.5s;
    z-index: -1;
  }
  
  .submit-btn:hover {
    background-color: #73583a;
  }
  
  .submit-btn:hover::before {
    left: 100%;
  }
  
  .submit-btn:disabled {
    background-color: #c0b19e;
    cursor: not-allowed;
    box-shadow: none;
  }
  
  .modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.6);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
    backdrop-filter: blur(3px);
  }
  
  .modal-content {
    background-color: #f7f0e2;
    background-image: url("https://www.transparenttextures.com/patterns/parchment.png");
    padding: 40px;
    border-radius: 10px;
    max-width: 700px;
    width: 90%;
    max-height: 90vh;
    overflow-y: auto;
    position: relative;
    box-shadow: 0 10px 30px rgba(78, 54, 41, 0.5);
    border: 2px solid #c0a080;
  }
  
  .close {
    position: absolute;
    top: 15px;
    right: 15px;
    font-size: 28px;
    cursor: pointer;
    color: #5c3a21;
    background: none;
    border: none;
    padding: 0;
    line-height: 1;
    transition: all 0.2s;
    width: 36px;
    height: 36px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    background-color: rgba(210, 180, 140, 0.3);
  }
  
  .close:hover {
    background-color: rgba(210, 180, 140, 0.6);
    transform: rotate(90deg);
  }
  
  .result-title {
    color: #5c3a21;
    margin-top: 10px;
    font-size: 1.8rem;
    text-align: center;
    position: relative;
    padding-bottom: 15px;
    margin-bottom: 25px;
    font-weight: bold;
  }
  
  .result-title::after {
    content: "";
    position: absolute;
    bottom: 0;
    left: 50%;
    transform: translateX(-50%);
    width: 100px;
    height: 3px;
    background: linear-gradient(90deg, transparent, #8c6b3b, transparent);
  }
  
  .percentage {
    font-weight: bold;
    color: #8c6b3b;
  }
  
  .answers-list {
    margin-top: 25px;
    padding-left: 0;
    list-style-type: none;
  }
  
  .answers-list li {
    margin-bottom: 15px;
    padding: 12px 15px;
    background-color: rgba(210, 180, 140, 0.15);
    border-radius: 5px;
    position: relative;
    padding-left: 30px;
    border-left: 3px solid #8c6b3b;
  }
  
  .answers-list li::before {
    content: "→";
    position: absolute;
    left: 10px;
    color: #8c6b3b;
  }
  
  .chart-container {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 15px 0;
  }
  
  .donut-chart {
    position: relative;
    width: 180px;
    height: 180px;
    margin: 0 auto;
    box-shadow: 0 4px 12px rgba(78, 54, 41, 0.15);
    border-radius: 50%;
    background: transparent;
  }
  
  .chart-center {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 100px;
    height: 100px;
    background-color: #f7f0e2;
    background-image: url("https://www.transparenttextures.com/patterns/parchment.png");
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    box-shadow: inset 0 2px 8px rgba(78, 54, 41, 0.1);
    border: 2px solid rgba(210, 180, 140, 0.3);
    z-index: 2;
  }
  
  .chart-percentage {
    font-size: 2rem;
    font-weight: bold;
    color: #5c3a21;
    line-height: 1;
    font-family: 'Cinzel', serif;
  }
  
  .chart-label {
    font-size: 0.7rem;
    color: #8c6b3b;
    letter-spacing: 1px;
    font-family: 'Cinzel', serif;
    margin-top: 3px;
  }
  
  .animate-in {
    animation: fadeScale 1.2s ease forwards;
    opacity: 0;
    transform: scale(0.8);
  }
  
  @keyframes fadeScale {
    0% {
      opacity: 0;
      transform: scale(0.8);
    }
    70% {
      opacity: 1;
      transform: scale(1.05);
    }
    100% {
      opacity: 1;
      transform: scale(1);
    }
  }
  
  .circle {
    fill: none;
    stroke-width: 12;
    stroke-dasharray: 0, 100;
    transform: rotate(-90deg);
    transform-origin: center;
    stroke-linecap: round;
    transition: all 0.8s ease;
  }
  
  .chart-background {
    stroke: rgba(210, 180, 140, 0.3);
    stroke-dasharray: 100, 0;
  }
  
  .chart-value {
    stroke: #8c6b3b;
    transition: stroke-dasharray 1.5s cubic-bezier(0.25, 0.8, 0.25, 1);
    stroke-linecap: round;
    filter: drop-shadow(0 2px 3px rgba(92, 58, 33, 0.3));
  }
  
  .result-section {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }
  
  .result-main {
    flex: 1 1 55%;
    padding-right: 20px;
  }
  
  .result-chart {
    flex: 1 1 40%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  
  .runner-up {
    margin-top: 20px;
    padding: 15px;
    border-top: 1px dotted #c0a080;
  }
  
  .scroll-decoration {
    height: 30px;
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 10'%3E%3Cpath d='M0,5 C20,0 30,10 50,5 C70,0 80,10 100,5' fill='none' stroke='%238c6b3b' stroke-width='1'/%3E%3C/svg%3E");
    background-repeat: repeat-x;
    opacity: 0.5;
    margin-bottom: 15px;
  }
  
  .header-decoration {
    height: 40px;
    background-image: url("data:image/svg+xml,%3Csvg width='100%25' height='100%25' xmlns='http://www.w3.org/2000/svg'%3E%3Cdefs%3E%3Cpattern id='smallGrid' width='10' height='10' patternUnits='userSpaceOnUse'%3E%3Cpath d='M 10 0 L 0 0 0 10' fill='none' stroke='%238c6b3b' stroke-width='0.5' opacity='0.3'/%3E%3C/pattern%3E%3C/defs%3E%3Crect width='100%25' height='100%25' fill='%23f5e9d0'/%3E%3Crect width='100%25' height='100%25' fill='url(%23smallGrid)'/%3E%3C/svg%3E");
    margin-bottom: 20px;
    position: relative;
  }
  
  .header-decoration::before, .header-decoration::after {
    content: "✦";
    position: absolute;
    bottom: -10px;
    color: #8c6b3b;
    font-size: 24px;
  }
  
  .header-decoration::before {
    left: 20%;
  }
  
  .header-decoration::after {
    right: 20%;
  }
  
  .compass {
    width: 60px;
    height: 60px;
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Ccircle cx='50' cy='50' r='45' fill='none' stroke='%238c6b3b' stroke-width='2'/%3E%3Ccircle cx='50' cy='50' r='3' fill='%238c6b3b'/%3E%3Cpath d='M50 5 L53 50 L50 95 L47 50 Z' fill='%235c3a21'/%3E%3Cpath d='M5 50 L50 47 L95 50 L50 53 Z' fill='%238c6b3b'/%3E%3Ctext x='50' y='15' text-anchor='middle' font-family='serif' font-size='10' fill='%235c3a21'%3EN%3C/text%3E%3Ctext x='85' y='52' text-anchor='middle' font-family='serif' font-size='10' fill='%235c3a21'%3EE%3C/text%3E%3Ctext x='50' y='90' text-anchor='middle' font-family='serif' font-size='10' fill='%235c3a21'%3ES%3C/text%3E%3Ctext x='15' y='52' text-anchor='middle' font-family='serif' font-size='10' fill='%235c3a21'%3EW%3C/text%3E%3C/svg%3E");
    background-size: contain;
    margin: 0 auto 30px;
    opacity: 0.8;
  }
  
  @media (max-width: 768px) {
    .result-section {
      flex-direction: column;
    }
    .result-main {
      padding-right: 0;
    }
    .header-decoration::before {
      left: 10%;
    }
    .header-decoration::after {
      right: 10%;
    }
  }
</style>

<div class="container">
  <div class="header-decoration"></div>
  <h1>What Ancient Ruler Are You?</h1>
  <div class="quote">
    "History is a tale told by the rulers of old. Which one tells your story?"
  </div>
  <div class="compass"></div>
  
  {#each quizData as question, qIndex}
    <div class="question">
      <h3>{qIndex + 1}. {question.question}</h3>
      <div class="choices">
        {#each question.choices as choice, cIndex}
          <button 
            class="choice {userAnswers[qIndex] === cIndex ? 'selected' : ''}" 
            on:click={() => selectAnswer(qIndex, cIndex)}
            type="button"
          >
            {choice.text}
          </button>
        {/each}
      </div>
    </div>
  {/each}
  
  <button 
    class="submit-btn" 
    disabled={!allAnswered} 
    on:click={calculateResults}
  >
    {allAnswered ? 'Show My Results' : `Answer All Questions (${userAnswers.filter(a => a >= 0).length}/${quizData.length})`}
  </button>
</div>

{#if showResults}
  <div class="modal" on:click={closeResults}>
    <div class="modal-content" on:click|stopPropagation>
      <button 
        class="close" 
        on:click={closeResults} 
        on:keydown={(e) => e.key === 'Enter' && closeResults()}
        aria-label="Close results"
      >&times;</button>
      <div class="scroll-decoration"></div>
      <h2 class="result-title">You Are Most Like: {resultData.topRuler}</h2>
      
      <div class="result-section">
        <div class="result-main">
          <p>The scrolls of history have revealed your true nature!</p>
          <h3>Top Answers That Made You {resultData.topRuler}:</h3>
          <ul class="answers-list">
            {#each resultData.topAnswers as answer}
              <li>
                <strong>"{answer.question}"</strong> - You chose: "{answer.answer}"
              </li>
            {/each}
          </ul>
        </div>
        
        <div class="result-chart">
          <div class="chart-container">
            <div class="donut-chart">
              <svg width="180" height="180" viewBox="0 0 100 100">
                <circle class="circle chart-background" cx="50" cy="50" r="40" />
                <circle class="circle chart-value" cx="50" cy="50" r="40" 
                  style="stroke-dasharray: {resultData.topPercentage >= 100 ? '100, 0' : `${resultData.topPercentage}, 100`}" />
              </svg>
              <div class="chart-center">
                <span class="chart-percentage animate-in">{resultData.topPercentage}%</span>
                <span class="chart-label animate-in">MATCH</span>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <div class="runner-up">
        <p>Your runner-up is <strong>{resultData.runnerUp}</strong> with a 
          <span class="percentage">{resultData.runnerUpPercentage}%</span> match. 
          In another time, you might have ruled differently!</p>
      </div>
    </div>
  </div>
{/if}
