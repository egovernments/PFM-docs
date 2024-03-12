# Features

## Filters on the Dashboard

**Date/Time Filter**&#x20;

The date & time filter on the dashboard defaults to the current financial year since most of the calculations and visualizations makes sense when viewed from a fiscal year perspective rather than an individual week/month view. However, users can change to respective dates and most charts will be filtered to the selected time range.

**Department Hierarchy Filter**

&#x20;Currently, there are 6 levels of hierarchy as per administration set up by the Department of Water supply and Sanitation Punjab. These are State, Zone, Circle, Division, Sub Division, Section, Gram Panchayat.

All these filters are independent and work on the dashboard irrespective of whether other filters in the hierarchy are selected or not.

## Visualization&#x20;

**Surplus/Deficit**&#x20;

This number shows whether the selected Administrative entity is financially surplus or not. It also compares with the previous year using the “trend” visualization in Metabase.

**Pending Collections**&#x20;

For selected Administrative boundary what is the pending collections through water charges is represented in this card. If the pending amount is null. Then this card should display zero.

**Outstanding Electricity Bills**

Since electricity bills create a major component of the expenditure for all projects, it is important to show how much electricity bills are pending at each administrative entity. The total amount of pending bills filtered by electricity under COA gives us pending electricity bills&#x20;

**GPWSCs at Risk**&#x20;

Risky GPWSCs are divided into 3 types

_High Risk_: Demand is less than Bill. Medium Risk: Demand is more than bill but pending collections is less than pending bills.&#x20;

_Low Risk_: Demand is more than bill and also pending collections is more than pending bills.

It is important to identify the risky GPWSCs and keep the officials of DWSS informed, for them to take the right actions before it’s too late.

**Collections & Expenditure Time Series Graphs**

These charts represent the Demand, Net Collections, Bills and Net Payments across time(month-on-month) so that officials get a fair idea of how the amount that is getting collected is being spent.

Any abnormalities in the graphs (Low collections or excessive spending) is something that needs to be paid attention to.

**Expenditure by Chart of Accounts**

Expenditure is currently divided into 4 broad categories - Electricity Bills, Salaries, Operations and Maintenance and Miscellaneous. How these 4 categories accumulate to total expenditure for the selected entity over time is presented on the chart. Usually, 75% of the expenditure should be of type electricity

**Department Hierarchy Table**&#x20;

Here, we represent Total Demand, Receipt, Bills and Payments by all levels of the hierarchy so that officials at any point, instead of just viewing the charts, trends from the visualizations can also see the tables and compare best performing entities.

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
