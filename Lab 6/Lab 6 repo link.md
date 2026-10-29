# Lab 6: Attendance Eligibility — Code and Branch Coverage

## Project repository

[PiyaB06/L6_L7_62_attendance_eligibility](https://github.com/PiyaB06/L6_L7_62_attendance_eligibility)

## Project overview

This project is a small Python application for evaluating student attendance and its effect on exam eligibility. It includes logic to calculate an attendance percentage while accounting for medical leave, decide whether a student is eligible to sit an exam, and select an attendance warning based on the student's percentage and the time remaining.

The lab focuses on code and branch coverage: tests exercise the different conditions and outcomes in these functions, including boundary values and invalid input.

## Work completed

Added test cases to the existing test file to cover more of the application's logic:

- **Attendance calculation:** Tests the standard percentage calculation, invalid total-class and attended-class values, the medical-leave credit cap, and the cap on credited attendance.
- **Exam eligibility:** Tests the eligible and detained outcomes, the fees-pending outcome, and cases where condonation either makes a student eligible or is required.
- **Attendance warnings:** Tests when no warning is needed, when a reminder is sent, and the critical-warning and final-notice outcomes based on weeks remaining.

Parameterized tests are used for related invalid-input cases. The work was limited to the test file; the application's implementation was not changed.
