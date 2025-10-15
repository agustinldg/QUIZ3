# Requirements Document

## Introduction

QUIZ3 is a client-side web application that creates interactive quizzes by reading questions and answers from a Google Apps Script service. The application presents questions with multiple choice answers (typically 3 options) and includes support for base64-encoded images in both questions and answer options. The app operates entirely in the browser without requiring a server backend, using JSONP to communicate with Google Apps Script.

## Requirements

### Requirement 1

**User Story:** As a quiz creator, I want to store quiz questions and answers in a Google Spreadsheet processed by Google Apps Script, so that I can easily manage and update quiz content with images converted to base64 format.

#### Acceptance Criteria

1. WHEN the application starts THEN the system SHALL fetch quiz data from a Google Apps Script service using JSONP
2. WHEN the service returns quiz data THEN the system SHALL parse questions with prompt images, answer choices, and correct answer IDs
3. IF the Google service is inaccessible THEN the system SHALL display an error message with retry options
4. WHEN the service fails THEN the system SHALL offer fallback to local JSON file
5. WHEN loading data THEN the system SHALL display a countdown timer during the fetch process

### Requirement 2

**User Story:** As a quiz taker, I want to see questions with multiple choice answers that are shuffled for each quiz session, so that I can select my response from randomized options.

#### Acceptance Criteria

1. WHEN a question is displayed THEN the system SHALL show exactly 3 answer options
2. WHEN answer options are presented THEN the system SHALL shuffle the choices using Fisher-Yates algorithm
3. WHEN an answer is selected THEN the system SHALL provide visual feedback with a green checkmark
4. WHEN the user clicks an answer THEN the system SHALL record the selection and maintain it during navigation
5. WHEN shuffling occurs THEN the system SHALL track the correct answer index in the shuffled array

### Requirement 3

**User Story:** As a quiz taker, I want to see base64-encoded images with questions and answers, so that the quiz can be more engaging and visual without external dependencies.

#### Acceptance Criteria

1. WHEN a question has a base64 image THEN the system SHALL display the image in a clickable button format
2. WHEN answer options have base64 images THEN the system SHALL display images with captions below each option
3. IF an image fails to load THEN the system SHALL display appropriate alt text
4. WHEN images are displayed THEN the system SHALL ensure they are responsive and properly sized for different devices
5. WHEN images are clicked THEN the system SHALL trigger text-to-speech for the associated caption

### Requirement 4

**User Story:** As a quiz taker, I want to navigate through questions with previous/next buttons, so that I can review and change my answers before finishing.

#### Acceptance Criteria

1. WHEN the quiz starts THEN the system SHALL display the first question with navigation controls
2. WHEN on the first question THEN the system SHALL disable the previous button
3. WHEN on the last question THEN the system SHALL change the next button text to "Finalizar"
4. WHEN navigating between questions THEN the system SHALL maintain the user's previous selections
5. WHEN using keyboard navigation THEN the system SHALL support arrow keys for navigation and Enter for next question

### Requirement 5

**User Story:** As a quiz taker, I want to see my quiz results with the option to download a PDF report, so that I can understand my performance and keep a record.

#### Acceptance Criteria

1. WHEN all questions are completed THEN the system SHALL calculate and display the total score
2. WHEN results are shown THEN the system SHALL display the score in format "X / Y" 
3. WHEN viewing results THEN the system SHALL provide options to restart the quiz and download results
4. WHEN downloading results THEN the system SHALL generate a PDF with question images, user answers, and correct answers
5. WHEN generating PDF THEN the system SHALL mark correct answers with green borders and incorrect answers with red diagonal lines

### Requirement 6

**User Story:** As a user, I want the application to work entirely in my browser with accessibility features, so that I don't need to install server software and can use the app with assistive technologies.

#### Acceptance Criteria

1. WHEN the application is accessed THEN the system SHALL run entirely in the client browser
2. WHEN processing quiz data THEN the system SHALL use JSONP to avoid CORS issues with Google Apps Script
3. WHEN accessing the quiz THEN the system SHALL support keyboard navigation (1/2/3 for answers, Enter for next, arrows for navigation)
4. WHEN images are clicked THEN the system SHALL use speech synthesis to read captions aloud
5. WHEN using speech synthesis THEN the system SHALL support voice selection and language preferences
### 
Requirement 7

**User Story:** As a user on different devices, I want the quiz to display properly on mobile, tablet, and desktop screens, so that I can take the quiz on any device.

#### Acceptance Criteria

1. WHEN accessing on mobile devices THEN the system SHALL display choices in a 2-column grid layout
2. WHEN accessing on tablets in landscape THEN the system SHALL use a split layout with prompt on left and choices on right
3. WHEN accessing on tablets in portrait THEN the system SHALL use a single column layout with larger elements
4. WHEN displaying on any device THEN the system SHALL use responsive font sizes and spacing
5. WHEN using touch devices THEN the system SHALL provide appropriate touch targets and hover effects