## Part D — Team Project Gherkin Scenarios

**Selected Story:** `SSPT-5 — Create and manage courses` (MVP, High Priority, 5 Story Points)  
*As a student, I want to create and manage my courses so that I can organize my study sessions and track my progress for each course.*

```gherkin
Feature: Create and manage courses (SSPT-5)
  As a student
  I want to create and manage my courses
  So that I can organize my study sessions and track my progress for each course

  Background:
    Given the student is on the courses page

  # Scenario 1 (happy path)
  Scenario: Create a valid course
    When the student submits course name "Agile Software Engineering" and course code "SET312"
    Then the course "SET312" is added to the student's course list
    And "SET312" is selectable when starting a Pomodoro session

  # Scenario 2 (refused / error)
  Scenario: Refuse a duplicate course code
    Given the student already has course "SET312" in their course list
    When the student submits course name "Agile Software Engineering" and course code "SET312"
    Then the duplicate course creation is refused
    And existing course-linked history remains associated with the original course "SET312"

  # Scenario 3 (edge / outline)
  Scenario Outline: Reject course creation when required fields are missing
    When the student submits course name "<name>" and course code "<code>"
    Then no course is created
    And a field-level validation message is shown

    Examples:
      | name                       | code   |
      |                            | SET312 |
      | Agile Software Engineering |        |
      |                            |        |

      