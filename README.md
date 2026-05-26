# Workita Workshop May 2026 - Instructions
Welcome to the Workita Workshop!
In this workshop you will learn about:
- Workita's capabilities and user journeys
- How to use workita to find the perfect position for you and guide you through the application process
And on the technical side, you will learn about:
- Claude Code as a code companion
- Google Gemini AI and Google Genkit as a way to integrate AI in our Workita app
- Open Spec framework as a way to create and manage new specs for your app, Workita in this case
- Google Cloud OAuth 2.0 as a way to authenticate users in your app with Google SSO

## Step by step instructions
### Step 0. Set up your local environment
OS: Windows 11 Home
Docker Desktop: 4.28.0 
Claude Code (Pro Plan): 2.1.150
IDE: Visual Studio 2022
Github CLI: 2.92.0 
Open Spec CLI: 1.3.1
[Optional] Genkit CLI: 1.30.1
### Step 1. Start Claude Code and create a new Github repository
1. Open Claude Code (I use the CLI)
2. Prompt for Claude Code: "Create a new Github repository called 'workita-yourAICompanion, initialize it with a README.md file and clone it to my computer"
### Step 2. Set the new repository as the working directory in Claude Code
1. Prompt for Claude Code: "we will be working with the repository workita-yourAICompanion""
### Step 3. Create and define CLAUDE.md for Workita
1. Prompt for Claude Code: "Create and edit CLAUDE.md to reflect the following information: Workita is your AI Job Companion. The main features of Workita are: Job Search, Application Tracking, Interview Preparation. Technology stack is: Frontend is Typescript, 
Backend is Node.js, Database is Postgres. Workita will run on http://localhost:8080 via docker-compose. Workita uses Google SSO for user registration and log in, and Google Genkit framework to integrate Google Gemini in the app to provide candidate with best recommendations"
### Step 4. Update manually the CLAUDE.md file with the information about the user journeys:
1. Prompt for Claude Code: "I will now update the CLAUDE.md file with the user journeys locally on my computer, I will let you know once it's done"
2. Update the CLAUDE.md file with the following user journeys:
#### Journeys
Each journey is designed to support users in different stages of their job search, from registration and onboarding to applying for specific roles. The app leverages AI to analyze user profiles, job descriptions, and provide personalized recommendations to enhance the user's chances of success in their job applications.
Each journey will be presented in the UI as a separate section or tab, allowing users to easily navigate between them and access the specific features and guidance they need at each stage of their job search process.
These are the main user journeys that the app supports:
**Registration / Log in**
- Users can register and log in using Google SSO, providing a seamless and secure authentication process.
**Onboarding**
**New Candidature**
**Selection process**
**Closing**
**Glossary of key terms and concepts**
**Quizzes**
3. Save CLAUDE.md file
4. Prompt for Claude Code: "I have updated the CLAUDE.md file with the user journeys, you can now use this information to guide us in the development of the app and make sure we are aligned with the user needs and expectations. Update accordingly the README.md file"
### Step 5. Run locally Workita:
0. Start Docker Desktop in your computer
1. Get Google Gemini API key on https://aistudio.google.com/api-keys
2. Get Google Cloud OAuth 2.0 credentials for Google SSO on https://console.cloud.google.com/apis/credentials. Authorized Javascript origin should be http://localhost:8080 and authorized redirect URI should be http://localhost:3001/api/auth/google/callback
1. Prompt for Claude Code: "Build Workita app based on CLAUDE.md information. Run Workita locally using docker-compose on http://localhost:8080, make sure to set up the necessary environment variables for Google SSO and Google Gemini AI via Genkit integration"
2. Follow the instructions provided by Claude Code to set up the environment variables and run the app
3. Once the app is running, open http://localhost:8080 in your browser to access Workita and explore its features
4. You will get an "unexpected error" when you try to use the app. Trust Claude Code recommendation to fix the error by creating the tables in the database and applying the necessary migrations, then try again to use the app and it should work fine
5. Prompt for Claude Code: "stop all the containers, rebuild it and run it with docker compose on localhost:8080"
6. Once the app is running, open http://localhost:8080 in your browser to access Workita and explore its features
7. When trying to generate with Gemini AI in Workita, you will notice that it doesn't work, check the logs of the container, you will find the Gemini AI model is deprecated. Prompt for Claude Code: "Stop all containers. Gemini AI model is deprecated, please update the app to use gemini-2.5-flash and make sure to update the Genkit integration accordingly"
8. Prompt for Claude Code: "rebuild the app with the necessary updates to use gemini-2.5-flash and run it again with docker compose on localhost:8080"
9. Prompt for Claude Code: "Update CLAUDE.md and README.md files to reflect the changes we made to the app regarding the update of Gemini AI model to gemini-2.5-flash and the necessary updates in Genkit integration"
### Step 6. Set up Open Spec:
1. Prompt for Claude Code:"I want to use Spec Driven Development approach for Workita app, set up Open Spec framework in this repository"
### Step 7. Set up Open Spec:
1. Prompt for Claude Code:"run open-spec init to create the initial Open Spec files for Workita app, make sure to define the necessary specs for the app based on the information in CLAUDE.md file and the user journeys we defined"
2. Follow the instructions provided by Claude Code to implement each of the initial specs e.g. "run openspec new change 01-home-page". 
3. Then prompt for Claude Code: "Implement the home page of Workita app based on the spec we just created, make sure to follow the spec requirements and acceptance criteria, once you are done, create a pull request with the changes and assign it to me for review". 
4. Then prompt for Claude Code: " Run openspec archite 01-home-page"


