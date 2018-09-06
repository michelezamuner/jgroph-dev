# Ideas

Below are gathered ideas for the project that are too broad or too many to be picked up immediately in the first iteration, or that might not be implemented at all in the future.


## Actors

By looking at the project as a whole, the following proposals of actors have been produced.


### User (primary)

This would be the regular user of the application, whose purpose is to manage a collection of bookmarks, which means to retrieve them (in order to follow them and ultimately display the desired resource from its original source), update their meta data or delete them.


### Administrator (primary)

The Administrator will have special access to the application, which is not granted to regular managers, in order to be able to change configuration parameters, or perform other administrative tasks that impact the functioning of the application itself, rather than its data.


### Archiver (primary)

This actor represents any device which has an interest to handle some of all bookmarks data as archives, for example to download a set of data, or to upload one, in batch, rather than working with single bookmarks, like a User would do.


### Message Sender (primary)

In case the application is deployed within an event-driven system, other systems that want to communicate with this application would send messages to it, and as such they'd be regarded as Message Senders.


### Storage (secondary)

The Storage system persisting bookmarks data used by the application.


### Notification Subscriber (secondary)

The application will send notifications upon occurrence of certain events to subscribed parties, which are regarded as Notification Subscribers.


### Feed (secondary)

The application might be configured to automatically fetch bookmarks data from external sources in batch mode (much like the reverse of what is done with the Archivers). These external sources would be known as Feeds.


### Message Receiver (secondary)

In case the application is deployed within an event-driven system, Message Receivers are the other systems that receive messages from this application.


## Ports and adapters

The previous selection of actors can be translated in the following ports and adapters.


### Bookmarks (primary)

The Bookmarks port is the one used by Users, exposing the use cases related to that actor. Possible adapters could be the Web adapter when the User is a person, and the API adapter when the User is another system consuming a Web service.


### Administration (primary)

The Administration port would be used by the Administrator. A possible adapter could be the Web adapter, since Administrators are usually humans. It's not clear if it would make sense to use also an API adapter for this.


### Archive (primary)

The Archive port would be used by the Archiver. Possible adapter could be the Web adapter to support manual upload and download of data as archives, and the API adapter to support the same team, but done by a machine.


### Feed (secondary)

The Feed port would be using the Feed actors to get data from them, for example at pre-determined times. There are many adapter that can be supported here: a filesystem feed reading data from a file that is regularly updated by someone, an HTTP feed if data is stored on some external server, or a Torrent feed if the Torrent protocol is used to download data from a remote source.


### Message Input (primary)

The Message Input port is the one used to communicate with the application through messages, and is used by Message Senders. Possible adapters could be an HTTP adapter and an AMQP one.


### Message Output (secondary)

Much like the Message Input, the Message Output port is used to let the application communicate with Message Receivers by means of messages. Here as well HTTP and AMQP adapters are examples of what can be supported.


### Storage (secondary)

The Storage port is the one used by the application to communicate with the Storage actor, to store data persistently. Possible adapters could be a memory storage and a database storage.


### Notifications (secondary)

The Notifications port is used by the application to communicate with Notification Subscribers. Possible adapters could be email notifications and push notifications (like WebSockets).
