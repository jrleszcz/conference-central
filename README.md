A cloud-based API backend server for a Conference organization application. Built in Google App Engine and designed to be platform agnostic. 

The API supports user authentication, user profiles, conference information, registration, and a number of ways in which to query the data. 

## Design

### Conferences
Conference objects are children of a specific user and only that user may edit the conference. 

Conference objects have a `maxAttendees` property and a `seatsAvailable` count which decrements as attendees register for the Conference. 

The remaining attributes are: description, topics, city, startDate, endDate, and month. All of these attributes may be used to query for and filter conferences. 

### Sessions
Session objects are children of conference objects and can be created by the organizer of the conference. 

Speakers at sessions should be registered users with a Profile just like attendees, so  `Session.speaker` simply points to a user_id (via the `speakerUserId` attribute). Just like Conferences, Sessions have a `maxAttendees` property and a `seatsAvailable` count.

### Profile
Conference attendees, speakers, and organizers are all register using the same Profile object. 
In addition to the descriptive properties of `displayName`, `mainEmail`, and `teeShirtSize`, Profile objects have links to conferences and sessions: `conferenceKeysToAttend` and `sessionsKeysToAttend`.  Finally, there is a `sessionsKeysWishlist` which holds the id of sessions the user has added to their wishlist.


## Products
- [App Engine][1]

## Language
- [Python][2]

## APIs
- [Google Cloud Endpoints][3]

## Setup Instructions
1. Update the value of `application` in `app.yaml` to the app ID you
   have registered in the App Engine admin console and would like to use to host
   your instance of this sample.
1. Update the values at the top of `settings.py` to
   reflect the respective client IDs you have registered in the
   [Developer Console][4].
1. Update the value of CLIENT_ID in `static/js/app.js` to the Web client ID
1. (Optional) Mark the configuration files as unchanged as follows:
   `$ git update-index --assume-unchanged app.yaml settings.py static/js/app.js`
1. Run the app with the devserver using `dev_appserver.py DIR`, and ensure it's running by visiting your local server's address (by default [localhost:8080][5].)
1. (Optional) Generate your client library(ies) with [the endpoints tool][6].
1. Deploy your application.


[1]: https://developers.google.com/appengine
[2]: http://python.org
[3]: https://developers.google.com/appengine/docs/python/endpoints/
[4]: https://console.developers.google.com/
[5]: https://localhost:8080/
[6]: https://developers.google.com/appengine/docs/python/endpoints/endpoints_tool
