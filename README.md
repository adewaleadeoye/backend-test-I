## Back-end Developer Test

### Laravel Twitter Bot: 

Pulls name and followers count based on filtered hashtag and stores it on google spreadsheet.

### Prerequisites
To run this project, your server must satisfy the following requirements
* PHP >= 7.1.3
* OpenSSL PHP Extension
* PDO PHP Extension
* Mbstring PHP Extension

## How to install and run the project

### Clone and run composer install
1. From a terminal and within a directory of choice run git clone 'git-url'
```
git clone https://github.com/adewaleadeoye/backend-test-I
```
2. cd into backend-test-I and run composer install
```
cd backend-test-I
backend-test-I> composer install
```
### Create a Twitter App
- Go to https://developer.twitter.com/en/apply/user and follow the instructions to setup a twitter application. 
- Once you've created your application, click on the Keys and access tokens tab to retrieve your consumer_key, consumer_secret, access_token and access_token_secret. We will need them later

### Enable Google Drive API and Create a new Spreadsheet
#### Enable the Google drive API following the steps below
![Enable Google Drive API](https://s3.amazonaws.com/com.twilio.prod.twilio-docs/original_images/google-developer-console.gif)
- Go to the Google APIs Console. https://console.developers.google.com/
- Create a new project.
- Click Enable API. Search for and enable the Google Drive API.
- Create credentials for a Web Server to access Application Data.
- Name the service account and grant it a Project Role of Editor. Copy the generated service account id (a pretty long email address) somewhere. It will be needed later
- Download the JSON file.
- Copy the JSON file to the project's root directory
#### Create spreadsheet
- Go to https://docs.google.com/spreadsheets and Create a google spreadsheet 
- Rename the Spreadsheet
- Click on the share button and give edit permission to the service account id you copied earlier.

### Set Environment variables
- Open .env file at the root of your project. If it doesn't exist, make a copy of .env.example and rename as .env
- Set up the following variables.
```
TWITTER_CONSUMER_KEY=twitter consumer key
TWITTER_CONSUMER_SECRET=twitter consumer secret
TWITTER_ACCESS_TOKEN=twitter access token
TWITTER_ACCESS_TOKEN_SECRET=twitter access token secret

GOOGLE_APPLICATION_CREDENTIALS=name of downloaded json file 
GOOGLE_SPREADSHEET_FILENAME=name of spreadsheet you created

Ensure QUEUE_DRIVER=sync
```
- We need an application key for the bot to run. On your terminal, type the following and press enter to set it up
```
php artisan key:generate
```
#### Running the project
- Open app.php in the config directory.
- Under Application Service Providers..., look for this line
```
//App\Providers\GoogleSheetServiceProvider::class,
```
- Uncomment it and save the app.php file
- On your terminal, run
```
php artisan twitter:stream 
At the prompt, type in an hashtag and press enter
```
