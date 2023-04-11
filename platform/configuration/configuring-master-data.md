# Configuring Master Data

## **ADMIN ONLY**

Before the iFIX platform can be used, the master data must be configured directly into the respective collections in MongoDB. Associated APIs for configuring Master Data will be made available in the next version.&#x20;

* Add Government - Insert into MongoDB collection
* Add Department&#x20;
* Add Department Hierarchy - It defines the hierarchy definition for the department&#x20;
  * department id: It is master department id (UUID)
  * level: It defines the depth of hierarchy of department level&#x20;
    * Root level department hierarchy will not contain any parent value and level value will be zero
    * Level value incrementation rule:
      * When parent id is having any value then we search parent in department hierarchy record for hierarchy level evaluation
      * Get level value from parent department hierarchy and increment current department hierarchy level value by one
  * parent: It provides details about department parent (UUID)
* Add Department Entity - It contains department entity information along with its hierarchy level and also attaches master department information (department id - UUID). Here we keep all children information list at every department node (department record). Leaf level department will not have any children info. Children list contains department entity id list, which makes current department entity parent of all children list (department id list), that's how it maintains department entity level. Entities can be created by&#x20;
  * First defining the hierarchy level top to bottom because it has parent's reference
  * Then we can start adding department entities, bottom-to-top because it has child's reference.

**Note**:

* The root department hierarchy will have the label "Department", and the root department entity will be the department itself
* When we have to update the existing children list of Department Entity then update the existing children list using mongodb command like below:
  * Find the department entity parent where the new children need to be added. Do search by name and hierarchy level `db.departmentEntity.find({"name" : "<current_department_entity's_name>","hierarchyLevel": <Current_department_entity_hierarchy_level>});`
  * Append the department entity id at the end of the current department entity children's list. So first find the length of the current array and then set it as "children.n": "" (where n is the length of the array.)`db.departmentEntity.update({"_id": ""},{$set: {"children.n": "", "children.n+1": ""} })`
* Add Chart of Accounts - Insert manually into MongoDB collection
* Add Expenditure - Insert manually into MongoDB collection.

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
