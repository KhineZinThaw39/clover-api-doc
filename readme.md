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
  - [Get Chat Types](#get-chat-types)
  - [Get Chat Messages by Chat Type](#get-chat-messages-by-chat-type)
  - [Send Chat Message](#send-chat-message)
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
            "view_type": "Sea View",
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
        "view_type": "Sea View",
        "bed_type": "King",
        "room_type": "Deluxe",
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
            "name_mm": "Hotel A",
            "name_en": "Hotel A",
        },
        "room": {
            "id": 1,
            "name_mm": "Room A",
            "name_en": "Room A",
            "room_type": "Deluxe",
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
### Get Chat Types
#### URL
`GET /api/chat-types`
#### Description
Retrieve the authenticated customer's chat types.
#### Headers
- `Authorization`: Bearer Token
#### Response
```json
{
    "success": true,
    "message": "Chat types retrieved successfully",
    "data": [
        {
            "id": 1,
            "title_en": "How to take reservation?",
            "title_mm": "How to take reservation?",
        }, ...
    ]
}
```
### Get Chat Messages by Chat Type
#### URL
`GET /api/chat-messages/{chat_type_id}`
#### Description
Retrieve the authenticated customer's chat messages by hotel and chat type.
#### Headers
- `Authorization`: Bearer Token
#### Response
```json
{
    "success": true,
    "message": "Chat messages retrieved successfully",
    "data": [
        {
            "id": 1,
            "message": "Hello, how can I help you?",
            "created_at": "2023-09-12 10:30:00",
            "customer": {
                "id": 1,
                "name": "John Doe",
                "image": "img_url",
            },
            "hotel": {
                "id": 1,
                "name": "Hotel A",
            },
        }, ...
    ]
}
```

### Send Chat Message
#### URL
`POST /api/chat-messages`
#### Description
Send a chat message to the hotel.
#### Headers
- `Authorization`: Bearer Token
#### Request Parameters
- `hotel_id`: (integer) Hotel ID.
- `chat_type_id`: (integer) Chat type ID.
- `message`: (string) Chat message.
#### Response
```json
{
    "success": true,
    "message": "Chat message sent successfully",
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













    









