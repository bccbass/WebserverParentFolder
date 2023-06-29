# PersonnelAPI Endpoint Documentation

All endpoints require an account and for the user to be logged in with an active JWT token. The token has an expiration 30 days after creation, logging in again will grant a fresh new token. At this point most of the public functionality of the API is read only, with creation, updating and deletion of resources reserved for users with admin credentials.

## Index:
1. [Authentication](#Authentication)
1. [Album](#Album)
1. [Artist](#Artist)
1. [Track](#Track)
1. [Musician](#Musician)
1. [Credit (track_musician)](#Credit-(track_musician))
1. [Instrument](#Instrument)

## Authentication

Authentication routes cover the concerns of Users, inlcuding logging in and admin credentials. 

### **POST** `/users/register`
Create a new new user so you can interact with the API
- Methods: **POST**
- parameters: None
- Headers: None
- Response: _201_

### **POST** `/users/login`
Log in to your account so you can access a token to interact with the API
- Methods: **POST**
- parameters: None
- Headers: None
- Response: _200_

### **POST** `/grant_admin_access/{user_id}`
Admins are allowed to grant admin access to users.  
*Admin credentials required.*

- Methods: **POST**
- parameters: 
  - **user_id**: `Integer` _Required_  
     The id of the user you are attempting to grant admin access to.
- Headers: Authorization: {Bearer Token}
- Response: _202_
- Response: _404_

### **GET** `/users`
Retrieves a list of all users in the database.  
*Admin credentials required.*

- Methods: **GET**
- parameters: None
- Headers: Authorization: {Bearer Token}
- Response: _200_
- Response: _404_

<hr>
## Album

Albums are releases forming a collection tracks by a given artist. 

### **GET** `/albums`

Retrieves a list of all albums in the database.

- Methods: **GET**
- parameters: None
- Headers: Authorization: {Bearer Token}
- Response: _200_

### **GET** `/albums/{album_id}`

Retrieves a single album from the database.

- Methods: **GET**
- Parameters:
  - **album_id**: `Integer` _Required_  
     The id of the album you are attempting to access.
- Headers: Authorization: {Bearer Token}
- Response: _200_
- Response: _404_


### **POST** `/albums`

Creates a new album record and adds to the database.  
*Admin credentials required.*

- Methods: **POST**
- Parameters: None
- Headers: Authorization: {Bearer Token}
- Response: _201_
- Response: _401_


### **PUT/PATCH** `/albums/{album_id}`

Update an album from the database.  
*Admin credentials required.*

- Methods: **PUT/PATCH**
- Parameters: 
  - **album_id**: `Integer` _Required_  
     The id of the album you are attempting to update.
- Headers: Authorization: {Bearer Token}
- Response: _201_
- Response: _401_, _404_


### DELETE `/albums/{album_id}`

Deletes an album from the database.  
*Admin credentials required.*

- Methods: DELETE
- Parameters: 
  - **album_id**: `Integer` _Required_  
     The id of the album you are attempting to delete.
- Headers: Authorization: {Bearer Token}
- Response: _200_
- Response: _401_, _404_
<hr>


## Artist

Artists represent either the person or group name an album is released by.

### **GET** `/artists`

Retrieves a list of all artists in the database.

- Methods: **GET**
- parameters: None
- Headers: Authorization: {Bearer Token}
- Response: _200_

### **GET** `/artists/{artist_id}`

Retrieves a single artist from the database.

- Methods: **GET**
- Parameters:
  - **artist_id**: `Integer` _Required_  
     The id of the artist you are attempting to access.
- Headers: Authorization: {Bearer Token}
- Response: _200_
- Response: _404_


### **POST** `/artists`

Creates a new artist record and adds to the database.  
*Admin credentials required.*

- Methods: **POST**
- Parameters: None
- Headers: Authorization: {Bearer Token}
- Response: _201_
- Response: _401_


### **PUT/PATCH** `/artists/{artist_id}`

Update an artist from the database.  
*Admin credentials required.*

- Methods: **PUT/PATCH**
- Parameters: 
  - **artist_id**: `Integer` _Required_  
     The id of the artist you are attempting to update.
- Headers: Authorization: {Bearer Token}
- Response: _201_
- Response: _401_, _404_


### DELETE `/artists/{artist_id}`

Deletes an artist from the database.  
*Admin credentials required.*

- Methods: DELETE
- Parameters: 
  - **artist_id**: `Integer` _Required_  
     The id of the artist you are attempting to delete.
- Headers: Authorization: {Bearer Token}
- Response: _200_
- Response: _401_, _404_

<hr>


## Track

Tracks represent individual songs, and may or may not be associated with an album. It is completely permissible for them to exist as their own entities, and they can be updated at a later date to asssociate them with an album release. 

### **GET** `/tracks/{track_id}`

Retrieves a single track from the database.

- Methods: **GET**
- Parameters:
  - **track_id**: `Integer` _Required_  
     The id of the track you are attempting to access.
- Headers: Authorization: {Bearer Token}
- Response: _200_
- Response: _404_

### **POST** `/tracks`

Creates a new track record and adds it to the database.  
*Admin credentials required.*

- Methods: **POST**
- Parameters: None
- Headers: Authorization: {Bearer Token}
- Response: _201_
- Response: _401_


### **PUT/PATCH** `/tracks/{track_id}`

Update an track from the database.  
*Admin credentials required.*

- Methods: **PUT/PATCH**
- Parameters: 
  - **track_id**: `Integer` _Required_  
     The id of the track you are attempting to update.
- Headers: Authorization: {Bearer Token}
- Response: _201_
- Response: _401_, _404_


### DELETE `/tracks/{track_id}`

Deletes a track from the database.  
*Admin credentials required.*

- Methods: DELETE
- Parameters: 
  - **track_id**: `Integer` _Required_  
     The id of the track you are attempting to delete.
- Headers: Authorization: {Bearer Token}
- Response: _200_
- Response: _401_, _404_

<hr>


## Musician

Musicians represent the individual contributors of an album. For example, if The Beach Boys represent the Artist, the musicians would be all the members of the wrecking crew who performed on the songs. 

### **GET** `/musicians/{musician_id}`

Retrieves a single musician from the database.

- Methods: **GET**
- Parameters:
  - **musician_id**: `Integer` _Required_  
     The id of the musician you are attempting to access.
- Headers: Authorization: {Bearer Token}
- Response: _200_
- Response: _404_

### **POST** `/musicians`

Creates a new musician record and adds it to the database.  
*Admin credentials required.*

- Methods: **POST**
- Parameters: None
- Headers: Authorization: {Bearer Token}
- Response: _201_
- Response: _401_


### **PUT/PATCH** `/musicians/{musician_id}`

Update an musician from the database.  
*Admin credentials required.*

- Methods: **PUT/PATCH**
- Parameters: 
  - **musician_id**: `Integer` _Required_  
     The id of the musician you are attempting to update.
- Headers: Authorization: {Bearer Token}
- Response: _201_
- Response: _401_, _404_


### DELETE `/musicians/{musician_id}`

Deletes a musician from the database.  
*Admin credentials required.*

- Methods: DELETE
- Parameters: 
  - **musician_id**: `Integer` _Required_  
     The id of the musician you are attempting to delete.
- Headers: Authorization: {Bearer Token}
- Response: _200_
- Response: _401_, _404_

<hr>


## Credit (track_musician)

Credits represents the association between musicians and tracks. They are simple join records so the only provided routes are creation and deletion. 


### **POST** `/credit`

Creates a new track_musician association and adds it to the database.  
*Admin credentials required.*

- Methods: **POST**
- Parameters: None
- Headers: Authorization: {Bearer Token}
- Response: _201_
- Response: _401_

### **DELETE** `/credit/{credit_id}` optional locate with query paramaters: **DELETE** `/credit/0/track_id={integer}&musician_id={integer}`

Creates a new track record and adds it to the database.  
*Admin credentials required.*

- Methods: **POST**
- Parameters: 
  - **credit_id**: `Integer` _Required_  
     The id of the musician you are attempting to delete.
  - if **credit_id** is set to `0` query paramaters can be used to locate and delete credit instead of credit_id:
    - `{musician_id}`: integer ID representing the musician to locate
    - `{track_id}`: integer ID representing the track to locate
    - example url: `/credit/0/track_id={integer}&musician_id={integer}`
- Headers: Authorization: {Bearer Token}
- Response: _200_
- Response: _401_, _404_

<hr>


## Instrument

The Instruments table is a collection of availabe instruments to be associated with musicians. It is meant to be a static collection so the routes are limited and only include an indexed list of all available instruments with their corresponding IDs.

### **GET** `/instruments`

Retrieves a list of all instruments in the database.

- Methods: **GET**
- parameters: None
- Headers: Authorization: {Bearer Token}
- Response: _200_  

<hr>