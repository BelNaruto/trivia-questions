# Trivia API Documentation

## Overview

Welcome to the Trivia API documentation! This API provides a simple and effective way to access trivia questions across various categories, difficulties, and formats. Whether you're building a quiz app, a game night application, or just want to challenge your friends, this API has you covered.

## Why Use This Trivia API?

This API is an excellent resource for developers who need reliable trivia content. Here's why you should consider using it:

1. **Easy to Integrate**: Simple endpoints with clear parameters make integration a breeze, even for beginners.
2. **Customizable**: Choose from multiple categories, difficulty levels, and question types to create the perfect trivia experience.
3. **Reliable**: Built on a robust backend that ensures minimal downtime and quick response times.
4. **Free to Use**: Get started without any upfront costs (standard RapidAPI usage limits apply).
5. **Perfect for Learning**: If you're new to APIs, this is an ideal starting point due to its straightforward structure.

## Getting Started

### Prerequisites

- A RapidAPI account
- Your RapidAPI [key](https://rapidapi.com/belchiorarkad-FqvHs2EDOtP/api/trivia-api1)
- Basic understanding of HTTP requests (but don't worry, we'll guide you!)

### Authentication

All requests to the Trivia API require your RapidAPI key in the headers. This is added automatically when you subscribe to the API on RapidAPI.

```javascript
const options = {
  method: 'GET',
  headers: {
    'X-RapidAPI-Key': 'your-rapid-api-key',
    'X-RapidAPI-Host': 'trivia-api1.p.rapidapi.com'
  }
};
```

## Endpoints

The API provides two main endpoints:

### 1. Get Categories

Retrieves all available trivia categories.

**Endpoint:** `/categories`

**Method:** GET

**Example Request:**

```javascript
fetch('https://trivia-api1.p.rapidapi.com/categories', options)
  .then(response =&gt; response.json())
  .then(data =&gt; console.log(data))
  .catch(err =&gt; console.error('Error:', err));
```

**Example Response:**

```json
{
  "success": true,
  "data": [
    {"id": 9, "name": "General Knowledge"},
    {"id": 10, "name": "Entertainment: Books"},
    {"id": 11, "name": "Entertainment: Film"},
    // More categories...
  ]
}
```

### 2. Get Questions

Retrieves trivia questions based on specified parameters.

**Endpoint:** `/getquestions`

**Method:** GET

**Query Parameters:**

| Parameter   | Type   | Required | Default   | Description                                     |
|-------------|--------|----------|-----------|------------------------------------------------|
| type        | string | No       | multiple  | Type of questions to retrieve (multiple/boolean)|
| amount      | number | No       | 10        | Number of questions to retrieve (1-100)         |
| difficulty  | string | No       | easy      | Difficulty level (easy/medium/hard)             |
| categoryId  | number | No       | 10        | Category ID from the categories endpoint        |

**Example Request:**

```javascript
fetch('https://trivia-api1.p.rapidapi.com/getquestions?type=multiple&amount=5&difficulty=medium&categoryId=9', options)
  .then(response =&gt; response.json())
  .then(data =&gt; console.log(data))
  .catch(err =&gt; console.error('Error:', err));
```

**Example Response:**

```json
{
  "success": true,
  "data": [
    {
      "category": "General Knowledge",
      "type": "multiple",
      "difficulty": "medium",
      "question": "What is the name of the popular theory that suggests the universe began from a singular point about 13.8 billion years ago?",
      "correct_answer": "The Big Bang Theory",
      "incorrect_answers": [
        "The Steady State Theory",
        "The Oscillating Universe Theory",
        "The Nebular Hypothesis"
      ]
    },
    // More questions...
  ]
}
```

## Using the API: A Step-by-Step Guide for Beginners

### Step 1: Get Your API Key

1. Go to [RapidAPI](https://rapidapi.com/)
2. Create an account or log in
3. Subscribe to Free [Trivia API]( https://trivia-api1.p.rapidapi.com)
4. Get your API key

### Step 2: Make Your First API Call

Let's start by getting all available categories:

```javascript
// Using fetch (browser)
const options = {
  method: 'GET',
  headers: {
    'X-RapidAPI-Key': 'your-rapid-api-key',
    'X-RapidAPI-Host': 'trivia-api1.p.rapidapi.com'
  }
};

fetch('https://trivia-api1.p.rapidapi.com/categories', options)
  .then(response =&gt; response.json())
  .then(data =&gt; {
    if (data.success) {
      console.log('Categories:', data.data);
    } else {
      console.error('Error:', data.message);
    }
  })
  .catch(err =&gt; console.error('Error:', err));
```

### Step 3: Get Some Questions

Now, let's get 5 easy questions about General Knowledge:

```javascript
const options = {
  method: 'GET',
  headers: {
    'X-RapidAPI-Key': 'your-rapid-api-key',
    'X-RapidAPI-Host': 'trivia-api1.p.rapidapi.com'
  }
};

fetch('https://trivia-api1.p.rapidapi.com/getquestions?type=multiple&amount=5&difficulty=easy&categoryId=9', options)
  .then(response =&gt; response.json())
  .then(data =&gt; {
    if (data.success) {
      // Display each question
      data.data.forEach((question, index) =&gt; {
        console.log(`Question ${index + 1}: ${question.question}`);
        console.log(`Correct Answer: ${question.correct_answer}`);
        console.log(`Incorrect Answers: ${question.incorrect_answers.join(', ')}`);
        console.log('---');
      });
    } else {
      console.error('Error:', data.message);
    }
  })
  .catch(err =&gt; console.error('Error:', err));
```

## Available Categories

The API provides access to numerous categories, including:

- General Knowledge (ID: 9)
- Entertainment: Books (ID: 10)
- Entertainment: Film (ID: 11)
- Entertainment: Music (ID: 12)
- Entertainment: Musicals & Theatres (ID: 13)
- Entertainment: Television (ID: 14)
- Entertainment: Video Games (ID: 15)
- Entertainment: Board Games (ID: 16)
- Science & Nature (ID: 17)
- Science: Computers (ID: 18)
- Science: Mathematics (ID: 19)
- Mythology (ID: 20)
- Sports (ID: 21)
- Geography (ID: 22)
- History (ID: 23)
- Politics (ID: 24)
- Art (ID: 25)
- Celebrities (ID: 26)
- Animals (ID: 27)
- Vehicles (ID: 28)
- Entertainment: Comics (ID: 29)
- Science: Gadgets (ID: 30)
- Entertainment: Japanese Anime & Manga (ID: 31)
- Entertainment: Cartoon & Animations (ID: 32)

## Error Handling

The API uses standard HTTP status codes and returns detailed error messages to help you debug issues.

### Common Error Codes

- **400 Bad Request**: Invalid parameters were provided
- **401 Unauthorized**: Invalid or missing API key
- **404 Not Found**: The requested resource doesn't exist
- **429 Too Many Requests**: You've exceeded your rate limit
- **500 Internal Server Error**: Something went wrong on the server

### Error Response Format

```json
{
  "success": false,
  "error": {
    "code": "400",
    "message": "Invalid type. Allowed values: 'multiple', 'boolean'."
  }
}
```

## Best Practices

1. **Cache Responses**: To reduce API calls, consider caching category data and frequently used questions.
2. **Validate User Input**: Always validate user input before passing it to the API to avoid unnecessary error responses.
3. **Handle Errors Gracefully**: Implement proper error handling to provide a smooth user experience.
4. **Respect Rate Limits**: Be mindful of the API's rate limits to avoid disruptions in your application.

## Creating a Simple Trivia Game

Here's a basic example of how to create a simple trivia game using this API:

```javascript
// Step 1: Get the categories and let user select one
async function loadCategories() {
  const options = {
    method: 'GET',
    headers: {
      'X-RapidAPI-Key': 'your-rapid-api-key',
      'X-RapidAPI-Host': 'trivia-api1.p.rapidapi.com'
    }
  };

  try {
    const response = await fetch('https://trivia-api1.p.rapidapi.com/categories', options);
    const data = await response.json();
    
    if (data.success) {
      // Create a dropdown for categories
      const select = document.getElementById('category-select');
      data.data.forEach(category =&gt; {
        const option = document.createElement('option');
        option.value = category.id;
        option.textContent = category.name;
        select.appendChild(option);
      });
    }
  } catch (error) {
    console.error('Error loading categories:', error);
  }
}

// Step 2: Get questions based on selected category and difficulty
async function loadQuestions() {
  const categoryId = document.getElementById('category-select').value;
  const difficulty = document.getElementById('difficulty-select').value;
  
  const options = {
    method: 'GET',
    headers: {
      'X-RapidAPI-Key': 'your-rapid-api-key',
      'X-RapidAPI-Host': 'trivia-api1.p.rapidapi.com'
    }
  };

  try {
    const response = await fetch(`https://trivia-api1.p.rapidapi.com/getquestions?type=multiple&amount=10&difficulty=${difficulty}&categoryId=${categoryId}`, options);
    const data = await response.json();
    
    if (data.success) {
      // Store questions in global variable
      window.questions = data.data;
      window.currentQuestion = 0;
      window.score = 0;
      
      // Display first question
      displayQuestion();
    }
  } catch (error) {
    console.error('Error loading questions:', error);
  }
}

// Step 3: Display current question
function displayQuestion() {
  if (window.currentQuestion &gt;= window.questions.length) {
    // Game over, show score
    document.getElementById('question-container').innerHTML = `
      <h2>Game Over!</h2>
      <p>Your score: ${window.score} out of ${window.questions.length}</p>
      &lt;button onclick="loadQuestions()"&gt;Play Again&lt;/button&gt;
    `;
    return;
  }
  
  const question = window.questions[window.currentQuestion];
  
  // Create an array with all answers
  const answers = [...question.incorrect_answers, question.correct_answer];
  // Shuffle answers
  answers.sort(() =&gt; Math.random() - 0.5);
  
  let answerHtml = '';
  answers.forEach(answer =&gt; {
    answerHtml += `&lt;button onclick="checkAnswer('${answer}')"&gt;${answer}&lt;/button&gt;`;
  });
  
  document.getElementById('question-container').innerHTML = `
    <h3>Question ${window.currentQuestion + 1} of ${window.questions.length}</h3>
    <p>${question.question}</p>
    <div>${answerHtml}</div>
  `;
}

// Step 4: Check if answer is correct
function checkAnswer(selectedAnswer) {
  const correctAnswer = window.questions[window.currentQuestion].correct_answer;
  
  if (selectedAnswer === correctAnswer) {
    window.score++;
    alert('Correct!');
  } else {
    alert(`Wrong! The correct answer was: ${correctAnswer}`);
  }
  
  window.currentQuestion++;
  displayQuestion();
}

// Initialize the game
document.addEventListener('DOMContentLoaded', loadCategories);
```

## Real-World Applications

This API can be used for various applications, including:

1. **Educational Tools**: Create interactive quizzes for students to test their knowledge.
2. **Party Games**: Develop an app for hosting virtual or in-person trivia nights.
3. **Content for Websites**: Add a "Question of the Day" feature to your website.
4. **Training and Assessment**: Use trivia questions to assess general knowledge for recruitment or training purposes.
5. **Ice Breakers**: Create team-building activities with themed trivia rounds.

## Limitations and Considerations

- The API has a rate limit, so monitor your usage if you have many users.
- Some questions may contain HTML entities (like &quot; for quotes) that you'll need to decode.
- The API doesn't support user-contributed questions at this time.

## Troubleshooting

### Common Issues and Solutions

1. **"Invalid API Key" Error**
   - Make sure you've correctly copied your RapidAPI key
   - Verify that your subscription is active

2. **No Questions Returned**
   - Check that the categoryId is valid
   - Try a different combination of parameters

3. **Rate Limit Exceeded**
   - Implement caching to reduce API calls
   - Consider upgrading your RapidAPI plan if needed

## Conclusion

The Trivia API is a versatile, easy-to-use solution for adding trivia functionality to your applications. With its wide range of categories and customization options, you can create engaging, educational, and entertaining experiences for your users.

Whether you're a beginner just learning about APIs or an experienced developer looking for a reliable trivia source, this API provides everything you need to get started quickly and build amazing trivia applications.

Happy coding!

## Support
- pintoflowpt@gmail.com
