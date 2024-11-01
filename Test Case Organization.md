# Test Case Creation: Planetarium User Registration
- Use Case Id: 1
- Description: Users should be able to open a new User account with the Planetarium
- Actors:
    - New User

### Test Data

#### Requirement: Usernames and passwords should not be longer than 30 characters
|0 character Username|30 characters Username|31 characters Usernames|
|-|--|--|
||BatmanAndRobinToTheRescue20202|JokerAndRiddlerAreAtItAgain1010|

|0 character Password|30 characters Password|31 characters Password|
|-|-|-|
||GordonIsMyHeroForeverGoodMan11|LexLuthorIsSchemingAgainOhNo!!!|

#### Requirement: Users should have unique usernames
|Unique Username|Non-Unique Username|
|-|-|
|Robin|Batman|

#### Requirement: Passwords should never be visible in plaintext
- Password that should be obfuscated: "I am the night"
    - use for both Exploratory Testing and Error Guess Testing

#### Acceptance Testing Data
Use positive and negative test data found for [credentials length](#requirement-usernames-and-passwords-should-not-be-longer-than-30-characters) and [username uniqueness](#requirement-users-should-have-unique-usernames) depending on what kind of Acceptance Testing you are performing

#### Environment Data
- Browser: Edge
- Operating System: Windows 10
- Version of Planetarium: 1.0
- Background Data:
    - Login Page for Planetarium: http://localhost:8080/

### Test Scenarios

#### Decision Table For Username/Password Character Length Requirement Testing
|Username|Password|Account Creation Result|Redirect|
|-|-|-|-|
|(0 characters)|(0 characters)|User created|User redirected to login page result|
|(0 characters)|GordonIsMyHeroForeverGoodMan11|User created|User redirected to login page|
|(0 characters)|LexLuthorIsSchemingAgainOhNo!!!|User not created|User remains on creation page|
|BatmanAndRobinToTheRescue20202|(0 characters)|User created|User redirected to login page|
|BatmanAndRobinToTheRescue20202|GordonIsMyHeroForeverGoodMan11|User created|User redirected to login page|
|BatmanAndRobinToTheRescue20202|LexLuthorIsSchemingAgainOhNo!!!|User not created|User remains on creation page|
|JokerAndRiddlerAreAtItAgain1010|(0 character)|User not created|User redirected to login page|
|JokerAndRiddlerAreAtItAgain1010|GordonIsMyHeroForeverGoodMan11|User not created|User remains on creation page|
|JokerAndRiddlerAreAtItAgain1010|LexLuthorIsSchemingAgainOhNo!!!|User not created|User remains on creation page|

#### Decision Table for Unique Username Requirement Testing
|Username|Password|User Created|User redirected to login page result|
|-|-|-|-|
|Robin|GordonIsMyHeroForeverGoodMan11|User created|User redirected to login page|
|Batman|GordonIsMyHeroForeverGoodMan11|User not created|User remains on creation page|

#### Parameterized Test Scenario
|Step|Actor|Data|Result|
|-|-|-|-|
|given the user is on the login page|new user|http://localhost:8080/||
|when the user clicks the create account button|new user||should be redirected to the registration page|
|when the user provides {username} and {password} and clicks the create button|new user|{username},{password}||
|then the user should be given an alert saying {Account Creation Result}|new user||{Account Creation Result}|
|and {User Redirected to Login Page Result}|new user||{User Redirected to Login Page Result}|


********************************************************************************************************************************************************************************************


## Test case 2 - User login into Planetarium
- Use Case Id: 2
- Description: Users should be able to securely access their account
- Actors:
    - Registered User 

### Test Data

## Requirement: -Usernames and passwords should not be longer than 30 characters
|0 character Username |	30 characters Username	        | 31 characters Username
|                     |BatmanAndRobinToTheRescue20202	|UniverseExplorerAndAstronomer2020

|0 character Password |	30 characters Password	        |31 characters Password
|                     |GordonIsMyHeroForeverGoodMan11	                        |StarsOverTheCosmosAndBeyond99999

#### Requirement: Users should receive message on successful or failed login attempts
Positive feedback example: "Login successful! Redirecting to home page."
Negative feedback example: "Login failed. Please check your credentials."



#### Requirement: There should be a limit on failed login attempts before temporarily account lockout.
Attempt Count	|Result after Last Attempt	                    |System Feedback
1	            |Unsuccessful	                                |"Incorrect password. Please try again."
2	            |Unsuccessful	                                |"Incorrect password. Please try again."
3	            |Account locked	                                |"Account temporarily locked. Try again later."

#### Environment Data
- Browser: Edge
- Operating System: Windows 10
- Version of Planetarium: 1.0
- Background Data:
    - Login Page for Planetarium: http://localhost:8080/

#### Acceptance Testing Data
- The login page should be simple to navigate, with accessible password reset options and feedback on incorrect logins.
Credentials length, username uniqueness, alert for reset password or locked account

### Test Scenarios

#### Decision Table for Username/Password Character Length Requirement Testing
|Username                           |Password                           |Account login                                          |Redirect|
(0 characters)	                    (0 characters)	                        Login failed	                                    User redirected to login page
(0 characters)	                    GordonIsMyHeroForeverGoodMan11	        Login failed	                                    User redirected to login page
BatmanAndRobinToTheRescue20202 	    (0 characters)	                        Login failed	                                    User redirected to login page
BatmanAndRobinToTheRescue20202	    GordonIsMyHeroForeverGoodMan11	        Login successful	                                    Planetarium Home Page




#### Decision Table for limit on failed login attempts before temporarily account lockout.
Username	                            Password	                Attempt Count	                  Result	                    
BatmanAndRobinToTheRescue20202	    LexLuthorIsSchemingAgainOhNo!!!	    1	                     Login failed Please Try Again	        
BatmanAndRobinToTheRescue20202	    (0)	                                2	                      Login failed Please Try Again	       
LexLuthorIsSchemingAgainOhNo!!!	    BatmanAndRobinToTheRescue20202	    3	                     Account locked	        


### Parameterized Test Scenario
Step                                                                                Actor                            Data                      Excepted Result
Given the user is on the login page     	                                        Registered User	        http://localhost:8080/	
When the user enters {username} and {password}	                                    Registered User	            {username}, {password}	
Then the user should see a feedback message saying {Welcome to the Home Page}	        Registered User		                                 {Valid Login}
If the user put invalid credentials should see a feedback message saying {Invalid Login}	Registered User		                             {InValid Login}
--And the user should be redirected based on {Login Result}	Registered User		                                                        {Welcome to the Home Page}


********************************************************************************************************************************************************************************************

#### Test case 3 - Add planets and moons to Planetarium
- Use Case Id: 3
- Description: Users should be able to see planets and moons added to the Planetarium
- Actors:
    - New User 

### Requirements:  Only logged-in users should be able to view the Planetarium home page
Login Status	                  Data                                                  Expected Access to Planetarium Home Page
Logged In	                      http://localhost:8080/planetarium                        Access Granted
Logged Out	                      http://localhost:8080/                                   Access Denied


### Requirements: Planets and moons should have unique names and display accurately
Planet Name (Unique)	            Moon Name (Unique)	            Expected Display Result
Earth(Planet 1)	                    Luna	                        Both Planet and Moon display
Mars (Planet 2)	                    Titan	                        Both Planet and Moon display
Duplicate Planet (e.g., "Mars")	    Duplicate Moon (e.g., "Luna")	Display error for duplicates

#### Environment Data
- Browser: Edge
- Operating System: Windows 10
- Version of Planetarium: 1.0
- Background Data:
    Planetarium Home Page URL: http://localhost:8080/planetarium

#### Acceptance Testing Data
-The layout should make it easy to locate planets and moons, with search or filtering options available

## Test Scenarios

## Decision Table for Login Status Requirement Testing

Login Status	Data                                                Action	Expected Result
Logged In	    http://localhost:8080/planetarium                User navigates to Planetarium Home Page	User is granted access
Logged Out	    http://localhost:8080/                           User navigates to Planetarium Home Page	Access denied; user is redirected to login page


## Decision Table for Planet and Moon Uniqueness Requirement Testing
Planet Name	                    | Moon Name |	                         Display Outcome |	                                
|-|-|-|-|
Earth(Planet 1)	                    |   Luna (Moon 1)	|                Planet and Moon display	               
Mars (Planet 2)	                    |   Titan (Moon 2)|                  Planet and Moon display	                
Mars (Duplicate)                    |	Luna (Duplicate)|                   not exist/Duplicate error displayed	    
Jupiter123456789123456789123456     |   Callisto123456789123456789123456 |   not exist/Duplicate error displayed
Venus (Planet 4)                    |   Callisto123456789123456789123456 |  not exist/Duplicate error displayed
Jupiter123456789123456789123456   |     Europa (Moon 4)  |                  not exist/Duplicate error displayed

## Parameterized Test Scenario
Steps |	Actor |	Data |	Expected Result |
|-|-|-|-|
Given the user is on the Planetarium home page and logged in |	Registered User |	http://localhost:8080/planetarium	|
When the user views the list of planets and moons |	Registered User		| All planets and moons are visible
Then all unique planets and moons should display |	Registered User	|	| All planets and moons are visible |
And the system should not allow duplicate planets or moons to display |	Registered User	||	Duplicate error displayed if duplicates are present 
New planet and moon added with character length requirement |	Registered User	||	not exist/Duplicate error displayed




********************************************************************************************************************************************************************************************


## Test Case 4:Add new Planets to the Planetarium
- Use Case Id: 4
- Description: Users should be able to add new planets to the planetarium
- Actors:
    - Registered User 

## Requirements: Planet names should not exceed 30 characters and should be unique
 Planet Name                                | Expected Outcome      
|-|-|-|
|(0 characters)|                               Error: Planet name is required                 
 MysticGalaxyPlanetAlphaCentauri  |             Planet added successfully 
 BeyondTheEventHorizonSuperPlanetX1 |          Planet not added

## Requirement: Planets should have unique names

Planet Name |  Expected Outcome
Earth        | Error: Planet name already exists
Mercury     |  Planet added successfully



## Requirements: Planets should allow an associated image but it should not be required
Planet Name	                Image Provided	                Expected Outcome
"Neptune"	                Yes	                            Planet added successfully
"Zephyron"	                No	                            Planet added successfully
"Jupiter"	                Yes (duplicate)	                Error: Planet name already exists


#### Environment Data
- Browser: Edge
- Operating System: Windows 10
- Version of Planetarium: 1.0
- Background Data:
    Planetarium Home Page URL: http://localhost:8080/planetarium

#### Acceptance Testing Data
-Users should easily navigate to the “Add Planet” feature, with prompts that guide input fields like name, image, and details.



## Test Scenarios

## Decision Table for Planet Name Character Length and Uniqueness Requirement Testing
Planet Name	| Image Provided  |	Action	 | Expected Outcome
|-|-|-|-|
(0 characters)	 | No	| Attempt to add |	Error: Planet name is required
"MysticGalaxyPlanetAlphaCentauri" |	No	| Add	| Planet added successfully
"BeyondTheEventHorizonSuperPlanetX1" |	Yes |	Add	|  Error: Planet name exceeds 30 chars
"Zypheron" |	Yes	| Add	|  Planet added successfully
"Jupiter" |	No |	Attempt to add duplicate	| Error: Planet name already exists

## Parameterized Test Scenario
Step	|Actor	|Data	|Expected Result
|-|-|-|-|
Given the user is on the Add Planet page and logged in	   |     Registered User   |     	http://localhost:8080/add-planet	| |
When the user provides {planet name} and optionally uploads an image	|Registered User	{planet name}, {image}	  | |
Then the user should see a feedback message saying {Outcome}	| Registered User	| |	{Outcome}
And the planet should be added to the Planetarium if data is valid	| Registered User	| |	Planet appears in list if added successfully

********************************************************************************************************************************************************************************************

## Test Case 5:Remove Planets from the Planetarium
- Use Case Id: 5
- Description: Users should be able to remove Planets from the Planetarium
- Actors:
    - Registered User 

## Requirements: Users should only be able to remove planets they have added
 User Name	                                                Planet Name	   Planet Owner 	Expected Outcome
BatmanAndRobinToTheRescue20202	                             Zephyron	        3	        Planet removed successfully
BatmanAndRobinToTheRescue20202	                             Earth	            1	       Failed to remove


## Requirements: Planet removal should trigger a confirmation prompt before deletion
Confirmation Response	        Expected Outcome
Confirm	                        Planet removed successfully
Cancel	                        Planet remains in the Planetarium


#### Environment Data
- Browser: Edge
- Operating System: Windows 10
- Version of Planetarium: 1.0
- Background Data:
    Planetarium Home Page URL: http://localhost:8080/planetarium




#### Acceptance Testing Data
-Users should be prompted to confirm deletion to avoid accidental removals, with a clear description of what will be removed.

## Decision Table for Planet Removal Access Control Testing
User Name	                           Planet Name	   Planet Owner		            Expected Outcome
BatmanAndRobinToTheRescue20202          Zephyron	        3	        	Planet removed successfully
BatmanAndRobinToTheRescue20202	        Earth	           	1      	        Failed to remove
Batman                                  Earth	            1	       	    Failed to remove




## Decision Table for Confirmation Prompt Requirement Testing
Confirmation Response	    Action	                            Expected Outcome
Confirm	                User confirms deletion	                Planet removed successfully
Cancel	                User cancels deletion	                Planet remains in Planetarium

## Parameterized Test Scenario
Step	                               Actor	                                         Data	                                                  Expected Result
Given the user is on the Planetarium home page and logged in	Registered User	    http://localhost:8080/planetarium	
When the user selects {planet name} and attempts to delete it	Registered User	    {planet name}	
Then a confirmation prompt should appear	                    Registered User		
And if the user confirms, {Outcome}	Registered User		                                                            Planet is removed if confirmed, retained if canceled

********************************************************************************************************************************************************************************************


## Test Case 6:Add Moons to the Planetarium associated with a Planet
- Use Case Id: 6
- Description: Users should be able to add Moons to the Planetarium associated with a Planet
- Actors:
    - Registered User 


## Requirements: Moon names should not exceed 30 characters and should be unique for each planet
Planet Name                                         Moon Name                                                                    | Expected Outcome      
|-|-|-|
|(0 characters)|                               (0 characters)                                                                   Error: Moon name is required                 
 MysticGalaxyPlanetAlphaCentauri  |             CelestialWandererSatellite1                                                     Moon added successfully 
 BeyondTheEventHorizonSuperPlanetX1 |            GalacticOrbitSpectreSatellite001                                               Moon not added

## Requirement: Moons should be associated with a specific planet
Username	                     Planet	Moon Name	    Expected Outcome
BatmanAndRobinToTheRescue20202	Earth	Luna	    Moon added successfully under "Earth"
BatmanAndRobinToTheRescue20202	Mars	Luna	    Moon added successfully under "Mars"
BatmanAndRobinToTheRescue20202	Earth	Titan	    Error: Duplicate moon name for "Earth"

## Requirement: Moons should allow an associated image but it should not be required
Moon Name	       Planet	Image Provided	     Expected Outcome
Phobos	            Mars	Yes         	        Moon added successfully
Deimos	            Mars	No	                    Moon added successfully
Titan	            Saturn	Yes (duplicate)	        Error: Duplicate moon




#### Environment Data
- Browser: Edge
- Operating System: Windows 10
- Version of Planetarium: 1.0
- Background Data:
    Planetarium Home Page URL: http://localhost:8080/planetarium

#### Acceptance Testing Data
-The interface should guide users in associating the moon with a specific planet, with clearly labeled fields for entry.


##  Test Scenarios
## Decision Table for Moon Name Character Length and Uniqueness Requirement Testing
Moon Name	                        Planet     	Image Provided	       	                Expected Outcome
(0 characters)	                    Earth	    Yes	                    	            Error: Moon name is required
CelestialWandererSatellite	        Mars	    Yes                                     Moon added successfully
GalacticOrbitSpectreSatellite001	Earth	    No             		                    Error: Moon name exceeds 30 chars
Titan                               Earth	    No	               	                    Error: Duplicate moon name for planet
Europa	                            Jupiter	    Yes	                	                Moon added successfully


## Parameterized Test Scenario
Step	                                                        Actor	                              Data	                                    Expected Result
Given the user is on the Add Moon page and logged in	    Registered User         	            http://localhost:8080/planetarium	
When the user selects {planet} and provides {moon name}, optionally uploads an image	Registered User	        {planet}, {moon name}	
Then the user should see a feedback message saying {Outcome}	Registered User		                                                                {Outcome}
And the moon should be added under the selected planet if data is valid	    Registered User		                                                Moon appears under planet if added successfully

********************************************************************************************************************************************************************************************

## Test Case 7: Remove Moons from the Planetarium
- Use Case Id: 7
- Description: Users should be able to remove Moons from the Planetarium
- Actors:
    - Registered User 


## Users should only be able to remove moons they have added
User	                             Planet     Moon Name	Moon Owner	    Expected Outcome
BatmanAndRobinToTheRescue20202	      Earth	    Luna	    1	        Moon removed successfully
BatmanAndRobinToTheRescue20202	       Mars	    Phobos	    none        Error: Access denied

#### Environment Data
- Browser: Edge
- Operating System: Windows 10
- Version of Planetarium: 1.0
- Background Data:
    Planetarium Home Page URL: http://localhost:8080/planetarium

#### Acceptance Testing Data
-Users should receive a prompt to confirm removal and a final success message, ensuring transparency in the deletion process

## Test Scenarios
Decision Table for Moon Removal Access Control Testing
User	                        Planet	Moon Name	Planet Owner		    Expected Outcome
BatmanAndRobinToTheRescue20202	Earth	Luna	    1	        	Moon removed successfully
BatmanAndRobinToTheRescue20202	Mars	Phobos	    none	    	Error: Access denied
Batman	                        Saturn	Titan	    none	    	Moon removed successfully

## Parameterized Test Scenario
Step	                                                                     Actor	                         Data	                         Expected Result
|-|-|-|
Given the user is on the Planetarium home page and logged in	            Registered User	            http://localhost:8080/planetarium	
When the user selects {planet} and {moon name} and attempts to delete it	Registered User	            {planet}, {moon name}	
Then a confirmation prompt should appear	                                Registered User		                                            {Outcome}
And if the user confirms, {Outcome}	                                        Registered User		                       Moon is removed if confirmed, retained if canceled




## Acceptance Summary for The Planetarium Project

Project Overview: 
The Planetarium is a web application developed by Space Initiative to provide astronomers with a comprehensive tool for tracking celestial bodies. This tool is designed to offer enhanced accuracy, user-friendly navigation, and reliable data access for both professional astronomers and enthusiasts. As part of the testing team, the focus was to ensure the application met functional, usability, and performance standards.

Acceptance Testing Data															
-All Use Cases Inspired Confidence
	Security prompts, confirmation dialogs, and well-labeled actions contributed to user trust, especially in critical actions like login and data deletion.

-Visual Cohesion in Majority of Use Cases
    The application maintained a consistent look across different features, particularly in the celestial body tracking interface.	

-Usability Issue	
    Users found the process of associating moons with planets initially confusing due to limited guidance, suggesting a need for more detailed prompts or helper text.														




- The login page should be simple to navigate, with accessible password reset options and feedback on incorrect logins.
Credentials length, username uniqueness, alert for reset password or locked account

-The layout should make it easy to locate planets and moons, with search or filtering options available

-Users should easily navigate to the “Add Planet” feature, with prompts that guide input fields like name, image, and details.

-Users should be prompted to confirm deletion to avoid accidental removals, with a clear description of what will be removed.

--Users should receive a prompt to confirm removal and a final success message, ensuring transparency in the deletion process








