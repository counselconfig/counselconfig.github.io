---
layout: post
title: UIs of yore
tags: modeling dialogue user interfaces
---

I do not think 'entity life history' is a common place term in today's dev communities. These are dialogue diagrams used in the 80's which I think are tremendously useful for modeling the logic of user interface (UI) interaction. I am talking <u>front-end</u> development in the days of Amstrad. Lest we forget, here is an abstract from a report I wrote using the techniques:-

# 4.1 AHC dialogue structure diagram

## 4.1.1 Function definition

A set of SSADM factored elementary processes descriptions based on (Appendix) (1.1.1…1.1.4) constitute a class of function that triggers an update to system survey report data with a Manager’s cottage appraisal.


## 4.1.2 User interface (UI) specification

Based on its function definition I produce an input/output (I/O) description for ‘Process appraisal’ containing data items that make up the final output dialogue.

| From  | To    | Dataflow      | Data Content                                                          | Comments                                                                                                                                                                                                                  |
| ----- | ----- | ------------- | --------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| a.    | 1.1.2 | Survey report | SurveyRequest#<br>Surveydetails<br>Value                              | Survey report is received. Details incorporate written information fields only about the property, plus a survey value. OwnerName abbreviates (Forename, Surname).<br>CottageAddress abbreviates each line of an address. |
| 1.1.2 | M1    | Survey report | SurveyRequest#<br>Surveydetails<br>Value                              | Survey report is manually stored on receipt for reference.                                                                                                                                                                |
| M1    | 1.1.2 | Survey report | SurveyRequest#<br>Surveydetails<br>Value                              | Survey report is retrieved manually as reference for input request number                                                                                                                                                 |
| 1.1.3 | D1    | Survey        | SurveyRequest#                                                        | Survey request number from the Survey report is entered into the system.                                                                                                                                                  |
| D1    | 1.1.3 | Survey report | SurveyRequest#<br>CottageAddress<br>OwnerName                         | The system outputs cottage and owner details.                                                                                                                                                                             |
| M1    | 1.1.3 | Survey report | SurveyRequest#<br>Surveydetails<br>Value                              | Survey report is retrieved manually to check owner and property details. We are not told whether survey report at this point is transient data.                                                                           |
| 1.1.4 | D1    | Survey        | SurveyRequest#<br>OwnerName CottageAddress PriceCategory ReasonDetail | PriceCategory depends on Value  in survey report, determining acceptance, while RejectReason is varchar                                                                                                                   |


# 4.1.2 Dialogue Structure