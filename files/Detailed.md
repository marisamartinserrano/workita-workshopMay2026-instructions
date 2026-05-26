# Detailed.md

This files provides the journeys to be implemented each as a separate spec for Open Spec

## About

**workita-stepbystep** is an AI-powered step-by-step job application companion. It guides users through the job application process using Google Gemini (via Genkit) to provide intelligent, contextual assistance at each stage.

## Navigation menu (Spec: 010-optimize-navigation_menu)
- The app navigation menu will always be displayed on the left side of the screen.
- The app navigation menu will mark where the user is in the app and will allow the user to easily navigate between the different sections of the app, including the different journeys
- The navigation menu will include the following sections and subsections:
- - Home: This will be the landing page of the app, it will display a welcome message and a dashboard with an overview of the user's job search progress, including the number of applications submitted, upcoming interviews, and recent activity.
- - Onboarding/Profile: This section will allow users to input and update their job preferences, upload their CV, and provide their LinkedIn profile URL. It will also display personalized recommendations for optimizing their CV and LinkedIn profile based on the information provided.
- - New Candidature: This section will allow users to start a new job application process
- - Selection Process: This section will guide users through each stage of the job application process, providing specific guidance and support for each stage.
  - - - Application submitted
  - - - Interview with recruiter
  - - - Technical interview
  - - - Use case or assignment
  - - - Team interview
  - - - Manager interview
  - - - Client/Stakeholder interview
  - - - Cultural interview
  - - - Leadership interview
  - - - Offer received or candidature rejected
- - Closing: This section will allow users to close their candidatures and provide feedback on the app's guidance and support throughout the job application process.
- - Glossary: This section will provide a glossary of key terms and concepts related to the
- - Quizzes: This section will provide playful quizzes to test users' understanding of the job application process and the specific requirements for the roles they are applying to.

## Home page (Spec: 011-optimize-home_page)
- This will be the landing page of the app, it will display a welcome message and a dashboard with an overview of the user's job search progress, including the number of applications submitted, upcoming interviews, and recent activity.
- It will be presented to the user after successfully logging in or registering, and it will also be accessible from the navigation menu at any time.

## Journeys
Each journey is designed to support users in different stages of their job search, from registration and onboarding to applying for specific roles. The app leverages AI to analyze user profiles, job descriptions, and provide personalized recommendations to enhance the user's chances of success in their job applications.
Each journey will be presented in the UI as a separate section or tab, allowing users to easily navigate between them and access the specific features and guidance they need at each stage of their job search process.
These are the main user journeys that the app supports:

**Registration / Log in** (NA: Already implemented)

- Users can create an account and log in to save their progress and access personalized features.
- Users will register and log in using Google SSO, leveraging their existing Google accounts for a seamless experience.
- If users have not registered, they will be prompted to do so when they first access the app. Once registered, they can log in using their Google credentials.
- Unless users log in, they can still explore the app and access general information, but personalized features and progress saving will be unavailable.
- On registration via Google SSO, the app will create a new user profile in the database using the information retrieved from the user's Google account (e.g., name, email). This allows for a personalized experience and enables users to save their progress and access it across devices.

**Onboarding** (Spec: 012-optimize-onboarding)

- After the user is registered and logged in, they will be guided through an onboarding process where they can input their job preferences: Role, Seniority, Industry, Location, preferred companies, Presencial/Remote/Hybrid, salary expectations.
- The app will ask the user to upload their extended CV as a document, this file will be stored locally and on the database. In case the file is not a CV, the AI will prompt the user to upload the proper file. This CV will be used to tailor the job application guidance and AI interactions to the user's specific background and experience.
  - The app will analyze the uploaded CV to extract relevant information such as skills, experience, and education. This information will be used to provide personalized recommendations for job applications, interview preparation, and networking opportunities.
  - The app will also use the information from the CV to identify potential gaps or areas for improvement in the user's profile. This may include suggestions for additional skills to acquire, certifications to pursue, or ways to better highlight existing experience.
  - The app will simulate how the user's CV would be parsed by common Applicant Tracking Systems (ATS) and provide feedback on how to optimize the CV for better visibility in these systems. This may include recommendations for formatting, keyword usage, and overall structure to increase the chances of passing through ATS filters.
- The app will also ask the user to input their LinkedIn profile URL. This information will be used to further customize the job application guidance and AI interactions based on the user's professional background and network.
  - The app will present recommendations for improving the user's LinkedIn profile based on the information provided in the CV and LinkedIn URL. This may include suggestions for optimizing the profile summary, adding relevant skills, or improving the overall presentation to make the profile more suitable for LinkedIn algorithms (recruiter search, consistency with CV, Application Tracking Systems filtering). The app will also present the user with the summary of recommendations and the rationale behind them, as well as a quick summary of how LinkedIn works for candidates.
- The app will ask the user about 
- The information collected during onboarding (job preferences, CV, LinkedIn profile) will be stored in the database and used to personalize the user's experience throughout the app. This allows for tailored job recommendations, application guidance, and interview preparation based on the user's specific background and preferences.

**New Candidature** (Spec: 013-optimize-new-candidature)

- The user will start a new job application process by sharing the link to the job description (e.g. from LinkedIn, company website, etc).
- The app will analyze the job description to extract and present key information such as:
  - Company overview, products and industry, financial health, news to provide context about the organization and its market.
  - Required skills, experience, and expected salary, presented to the user in a structured format. This will help the user understand the requirements and expectations for the role.
  - Based on the candidate profile (CV + LinkedIn) and the job description, the app will perform the following:
    - **% Match:** The app will calculate a percentage match between the user's profile and the job requirements.
    - **Strengths:** The app will identify and highlight the user's strengths in relation to the job requirements.
    - **Gaps:** The app will identify any gaps or areas where the user's profile may not fully meet the job requirements, providing insights into potential areas for improvement or additional focus in the application process.
    - **Candidate Key differentiators:** The app will identify key differentiators in the user's profile that can be emphasized in the application to make it stand out to recruiters and hiring managers.
    - **Keywords for ATS:** The app will extract relevant keywords from the job description that are important for passing through Applicant Tracking Systems (ATS) and provide recommendations on how to incorporate these keywords effectively into the user's CV and application materials.
    - **Recommendations for LinkedIn profile:** Based on the analysis of the job description and the user's LinkedIn profile, the app will provide specific recommendations for optimizing the LinkedIn profile to increase visibility and attractiveness to recruiters and hiring managers for the specific role.
    - **Recommendations for CV:** The app will provide tailored recommendations for optimizing the user's CV to better align with the job description and increase the chances of passing through ATS filters. This may include suggestions for formatting, keyword usage, and overall structure to make the CV more appealing to recruiters and hiring managers.
- The app will encourage the user to reach out to the recruiter or hiring manager or to people in their network who work at the company to gather more information about the role and increase their chances of success in the application process. The app will provide guidance on how to approach these contacts, what questions to ask, and how to leverage this information in the application and interview process.
- All the information above will be stored in the database, allowing the user to track their applications and refer back to the insights and recommendations provided for each job application.
- For each candidature, the app will create a glossary of industry-specific and role-specific terms and concepts mentioned in the job description. This glossary will be accessible to the user throughout the application process, providing definitions and explanations to help the user better understand the requirements and expectations for the role.

- **Selection process** (Spec: 014-optimize-selection-process)
- The app will guide the user through each stage of the job application process, providing specific guidance and support for each stage. 
- The app will create 10 questions for each interview type (recruiter, technical, use case/assignment, team, manager, client/stakeholder, cultural, leadership) to help the user prepare for each stage of the process. These questions will be based on common interview questions for each type of interview and will be tailored to the specific role and industry based on the information provided by the user during onboarding and the job description analysis.
- The stages include:
  - Application submitted: The user will be prompted to input the date when they submitted their application and any relevant information such as the method of application (e.g., through LinkedIn, company website, referral, etc.) and any initial feedback received from the hiring company (e.g., "Application received", "Application under review", etc.).
  - Interview with recruiter: The app will prompt the user to input the date when they had the interview with the recruiter and any relevant information such as the interview format (e.g., phone, video, in-person), the interviewer's name and role, and any feedback received from the recruiter (e.g., "Positive feedback, moving to next stage", "Requested additional information", etc.). The app will suggest a list of 10 questions that are typical for that interview
  - Technical interview: The app will prompt the user to input the date when they had the technical interview and any relevant information such as the interview format (e.g., coding challenge, whiteboard, take-home assignment), the interviewer's name and role, and any feedback received from the interviewer (e.g., "Strong technical skills demonstrated", "Struggled with certain concepts", etc.). The app will suggest a list of 10 questions that are typical for that interview
  - Use case or assignment: The app will prompt the user to input the date when they received the use case or assignment and any relevant information such as the format of the assignment (e.g., written report, presentation, project), the deadline for submission, and any feedback received from the hiring company (e.g., "Assignment received, under review", "Requested clarification on certain aspects", etc.). The app will suggest a list of 10 questions that are typical for that interview
  - Team interview: The app will prompt the user to input the date when they had the team interview and any relevant information such as the interview format (e.g., panel, group discussion), the names and roles of the team members involved, and any feedback received from the team (e.g., "Positive feedback from team members", "Concerns about cultural fit", etc.). The app will suggest a list of 10 questions that are typical for that interview
  - Manager interview: The app will prompt the user to input the date when they had the manager interview and any relevant information such as the interview format (e.g., one-on-one, panel), the manager's name and role, and any feedback received from the manager (e.g., "Strong leadership potential", "Concerns about experience in certain areas", etc.). The app will suggest a list of 10 questions that are typical for that interview
  - Client/Stakeholder interview: The app will prompt the user to input the date when they had the client/stakeholder interview and any relevant information such as the interview format (e.g., presentation, case study), the client's/stakeholder's name and role, and any feedback received from the client/stakeholder (e.g., "Impressed with communication skills", "Concerns about industry experience", etc.). The app will suggest a list of 10 questions that are typical for that interview
  - Cultural interview: The app will prompt the user to input the date when they had the cultural interview and any relevant information such as the interview format (e.g., panel, group discussion), the names and roles of the interviewers involved, and any feedback received from the interviewers (e.g., "Strong cultural fit", "Concerns about alignment with company values", etc.). The app will suggest a list of 10 questions that are typical for that interview
  - Leadership interview: The app will prompt the user to input the date when they had the leadership interview and any relevant information such as the interview format (e.g., one-on-one, panel), the leader's name and role, and any feedback received from the leader (e.g., "Strong leadership potential", "Concerns about experience in certain areas", etc.). The app will suggest a list of 10 questions that are typical for that interview
  - Offer received or candidature rejected: The app will prompt the user to input the date when they received the offer or rejection and any relevant information such as the details of the offer (e.g., salary, benefits, start date) or the feedback received in case of rejection (e.g., "Received offer with competitive salary", "Was informed that my profile was not a good fit for the role", etc.). The app will also provide guidance on how to evaluate job offers and negotiate terms if an offer is received, or how to learn from rejections and improve for future applications.
- For each stage, the app will save the date when the user entered that stage and prompt the user to input relevant information such as:
  - Interview questions asked
  - Feedback received from the hiring company
  - User's feelings and thoughts about the process at that stage

**Closing** (Spec: 015-optimize-closing)
- The user will be prompted to select the candidature to close. The candidature will be default to the one the user was most recently working on, but they can select any of the open candidatures in their profile. The app will present the full list of open candidatures including position, company, stage, last updated date
- The user will be prompted to select the reason for closing the candidature from a predefined list of options (e.g., "Received offer from another company", "No longer interested in the role", "Accepted another offer", "Position filled by the company", etc.). This information will be stored in the database and can be used for analytics and improving the app's guidance in the future.
- The user will be prompted to enter any additional information provided by the hiring company regarding the outcome of their application (e.g., "Received feedback that my profile was not a good fit for the role", "Was informed that the position was put on hold", etc.). This information will also be stored in the database and can provide valuable insights into the job market and help improve the app's recommendations and guidance for future users.
- The candidature will be marked as closed in the database
- At the end, the user will be prompted to rate (from 1 to 5) and provide feedback on the app's guidance and support throughout the job application process. This feedback will be used to continuously improve the app's AI models and user experience, ensuring that it remains a valuable tool for job seekers in their career journeys. 

**Glossary of key terms and concepts** (Spec: 016-optimize-glossary)
- The app will maintain a glossary of key terms and concepts related to the job search process, roles, industries, and other relevant topics by candidature. This glossary will be accessible to users throughout their journey, providing definitions and explanations to help them better understand the language and terminology used in job descriptions, interviews, and professional networking.
- The glossary will be continuously updated and expanded based on the job descriptions analyzed by the app and the feedback provided by users. This will ensure that the glossary remains relevant and comprehensive, covering a wide range of terms and concepts that job seekers may encounter during their job search process.
- The user can search the glossary by candidature, role, industry, or specific terms. This will allow users to quickly find definitions and explanations for any unfamiliar terms they encounter during their job search journey, enhancing their understanding and confidence as they navigate the application process.
- The user will enter role, seniority, industry, company and as optional a link to a job description (from LinkedIn or the Company's talent page), and the app will generate a list of relevant terms and concepts related to those inputs. This will help users to familiarize themselves with the specific language and terminology used in their target roles and industries, improving their ability to understand job descriptions, prepare for interviews, and engage in professional networking effectively.
- The glossary will include definitions, explanations, and examples for each term or concept, providing users with a comprehensive resource to enhance their understanding of the job search process and the specific requirements for their target roles and industries.
- For each iteration, the glossary will contain between 20 and 50 terms, depending on the role, seniority, industry, company and job description provided by the user. This will ensure that the glossary is comprehensive enough to cover the key terms and concepts relevant to the user's job search journey, while also being manageable and easy to navigate.
- The glossary will be saved on the database and will be accessible to the user at any time during their job search journey. This will allow users to refer back to the glossary as needed, reinforcing their understanding of key terms and concepts and helping them to navigate the job search process with greater confidence and clarity.

**Quizzes** (Spec: 017-optimize-quizzes)
- The user will be prompted with playful quizzes to test their understanding of the job application process and the specific requirements for the roles they are applying to. These quizzes will be designed to reinforce key concepts and provide an engaging way for users to learn and prepare for their job search.
- The quizzes will focus on the latest candidature the user is working on, using the information from the job description, the user's profile, and the insights provided by the app to create personalized quiz questions. This will help users to better understand the specific requirements and expectations for the roles they are applying to and to prepare more effectively for interviews and networking opportunities.
- The quizzes will cover topics such as:
  - Understanding job descriptions and requirements
  - Optimizing CVs for ATS
  - Best practices for LinkedIn profiles
  - Interview preparation and common questions indicating the interview stage, for all stages of the process described in the previous journeys
  - Power of professional networking
  - Glossary of key terms and concepts in the job search process, role, industry, etc.
