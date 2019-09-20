## Prepare PyCon JP 2019 with Python
#### PyCon JP 2019 LT
#### 2019/09/20 nikkie

---

### self-introduction / お前、誰よ

- nicknamed 'nikkie' （@fab[twitter] [@ftnext](https://twitter.com/ftnext)）
- came to PyCon TW 2019 from Japan
- engaged in [Django Girls Tutorial translation](https://tutorial.djangogirls.org/ja/)🇯🇵 & workshop coach
- PyCon JP 2019 staff, a member of program committee

Note:

please call me nikkie.
I'm from Japan.
I'm engaged Django Girls Tutorial translation & workshop coach.
and I'm PyCon JP 2019 staff. a member of program committee

+++

### PyCon JP (from 14th Sep. to 17th)

![PyCon JP logo](pycontw_lt_staff_python/assets/square_color.png)

Note:

As you already know(笑), PyCon JP 2019 was held from 14th September Saturday to 17th Tuesday.
is there anyone went to PyCon JP?
oh, many people!
I am happy if they had a fruitful time at PyCon JP.

+++

### For PyCon TW staffs

- This is my first PyCon TW
- This is my first time abroad
- I really enjoy PyCon TW 2019😆, so I appreciate all staffs

Note:

I really enjoy PyCon TW 2019, so I appreciate all staffs.
Thank you!

+++

### Python is a staff, too!

![a screenshot of PyCon TW site (created with Django)](pycontw_lt_staff_python/assets/pycontw_django_site.png)

https://github.com/pycontw/pycon.tw

Note:

and Python is a member of PyCon TW staffs!
For example, the site of PyCon TW 2019 made by Django

+++

### Python as a staff of PyCon JP

- Python worked hard in preparation of PyCon JP 2019.
- In this LT, I will share you **how Python supported PyCon JP**.

+++

### Contents

- *Introduction* <- NOW!!
- Situation
- Solution

Note:

now introduction ended.
next I will tell you about situation & solution

---

### Contents

- Introduction
- **Situation**
- Solution

+++

### What Python did

- Python supported application🈸 of developer's sprint
- Python was commited to publishing sprint themes

+++

### Our tool: connpass

![connpass page of sprint](pycontw_lt_staff_python/assets/sprint_connpass_page.png)

https://pyconjp.connpass.com/event/136558/

+++

### connpass is

- a web application by Be Proud inc. to manage applications of an event
- **free** to use
- in Japan, used in many events about IT (not only Python events, other language event)

+++

### Questionnaire form

![image of a questionnaire form](pycontw_lt_staff_python/assets/connpass_questionnaire.png)

Note:

in connpass, we can create a questionnaire form.
Participants will submit the questionnaire in applying the event

+++

### Requirements

- there are two types of participants: attendees and leaders
- we want **leaders** to **submit information** about their projects

Note:

In PyCon JP 2019 sprint, there are two types of participants: attendees and leaders
we want leaders to submit information about their projects

+++

### Issues

- Only staffs can see answers of the questionnaire form
- we want to publish a page so that **all the attendees can see themes**
- we want to **update** the page **regularly**

+++

## Automate this regularly stuff with Python

---

### Contents

- Introduction
- Situation
- **Solution**

+++

## Solve the issues

- Only staffs can see answers 👉 **download** answers as a CSV file
- we want to publish a page 👉 Google spreadsheet (share with **people who knows the link**)
- we want to update** regularly 👉 create **Python script**

+++

### How work the script

1. open the CSV file (already downloaded)
2. select rows of leaders (**not including attendees**)
3. select columns, only sprint theme information, **not including e-mail addresses** etc.
4. upload selected data via **Sheets API**

+++

### used packages

- google-api-python-client 1.7.10
- google-auth 1.6.3

Source code: @fab[github] https://github.com/ftnext/pyconjp2019.sprint.theme.update

Note:

I used two packages, google-api-python-client & google-auth

+++

### Solution

In my PC💻

1. download answers
2. kick the script

[The spreadsheet](https://docs.google.com/spreadsheets/d/1SNQsUUar-TD5AHfdDxupgjpdmvBF6Ao_wQ_lf5kJFjo/edit#gid=0)

+++

# Demo

answers is already downloaded

+++

### Operation

On Saturday morning 🐓

![slack reminder for nikkie](pycontw_lt_staff_python/assets/slack_reminder_operation.png)

Note:

Slack reminder says "hey nikkie! please kick the script"

---

### Summary: Prepare PyCon JP 2019 with Python

- I shared how Python worked in preparation of PyCon JP 2019 developer sprint
- select data from answers (CSV file) and upload to Google spreadsheet

+++

### Future works

- I think Python can do more as a PyCon JP staff💪
- Idea: Django apps for program committee
  - @fab[github] https://github.com/ftnext/pyconjp2020.proposal.management

Note:

I am going to develop with Django to help program committee manage proposals and create timetable, referencing sites of PyCon TW and other region

+++

I want to talk PyCon staffs about how they use Python in preparation of PyCon💖

### Thank you for your attention!
