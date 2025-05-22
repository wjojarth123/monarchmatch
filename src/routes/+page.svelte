<script>
  import { onMount } from 'svelte';

  // Quiz data structure based on CSV
  const quizData = [
    {
      question: "How would you expand your empire?",
      choices: [
        {
          text: "Violently raid them",
          rulers: [
            { name: "Genghis Khan", points: 6 },
            { name: "Napoleon", points: 3 },
            { name: "Mao Zedong", points: 0 },
            { name: "Joseph Stalin", points: 2 },
            { name: "Mansa Musa", points: 2 },
            { name: "Donald Trump", points: 2 }
          ]
        },
        {
          text: "Purchase them from another state",
          rulers: [
            { name: "Genghis Khan", points: 0 },
            { name: "Napoleon", points: 4 },
            { name: "Mao Zedong", points: 0 },
            { name: "Joseph Stalin", points: 0 },
            { name: "Mansa Musa", points: 4 },
            { name: "Donald Trump", points: 6 }
          ]
        },
        {
          text: "Methodically capture and control territory",
          rulers: [
            { name: "Genghis Khan", points: 0 },
            { name: "Napoleon", points: 6 },
            { name: "Mao Zedong", points: 1 },
            { name: "Joseph Stalin", points: 2 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 1 }
          ]
        },
        {
          text: "Install puppet rulers in your prey's government",
          rulers: [
            { name: "Genghis Khan", points: 0 },
            { name: "Napoleon", points: 6 },
            { name: "Mao Zedong", points: 1 },
            { name: "Joseph Stalin", points: 3 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 0 }
          ]
        }
      ]
    },
    {
      question: "How would you deal with protestors?",
      choices: [
        {
          text: "Give them more work, they can't protest if they are too tired/don't have time",
          rulers: [
            { name: "Genghis Khan", points: 0 },
            { name: "Napoleon", points: 2 },
            { name: "Mao Zedong", points: 6 },
            { name: "Joseph Stalin", points: 3 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 0 }
          ]
        },
        {
          text: "Police, drive them out",
          rulers: [
            { name: "Genghis Khan", points: 0 },
            { name: "Napoleon", points: 4 },
            { name: "Mao Zedong", points: 6 },
            { name: "Joseph Stalin", points: 3 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 2 }
          ]
        },
        {
          text: "Kill them, make an example",
          rulers: [
            { name: "Genghis Khan", points: 6 },
            { name: "Napoleon", points: 5 },
            { name: "Mao Zedong", points: 2 },
            { name: "Joseph Stalin", points: 6 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 1 }
          ]
        },
        {
          text: "Make propaganda about them",
          rulers: [
            { name: "Genghis Khan", points: 2 },
            { name: "Napoleon", points: 1 },
            { name: "Mao Zedong", points: 4 },
            { name: "Joseph Stalin", points: 5 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 6 }
          ]
        }
      ]
    },
    {
      question: "How tolerant would you be towards other religions?",
      choices: [
        {
          text: "There are other religions?",
          rulers: [
            { name: "Genghis Khan", points: 3 },
            { name: "Napoleon", points: 0 },
            { name: "Mao Zedong", points: 1 },
            { name: "Joseph Stalin", points: 0 },
            { name: "Mansa Musa", points: 1 },
            { name: "Donald Trump", points: 2 }
          ]
        },
        {
          text: "I do not care about religion and politics",
          rulers: [
            { name: "Genghis Khan", points: 4 },
            { name: "Napoleon", points: 3 },
            { name: "Mao Zedong", points: 4 },
            { name: "Joseph Stalin", points: 4 },
            { name: "Mansa Musa", points: 6 },
            { name: "Donald Trump", points: 1 }
          ]
        },
        {
          text: "I'm tolerant towards other religions",
          rulers: [
            { name: "Genghis Khan", points: 6 },
            { name: "Napoleon", points: 2 },
            { name: "Mao Zedong", points: 4 },
            { name: "Joseph Stalin", points: 4 },
            { name: "Mansa Musa", points: 6 },
            { name: "Donald Trump", points: 4 }
          ]
        },
        {
          text: "I hate them; Kick them out",
          rulers: [
            { name: "Genghis Khan", points: 0 },
            { name: "Napoleon", points: 1 },
            { name: "Mao Zedong", points: 6 },
            { name: "Joseph Stalin", points: 6 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 6 }
          ]
        }
      ]
    },
    {
      question: "How free would your empire be?",
      choices: [
        {
          text: "All people have many rights with property and in the court",
          rulers: [
            { name: "Genghis Khan", points: 1 },
            { name: "Napoleon", points: 3 },
            { name: "Mao Zedong", points: 0 },
            { name: "Joseph Stalin", points: 0 },
            { name: "Mansa Musa", points: 4 },
            { name: "Donald Trump", points: 2 }
          ]
        },
        {
          text: "I am a strict, tyrannical ruler with many restrictions on the people",
          rulers: [
            { name: "Genghis Khan", points: 2 },
            { name: "Napoleon", points: 2 },
            { name: "Mao Zedong", points: 4 },
            { name: "Joseph Stalin", points: 5 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 2 }
          ]
        },
        {
          text: "Democracy for land-owning elites only",
          rulers: [
            { name: "Genghis Khan", points: 0 },
            { name: "Napoleon", points: 6 },
            { name: "Mao Zedong", points: 0 },
            { name: "Joseph Stalin", points: 0 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 4 }
          ]
        },
        {
          text: "Taxes in exchange for religious tolerance",
          rulers: [
            { name: "Genghis Khan", points: 2 },
            { name: "Napoleon", points: 0 },
            { name: "Mao Zedong", points: 2 },
            { name: "Joseph Stalin", points: 2 },
            { name: "Mansa Musa", points: 6 },
            { name: "Donald Trump", points: 2 }
          ]
        }
      ]
    },
    {
      question: "How generous would you be with your money?",
      choices: [
        {
          text: "Hoard it all",
          rulers: [
            { name: "Genghis Khan", points: 3 },
            { name: "Napoleon", points: 4 },
            { name: "Mao Zedong", points: 2 },
            { name: "Joseph Stalin", points: 3 },
            { name: "Mansa Musa", points: 2 },
            { name: "Donald Trump", points: 6 }
          ]
        },
        {
          text: "Money for everyone!",
          rulers: [
            { name: "Genghis Khan", points: 0 },
            { name: "Napoleon", points: 2 },
            { name: "Mao Zedong", points: 6 },
            { name: "Joseph Stalin", points: 6 },
            { name: "Mansa Musa", points: 6 },
            { name: "Donald Trump", points: 0 }
          ]
        },
        {
          text: "They need to make their own money",
          rulers: [
            { name: "Genghis Khan", points: 2 },
            { name: "Napoleon", points: 6 },
            { name: "Mao Zedong", points: 1 },
            { name: "Joseph Stalin", points: 1 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 5 }
          ]
        },
        {
          text: "The money should go towards industry and the economy",
          rulers: [
            { name: "Genghis Khan", points: 0 },
            { name: "Napoleon", points: 3 },
            { name: "Mao Zedong", points: 6 },
            { name: "Joseph Stalin", points: 6 },
            { name: "Mansa Musa", points: 2 },
            { name: "Donald Trump", points: 3 }
          ]
        }
      ]
    },
    {
      question: "How would you consolidate power?",
      choices: [
        {
          text: "Inherit the monarchy",
          rulers: [
            { name: "Genghis Khan", points: 0 },
            { name: "Napoleon", points: 0 },
            { name: "Mao Zedong", points: 0 },
            { name: "Joseph Stalin", points: 0 },
            { name: "Mansa Musa", points: 6 },
            { name: "Donald Trump", points: 0 }
          ]
        },
        {
          text: "Get the vote of the people, and of the businesses",
          rulers: [
            { name: "Genghis Khan", points: 0 },
            { name: "Napoleon", points: 0 },
            { name: "Mao Zedong", points: 0 },
            { name: "Joseph Stalin", points: 0 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 6 }
          ]
        },
        {
          text: "Take over during revolution",
          rulers: [
            { name: "Genghis Khan", points: 0 },
            { name: "Napoleon", points: 6 },
            { name: "Mao Zedong", points: 6 },
            { name: "Joseph Stalin", points: 6 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 0 }
          ]
        },
        {
          text: "Kill everyone",
          rulers: [
            { name: "Genghis Khan", points: 6 },
            { name: "Napoleon", points: 0 },
            { name: "Mao Zedong", points: 0 },
            { name: "Joseph Stalin", points: 0 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 0 }
          ]
        }
      ]
    },
    {
      question: "How much would you benefit the business owners?",
      choices: [
        {
          text: "Let them do what they want",
          rulers: [
            { name: "Genghis Khan", points: 4 },
            { name: "Napoleon", points: 6 },
            { name: "Mao Zedong", points: 0 },
            { name: "Joseph Stalin", points: 0 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 6 }
          ]
        },
        {
          text: "Create state-sponsored trade expeditions and organizations",
          rulers: [
            { name: "Genghis Khan", points: 0 },
            { name: "Napoleon", points: 6 },
            { name: "Mao Zedong", points: 3 },
            { name: "Joseph Stalin", points: 3 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 0 }
          ]
        },
        {
          text: "Prohibit business owners, all money goes to the state",
          rulers: [
            { name: "Genghis Khan", points: 1 },
            { name: "Napoleon", points: 2 },
            { name: "Mao Zedong", points: 6 },
            { name: "Joseph Stalin", points: 6 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 0 }
          ]
        },
        {
          text: "Execute the richest occasionally to confiscate wealth",
          rulers: [
            { name: "Genghis Khan", points: 0 },
            { name: "Napoleon", points: 5 },
            { name: "Mao Zedong", points: 4 },
            { name: "Joseph Stalin", points: 3 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 0 }
          ]
        }
      ]
    },
    {
      question: "Are you fighting for an oppressed group?",
      choices: [
        {
          text: "Yes, I want my people to have more rights and be free",
          rulers: [
            { name: "Genghis Khan", points: 0 },
            { name: "Napoleon", points: 1 },
            { name: "Mao Zedong", points: 2 },
            { name: "Joseph Stalin", points: 0 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 0 }
          ]
        },
        {
          text: "Yes but only so when I gain ruling power, I can control them for my own gain",
          rulers: [
            { name: "Genghis Khan", points: 0 },
            { name: "Napoleon", points: 3 },
            { name: "Mao Zedong", points: 5 },
            { name: "Joseph Stalin", points: 0 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 0 }
          ]
        },
        {
          text: "No, I am not fighting for any group",
          rulers: [
            { name: "Genghis Khan", points: 6 },
            { name: "Napoleon", points: 0 },
            { name: "Mao Zedong", points: 0 },
            { name: "Joseph Stalin", points: 0 },
            { name: "Mansa Musa", points: 4 },
            { name: "Donald Trump", points: 2 }
          ]
        },
        {
          text: "I oppress other groups/classes",
          rulers: [
            { name: "Genghis Khan", points: 6 },
            { name: "Napoleon", points: 0 },
            { name: "Mao Zedong", points: 0 },
            { name: "Joseph Stalin", points: 0 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 6 }
          ]
        }
      ]
    },
    {
      question: "How would you like to leave your legacy?",
      choices: [
        {
          text: "A vast empire spanning continents",
          rulers: [
            { name: "Genghis Khan", points: 6 },
            { name: "Napoleon", points: 5 },
            { name: "Mao Zedong", points: 5 },
            { name: "Joseph Stalin", points: 5 },
            { name: "Mansa Musa", points: 5 },
            { name: "Donald Trump", points: 5 }
          ]
        },
        {
          text: "A strong centralized government with unilateral power",
          rulers: [
            { name: "Genghis Khan", points: 2 },
            { name: "Napoleon", points: 4 },
            { name: "Mao Zedong", points: 6 },
            { name: "Joseph Stalin", points: 6 },
            { name: "Mansa Musa", points: 1 },
            { name: "Donald Trump", points: 0 }
          ]
        },
        {
          text: "A wealthy economy",
          rulers: [
            { name: "Genghis Khan", points: 1 },
            { name: "Napoleon", points: 5 },
            { name: "Mao Zedong", points: 5 },
            { name: "Joseph Stalin", points: 5 },
            { name: "Mansa Musa", points: 4 },
            { name: "Donald Trump", points: 6 }
          ]
        },
        {
          text: "A huge palace that makes everyone jealous",
          rulers: [
            { name: "Genghis Khan", points: 0 },
            { name: "Napoleon", points: 5 },
            { name: "Mao Zedong", points: 0 },
            { name: "Joseph Stalin", points: 1 },
            { name: "Mansa Musa", points: 6 },
            { name: "Donald Trump", points: 0 }
          ]
        }
      ]
    },
    {
      question: "What's your policy on crime and punishment?",
      choices: [
        {
          text: "Harsh penalties—deterrence is key",
          rulers: [
            { name: "Genghis Khan", points: 4 },
            { name: "Napoleon", points: 3 },
            { name: "Mao Zedong", points: 6 },
            { name: "Joseph Stalin", points: 6 },
            { name: "Mansa Musa", points: 1 },
            { name: "Donald Trump", points: 2 }
          ]
        },
        {
          text: "Fines for the rich, executions for the poor",
          rulers: [
            { name: "Genghis Khan", points: 3 },
            { name: "Napoleon", points: 6 },
            { name: "Mao Zedong", points: 1 },
            { name: "Joseph Stalin", points: 2 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 5 }
          ]
        },
        {
          text: "Public trials, but the verdict is always guilty",
          rulers: [
            { name: "Genghis Khan", points: 2 },
            { name: "Napoleon", points: 4 },
            { name: "Mao Zedong", points: 2 },
            { name: "Joseph Stalin", points: 2 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 3 }
          ]
        },
        {
          text: "Forgive and Forget",
          rulers: [
            { name: "Genghis Khan", points: 5 },
            { name: "Napoleon", points: 2 },
            { name: "Mao Zedong", points: 0 },
            { name: "Joseph Stalin", points: 0 },
            { name: "Mansa Musa", points: 4 },
            { name: "Donald Trump", points: 1 }
          ]
        }
      ]
    },
    {
      question: "What is the role of religion in state?",
      choices: [
        {
          text: "Religion has no place in government",
          rulers: [
            { name: "Genghis Khan", points: 1 },
            { name: "Napoleon", points: 4 },
            { name: "Mao Zedong", points: 6 },
            { name: "Joseph Stalin", points: 6 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 2 }
          ]
        },
        {
          text: "The government should follow some religious guidelines, but not be dependent",
          rulers: [
            { name: "Genghis Khan", points: 6 },
            { name: "Napoleon", points: 2 },
            { name: "Mao Zedong", points: 2 },
            { name: "Joseph Stalin", points: 0 },
            { name: "Mansa Musa", points: 6 },
            { name: "Donald Trump", points: 3 }
          ]
        },
        {
          text: "Religious scholars are useful to have in government",
          rulers: [
            { name: "Genghis Khan", points: 2 },
            { name: "Napoleon", points: 1 },
            { name: "Mao Zedong", points: 3 },
            { name: "Joseph Stalin", points: 0 },
            { name: "Mansa Musa", points: 6 },
            { name: "Donald Trump", points: 0 }
          ]
        }
      ]
    },
    {
      question: "How much rights do your women have?",
      choices: [
        {
          text: "Little to no rights for themselves",
          rulers: [
            { name: "Genghis Khan", points: 1 },
            { name: "Napoleon", points: 6 },
            { name: "Mao Zedong", points: 2 },
            { name: "Joseph Stalin", points: 3 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 4 }
          ]
        },
        {
          text: "They have the same or almost the same amount of rights as men",
          rulers: [
            { name: "Genghis Khan", points: 5 },
            { name: "Napoleon", points: 0 },
            { name: "Mao Zedong", points: 0 },
            { name: "Joseph Stalin", points: 6 },
            { name: "Mansa Musa", points: 5 },
            { name: "Donald Trump", points: 2 }
          ]
        },
        {
          text: "They have some rights, but not as much as the men",
          rulers: [
            { name: "Genghis Khan", points: 2 },
            { name: "Napoleon", points: 5 },
            { name: "Mao Zedong", points: 5 },
            { name: "Joseph Stalin", points: 5 },
            { name: "Mansa Musa", points: 4 },
            { name: "Donald Trump", points: 4 }
          ]
        }
      ]
    },
    {
      question: "How do you display your glory?",
      choices: [
        {
          text: "Hold violent beheadings",
          rulers: [
            { name: "Genghis Khan", points: 6 },
            { name: "Napoleon", points: 1 },
            { name: "Mao Zedong", points: 2 },
            { name: "Joseph Stalin", points: 2 },
            { name: "Mansa Musa", points: 0 },
            { name: "Donald Trump", points: 0 }
          ]
        },
        {
          text: "Showcase your military might",
          rulers: [
            { name: "Genghis Khan", points: 6 },
            { name: "Napoleon", points: 6 },
            { name: "Mao Zedong", points: 5 },
            { name: "Joseph Stalin", points: 5 },
            { name: "Mansa Musa", points: 3 },
            { name: "Donald Trump", points: 4 }
          ]
        },
        {
          text: "Build grand monuments to your greatness",
          rulers: [
            { name: "Genghis Khan", points: 3 },
            { name: "Napoleon", points: 1 },
            { name: "Mao Zedong", points: 4 },
            { name: "Joseph Stalin", points: 3 },
            { name: "Mansa Musa", points: 6 },
            { name: "Donald Trump", points: 0 }
          ]
        },
        {
          text: "Displaying exotic goods obtained through widespread trade",
          rulers: [
            { name: "Genghis Khan", points: 2 },
            { name: "Napoleon", points: 2 },
            { name: "Mao Zedong", points: 0 },
            { name: "Joseph Stalin", points: 0 },
            { name: "Mansa Musa", points: 6 },
            { name: "Donald Trump", points: 0 }
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
  
  // Share results
  function shareResults() {
    const shareText = `I am most like ${resultData.topRuler} (${resultData.topPercentage}% match) according to the Historical Ruler Quiz! Discover which ruler you match with!`;
    
    if (navigator.share) {
      navigator.share({
        title: 'My Historical Ruler Match',
        text: shareText,
        url: window.location.href
      })
      .catch((error) => console.error('Error sharing:', error));
    } else {
      // Fallback for browsers that don't support the Web Share API
      navigator.clipboard.writeText(shareText + ' ' + window.location.href)
        .then(() => {
          alert('Results copied to clipboard! Share with your friends.');
        })
        .catch(err => {
          console.error('Failed to copy: ', err);
        });
    }
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
    stroke-dasharray: 0, 251.33; /* Circumference of circle with r=40: 2*PI*40 */
    transform: rotate(-90deg);
    transform-origin: center;
    stroke-linecap: round;
    transition: all 0.8s ease;
  }
  
  .chart-background {
    stroke: rgba(210, 180, 140, 0.3);
    stroke-dasharray: 251.33, 0; /* Full circumference */
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
  
  .share-container {
    text-align: center;
    margin-top: 30px;
    padding-top: 15px;
    border-top: 1px dotted #c0a080;
  }
  
  .share-btn {
    background-color: #8c6b3b;
    color: #fffaf0;
    border: none;
    border-radius: 5px;
    padding: 12px 24px;
    font-size: 1rem;
    font-weight: bold;
    font-family: 'Libre Baskerville', 'Palatino Linotype', serif;
    cursor: pointer;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    transition: all 0.3s ease;
    box-shadow: 0 3px 5px rgba(78, 54, 41, 0.2);
    position: relative;
    overflow: hidden;
  }
  
  .share-btn::before {
    content: "";
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
    transition: 0.5s;
    z-index: 1;
  }
  
  .share-btn:hover {
    background-color: #73583a;
    transform: translateY(-2px);
    box-shadow: 0 5px 10px rgba(78, 54, 41, 0.3);
  }
  
  .share-btn:hover::before {
    left: 100%;
  }
  
  .share-icon {
    margin-right: 10px;
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
  <h1>Which Historical Ruler Are You?</h1>
  <div class="quote">
    "From conquerors to revolutionaries, history is defined by those who rule. Discover which one you most resemble."
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
                  style="stroke-dasharray: {resultData.topPercentage >= 100 ? '251.33, 0' : `${Math.round(resultData.topPercentage * 2.5133)}, 251.33`}" />
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
      
      <div class="share-container">
        <button class="share-btn" on:click={shareResults}>
          <svg class="share-icon" viewBox="0 0 24 24" width="16" height="16">
            <path fill="currentColor" d="M18,16.08C17.24,16.08 16.56,16.38 16.04,16.85L8.91,12.7C8.96,12.47 9,12.24 9,12C9,11.76 8.96,11.53 8.91,11.3L15.96,7.19C16.5,7.69 17.21,8 18,8A3,3 0 0,0 21,5A3,3 0 0,0 18,2A3,3 0 0,0 15,5C15,5.24 15.04,5.47 15.09,5.7L8.04,9.81C7.5,9.31 6.79,9 6,9A3,3 0 0,0 3,12A3,3 0 0,0 6,15C6.79,15 7.5,14.69 8.04,14.19L15.16,18.34C15.11,18.55 15.08,18.77 15.08,19C15.08,20.61 16.39,21.91 18,21.91C19.61,21.91 20.92,20.61 20.92,19A2.92,2.92 0 0,0 18,16.08Z" />
          </svg>
          Share My Result
        </button>
      </div>
    </div>
  </div>
{/if}
