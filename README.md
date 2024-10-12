IT PAT 2024 – Phase 1
~ Ruan Oosthuizen
























Table of Contents
IT PAT 2024 – Phase 1	1
Scenario & Scope	3
User Requirements	4
Database Design	5
Data Dictionary	7
Classes and Objects	7
Text File	7
Array (2 dimensional)	8
Navigation/ Flow Diagram	9
Graphical User Interface Design	10
IPO	13
Screen 6: Property Edit	13
Screen 2: Property Search	17












Scenario & Scope

The topic that I have chosen for the PAT: A house listing program for a real estate agent business, where external users can also see listings.
A real estate agent business has asked me to design a program that all the agents in the business can use to see and upload all listings with their relevant information and calculate bonds. The specifications of the program: 

Create a property listing containing all the relevant specifications of the property (price, rooms, photos, etc.), the owner of the property’s information (ID, name, surname, e-mail, etc. 
A bond calculator must also be a feature. It calculates the monthly repayment. There must be an option for 10, 20 and 30 years.
There must also be a feature to view listings in more detail. Every agent can upload their property listing.

The program will serve as the companion this business needs, simplifying their admin processes and boosting their efficiency as partners. 

Disclaimer: This PAT does not aim to have an optimal security system. 
User Requirements

	User 1: General User	User 2: Agent
Role	The general users will only be able to browse listings.	The administrator will manage all listings added to the system.
Activity	Can search for specific listings and see their details. They can do bond calculations.	They have full access to the functionalities of the program. They can add, edit or remove listings from the system. 
Limitations	They cannot Interact with the listings. They do not have access to the agent dashboard.	None.








Database Design

tblProperty
	Field Name	Data Type	Field Size
PK	ID	Auto Number	Long Integer
	PropPrice	Number	Integer
FK	PropType	Number	Long Integer
	ErfSize	Number	Integer
	ParkingSpace	Number	Integer
	Bedrooms	Number	Integer
	Bathrooms	Number	Integer
FK	Province	Number	Long Integer
	Suburb	Short Text	30
	Adress	Short Text	30







tblProvince
	Field Name	Data Type	Field Size
PK	ID	Auto Number	Long Integer
FK	Province	Short Text	30


tblPropertyType
	Field Name	Data Type	Field Size
PK	ID	Auto Number	Long Integer
	PropertyType	String	20


 
 
Data Dictionary

Classes and Objects
TUser
Attributes
- fUsername : String;
- fIsAgent: Boolean
Methods
+ Constructor Create( parameters : pName : String; pIsAgent : Boolean);
+ property Username : String read fUsername write fUsername; 
( These properties allow for easy access setting or)
+ property IsAgent : Boolean read fIsAgent write fIsAgent;   
( getting the User's Username and IsAgent status)

- = private 
+ = public


Text File
It displays an example of the registered agents and their passwords.

 
 
Array (2 dimensional)

A parallel array will be used to store the data from the previously displayed text file.
Example of array data: arrName
1	2	3	4	5
admin	John Smith	Jane Doe	Michael Johnson	Emily Davis

Example of array data where it is not encrypted: arrPass
1	2	3	4	5
admin	Password123!	SecurePass456@	Welcome789#	StrongPass101$
 
 
Navigation/ Flow Diagram























 
Graphical User Interface Design

Screen 1: Welcome Page
 

Screen 2: Login Page (Agent)
 

Screen 3: Agent Dashboard (Agent)
 

Screen 4: Property Search
 


Screen 5: Property Details
 

Screen 6: Property Edit (Agent)
  
 
IPO

Screen 6: Property Edit
Input
Input	Source	Data Type	Format	GUI Component	Validation
iErfSize	Mouse Button/ Keyboard	Integer	Number	edtErfSize	There will be checked if the input is not zero.
…
Dialogs.MessageDlg(‘Invalid erf size', mtError,[mbOk], 0, mbOk);
rPropertyPrice	Keyboard
	Real	Number	edtPrice	There will be checked if a Number is entered(Not empty or letters)
…
Dialogs.MessageDlg(‘Enter a valid price.', mtError,[mbOk], 0, mbOk);
sAddress	Keyboard	String	Text	edtAddress	There will be checked that an address is entered. (not nul)
..
Dialogs.MessageDlg(‘Enter an owner name.', mtError,[mbOk], 0, mbOk);
iPropType	Mouse Button	Index	Number	cmbPropType	There will be checked that a Property type is selected.
..
Dialogs.MessageDlg(‘Select a Prop Type.', mtError,[mbOk], 0, mbOk);

Processing
What processing needs to be done	How processing will be done
1. Load Existing Property Details	Load data from the database into the form fields (Price, Suburb, Bedrooms, etc.) using the LoadExistingPropertyDetails method.
2. Validate Property Price	Ensure the input in the edtPrice field is a valid integer using TryStrToInt. If invalid, show a message and exit.
3. Validate Suburb Field	Check if the edtSuburb field is filled. If it's empty, show an error message and exit the procedure.
4. Validate Address Field	Check if the edtAddress field is filled. If it's empty, show an error message and exit the procedure.
5. Set Province	Validate that a province is selected from cmbProvince. If no selection is made, show an error message and exit.
6. Set Property Type	Validate that a property type is selected from cmbType. If no selection is made, show an error message and exit.
7. Save Property Data	Depending on the mode (insert/edit), save the property data to the database and update the respective fields.
8. Refresh Database and Update Grid Display	Refresh the dataset after saving to ensure the latest information is displayed in the grid (frmAgentDash).




 
Pseudo code / Example algorithms for four of these processes:
________________________________________
2. Validate Property Price
Pseudo Code:
if TryStrToInt(edtPrice.Text, iInteger) is False then
    Show error message "Please enter a valid price"
    Exit procedure

3. Validate Suburb Field
Pseudo Code:
if Trim(edtSuburb.Text) is empty then
    Show error message "Please enter a suburb"
    Exit procedure

5. Set Province
Pseudo Code:
if cmbProvince.ItemIndex is less than or equal to 0 then
    Show error message "Please select a province"
    Exit procedure
else
    Set province to the selected index value from cmbProvince








6. Refresh Database and Update Grid Display
Example Code:
dmData.ExecQry('SELECT tblProperty.ID, FORMAT(PropPrice, "CURRENCY") AS PropertyPrice, ' +
               'Suburb, Address, tblPropType.PropertyType FROM tblProperty LEFT JOIN ' +
               'tblPropType ON tblProperty.PropertyType = tblPropType.ID');

with frmAgentDash do
begin
  dbgProp.Columns[0].Width := 30;
  dbgProp.Columns[1].Width := 150;
  dbgProp.Columns[2].Width := 150;
  dbgProp.Columns[3].Width := 180;
  dbgProp.Columns[4].Width := 220;
end;


Output
Data	Format	GUI Component
Property Price	Price: <Price in integer format>	edtPrice: TEdit, dbgProp: TDBGrid
Parking Spaces	Parking Spaces: <Number of parking spaces>	sedPark: TSpinEdit
Erf Size	rf Size: <Size of erf in square meters>	sedErf: TSpinEdit
Province	Province: <Selected province name>	cmbProvince: TComboBox, dbgProp: TDBGrid
Property Type	Property Type: <Type of property>	cmbType: TComboBox, dbgProp: TDBGrid





 
Screen 2: Property Search
Input
Input	Source	Data Type	Format	GUI Component	Validation
rPrice	Keyboard	Real	Decimal	edtPrice.text	There will be checked if a Number is entered(Not empty or letters) If nothing is entered the filter will not be applied
…
Dialogs.MessageDlg(‘Enter a valid price.', mtError,[mbOk], 0, mbOk);
iProvince	Mouse Button	Index	Number	cmbProvince	There will be checked that a Province is chosen(if Index 0 then filter will not be applied).
iRooms	Mouse Button	Integer	Number	sedRooms	There will be checked if a value is selected, if not, filter will not be applied
sSymbol	Mouse Button	String	String	cmbSymbol	There will be checked that a Symbol is chosen(if Index 0 then filter will not be applied).
If price is entered
…
Dialogs.MessageDlg(‘Choose a symbol', mtError,[mbOk], 0, mbOk);



Processing
What processing needs to be done	How processing will be done
1. Load Listings Data on Form Activation	On form activation, the SQL query will be executed to load property listings into the grid using dmData.ExecQry.
2. Validate Price Filter	Check if a valid number is entered in the edtPrice field. If invalid, show a message and exit the filter procedure.
3. Set Province Filter	Check if a province is selected from cmbProvince. If not, no filter will be applied for the province.
4. Set Bedrooms Filter	Check the value of the sedBedroom control. If 0, no filter will be applied; otherwise, filter by number of bedrooms.
5. Filter Listings by User Input	Apply the filters for price, bedrooms, suburb, and province in the SQL query and display the filtered data in dbgSearch.
6. Delete a Listing	If the user confirms, the currently selected listing will be deleted from the database using dmData.tblProp.Delete.
7. View Detailed Property Information	On clicking "View", the detailed information of the selected property is shown in a new form using ShowListingDetail.
8. Add or Edit a Property	Depending on the mode (add or edit), the form for property details will open with ShowPropEdit to either create or edit.






 
Pseudo code / Example algorithms for four of these processes:
________________________________________
2. Validate Price Filter
Pseudo Code:
if edtPrice.Text is empty then
    sPrice := 'No price filter'
else if edtPrice.Text is a valid float number then
    Set sPrice to the entered value
else
    Show error message "Please enter a valid property price"
    Exit procedure
________________________________________
3. Set Province Filter
Pseudo Code:
if cmbProvince.ItemIndex <= 0 then
    Set sProvince to 'No province filter'
else
    Set sProvince to 'Province = selected province value'
________________________________________
5. Filter Listings by User Input
Example Code:
dmDAta.ExecQry('SELECT tblProperty.ID, FORMAT(PropPrice, "CURRENCY") AS PropertyPrice, ' +
               'Suburb, Address, tblPropType.PropertyType FROM tblProperty LEFT JOIN ' +
               'tblPropType ON tblProperty.PropertyType = tblPropType.ID ' +
               'WHERE ' + sProvince + ' AND ' + sSuburb + ' AND ' + sRoom + ' AND ' + sPrice);
________________________________________



7. View Detailed Property Information
Example Code:
PropertyID := dbgSearch.DataSource.DataSet.FieldByName('ID').AsInteger;
ShowListingDetail(PropertyID);

Output
Data	Format	GUI Component
Property Price	"Property Price: <Price in currency format>"	dbgSearch: TDBGrid, edtPrice: TEdit
Bedrooms	"Bedrooms: <Number of bedrooms>"	dbgSearch: TDBGrid, sedBedroom: TSpinEdit
Bathrooms	"Bathrooms: <Number of bathrooms>"	sedBath: TSpinEdit
Property Type	"Property Type: <Type of property>"	cmbType: TComboBox, dbgSearch: TDBGrid
Province	"Province: <Selected province name>"	cmbProvince: TComboBox, dbgSearch: TDBGrid



