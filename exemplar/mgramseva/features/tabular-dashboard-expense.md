# Tabular Dashboard - Expense

Clicking on the Dashboard on the home screen takes the user directly to the revenue dashboard of the current month. From here, the user can switch to the expenditure tab to get a view of expenses. This provides a tabular view of all expenses incurred in that month.

![](<../../../.gitbook/assets/image (13).png>)

Following are the data points/actions needed on the screen

| [**S.No**](http://s.no) | **Item**             | **Explanation**                                                                                                                                                                                                                                                                                                                                                                                         |
| ----------------------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1                       | Search Expense Bills | <ul><li>Search by Bill ID or Vendor</li><li>The Vendor Name should be a partial match. As the user starts typing a consumer name, respective vendors get filtered in the table displayed below</li><li>Bill ID should be a partial match. As the user starts typing a New Bill ID, respective Bills should get filtered in the table displayed below</li></ul>                                          |
| 1.1                     | Filters              | <ul><li>Default is “All” View. Switching to Paid or Pending filters the table accordingly. Alongside the filter, how many Bills fall into that filter is shown in numbers</li><li>The table also has sort options for each column (ascending, descending)</li></ul>                                                                                                                                     |
| 1.2                     | Columns              | <ul><li><p>Bill ID - Vendor Name</p><ul><li>Bill ID is assigned to each bill while creating an expense entry record</li><li>Sort happens on the Bill ID</li></ul></li><li><p>Expense Type</p><ul><li>Under which expense head the bill is tagged to</li></ul></li><li>Amount</li><li>Bill Date</li><li><p>Paid Date</p><ul><li>If Bill is not paid, this should show pending in RED</li></ul></li></ul> |

The table on the screen is a horizontal scrollable one with the left-most column fixed.

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
