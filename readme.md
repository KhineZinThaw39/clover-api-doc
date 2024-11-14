# Clover's API Documentation 

## Table of Contents
- [Authentication](#authentication)
  - [Login](#login)
  - [Register](#register)
  - [Logout](#logout)
- [Home Page](#home-page)
- [Hotels](#hotels)
  - [Get All Hotels](#get-all-hotels)
  - [Get Hotel Details](#get-hotel-details)
- [Rooms](#rooms)
  - [Get Rooms by Hotel](#get-rooms-by-hotel)
  - [Get Room Details](#get-room-details)
  - [Room Filter](#room-filter)
- [Bookings](#bookings)
  - [Create Booking](#create-booking)
  - [Get Bookings](#get-bookings)
  - [Get Booking Details](#get-booking-details)
- [Profile](#profile)
  - [Get Profile](#get-profile)
  - [Update Profile](#update-profile)
- [Rewards](#rewards)
  - [Get Rewards](#get-rewards)
- [Point History](#point-history)
  - [Get Point History](#get-point-history)
- [Chat](#chat)
  - [Get Chat Questions](#get-chat-questions)
  - [Get Chat Messages List](#get-chat-messages-list)
  - [Start Chat](#start-chat)
  - [Send Chat Message](#send-chat-message)
  - [Send Image](#send-image)
  - [Send Multiple Image](#send-multiple-image)
  - [Send Voice](#send-voice)
  - [Read Message](#read-message)
- [Notifications](#notifications)
  - [Get Notifications](#get-notifications)
- [Delete Account](#delete-account)


## Authentication

### Login

#### URL
`POST /api/login`

#### Description
Authenticate a customer and return a Bear token.

#### Request Parameters
- `user_id`: (string) User's email address. (required)
- `password`: (string) User's password. (required)
- `fcm_token`: (string) User's FCM token. (required)

#### Show Validation Errors
```json
{
    "message": "The user_id field is required. (and 2 more errors)",
    "errors": {
        "user_id": [
            "The user id field is required."
        ],
        "password": [
            "The password field is required."
        ]
    }
}
```
#### Response (Status 200)
```json
{
  "success": true,
  "message": "Login successful",
  "token": "your_bear_token"
}
```
### Register
#### URL
`POST /api/register`

#### Description
Register a new customer.

#### Request Parameters
- `name`: (string) User's full name. (required)
- `phone`: (string) User's phone number. (required)
- `password`: (string) User's password. (required)
- `password_confirmation`: (string) Confirmation of the password. (required)
- `nrc`: (string) User's NRC number. (optional)
- `fcm_token`: (string) User's FCM token. (required)

#### Show Validation Errors
```json
{
    "message": "The name field is required. (and 2 more errors)",
    "errors": {
        "name": [
            "The name field is required."
        ],
        "phone": [
            "The phone field is required."
        ], ...
    }
}
```

#### Response
```json
{
  "success": true,
  "message": "Registration successful",
  "token": "your_bearer_token"
}
```
### Logout
#### URL
`POST /api/logout`
#### Description
Logout the authenticated customer.
#### Headers
- `Authorization`: Bearer Token
#### Response
```json
{
    "success": true,
    "message": "Logout successful",
}
```

## Home Page
### Get Home Page Data
#### URL
`GET /api/home`
#### Description
Retrieve data for the home page.
#### Response
```json
{
    "success": true,
    "message": "Home page data retrieved successfully",
    "data": {
        "customer" : {
            "name": "John Doe",
            "total_points": 1000,
            "tier": "Gold"
        }
        "promotions": [
            {
                "id": 1,
                "title": "Summer Sale",
                "description": "Text",
                "image": {
                    "id": 7,
                    "url": "img_url",
                }
            }, ...
        ],
        "benefits_of_points": [
            {
                "id": 1,
                "name_en": "Swimming Pool",
                "name_mm": "Swimming Pool",
                "point_count": 10,
                "image": {
                    "id": 7,
                    "url": "img_url",
                }
            }, ...
        ],
    }
}
```

## Hotels
### Get All Hotels
#### URL
`GET /api/hotels`
#### Description
Retrieve a list of all hotels.
#### Response
```json
{
    "success": true,
    "message": "Hotels retrieved successfully",
    "data": [
        {
            "id": 1,
            "name": "Hotel A",
            "address": "123 Main St",
            "phone_numbers": "123-456-7890, 987-654-3210",
            "feature_image": {
                "id": 1,
                "url": "img_url",
            },
            "images": [
                {
                    "id": 1,
                    "url": "img_url",
                }, ...
            ],
        }, ...
    ]
}
```
### Get Hotel Details
#### URL
`GET /api/hotels/{id}`
#### Description
Retrieve details of a specific hotel.
#### Response
```json
{
    "success": true,
    "message": "Hotel details retrieved successfully",
    "data": {
        "id": 1,
        "name": "Hotel A",
        "address": "123 Main St",
        "phone_numbers": "123-456-7890, 987-654-3210",
        "feature_image": {
            "id": 1,
            "url": "img_url",
        },
        "images": [
            {
                "id": 1,
                "url": "img_url",
            }, ...
        ],
    }
}
```

## Rooms
### Get Rooms by Hotel
#### URL
`GET /api/hotels/{hotel_id}/rooms`
#### Description
Retrieve a list of rooms for a specific hotel.
#### Response
```json
{
    "success": true,
    "message": "Rooms retrieved successfully",
    "data": [
        {
            "id": 1,
            "name_mm": "Room A",
            "name_en": "Room A",
            "size": 200 ft,
            "view_type": {
              "id": 1,
              "name_mm": "Sea View",
              "name_en": "Sea View"
            },
            "bed_type": "King",
            "feature_image": {
                "id": 1,
                "url": "img_url",
            },
        }, ...
    ]
}
```

### Get Room Details
#### URL
`GET /api/rooms/{room_id}`
#### Description
Retrieve details of a specific room.
#### Response
```json
{
    "success": true,
    "message": "Room details retrieved successfully",
    "data": {
        "id": 1,
        "name_mm": "Room A",
        "name_en": "Room A",
        "hotel_name": "Hotel A",
        "size": 200 ft,
         "view_type": {
            "id": 1,
            "name_mm": "Sea View",
            "name_en": "Sea View"
        },
        "bed_type": "King",
        "room_type": {
            "id": 1,
            "name_mm": "Deluxe",
            "name_en": "Deluxe"
        },
        "description_mm": "Text",
        "description_en": "Text",
        "is_smoking": true,
        "is_shower": true,
        "weekday_price": 100,
        "weekend_price": 150,
        "weekday_points": 10,
        "weekend_points": 15,
        "staycation_from": "2 pm",
        "staycation_to": "9 am",
        "daycation_from": "2 pm",
        "daycation_to": "9 am",
        "feature_image": {
            "id": 1,
            "url": "img_url",
        },
        "images": [
            {
                "id": 1,
                "url": "img_url",
            }, ...
        ],
    }
}
```

## Rooms
### Room Filter
#### URL
`POST /api/filter`
#### Description
Retrieve a list of rooms by filter.
#### Request Parameters
- `hotel_id`: (integer) ID of the hotel. (required)
- `room_type_id`: (integer) ID of the room.
- `from_date`: (date) Check-in date. (required)
- `to_date`: (date) Check-out date.
#### Response
```json
{
    "success": true,
    "message": "Rooms retrieved successfully",
    "data": {
        "rooms": [
            {
                "id": 1,
                "name_mm": "Ashely Gilmore",
                "name_en": "Larissa Horton",
                "size": "60 ft",
                "view_type": {
                    "id": 1,
                    "name_mm": "Ava Weaver",
                    "name_en": "Hermione Hardin"
                },
                "bed_type": "Quisquam dolor cillu",
                "feature_image": {
                    "id": 4,
                    "url": "http://clover-hotel.test/storage/4/71rE1fTEeDL._SL1500_.jpg"
                }
            }
        ],
        "all_hotels": [
            {
                "id": 1,
                "name": "Xanthus Tucker",
                "address": "Consequuntur exercit",
                "phone_numbers": "+1 (128) 887-1586",
                "feature_image": {
                    "id": 1,
                    "url": "aaa.jpg"
                },
                "images": [
                    {
                        "id": 2,
                        "url": "aaa.jpg"
                    },
                ]
            }
        ],
        "hotel": {
            "id": 1,
            "hotel_admin_id": 2,
            "hotel_assistant_id": 3,
            "name": "Xanthus Tucker",
            "address": "Consequuntur exercit",
            "phone_numbers": "+1 (128) 887-1586",
            "created_at": "2024-11-11T07:18:27.000000Z",
            "updated_at": "2024-11-11T07:18:27.000000Z"
        }
    }
}
```

## Bookings
### Create Booking
#### URL
`POST /api/bookings`
#### Description
Create a new booking.

#### Headers
- `Authorization`: Bearer Token

#### Request Parameters
- `hotel_id`: (integer) ID of the hotel. (required)
- `room_id`: (integer) ID of the room. (required)
- `check_in_date`: (date) Check-in date. (required)
- `check_out_date`: (date) Check-out date. (required)
- `duration`: (integer) Duration of the booking. (required)
- `total`: (decimal) Total price of the booking. (required)

#### Response
```json
{
    "success": true,
    "message": "Booking created successfully",
    "data": {
        "id": 1,
        "uuid": "123e4567-e89b",
    }
}
```

### Get Bookings
#### URL
`GET /api/bookings`
#### Description
Retrieve a list of bookings for the authenticated customer.
#### Headers
- `Authorization`: Bearer Token
#### Response
```json
{
    "success": true,
    "message": "Bookings retrieved successfully",
    "data": [
        {
            "id": 1,
            "uuid": "123e4567-e89b",
            "status": "Pending",
            "created_at": "2023-09-12 10:30:00",
        }, ...
    ]
}
```
### Get Booking Details
#### URL
`GET /api/bookings/{booking_id}`
#### Description
Retrieve details of a specific booking.
#### Headers
- `Authorization`: Bearer Token
#### Response
```json
{
    "success": true,
    "message": "Booking details retrieved successfully",
    "data": {
        "id": 1,
        "uuid": "123e4567-e89b",
        "status": "Pending",
        "created_at": "2023-09-12 10:30:00",
        "hotel": {
            "id": 1,
            "name": "Hotel A",
        },
        "room": {
            "id": 1,
            "name_mm": "Room A",
            "name_en": "Room A",
            "room_type": {
                "id" : 1,
                "name_en" : "Delux",
                "name_mm" : "Delux",
            }
        },
        "check_in_date": "2023-09-12",
        "check_out_date": "2023-09-15",
        "duration": 3,
        "total": 300000,
    }
}
```
## Profile
### Get Customer Profile
#### URL
`GET /api/profile`
#### Description
Retrieve the authenticated customer's profile.
#### Headers
- `Authorization`: Bearer Token
#### Response
```json
{
    "success": true,
    "message": "Profile retrieved successfully",
    "data": {
        "id": 1,
        "uuid": "123e4567-e89b",
        "name": "John Doe",
        "phone": "123-456-7890",
        "nrc": "1234567890",
        "dob": "1990-01-01",
        "image": "img_url",
    }
}
```
### Update Customer Profile
#### URL
`PUT /api/profile`
#### Description
Update the authenticated customer's profile.
#### Headers
- `Authorization`: Bearer Token
#### Request Parameters
- `name`: (string) Customer's name.
- `phone`: (string) Customer's phone number.
- `nrc`: (string) Customer's NRC number.
- `dob`: (date) Customer's date of birth.
- `image`: (file) Customer's profile image.
- `password`: (string) Customer's password.
- `password_confirmation`: (string) Confirmation of the password.
#### Response
```json
{
    "success": true,
    "message": "Profile updated successfully",
}
```

## Rewards
### Get Rewards
#### URL
`GET /api/rewards`
#### Description
Retrive the authenticated customer's rewards.
#### Headers
- `Authorization`: Bearer Token
#### Response
```json
{
    "success": true,
    "message": "Rewards retrieved successfully",
    "data": {
        "rewards": [
            {
                "id": 1,
                "name": "Gold",
                "benefits_mm": "Free breakfast,etc.",
                "benefits_en": "Free breakfast,etc.",
                "start_points": 1000,
                "image": "img_url",
            }, ...
        ],
        "current_reward": {
            "id": 1,
            "name": "Gold",
        },
        "total_earned_points": 1500,
        "total_remaining_points": 500,
    }
}
```

## Point History
### Get Point History
#### URL
`GET /api/point-history`
#### Description
Retrieve the authenticated customer's point history.
#### Headers
- `Authorization`: Bearer Token
#### Response
```json
{
    "success": true,
    "message": "Point history retrieved successfully",
    "data": [
        "all": [
            {
                "id": 1,
                "status" : "Earned",
                "points": 100,
                "hotel_name": "Hotel A",
                "discount": 10000,
                "created_at": "2023-09-12 10:30:00",
            }, ...
        ],
        "earned": [
            {
                "id": 1,
                "status" : "Earned",
                "points": 100,
                "hotel_name": "Hotel A",
                "created_at": "2023-09-12 10:30:00"
            }, ...
        ],
        "used": [
             {
                "id": 1,
                "status" : "Earned",
                "points": 100,
                "hotel_name": "Hotel A",
                "discount": 10000,
                "created_at": "2023-09-12 10:30:00"
            }, ...
        ]
    ]
}
```
## Notifications
### Get Notifications
#### URL
`GET /api/notifications`
#### Description
Retrieve the authenticated customer's notifications.
#### Headers
- `Authorization`: Bearer Token
#### Response
```json
{
    "success": true,
    "message": "Notifications retrieved successfully",
    "data": [
        {
            "id": 1,
            "title": "Welcome to our hotel!",
            "body": "Thank you for choosing our hotel.!",
        },
        ...
    ]
}
```

## Chat
### Get Chat Questions
#### URL
`GET /api/chat-questions`
#### Description
Retrieve the authenticated customer's chat questions.
#### Headers
- `Authorization`: Bearer Token
#### Response
```json
{
    {
    "data": [
        {
            "id": 1,
            "question": "How to take reservation?"
        },
        {
            "id": 2,
            "question": "How to contact us?"
        },
        {
            "id": 3,
            "question": "What service do you serve?"
        }
    ]
}
}
```
### Get Chat Messages List
#### URL
`GET /api/chats/{hotel_id}`
#### Description
Retrieve the authenticated customer's chat messages by hotel.
#### Headers
- `Authorization`: Bearer Token
#### Response
```json
{
    "success": true,
    "message": "Chats fetched successfully.",
    "data": [
        {
            "hotel_id": "1",
            "admin_id": 1,
            "customer_id": null,
            "is_read": true,
            "message": "How can I help you?",
            "imageUrl": "",
            "audioUrl": "",
            "timestamp": "2024-11-13T07:58:03.716640Z"
        },
        {
            "hotel_id": "1",
            "admin_id": null,
            "customer_id": 1,
            "is_read": true,
            "message": "",
            "imageUrl": "{{ imageURL }}",
            "audioUrl": "",
            "timestamp": "2024-11-13T08:08:42.289242Z"
        },
        {
            "hotel_id": "1",
            "admin_id": null,
            "customer_id": 1,
            "is_read": true,
            "message": "",
            "imageUrl": "",
            "audioUrl": "{{ audioUrl }}",
            "timestamp": "2024-11-13T08:09:13.863783Z"
        },
        ...
    ]
}
```

### Start Chat
#### URL
`POST /api/start-chat`
#### Description
Start chat message to the hotel.
#### Headers
- `Authorization`: Bearer Token
#### Request Parameters
- `hotel_id`: (integer) Hotel ID.
#### Response
```json
{
    "success": true,
    "message": "Start Chat successfully."
}
```


### Send Chat Message
#### URL
`POST /api/send-message`
#### Description
Send a chat message to the hotel.
#### Headers
- `Authorization`: Bearer Token
#### Request Parameters
- `hotel_id`: (integer) Hotel ID.
- `message`: (string) Chat message.
#### Response
```json
{
    "success": true,
    "message": "Message sent successfully."
}
```

### Send Image
#### URL
`POST /api/send-image`
#### Description
Send a chat image to the hotel.
#### Headers
- `Authorization`: Bearer Token
#### Request Parameters
- `hotel_id`: (integer) Hotel ID.
- `image`: (file) Image file.
#### Response
```json
{
    "success": true,
    "message": "Image sent successfully."
}
```

### Send Multiple Image
#### URL
`POST /api/send-multiple-image`
#### Description
Send a multiple image to the hotel.
#### Headers
- `Authorization`: Bearer Token
#### Request Parameters
- `hotel_id`: (integer) Hotel ID.
- `images`: (array) Image file array.
#### Response
```json
{
    "success": true,
    "message": "Images sent successfully."
}
```

### Send Voice
#### URL
`POST /api/send-voice`
#### Description
Send a multiple image to the hotel.
#### Headers
- `Authorization`: Bearer Token
#### Request Parameters
- `hotel_id`: (integer) Hotel ID.
- `voice`: (file) Voice file.
#### Response
```json
{
    "success": true,
    "message": "Voice sent successfully."
}
```

### Read Message
#### URL
`POST /api/read-message/{hotel_id}`
#### Description
Read message for hotel chat.
#### Headers
- `Authorization`: Bearer Token
#### Response
```json
{
    "success": true,
    "message": "Read message successfully."
}
```

## Delete Account
#### URL
`DELETE /api/delete-account`
#### Description
Delete the authenticated customer's account.
#### Headers
- `Authorization`: Bearer Token
#### Response
```json
{
    "success": true,
    "message": "Account deleted successfully",
}
```













    









