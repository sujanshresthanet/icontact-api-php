# About iContact
[iContact](http://www.icontact.com/) allows businesses, non-profit organizations, and associations to easily create, send, and track email newsletters, surveys, and autoresponders. The latest release of this Drupal module utilizes [iContact’s](http://www.icontact.com/) 2.0 API allowing for management of [iContact](http://www.icontact.com/) accounts from your Drupal powered web site as well as allowing new subscriptions by users and message statistics.

## Php integration

*   Manage accounts, client folders, contacts and more
*   Provide methods for users to subscribe to lists via user profile and/or during user registration

## Optimized for performance

The data gathered via [iContact’s](http://www.icontact.com/) 2.0 API is cached locally to reduce the web traffic on the API and only updates on saving or adding new data or by force dumping the cache. Each individual resource is cached separately thus preventing refreshing any unchanged resource data.

## Extensible

The iContact object provided holds all the data associated with an authenticated [iContact](http://www.icontact.com/) account and is made available for other modules to extend features that this module lacks.

## About

iContact is the easiest email marketing platform for small businesses. It was built to take the pain out of email marketing. Our easy-to-use tools help you grow your audience, design beautiful emails, personalize your messages and automate your communications. Click here for more details.

## Uses

`Using simple actions  `
Simple actions do not require configuration and are listed automatically as available on the Actions page.  
`Creating and configuring advanced actions`
Advanced actions are user-created and have to be configured individually. Create an advanced action on the Actions page by selecting an action type from the drop-down list. Then configure your action, for example by specifying the recipient of an automated email message.

## How to use
```php
<?php
ini_set('display_errors', true);
ini_set('error_reporting', E_ALL);

// Load the iContact library
require_once('lib/iContactApi.php');

// Give the API your information
iContactApi::getInstance()->setConfig(array(
	'appId'       => '', 
	'apiPassword' => '', 
	'apiUsername' => ''
));

// Store the singleton
$oiContact = iContactApi::getInstance();
// Try to make the call(s)
try {
	//  are examples on how to call the  iContact PHP API class
	// Grab all contacts
	var_dump($oiContact->getContacts());
	// Grab a contact
	var_dump($oiContact->getContact(42094396));
	// Create a contact
	var_dump($oiContact->addContact('joe@shmoe.com', null, null, 'Joe', 'Shmoe', null, '123 Somewhere Ln', 'Apt 12', 'Somewhere', 'NW', '12345', '123-456-7890', '123-456-7890', null));
	// Get messages
	var_dump($oiContact->getMessages());
	// Create a list
	var_dump($oiContact->addList('somelist', 1698, true, false, false, 'Just an example list', 'Some List'));
	// Subscribe contact to list
	var_dump($oiContact->subscribeContactToList(42094396, 179962, 'normal'));
	// Grab all campaigns
	var_dump($oiContact->getCampaigns());
	// Create message
	var_dump($oiContact->addMessage('An Example Message', 585, '<h1>An Example Message</h1>', 'An Example Message', 'ExampleMessage', 33765, 'normal'));
	// Schedule send
	var_dump($oiContact->sendMessage(array(33765), 179962, null, null, null, mktime(12, 0, 0, 1, 1, 2012)));
	// Upload data by sending a filename (execute a PUT based on file contents)
	var_dump($oiContact->uploadData('/path/to/file.csv', 179962));
	// Upload data by sending a string of file contents
	$sFileData = file_get_contents('/path/to/file.csv');  // Read the file
	var_dump($oiContact->uploadData($sFileData, 179962)); // Send the data to the API
} catch (Exception $oException) { // Catch any exceptions
	// Dump errors
	var_dump($oiContact->getErrors());
	// Grab the last raw request data
	var_dump($oiContact->getLastRequest());
	// Grab the last raw response data
	var_dump($oiContact->getLastResponse());
}
```
