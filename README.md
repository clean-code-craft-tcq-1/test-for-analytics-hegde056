# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

Fill the parts marked 'ENTER' in the **Tasks** section below.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
1. Validity of csv file i.e Uncorrupted 
2. Read access to csv file i.e not locked 
3. Threshold levels for calculating breaches. 
4. Server and storage space availability for storing PDF reports
5. Notification Utility availability (network online/offline)
6. Fixing a day of week for PDF storage per week. 


### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No            | PDF convertor utility taken from third party who would be responsible for PDF conversion and covers the tests
Counting the breaches       | Yes           | This is part of the analysis-functionality software being developed. 
Detecting trends            | Yes           | This is part of the analysis-functionality software being developed.
Notification utility        | No            | Testing if notification has reached the user is not part of test.   

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
1. Write "Invalid input" to the PDF when the csv doesn't contain expected data
1. Write "File Inaccessible" to the PDF when the csv file is inacessible i.e no read access due to locks. 
1. Write "File not found" to PDF when csv file is not available in the server. 
2. Write N number of breaches to PDF from a csv containing readings that cross upper and/or lower thresholds
3. Write 0 number of breaches to PDF from a csv containing readings that do NOT cross upper or lower thresholds
4. Write timestamp to PDF for recording trends when the reading was continuously increasing for 30 minutes
5. No timestamp trend in PDF report when the reading was NOT continuously increasing for 30 minutes
6. PDF storage to server is triggered when the new PDF report is generated on pre-determined day of week. 
7. No PDF report storage when the day is other than the pre-determined storing day.
8. "New report available" trigger to Notification Utility when new PDF report is available in the storage server. 
9. No triggering of Notification utility when the day is other than the pre-determined day when PDF report will be available. 

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | New PDF report| Notification to user(say Email)| Mock the email notification
Report inaccessible server | server path/location | error code/message  | mock server inacessibility
Find minimum and maximum   | validated csv data | min value & max value from the total csv data| None - it's a pure function
Detect trend               | validated csv data |    timestamp data      | None - it's a pure function
Write to PDF               | internal analysis data | PDF report file   | Fake PDF creation from internal analysis data
