# Ventures
Ventures is a 4 person group project for Module 4 at the [Turing School of Software & Design](https://turing.io/). It is a cross-pollination project with two students from the [Front-End Engineering Program](https://turing.io/programs/front-end-engineering/) and two students from the [Back-End Engineering Program](https://turing.io/programs/back-end-engineering/).The project specifications can be found [here](http://backend.turing.io/module4/projects/cross_pollination/cross_pollination_spec).

Ventures is an application to allow users to browse outdoor festivals and events. You can browse through a variety of climbing, mountain biking, hiking, running, and white water rafting events all throughout the US. Each card gives more details including the start/end dates, a link to the events website, an accompanying photo and YouTube video, as well as buttons for the you to add that event to your ‘wishlist’ or ‘attending’ lists. Your profile page allows you to edit your user name and personal bio as well as view events filtered by upcoming events, wish-listed events, and past events you’ve attended. Ventures is here to help you find the right events for you!

The link to the Ventures deployed frontend can be found [here](https://ventures-fe.herokuapp.com) along with the [github repo](https://github.com/whitneyburton/ventures-fe). The link to the deployed Ventures Backend API can be found [here](https://ventures-be.herokuapp.com/api/v1/events) along with the [github repo](https://github.com/mgoodhart5/ventures-be). We used waffle.io for our [agile board](https://waffle.io/whitneyburton/ventures-fe).

## Ventures Backend
The Ventures backend API was created with Ruby on Rails. It is a [json:api](https://jsonapi.org/) compliant versioned API which we implemented using [Fast JSON:API](https://github.com/Netflix/fast_jsonapi). This is [deployed](https://ventures-be.herokuapp.com/api/v1/events) on Heroku using a Docker image. Continuous integration was implemented using [CircleCI](https://circleci.com/gh/mgoodhart5/ventures-be).

## Contributors
#### Backend
**[Anna Smolentzov](https://github.com/asmolentzov)**

**[Mary Goodhart](https://github.com/mgoodhart5)**

#### Frontend
**[Whitney Burton](https://github.com/whitneyburton)**

**[Karin Ohman](https://github.com/kaohman)**

## Endpoints
### Events
#### `GET /api/v1/events`
Returns all the events in the system.
#### Optional Parameters for Filtering
One or multiple of the following parameters can be added to endpoint to filter which events are returned.

If no parameters are specified, all events are returned.

`event_type`

`state`

`month`

Example:
`GET /api/v1/events?event_type=running&month=6`
#### Returned Data Format
```
{
  "data": [
    {
      "id": "1",
      "type": "event",
      "attributes": {
      "name": "Shelf Road Craggin' Classic",
      "city": "Canon Springs",
      "state": "CO",
      "event_type": "climbing",
      "price": 35,
      "start_date": "10-19-2018",
      "end_date": "10-21-2018",
      "description": "This October 19-21, head on down to the best limestone sport cragging Colorado has to offer, and with the American Alpine Club and CAMP USA, and be treated to a weekend of climbing, community, clinics, contests, beer, slideshows, films, giveaways, stewardship and fun.",
      "event_url": "https://americanalpineclub.org/shelf-road-cc",
      "image_url": "https://static1.squarespace.com/static/55830fd9e4b0ec758c892f81/57bc7284f7e0abe0efbb523e/59417dc21b631bad37b19a74/1497464437416/_MG_1604.jpg",
      "video_url": "https://www.youtube.com/embed/Cnjv_Brs2Bo"
      }
    },
    {
      "id": "2",
      "type": "event",
      "attributes": {
      "name": "Crested Butte Bike Week",
      "city": "Crested Butte",
      "state": "CO",
      "event_type": "biking",
      "price": 0,
      "start_date": "06-27-2019",
      "end_date": "06-30-2019",
      "description": "Bike week is a multi-day celebration of all things mountain bike in the Gunnison Valley. We still have the big thigh burner of a singletrack race, the Fat Tire 40, but now CB Bike Week is more of a celebration of how mountain biking defines our community in the summer. Join us for clinics, a film festival, the Chainless Downhill World Championships, good beer, and a great party.",
      "event_url": "http://www.cbchamber.com/chamberevents/cb-bike-week/",
      "image_url": "https://travelcrestedbutte.com/wp-content/uploads/bike-week-feature.jpg",
      "video_url": "https://www.youtube.com/embed/0cFSZCDMP_U"
      }
    }
  ]
}
```

#### `GET /api/v1/events/:id`
Returns a single event.
#### Returned Data Format
```
{
  "data": {
  "id": "5",
  "type": "event",
  "attributes": {
    "name": "Fjallraven US Classic",
    "city": "Leadville",
    "state": "CO",
    "event_type": "hiking",
    "price": 299,
    "start_date": "08-27-2019",
    "end_date": "08-30-2019",
    "description": "The Classic trekking series embodies Fjällräven’s spirit. The communal trek is all about spending time in nature with a crew of like-minded people, creating lasting memories on the trail and sharing stories around the campfire. We get excited to introduce fans of Fjallraven to the Swedish trekking tradition in our beautiful backyard.",
    "event_url": "https://classic.fjallraven.com/usa/classic-usa/about-classic-usa/",
    "image_url": "https://www.outsideonline.com/sites/default/files/styles/full-page/public/2016/08/26/fjallraven-classic_h.jpg?itok=-kiFQlnk",
    "video_url": "https://www.youtube.com/embed/lfy1c72XFgQ"
    }
  }
}
```

### Users
#### `GET /api/v1/users/:id`
Returns a single user.
#### Returned Data Format
```
{
  "data": {
    "id": "1",
    "type": "user",
    "attributes": {
      "name": "Wonder Woman",
      "email": "wonderful@gmail.com",
      "image_url": "https://images.unsplash.com/photo-1536626420752-b144a129fde9?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=668&q=80",
      "bio": "Diana is the daughter of Queen Hippolyta, the first child born on Paradise Island in the three thousand year history that the immortal Amazons lived there. The Amazons had been created around 1200 B.C. when the Greek goddesses drew forth the souls of all women who had been murdered by men and placed them on the island."
    }
  }
}
```

#### `PUT /api/v1/users/:id`
Edits any one attribute for a user or any attributes combined except for image_url.

Returns a 200 status.

Returns the user with updated attributes.

This can be done as parameters or as a body.
#### Parameters
`name=New Name`

`bio=New Bio`

`email=New Email`

Example:
`PUT /api/v1/users/:id?name=New Name&email=newemail@gmail.com`
#### Body
Example:
`{ "email": "diana@gmail.com" }`
#### Returned Data Format
```
{
    "data": {
        "id": "2",
        "type": "user",
        "attributes": {
            "name": "Wonder Woman",
            "email": "wonderful@gmail.com",
            "image_url": "https://images.unsplash.com/photo-1536626420752-b144a129fde9?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=668&q=80",
            "bio": "Diana is the daughter of Queen Hippolyta, the first child born on Paradise Island in the three thousand year history that the immortal Amazons lived there. The Amazons had been created around 1200 B.C. when the Greek goddesses drew forth the souls of all women who had been murdered by men and placed them on the island."
        }
    }
}
```

### User Events
#### `GET /api/v1/users/:id/events`
Returns all of the events for the specified user. Returns all event attributes along with the status for that user_event.
#### Returned Data Format
```
{
    "data": [
        {
            "id": "18",
            "type": "my_event",
            "attributes": {
                "name": "Shelf Road Craggin' Classic",
                "city": "Canon Springs",
                "state": "CO",
                "event_type": "climbing",
                "price": 35,
                "start_date": "10-19-2018",
                "end_date": "10-21-2018",
                "description": "This October 19-21, head on down to the best limestone sport cragging Colorado has to offer, and with the American Alpine Club and CAMP USA, and be treated to a weekend of climbing, community, clinics, contests, beer, slideshows, films, giveaways, stewardship and fun.",
                "event_url": "https://americanalpineclub.org/shelf-road-cc",
                "image_url": "https://static1.squarespace.com/static/55830fd9e4b0ec758c892f81/57bc7284f7e0abe0efbb523e/59417dc21b631bad37b19a74/1497464437416/_MG_1604.jpg",
                "video_url": "https://www.youtube.com/embed/Cnjv_Brs2Bo",
                "status": "past"
            }
        },
        {
            "id": "22",
            "type": "my_event",
            "attributes": {
                "name": "Fjallraven US Classic",
                "city": "Leadville",
                "state": "CO",
                "event_type": "hiking",
                "price": 299,
                "start_date": "08-27-2019",
                "end_date": "08-30-2019",
                "description": "The Classic trekking series embodies Fjällräven’s spirit. The communal trek is all about spending time in nature with a crew of like-minded people, creating lasting memories on the trail and sharing stories around the campfire. We get excited to introduce fans of Fjallraven to the Swedish trekking tradition in our beautiful backyard.",
                "event_url": "https://classic.fjallraven.com/usa/classic-usa/about-classic-usa/",
                "image_url": "https://www.outsideonline.com/sites/default/files/styles/full-page/public/2016/08/26/fjallraven-classic_h.jpg?itok=-kiFQlnk",
                "video_url": "https://www.youtube.com/embed/lfy1c72XFgQ",
                "status": "wishlist"
            }
        }
    ]
}
```

#### `POST /api/v1/users/:id/events/:event_id`
Creates a new user_event for the specified user and event.

Returns a 201 status.

Returns the event that the user_event refers to, along with the status. The default status is `wishlist` if no optional parameter is passed.
#### Optional Parameter
`status`
Options:
  - `attending`
  - `wishlist` - this is the default

Example:
`POST /api/v1/users/:id/events/:event_id?status=attending`
#### Returned Data Format
```
{
    "data": {
        "id": "10",
        "type": "my_event",
        "attributes": {
            "name": "International Climbers' Festival",
            "city": "Lander",
            "state": "WY",
            "event_type": "climbing",
            "price": 120,
            "start_date": "07-10-2019",
            "end_date": "07-14-2019",
            "description": "COME CELEBRATE THE CLIMBING LIFESTYLE! WITH COMPETITIONS, ART, FOOD, MUSIC, BEER, AND SO MUCH MORE, IT'S SURE TO BE A PARTY.",
            "event_url": "https://www.climbersfestival.org/#welcome",
            "image_url": "https://static1.squarespace.com/static/52d067f7e4b0309df5e103de/t/52fab709e4b08ba35fbe1207/1392162571068/serivice+project.jpg",
            "video_url": "https://www.youtube.com/embed/w9qQhpt7Ggs",
            "status": "wishlist"
        }
    }
}
```

#### `PUT /api/v1/users/:id/events/:event_id`
Updates a user_event specified by the user ID and event ID. Updates the status of the event.

Returns a 200 status.

Returns the event with the updated status of the associated user_event.

This can be done as parameters or as a body.
#### Parameters
`status=wishlist`

Options for the status are `wishlist`, `attending`, and `past`.

Example:
`PUT /api/v1/users/:id/events/:event_id?status=attending`
#### Body
Example:
`{ "status": "attending" }`
#### Returned Data Format
```
{
    "data": {
        "id": "20",
        "type": "my_event",
        "attributes": {
            "name": "Crested Butte Bike Week",
            "city": "Crested Butte",
            "state": "CO",
            "event_type": "biking",
            "price": 0,
            "start_date": "06-27-2019",
            "end_date": "06-30-2019",
            "description": "Bike week is a multi-day celebration of all things mountain bike in the Gunnison Valley. We still have the big thigh burner of a singletrack race, the Fat Tire 40, but now CB Bike Week is more of a celebration of how mountain biking defines our community in the summer. Join us for clinics, a film festival, the Chainless Downhill World Championships, good beer, and a great party.",
            "event_url": "http://www.cbchamber.com/chamberevents/cb-bike-week/",
            "image_url": "https://images.unsplash.com/photo-1544191696-102dbdaeeaa0?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2850&q=80",
            "video_url": "https://www.youtube.com/embed/0cFSZCDMP_U",
            "status": "attending"
        }
    }
}
```

#### `DELETE /api/v1/users/:id/events/:event_id`
Deletes a user_event specified by the user ID and event ID.

Returns a 204 status.

Does not return any data.

____

## Local Installation and Setup

This app is containerized with Docker.
- Follow [these](https://www.docker.com/get-started) instructions to download and set up Docker on your local machine.
- Clone this repo `git clone https://github.com/mgoodhart5/ventures-be`
- Type these commands in the terminal to build and set up your local environment:
  - To build the docker image:
```
docker-compose build
```
  - To setup environment variables:
```
docker-compose run web bundle exec figaro install
```
  - This will create an `application.yml` file in the `config` directory.
  - Open this file and type `PGUSER: postgres` at the bottom of the file, then save and close the file.

  - To setup the database:
```
docker-compose run web rake db:{create,migrate,seed}
```
  - To run your local environment:
```
docker-compose up
```
  - To gracefully shut down the local environment, in a separate terminal window type:
```
docker-compose down
```

### Notes
- To run standard `rails` commands in this environment, they **must** be prefaced with
```
docker-compose run web <your command here>
```
- To install and run the frontend of this application locally, please refer to the instructions located in the [frontend repo](https://github.com/whitneyburton/ventures-fe) for this app.


## Running Tests
This repo is fully tested using RSpec. To run the tests locally, run the following command:
```
docker-compose run web rspec
```
Green is passing, red is failing.

## Backend Built With: Technologies and Versions
* [Ruby 2.4.5](https://ruby-doc.org/core-2.4.5/)
* [Rails 5.2.2](https://guides.rubyonrails.org/)
* [Fast JSON:API](https://github.com/Netflix/fast_jsonapi)
* [Heroku](https://www.heroku.com/)
* [RSpec](http://rspec.info/)
* [Docker Compose](https://docs.docker.com/compose/)
* [Postgres](https://www.postgresql.org/)
