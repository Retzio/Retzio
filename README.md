<a id="Top"></a>

# Welcome! This is a little about me and a sample of my work. 

<hr>

## Table of Contents


* [About Me](#1)<br>
* [Samples of my work](#2)<br>
  * [OLTP Database](#2.1)<br>
  * [Python](#2.2)<br>
* [Resume](#3)<br>
    * [Skills](#3.1)<br>
    * [Sales Expierence](#3.2)<br>
    * [Education](#3.3)<br>
  
<br>
<hr>

# About Me<a id=1></a>

I plan to work in a career where I can combine my skills in sales, technical analysis, and operational execution to achieve differentiated results in sales and product development.

Happiness for me is found in the endless learning and growth attained by living a life of curiosity, abundance, alignment, and co-creation.

In my freetime I like to
* Ski 
* Play chess
* Hike
* Find new restaurants to eat at
* Experience new things and meet new people

<br>
<hr>

# Samples of my work<a id=2></a>
<hr>

## OLTP Database <a id=2.1></a>

### Description

This database that I built is for a mock company called Maple Estate Investments. The company is a real estate brokerage that specializes in growing and managing real estate portfolios for investors. There are a few things that make Maple Estate Investments so unique. To start, the company tracks the Multiple Listing Service (MLS) and off-market deals for any properties that have good capitalization rates and cash flow potential for investing. Maple Estate Investments also monitors investors' current portfolios, ensuring that all properties have good returns. If a home isn't performing well, an investor wants to diversify or grow their portfolio, Maple Estate Investments can conduct any transactions needed through the brokerage itself. The brokerage also tracks all current loans to factor in interest payments and amortization. If an investor qualifies for a better loan that is more aligned with their unique needs and goals, Maple Estates works heavily with loan officers to help them get the best possible loans. They meet with their investors regularly to discuss the current goals for their portfolio and the amount of risk/return they are willing to take. Maple Estate Investments uses foresight and planning to help their clients achieve their goals.

With all this information being recorded, stored, and analyzed, Maple Estate Investments needs a database. That is why I built Maple_Estate_Investments_Database. I've included a build script for the database as well as views, stored procedures, and user-defined functions in Microsoft SQL Server Management Studios. I also created forms and reports for the database in Microsoft Visual Studios to help track the database and add data entries as needed. Lastly, I created a dashboard for management to track ongoing sales and other important metrics in Power BI.


To see the full project including the build script, VB.Net forms, Power BI dashboard and more, see [Maple Estate Investments Database](https://github.com/Retzio/MapleEstateInvestments_Database).

<hr>

### Entity Relationship Diagram (ERD) for Database
To view the build script for Maples Estate Investments' Database, see [BuildMapleEstateInvestments](https://github.com/Retzio/MapleEstateInvestments_Database/blob/main/BuildMapleEstateInvestments.sql).


![ERD_MapleEstInv](https://user-images.githubusercontent.com/105741175/169920126-8e87ba49-6122-492a-b163-367658509f5b.png)



<hr>

### Microsoft Visual Studios VB.Net Forms and Reports 
The forms and reports were built in Microsoft Visual Studios. The forms were built on VB.Net framework to create a platform for the brokers to access the data and add any needed data entries. The reports were created for the brokers to monitor data that is constantly being updated such as the MLS or loan rates for the investors. To view a more in-depth explanation of each of the reports and download the solutions files for Visual Studios, see 
[VS_Forms_Reports_MapleEstateInvestments](https://github.com/Retzio/MapleEstateInvestments_Database/tree/main/VS_Forms_Reports_MapleEstateInvestments).
<br>(Unmute for narration)<br>

https://user-images.githubusercontent.com/105741175/169918503-df8368cc-5ce4-4b94-aabc-191b5b193e67.mp4


<hr>



### Power BI Dashboard
The dashboard for Maple Estate Investments' database was built in Power BI and was created for management to view inportant metrics such as sales.
To view the dashboard, see
[Maple Estate Investments Dashboard](https://app.powerbi.com/groups/me/reports/633b699c-1f4e-4fe1-9f3f-7b3509f47883/ReportSection?ctid=6f3c7037-85c2-40e6-9dec-18b02d289288).
To download the .pbix, see 
[PowerBI_Dashboard_MapleEstateInvestments](https://github.com/Retzio/MapleEstateInvestments_Database/tree/main/PowerBI_Dashboard_MapleEstateInvestments).


![PowerBI](https://user-images.githubusercontent.com/105741175/169918711-7b4952f0-0b93-4636-9632-166fb0b41d6e.png)


<hr>
<br>

##### [Back to Top](#Top)
<hr>



## Python<a id=2.2></a>
### Python GLPK Solver

I created a DraftKings NHL fantasy lineup using GLPK Solver. For the DraftKings NHL fatasy lineup contest a set of constrainst is given to build a fantasy team. To view all the rules, points, and contraints, see [DraftKings](https://www.draftkings.com/help/rules/3). Using GLPK I created the best possible team based each player's current season statistics. Because this was just for fun and based on a contest that had already happened, I created a second lineup for what the best possible team would have been based on the games for the contest. The results for the predicted and actual optimal lineup can be seen below.

To view the full project, see [DraftKings_Fantasy_NHL_Team](https://github.com/Retzio/DraftKings_Fantasy_NHL_Team).

<details>
  <summary><b><i>Click here</i> to see the code for the constraints.</b></summary>
 
```python
#Budget Constraint
model.cons_budget = pe.Constraint(expr = sum([skater_points.loc[idx, 'Salary']*model.skater[idx] 
                                             for idx in DV_Index]) <= 50000)
#Total of 9 Players Constraint
model.cons_size = pe.Constraint(expr = sum(model.skater[idx] for idx in DV_Index) == 9)

# Center Constraint
model.cons_center = pe.Constraint(expr = sum([skater_pos.loc[idx, 'C'] * model.skater[idx] 
                                             for idx in DV_Index]) >= 2)

# Wing Constraint
model.cons_wing = pe.Constraint(expr = sum([skater_pos.loc[idx, 'W'] * model.skater[idx] 
                                             for idx in DV_Index]) >= 3)

# Defence Constraint
model.cons_defence = pe.Constraint(expr = sum([skater_pos.loc[idx, 'D'] * model.skater[idx] 
                                             for idx in DV_Index]) >= 2)

# Goalie Constraint
model.cons_goalie = pe.Constraint(expr = sum([skater_pos.loc[idx, 'G'] * model.skater[idx] 
                                             for idx in DV_Index]) == 1)
    
    
#Team Constraints 3 or more teams
     
def team_rule(_, t):
    return sum([skater_team.loc[idx, t] * model.skater[idx] for idx in DV_Index]) >= model.teams[t]

def team(_):
    return sum([model.teams[i] for i in DV_team_index]) >=3

model.team_cons = pe.Constraint(model.team_set, rule = team_rule)

```
</details>
 
<table>
  <tr>
    <th><b>Predicted Optimal Lineup</b></th>
    <th><b>Actual Optimal Lineup Based On the Games</b></th>
  </tr>
  <tr>
    <td><img src= "https://user-images.githubusercontent.com/105741175/169449698-fd577d19-55e8-4cb1-aaeb-0644400676e9.png" height="auto" width="auto"></td>
    <td><img src= "https://user-images.githubusercontent.com/105741175/169449718-e184437b-9219-42f2-a51a-65eb48a9a59c.png" height="auto" width="auto"></td>
  </tr>
  <tr>
</table>
  



<hr>
<br>

##### [Back to Top](#Top)
<hr>



# Resume <a id=3></a>
For a copy of my resume, see
[Resume](https://github.com/Retzio/Resume/blob/main/Retzio_Gredig-Resume.pdf).

<hr>

## Skills <a id=3.1></a>


<table>
  <tr>
    <th>Coding Languages</th>
    <th>Micrsoft Office Specialist Certifications</th>
  </tr>
  <tr>
   <td valign="top">
     <ul>
        <li>SQL</li>
        <li>Python</li>
        <li>R</li>
        <li>VBA</li>
        <li>VB.Net</li>
      </ul>
    </td>
   <td valign="top">
     <ul>
        <li>Access</li>
        <li>Excel</li>
        <li>PowerPoint</li>
        <li>Word</li>  
      </ul>
    </td>
  </tr>
  <tr>
    <th>Tools</th>
    <th>Data Anlysis and Presntation</th>
 </tr>
 <tr>
   <td valign="top">
     <ul>
        <li>Microsoft SQL Server Management Studio</li>
        <li>Microsoft Visual Studio</li>
        <li>Tableau</li>
        <li>Power BI</li>
        <li>SPSS Modeler</li>
        <li>JMP</li>
     </ul>
   </td>
   <td>
     <ul>
        <li>Inferential statistics</li>
        <li>Prediction</li>
        <li>Segmentation</li>
        <li>Classification</li>
        <li>Text analytics</li>
        <li>Analytic visualization</li>
        <li>Data storytelling</li>
        <li>Business-technical interpretation and translation</li>
     </ul>
   </td>
 </tr>
</table>

<hr>

## Sales Expierence<a id=3.2></a>

#### Clear home December 2020 ??? Present

<div dir="lft">Market Development and Sales Training Specialist: Contracted by Amazon <div dir="rtl"> London, England </div>

* Conducted R&D and Piloted Amazon???s expansion of the Key for Business program into England
* Co-created sales processes and training material while also recruiting and training local sales representatives
* Presented Amazon???s Key for Business technology to property management teams, board members, and councils
* Piloted the England expansion and establish 10% of the annual new accounts in two months

##

<div dir="lft"> Territory Sales Manager: Contracted by Amazon <div dir="rtl"> Phoenix, Arizona </div>

* Grew and managed a team of 8 people, developing personal and sales skills
* Developed leadership and sales influence skills, learned how to effectively recruit, hire, and train employees
* Led a team that sold 33,597 units with 279 commercial B2B accounts, and placed 2nd for quarter 3 of 2021

##

<div dir="lft"> Sales Specialist for Contract Negotiations: Contracted by Door Dash <div dir="rtl"> Los Angeles, California </div>

* As a top performer, was chosen to demo our team???s sales volume for Door Dash during contract negotiation
* Worked with small business owners to onboard them to Door Dash

##

<div dir="lft"> Outside Sales Representative: Contracted by Amazon <div dir="rtl"> Denver, Colorado </div>

* Expanded my client acquisition and retention skills in B2B by conducting the full sales cycle for multiple accounts
at a time with Amazon???s Key for Business, an IoT solution for residential real estate developments
* Sold 16,826 units with 156 B2B accounts, placing 3rd in the company for quarter 3 and 18th for the 2021 year
* Utilized a combination of my skills in data and sales to generate more efficient and effective lead generation
strategies, which reduced time spent by 60% and increased conversion rates by 25%
##
#### Caliber Smart June 2020 ??? September 2020

<div dir="lft"> D2D Sales Representative: Contracted by Dish Network and T-Mobile <div dir="rtl"> Nashville, Tennessee </div>

* Sold 106 accounts in 3 months and achieved highest completion rate of 87% in the office
* Achieved top rookie status both locally and nationally
* Mastered pitching, tonality, and subtle sales techniques through the rawest form of sales

<hr>
 
## Education<a id=3.3></a>
#### University of Denver, Daniels College of Business
Bachelor of Science Business Administration ??? Business Information and Analytics, June 2022

<hr>

##### [Back to Top](#Top)









