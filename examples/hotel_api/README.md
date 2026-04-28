# Locky Reservation API

We have made it as easy as possible to integrate third parties to our cloud access control system. If you are aiming to get an ACCESS code for the lock and remove it, then you basically need only two end-points.

## Authentication
We provide you with a JSON Webtoken that will be valid for 10 years, and can be invalidated when the application is deactivated in the locky web interface. All you need to do is to add the json webtoken to the header.

## Endpoints
Server 1 : https://locky.server1.thundertech.no
Server 2 : https://locky.server2.thundertech.no

## Create a reservation
Simply post the reservation to the rest interface: /locky/hotel/booking

    # Header params:
    'accept: application/json'
    'jwt: you_secret_jwt'
    'Content-Type: application/json'
     
    # Payload
    {
	  "roomId": "we_provide_you_with_the_room_id",
	  "guestName": "Henrik Test",
	  "guestEmail": "kai@yalidian.com",
	  "phonePrefix": "47",
	  "phoneNumber": "48311484",
	  "start": "2025-07-10T15:00:00.000Z",
	  "end" : null
	  "comment": "string",
	  "type": "booking",
	  "bookingId": "686f6f73911765443a6b36a7",
	  "checkedIn" : true
	}

Note:
 - bookingId => your reservation id, can be used when you send delete request below.
 - checkedIn => can be set to true or false. 
 - end => Can be set and activated automatically checkout, but normally its better you handle deletion of the event upon checkout, contract end or pausing.
 - start => Can be todays date or in the future, if automatically checkin is activated the code given will start working at that time.

### Return response
The request will return a HotelBooking that also have a code field.

Thats all you need to do to generate an valid access with an access code.

## Delete reservation

We offer a delete request to delete reservations, simply send headers and to the following address.

    # Headers
    'accept: application/json'
    'jwt: you_secret_jwt'
    'Content-Type: application/json'
    
    #Request
    Deleterequest to /locky/booking/{bookingId} 

## Extra notes 
Make sure to add / remove reservations upon checkin, checkout, undo checkout, undo checkin. If you need to change the reservation just simply call the create reservation with the same bookingid.
