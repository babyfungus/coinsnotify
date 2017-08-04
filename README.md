# Coinsnotify
Bitcoin notification API

# API KEY

Wherever you use the Coinsnotify API, you must use a Coinsnotify member ID for client_id and an API key for client_secret.

# Example of API key usage

"client_id=$CLIENT_ID&client_secret=$CLIENT_SECRET"
Issue an API key

To use the Coinsnotify API, you need to get an API key. The API key is issued automatically when you register. You can check the API KEY menu of the member information.

# Reset API Key

Enter API key menu of member information and press API key reset button to change to new API key.

# Group

Once you register and authenticate your email, a default group called main_group will be created. You can also add new groups. You can assign an HTTP Callback URL for each group.

# Group registration

You must register a bitcoin address with the group before you can receive an HTTP Callback. If you register an address in a group, you will receive a bitcoin deposit details (deposit address, deposit amount) with the HTTP Callback URL registered in the group when the bit coin is deposited to the address. Only one HTTP Callback URL can be registered in a group. If you want to add a new group, you can add a group. The new group must include the group name and HTTP Callback URL. When registering HTTP Callback URL using API, only URL can be registered and email address registration is not allowed. When registering using the bit coin notification form on Coinsnotify's home screen, it will be registered in the main group, main_group, and the HTTP Callback URL in main_group will be changed to the URL you entered.

# New group registration URL

POST https://coinsnotify.com/api/group/add

Request example

curl -d "group_name=$GROUP_NAME&callback_url=$CALLBACK_URL"
https://coinsnotify.com/api/group/add

Response example

{ 
    "group_name":"exchange", 
    "callback_url":"https://my.domain.com/callback/alarm" 
}

# New group registration URL

An API that allows you to modify the group's HTTP Callback URL. You can not change the group name.

# Edit group URL
POST https://coinsnotify.com/api/group/update

Request example

curl -d "group_name=$MY_GROUP_NAME&callback_url=$CALLBACK_URL"
https://coinsnotify.com/api/group/update

Response example

{ 
    "group_name":"main_group", 
    "callback_url":"https://my.domain.com/callback/payment" 
}

# Delete group

An API that allows you to delete a group. You can delete only when there is no registered address in the group. The default group, main_group, can not be deleted.

# Delete group URL
POST https://coinsnotify.com/api/group/delete

Request example

curl -d "group_name=$MY_GROUP_NAME
https://coinsnotify.com/api/group/delete

Response example

{ 
    "group_name":"exchange", 
    "deleted":true 
}

# Group List

API to view all group names.

Group List URL
GET https://coinsnotify.com/api/group/list

Request example

GET https://coinsnotify.com/api/group/list

Response example

{ 
    "group_names": [ 
        "main_group", 
        "exchange", 
        "sub_group" 
    ] 
}

# HTTP Callback

When the bitcoin is deposited into the bitcoin address in the group, the callback is delivered to the HTTP Callback URL registered in the group. Confirmed means the number of bit coin confirms and passes callbacks from one to three conform. Value is bitcoin quantity, and the unit is Satoshi. Details about the bitcoin transaction can be found with txid.


HTTP Callback Example

/api/callback_url?txid=58402cd1367cb959c5f02a3d6c7cb1f43893d6b96101433bdb223f1b09363d79&address=1B2L3cfm1CFH8cUB9BRKUs8zFGYEJLtWev&value=10000&confirmed=1

# Bitcoin address

When you register a bitcoin address in a group, you can receive a bitcoin deposit alarm in the corresponding bit coin address as an HTTP Callback. You must enter the name of the group to which you want to register the address. The name of the default group is main_group.

# Address registration

An API that allows you to register a bitcoin address in a group.

Bitcoin address registration URL
POST https://coinsnotify.com/api/address/add

Request example

curl -d "group_name=$MY_GROUP_NAME&address=$MY_ADDRESS"
https://coinsnotify.com/api/address/add

Response example

{ 
    "group_name":"main_group", 
    "address":"1B2L3cfm1CFH8cUB9BRKUs8zFGYEJLtWev" 
}

# Bitcoin Address Multiple Registration

You can register multiple bitcoin addresses at once. If any of the addresses to be registered are already registered, the registration will be stopped. Up to 100 can be registered at one time.

Example of address bulk registration request

$address1 = "17QqxasYgbpRgLVPXYNWCB8Eva47SQMzFQ";
$address2 = "1FGfw2u58vdxZwULYnB3Pe5Brj7phFgsuy";
$ADDRESSES = urlencode('{
    "' . $address1 . '",
    "' . $address2 . '"
}');

curl -d group_name=$GROUP_NAME&addresses=$ADDRESSES
https://coinsnotify.com/api/address/add

Response example

{ 
    "group_name":"main_group", 
    "addresses":[
        "17QqxasYgbpRgLVPXYNWCB8Eva47SQMzFQ",
        "1FGfw2u58vdxZwULYnB3Pe5Brj7phFgsuy"
    ]
}

# Remove address

An API that deletes registered bitcoin addresses in a group.

Bit coin address removal URL
POST https://coinsnotify.com/api/address/delete

Request example

curl -d "group_name=$MY_GROUP_NAME&address=$MY_ADDRESS"
https://coinsnotify.com/api/address/delete

Response example

{ 
    "address":"1B2L3cfm1CFH8cUB9BRKUs8zFGYEJLtWev", 
    "deleted":true 
}

# Address List

An API that allows you to see a list of all addresses registered in the group.

Address List URL
GET https://coinsnotify.com/api/address/list

Request example

GET https://coinsnotify.com/api/address/list?group_name=$MY_GROUP_NAME

Response example

{ 
    "group_name":"main_group", 
    "addresses": [ 
        "1HU75qzZTz7H42rfriijCFRxGV9vWZa9vi", 
        "18ZDqSNmUscKN63B3P32CJagVaJs8j7q5i", 
        "122mMpoQ75s6vyA5o5n6HDJwaNDHjiZo85" 
    ] 
}
