# Home

Users are redirected to this screen after successful login.![](blob:https://digit-discuss.atlassian.net/cdc281ad-7766-457d-b7dc-e66837f96566#media-blob-url=true\&id=3bfe62d4-1653-4f5e-b3dd-709a01f7692a\&collection=contentId-1923416085\&contextId=1923416085\&mimeType=image%2Fpng\&name=Screenshot%202021-09-16%20at%205.56.04%20PM.png\&size=20588\&width=327\&height=576\&alt=)

This screen consists of multiple sections and user interactions.

If the user is mapped to multiple tenants then a dropdown appears. The user can select the desired tenant to proceed further.

Once the user selects the tenant, the features cards are displayed on the screen based on the roles mapped for the selected tenant.

## **Login For First Time**

YES → WalkThrough/User Guidance Enabled

NO → Home Screen

![](<../../../../.gitbook/assets/image (38).png>)

If the user logs in for the first time a system walkthrough begins automatically.

Else, users can view walkthroughs any time by clicking on the help icon.

### **Logic Implemented for Walkthrough**

![](<../../../../.gitbook/assets/image (96).png>)

Create a global key for each card.

Create placeholder cards, pointer and description widgets.

On click, the position of the card is determined and the placeholder card appears on the overlay exactly.

### **Files Path**

Primary Files

[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/HomeWalkThroughContainer.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/Home/HomeWalkThrough/HomeWalkThroughContainer.dart),

[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/Home/HomeWalkThrough/HomeWalkThroughList.dart)[punjab-mgramseva/HomeWalkThroughList.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/Home/HomeWalkThrough/HomeWalkThroughList.dart)

Next → Changes the active index of the global key and repeats the same process outlined in the implementation logic

skip, End → closes the overlay![](blob:https://digit-discuss.atlassian.net/89f22c1b-5a38-4e97-afa0-87a62a466c52#media-blob-url=true\&id=08bca3ac-fc32-4d3e-b09f-67937a509523\&collection=contentId-1923416085\&contextId=1923416085\&mimeType=image%2Fpng\&name=Screenshot%202021-09-20%20at%2011.39.48%20AM.png\&size=50244\&width=340\&height=606\&alt=)

Home Screen - consists of multiple feature cards

Cards are displayed based on Role Access

### **Files Path**

Primary Files[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/Home.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/Home/Home.dart)

The home screen also consists of notifications. The notifications are customized for each user ID and user role.

### **Logic Implemented for Notifications**

![](<../../../../.gitbook/assets/image (41).png>)

Individual API calls are made with the user ID and with the user role that merges both and notifications are displayed accordingly.

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
