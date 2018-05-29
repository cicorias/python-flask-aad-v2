# Python-Flask OAuth2 Sign-In using Flask-OAuthlib Open Source Library

This example demonstrates how to use Azure AD with a 3rd party Python-Flask library ([flask-oauthlib](https://github.com/lepture/flask-oauthlib)) to do OAuth 2.0 against the v2.0 endpoint.  It then makes a call to the `/me` endpoint of the Microsoft Graph to get information about the user. 

## Steps to Run
We will use a virtual Python environment and Python3 for running this sample.  Note that beyond the Python-Flask environment, there is a need to logon to the [Azure Portal](https://portal.azure.com) and create an Azure AD Application

1. Clone the Repo

    ```
    git clone https://github.com/cicorias/aad-v2-python-flask
    cd aad-v2-python-flask
    ```
1. Create the Python virtual environment and install requirements
    ```
    python3 -m venv venv
    pip install -f requirements.txt
    ```

### Setup your Application in your Azure AD Tenant

1. Register your Azure AD v2.0 app.  
    - Navigate to the [Azure Portal Active Directory Blade](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade)
    - Go to the `Application Registrations` blade
    - From the Toolbar click on `+ New application registration`
    - Enter a Name for the application - `python-flask-sample` works fine
    - Make sure that `Web app/API` is selected for the **Application Type**
    - Enter the Return URL for this sample - `http://localhost:5000/login/authorized`.  -  make sure it's exactly that value.
    - Click the `Create` button
    - Once Created, click on the app in the Application Registration List - **NOTE:** You may have to click on `View All Applications` button to see.
    - In the Application Blade - click on `Settings` from the Toolbar
    - Under settings, click on `Keys`
    - In the section `Passwords` - enter a new value for `Key Description` then select the `Duration` - 1 year is fine for this sample
    - Click on `Save` on the Toolbar
    - Once Saved, ensure you capture the Value - it will be a 44 characters long string
    
1. From the Directory where the Flask App was cloned, create a new file `.env`
	- Enter the values as follows:
		- Replace the `APP_OAUTH_ID` with the Application ID value shown on the Azure Portal for the application registration - it will be a uuid/guid value.
		- Replace the `APP_OAUTH_SECRET` with the value from the Passwords you just created from settings on the Application Regisgtration
		- Replace the `APP_AAD_TENANT` with the friendly name of your AAD - this shows up in the Azure Portal AAD Blade under **Custom Domain Names**.

```
FLASK_ENV=development
APP_OAUTH_ID=<From App Registration Application ID>
APP_OAUTH_SECRET=<from App Registration Passwords>
APP_AAD_TENANT=<fromPortal>.onmicrosoft.com
```

1. From the same directory, you are ready to run the application. We set 1 environment variable `FLASK_APP` that is the main Python source file for the Application in this example

```
FLASK_APP=server.py flask run
```


1. At this point, you should be presented with a very plain screen showing a single `Login` button. This will redirect the Browser to the Azure AD Login Screen.
	- you should be prompted for User Permissions - This application will the user profile from the Microsoft Graph.
	- once you logon, and grant permissions, the page should redirect to the `/me` path - there the values retrieved from the `/me` Graph call will be dumped to the HTML view.




This sample was tested with Python 3.6.5 and the libraries and version in the `requirements.txt` file in the root of the Repository

## Notices

This sample is using a 3rd party library that has been tested for compatibility in basic scenarios with the v2.0 endpoint.  Microsoft does not provide fixes for these libraries and has not done a review of these libraries.  Issues and feature requests should be directed to the library's open-source project.  Please see this [document](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-libraries) for more information.   


## Acknowledgements

Updated based upon an original sample from [Navya Canumalla](https://github.com/navyasric) - note the original Sample has been Archived here [AAD Python Flask](https://github.com/Azure-Samples/active-directory-python-flask-graphapi-web-v2/tree/archive)

[flask-oauthlib](https://github.com/lepture/flask-oauthlib)

[oauthlib](https://github.com/oauthlib/oauthlib)

