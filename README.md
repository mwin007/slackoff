# SlackOff

![SlackOff Main Application](/docs/screenshots/slackoff-main.jpg)

SlackOff is a clone of a popular chat client, Slack.

Live Site: [http://slackoff.today]

## Implementation

SlackOff utilizes the following:

- Ruby on Rails
- React.js
- Redux
- PostgreSQL
- jQuery
- Heroku
- BCrypt
- Figaro
- jBuilder
- react-modal
- react-alert

## Features

The chat application is composed of three main features:

### Authentication

BCrypt gem is utilized in order to hash a password, and only the digest of the user is saved into the database.  A cookie storing a BCrypt token is used to keep track of the user's current session.  Without a valid matching session token, the user is redirected to the login page.  

### Live Chat

Pusher API is utilized for maintaining a Websocket TCP-based protocol connection which allows bi-directional communication between the server and the client.  

![Chat View](/docs/screenshots/chat.png)

```javascript
this.pusher = new Pusher('// API KEY //', {
  encrypted: true
});

const channelId = this.props.user.currentChannel.toString();
this.channel = this.pusher.subscribe(channelId);

this.channel.bind('message', (message) => {
  this.props.receiveMessage(message);
}, this);

this.channel.bind('editMessage', (data) => {
  this.props.editMessage(data.message);
}, this);

this.channel.bind('deleteMessage', (data) => {
  this.props.removeMessage(data.id);
}, this);
```

When a user accesses the main application page, the client is subscribed to the Pusher channel.  From this channel, the client receives a specified event such as `message`, `editMessage` and `deleteMessage`.  The message event triggers the `receiveMessage` action which updates the application's Redux store through the reducer.  Once the store updates, React re-renders the chat view through the utilization of the virtual DOM.

### Channels

![Channel View](/docs/screenshots/channels.png)

Public channels can be created/joined/subscribed by all users on the application.

![Channel Browse View](/docs/screenshots/channels-browse.png)

### Direct/Team Messaging

![Direct Message View](/docs/screenshots/direct-message.png)

Direct and Team messaging capability is implemented through creation of private channels.

![Direct Message View](/docs/screenshots/dm-users.png)

![Direct Message View](/docs/screenshots/dm-example.png)

## Design

![Wireframe](docs/wireframes/slackoff-wireframe-main-app.jpg)


## Future Release

* [ ] Notification
* [ ] Avatar Upload
* [ ] Search
* [ ] Emoticons
