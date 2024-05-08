<template>
  <div class="courses">
    <h3 class="text-center lorem-ipsum-heading">Welcome. Here you can practice your programming skills. By clicking on the generate task button you will get a random programming task that you can solve. After solving it by clicking the review code button an AI assistant will give you feedback on your code.</h3>
    <div class="text-center mb-4">
      <h2>Programming Task:</h2>
      <p>{{ task }}</p>
      <br>
      <button @click="generateTask" class="btn grey darken-1 white-text">Generate Task</button>
    </div>

    <div class="text-center mb-4">
      <h2>Enter Your Code:</h2>
      <textarea v-model="inputCode" rows="10" cols="50" class="bordered-textarea"></textarea>
      <br>
      <button @click="gradeCode" class="btn grey darken-1 white-text" :disabled="gradingInProgress">Review Code</button>
    </div>

    <v-progress-linear v-if="gradingInProgress" indeterminate color="primary"></v-progress-linear>

    <v-dialog v-model="dialog" persistent max-width="800px">
      <v-card>
        <v-card-title class="headline">Code Review</v-card-title>
        <v-card-text>
          <div v-for="(comment, index) in grade.comments.split('\\n')"
    :key="index" class="review-comment">
            {{ comment }}
          </div>
          <div class="grade-display">
            Grade: {{ grade.grade }}/5
          </div>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="green darken-1" text @click="dialog = false">Close</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>


  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      inputCode: '',
      task: '',
      grade: null,
      dialog: false,
      gradingInProgress: false
    };
  },
  methods: {
    generateTask() {
      const tasks = [
        "Write a function to calculate the factorial of a number.",
        "Implement a function to check if a string is a palindrome.",
        "Write a function to reverse a string.",
        "Implement a function to find the maximum number in an array.",
        "Write a program to check if a number is prime or not.",
        "Implement a function to remove duplicate elements from an array.",
        "Write a function to find the Fibonacci sequence up to a certain number of terms.",
        "Implement a function to check if two strings are anagrams of each other.",
        "Write a program to find the square root of a number.",
        "Implement a function to merge two sorted arrays into one sorted array.",
        "Write a function to convert Celsius to Fahrenheit.",
        "Implement a function to find the longest word in a sentence.",
        "Write a program to count the number of vowels in a string.",
        "Implement a function to check if a given year is a leap year or not.",
        "Write a function to generate a random number within a given range.",
        "Implement a function to capitalize the first letter of each word in a sentence.",
        "Write a program to find the sum of all elements in an array.",
        "Implement a function to remove all whitespace from a string.",
        "Write a function to check if a number is even or odd.",
        "Implement a function to find the factorial of all numbers up to a given number.",
        "Write a program to find the median of an array.",
        "Implement a function to check if a given string contains only digits.",
        "Write a function to find the GCD (Greatest Common Divisor) of two numbers.",
        "Implement a function to rotate elements in an array to the left by a given number of positions.",
        "Write a program to reverse a linked list.",
        "Implement a function to find the power of a number using recursion.",
        "Write a function to convert a binary number to decimal.",
        "Implement a function to remove all occurrences of a specified element from an array.",
        "Write a program to find the sum of digits of a number.",
        "Implement a function to check if a string is a valid email address.",
        "Write a program to sort an array of integers in ascending order using bubble sort.",
        "Implement a function to calculate the area of a triangle given the lengths of its sides.",
        "Write a function to convert decimal to binary.",
        "Implement a function to find the number of occurrences of a character in a string.",
        "Write a program to find the largest and smallest elements in an array.",
        "Implement a function to find the longest common prefix of an array of strings.",
        "Write a function to check if a given number is a perfect number or not.",
        "Implement a function to find the index of the first occurrence of a given element in an array.",
        "Write a program to check if a given string is a valid palindrome ignoring non-alphanumeric characters.",
        "Implement a function to calculate the sum of natural numbers up to a given number.",
        "Write a function to reverse words in a sentence.",
        "Implement a function to check if a given number is a Fibonacci number.",
        "Write a program to find the length of the longest consecutive sequence in an unsorted array.",
        "Implement a function to check if a string is a valid IPv4 address.",
        "Write a function to calculate the nth term of the Fibonacci sequence without using recursion.",
        "Implement a function to find the intersection of two arrays.",
        "Write a program to check if a given string is a valid IPv6 address.",
        "Implement a function to find the number of trailing zeroes in the factorial of a given number."
      ];

      const randomIndex = Math.floor(Math.random() * tasks.length);
      this.task = tasks[randomIndex];
    },
    gradeCode() {
      const OPENAI_API_KEY = 'OVDJE KLJUČ IDE';

      this.gradingInProgress = true;
      
      const data = {
        model: "gpt-3.5-turbo",
        messages: [
          {
            role: "system",
            content: "You are a helpful assistant."
          },
          {
            role: "user",
            content: "Please grade the following code:\n\n" + this.inputCode
          },
          
        ]
      };

      const headers = {
        'Content-Type': 'application/json',
        'Authorization': `Bearer ${OPENAI_API_KEY}`
      };

      axios.post('https://api.openai.com/v1/chat/completions', data, { headers })
        .then(response => {
          const feedback = response.data.choices[0].message.content.trim();

          this.dialog = true;
          this.gradingInProgress = false;
          
          const lines = feedback.split('\n');
          
          let comments = [];
          let grade = null;

          for (let line of lines) {
            let parsed = parseInt(line);

            if (!isNaN(parsed) && parsed >= 1 && parsed <= 5) {
              grade = parsed;
            } else {
              comments.push(line);
            }
          }

          comments = comments.join('\n');

          if (grade === null) {
            grade = 1;
          }

          this.grade = {
            "grade": grade,
            "comments": comments,
            "formattedResponse": `<div><h2>Review:</h2><p class="grade-feedback">${comments}</p><p class="grade-feedback">Grade: ${grade}/5</p></div>`
          };

          this.dialog = true;
        })
        .catch(error => {
          console.error(error);
          this.gradingInProgress = false;
        });
    }
  }
}
</script>

<style scoped>
.courses {
  background-image: url('https://img.freepik.com/free-vector/binary-code-algorithm-concept-background-virtual-learning_1017-45444.jpg?w=996&t=st=1713806388~exp=1713806988~hmac=b10a707d35bc4a00573fdaf37691bec0d03c0d58ec1238f6aa899b423a5f8386');
  background-size: cover;
  background-position: center;
  min-height: 100vh;
  background-color: rgba(255, 255, 255, 0.601);
  
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.mb-4 {
  margin-bottom: 1.5rem; 
}

.bordered-textarea {
  border: 1px solid #ccc;
  padding: 5px;
  width: 100%;
  max-width: 500px;
  resize: vertical;
}

.btn {
  background-color: #424242;
  color: white;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  border-radius: 5px;
  transition: background-color 0.3s;
}

.btn:hover {
  background-color: #616161;
}

.grade-feedback {
  padding: 0 20px; 
}

.lorem-ipsum-heading {
  font-size: 1rem;
  margin-top: 80px; 
  margin-bottom: 30px; 
  max-width: 700px; 
  line-height: 1.5; 
  text-align: center; 
}

h2 {
  margin-top: 30px; 
}

.review-comment {
  margin-bottom: 10px;
  padding: 10px;
  background-color: #6560602f;
  border-left: 5px solid #2e7d32;
  font-size: 1.1rem; }

.grade-display {
  margin-top: 20px;
  font-size: 1.4rem;
  font-weight: bold;
  color: #2e7d32;
}

.v-dialog .v-card {
  background-color: #ffffff;
}

.v-btn {
  transition: background-color 0.3s;
}

.v-btn:hover {
  background-color: #023004;
}
</style>
