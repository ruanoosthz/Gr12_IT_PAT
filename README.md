# IT PAT 2024
### ~ Ruan Oosthuizen

## Table of Contents

- [Scenario & Scope](#scenario--scope)
- [User Requirements](#user-requirements)
- [Database Design](#database-design)
- [Data Dictionary](#data-dictionary)
- [Text File](#text-file)
- [Array (2 dimensional)](#array-2-dimensional)
- [Navigation/ Flow Diagram](#navigation-flow-diagram)
- [Graphical User Interface Design](#graphical-user-interface-design)
- [IPO](#ipo)
  - [Screen 6: Property Edit](#screen-6-property-edit)
  - [Screen 2: Property Search](#screen-2-property-search)


## Scenario & Scope

The topic that I have chosen for the PAT: A house listing program for a real estate agent business, where external users can also see listings.
A real estate agent business has asked me to design a program that all the agents in the business can use to see and upload all listings with their relevant information and calculate bonds. The specifications of the program: 

Create a property listing containing all the relevant specifications of the property (price, rooms, photos, etc.), the owner of the property’s information (ID, name, surname, e-mail, etc. 
A bond calculator must also be a feature. It calculates the monthly repayment. There must be an option for 10, 20 and 30 years.
There must also be a feature to view listings in more detail. Every agent can upload their property listing.

The program will serve as the companion this business needs, simplifying their admin processes and boosting their efficiency as partners. 

Disclaimer: This PAT does not aim to have an optimal security system. 


## User Requirements

| Tables        | User 1: General User           | User 2: Agent  |
| ------------- | ------------- | ----- |
| Role      | The general users will onlybe able to browse listings.  | The administrator will manage all listings added to the system.|
| Activity        |Can search for specific listings and see their details. They can do bond calculations.	| They have full access to the functionalities of the program. They can add, edit or remove listings from the system. ||
| They cannot Interact with the listings. They do not have access to the agent dashboard.| are neat      |   None. |


## Database Design

### tblProperty

|	| Field Name       | Data Type | Field Size |
|:-----:| ------------- |-------------| -----|
|PK	| ID      | Auto Number |Long Integer |
|	| PropPrice    | Number       |  Integer |
|FK	| PropType |  Number  |  Long Integer|
| |ErfSize |Number |Integer |
| | ParkingSpace|Number | Integer|
| |Bedrooms | Number| Integer|
| | Bathrooms|Number | Integer|
|FK |Province |Number |Long Integer |
| | Suburb| Short Text|30 |
| | Adress| Short Text|30 |


### tblProvince

| | Field Name        | Data Type          | Field Size |
| --- | ------------- |:-------------:| -----:|
|PK| ID     | Auto Number | Long Integer|
|FK| Province      | Short Text    |  30 |


### tblPropertyType

| | Field Name        | Data Type          | Field Size |
| --- | ------------- |:-------------:| -----:|
|PK| ID     | Auto Number | Long Integer|
| | PropertyType      | String    |  20 |


 
## Data Dictionary

| ** Classes and Objects ** |
| --- |
|TUser|
|Attributes|
|- fUsername : String;|
|- fIsAgent: Boolean|

| ** Methods ** |
| --- |
|+ Constructor Create( parameters : pName : String; pIsAgent : Boolean);|
|+ property Username : String read fUsername write fUsername; |
|( These properties allow for easy access setting or)|
|+ property IsAgent : Boolean read fIsAgent write fIsAgent;|   
|( getting the User's Username and IsAgent status)|

'-' = private 
'+' = public


## Text File
It displays an example of the registered agents and their passwords.
<img width="638" height="412" alt="image" src="https://github.com/user-attachments/assets/7318c363-e267-4b16-9f56-12e115e237f4" />

 
 
## Array (2 dimensional)

A parallel array will be used to store the data from the previously displayed text file.

### Example of array data: arrName
|1	|2	|3	|4 	|5|
| :---:	| :---:	| :---:	| :---:	| :---: |
|admin  |	John Smith|	Jane Doe|	Michael Johnson|	Emily Davis|

### Example of array data where it is not encrypted: arrPass
|1	|2	|3	|4 	|5|
| :---:	| :---:	| :---:	| :---:	| :---: |
|admin|	Password123!|	SecurePass456@|	Welcome789#|	StrongPass101$|
 
 
## Navigation/ Flow Diagram

<img width="713" height="721" alt="image" src="https://github.com/user-attachments/assets/a0bf2a08-f035-4af9-b418-dda2c1342eab" />



 
## Graphical User Interface Design

## Screen 1: Welcome Page

<img width="719" height="556" alt="image" src="https://github.com/user-attachments/assets/6eb63a13-426a-441f-b1d7-42375047a2ea" />


## Screen 2: Login Page (Agent)

<img width="718" height="559" alt="image" src="https://github.com/user-attachments/assets/79de3a14-f1f5-4e1e-a24e-efaabb6da0d9" />


## Screen 3: Agent Dashboard (Agent)

<img width="769" height="597" alt="image" src="https://github.com/user-attachments/assets/435b9279-9af3-4dde-ab95-1d66a79002ad" />


## Screen 4: Property Search

<img width="772" height="594" alt="image" src="https://github.com/user-attachments/assets/765f71c0-a01d-496b-bdff-da53deb51f1e" />


## Screen 5: Property Details

<img width="791" height="616" alt="image" src="https://github.com/user-attachments/assets/c5fecf29-ce35-45af-b097-ddf8aa793502" />


## Screen 6: Property Edit (Agent)
  
<img width="848" height="659" alt="image" src="https://github.com/user-attachments/assets/f5f09e4c-03fe-4b22-bfe2-4c628b1e4c56" />



## IPO

---

# Screen 6: Property Edit

## Input

| Input | Source | Data Type | Format | GUI Component | Validation |
|------|--------|-----------|--------|--------------|------------|
| iErfSize | Mouse Button / Keyboard | Integer | Number | edtErfSize | Check that value is not zero. Show message: "Invalid erf size" |
| iPropertyPrice | Keyboard | Integer | Number | edtPrice | Check that a valid number is entered (not empty or letters). Show message: "Enter a valid price." |
| sAddress | Keyboard | String | Text | edtAddress | Check that an address is entered (not empty). Show message: "Enter an address." |
| iPropType | Mouse Button | Index | Number | cmbType | Check that a property type is selected. Show message: "Select a Prop Type." |

---

## Processing

| What processing needs to be done | How processing will be done |
|----------------------------------|------------------------------|
| 1. Load Existing Property Details | Load data from the database into form fields using LoadExistingPropertyDetails method. |
| 2. Validate Property Price | Ensure edtPrice contains a valid integer using TryStrToInt. If invalid, show message and exit. |
| 3. Validate Suburb Field | Check if edtSuburb is filled. If empty, show error message and exit. |
| 4. Validate Address Field | Check if edtAddress is filled. If empty, show error message and exit. |
| 5. Set Province | Ensure a province is selected from cmbProvince. If not, show error and exit. |
| 6. Set Property Type | Ensure a property type is selected from cmbType. If not, show error and exit. |
| 7. Save Property Data | Save property data to database depending on insert/edit mode. |
| 8. Refresh Database and Update Grid Display | Refresh dataset and update frmAgentDash grid display. |

---

### Pseudo Code / Example Algorithms

#### 2. Validate Property Price
Pseudo Code:
```
if TryStrToInt(edtPrice.Text, iInteger) is False then
    Show error message "Please enter a valid price"
    Exit procedure
```

#### 3. Validate Suburb Field
Pseudo Code:
```
if Trim(edtSuburb.Text) is empty then
    Show error message "Please enter a suburb"
    Exit procedure
```

#### 5. Set Province
Pseudo Code:
```
if cmbProvince.ItemIndex is less than or equal to 0 then
    Show error message "Please select a province"
    Exit procedure
else
    Set province to the selected index value from cmbProvince
```

#### 6. Refresh Database and Update Grid Display
Example Code:
``` pascal
dmData.ExecQry('SELECT tblProperty.ID, FORMAT(PropPrice, "CURRENCY") AS PropertyPrice, ' +
               'Suburb, Address, tblPropType.PropertyType FROM tblProperty LEFT JOIN ' +
               'tblPropType ON tblProperty.PropertyType = tblPropType.ID');
```
``` pascal
with frmAgentDash do
begin
  dbgProp.Columns[0].Width := 30;
  dbgProp.Columns[1].Width := 150;
  dbgProp.Columns[2].Width := 150;
  dbgProp.Columns[3].Width := 180;
  dbgProp.Columns[4].Width := 220;
end;
```


---

## Output

| Data | Format | GUI Component |
|------|--------|--------------|
| Property Price | Price: <Price in integer format> | edtPrice: TEdit, dbgProp: TDBGrid |
| Parking Spaces | Parking Spaces: <Number of parking spaces> | sedPark: TSpinEdit |
| Erf Size | Erf Size: <Size in square meters> | sedErf: TSpinEdit |
| Province | Province: <Selected province name> | cmbProvince: TComboBox, dbgProp: TDBGrid |
| Property Type | Property Type: <Type of property> | cmbType: TComboBox, dbgProp: TDBGrid |

---

# Screen 2: Property Search

## Input

| Input | Source | Data Type | Format | GUI Component | Validation |
|------|--------|-----------|--------|--------------|------------|
| rPrice | Keyboard | Real | Decimal | edtPrice | Check valid number. If empty, filter not applied. Show message if invalid. |
| iProvince | Mouse Button | Index | Number | cmbProvince | If index = 0, filter not applied. |
| iRooms | Mouse Button | Integer | Number | sedRooms | If value not selected, filter not applied. |
| sSymbol | Mouse Button | String | String | cmbSymbol | If price entered, symbol must be selected. |

---

## Processing

| What processing needs to be done | How processing will be done |
|----------------------------------|------------------------------|
| 1. Load Listings Data | Execute SQL query on form activation using dmData.ExecQry. |
| 2. Validate Price Filter | Check if edtPrice contains valid number. If invalid, show message and exit. |
| 3. Set Province Filter | Apply province filter only if selected. |
| 4. Set Bedrooms Filter | Apply bedrooms filter if value > 0. |
| 5. Filter Listings | Apply filters in SQL query and display results in dbgSearch. |
| 6. Delete Listing | Delete selected listing after confirmation. |
| 7. View Detailed Property | Show details using ShowListingDetail. |
| 8. Add or Edit Property | Open property edit form using ShowPropEdit. |

---

### Pseudo Code / Example Algorithms

#### 2. Validate Price Filter
Pseudo Code:
```
if edtPrice.Text is empty then
    sPrice := 'No price filter'
else if edtPrice.Text is a valid float number then
    Set sPrice to the entered value
else
    Show error message "Please enter a valid property price"
    Exit procedure
```
________________________________________
#### 3. Set Province Filter
Pseudo Code:
```
if cmbProvince.ItemIndex <= 0 then
    Set sProvince to 'No province filter'
else
    Set sProvince to 'Province = selected province value'
```
________________________________________
#### 5. Filter Listings by User Input
Example Code:
``` pascal
dmDAta.ExecQry('SELECT tblProperty.ID, FORMAT(PropPrice, "CURRENCY") AS PropertyPrice, ' +
               'Suburb, Address, tblPropType.PropertyType FROM tblProperty LEFT JOIN ' +
               'tblPropType ON tblProperty.PropertyType = tblPropType.ID ' +
               'WHERE ' + sProvince + ' AND ' + sSuburb + ' AND ' + sRoom + ' AND ' + sPrice);
```
________________________________________



#### 7. View Detailed Property Information
``` pascal
Example Code:
PropertyID := dbgSearch.DataSource.DataSet.FieldByName('ID').AsInteger;
ShowListingDetail(PropertyID);
```


---

## Output

| Data | Format | GUI Component |
|------|--------|--------------|
| Property Price | Property Price: <Price in currency format> | dbgSearch: TDBGrid, edtPrice |
| Bedrooms | Bedrooms: <Number of bedrooms> | dbgSearch: TDBGrid, sedBedroom |
| Bathrooms | Bathrooms: <Number of bathrooms> | sedBath: TSpinEdit |
| Property Type | Property Type: <Type of property> | cmbType: TComboBox, dbgSearch |
| Province | Province: <Selected province name> | cmbProvince: TComboBox, dbgSearch |
